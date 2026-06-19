# Packaging and deployment

This page covers how to turn your class library into something you can install on a MIM server. [How the framework works](architecture-overview.md) explains the shim and worker that this page refers to.

## Build output

Your project is a class library, but when you publish it the framework produces three things to deploy:

* the **worker**, a self-contained executable (`Ecma2Host.exe` and its supporting files) that runs your provider code;
* the **shim**, a .NET Framework 4.8 assembly (`<YourAssembly>.Ecma2.dll`) that MIM loads; and
* the **Packaged MA manifest**, an XML file that registers your agent as a named management agent type in MIM (optional, see below).

## Build and publish

The framework produces two shapes of worker depending on how you compile.

`dotnet build` produces a framework-dependent worker. It is fast and small, and it is what you want while developing. It needs the matching .NET runtime present on the machine.

`dotnet publish` produces a self-contained worker, with the .NET runtime bundled in, so the target server needs no .NET installation. This is what you ship.

## Worker options

A few MSBuild properties in your project control how the worker is published. Set them in your `.csproj`:

```xml
<PropertyGroup>
  <!-- Bundle the .NET runtime into the worker so the MIM server needs no .NET install. -->
  <Ecma2WorkerSelfContained>true</Ecma2WorkerSelfContained>
  <!-- Pre-compile (ReadyToRun) the worker for a faster cold start. -->
  <Ecma2WorkerReadyToRun>true</Ecma2WorkerReadyToRun>
</PropertyGroup>
```

These apply when you publish, and only when the worker targets .NET (Core). The worker is always built for `win-x64`, which is the platform the Synchronization Service runs on. If your project targets .NET Framework, these properties do not apply, and the worker is published framework-dependent.

## Publishing

Publish your project as you would any .NET project. A publish profile keeps the settings with the project:

```
dotnet publish -p:PublishProfile=FolderProfile
```

The output is laid out like this:

```
<publish folder>\
├─ Ecma2Host.exe              the worker and its self-contained runtime
├─ ... (worker dependencies)
└─ ecma2\
   ├─ <YourAssembly>.Ecma2.dll                 the shim
   └─ <YourAssembly>.Ecma2.PackagedMA.xml      the manifest (if enabled)
```

The split matters at install time. The worker files are one set, and the `ecma2\` subfolder holds the two files that go into MIM's own folders.

## Packaged MA manifest

Emitting a manifest makes your agent appear as a named entry in MIM's "Create Management Agent" list, instead of a generic "load a DLL" connector. It is optional. Turn it on with a `Lithnet.Ecma2Framework.PackagedMa.props` file next to your project:

```xml
<Project>
  <PropertyGroup>
    <Ecma2GeneratePackagedMa>true</Ecma2GeneratePackagedMa>
    <!-- A stable GUID that identifies this management agent type. Generate it once and keep it. -->
    <Ecma2PackagedManagementAgentId>{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</Ecma2PackagedManagementAgentId>
    <Ecma2PackagedMaCompany>Your Company</Ecma2PackagedMaCompany>
    <Ecma2PackagedMaListName>Your Management Agent</Ecma2PackagedMaListName>
  </PropertyGroup>
</Project>
```

Keep the GUID stable across releases. It is how MIM recognises an upgraded version of the same agent rather than treating it as a new one.

## Building the installer

The framework gives you the files. Your installer puts them in the right places on the MIM server. An installer needs to do four things:

1. **Find the Synchronization Service install path.** Read it from the registry value `HKLM\SYSTEM\CurrentControlSet\services\FIMSynchronizationService\Parameters\Path`, using the 64-bit view. The paths below are relative to it.
2. **Install the shim.** Copy `<YourAssembly>.Ecma2.dll` into `<sync install>\Extensions\`. This is the assembly MIM loads.
3. **Install the worker.** Copy the worker files (everything in the publish folder except the `ecma2\` subfolder) into a program folder of your choosing, for example `%ProgramFiles%\<Your Company>\<Your Agent>\`.
4. **Install the manifest** (if you enabled it). Copy `<YourAssembly>.Ecma2.PackagedMA.xml` into `<sync install>\UIShell\XMLs\PackagedMAs\`.

The installer also has to write the registry value that tells the shim where the worker is:

```
HKEY_LOCAL_MACHINE\Software\Lithnet\Ecma2\<YourAssembly>.Ecma2
    WorkerPath = <full path to the installed Ecma2Host.exe>   (REG_SZ, 64-bit view)
```

The shim runs inside `miiserver.exe` and reads this value to find and start the worker. The sub-key name (`<YourAssembly>.Ecma2`) is the shim assembly's own name. Without this value the shim cannot start the worker, so make sure your installer writes it. During development you can instead set the `LITHNET_ECMA2_WORKER_EXE` environment variable to the worker's path, which takes precedence over the registry.

The install touches `miiserver.exe`'s folders and the machine registry, so the installer runs elevated, per-machine, as a 64-bit package.

The [Lithnet Okta Management Agent](https://github.com/lithnet/okta-managementagent) is a complete agent built on this framework. Its `Lithnet.Okta.ManagementAgent.Setup` project is an Advanced Installer project that does all four steps and writes the registry value, and is a good starting point to copy.

## Shim name

The shim is named `<YourAssembly>.Ecma2.dll` by default, and the registry sub-key and worker lookup use the same name. You can set it explicitly with the `Ecma2ManagementAgentName` property:

```xml
<PropertyGroup>
  <Ecma2ManagementAgentName>YourConnectorName</Ecma2ManagementAgentName>
</PropertyGroup>
```

MIM identifies an ECMA2 connector by the filename of the extension DLL recorded in the management agent's configuration. If you are replacing an existing connector and want a configured management agent to load the new shim without being recreated, set the name so the shim filename matches the one the existing agent already uses.

## Upgrades

If you ship updates as an upgrade rather than a side-by-side install, keep two things stable across versions so MIM and Windows treat the new build as an upgrade:

* the installer's upgrade code, so the new package replaces the old one; and
* the Packaged MA GUID, so the existing management agent and its configuration survive the upgrade instead of appearing as a new type.

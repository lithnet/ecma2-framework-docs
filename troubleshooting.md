# Troubleshooting

This page covers the problems you're most likely to hit when running a management agent built with version 3 of the framework. The [architecture overview](architecture-overview.md) describes the parts referred to below: the shim that MIM loads, the worker process it launches, and the registry value that links them.

## The management agent doesn't appear in MIM

If your agent isn't listed when you create a new management agent, the **Packaged MA manifest** is most likely missing or in the wrong place. Confirm the manifest XML was installed into the Synchronization Service's `UIShell\XMLs\PackagedMAs` folder, and restart the MIM Synchronization Service Manager so it re-reads that folder.

## A run step fails immediately, or the connection can't be opened

When MIM starts an operation, the shim has to launch the worker. If it can't, the operation fails right away. The usual cause is a missing or incorrect **worker path**.

The shim finds the worker by reading this registry value (64-bit view):

```
HKEY_LOCAL_MACHINE\Software\Lithnet\Ecma2\<YourAssembly>.Ecma2
    WorkerPath = <full path to Ecma2Host.exe>
```

Check that:

* the value exists under the sub-key named after your shim assembly (`<YourAssembly>.Ecma2`);
* it points at the `Ecma2Host.exe` that your installer actually deployed; and
* the file is present at that path.

If the value is missing, the shim raises an error that names both the registry key it looked for and the `LITHNET_ECMA2_WORKER_EXE` environment-variable override, so the MIM run-step error usually tells you exactly what wasn't configured. Your installer is responsible for writing this value; see [Packaging and deployment](packaging-and-deployment.md).

> **For development and testing**, you can set the `LITHNET_ECMA2_WORKER_EXE` environment variable to the full path of a worker you built locally. It takes precedence over the registry value, so you can point MIM at a fresh build without reinstalling.

## "Refresh interfaces" fails, or the agent won't load at all

If MIM can't load the shim when you refresh interfaces or open the agent, check the **Application event log** on the MIM server for the underlying error.

The shim is a small .NET Framework 4.8 assembly, so the server needs .NET Framework 4.8 installed (it is present on any supported MIM server). Unlike older versions of the framework, the shim has no third-party dependencies, so the DLL-conflict and embedded-assembly errors that affected in-process agents no longer apply.

## The worker starts but then fails

Because your provider runs in the worker process, errors in your own code surface there. The worker logs to the Windows event log and can be configured to log to a file. Start there when an import or export runs but produces unexpected results or per-object errors.

The worker is published self-contained, so it carries its own copy of the .NET runtime and the server does not need .NET installed. If you instead deployed a framework-dependent build (the output of `dotnet build` rather than `dotnet publish`), the worker will fail to start unless the matching runtime is installed. Always deploy the published, self-contained worker.

## The schema is empty or out of date

The Packaged MA manifest ships with a minimal placeholder schema so MIM can register the agent. Your agent's real schema comes from your `ISchemaProvider` at run time. If MIM is showing an empty or stale schema, run a schema refresh on the management agent so MIM asks your provider for the current schema.

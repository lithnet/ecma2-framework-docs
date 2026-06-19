# How the framework works

You don't need to read this to build a management agent. It explains what the framework does when you build and run an agent, which helps when you are deploying or troubleshooting.

## Background

MIM loads every Extensible Connectivity (ECMA2) management agent into a single process, `miiserver.exe`, and all agents share one `Extensions` folder. This causes two problems.

`miiserver.exe` is a .NET Framework process and can load only one version of any assembly. If two agents need different versions of the same library, such as `Newtonsoft.Json` or `System.Text.Json`, they conflict. The failure usually appears as a type-load error when MIM inspects the agent, and it becomes more likely as you add agents.

An in-process agent also has to target .NET Framework, because that is what the host uses. Some client libraries are only published for .NET (Core), so an in-process agent either cannot use them or has to stay on an older version that still supports .NET Framework.

Earlier versions of the framework reduced the conflict problem by embedding an agent's dependencies into a single DLL using Costura.Fody. It helped, but it was unreliable, and it did nothing about the framework target.

## Architecture

Version 3 runs your agent's code in a separate process from `miiserver.exe`. Your providers run with their own copy of the .NET runtime and their own dependencies, and nothing is shared with MIM or with other agents.

```
  miiserver.exe (.NET Framework)             Worker process (.NET)
  ┌──────────────────────────┐               ┌──────────────────────────┐
  │  shim (net48)            │  named pipe   │  your providers,         │
  │  MIM IMAExtensible2 API  │ ◄───────────► │  dependencies, runtime   │
  └──────────────────────────┘   JSON-RPC    └───────────┬──────────────┘
                                                         │
                                                         ▼
                                                target system (e.g. Okta)
```

There are two parts, both produced by the framework when you build.

### The shim

The shim is a small .NET Framework 4.8 assembly, and it is the only thing MIM loads into `miiserver.exe`. It implements the management agent interfaces MIM calls, such as `IMAExtensible2CallImport`, `IMAExtensible2CallExport`, and the password interfaces. It contains no provider logic and no third-party dependencies, so it cannot conflict with other agents. Its job is to start the worker and forward calls to it.

### The worker

The worker is a separate executable that holds your provider code, its dependencies, and its own copy of the .NET runtime. Your import, export, password, and schema logic runs here.

### Communication

The shim and the worker communicate over a local named pipe using JSON-RPC. When MIM calls the shim to run an operation, the shim sends the request to the worker, the worker runs your provider, and the results come back over the pipe. The MIM types, such as `CSEntryChange` and `Schema`, are passed across in both directions, so your provider works with the same objects it always has.

The worker runs under the same identity as the Synchronization Service, and the pipe is local to the machine, so the channel is only reachable by that account and never leaves the server.

## The management agent project

You write a class library. You implement the providers you need (schema, capabilities, import, export, password) and a startup class that registers them. You do not implement MIM's `IMAExtensible2` interfaces.

When you build, the framework runs a source generator that reads your `IEcmaStartup` class and your providers, and writes the worker's entry point and configuration code. It then compiles the worker and the shim, and produces the Packaged MA manifest.

The source generator reads your library's public types to find your code, so your startup class and your configuration option classes must be `public`.

Your library can target .NET Framework or .NET. Targeting .NET lets you use libraries that are not published for .NET Framework.

## The NuGet package

You reference one package, `Lithnet.Ecma2Framework`. It provides the interfaces and attributes you write against, and the build tooling that produces the worker and the shim.

## The Packaged MA manifest

You normally create an ECMA2 agent in MIM by selecting a DLL. A Packaged MA registers your agent as a named management agent type instead, so it appears by name in the list when an operator creates a management agent. The framework produces the manifest when you build, and the installer places it in MIM's `UIShell\XMLs\PackagedMAs` folder.

## Deployment

When you install an agent (see [Packaging and deployment](packaging-and-deployment.md)), the build outputs go to three places:

* the shim goes into MIM's `Extensions` folder,
* the worker goes into its own folder, and
* the manifest goes into MIM's `UIShell\XMLs\PackagedMAs` folder.

A registry value records the worker's location so the shim, running inside `miiserver.exe`, knows which executable to start.

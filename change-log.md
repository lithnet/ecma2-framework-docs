# v3.0
A re-architecture: management agents now run out of process. Your provider code runs in a self-contained worker that the Synchronization Service launches through a small .NET Framework shim, communicating over a local named pipe. This removes the dependency conflicts of the shared `Extensions` folder, and lets you target .NET (Core) rather than being limited to .NET Framework. See [How the framework works](architecture-overview.md).

Notable changes for management agent authors:
- Your project is now a class library. It can target .NET Framework or .NET.
- Your `IEcmaStartup` class and any configuration option classes must be `public`. The framework finds them by reading your library's public types.
- The single-file-assembly (Costura) approach is no longer needed or supported. Out-of-process isolation replaces it.

# v2.0
Initial release

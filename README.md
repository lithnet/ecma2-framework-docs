# Lithnet ECMA2 framework

The Lithnet ECMA2 framework is a .NET library that provides a simplified interface for creating ECMA2 connectors for the Microsoft Identity Manager (MIM) synchronization engine.

It has native support for async operations, and provides a simplified interface for common operations such as creating and updating objects, and handling multivalued attributes.

Management agents built with the framework run out of process. Your provider code runs in a separate worker process, isolated from the Synchronization Service and from other agents. This removes the dependency conflicts of the shared `Extensions` folder, and lets you target .NET (Core) rather than being limited to .NET Framework. See [How the framework works](architecture-overview.md).

The framework is available as a [NuGet package](https://www.nuget.org/packages/Lithnet.Ecma2Framework/).

## Features
- Runs your agent out of process, with its own private dependencies, so there are no DLL conflicts in the shared `Extensions` folder
- Support for .NET 8.0 and later, as well as .NET Framework 4.8 and later.
- Full async support
- Support for dependency injection 
- Support for `IOptions<T>` pattern for configuration with validation
- Strongly typed MIM configuration
- Implements the producer/consumer pattern for high performance imports
- Removes the need to manage paging of import results back to MIM
- Exports are multithreaded by default
- Manages object import/export exceptions automatically and reports them back to MIM
- No need to implement `IMAExtensible*` interfaces. The framework generates the connector and the out-of-process host for you

## Examples
You can see a full working example by referencing the [Lithnet.Okta.ManagementAgent](https://github.com/lithnet/okta-managementagent) project, which is based on this framework.

For a smaller, simple starting point program, you can refer to the [Lithnet.Ecma2Framework.Example](https://github.com/lithnet/ecma2-framework/tree/master/src/Lithnet.Ecma2Framework.Example) project in the GitHub repository.

## Getting started
Get started reading our [guide](getting-started.md).

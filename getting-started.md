# Getting started

This guide walks through creating a management agent with the Lithnet ECMA2 Framework. If you want the background on how it works first, see [How the framework works](architecture-overview.md), but you don't need to in order to follow along here.

## Step 1: Create a .NET class library

Create a new class library project. Your code no longer runs inside the Synchronization Service, so it is no longer tied to .NET Framework: the framework runs your library in a separate worker process. Your project is a library, so it has no `Main` method or entry point of its own. The framework generates the host for you.

Your library can target .NET Framework or .NET (Core). Targeting .NET (for example `net10.0-windows`) lets you use client libraries that are not published for .NET Framework, which is often the reason to choose it.

## Step 2: Add a reference to Microsoft.MetadirectoryServicesEx.dll

Your provider code works with the MIM types (`Schema`, `CSEntryChange`, and others), so add a reference to `Microsoft.MetadirectoryServicesEx.dll`. This assembly ships with MIM and is found on your Synchronization Service server, usually under `C:\Program Files\Microsoft Forefront Identity Manager\2010\Synchronization Service\Bin\Assemblies`.

```xml
<ItemGroup>
  <Reference Include="Microsoft.MetadirectoryServicesEx">
    <HintPath>path\to\Microsoft.MetadirectoryServicesEx.dll</HintPath>
    <Private>true</Private>
  </Reference>
</ItemGroup>
```

`Private` set to `true` copies the assembly into the worker output, which is the simplest option. If you distribute your management agent and would rather not include Microsoft's assembly in your package, set `Private` to `false`. The worker then loads the copy already installed on the MIM server at runtime.

## Step 3: Add the Lithnet.Ecma2Framework NuGet package

Add the `Lithnet.Ecma2Framework` package to your project. This package provides the interfaces and attributes you write against, and the build tooling that compiles the host and the connector for you.

```xml
<ItemGroup>
  <PackageReference Include="Lithnet.Ecma2Framework" Version="3.*" />
</ItemGroup>
```

You can find the package on [NuGet](https://www.nuget.org/packages/Lithnet.Ecma2Framework/).

## Step 4: Define your management agent's capabilities

Implement the [`ICapabilitiesProvider`](defining-capabilities.md) interface to tell MIM what your agent can do, such as whether it supports import, export, password operations, and delta imports.

## Step 5: Define your management agent's schema

Implement the [`ISchemaProvider`](defining-the-schema.md) interface to describe your agent's object types and their attributes.

## Step 6: Define your management agent's configuration

The framework offers [two ways](ma-config.md) to define the configuration shown in the MIM UI: building `ConfigParameterDefinition` objects yourself, or a strongly-typed `IOptions<T>` pattern driven by attributes.

## Step 7: Add import, export and password providers

Implement the providers your agent needs:

* [`IObjectImportProvider`](reference/lithnet.ecma2framework.iobjectimportprovider.md) for importing objects,
* [`IObjectExportProvider`](reference/lithnet.ecma2framework.iobjectexportprovider.md) for exporting objects, and
* [`IObjectPasswordProvider`](reference/lithnet.ecma2framework.iobjectpasswordprovider.md) for password set and change operations.

Add as many as you need to cover the object types in your schema. For imports, the framework also provides a [`ProducerConsumerImportProvider<T>`](using-the-producer-consumer.md) base class. It implements the producer/consumer pattern, so you produce model objects on one thread and the framework converts them to `CSEntryChange` objects on another, without you managing paging.

## Step 8: Add the startup class

Add a [startup class](building-the-startup-class.md) that implements `IEcmaStartup`. This is where you register your providers and any other services into the dependency-injection container. The framework uses that container to find and run your providers.

Your startup class and any configuration option classes must be `public`. The framework finds them by reading your library's public types when it generates the host. (Older, in-process versions of the framework suggested making these classes `internal`. That no longer applies.)

## Step 9: Build, package and deploy

Build your project, and the framework generates and compiles the host and the connector automatically. There is nothing else to wire up. When you are ready to install your agent on a MIM server, see [Packaging and deployment](packaging-and-deployment.md).

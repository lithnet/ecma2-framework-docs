# Getting Started
To get started with the Lithnet ECMA2 Framework, follow the steps below:

### Step 1: Create a new .NET Framework project
Start by creating a new .NET Framework 4.72 or higher project. It's important to note that Microsoft Identity Manager does not support .NET Core assemblies.

### Step 2: Add a reference to Microsoft.MetadirectoryServicesEx.dll
Next, add a reference to the `Microsoft.MetadirectoryServicesEx.dll` assembly. This assembly is located on your Microsoft Identity Manager (MIM) server, usually at the following path: `C:\Program Files\Microsoft Forefront Identity Manager\2010\Synchronization Service\Bin\Assemblies`. 

### Step 3: Add the Lithnet.Ecma2Framework NuGet package
Add the `Lithnet.Ecma2Framework` NuGet package to your project. This package provides the necessary APIs and tools for working with the ECMA2 framework.

You can find the `Lithnet.Ecma2Framework` NuGet package on the NuGet website [here](https://www.nuget.org/packages/Lithnet.Ecma2Framework/).

### Step 4: Define your management agent's capabilites
The ECMA2 framework provides an [`ICapabilitiesProvider` interface](defining-capabilities.md) that allows your to define your management agent's capabilities.

### Step 5: Define your management agent's schema
Create a class that derrives from the [`ISchemaProvider` interface](defining-the-schema.md) that allows your to define your management agent's object types and attributes. 

### Step 6: Define your management agent's configuration
The framework provides [two methods](ma-config.md) of defining the management agent's configuration UI. It supports the traditional definition of MIM `ConfigurationParameterDefinition` objects, as well as a native `Options<T>` pattern. 

### Step 7: Adding import and export and password providers
The framework provides `IObjectImportProvider`, `IObjectExportProvider`, and `IObjectPasswordProvider` interfaces, used for importing objects, exporting objects, and changing passwords, respectively.

You can add as many of these interfaces as required to support the classes defined in your schema. 

We also provide an import provider base class that implements the producer/consumer pattern. The [`ProducerConsumerImportProvider<T>` class](using-the-producer-consumer.md) provides a managed implementation that will allow you to define your producer method to create objects of type `T` on one thread, and convert them to CSEntryChanges on another.

### Step 9: Adding the Startup class
Bringing it all together is the [startup class](building-the-startup-class.md). This is where you setup the dependency injection container, registering your various providers and their dependencies. The framework will use this container to find your provider implementations and load them at run time.

### Step 10: Creating a single-file assembly (optional)
One of the main pain points of having multiple management agents all stored in the single `Extensions` folder that MIM provides is DLL depenendency clashes. The framework provides guidance to build a [single-file assembly](single-file-assemblies.md) that can help minimize this issue.



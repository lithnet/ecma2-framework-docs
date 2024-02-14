# IEcmaStartup

Namespace: Lithnet.Ecma2Framework

Defines the methods and properties that a start up class must implement

```csharp
public interface IEcmaStartup
```

## Methods

### **Configure(IConfigurationBuilder)**

This method is called when the ECMA2 framework is initializing. Use this method to configure the configuration builder.

```csharp
void Configure(IConfigurationBuilder builder)
```

#### Parameters

`builder` IConfigurationBuilder<br>
The configuration builder to configure

### **SetupServices(IServiceCollection, IConfigParameters)**

This method is called when the ECMA2 framework is initializing. Use this method to register your custom services with the DI container.

```csharp
void SetupServices(IServiceCollection services, IConfigParameters configParameters)
```

#### Parameters

`services` IServiceCollection<br>
A collection of services to add your custom services to

`configParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The configuration parameters as made available from the Microsoft Identity Management service

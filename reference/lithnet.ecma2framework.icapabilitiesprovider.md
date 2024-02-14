# ICapabilitiesProvider

Namespace: Lithnet.Ecma2Framework

Defines the methods and properties that a capabilities provider must implement

```csharp
public interface ICapabilitiesProvider
```

## Methods

### **GetCapabilitiesAsync(IConfigParameters)**

Gets the capabilities of the management agent

```csharp
Task<MACapabilities> GetCapabilitiesAsync(IConfigParameters configParameters)
```

#### Parameters

`configParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The configuration parameters of the management agent that have already been selected in the user interface, if the management agent chose to show a "Capabilities" configuration page

#### Returns

[Task&lt;MACapabilities&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
A MACapabilities object representing the capabilities of the management agent

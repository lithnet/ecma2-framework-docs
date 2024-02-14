# IConfigParametersProvider

Namespace: Lithnet.Ecma2Framework

Represents a provider that can provide configuration parameters to the synchronization service

```csharp
public interface IConfigParametersProvider
```

## Methods

### **GetConnectivityConfigParametersAsync(IConfigParameters, IList&lt;ConfigParameterDefinition&gt;)**

Gets the configuration parameters that are displayed on the Connectivity page of the management agent configuration

```csharp
Task GetConnectivityConfigParametersAsync(IConfigParameters existingParameters, IList<ConfigParameterDefinition> newDefinitions)
```

#### Parameters

`existingParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The set of configuration parameters and their values from configuration sections that have already been displayed and had their values set in the management agent configuration

`newDefinitions` [IList&lt;ConfigParameterDefinition&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ilist-1)<br>
A list that new configuration parameters for this page can be added to

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **GetGlobalConfigParametersAsync(IConfigParameters, IList&lt;ConfigParameterDefinition&gt;)**

Gets the configuration parameters that are displayed on the Global page of the management agent configuration

```csharp
Task GetGlobalConfigParametersAsync(IConfigParameters existingParameters, IList<ConfigParameterDefinition> newDefinitions)
```

#### Parameters

`existingParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The set of configuration parameters and their values from configuration sections that have already been displayed and had their values set in the management agent configuration

`newDefinitions` [IList&lt;ConfigParameterDefinition&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ilist-1)<br>
A list that new configuration parameters for this page can be added to

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **GetRunStepConfigParametersAsync(IConfigParameters, IList&lt;ConfigParameterDefinition&gt;)**

Gets the configuration parameters that are displayed on the Run Step page of the management agent configuration

```csharp
Task GetRunStepConfigParametersAsync(IConfigParameters existingParameters, IList<ConfigParameterDefinition> newDefinitions)
```

#### Parameters

`existingParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The set of configuration parameters and their values from configuration sections that have already been displayed and had their values set in the management agent configuration

`newDefinitions` [IList&lt;ConfigParameterDefinition&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ilist-1)<br>
A list that new configuration parameters for this page can be added to

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **GetPartitionConfigParametersAsync(IConfigParameters, IList&lt;ConfigParameterDefinition&gt;)**

Gets the configuration parameters that are displayed on the Partition page of the management agent configuration

```csharp
Task GetPartitionConfigParametersAsync(IConfigParameters existingParameters, IList<ConfigParameterDefinition> newDefinitions)
```

#### Parameters

`existingParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The set of configuration parameters and their values from configuration sections that have already been displayed and had their values set in the management agent configuration

`newDefinitions` [IList&lt;ConfigParameterDefinition&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ilist-1)<br>
A list that new configuration parameters for this page can be added to

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **GetCapabilitiesConfigParametersAsync(IConfigParameters, IList&lt;ConfigParameterDefinition&gt;)**

Gets the configuration parameters that are displayed on the Capabilities page of the management agent configuration. Note that the capabilities page is only shown when a management agent is first created.

```csharp
Task GetCapabilitiesConfigParametersAsync(IConfigParameters existingParameters, IList<ConfigParameterDefinition> newDefinitions)
```

#### Parameters

`existingParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The set of configuration parameters and their values from configuration sections that have already been displayed and had their values set in the management agent configuration

`newDefinitions` [IList&lt;ConfigParameterDefinition&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ilist-1)<br>
A list that new configuration parameters for this page can be added to

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **GetSchemaConfigParametersAsync(IConfigParameters, IList&lt;ConfigParameterDefinition&gt;, Int32)**

Gets the configuration parameters that are displayed on the Schema page of the management agent configuration
 Management agents can display multiple schema pages, and the synchronization service will call this method on a loop, incrementing the page number each time, until no new items are returned.
 Make sure that you only return items for the requested page number, and that you return an empty list when the requested page number is greater than the number of pages you have to display.

```csharp
Task GetSchemaConfigParametersAsync(IConfigParameters existingParameters, IList<ConfigParameterDefinition> newDefinitions, int pageNumber)
```

#### Parameters

`existingParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The set of configuration parameters and their values from configuration sections that have already been displayed and had their values set in the management agent configuration

`newDefinitions` [IList&lt;ConfigParameterDefinition&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ilist-1)<br>
A list that new configuration parameters for this page can be added to

`pageNumber` [Int32](https://docs.microsoft.com/en-us/dotnet/api/system.int32)<br>
The page number that is being requested

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **ValidateSchemaConfigParametersAsync(IConfigParameters, Int32)**

Validates the configuration parameters that are displayed on the Schema page of the management agent configuration.
 If there is no validation to perform, return a successful validation result.

```csharp
Task<ParameterValidationResult> ValidateSchemaConfigParametersAsync(IConfigParameters configParameters, int pageNumber)
```

#### Parameters

`configParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The set of configuration parameters and their values from the Schema page of the management agent configuration

`pageNumber` [Int32](https://docs.microsoft.com/en-us/dotnet/api/system.int32)<br>
The page number that is being validated

#### Returns

[Task&lt;ParameterValidationResult&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
A task that represents the asynchronous operation

### **ValidateCapabilitiesConfigParametersAsync(IConfigParameters)**

Validates the configuration parameters that are displayed on the Capabilities page of the management agent configuration.
 If there is no validation to perform, return a successful validation result.

```csharp
Task<ParameterValidationResult> ValidateCapabilitiesConfigParametersAsync(IConfigParameters configParameters)
```

#### Parameters

`configParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The set of configuration parameters and their values from the Schema page of the management agent configuration

#### Returns

[Task&lt;ParameterValidationResult&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
A task that represents the asynchronous operation

### **ValidateConnectivityConfigParametersAsync(IConfigParameters)**

Validates the configuration parameters that are displayed on the Connectivity page of the management agent configuration.
 If there is no validation to perform, return a successful validation result.

```csharp
Task<ParameterValidationResult> ValidateConnectivityConfigParametersAsync(IConfigParameters configParameters)
```

#### Parameters

`configParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The set of configuration parameters and their values from the Schema page of the management agent configuration

#### Returns

[Task&lt;ParameterValidationResult&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
A task that represents the asynchronous operation

### **ValidateGlobalConfigParametersAsync(IConfigParameters)**

Validates the configuration parameters that are displayed on the Global page of the management agent configuration.
 If there is no validation to perform, return a successful validation result.

```csharp
Task<ParameterValidationResult> ValidateGlobalConfigParametersAsync(IConfigParameters configParameters)
```

#### Parameters

`configParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The set of configuration parameters and their values from the Schema page of the management agent configuration

#### Returns

[Task&lt;ParameterValidationResult&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
A task that represents the asynchronous operation

### **ValidateRunStepConfigParametersAsync(IConfigParameters)**

Validates the configuration parameters that are displayed on the Run Step page of the management agent configuration.
 If there is no validation to perform, return a successful validation result.

```csharp
Task<ParameterValidationResult> ValidateRunStepConfigParametersAsync(IConfigParameters configParameters)
```

#### Parameters

`configParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The set of configuration parameters and their values from the Schema page of the management agent configuration

#### Returns

[Task&lt;ParameterValidationResult&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
A task that represents the asynchronous operation

### **ValidatePartitionConfigParametersAsync(IConfigParameters)**

Validates the configuration parameters that are displayed on the Partition page of the management agent configuration.
 If there is no validation to perform, return a successful validation result.

```csharp
Task<ParameterValidationResult> ValidatePartitionConfigParametersAsync(IConfigParameters configParameters)
```

#### Parameters

`configParameters` [IConfigParameters](./lithnet.ecma2framework.iconfigparameters.md)<br>
The set of configuration parameters and their values from the Schema page of the management agent configuration

#### Returns

[Task&lt;ParameterValidationResult&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
A task that represents the asynchronous operation

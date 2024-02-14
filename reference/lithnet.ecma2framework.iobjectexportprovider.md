# IObjectExportProvider

Namespace: Lithnet.Ecma2Framework

Defines the methods and properties that an object export provider must implement

```csharp
public interface IObjectExportProvider
```

## Methods

### **InitializeAsync(ExportContext)**

Initializes the object export provider. This method is called once at the start of an export operation

```csharp
Task InitializeAsync(ExportContext context)
```

#### Parameters

`context` [ExportContext](./lithnet.ecma2framework.exportcontext.md)<br>
The context of the operation

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **CanExportAsync(CSEntryChange)**

Indicates whether the object export provider can export objects of the specified type

```csharp
Task<bool> CanExportAsync(CSEntryChange csentry)
```

#### Parameters

`csentry` CSEntryChange<br>
The CSEntryChange representing the object to be exported

#### Returns

[Task&lt;Boolean&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
if the provider can export the object, otherwise

### **PutCSEntryChangeAsync(CSEntryChange, CancellationToken)**

Exports the specified object

```csharp
Task<CSEntryChangeResult> PutCSEntryChangeAsync(CSEntryChange csentry, CancellationToken cancellationToken)
```

#### Parameters

`csentry` CSEntryChange<br>
The CSEntryChange representing the object to be exported

`cancellationToken` [CancellationToken](https://docs.microsoft.com/en-us/dotnet/api/system.threading.cancellationtoken)<br>
A cancellation token

#### Returns

[Task&lt;CSEntryChangeResult&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
A task that represents the asynchronous operation

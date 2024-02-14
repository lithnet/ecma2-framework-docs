# IObjectImportProvider

Namespace: Lithnet.Ecma2Framework

Defines the methods and properties that an object import provider must implement

```csharp
public interface IObjectImportProvider
```

## Methods

### **InitializeAsync(ImportContext)**

Initializes the object import provider. This method is called once at the start of an import operation

```csharp
Task InitializeAsync(ImportContext context)
```

#### Parameters

`context` [ImportContext](./lithnet.ecma2framework.importcontext.md)<br>
The context of the operation

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **CanImportAsync(SchemaType)**

Indicates whether the object import provider can import objects of the specified type

```csharp
Task<bool> CanImportAsync(SchemaType type)
```

#### Parameters

`type` SchemaType<br>
The type of object to be imported

#### Returns

[Task&lt;Boolean&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
if the provider can import the object, otherwise

### **GetCSEntryChangesAsync(SchemaType, ICSEntryChangeCollection, String, CancellationToken)**

Initiates the operation to import objects of the specified type. Created CSEntryChanges should be added to the provided ICSEntryChangeCollection object.

```csharp
Task GetCSEntryChangesAsync(SchemaType type, ICSEntryChangeCollection csentryCollection, string incomingWatermark, CancellationToken cancellationToken)
```

#### Parameters

`type` SchemaType<br>
The type of object to import

`csentryCollection` [ICSEntryChangeCollection](./lithnet.ecma2framework.icsentrychangecollection.md)<br>
The collection of CSEntryChange objects to add the imported objects to

`incomingWatermark` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The watermark value provided by the management agent after its last successful import

`cancellationToken` [CancellationToken](https://docs.microsoft.com/en-us/dotnet/api/system.threading.cancellationtoken)<br>
A cancellation token

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **GetOutboundWatermark(SchemaType, CancellationToken)**

Gets the outbound watermark to save to the synchronization service at the completion of the import operation
 If the management agent doesn't support delta operations, then this method should return null

```csharp
Task<string> GetOutboundWatermark(SchemaType type, CancellationToken cancellationToken)
```

#### Parameters

`type` SchemaType<br>
The object type to get the watermark for

`cancellationToken` [CancellationToken](https://docs.microsoft.com/en-us/dotnet/api/system.threading.cancellationtoken)<br>
A cancellation token

#### Returns

[Task&lt;String&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
The outbound watermark, or null if the management agent doesn't support delta operations

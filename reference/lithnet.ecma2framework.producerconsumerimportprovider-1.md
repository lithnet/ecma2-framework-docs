# ProducerConsumerImportProvider&lt;TObject&gt;

Namespace: Lithnet.Ecma2Framework

The ProducerConsumerImportProvider class provides a base class for import providers that use a producer-consumer pattern.

This class provides a simple implementation of the producer-consumer pattern, and allows the developer to focus on the import logic, rather than the threading logic.
 Implementers implement the mandatory methods that enumerate the raw objects of type TObject, and provide the logic to convert these objects into CSEntryChange objects. The provider takes care of constructing the CSEntryChanges and passing them back to the sync engine.

```csharp
public abstract class ProducerConsumerImportProvider<TObject> : IObjectImportProvider
```

#### Type Parameters

`TObject`<br>
The type of object that the provider will enumerate

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [ProducerConsumerImportProvider&lt;TObject&gt;](./lithnet.ecma2framework.producerconsumerimportprovider-1.md)<br>
Implements [IObjectImportProvider](./lithnet.ecma2framework.iobjectimportprovider.md)

## Methods

### **CanImportAsync(SchemaType)**

Gets a value indicating whether the provider can import objects of the specified type

```csharp
public abstract Task<bool> CanImportAsync(SchemaType type)
```

#### Parameters

`type` SchemaType<br>
The type of object to be imported

#### Returns

[Task&lt;Boolean&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
if the provider can import the object, otherwise

### **InitializeAsync(ImportContext)**

Initializes the object import provider. This method is called once at the start of an import operation

```csharp
public Task InitializeAsync(ImportContext context)
```

#### Parameters

`context` [ImportContext](./lithnet.ecma2framework.importcontext.md)<br>
The context of the operation

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **GetCSEntryChangesAsync(SchemaType, ICSEntryChangeCollection, String, CancellationToken)**

```csharp
public Task GetCSEntryChangesAsync(SchemaType type, ICSEntryChangeCollection collection, string watermark, CancellationToken cancellationToken)
```

#### Parameters

`type` SchemaType<br>

`collection` [ICSEntryChangeCollection](./lithnet.ecma2framework.icsentrychangecollection.md)<br>

`watermark` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>

`cancellationToken` [CancellationToken](https://docs.microsoft.com/en-us/dotnet/api/system.threading.cancellationtoken)<br>

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>

### **GetOutboundWatermark(SchemaType, CancellationToken)**

```csharp
public abstract Task<string> GetOutboundWatermark(SchemaType type, CancellationToken cancellationToken)
```

#### Parameters

`type` SchemaType<br>

`cancellationToken` [CancellationToken](https://docs.microsoft.com/en-us/dotnet/api/system.threading.cancellationtoken)<br>

#### Returns

[Task&lt;String&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>

### **OnFinalizeCsEntryChangeAsync(CSEntryChange, CancellationToken)**

A method that is called when the CSEntryChange has been completed, but before it is returned to the sync engine.
 Override this method to inspect or modify the CSEntryChange before it is returned to the sync engine

```csharp
protected Task OnFinalizeCsEntryChangeAsync(CSEntryChange csentry, CancellationToken cancellationToken)
```

#### Parameters

`csentry` CSEntryChange<br>
The CSEntryChange object that has been created

`cancellationToken` [CancellationToken](https://docs.microsoft.com/en-us/dotnet/api/system.threading.cancellationtoken)<br>
A cancellation token

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **OnPrepareCSEntryChangeAsync(CSEntryChange, CancellationToken)**

A method that is called when the CSEntryChange has been created, but before any attribute changes have been added to it.
 Override this method to inspect or modify the CSEntryChange before any attributes have been added to it

```csharp
protected Task OnPrepareCSEntryChangeAsync(CSEntryChange csentry, CancellationToken cancellationToken)
```

#### Parameters

`csentry` CSEntryChange<br>
The CSEntryChange object that has been created

`cancellationToken` [CancellationToken](https://docs.microsoft.com/en-us/dotnet/api/system.threading.cancellationtoken)<br>
A cancellation token

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **PrepareObjectForImportAsync(TObject, CancellationToken)**

A method that is called when the object has been retrieved from the source, but before it is converted into a CSEntryChange object.
 Override this method to inspect or modify the object before it is converted into a CSEntryChange object

```csharp
protected Task PrepareObjectForImportAsync(TObject item, CancellationToken cancellationToken)
```

#### Parameters

`item` TObject<br>
The object that has been retrieved from the source

`cancellationToken` [CancellationToken](https://docs.microsoft.com/en-us/dotnet/api/system.threading.cancellationtoken)<br>
A cancellation token

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **OnInitializeAsync()**

A method that is called when the provider is initialized, but before any objects are retrieved from the source.
 Override this method to perform any initialization logic

```csharp
protected Task OnInitializeAsync()
```

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **OnStartProducerAsync()**

A method that is called when the provider is initialized, but before any objects are retrieved from the source.
 Override this method to perform any initialization logic required to start producing objects

```csharp
protected Task OnStartProducerAsync()
```

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **OnCompleteProducerAsync()**

A method that is called when the provider has finished producing objects.
 Override this method to perform any cleanup logic required after all objects have been produced

```csharp
protected Task OnCompleteProducerAsync()
```

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **OnStartConsumerAsync()**

A method that is called when the provider has started consuming objects.
 Override this method to perform any initialization logic required to start consuming objects

```csharp
protected Task OnStartConsumerAsync()
```

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **OnCompleteConsumerAsync()**

A method that is called when the provider has finished consuming objects.
 Override this method to perform any cleanup logic required after all objects have been consumed and the provider is about to be terminated

```csharp
protected Task OnCompleteConsumerAsync()
```

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **GetAnchorAttributesAsync(TObject)**

Gets the list of AnchorAttributes for the specified object

```csharp
protected abstract Task<List<AnchorAttribute>> GetAnchorAttributesAsync(TObject item)
```

#### Parameters

`item` TObject<br>
The object to get the AnchorAttributes for

#### Returns

[Task&lt;List&lt;AnchorAttribute&gt;&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
A list of AnchorAttributes

### **CreateAttributeChangeAsync(SchemaAttribute, ObjectModificationType, TObject, CancellationToken)**

Creates an AttributeChange object for the specified attribute

```csharp
protected abstract Task<AttributeChange> CreateAttributeChangeAsync(SchemaAttribute type, ObjectModificationType modificationType, TObject item, CancellationToken cancellationToken)
```

#### Parameters

`type` SchemaAttribute<br>
The schema attribute to create the AttributeChange for

`modificationType` ObjectModificationType<br>
The modification type of the object

`item` TObject<br>
The object to create the AttributeChange from

`cancellationToken` [CancellationToken](https://docs.microsoft.com/en-us/dotnet/api/system.threading.cancellationtoken)<br>
A cancellation token

#### Returns

[Task&lt;AttributeChange&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
An AttributeChange represnting the specified attribute, or null if there are no changes to the attribute provided

### **GetDNAsync(TObject)**

Gets the DN of the specified object. This will be used to populate the DN property of the CSEntryChange

```csharp
protected abstract Task<string> GetDNAsync(TObject item)
```

#### Parameters

`item` TObject<br>
The item to return the DN of

#### Returns

[Task&lt;String&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
The DN that will be used in the CSEntryChange

### **GetObjectsAsync(String, CancellationToken)**

Gets the objects to be imported.

```csharp
protected abstract IAsyncEnumerable<TObject> GetObjectsAsync(string watermark, CancellationToken cancellationToken)
```

#### Parameters

`watermark` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The watermark value provided by the management agent after its last successful import

`cancellationToken` [CancellationToken](https://docs.microsoft.com/en-us/dotnet/api/system.threading.cancellationtoken)<br>
A cancellation token

#### Returns

IAsyncEnumerable&lt;TObject&gt;<br>
An enumerable of objects to be imported

### **GetObjectModificationTypeAsync(TObject)**

Gets the modification type of the specified object. This will be used to determine the object modification type of the CSEntryChange

```csharp
protected abstract Task<ObjectModificationType> GetObjectModificationTypeAsync(TObject item)
```

#### Parameters

`item` TObject<br>
The object to get the modification type of

#### Returns

[Task&lt;ObjectModificationType&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
The modification type of the object

# ISchemaProvider

Namespace: Lithnet.Ecma2Framework

Defines the methods and properties that a schema provider must implement

```csharp
public interface ISchemaProvider
```

## Methods

### **GetMmsSchemaAsync()**

Gets the management agent's schema

```csharp
Task<Schema> GetMmsSchemaAsync()
```

#### Returns

[Task&lt;Schema&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
A Schema object representing the objects and attributes used by the management agent

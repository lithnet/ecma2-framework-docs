# ImportContext

Namespace: Lithnet.Ecma2Framework

The import context contains information about the currently running import operation

```csharp
public class ImportContext
```

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [ImportContext](./lithnet.ecma2framework.importcontext.md)

## Properties

### **RunStep**

Gets information about the run step that is currently executing

```csharp
public OpenImportConnectionRunStep RunStep { get; }
```

#### Property Value

OpenImportConnectionRunStep<br>

### **InDelta**

Gets a value that indicates if the import operation is a delta import

```csharp
public bool InDelta { get; }
```

#### Property Value

[Boolean](https://docs.microsoft.com/en-us/dotnet/api/system.boolean)<br>

### **Types**

Gets the current schema of the management agent

```csharp
public Schema Types { get; }
```

#### Property Value

Schema<br>

### **CustomData**

Gets or sets an object that can be used to store user-defined custom data that is shared by all import providers

```csharp
public object CustomData { get; set; }
```

#### Property Value

[Object](https://docs.microsoft.com/en-us/dotnet/api/system.object)<br>

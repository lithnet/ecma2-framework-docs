# ExportContext

Namespace: Lithnet.Ecma2Framework

The export context contains information about the currently running export operation

```csharp
public class ExportContext
```

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [ExportContext](./lithnet.ecma2framework.exportcontext.md)

## Properties

### **RunStep**

Gets information about the run step that is currently executing

```csharp
public OpenExportConnectionRunStep RunStep { get; }
```

#### Property Value

OpenExportConnectionRunStep<br>

### **Types**

Gets the current schema of the management agent

```csharp
public Schema Types { get; }
```

#### Property Value

Schema<br>

### **CustomData**

Gets or sets an object that can be used to store user-defined custom data that is shared by all export providers

```csharp
public object CustomData { get; set; }
```

#### Property Value

[Object](https://docs.microsoft.com/en-us/dotnet/api/system.object)<br>

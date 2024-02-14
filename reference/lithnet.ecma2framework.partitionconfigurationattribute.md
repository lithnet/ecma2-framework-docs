# PartitionConfigurationAttribute

Namespace: Lithnet.Ecma2Framework

An attribute that is used to decorate a class that contains configuration information that should be shown on the Partition page of the management agent configuration

```csharp
public class PartitionConfigurationAttribute : System.Attribute
```

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [Attribute](https://docs.microsoft.com/en-us/dotnet/api/system.attribute) → [PartitionConfigurationAttribute](./lithnet.ecma2framework.partitionconfigurationattribute.md)

## Properties

### **Name**

Gets the name of the configuration section

```csharp
public string Name { get; }
```

#### Property Value

[String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>

### **TypeId**

```csharp
public object TypeId { get; }
```

#### Property Value

[Object](https://docs.microsoft.com/en-us/dotnet/api/system.object)<br>

## Constructors

### **PartitionConfigurationAttribute()**

Initializes a new instance of the PartitionConfigurationAttribute class

```csharp
public PartitionConfigurationAttribute()
```

### **PartitionConfigurationAttribute(String)**

Initializes a new instance of the PartitionConfigurationAttribute class

```csharp
public PartitionConfigurationAttribute(string name)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
An optional name of the configuration section. This value defaults to Ecma:Partition

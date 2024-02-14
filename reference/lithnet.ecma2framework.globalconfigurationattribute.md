# GlobalConfigurationAttribute

Namespace: Lithnet.Ecma2Framework

An attribute that is used to decorate a class that contains configuration information that should be shown on the Global page of the management agent configuration

```csharp
public class GlobalConfigurationAttribute : System.Attribute
```

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [Attribute](https://docs.microsoft.com/en-us/dotnet/api/system.attribute) → [GlobalConfigurationAttribute](./lithnet.ecma2framework.globalconfigurationattribute.md)

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

### **GlobalConfigurationAttribute()**

Initializes a new instance of the GlobalConfigurationAttribute class

```csharp
public GlobalConfigurationAttribute()
```

### **GlobalConfigurationAttribute(String)**

Initializes a new instance of the GlobalConfigurationAttribute class

```csharp
public GlobalConfigurationAttribute(string name)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
An optional name of the configuration section. This value defaults to Ecma:Global

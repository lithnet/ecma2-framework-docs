# SchemaConfigurationAttribute

Namespace: Lithnet.Ecma2Framework

An attribute that is used to decorate a class that contains configuration information that should be shown on the Schema page of the management agent configuration

```csharp
public class SchemaConfigurationAttribute : System.Attribute
```

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [Attribute](https://docs.microsoft.com/en-us/dotnet/api/system.attribute) → [SchemaConfigurationAttribute](./lithnet.ecma2framework.schemaconfigurationattribute.md)

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

### **SchemaConfigurationAttribute()**

Initializes a new instance of the SchemaConfigurationAttribute class

```csharp
public SchemaConfigurationAttribute()
```

### **SchemaConfigurationAttribute(String)**

Initializes a new instance of the SchemaConfigurationAttribute class

```csharp
public SchemaConfigurationAttribute(string name)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
An optional name of the configuration section. This value defaults to Ecma:Schema

# StringParameterAttribute

Namespace: Lithnet.Ecma2Framework

Defines a configuration parameter that is rendered as a text box in the management agent's configuration pages

```csharp
public class StringParameterAttribute : DataParameterAttribute
```

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [Attribute](https://docs.microsoft.com/en-us/dotnet/api/system.attribute) → [ParameterAttribute](./lithnet.ecma2framework.parameterattribute.md) → [DataParameterAttribute](./lithnet.ecma2framework.dataparameterattribute.md) → [StringParameterAttribute](./lithnet.ecma2framework.stringparameterattribute.md)

## Properties

### **Name**

Gets the name of the parameter, as shown to the user on the MIM configuration page

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

### **StringParameterAttribute(String)**

Creates a new instance of the StringParameterAttribute class

```csharp
public StringParameterAttribute(string name)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The name of the parameter, as shown to the user on the MIM configuration page

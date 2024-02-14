# MultilineTextboxParameterAttribute

Namespace: Lithnet.Ecma2Framework

Defines a configuration parameter that is rendered as a multi-line text box in the management agent's configuration pages

```csharp
public class MultilineTextboxParameterAttribute : DataParameterAttribute
```

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [Attribute](https://docs.microsoft.com/en-us/dotnet/api/system.attribute) → [ParameterAttribute](./lithnet.ecma2framework.parameterattribute.md) → [DataParameterAttribute](./lithnet.ecma2framework.dataparameterattribute.md) → [MultilineTextboxParameterAttribute](./lithnet.ecma2framework.multilinetextboxparameterattribute.md)

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

### **MultilineTextboxParameterAttribute(String)**

Initializes a new instance of the MultilineTextboxParameterAttribute class

```csharp
public MultilineTextboxParameterAttribute(string name)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The name of the parameter, as shown to the user on the MIM configuration page

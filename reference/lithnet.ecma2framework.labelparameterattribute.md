# LabelParameterAttribute

Namespace: Lithnet.Ecma2Framework

Defines a configuration parameter that is rendered as a heading label in the management agent's configuration pages
 The label has no data backing and therefore is not associated with a property, rather it is added to an existing property. The label will be displayed above the decorated property.

```csharp
public class LabelParameterAttribute : UIParameterAttribute
```

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [Attribute](https://docs.microsoft.com/en-us/dotnet/api/system.attribute) → [ParameterAttribute](./lithnet.ecma2framework.parameterattribute.md) → [UIParameterAttribute](./lithnet.ecma2framework.uiparameterattribute.md) → [LabelParameterAttribute](./lithnet.ecma2framework.labelparameterattribute.md)

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

### **LabelParameterAttribute(String)**

Initializes a new instance of the LabelParameterAttribute class

```csharp
public LabelParameterAttribute(string name)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The name of the parameter, as shown to the user on the MIM configuration page

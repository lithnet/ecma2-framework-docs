# UIParameterAttribute

Namespace: Lithnet.Ecma2Framework

Base class that represents a configuration parameter that does not store data

```csharp
public abstract class UIParameterAttribute : ParameterAttribute
```

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [Attribute](https://docs.microsoft.com/en-us/dotnet/api/system.attribute) → [ParameterAttribute](./lithnet.ecma2framework.parameterattribute.md) → [UIParameterAttribute](./lithnet.ecma2framework.uiparameterattribute.md)

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

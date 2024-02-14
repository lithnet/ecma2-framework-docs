# EncryptedStringParameterAttribute

Namespace: Lithnet.Ecma2Framework

Defines a configuration parameter that is rendered as a textbox in the management agent's configuration pages, and is stored as an encrypted string

```csharp
public class EncryptedStringParameterAttribute : DataParameterAttribute
```

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [Attribute](https://docs.microsoft.com/en-us/dotnet/api/system.attribute) → [ParameterAttribute](./lithnet.ecma2framework.parameterattribute.md) → [DataParameterAttribute](./lithnet.ecma2framework.dataparameterattribute.md) → [EncryptedStringParameterAttribute](./lithnet.ecma2framework.encryptedstringparameterattribute.md)

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

### **EncryptedStringParameterAttribute(String)**

Initializes a new instance of the EncryptedStringParameterAttribute class

```csharp
public EncryptedStringParameterAttribute(string name)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The name of the parameter, as shown to the user on the MIM configuration page

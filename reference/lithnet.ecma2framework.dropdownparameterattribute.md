# DropdownParameterAttribute

Namespace: Lithnet.Ecma2Framework

Defines a configuration parameter that is rendered as a drop down control in the management agent's configuration pages

```csharp
public class DropdownParameterAttribute : DataParameterAttribute
```

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [Attribute](https://docs.microsoft.com/en-us/dotnet/api/system.attribute) → [ParameterAttribute](./lithnet.ecma2framework.parameterattribute.md) → [DataParameterAttribute](./lithnet.ecma2framework.dataparameterattribute.md) → [DropdownParameterAttribute](./lithnet.ecma2framework.dropdownparameterattribute.md)

## Properties

### **Extensible**

Gets a boolean value that indicates if users should be able to specify their own value in addition to the displayed values

```csharp
public bool Extensible { get; }
```

#### Property Value

[Boolean](https://docs.microsoft.com/en-us/dotnet/api/system.boolean)<br>

### **DisplayedValues**

Gets the list of values that should be displayed in the drop down list

```csharp
public String[] DisplayedValues { get; }
```

#### Property Value

[String[]](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>

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

### **DropdownParameterAttribute(String, Boolean, String[])**

Initializes a new instance of the DropdownParameterAttribute class

```csharp
public DropdownParameterAttribute(string name, bool extensible, String[] displayedValues)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The name of the parameter, as shown to the user on the MIM configuration page

`extensible` [Boolean](https://docs.microsoft.com/en-us/dotnet/api/system.boolean)<br>
A boolean value that indicates if users should be able to specify their own value in addition to the displayed values

`displayedValues` [String[]](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The list of values that should be displayed in the drop down list

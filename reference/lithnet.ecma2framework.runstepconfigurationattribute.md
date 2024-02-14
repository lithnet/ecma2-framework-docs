# RunStepConfigurationAttribute

Namespace: Lithnet.Ecma2Framework

An attribute that is used to decorate a class that contains configuration information that should be shown on the Run step page of the management agent configuration

```csharp
public class RunStepConfigurationAttribute : System.Attribute
```

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [Attribute](https://docs.microsoft.com/en-us/dotnet/api/system.attribute) → [RunStepConfigurationAttribute](./lithnet.ecma2framework.runstepconfigurationattribute.md)

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

### **RunStepConfigurationAttribute()**

Initializes a new instance of the RunStepConfigurationAttribute class

```csharp
public RunStepConfigurationAttribute()
```

### **RunStepConfigurationAttribute(String)**

Initializes a new instance of the RunStepConfigurationAttribute class

```csharp
public RunStepConfigurationAttribute(string name)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
An optional name of the configuration section. This value defaults to Ecma:RunStep

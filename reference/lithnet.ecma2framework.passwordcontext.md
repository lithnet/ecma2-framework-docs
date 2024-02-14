# PasswordContext

Namespace: Lithnet.Ecma2Framework

Provides context information to the password management system

```csharp
public class PasswordContext
```

Inheritance [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object) → [PasswordContext](./lithnet.ecma2framework.passwordcontext.md)

## Properties

### **Partition**

Gets the partition that the password operation is running against

```csharp
public Partition Partition { get; }
```

#### Property Value

Partition<br>

### **CustomData**

Gets or sets an object that can be used to store user-defined custom data that is shared by all password providers

```csharp
public object CustomData { get; set; }
```

#### Property Value

[Object](https://docs.microsoft.com/en-us/dotnet/api/system.object)<br>

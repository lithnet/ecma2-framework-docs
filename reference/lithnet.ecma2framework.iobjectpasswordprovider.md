# IObjectPasswordProvider

Namespace: Lithnet.Ecma2Framework

Defines the methods and properties that a password provider must implement

```csharp
public interface IObjectPasswordProvider
```

## Methods

### **InitializeAsync(PasswordContext)**

Initializes the password provider. This method is called once at the start of a batch of password operations

```csharp
Task InitializeAsync(PasswordContext context)
```

#### Parameters

`context` [PasswordContext](./lithnet.ecma2framework.passwordcontext.md)<br>
The context of the operation

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **CanPerformPasswordOperationAsync(CSEntry)**

Indicates whether the password provider can perform password operations on the specified object

```csharp
Task<bool> CanPerformPasswordOperationAsync(CSEntry csentry)
```

#### Parameters

`csentry` CSEntry<br>
The CSEntry representing the object with the associated password change

#### Returns

[Task&lt;Boolean&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1)<br>
if the provider can process the password change, otherwise

### **SetPasswordAsync(CSEntry, SecureString, PasswordOptions)**

Sets the password on the specified object

```csharp
Task SetPasswordAsync(CSEntry csentry, SecureString newPassword, PasswordOptions options)
```

#### Parameters

`csentry` CSEntry<br>
The CSEntry representing the object whose password should be set

`newPassword` [SecureString](https://docs.microsoft.com/en-us/dotnet/api/system.security.securestring)<br>
The new password

`options` PasswordOptions<br>
Flags that indicate additional steps that may need to be taken once the password it set

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **ChangePasswordAsync(CSEntry, SecureString, SecureString)**

Changes the password on the specified object

```csharp
Task ChangePasswordAsync(CSEntry csentry, SecureString oldPassword, SecureString newPassword)
```

#### Parameters

`csentry` CSEntry<br>
The CSEntry representing the object whose password should be changed

`oldPassword` [SecureString](https://docs.microsoft.com/en-us/dotnet/api/system.security.securestring)<br>
The old password

`newPassword` [SecureString](https://docs.microsoft.com/en-us/dotnet/api/system.security.securestring)<br>
The new password

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

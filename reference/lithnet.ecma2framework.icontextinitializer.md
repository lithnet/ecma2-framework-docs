# IContextInitializer

Namespace: Lithnet.Ecma2Framework

Context initializers are called before each import, export or password operation to allow the management agent to perform any required initialization. While import and export providers are each initialized at the start of the operation, context initializers are called only once prior to all operations.

```csharp
public interface IContextInitializer
```

## Methods

### **InitializeImportAsync(ImportContext)**

Initializes the context prior to any import providers being initialized

```csharp
Task InitializeImportAsync(ImportContext context)
```

#### Parameters

`context` [ImportContext](./lithnet.ecma2framework.importcontext.md)<br>
The ImportContext to be shared by the import providers

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **InitializeExportAsync(ExportContext)**

Initializes the context prior to any export providers being initialized

```csharp
Task InitializeExportAsync(ExportContext context)
```

#### Parameters

`context` [ExportContext](./lithnet.ecma2framework.exportcontext.md)<br>
The ExportContext to be shared by the export providers

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

### **InitializePasswordOperationAsync(PasswordContext)**

Initializes the context prior to any password providers being initialized

```csharp
Task InitializePasswordOperationAsync(PasswordContext context)
```

#### Parameters

`context` [PasswordContext](./lithnet.ecma2framework.passwordcontext.md)<br>
The PasswordContext to be shared by the password providers

#### Returns

[Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task)<br>
A task that represents the asynchronous operation

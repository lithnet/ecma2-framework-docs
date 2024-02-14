# IConfigParameters

Namespace: Lithnet.Ecma2Framework

Represents a collection of configuration parameters provided by the Synchronization Service

```csharp
public interface IConfigParameters
```

## Properties

### **Parameters**

Gets the raw configuration parameter dictionary as provided by the synchronization service

```csharp
public abstract KeyedCollection<string, ConfigParameter> Parameters { get; }
```

#### Property Value

KeyedCollection&lt;String, ConfigParameter&gt;<br>

## Methods

### **GetBool(String, Boolean)**

Gets a boolean value from the configuration parameter set

```csharp
bool GetBool(string name, bool defaultValue)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The name of the configuration parameter

`defaultValue` [Boolean](https://docs.microsoft.com/en-us/dotnet/api/system.boolean)<br>
A value to provide if the key is not present or it's value is not present

#### Returns

[Boolean](https://docs.microsoft.com/en-us/dotnet/api/system.boolean)<br>
The value of the configuration parameter, or the default value if it doesn't exist

### **GetInt(String, Int32)**

Gets an integer value from the configuration parameter set

```csharp
int GetInt(string name, int defaultValue)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The name of the configuration parameter

`defaultValue` [Int32](https://docs.microsoft.com/en-us/dotnet/api/system.int32)<br>
A value to provide if the key is not present or it's value is not present

#### Returns

[Int32](https://docs.microsoft.com/en-us/dotnet/api/system.int32)<br>
The value of the configuration parameter, or the default value if it doesn't exist

### **GetList(String, String)**

Gets a list of string values from the configuration parameter set

```csharp
List<string> GetList(string name, string separator)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The name of the configuration parameter

`separator` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The character used a separator between string values

#### Returns

[List&lt;String&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1)<br>
The value of the configuration parameter, or the default value if it doesn't exist

### **GetLong(String, Int64)**

Gets a long integer value from the configuration parameter set

```csharp
long GetLong(string name, long defaultValue)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The name of the configuration parameter

`defaultValue` [Int64](https://docs.microsoft.com/en-us/dotnet/api/system.int64)<br>
A value to provide if the key is not present or it's value is not present

#### Returns

[Int64](https://docs.microsoft.com/en-us/dotnet/api/system.int64)<br>
The value of the configuration parameter, or the default value if it doesn't exist

### **GetString(String)**

Gets a string value from the configuration parameter set

```csharp
string GetString(string name)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The name of the configuration parameter

#### Returns

[String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
THe value of the configuration parameter, or null if the value doesn't exist

### **GetString(String, String)**

Gets a string value from the configuration parameter set

```csharp
string GetString(string name, string defaultValue)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The name of the configuration parameter

`defaultValue` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
A value to provide if the key is not present or it's value is not present

#### Returns

[String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The value of the configuration parameter, or the default value if it doesn't exist

### **HasValue(String)**

Determines if a configuration parameter exists

```csharp
bool HasValue(string name)
```

#### Parameters

`name` [String](https://docs.microsoft.com/en-us/dotnet/api/system.string)<br>
The name of the configuration parameter

#### Returns

[Boolean](https://docs.microsoft.com/en-us/dotnet/api/system.boolean)<br>
if the parameter is present, if it is not

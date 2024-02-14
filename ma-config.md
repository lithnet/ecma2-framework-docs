# Configuration parameters
The Lithnet ECMA2 Framework provides two ways for you to configure the parameters that are shown in the MIM user interface. 

MIM allows you to provide configuration pages for the following sections

| Page | Description |
| --- | --- |
| Capabilities | The capabilites when a management agent is first added to the sync engine. It is not shown again after the MA is created. It is a one-time-setup opportunity to define the capability of the management agent to MIM. |
| Connectivity | The connectivity page is typically used to define the setup to the remote server or data source. It's shown before the schema, but after capabilites have been determined |
| Schema | Before MIM calls for your schema, you have a chance to ask the user for configuration that will influence the schema provided to MIM |
| Global | The Global page contains generic settings used for all operations |
| RunStep | The RunStep page is shown when configuring a run step on the management agent |
| Partition | The partition page is shown only on management agents that support partitions, and can be used to configure partition-specific information. |

## Method 1: Manual definition using `IConfigParametersProvider`
The configuration parameters can be configured in the traditional way by implementing the `IConfigParametersProvider` interface. This is similar to using the native `IMAExtensible2GetParameters` interface, in that you get to define your parameters and validation logic in code.

This method should be used when config parameters are static and don't change in relation to other parameter values.

As shown in the validation example, you access the parameters using the `IConfigParameters` object. This is a wrapper with some helper functions that allow you to get the native values provided by the MIM engine.

```cs
internal class ConfigParametersProvider : IConfigParametersProvider
{
    public Task GetCapabilitiesConfigParametersAsync(IConfigParameters existingParameters, IList<ConfigParameterDefinition> newDefinitions)
    {
        return Task.CompletedTask;
    }

    public Task GetConnectivityConfigParametersAsync(IConfigParameters existingParameters, IList<ConfigParameterDefinition> newDefinitions)
    {
        newDefinitions.Add(ConfigParameterDefinition.CreateStringParameter("API URL", null));
        return Task.CompletedTask;
    }

    public Task GetGlobalConfigParametersAsync(IConfigParameters existingParameters, IList<ConfigParameterDefinition> newDefinitions)
    {
        newDefinitions.Add(ConfigParameterDefinition.CreateStringParameter("Log file name", null));
        return Task.CompletedTask;
    }

    public Task<ParameterValidationResult> ValidateCapabilitiesConfigParametersAsync(IConfigParameters configParameters)
    {
        return Task.FromResult(new ParameterValidationResult());
    }

    public Task<ParameterValidationResult> ValidateConnectivityConfigParametersAsync(IConfigParameters configParameters)
    {
        var url = configParameters.GetString("API URL");

        if (!Uri.IsWellFormedUriString(url, UriKind.Absolute))
        {
            return Task.FromResult(new ParameterValidationResult(ParameterValidationResultCode.Failure, "The API URL is not a valid URL", "API URL"));
        }

        return Task.FromResult(new ParameterValidationResult());
    }

    public Task<ParameterValidationResult> ValidateGlobalConfigParametersAsync(IConfigParameters configParameters)
    {
        return Task.FromResult(new ParameterValidationResult());
    }
}
```

### Accessing configuration

You can access these parameters in your classes by injecting and `IConfigParameters` into the class of a  constructor where they are required.

In the example below, the "API URL" parameter is obtained from the `IConfigParameters` object passed into the class's constructor.

```cs
internal class UserImportProvider : ProducerConsumerImportProvider<User>
{
    private readonly HttpClient client;
    private readonly ILogger<UserImportProvider> logger;
    private readonly IConfigParameters configParameters;
    private string apiUrl;

    public UserImportProvider(HttpClient client, ILogger<UserImportProvider> logger, IConfigParameters configParameters) : base(logger)
    {
        this.client = client;
        this.logger = logger;
        this.configParameters = configParameters;
        this.apiUrl = this.configParameters.GetString("API URL");
    }
}

```

## Method 2: Automatic definition using `IOptions<T>` pattern
We've implemented a much simpler mechanism to provide strongly-typed configuration for your application. 

The [`Options<T>` pattern](https://learn.microsoft.com/en-us/dotnet/core/extensions/options) allows you to define the configuration parameters as a class, and the framework will create the necessary parameter binds for you.

Define a class, and decorate it with one of the following attributes
- `[ConnectivityConfiguration]`
- `[CapabilitiesConfiguration]`
- `[SchemaConfiguration]`
- `[GlobalConfiguration]`
- `[RunStepConfiguration]`
- `[PartitionConfiguration]`

For each configuration option you want to expose, create a property with a public getting and setter, and decorate it with one of the following attributes
- `[CheckboxParameter]`
- `[StringParameter]`
- `[DropdownParameter]`
- `[EncryptedStringParameter]`
- `[FileParameter]`
- `[MultilineTextboxParameter]`

You can also add any validation attribute from the `System.ComponentModel.DataAnnotations` namespace. These will be used to automatically validate the data provided by the user in the UI.

Optionally, use the `[DefaultValue]` attribute to specify the default value that will be shown to users in the UI.

```cs
using System.ComponentModel;
using System.ComponentModel.DataAnnotations;

namespace Lithnet.Ecma2Framework.Example
{
    [ConnectivityConfiguration]
    internal class ConnectivityOptions
    {
        [StringParameter("API URL")]
        [Required]
        [Url]
        [DefaultValue("https://jsonplaceholder.typicode.com")]
        public string ApiUrl { get; set; }
    }
}
```

The framework will use these attributes to build the configuration definition for the MIM sync engine, and will then be able to provide stronly-typed options classes back to your management agent for consumption.

### Accessing configuration

In a classes that requires access to the configuration, you can simply inject the relevant IOptions<T> interface to get the options you need.

```cs
internal class UserImportProvider : ProducerConsumerImportProvider<User>
{
    private readonly HttpClient client;
    private readonly ILogger<UserImportProvider> logger;
    private readonly ConnectivityOptions connectivityOptions;
    private string ApiUrl;

    public UserImportProvider(HttpClient client, ILogger<UserImportProvider> logger, IOptions<ConnectivityOptions> connectivityOptions) : base(logger)
    {
        this.client = client;
        this.logger = logger;
        this.connectivityOptions = connectivityOptions.Value;
        this.ApiUrl = this.connectivityOptions.ApiUrl;
    }
}
```

In this example, we're injecting the `ConnectivityOptions` class directly into the constructor of our UserImportProvider class, and accessing the `ApiUrl` property directly from the object.

## Notes
- You must choose to use either the `Options<T>` pattern, or the `IConfigParametersProvider` approach. You cannot combine the two.
- The `IConfigParameters` method of _accessing_ config parameters is available using either approach.
- Use the `IConfigParametersProvider` when you need to dynamically render the config parameters. Using the `Options<T>` pattern requires knowing all the config options at compile time.
- Use the `IConfigParametersProvider` when you want to show more than one Schema page. The `Options<T>` pattern only supports a single Schema page.
- You can only create a single  `Options<T>` class for each config page.
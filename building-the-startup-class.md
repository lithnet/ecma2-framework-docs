# Building the Startup class
Once you have built your providers, you need to setup your Startup class.
This will be used to tell your framework how to load your providers, and provide the opporunity to add any additional services to the dependency injection container.

Create a new class, inheriting from `IEcmaStartup`. This class is where you register your services for dependency injection and configure any logging providers required. 

You'll need to add your implementations here. 
Any classes you have created that inherit from the following interfaces provided by the framework are added here.
- `ICapabilitiesProvider`
- `IObjectImportProvider`
- `IObjectExportProvider`
- `ISchemaProvider` 
- `IObjectPasswordProvider`
- `IContextInitializer`

You can add any other items you will need injected into classes. In the example below, we also create a HttpClient and make that availble to classes that need it. 

```cs
using System;
using System.Net.Http;
using System.Net.Http.Headers;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Options;

namespace Lithnet.Ecma2Framework.Example
{
    internal class Startup : IEcmaStartup
    {
        public void Configure(IConfigurationBuilder builder)
        {
        }

        public void SetupServices(IServiceCollection services, IConfigParameters configParameters)
        {
            services.AddSingleton<ICapabilitiesProvider, CapabilitiesProvider>();
            services.AddSingleton<IObjectImportProvider, UserImportProvider>();
            services.AddSingleton<ISchemaProvider, SchemaProvider>();

            services.AddSingleton<HttpClient>((services) =>
            {
                var options = services.GetRequiredService<IOptions<ConnectivityOptions>>();

                HttpClient client = new HttpClient();
                client.BaseAddress = new Uri(options.Value.ApiUrl);
                client.DefaultRequestHeaders.Accept.Clear();
                client.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
                return client;
            });
        }
    }
}
```
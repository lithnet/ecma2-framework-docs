# Defining management agent capabilities

MIM needs to know what capabilities your management agent has. In order to achieve this, we need to create a new class that inherits from `ICapabilitiesProvider`.

Here is an example of a `CapabilitiesProvider` class that implements the `GetCapabilitiesAsync` method:

```cs
using System.Threading.Tasks;
using Microsoft.MetadirectoryServices;

namespace Lithnet.Ecma2Framework.Example
{
    public class CapabilitiesProvider : ICapabilitiesProvider
    {
        public Task<MACapabilities> GetCapabilitiesAsync(IConfigParameters configParameters)
        {
            return Task.FromResult(
                new MACapabilities
                {
                    ConcurrentOperation = true,
                    DeltaImport = false,
                    DistinguishedNameStyle = MADistinguishedNameStyle.Generic,
                    SupportExport = false,
                    SupportImport = true
                });
        }
    }
}
 ```
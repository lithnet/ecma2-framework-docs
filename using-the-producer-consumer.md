# Using the producer/consumer import provider
The framework comes with an import provider that uses the producer/consumer pattern to generate your CSEntryChanges and pass them back to the MIM sync engine.

This class abstracts away a lot of the boilerplate associated with generating CSEntryChange objects, and paging their results back to the MIM sync engine.

At a minimum, the following methods must be implemented.
### `CanImportAsync`
This method tells the framework if this provider is capable of importing the specific object type. 

### `GetObjectsAsync`
This method is called at the start of the import operation. The method must return the models that represent the objects to be imported.

Typically this would be something like a 'get all users' call from the API. 

Yield new objects as soon as they are available, as the consumer thread will start picking them up and converting them to CSEntryChanges.

### `GetAnchorAttributesAsync`
Once an object has been picked up by the consumer thread, this method will be called to obtain the anchor attributes. Using the model passed into the method, create the relevant `AnchorAttribute` values and return them. They will be added to the resulting CSEntryChange

### `GetDNAsync`
The consumer thread will call out to this method and request the DN that should be used for the given model object.

### `GetObjectModificationTypeAsync`
The consumer thread will call out to this method to request the type of change to the object that is being processed. When in a full import operation, this will always be `Add`. In a delta import operation, determine the type of change that was made, and return the appopriate value.

### `CreateAttributeChangeAsync`
For each attribute in the schema, the consumer will call this method and ask for relevant AttributeChange objects for the schema attribute in question.

If there are no changes to the specified attribute, simply return null.

### `GetOutboundWatermark`
Once the producer thread has completed, this method is called to obtain the watermark value. This value will be provided on the next import to the `GetObjectsAsync` method. This allows a delta import to resume from the last known location.

If the management agent doesn't support delta imports, then simply return `null`.

```cs
using System.Collections.Generic;
using System.Net.Http;
using System.Runtime.CompilerServices;
using System.Text.Json;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Extensions.Logging;
using Microsoft.MetadirectoryServices;

namespace Lithnet.Ecma2Framework.Example
{
    internal class UserImportProvider : ProducerConsumerImportProvider<User>
    {
        private readonly HttpClient client;
        private readonly ILogger<UserImportProvider> logger;

        public UserImportProvider(HttpClient client, ILogger<UserImportProvider> logger) : base(logger)
        {
            this.client = client;
            this.logger = logger;
        }

        /// <summary>
        /// Determines if this provider can import objects of the specified type
        /// </summary>
        /// <param name="type">The type of object to import</param>
        public override Task<bool> CanImportAsync(SchemaType type)
        {
            return Task.FromResult(type.Name == "user");
        }

        /// <summary>
        /// Gets an enumerable of objects to import
        /// </summary>
        /// <param name="watermark">The incoming watermark for this object type</param>
        /// <param name="cancellationToken">A cancellation token</param>
        /// <returns>An enumerable of objects to import</returns>
        protected override async IAsyncEnumerable<User> GetObjectsAsync(string watermark, [EnumeratorCancellation] CancellationToken cancellationToken)
        {
            var result = await this.client.GetAsync(this.client.BaseAddress + "/users");

            result.EnsureSuccessStatusCode();

            var usersData = await result.Content.ReadAsStringAsync();

            var users = JsonSerializer.Deserialize<List<User>>(usersData);

            this.logger.LogInformation("Retrieved {count} users", users.Count);

            foreach (User user in users)
            {
                yield return user;
            }
        }

        /// <summary>
        /// This method gets the anchor attributes for the specified object
        /// </summary>
        /// <param name="item">The object returned from <see cref="GetObjectsAsync(string, CancellationToken)"/> which the anchor attributes are needed for</param>
        /// <returns>A list of anchor attributes</returns>
        protected override Task<List<AnchorAttribute>> GetAnchorAttributesAsync(User item)
        {
            List<AnchorAttribute> anchors = new List<AnchorAttribute>();
            anchors.Add(AnchorAttribute.Create("id", item.Id));
            return Task.FromResult(anchors);
        }

        /// <summary>
        /// This method builds the DN for the specified object
        /// </summary>
        /// <param name="item">The object returned from <see cref="GetObjectsAsync(string, CancellationToken)"/> which the DN is needed for</param>
        /// <returns></returns>
        protected override Task<string> GetDNAsync(User item)
        {
            return Task.FromResult(item.Id);
        }

        /// <summary>
        /// This method gets the modification type for the specified object. When performing a full import, this should always be <see cref="ObjectModificationType.Add"/>
        /// </summary>
        /// <param name="item">The object returned from <see cref="GetObjectsAsync(string, CancellationToken)"/> which the modification type is needed for</param>
        /// <returns>The type of modification to report for this object</returns>
        protected override Task<ObjectModificationType> GetObjectModificationTypeAsync(User item)
        {
            return Task.FromResult(ObjectModificationType.Add);
        }

        /// <summary>
        /// Creates an attribute change for the specified schema attribute
        /// </summary>
        /// <param name="type">The schema attribute to create the change for</param>
        /// <param name="modificationType">The type of modification taking place on this object</param>
        /// <param name="item">The object returned from <see cref="GetObjectsAsync(string, CancellationToken)"/> which the attribute change is needed for</param>
        /// <param name="cancellationToken">A cancellation token</param>
        /// <returns>An attribute change, or null if there are no changes to report for the given attribute</returns>
        protected override Task<AttributeChange> CreateAttributeChangeAsync(SchemaAttribute type, ObjectModificationType modificationType, User item, CancellationToken cancellationToken)
        {
            switch (type.Name)
            {
                case "name":
                    return Task.FromResult(AttributeChange.CreateAttributeAdd(type.Name, item.Name));

                case "email":
                    return Task.FromResult(AttributeChange.CreateAttributeAdd(type.Name, item.Email));

                case "phone":
                    return Task.FromResult(AttributeChange.CreateAttributeAdd(type.Name, item.Phone));
            }

            return Task.FromResult<AttributeChange>(null);
        }

        /// <summary>
        /// Optionally provides an outbound watermark value for the specified object type
        /// </summary>
        /// <param name="type">The object type to get the watermark for</param>
        /// <param name="cancellationToken">A cancellation token</param>
        /// <returns>An outbound watermark, or null if the management agent doesn't support delta operations</returns>
        public override Task<string> GetOutboundWatermark(SchemaType type, CancellationToken cancellationToken)
        {
            return Task.FromResult<string>(null);
        }
    }
}


```
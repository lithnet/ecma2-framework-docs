# Defining the schema

To define the schema for your management agent, you need to create a new schema provider class that inherits from the `ISchemaProvider` interface. This class will be responsible for providing the schema definition.

Let's break down how the provided example works:

1. Inheriting from `ISchemaProvider`:

The `SchemaProvider` class implements the `ISchemaProvider` interface, which requires the implementation of the `GetMmsSchemaAsync` method. This method returns a `Task<Schema>` object representing the schema.

2. Defining the schema:

The `GetMmsSchemaAsync` method creates a new instance of the `Schema` class, which represents the entire schema for the management agent. It then adds a single schema type, "user", to the `Schema` object by calling the `GetSchemaTypeUser` method.

3. Defining schema attributes:

The `GetSchemaTypeUser` method creates a new instance of the `SchemaType` class, representing a specific type within the schema. In this case, the type is "user". It defines attributes such as "id", "name", "email", and "phone" using the appropriate methods.

4. Returning the schema:

Once the schema is defined, the `GetMmsSchemaAsync` method returns the `Schema` object wrapped in a completed `Task` using the `Task.FromResult` method.

In summary, the `SchemaProvider` class defines a schema for a data model by creating a `Schema` object, adding a "user" type with specific attributes, and returning the schema through the `GetMmsSchemaAsync` method. This allows other components of the application to access and utilize the defined schema for various purposes, such as data import and export.

 ```cs
using System.Threading.Tasks;
using Microsoft.MetadirectoryServices;

namespace Lithnet.Ecma2Framework.Example
{
    internal class SchemaProvider : ISchemaProvider
    {
        public Task<Schema> GetMmsSchemaAsync()
        {
            Schema mmsSchema = new Schema();
            mmsSchema.Types.Add(this.GetSchemaTypeUser());

            return Task.FromResult(mmsSchema);
        }

        private SchemaType GetSchemaTypeUser()
        {
            SchemaType mmsType = SchemaType.Create("user", true);
            SchemaAttribute mmsAttribute = SchemaAttribute.CreateAnchorAttribute("id", AttributeType.String, AttributeOperation.ImportOnly);
            mmsType.Attributes.Add(mmsAttribute);

            mmsAttribute = SchemaAttribute.CreateSingleValuedAttribute("name", AttributeType.String, AttributeOperation.ImportExport);
            mmsType.Attributes.Add(mmsAttribute);

            mmsAttribute = SchemaAttribute.CreateSingleValuedAttribute("email", AttributeType.String, AttributeOperation.ImportExport);
            mmsType.Attributes.Add(mmsAttribute);

            mmsAttribute = SchemaAttribute.CreateSingleValuedAttribute("phone", AttributeType.String, AttributeOperation.ImportExport);
            mmsType.Attributes.Add(mmsAttribute);

            return mmsType;
        }
    }
}

## Configuration parameters
You can get the configuration parameters set for the management agent, by injecting `IConfigParameters` into your classes constructor.


 ```cs
using System.Threading.Tasks;
using Microsoft.MetadirectoryServices;

namespace Lithnet.Ecma2Framework.Example
{
    internal class SchemaProvider : ISchemaProvider
    {
        private readonly IConfigurationParameters configParameters;

        public SchemaProvider(IConfigurationParameters configParameters)
        {
            this.configParameters = configParameters;
        }

        // Class implementation
    }
}
```

If you are using the `Options<T>` pattern for configuration, then simply inject the relevant strongly-typed options objects into your class.

 ```cs
using System.Threading.Tasks;
using Microsoft.MetadirectoryServices;

namespace Lithnet.Ecma2Framework.Example
{
    internal class SchemaProvider : ISchemaProvider
    {
        private readonly SchemaOptions schemaOptions;

        public SchemaProvider(IOptions<SchemaOptions> schemaOptions)
        {
            this.schemaOptions = schemaOptions.Value;
        }

        // Class implementation
    }
}
```
# `swagger.config.ts`

The `swagger.config.ts` file is a configuration file used for setting up Swagger (now known as OpenAPI) documentation in a Fastify application. Swagger is widely used for designing, building, documenting, and consuming RESTful web services. The configuration defined in this file helps in generating interactive API documentation that can be used by developers to understand the API endpoints and their functionalities.

## Configuration Details

Below is a detailed explanation of the configuration settings provided in the `swagger.config.ts` file.

```typescript
export const swaggerConfig = {
  swagger: {
    info: {
      title: "RESTful APIs using Fastify",
      description: "CRUDs using Swagger, Fastify and Prisma",
      version: "0.0.1",
    },
    externalDocs: {
      url: "https://swagger.io",
      description: "Find more info here",
    },
    schemes: ["http"],
    consumes: ["application/json"],
    produces: ["application/json"],
  },
};
```

### Configuration Object Breakdown

- **`info`**: This object contains metadata about the API.

  - **`title`**: The title of the application or API.
  - **`description`**: A short description of what the API does.
  - **`version`**: The version of the API.

- **`externalDocs`**: This object provides additional documentation that is external to the Swagger documentation.

  - **`url`**: A URL where more information can be obtained.
  - **`description`**: A brief description of what the external documentation offers.

- **`schemes`**: An array of transfer protocols supported by the API. In this case, it's only HTTP.

- **`consumes`**: An array of MIME types the API can consume. This is set to `application/json`, meaning the API expects to receive JSON formatted requests.

- **`produces`**: An array of MIME types the API can produce. Similar to `consumes`, this is set to `application/json`, indicating that the API will send responses in JSON format.

## Usage

This configuration is typically imported and used in the Fastify application setup file where the Swagger plugin is registered. Registering this configuration enables automatic generation of API documentation based on routes and schema definitions provided in the Fastify server instance.

## Benefits

- **Interactive Documentation**: Allows interactive exploration of API routes, making it easier for frontend developers and API consumers to understand and test the API.
- **Standardization**: Adheres to the Swagger/OpenAPI standards, which are widely recognized and used across the industry.
- **Automation**: Automatically generates up-to-date API documentation, reducing the manual effort required to keep documentation in sync with the codebase.

In summary, the `swagger.config.ts` file plays a crucial role in setting up automatic and standardized API documentation for Fastify applications using Swagger, facilitating better developer experience and API usability.

# Environment Configuration Documentation

This documentation provides detailed information about the `env.config.ts` file, which is responsible for defining and configuring the environmental variables used within a Fastify application. The environment configuration ensures that the application can access necessary settings like database URL, server binding address, and port through a structured schema.

## Overview

`env.config.ts` exports a single configuration object named `Config`, which integrates with the Fastify environment plugin to validate and parse environment variables based on a predefined schema.

## Configuration Details

Here's a breakdown of the `Config` object:

- **confKey**: A string that represents the key under which the configuration will be available in the Fastify instance.
- **schema**: An object that describes the structure, requirements, and default values of the environment variables.

### Schema Structure

The schema object is detailed as follows:

| Property          | Type    | Required | Default Value  | Description                                                                 |
| ----------------- | ------- | -------- | -------------- | --------------------------------------------------------------------------- |
| `BIND_PORT`       | number  | No       | `5000`         | The port number on which the server listens.                                |
| `BIND_ADDR`       | string  | No       | `127.0.0.1`    | The IP address on which the server binds.                                   |
| `APP_SERVER_NAME` | string  | No       | `localhost`    | The name of the server, used internally for identification.                 |
| `PROJECT_NAME`    | string  | No       | `fastify-rest` | The name of the project, used for logging or other identification purposes. |
| `DATABASE_URL`    | string  | Yes      | None           | The URL for the database connection. Required for database operations.      |
| `ENABLE_SWAGGER`  | boolean | No       | `true`         | Flag to enable or disable Swagger documentation generation.                 |

### Required Variables

- `DATABASE_URL`: This is a mandatory variable as it's essential for connecting to the database.

## Default Values

Default values are provided for some environment variables, ensuring the application can run with minimal configuration in a development environment:

- **BIND_PORT**: Defaults to `5000`.
- **BIND_ADDR**: Defaults to `127.0.0.1`.
- **APP_SERVER_NAME**: Defaults to `localhost`.
- **PROJECT_NAME**: Defaults to `fastify-rest`.
- **ENABLE_SWAGGER**: Defaults to `true`.

## Usage

To use these configurations, the Fastify environment plugin reads the `Config` object, validates the environment variables against the schema, and makes them available through the Fastify instance. Example usage in a Fastify setup might look like this:

```typescript
import fastify from "fastify";
import envConfig from "./env.config";

const app = fastify();

app.register(require("@fastify/env"), envConfig);

app.ready((err) => {
  if (err) console.error(err);
  console.log(app.config); // Access the validated and parsed configuration
});
```

## Conclusion

The `env.config.ts` file plays a critical role in setting up environment-based configurations for a Fastify application, ensuring that essential variables are defined, validated, and easily accessible throughout the application. This setup promotes a structured approach to configuration management, aiding in maintaining clean and robust application setups.

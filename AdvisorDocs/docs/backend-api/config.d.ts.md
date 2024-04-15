# `config.d.ts`

The `config.d.ts` file is a TypeScript declaration file used within a Fastify project. This file extends the Fastify library's core types to include custom configuration options that are specific to the application. This approach allows for strongly-typed access to configuration variables throughout the application, enhancing development experience with type checking and autocompletion features.

## Overview

The purpose of this file is to declare a module augmentation for the `FastifyInstance` interface from the `fastify` package. This augmentation adds a new `config` property to the `FastifyInstance` interface, which includes several environment-specific settings that are crucial for the application's operation.

## Detailed Description

### FastifyInstance Extension

- **Interface**: `FastifyInstance`
- **Module**: `fastify`

The `config` property added to the `FastifyInstance` includes the following fields:

| Field             | Type                                      | Description                                                        |
| ----------------- | ----------------------------------------- | ------------------------------------------------------------------ |
| `NODE_ENV`        | `'development' \| 'production' \| 'test'` | The environment in which the application is running.               |
| `BIND_PORT`       | `number`                                  | The port number on which the application server should bind.       |
| `BIND_ADDR`       | `string`                                  | The IP address on which the application server should bind.        |
| `PROJECT_NAME`    | `string`                                  | The name of the project.                                           |
| `APP_SERVER_NAME` | `string`                                  | A custom name for the application server.                          |
| `DATABASE_URL`    | `string`                                  | The URL to the database used by the application.                   |
| `ENABLE_SWAGGER`  | `boolean`                                 | Flag to determine whether Swagger documentation should be enabled. |

### Example Usage

In a Fastify server setup file, you could access these configuration options like so:

```typescript
import { FastifyInstance } from "fastify";

const startServer = async (fastify: FastifyInstance) => {
  console.log(fastify.config.NODE_ENV); // Access the NODE_ENV from config
  fastify.listen(fastify.config.BIND_PORT, fastify.config.BIND_ADDR);
};

export default startServer;
```

### Benefits

Using this declaration file offers the following benefits:

1. **Type Safety**: Ensures that the configuration options are accessed correctly throughout the application, reducing runtime errors due to typos or incorrect types.
2. **Autocompletion**: Enhances developer productivity by providing autocompletion for configuration options in IDEs that support TypeScript.
3. **Centralization**: Centralizes the configuration schema definition, making it easier to manage and refactor.

### Conclusion

The `config.d.ts` file is an essential part of setting up a TypeScript-based Fastify application, providing type definitions for custom configuration that can be used reliably across the application codebase. This setup ensures maintainability and scalability of the application configuration management.

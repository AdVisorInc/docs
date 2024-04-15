# `prisma.plugin.ts`

This documentation provides a comprehensive overview of the `prisma.plugin.ts` file used in a Fastify application. The functionality revolves around integrating Prisma into the Fastify framework as a reusable plugin.

## Overview

The `prisma.plugin.ts` file defines a plugin for the Fastify framework that integrates Prisma as an ORM (Object-Relational Mapping) tool. This plugin is responsible for adding Prisma's capabilities directly to the Fastify instance, allowing the application to interact with a database using Prisma's client.

## Detailed Components

### Import Statements

```typescript
import fp from "fastify-plugin";
import { FastifyInstance, FastifyPluginAsync } from "fastify";
import { PrismaClient } from "@prisma/client";
```

- `fastify-plugin`: Utility to create Fastify plugins.
- `FastifyInstance, FastifyPluginAsync`: Fastify types for plugin and instance.
- `PrismaClient`: Main class from Prisma that interacts with the database.

### Prisma Plugin

```typescript
const prismaPlugin: FastifyPluginAsync = fp(async function prismaPlugin(
  fastify: FastifyInstance
) {
  const prisma = new PrismaClient();
  fastify.decorate("prisma", prisma);

  fastify.addHook("onClose", async (instance) => {
    await instance.prisma.$disconnect();
  });
});
```

- **Function `prismaPlugin`**: A function that takes a `FastifyInstance` and asynchronously sets up Prisma.
  - **Prisma Client Initialization**: A new instance of `PrismaClient` is created.
  - **Decoration**: The Fastify instance is decorated with the Prisma client, making it accessible throughout the application via `fastify.prisma`.
  - **Hook 'onClose'**: Ensures that the Prisma client disconnects from the database when the Fastify server is closed. This is crucial for cleanly shutting down the application and releasing database resources.

### Export

```typescript
export default prismaPlugin;
```

The Prisma plugin is exported as a default export, making it easy to include and use in the main application or other parts of the system that utilize plugins.

## Usage

To use this plugin in a Fastify application:

1. Import the plugin: `import prismaPlugin from './prisma.plugin';`
2. Register the plugin with the Fastify instance:
   ```typescript
   fastify.register(prismaPlugin);
   ```

## Conclusion

The `prisma.plugin.ts` file encapsulates the initialization and lifecycle management of the Prisma client within a Fastify application, promoting good practices such as proper resource management and modularity. This setup not only makes the Prisma client readily available throughout the Fastify application but also ensures that connections are properly closed when the application shuts down. This integration leverages Fastify's plugin system for a clean and efficient setup.

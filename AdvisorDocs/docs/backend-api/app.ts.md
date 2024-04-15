# `app.ts`

The `app.ts` file is a key component of the server application, responsible for setting up the Fastify server with all its configurations, plugins, routes, and middleware. Below is a detailed breakdown of its functionalities, configurations, and integrations.

## Overview

`app.ts` initializes and configures a Fastify server instance with various plugins and middleware to handle environment variables, CORS, compression, security headers, and optionally Swagger documentation. It also sets up API routes and integrates Prisma for ORM support.

## Table of Contents

- [Imports](#imports)
- [Function: main](#function-main)
- [Server Initialization](#server-initialization)
- [Plugin Registrations](#plugin-registrations)
- [Schema Definitions](#schema-definitions)
- [Swagger Documentation](#swagger-documentation)
- [API Endpoints](#api-endpoints)
- [Export](#export)

## Imports

The file begins with several imports, each serving a specific purpose in setting up the server:

```typescript
import fastify from "fastify";
import fastifyEnv from "@fastify/env";
import fastifyCors from "@fastify/cors";
import fastifyCompress from "@fastify/compress";
import fastifyHelmet from "@fastify/helmet";
import fastifySwagger from "@fastify/swagger";
import fastifySwaggerUi from "@fastify/swagger-ui";
import envConfig from "./lib/env.config";
import corsConfig from "./config/cors.config";
import loggerConfig from "./config/logger.config";
import compressConfig from "./config/compress.config";
import prismaPlugin from "./plugins/prisma.plugin";
import helmetConfig from "./config/helmet.config";
import { swaggerConfig } from "./config/swagger.config";
import {
  messageSchema,
  paramIdSchema,
  paginationSchema,
} from "./schema/common.schema";
import googleRoutes from "./routes/google.routes";
```

## Function: main

The `main` function is an asynchronous function responsible for configuring and returning a Fastify server instance.

### Server Initialization

A new Fastify server is created with a logging configuration:

```typescript
const app = fastify({ logger: loggerConfig });
```

### Plugin Registrations

Several plugins are registered to the server to handle various functionalities:

- **Environment Variables:** Configured via `fastifyEnv` using settings from `envConfig`.
- **CORS:** Set up using `fastifyCors` with configurations imported from `corsConfig`.
- **Compression:** Managed by `fastifyCompress` with settings from `compressConfig`.
- **Security Headers:** Handled by `fastifyHelmet` using `helmetConfig`.
- **ORM Integration:** Prisma plugin is registered to integrate Prisma ORM.

```typescript
await app.register(fastifyEnv, envConfig);
await app.register(fastifyCors, corsConfig);
await app.register(fastifyCompress, compressConfig);
await app.register(fastifyHelmet, helmetConfig);
await app.register(prismaPlugin);
```

### Schema Definitions

Common JSON schemas (`paginationSchema`, `paramIdSchema`, `messageSchema`) are added to the Fastify instance:

```typescript
app.addSchema(paginationSchema);
app.addSchema(paramIdSchema);
app.addSchema(messageSchema);
```

### Swagger Documentation

If Swagger is enabled in the configuration, the server registers the Swagger plugins and sets up a route to redirect the root URL to the Swagger UI documentation:

```typescript
if (app.config.ENABLE_SWAGGER) {
  await app.register(fastifySwagger, swaggerConfig);
  await app.register(fastifySwaggerUi, { routePrefix: "/docs" });
  app.get("/", async (request, reply) => {
    reply.redirect("/docs");
  });
}
```

### API Endpoints

API endpoint routes are registered under a specific versioning prefix (`/api/v1`). The `googleRoutes` are loaded under another prefix (`/google`):

```typescript
await app.register(
  async (api) => {
    api.register(googleRoutes, { prefix: "/google" });
  },
  { prefix: "/api/v1" }
);
```

## Export

The `main` function is exported for use in other parts of the application, such as the entry point `index.ts`:

```typescript
export { main };
```

## Summary

The `app.ts` file orchestrates the setup and configuration of the Fastify server, integrating essential middleware, plugins, and routes to ensure the server is robust, secure, and ready to handle requests according to defined API specifications.

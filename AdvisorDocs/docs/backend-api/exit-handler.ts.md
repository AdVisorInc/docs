# `exit-handler.ts`

The `exit-handler.ts` module is designed to manage the application's shutdown process, ensuring that the application closes gracefully under different circumstances, such as unhandled exceptions or manual interruptions. This is critical for releasing resources properly and avoiding potential data corruption or inconsistencies.

## Functions

This file defines three primary functions to handle different types of application termination scenarios:

### 1. `exitHandler`

**Purpose**: Safely close the Fastify server instance and exit the application with a provided exit code.

**Parameters**:

- `app`: `FastifyInstance` - The instance of the Fastify server.
- `exitCode`: `number` - The exit code with which the process will terminate.

**Implementation Details**:

- The function calls `app.close()` to stop the Fastify server.
- Once the server is closed, it logs the closure and then exits the process with the specified `exitCode`.

```typescript
const exitHandler = (app: FastifyInstance, exitCode: number) => {
  app.close(() => {
    app.log.info("Server closed");
    process.exit(exitCode);
  });
};
```

### 2. `unexpectedErrorHandler`

**Purpose**: Handle unexpected errors by logging the error and then shutting down the application with an error exit code.

**Parameters**:

- `app`: `FastifyInstance` - The instance of the Fastify server.
- `error`: `any` - The error object caught by the process.

**Implementation Details**:

- Logs the error using `app.log.error`.
- Calls `exitHandler` with an exit code of `1` to indicate an error-led shutdown.

```typescript
const unexpectedErrorHandler = (app: FastifyInstance, error: any) => {
  app.log.error(error);
  exitHandler(app, 1);
};
```

### 3. `gracefullyShutdown`

**Purpose**: Initiate a graceful shutdown process, logging the intent and then closing the application with a success exit code.

**Parameters**:

- `app`: `FastifyInstance` - The instance of the Fastify server.

**Implementation Details**:

- Logs the information about attempting a graceful shutdown.
- Calls `exitHandler` with an exit code of `0`, indicating a normal shutdown.

```typescript
const gracefullyShutdown = (app: FastifyInstance) => {
  app.log.info("Attempting to gracefully shutdown the app...");
  exitHandler(app, 0);
};
```

## Usage and Integration

These functions are typically used in conjunction with Node.js global error handlers and signal listeners to manage different shutdown scenarios:

- `unexpectedErrorHandler` is used for handling uncaught exceptions and unhandled promise rejections.
- `gracefullyShutdown` is used for handling termination signals such as `SIGTERM` and `SIGINT`, which are commonly used in containerized environments or during server maintenance.

By centralizing the shutdown logic, `exit-handler.ts` helps maintain a clean and manageable approach towards handling application termination, ensuring that resources are properly cleaned up and that the application does not exit prematurely or without proper clean-up activities in the event of errors or manual termination requests.

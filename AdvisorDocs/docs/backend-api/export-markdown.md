# `index.ts`

## Overview

The `index.ts` file serves as the entry point for a Node.js application. It is responsible for initializing the application by importing and invoking functions from other modules. This file also handles various types of process-level exceptions and signals to ensure graceful shutdowns and error handling.

## Code Structure

```typescript
import { main } from "./app";
import { gracefullyShutdown, unexpectedErrorHandler } from "./lib/exit-handler";

/* * Build service */
main()
  .then((app) => {
    // Handle uncaught exceptions and unhandled promise rejections
    process.on("uncaughtException", (err) => unexpectedErrorHandler(app, err));
    process.on("unhandledRejection", (err) => unexpectedErrorHandler(app, err));

    // Handle termination signals for graceful shutdown
    process.on("SIGTERM", () => gracefullyShutdown(app));
    process.on("SIGINT", () => gracefullyShutdown(app));

    /* * Start the server */
    app
      .listen({
        port: app.config.BIND_PORT,
        host: app.config.BIND_ADDR,
      })
      .then((_) => {
        app.log.info("Ready, Waiting for connections...");
      })
      .catch((err) => {
        app.log.error(
          {
            addr: app.config.BIND_ADDR,
            port: app.config.BIND_PORT,
            error: err.message,
          },
          "Failed to start server"
        );
      });
  })
  .catch((err) => {
    console.log(err);
    process.exit(1);
  });
```

## Key Components

### Import Statements

- **`main` function from `./app`**: This function is expected to initialize and configure the application, returning an instance that can be used to start the server and handle logging.
- **`gracefullyShutdown` and `unexpectedErrorHandler` from `./lib/exit-handler`**: These functions handle graceful shutdowns of the application and unexpected errors respectively.

### Application Initialization and Server Startup

- **`main()` function invocation**: Calls the `main` function which sets up the application.
  - **`.then(app => {...})`**: Upon successful setup, the `app` object is used to configure server listeners and error handlers.
  - **`process.on(...)` event handlers**:
    - **`uncaughtException` and `unhandledRejection`**: Captures uncaught exceptions and unhandled promise rejections, passing them to `unexpectedErrorHandler` for logging and potential recovery actions.
    - **`SIGTERM` and `SIGINT`**: Listens for termination signals to trigger `gracefullyShutdown`, allowing the application to close connections and cleanup resources before shutting down.
  - **`app.listen(...)`**: Starts the server using the configuration specified in `app.config`. Logs success or failure messages based on the outcome of the server startup process.
- **`.catch(err => {...})`**: Catches any error that occurs during the initial setup phase and logs it before exiting the process with a non-zero status code.

## Detailed Function Descriptions

### `main()`

- **Purpose**: Initializes the application with all necessary configurations and middleware.
- **Returns**: A promise that resolves to the application instance.

### `unexpectedErrorHandler(app, err)`

- **Purpose**: Handles unexpected errors by logging them and potentially performing cleanup tasks.
- **Parameters**:
  - `app`: The application instance.
  - `err`: The error object.
- **Returns**: None.

### `gracefullyShutdown(app)`

- **Purpose**: Performs necessary cleanup operations and shuts down the application gracefully.
- **Parameters**:
  - `app`: The application instance.
- **Returns**: None.

## Conclusion

The `index.ts` file is crucial for setting up the application, handling errors, and ensuring that the server can respond to termination signals appropriately for a graceful shutdown. It plays a fundamental role in maintaining the robustness and reliability of the application during runtime.

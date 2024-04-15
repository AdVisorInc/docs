# `logger.config.ts`

## Overview

The `logger.config.ts` file configures the logging behavior for a Fastify application based on the environment in which it is running. It utilizes Pino, a very low overhead Node.js logger, for logging purposes. The configuration differs between development and production environments to adapt to the varying needs such as debugging in development and performance in production.

## Configuration Details

### Environment Configurations

- **Development**:

  - **Level**: `debug` - Logs everything at debug level and above, which is useful for development when more verbose logs are helpful for debugging.
  - **Transport**:
    - **Target**: `pino-pretty` - This makes the log output more human-readable.
    - **Options**:
      - **TranslateTime**: `'HH:MM:ss Z'` - Formats the timestamp in a human-readable form.
      - **Ignore**: `'pid,hostname'` - Avoids logging the process ID and hostname to keep the logs cleaner.

- **Production**:
  - Logs are set to a truthy value (`true`), meaning that logging is enabled with default settings optimized for production use. This likely focuses on higher log levels (e.g., error) and minimal output for performance reasons.

### Function: `getConfig`

- **Purpose**: Determines the appropriate logging configuration based on the current environment.
- **Parameters**: None.
- **Returns**: Based on the environment, it returns either:
  - A `PinoLoggerOptions` object for 'development'.
  - A boolean (`true`) for 'production'.
  - `false` for any environment that's neither 'development' nor 'production', effectively disabling logging.

#### Usage

```typescript
import getConfig from "./logger.config";

const loggerOptions = getConfig();
```

This function checks the `NODE_ENV` environment variable and returns the corresponding configuration. If `NODE_ENV` is not set, it defaults to `development`.

## Summary

This configuration module is crucial for tailoring the logging behavior of the application to match the operational environment, enhancing both the development experience and production performance. By separating the configurations, developers can ensure that the application logs sufficient information during development for debugging, while keeping the production logs optimized for performance and security.

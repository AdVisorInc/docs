# `google.controller.ts`

## Overview

The `google.controller.ts` file defines controller functions for handling Google Ads-related operations in a Fastify application. It integrates with the Google Ads API to perform various tasks, such as importing campaigns, listing accessible customers, and fetching customer names based on a given customer ID.

## Functions

### `importCampaigns`

- **Purpose**: Imports Google Ads campaigns using a provided refresh token.
- **Parameters**:
  - `request`: FastifyRequest - Contains the request details and body.
  - `reply`: FastifyReply - Used to send back the server responses.
- **Returns**: Sends a JSON response with either the imported campaigns or an error message.
- **Errors**:
  - Returns HTTP 400 if the refresh token is missing.
  - Returns HTTP 500 if there is an error during the import process.

### `listAccessibleCustomers`

- **Purpose**: Lists accessible Google Ads customer IDs and names using a provided refresh token.
- **Parameters**:
  - `request`: FastifyRequest - Contains the request details and body.
  - `reply`: FastifyReply - Used to send back the server responses.
- **Returns**: Sends a JSON response with either the list of accessible customers or an error message.
- **Errors**:
  - Returns HTTP 400 if the refresh token is missing.
  - Returns HTTP 500 if there is an error during the listing process.

### `getCustomerName`

- **Purpose**: Retrieves the name of a Google Ads customer by customer ID using a provided refresh token.
- **Parameters**:
  - `request`: FastifyRequest - Contains the request details and body.
  - `reply`: FastifyReply - Used to send back the server responses.
- **Returns**: Sends a JSON response with either the customer's name or an error message.
- **Errors**:
  - Returns HTTP 500 if there is an error during the fetch process.

## Implementation Details

- Controllers make use of `google-ads-api` client for interacting with Google Ads services.
- Error handling is done using try-catch blocks, and appropriate HTTP status codes are returned based on the type of error.
- Refresh tokens are used for authentication with the Google Ads API.
- The Google Ads API methods used include `listAccessibleCustomers` and `Customer` for various customer and campaign related operations.

## Usage Example

These controllers can be hooked up to routes in a Fastify application to provide endpoints for Google Ads operations. For example, routes can be defined to handle POST requests for importing campaigns, listing accessible customers, and fetching customer names, which then utilize these controllers to interact with the Google Ads API.

```javascript
fastify.post("/import-campaigns", googleController.importCampaigns);
fastify.post("/list-customers", googleController.listAccessibleCustomers);
fastify.post("/get-customer-name", googleController.getCustomerName);
```

Each function is designed to be asynchronous to handle API calls efficiently and uses JavaScript promises for handling asynchronous data. The responses are sent back in JSON format, making it easy for clients to parse and use the data.

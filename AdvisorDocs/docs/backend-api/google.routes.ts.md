# `google.routes.ts`

## Overview

The `google.routes.ts` file is a part of the routing mechanism within a Fastify-based application, particularly focusing on routes related to Google Ads operations. This file sets up API endpoints to handle requests for importing campaigns, listing accessible customers, and retrieving the name of a Google Ads customer. It integrates specific controller functions and validation schemas to manage the requests and responses effectively.

## Routes Definition

The file defines three POST routes within the Fastify framework:

1. **Import Campaigns**
2. **List Accessible Customers**
3. **Get Customer Name**

Each route is associated with a controller function and a validation schema to ensure that incoming requests comply with the expected format.

### Route: `/import-campaigns`

- **Method:** POST
- **Controller Function:** `importCampaigns`
- **Schema:** `importCampaignsSchema`
- **Description:** This endpoint allows users to import Google Ads campaigns using a refresh token provided in the request body.

### Route: `/list-accessible-customers`

- **Method:** POST
- **Controller Function:** `listAccessibleCustomers`
- **Schema:** `listAccessibleCustomersSchema`
- **Description:** This endpoint provides a list of accessible customer IDs and names from Google Ads, requiring a refresh token.

### Route: `/get-customer-name`

- **Method:** POST
- **Controller Function:** `getCustomerName`
- **Schema:** `getCustomerNameSchema`
- **Description:** This endpoint retrieves the descriptive name of a Google Ads customer based on a provided customer ID and refresh token.

## Code Structure

```typescript
// Import necessary modules and functions
import { FastifyInstance } from "fastify";
import {
  getCustomerName,
  importCampaigns,
  listAccessibleCustomers,
} from "../controllers/google.controller";
import {
  getCustomerNameSchema,
  importCampaignsSchema,
  listAccessibleCustomersSchema,
} from "../schema/google.schema";

// Define and export the function to set up the routes
export default async function (fastify: FastifyInstance) {
  fastify.post(
    "/import-campaigns",
    { schema: importCampaignsSchema },
    importCampaigns
  );
  fastify.post(
    "/list-accessible-customers",
    { schema: listAccessibleCustomersSchema },
    listAccessibleCustomers
  );
  fastify.post(
    "/get-customer-name",
    { schema: getCustomerNameSchema },
    getCustomerName
  );
}
```

## Details

- **FastifyInstance:** This is the instance of the Fastify application. It is used to register routes and their respective handlers.
- **Schemas:** Defined in `google.schema.ts`, these JSON schemas validate the request bodies and structure the responses for consistency and reliability.
- **Controllers:** Functions from `google.controller.ts` handle the business logic for each endpoint, interacting with Google Ads API as needed.

## Usage

To use these routes, the Fastify instance must register this module. Each route expects POST requests with specific parameters and returns responses based on the operation outcomes, adhering to the defined schemas.

## Exception Handling

Each controller function is designed to handle exceptions internally, ensuring that appropriate HTTP response statuses and messages are returned to the client, thereby promoting robust error handling and client-friendly error messages.

---

This documentation provides a concise overview and technical details necessary for understanding and utilizing the `google.routes.ts` routes within the larger application context.

# `google.schema.ts`

The `google.schema.ts` file defines JSON schemas for various API endpoints related to Google Ads operations within a Fastify application. These schemas are crucial for validating the structure of incoming requests and formatting outgoing responses correctly. Below are the details of each schema defined in this file.

## Table of Contents

1. [importCampaignsSchema](#importcampaignsschema)
2. [listAccessibleCustomersSchema](#listaccessiblecustomersschema)
3. [getCustomerNameSchema](#getcustomernameschema)

---

## importCampaignsSchema

This schema is used for the endpoint that imports Google Ads campaigns.

**Endpoint Tags**: `Google Ads`

**Description**:

- **Purpose**: Import Google Ads campaigns.
- **Body Requirements**:
  - `refreshToken`: A required string that authenticates the request.
- **Responses**:
  - `200`: Successful import of campaigns, returns an array of campaign objects.
  - `400` and `500`: Error responses, which refer to a common message response schema for error details.

**Body Schema**:

```json
{
  "type": "object",
  "required": ["refreshToken"],
  "properties": {
    "refreshToken": {
      "type": "string"
    }
  }
}
```

**Response Schema (200 OK)**:

```json
{
  "type": "object",
  "properties": {
    "campaigns": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": { "type": "string" },
          "name": { "type": "string" },
          "status": { "type": "string" },
          "start_date": { "type": "string" },
          "end_date": { "type": "string" }
        }
      }
    }
  }
}
```

---

## listAccessibleCustomersSchema

This schema supports the endpoint to list accessible Google Ads customer IDs and names.

**Endpoint Tags**: `Google Ads`

**Description**:

- **Purpose**: List accessible Google Ads customer IDs and names.
- **Body Requirements**:
  - `refreshToken`: A required string that authenticates the request.
- **Responses**:
  - `200`: Successfully lists customers, returns an array of customer objects.
  - `400` and `500`: Error responses, which refer to a common message response schema for error details.

**Body Schema**:

```json
{
  "type": "object",
  "required": ["refreshToken"],
  "properties": {
    "refreshToken": {
      "type": "string"
    }
  }
}
```

**Response Schema (200 OK)**:

```json
{
  "type": "object",
  "properties": {
    "customers": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "resourceName": { "type": "string" },
          "id": { "type": "string" },
          "name": { "type": "string", "nullable": true }
        }
      }
    }
  }
}
```

---

## getCustomerNameSchema

This schema defines the endpoint for fetching a Google Ads customer's name by their ID.

**Endpoint Tags**: `Google Ads`

**Description**:

- **Purpose**: Get Google Ads customer name by ID.
- **Body Requirements**:
  - `refreshToken`: A required string that authenticates the request.
  - `customerId`: A required string that specifies the customer ID.
- **Responses**:
  - `200`: Successfully retrieves the customer's name, returns an object containing the name.
  - `400` and `500`: Error responses, which refer to a common message response schema for error details.

**Body Schema**:

```json
{
  "type": "object",
  "required": ["refreshToken", "customerId"],
  "properties": {
    "refreshToken": {
      "type": "string"
    },
    "customerId": {
      "type": "string"
    }
  }
}
```

**Response Schema (200 OK)**:

```json
{
  "type": "object",
  "properties": {
    "name": { "type": "string" }
  }
}
```

---

This file ensures that the API handles Google Ads data consistently and adheres to specified formats, enhancing the reliability and maintainability of the codebase.

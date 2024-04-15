# Common Schema Documentation

The `common.schema.ts` file defines JSON schemas that are utilized throughout the application for validating and serializing data. These schemas ensure that the data exchanged between the client and the server adheres to specified formats and rules. Below are the detailed descriptions and use cases for each schema defined in the `common.schema.ts` file.

## Schemas

1. **Pagination Schema**
2. **Message Response Schema**
3. **Parameter ID Schema**

### 1. Pagination Schema

The pagination schema is designed for cursor-based pagination mechanisms. It validates the parameters used to control the pagination of data results, particularly in API responses that support fetching data in chunks/pages.

#### Schema Details:

- **ID:** `paginationSchema`
- **Type:** `object`
- **Properties:**
  - **take:** Specifies the number of items to fetch. It accepts predefined values (5, 10, 25) with a default value of 10.
  - **from:** Represents the cursor or starting point for data fetching. It matches the MongoDB document ID pattern.

#### Usage Example:

```json
{
  "take": 10,
  "from": "5f8d0d55b54764421b7156cd"
}
```

### 2. Message Response Schema

This schema is used for standardizing API responses that primarily convey a message, often used in error handling or simple notifications.

#### Schema Details:

- **ID:** `messageResponseSchema`
- **Type:** `object`
- **Properties:**
  - **message:** A string that contains the actual message to be delivered to the client.

#### Usage Example:

```json
{
  "message": "Operation successful."
}
```

### 3. Parameter ID Schema

The parameter ID schema is crucial for validating route parameters that include document identifiers, ensuring they conform to a specific format (e.g., MongoDB's ObjectID).

#### Schema Details:

- **ID:** `paramIdSchema`
- **Type:** `object`
- **Properties:**
  - **id:** The identifier that should match the MongoDB ObjectID pattern.

#### Usage Example:

```json
{
  "id": "5f8d0d55b54764421b7156cd"
}
```

## Conclusion

The schemas defined in `common.schema.ts` provide a reliable mechanism for data validation across the application, ensuring consistency, reliability, and adherence to standards. These schemas are integrated into various parts of the application to validate requests, standardize responses, and manage data pagination effectively.

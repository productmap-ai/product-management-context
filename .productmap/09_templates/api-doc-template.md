# API Documentation Template

> Draft — Templates

An API documentation template ensures that every endpoint is described consistently, reducing integration time for engineers and preventing support requests caused by ambiguous specifications.

---

## Purpose

<!-- What decision or outcome does this document support? -->

## Endpoint Overview

**Name:** [Human-readable endpoint name]
**Version:** [API version, e.g., v1]
**Base URL:** `https://api.example.com/v1`

## Authentication

<!-- Authentication method: Bearer token / API key / OAuth 2.0 -->
<!-- Header required: `Authorization: Bearer {token}` -->

## Request

**Method:** `GET` / `POST` / `PUT` / `PATCH` / `DELETE`
**URL:** `/resource/{id}`

### Headers

| Header | Required | Description |
|---|---|---|
| Authorization | Yes | `Bearer {access_token}` |
| Content-Type | Yes (POST/PUT/PATCH) | `application/json` |

### Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| id | string | Yes | Unique identifier of the resource |

### Query Parameters

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| | | | | |

### Request Body

```json
{
  "field": "value"
}
```

## Response

### 200 — Success

```json
{
  "id": "string",
  "field": "value",
  "created_at": "ISO 8601 timestamp"
}
```

### 4xx — Client Errors

| Status | Code | Description |
|---|---|---|
| 400 | bad_request | Invalid request body or parameters |
| 401 | unauthorized | Missing or invalid authentication |
| 404 | not_found | Resource does not exist |

### 5xx — Server Errors

| Status | Code | Description |
|---|---|---|
| 500 | internal_error | Unexpected server error |

## Examples

### Request Example

```bash
curl -X POST https://api.example.com/v1/resource \
  -H "Authorization: Bearer {token}" \
  -H "Content-Type: application/json" \
  -d '{"field": "value"}'
```

### Response Example

```json
{
  "id": "abc123",
  "field": "value",
  "created_at": "2024-01-15T10:30:00Z"
}
```

## Rate Limits

<!-- Requests per minute/hour, rate limit headers returned, retry-after behaviour. -->

## Related

- [Development](../04_delivery/development/development.md)
- [adr-template.md](./adr-template.md)

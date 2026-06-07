# API Test Guide

## Purpose
Verify correct operation of REST/GraphQL API endpoints.

## Test Targets
- HTTP methods (GET, POST, PUT, DELETE, PATCH)
- Request parameters (path, query, body, header)
- Response (status code, body, header)
- Authentication/Authorization
- Error responses

## Scenario Derivation Criteria

### 1. CRUD Basics
| Operation | Test Cases |
|-----------|------------|
| Create | Normal creation, missing required fields, duplicate data |
| Read | Existing resource, non-existing resource, list query |
| Update | Full update, partial update, update non-existing |
| Delete | Normal delete, delete non-existing, related data |

### 2. Status Codes
| Code | Scenario |
|------|----------|
| 200 | Success response |
| 201 | Resource created |
| 204 | No content (delete) |
| 400 | Bad request |
| 401 | Authentication failed |
| 403 | Forbidden |
| 404 | Resource not found |
| 409 | Conflict (duplicate) |
| 422 | Validation failed |
| 500 | Server error |

### 3. Authentication/Authorization
- Request without token
- Expired token
- Unauthorized user
- Role-based access control

### 4. Paging/Sorting/Filtering
- Default paging
- Custom page size
- Sort options
- Complex filters

## Test Case Example

```markdown
## TC-API-001: Get user list

| Item | Content |
|------|---------|
| **Endpoint** | `GET /api/v1/users` |
| **Priority** | High |

### Request
| Item | Value |
|------|-------|
| Method | GET |
| Headers | `Authorization: Bearer {token}` |
| Query | `page=1&limit=10&sort=createdAt:desc` |

### Test Cases
| # | Scenario | Expected Status | Verification |
|---|----------|-----------------|--------------|
| 1 | Normal request | 200 | Returns array, pagination info |
| 2 | No token | 401 | error message |
| 3 | Invalid page | 400 | validation error |
```

## Response Verification Points

| Item | Verification |
|------|--------------|
| **Status Code** | Matches expected code |
| **Response Time** | Within SLA |
| **Body Schema** | Schema match (JSON Schema) |
| **Data Integrity** | Data accuracy |
| **Headers** | Content-Type, Cache, etc. |

## Automation Tools
- Postman/Newman
- REST Assured (Java)
- Supertest (Node.js)
- httpx/requests (Python)
- Bruno, Insomnia

# Exception Middleware Skill

Use a single global exception middleware for consistent API error responses.

## Location

`Api/Middleware/ExceptionMiddleware.cs`

## Responsibilities

- Catch exceptions from the entire HTTP request pipeline.
- Convert known application/domain exceptions into appropriate HTTP responses.
- Convert unexpected exceptions into `500 Internal Server Error`.
- Return all errors using `ApiResponse<object>`.
- Log exceptions appropriately.

## Exception Mapping

| Exception | HTTP Status | Response |
|---|---:|---|
| `AppException` | `AppException.StatusCode` | Use exception message |
| `DomainException` | `400 Bad Request` | Use exception message |
| `Exception` | `500 Internal Server Error` | Generic safe message |

## Rules

- Register middleware globally in the API pipeline.
- Never expose internal exception details, stack traces, SQL errors, or infrastructure details to clients.
- Log unexpected exceptions with full exception details.
- Use `ApiResponse<object>.Fail(...)` for error responses.
- Return JSON using camelCase naming.
- Keep exception handling centralized; controllers should not duplicate global try/catch logic.
- `DomainException` and `AppException` remain independent of HTTP middleware.
- The middleware may depend on `Application`/`Core` exception contracts, but `Core` and `Application` must not depend on the middleware.
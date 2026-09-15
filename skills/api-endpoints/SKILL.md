---
description: Guides the creation of new API endpoints, use when adding routes, handlers or controllers to the project
---

# API Endpoints

Conventions for adding a new API endpoint to this project.

## Where route files live

- Routes live under `src/routes/`, one file per resource (e.g. `src/routes/users.ts`, `src/routes/orders.ts`).
- Handler/controller logic lives under `src/controllers/`, mirroring the route file name (e.g. `src/controllers/users.ts`).
- Register new route files in the central router (`src/routes/index.ts`) rather than mounting them ad hoc elsewhere.

## Naming conventions

- Route paths are plural, kebab-case nouns (e.g. `/users`, `/order-items`), never verbs.
- Handler functions are named `<verb><Resource>` (e.g. `getUser`, `listOrders`, `createOrder`, `updateOrder`, `deleteOrder`).
- File names match the resource name in kebab-case; exported handlers use camelCase.

## Error handling pattern

- Handlers never construct raw error responses inline. Throw a typed error (e.g. `NotFoundError`, `ValidationError`, `UnauthorizedError`) and let the shared error-handling middleware translate it into the response.
- Validate input at the top of the handler before any side effects; validation failures throw `ValidationError` with a field-level detail list.
- Never swallow errors silently — unexpected exceptions propagate to the global error handler, which logs them and returns a generic 500.

## Response shape

- Successful responses return `{ data: <payload> }`.
- List endpoints return `{ data: [...], meta: { total, page, pageSize } }`.
- Error responses return `{ error: { code, message, details? } }` with an HTTP status matching the error type (400 validation, 401 unauthorized, 404 not found, 500 unexpected).
- Never return bare arrays or unwrapped objects from a handler.

## Before committing

- [ ] Route is registered in the central router.
- [ ] Handler validates all input and uses the shared error types (no inline error responses).
- [ ] Response follows the `{ data }` / `{ error }` shape above.
- [ ] Tests cover the happy path and at least one error case.
- [ ] New endpoint is documented (README or API docs) if one is maintained for this project.

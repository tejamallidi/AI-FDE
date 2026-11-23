# Study notes

- Compare integer path parameters with bounded `Path` and `Query` values. Invalid inputs are rejected during validation. A valid ID missing from the store yields 404.
- Use a Pydantic request model to validate work-order creation. A PATCH model can use `model_dump(exclude_unset=True)` to preserve omitted fields. Decide explicitly whether a supplied null should clear a field.
- Declare a public response model to control which fields the API returns. Use `Depends()` to share store access and pagination across endpoints. The header example demonstrates dependency-based checks in a lab.

**Recall drill:** Design a PATCH endpoint for a work order. Explain what happens when the status is omitted, invalid, or valid but the order does not exist.

Based on the session code. See [resource inventory](resources.md) for the transcript and handout.

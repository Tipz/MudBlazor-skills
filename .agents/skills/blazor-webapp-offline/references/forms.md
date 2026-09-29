# Blazor forms infrastructure

This reference covers platform forms. Component-library field APIs belong to their own skill.

## EditForm and EditContext

Use a model or explicit `EditContext` according to existing project conventions. An `EditContext` owns field modification and validation state; replacing the model generally requires a new context.

- Add the validation provider required by the project, such as DataAnnotations or a custom validator.
- Use field expressions so validation associates messages with the correct member.
- Choose one submit flow: valid/invalid callbacks or a general submit callback with explicit validation.
- Prevent duplicate asynchronous submissions and preserve user input on recoverable failures.

## Validation

Client/UI validation improves feedback but is never authoritative. Validate and authorize the trusted server operation.

- Map server validation failures to fields or form-level messages using the project's validation-store pattern.
- Clear only messages owned by that validator/store.
- Notify validation-state changes after updating messages.
- Define when validation runs: change, blur, submit, or an explicit async workflow.
- Handle model replacement and dynamic fields deliberately.

## Antiforgery and security

Follow the target framework/template's antiforgery behavior. Do not disable antiforgery to fix a form symptom. Bind to dedicated input models where overposting or domain-entity mutation is a concern.

## Lifecycle

If code subscribes to `EditContext` events, unsubscribe on disposal. Cancellation and error state should remain visible and should not destroy valid user input.


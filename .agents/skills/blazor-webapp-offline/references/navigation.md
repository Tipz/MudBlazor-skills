# Routing and navigation

## Routes and parameters

- Keep route templates unambiguous and verify constraints against the installed framework.
- Treat route and query values as untrusted input; parse/validate before use.
- Parameter changes can reuse the same component instance, so reload state in the parameter lifecycle rather than only initialization.
- Encode generated path/query values using supported helpers instead of string concatenation.

## NavigationManager

Use `NavigationManager` for application navigation and URI inspection when a normal link is insufficient. Prefer semantic links for ordinary navigation so browser affordances continue to work.

- Avoid forced reload unless the target truly requires a full document navigation.
- Preserve return URLs only after validating they are local/allowed.
- Subscribe to location changes only when needed and always unsubscribe.

## Enhanced navigation and streaming

These behaviors depend on target framework and project configuration. They can preserve document context or update content differently from full reloads.

- Do not assume page-load JavaScript reruns after enhanced navigation.
- Use the version-supported hooks/patterns for DOM initialization.
- Verify form/navigation interception locally before overriding it.

## Unsaved changes

Navigation locks/prompts improve UX but do not guarantee persistence or prevent every external close. Track a real dirty state, avoid prompting after successful save, and keep server operations consistent even if navigation occurs.


# File upload UX

Treat upload as a queue of explicit file states, not as a single button. Separate selecting files, validating them, transferring bytes, server processing/packaging, and producing the final result.

## Entry and selection

- Provide a clearly labeled browse action. Drag and drop is an enhancement, never the only path.
- State accepted types, count limits, and size limits before selection when known.
- For multiple files, show an itemized queue immediately after selection.
- Make the drop target visibly active during drag and avoid turning the entire page into an ambiguous target.
- Support keyboard and assistive-technology users through the browse path.

## Queue item model

Each file may need:

- full filename and distinguishing path/context when permitted;
- size and type;
- validation state and message;
- queued, uploading, uploaded, processing, failed, cancelled, or removed state;
- per-file progress when meaningful;
- retry or remove action when allowed.

Do not identify files by visible filename alone. Duplicate names may be valid from different sources; define whether duplicates mean same name, same path, same content hash, or a domain-specific collision.

## Validation

Validate early for feedback, then validate authoritatively on the server. Consider:

- file count;
- individual and aggregate size;
- allowed extension and actual content/type rules;
- zero-byte or unreadable file;
- duplicate/collision policy;
- destination naming and unsafe path input;
- business rules and security scanning where the application provides them.

Show item-level errors beside the file and a queue-level summary for aggregate rules. A rejected file should not erase valid queued items.

## Long filenames

- Preserve the extension and distinguishing end when truncating.
- Provide a reliable way to inspect or copy the full name.
- Allow wrapping in detail views; use middle truncation only where row height must stay compact.
- Keep status and remove/retry controls from overlapping the name.

## Transfer and progress

For multi-GB files, do not imply browser memory buffering or one-request behavior without verifying the architecture. The UX should expose the capabilities actually supported: streaming, chunking, resumability, server limits, timeouts, and reconnect behavior.

- Show bytes transferred and total only when trustworthy.
- Distinguish aggregate progress from per-file progress.
- Distinguish upload completion from subsequent verification or packaging.
- Prevent duplicate starts and accidental reselection from silently resetting progress.
- If the user may navigate away, explain the consequence or provide a reliable background/resume model.

Interactive Server disconnection may interrupt UI observation even if server work continues. Define how status is recovered after reconnect; use `blazor-webapp-offline` for the implementation model.

## Failure, interruption, and retry

State which files succeeded and which failed. Preserve the queue and valid metadata. Retry only failed items when the backend can do so safely; otherwise explain why the whole operation restarts.

Differentiate:

- user cancellation;
- connection interruption;
- server rejection;
- storage/processing failure;
- session or authorization expiry.

Never display a resumable claim unless the transport and server protocol actually support it.

## Removal before packaging

Make removal available while an item is queued or when the backend can safely exclude it. If upload has begun, define whether removal cancels transfer, deletes a temporary object, or merely excludes it from packaging. Reflect “removing” as an operation state when cleanup is asynchronous.

If packaging has already started, either lock the manifest with a clear explanation or cancel/restart through an explicit workflow. Do not silently create a ZIP from a different file set than the visible queue.

## Review matrix

Test browse and drag/drop; one and many files; duplicates; invalid type; zero-byte, very large, and long-name files; partial failure; cancellation; retry; removal before and during upload; packaging after upload; connection interruption; reconnect; accidental double activation; and keyboard-only operation.

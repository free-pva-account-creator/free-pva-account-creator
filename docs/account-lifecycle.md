# Account Lifecycle

An account should be treated as a state machine rather than a single registration action.

## Lifecycle

```text
CREATED
   ↓
REGISTERING
   ↓
EMAIL_PENDING
   ↓
PHONE_PENDING
   ↓
VERIFIED
   ↓
VALIDATED
```

A failure may move the account into:

```text
FAILED
```

An account can later become:

```text
DISABLED
```

## Why State Matters

Without explicit state management, a failed workflow can become difficult to resume.

For example:

```text
Registration succeeds
        ↓
Email verification fails
        ↓
Application crashes
        ↓
Restart
        ↓
What happens?
```

A stateful system knows the account reached:

```text
EMAIL_PENDING
```

and can resume or report the workflow appropriately.

## Account Record

A basic internal account object might contain:

```text
account_id
username
email
phone_reference
status
profile_id
created_at
updated_at
last_error
```

Sensitive credentials should not be stored in plaintext.

## Idempotency

Operations should ideally be safe to retry.

For example:

```text
verify_email()
```

should determine whether verification has already completed before performing unnecessary work.

## Failure States

Common failure categories include:

* Invalid configuration
* Registration rejected
* Verification timeout
* Browser failure
* Network failure
* Provider failure
* Application validation failure

Failures should be recorded with machine-readable error codes.

## Recovery

A robust workflow should support:

* Retry
* Resume
* Cancel
* Reset
* Manual intervention

## Audit Trail

For development and QA, maintain an audit trail containing:

* Workflow start
* State transitions
* Errors
* Completion status
* Test results

Do not record sensitive secrets in the audit log.

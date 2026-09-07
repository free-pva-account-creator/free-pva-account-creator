# Phone Verification

Phone verification introduces an additional external dependency into an account-registration workflow.

This project provides an abstraction for authorized testing rather than instructions for bypassing phone verification systems.

## Basic Flow

```text
Registration
     ↓
Phone Number Assigned
     ↓
Verification SMS
     ↓
SMS Provider
     ↓
Retrieve Code
     ↓
Submit Code
     ↓
Verification Complete
```

## Provider Interface

A provider abstraction might look like:

```python
class SmsProvider:
    def request_number(self, context):
        raise NotImplementedError

    def wait_for_code(self, reference):
        raise NotImplementedError

    def release(self, reference):
        raise NotImplementedError
```

## Provider Independence

The workflow engine should not know which SMS provider is being used.

Instead:

```text
Workflow
   ↓
SMS Provider Interface
   ↓
Authorized Provider
```

This keeps the architecture maintainable.

## Verification Timeouts

SMS delivery is not always immediate.

Use configurable timeouts and retry intervals.

Example:

```text
Request verification
        ↓
Wait
        ↓
Check message
        ↓
Retry
        ↓
Timeout
```

## Testing

Integration tests should use numbers and environments that the developer is authorized to control.

Test scenarios should include:

* Successful SMS
* Delayed SMS
* Incorrect code
* Expired code
* Provider timeout
* Provider failure

## Privacy

Phone numbers should be treated as sensitive data.

Avoid storing unnecessary personal information.

Use references or encrypted storage where appropriate.

## Responsible Usage

Do not use this project to circumvent identity verification, create fraudulent identities, evade platform restrictions, or operate accounts without authorization.

# Architecture

Free PVA Account Creator uses a modular architecture.

The goal is to prevent registration logic, verification logic, browser automation, and storage from becoming one tightly coupled application.

## High-Level Architecture

```text
                    Workflow Engine
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        ↓                 ↓                 ↓
 Registration         Verification       Profile
 Adapter                 Layer           Manager
        │                 │                 │
        ↓            ┌────┴────┐            ↓
 Platform           Email    Phone      Browser
 Adapter          Provider  Provider    Session
        │                 │                 │
        └─────────────────┼─────────────────┘
                          ↓
                    Account Store
```

## Core Components

### Workflow Engine

Controls the sequence of operations.

Example:

```text
Initialize
↓
Create Profile
↓
Open Registration
↓
Submit Registration
↓
Wait for Verification
↓
Verify Account
↓
Validate
↓
Persist Result
```

### Registration Adapter

Provides a common interface for registration workflows.

Different applications can implement their own adapters.

```python
class RegistrationAdapter:
    def register(self, account):
        raise NotImplementedError
```

### Verification Layer

Verification should be independent from registration.

This allows email and phone providers to be replaced without rewriting the workflow engine.

### Profile Manager

Responsible for browser-session isolation and profile state.

A profile may contain:

* Cookies
* Local storage
* Session state
* Browser preferences
* Authorized test metadata

### Account Store

Stores workflow state and test results.

A recommended account state model is:

```text
CREATED
REGISTERING
EMAIL_PENDING
PHONE_PENDING
VERIFIED
VALIDATED
FAILED
DISABLED
```

## Adapter Pattern

External services should be accessed through adapters.

```text
Workflow
   ↓
Adapter Interface
   ↓
Provider Implementation
```

This prevents the core application from becoming dependent on one provider.

## Error Handling

Errors should be categorized.

Examples:

* RegistrationError
* VerificationError
* ProfileError
* NetworkError
* ConfigurationError
* ValidationError

Each error should contain enough information for debugging without exposing secrets.

## Logging

Use structured logging wherever possible.

Avoid logging:

* Passwords
* Authentication tokens
* Verification codes
* API secrets
* Private personal information

## Testing

Each component should have unit tests.

Integration tests should use controlled test environments.

The architecture should allow the workflow engine to be tested without connecting to a third-party production platform.

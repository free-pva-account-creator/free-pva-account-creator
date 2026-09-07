# Platform Adapters

Different websites and applications implement registration differently.

Instead of putting platform-specific logic into the core workflow engine, Free PVA Account Creator uses an adapter architecture.

## Adapter Concept

```text
Core Workflow
      ↓
Platform Adapter
      ↓
Authorized Application
```

The core engine defines what needs to happen.

The adapter defines how that particular application implements it.

## Example Interface

```python
class PlatformAdapter:
    def open_registration(self):
        raise NotImplementedError

    def submit_registration(self, account):
        raise NotImplementedError

    def check_verification(self):
        raise NotImplementedError

    def get_account_status(self):
        raise NotImplementedError
```

## Why Adapters?

Without adapters:

```text
Core
 ├── Platform A logic
 ├── Platform B logic
 ├── Platform C logic
 ├── Platform D logic
 └── ...
```

The application becomes difficult to maintain.

With adapters:

```text
Core
 ├── Adapter A
 ├── Adapter B
 ├── Adapter C
 └── Adapter D
```

The core remains independent.

## Test Adapter

The first adapter should ideally target a local or staging application controlled by the developer.

For example:

```text
tests/
└── fixtures/
    └── registration_app/
```

This allows the complete workflow to be tested without depending on a production platform.

## Adapter Responsibilities

An adapter may be responsible for:

* Opening registration
* Locating form fields
* Entering test data
* Submitting the form
* Detecting validation errors
* Detecting verification requirements
* Confirming successful registration

## Adapter Should Not

Adapters should not contain:

* Secret credentials
* Hard-coded private tokens
* Security bypasses
* CAPTCHA circumvention
* Anti-abuse evasion logic

## Versioning

Web applications change.

Adapters should therefore expose a version or compatibility identifier when appropriate.

Example:

```text
adapter: example-staging
version: 1.2
```

## Testing

Every adapter should have:

### Unit tests

Test parsing and internal logic without opening a browser.

### Integration tests

Run against a controlled test environment.

### Failure tests

Verify behavior when:

* Fields change
* Registration fails
* Verification is unavailable
* Network errors occur
* The application returns unexpected responses

## Future Extensions

The adapter system can eventually support plugins.

```text
Core
  ↓
Adapter Registry
  ↓
┌──────────────┬──────────────┬──────────────┐
│ Adapter A    │ Adapter B    │ Adapter C    │
└──────────────┴──────────────┴──────────────┘
```

This allows the project to grow without turning the core codebase into a giant collection of platform-specific scripts.

# Email Verification

Email verification is a common stage in account-registration workflows.

This project treats email verification as an independent service.

## Verification Flow

```text
Registration
     ↓
Verification Email Sent
     ↓
Email Provider
     ↓
Retrieve Message
     ↓
Extract Verification Data
     ↓
Submit Verification
     ↓
Confirm Account State
```

## Provider Abstraction

The core application should not depend directly on a specific mailbox provider.

Instead:

```python
class EmailProvider:
    def wait_for_message(self, criteria):
        raise NotImplementedError

    def get_verification_data(self, message):
        raise NotImplementedError
```

A provider implementation can then be created for an authorized test mailbox system.

## Test Mailboxes

For automated testing, dedicated test mailboxes are recommended.

Useful options include:

* Local mail servers
* Staging mail systems
* Developer-controlled mailboxes
* Test email APIs

## Verification Matching

Messages can be identified using:

* Recipient
* Subject
* Sender
* Message ID
* Timestamp
* Test-specific identifier

Avoid relying solely on email subject lines.

## Timeouts

Verification workflows should have explicit timeouts.

Example:

```text
Wait 10 seconds
↓
Check mailbox
↓
Wait
↓
Check again
↓
Timeout
```

Avoid infinite polling.

## Security

Never write the following into logs:

* Email passwords
* Authentication tokens
* Private mailbox credentials
* Verification codes

Use environment variables or a secrets manager for credentials.

## Testing

Email verification should be tested independently from the registration interface.

A good test suite includes:

* Message received
* Message delayed
* Incorrect message
* Expired verification
* Malformed message
* Provider unavailable
* Successful verification

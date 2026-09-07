# Free PVA Account Creator
![Uploading ChatGPT Image Sep 7, 2026, 03_08_07 PM.png…]()


An open-source framework for building and testing phone-verified account creation workflows in authorized environments.

Free PVA Account Creator is designed for developers, QA engineers, automation researchers, and businesses that need a structured way to experiment with account-registration workflows without building every component from scratch.

The project focuses on modular account creation, verification workflows, browser profiles, platform adapters, testing infrastructure, and reliable workflow management.

> **Important:** This project is intended for accounts, websites, applications, and environments that you own or are explicitly authorized to test. It does not provide instructions for bypassing platform security, CAPTCHA systems, rate limits, identity verification, or other anti-abuse controls.

## Features

* Modular account-creation workflow
* Email verification workflow support
* Phone verification workflow architecture
* Browser-profile isolation
* Configurable account lifecycle
* Platform adapter architecture
* Test-environment support
* Proxy configuration support for authorized environments
* CAPTCHA detection and human-verification handling
* Logging and troubleshooting tools
* Extensible Python-based architecture
* Open-source documentation

## Project Goals

The goal is not simply to automate a registration form.

A reliable account-creation system needs to manage an entire lifecycle:

```text
Configuration
     ↓
Registration
     ↓
Email Verification
     ↓
Phone Verification
     ↓
Profile Initialization
     ↓
Validation
     ↓
Storage
     ↓
Testing / Monitoring
```

Each stage should be independently testable.

## Why This Project Exists

Account-registration workflows are often surprisingly complicated.

A registration process may involve:

* Email addresses
* Phone numbers
* Verification codes
* Browser sessions
* Cookies
* Profile data
* Network configuration
* Device/browser characteristics
* CAPTCHA challenges
* Platform-specific registration requirements

Putting everything into one large automation script quickly becomes difficult to maintain.

This project therefore uses a modular architecture so individual components can be developed, tested, and replaced independently.

## Architecture

The project is organized around several major components:

```text
                    ┌─────────────────────┐
                    │   Workflow Engine   │
                    └──────────┬──────────┘
                               │
          ┌────────────────────┼────────────────────┐
          ↓                    ↓                    ↓
   Registration          Verification          Profiles
      Adapter               Layer              Manager
          │                    │                    │
          ↓                    ↓                    ↓
     Platform             Email / SMS        Browser Session
      Adapter             Providers             Storage
```

## Supported Environments

The project is intended primarily for:

* Local development
* Automated QA environments
* Staging environments
* Internal applications
* Test websites
* Authorized platform integrations
* Research environments where the operator has permission

## Quick Start

Clone the repository:

```bash
git clone https://github.com/YOUR-USERNAME/free-pva-account-creator.git
cd free-pva-account-creator
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Windows:

```bash
.venv\Scripts\activate
```

Activate it on macOS/Linux:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Copy the example configuration:

```bash
cp examples/configuration.example.yaml config.yaml
```

Run the test suite:

```bash
pytest
```

## Documentation

Start here:

1. [Getting Started](docs/getting-started.md)
2. [Architecture](docs/architecture.md)
3. [Account Lifecycle](docs/account-lifecycle.md)
4. [Email Verification](docs/email-verification.md)
5. [Phone Verification](docs/phone-verification.md)
6. [Browser Profiles](docs/browser-profiles.md)
7. [Proxy Management](docs/proxy-management.md)
8. [CAPTCHA Handling](docs/captcha-handling.md)
9. [Platform Adapters](docs/platform-adapters.md)
10. [Troubleshooting](docs/troubleshooting.md)

## Design Principles

### Modular

Every major component should have a clearly defined responsibility.

### Testable

Registration and verification logic should be testable without depending on a production platform.

### Replaceable

Providers such as email, SMS, browser automation, and storage should be replaceable through adapters.

### Observable

A workflow that fails silently is difficult to maintain. Logging and structured error reporting are therefore first-class features.

### Responsible

Automation should operate only where the operator has permission.

## Roadmap

### Phase 1

* Core workflow engine
* Configuration system
* Test fixtures
* Email verification abstraction
* Browser profile abstraction
* Logging

### Phase 2

* SMS verification abstraction
* Platform adapter interface
* Account state management
* Improved testing utilities

### Phase 3

* Web dashboard
* Workflow monitoring
* Job queue
* Account lifecycle reporting
* Plugin architecture

## Contributing

Contributions are welcome.

Before submitting a pull request, please read:

* CONTRIBUTING.md
* SECURITY.md
* CODE_OF_CONDUCT.md

## License

This project is released under the MIT License.

See [LICENSE](LICENSE) for details.

## Disclaimer

This software is provided for educational, development, testing, and authorized automation purposes.

Users are responsible for complying with the terms, policies, laws, and regulations applicable to the services they interact with.

The maintainers do not endorse unauthorized account creation, identity impersonation, spam, fraud, or attempts to circumvent security and anti-abuse systems.

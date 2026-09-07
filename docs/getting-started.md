# Getting Started

Welcome to Free PVA Account Creator.

This guide explains how to set up the project and run its development and testing environment.

## Requirements

Recommended environment:

* Windows, macOS, or Linux
* Python 3.10+
* Git
* Internet access for authorized test environments
* A test application or staging environment

## Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/free-pva-account-creator.git
cd free-pva-account-creator
```

## Create a Virtual Environment

```bash
python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

macOS/Linux:

```bash
source .venv/bin/activate
```

## Install Dependencies

```bash
pip install -r requirements.txt
```

## Configuration

Copy the example configuration:

```bash
cp examples/configuration.example.yaml config.yaml
```

Never commit passwords, API keys, verification credentials, or other secrets to Git.

Use environment variables or a local secrets manager instead.

## Run Tests

```bash
pytest
```

The test suite should be the first thing you run after installation.

## Development Workflow

A typical development cycle is:

```text
Clone
  ↓
Install
  ↓
Configure
  ↓
Run Tests
  ↓
Implement Feature
  ↓
Add Tests
  ↓
Run Tests Again
  ↓
Submit Pull Request
```

## Recommended First Experiment

Do not begin with a production platform.

Instead, create a small local or staging registration application containing:

* Username
* Email
* Password
* Verification code
* Profile information

Use that environment to test the workflow engine.

This makes debugging dramatically easier because you control the registration process.

## Next Steps

After installation, read:

* Architecture
* Account Lifecycle
* Email Verification
* Browser Profiles

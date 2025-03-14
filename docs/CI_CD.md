# CI/CD Pipeline Documentation

This document describes the Continuous Integration and Continuous Deployment (CI/CD) pipeline for the Claude Desktop Installer.

## Pipeline Overview

The CI/CD pipeline is implemented using GitHub Actions and consists of the following stages:

1. **Syntax Validation**: Checks the shell script syntax using ShellCheck
2. **Distribution Tests**: Tests the installer on multiple Linux distributions
   - Ubuntu (latest)
   - Debian (stable)
   - Arch Linux (latest)

## Workflow Details

### When the Pipeline Runs

The pipeline is triggered on:

- Push to the `main` branch
- Pull requests targeting the `main` branch

### Job: Lint

This job runs ShellCheck to validate the syntax and catch potential issues in the shell scripts.

- Environment: Ubuntu latest
- Tool: ShellCheck
- Severity Level: Warning (catches potential issues but allows idiomatic code)

### Jobs: Test Installation

These jobs test the actual installation process on different Linux distributions:

- **test-ubuntu**: Tests on the latest Ubuntu version
- **test-debian**: Tests on the stable Debian release
- **test-arch**: Tests on the latest Arch Linux version

Each job:

1. Sets up a container with the target distribution
2. Installs necessary dependencies
3. Runs the installer script with the `--test-env` option
4. Verifies the test environment was set up correctly

## Adding New Tests

To add tests for additional Linux distributions:

1. Copy one of the existing test jobs in `.github/workflows/ci.yml`
2. Modify the container image and package installation commands as needed
3. Ensure the verification steps are appropriate for the new distribution

## Troubleshooting Failed Tests

If a test fails in the CI pipeline:

1. Check the GitHub Actions logs for error messages
2. Common issues include:
   - Missing dependencies
   - Distribution-specific path differences
   - Permission issues in the container environment
3. Try to reproduce the issue locally using a container:
   ```bash
   docker run -it --rm ubuntu:latest /bin/bash
   # Then install dependencies and run the test
   ```

## Manual Testing

Before submitting a pull request, it's recommended to:

1. Run the shellcheck manually:

   ```bash
   shellcheck claude-install.sh
   ```

2. Test the installation in a clean environment:

   ```bash
   ./claude-install.sh --test-env
   ```

3. If possible, test on actual installations of the supported distributions

# Agent Guidelines

This repository demonstrates the integration of `mage-remote-run` within GitHub Actions.
It contains workflow configurations to automated testing and usage of the `mage-remote-run` tool.

## 1. Build, Lint, and Test

Since this is a configuration repository for GitHub Actions, "building" and "testing" primarily involve validating the YAML workflows.

### Testing
- **Local Validation**: Ensure `mage-remote-run` is installed locally to verify commands.
  ```bash
  # Check version
  mage-remote-run --version
  
  # Test connection (requires configured connection)
  mage-remote-run connection test
  ```
- **CI Validation**: The primary test is the GitHub Action itself defined in `.github/workflows/demo.yml`.

### Linting
- **YAML**: Ensure all `.yml` files in `.github/workflows` are valid YAML.
- **Action Syntax**: Follow standard GitHub Actions syntax.

## 2. Code Style & Conventions

### Workflows (YAML)
- **Indentation**: Use 2 spaces for indentation.
- **Naming**:
  - Jobs and steps should have clear, descriptive names.
  - Environment variables should be uppercase (e.g., `MAGE_URL`).
- **Secrets**: NEVER hardcode credentials. Always use `${{ secrets.VARIABLE_NAME }}`.
  - `MAGE_URL`
  - `MAGE_CONSUMER_KEY`
  - `MAGE_CONSUMER_SECRET`
  - `MAGE_ACCESS_TOKEN`
  - `MAGE_ACCESS_TOKEN_SECRET`
- **Shell Commands**:
  - Use `|` for multi-line commands to improve readability.
  - Quote all variables in bash scripts (e.g., `"$MAGE_URL"`).

### Tool Usage (`mage-remote-run`)
- **Connection Setup**:
  - Use `connection add` with explicit flags for all parameters.
  - Always include `--no-test` in CI pipelines during the configuration step to separate configuration logic from connection verification.
  - Use `--active` to ensure the new connection is immediately usable.
- **Command Structure**:
  ```bash
  mage-remote-run connection add \
    --name "ProfileName" \
    --type "ac-on-prem" \
    ... flags
  ```

### Project Structure
- `.github/workflows/`: Contains all CI/CD definitions.
- `README.md`: Documentation for the example.

## 3. Error Handling
- In CI steps that might fail due to missing secrets (like connection tests in a demo), use `continue-on-error: true` if the failure is expected or acceptable for the demonstration.
- In production scripts, fail fast on error.

## 4. Updates
- When updating the `mage-remote-run` version, check the [npm registry](https://www.npmjs.com/package/mage-remote-run) for the latest version and changelog.

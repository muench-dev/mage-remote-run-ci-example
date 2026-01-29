# Mage Remote Run CI Example

This repository demonstrates how to integrate `mage-remote-run` into a CI/CD pipeline using GitHub Actions. It showcases the simplicity of setting up and using the tool to interact with Magento/Adobe Commerce instances remotely during your automated workflows.

## Features

- **Easy Integration**: Uses the [setup-mage-remote-run](https://github.com/marketplace/actions/setup-mage-remote-run) action from the GitHub Marketplace.
- **Automated Configuration**: Shows how to securely configure connection profiles using GitHub Secrets, specifically for **OAuth 1.0a** authentication.
- **Verification**: Includes steps to verify the connection and execute commands against a remote instance.

## Usage

The core of this example is the GitHub Action workflow defined in `.github/workflows/demo.yml`.

### Example Workflow

The workflow utilizes the `muench-dev/mage-remote-run-action` to setup the environment. Here is a simplified overview of the process:

1.  **Checkout Code**: Standard checkout step.
2.  **Setup Node.js**: Ensures the environment is ready.
3.  **Configure Mage Remote Run**: Uses the action to install and configure the tool with provided credentials.
4.  **Execute Commands**: Runs standard `mage-remote-run` commands (e.g., listing websites, store groups).

```yaml
- name: Configure Mage Remote Run
  uses: muench-dev/mage-remote-run-action@main
  with:
    profile-name: "PaaS-Instance"
    type: "ac-cloud-paas"
    url: ${{ secrets.MAGE_URL }}
    consumer-key: ${{ secrets.MAGE_CONSUMER_KEY }}
    consumer-secret: ${{ secrets.MAGE_CONSUMER_SECRET }}
    access-token: ${{ secrets.MAGE_ACCESS_TOKEN }}
    token-secret: ${{ secrets.MAGE_ACCESS_TOKEN_SECRET }}

- name: List Websites
  run: mage-remote-run website list --format json
```

## Setup

To use this in your own repository:

1.  Add the `muench-dev/mage-remote-run-action` step to your workflow.
2.  Configure the necessary [GitHub Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) for your Magento / Mage-OS / Adobe Commerce instance:
    - `MAGE_URL`
    - `MAGE_CONSUMER_KEY`
    - `MAGE_CONSUMER_SECRET`
    - `MAGE_ACCESS_TOKEN`
    - `MAGE_ACCESS_TOKEN_SECRET`

For more details on the action, visit the [GitHub Marketplace](https://github.com/marketplace/actions/setup-mage-remote-run).

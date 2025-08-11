# 1fe-ci-cd

This repository contains the code and configuration for the "1fe-ci-cd" project, focusing on implementing Continuous Integration and Continuous Deployment (CI/CD) pipelines for 1fe-widgets.

## Features

- Automated build and test workflows
- Deployment scripts and configuration
- Example frontend application code

## Getting Started

### Prerequisites

- Node.js (version 22 or higher recommended)
- yarn
- Docker

### Installation

1. Clone the repository:
   ```sh
   git clone https://github.com/your-org/1fe-ci-cd.git
   cd 1fe-ci-cd
   ```

### CI/CD

This repository is set up for CI/CD using GitHub Actions (or your preferred CI/CD tool). Workflows are defined in the `.github/workflows` directory.

## Contributing

Contributions are welcome! Please open issues or submit pull requests for improvements.

## License

This project is licensed under the MIT License.

# 1FE CI/CD Workflows

This repository contains shared reusable GitHub Actions and workflows for managing 1FE widget lifecycle.

## 📦 Key Components

### ✅ Composite Actions
- **check-cdn-asset**: Verifies that a widget bundle exists on Akamai CDN before performing rollback.

### 🔁 Reusable Workflows
- **reusable-rollback-ci.yml**: Used to roll back a widget version, only if the asset exists on CDN.
- **reusable-update-azure-config.yml**: Updates Azure App Configuration with the widget version.

## 📌 Usage from Caller Repo

### Example: `rollback-widget.yml` in `1fe-widget-starter-kit`

```yaml
jobs:
  call-reusable-rollback:
    uses: docusign/1fe-ci-cd/.github/workflows/reusable-rollback-ci.yml@main
    with:
      target-version: ...
      environment: ...
      caller-repo: ...
      caller-repo-ref: ...
    secrets:
      AZURE_APP_CONFIG_CONNECTION_STRING: ...


---

### Issues and Discussions

If you have questions or want to discuss this project, please visit the [Issues](https://github.com/docusign/1fe/issues) or [Discussions](https://github.com/docusign/1fe/discussions) pages in our monorepo.

# bactions/workflows - Reusable GitHub Actions Workflows

`bactions/workflows` is a repository harboring a curated set of opinionated GitHub Actions workflows that have been rigorously tested in production environments. Tailored for different programming languages and project types within those languages, these workflows encapsulate standard practices for project management and code quality assurance.

## Key Features:

1. **Standard Checks**: 
   These workflows provide a robust suite of checks for all code pushed to branches, establishing a requirement for passing these checks prior to merging pull requests.

2. **Conventional Commits**:
   Adopting the use of conventional commits, a solution is provided to calculate version numbers based on commit messages.

3. **Automated Releases**:
   Automatisation is at the heart of these workflows, streamlining the release of new versions, attachment of compiled binaries as artifacts, publishing Docker images, and notifying designated Slack channels upon release creation.

## Language Support:

### Go

- **Backend Applications**: 
    - Discover workflows and examples tailored for backend applications written in Go by exploring the [example-go-server repository](https://github.com/bactions/example-go-server).

- **Libraries**:
    - Uncover workflows and examples dedicated to libraries written in Go by navigating to the [example-go-lib repository](https://github.com/bactions/example-go-lib).

## General Usage:

Before diving into the utilization of the reusable workflows contained in this repository, ensure that the option to allow the usage of reusable workflows from outside of the organization is enabled in your repository setup. This is a pivotal step to unlock the full potential of these reusable workflows.

1. **Workflow Reference**:
    In your project's GitHub Actions configuration, reference the desired workflow from `bactions/workflows`. For instance:
    ```yaml
    jobs:
      on-push:
        uses: bactions/workflows/.github/workflows/on-push-go.yml@main
    ```

2. **Secrets and Permissions**:
   Specify any required secrets and permissions within your GitHub Actions configuration as demonstrated in the workflow usage examples.

For in-depth understanding and tailored usage based on specific languages and use cases, refer back to the **Language Support** section. Moreover, for a more comprehensive understanding of reusable workflows, delve into the [GitHub Documentation on Reusable Workflows](https://docs.github.com/en/actions/learn-github-actions/reusing-workflows).


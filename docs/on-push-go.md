# [on-push-go.yml](..%2F.github%2Fworkflows%2Fon-push-go.yml)

---

`on-push-go.yml` is a reusable workflow specifically designed for Go projects. 
This workflow springs into action upon every push to a branch, 
performing a series of checks on the code to ensure adherence to the highest standards of quality and correctness.

## Trigger:
- This workflow is meant to be used when triggered on a push to any branch.

## Key Features:

1. **Comprehensive Checks**:
    - Various checks are performed on the code, and can be set as required in the GitHub repository settings to enforce code quality standards.
    - The checks provided are as follows:
        - **Build**: Verifies the codebase can be successfully built.
        - **Unit Tests**: Runs unit tests to ensure code correctness.
        - **Code Coverage**: Calculates code coverage to maintain a standard of testing.
        - **Code Style**: Checks code style for consistency and runs `go mod tidy`, committing & pushing any resultant changes.
        - **Dependency Security**: Scans dependencies for known security vulnerabilities.

2. **Non-blocking Checks**:
    - The checks are designed to not break the workflow, allowing the author to see all potential failures. This minimizes the iterative fix-and-fail cycle by revealing all issues at once.

3. **Slack Notifications**:
    - The workflow has the capability to send notifications to a Slack channel regarding the result of the run.

## Example Configuration:

```yaml
name: "On push changes"

on:
  push:
    branches-ignore:
      - main
      - master

permissions:
  contents: write

jobs:
  on-push:
    uses: bactions/workflows/.github/workflows/on-push-go.yml@main
    with:
      go_version: '1.21'  # [Optional] Version of Go which should be used to perform the checks
    secrets:
      DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}  # Private key for a GitHub deploy key
      SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK_URL }}  # Slack webhook URL used for notifications
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}  # Codecov token for uploading coverage reports

```

### GitHub Permissions:
- The token requires `write` permission for contents.

### Deploy Key Setup:
`DEPLOY_KEY` secret is the private key for a GitHub deploy key.
It is used to trigger the workflow again, after commiting changes made during Code Style job.
  
[Creating a GitHub deploy key](https://developer.github.com/v3/guides/managing-deploy-keys/#deploy-keys).

### Slack Webhook Setup:
- `SLACK_WEBHOOK_URL` secret should contain the webhook URL generated following the [instructions here](https://api.slack.com/messaging/webhooks).
- If not provided workflow will omit the notification.

**Failed checks:**

![failed checks notification](images%2Ffailed_checks_slack_notify.png)

The Slack message for failed checks contains:
- Red margin on the left
- A header linking to the workflow.
- Mention of checks that failed.
- Link to project
- If a PR was created for the push, a link to that PR will be included.

![success checks notification](images%2Fsuccess_checks_slack_notify.png)

The Slack message for failed checks contains:
- Green margin on the left
- A header linking to the workflow.
- Link to project
- If a PR was created for the push, a link to that PR will be included.

---

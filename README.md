# Branch Cleanup Workflow

This repository contains a GitHub Actions workflow designed to automate the process of archiving and deleting stale branches in a repository. The workflow helps keep the repository clean by managing branches that are no longer actively used.

## Workflow Overview

The **Branch Cleanup Workflow** is scheduled to run daily at midnight UTC and can also be triggered manually. It performs the following tasks:

1. **Identify Stale Branches**: Branches that have been inactive for a specified number of days (`DAYS_INACTIVE`, default is 90 days) are identified as stale.
2. **Archive Stale Branches**: Stale branches are renamed with the prefix `archive/`, signaling that they are no longer actively used but retained temporarily for reference.
3. **Delete Archived Branches**: Branches that have been archived for an additional specified number of days (`DAYS_ARCHIVED`, default is 30 days) are permanently deleted from the repository.

## Key Features
- **Manual Trigger**: The workflow can be triggered manually using the GitHub Actions interface.
- **Configurable Retention Periods**: You can customize the number of days for branch inactivity (`DAYS_INACTIVE`) and archiving (`DAYS_ARCHIVED`) using environment variables.
- **Dry Run Mode**: A `DRY_RUN` mode is available to simulate the process without making actual changes, allowing for safe testing.
- **Logging and Artifact Storage**: The workflow logs all actions taken (or simulated in dry run mode) and stores the log file as an artifact for review.

## Configuration
- **DAYS_INACTIVE**: The number of days a branch must be inactive before it is considered for archiving. Default: `90`.
- **DAYS_ARCHIVED**: The number of days an archived branch must exist before it is deleted. Default: `30`.
- **DRY_RUN**: Set to `true` to test the workflow without making any actual changes. Default: `false`.

## Usage
To use this workflow, create a new file in your repository at `.github/workflows/branch-cleanup.yml` and paste the workflow YAML content. Adjust the environment variables as needed.

## Safety Considerations
- **Protected Branches**: The workflow skips protected branches like `main` and `master` to ensure they are not inadvertently archived or deleted.
- **Retention of Recent Branches**: By archiving branches first, the workflow provides an additional buffer period before deleting branches, ensuring that recently archived branches are available for rollback if needed.

## Manual Execution
To manually trigger the workflow:
1. Go to the **Actions** tab of your repository.
2. Select **Branch Cleanup Workflow** from the list of workflows.
3. Click the **Run workflow** button.

## Logging and Artifacts
The workflow generates a detailed log of all actions performed, including branch checks, archiving, and deletion. The log file (`cleanup.log`) is uploaded as an artifact and can be downloaded for review from the **Actions** tab after each run.

## Future Improvements
- Implement a similar workflow to manage stale deployment artifacts, keeping only the latest few versions to ensure rollback safety.
- Enhance notification capabilities to alert maintainers before branches are archived or deleted.

## Contributions
Contributions are welcome! If you have suggestions for improvements or additional features, feel free to open an issue or submit a pull request.


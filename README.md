# aio-cloudmanager-pipeline-update

A GitHub Action to update and trigger an Adobe Cloud Manager pipeline for your AEM projects. This action configures the AIO CLI, installs the Cloud Manager plugin, and runs pipeline updates using secure credentials and parameters.

## Features
- Uses the latest LTS Node.js environment
- Caches dependencies for faster builds
- Installs and configures the AIO CLI and Cloud Manager plugin locally
- Securely handles secrets and cleans up sensitive files
- Runs all logic in the action directory for reliability

## Authentication

To use this action, you must create aan integration must be created in the [Adobe I/O Developer Console](https://console.adobe.io) which has the Cloud Manager service. See the [Cloud Manager API Documentation](https://www.adobe.io/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/) for more information.

## Usage
Add this action to your workflow:

```yaml
jobs:
  update-pipeline:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: jfmitchell/aio-cloudmanager-pipeline-update@v1.0.0
        with:
          pipelineId: ${{ secrets.PIPELINE_ID }}
          programId: ${{ secrets.PROGRAM_ID }}
          repositoryId: ${{ secrets.REPOSITORY_ID }} # optional
          stageEnvironmentId: ${{ secrets.STAGE_ENVIRONMENT_ID }} # optional
          imsOrgId: ${{ secrets.IMS_ORG_ID }}
          technicalAccountId: ${{ secrets.TECHNICAL_ACCOUNT_ID }}
          technicalAccountEmail: ${{ secrets.TECHNICAL_ACCOUNT_EMAIL }}
          clientId: ${{ secrets.CLIENT_ID }}
          clientSecret: ${{ secrets.CLIENT_SECRET }}
```

## Inputs
| Name                  | Description                                 | Required |
|-----------------------|---------------------------------------------|----------|
| pipelineId            | Cloud Manager Pipeline ID                   | Yes      |
| programId             | Cloud Manager Program ID                    | Yes      |
| repositoryId          | Cloud Manager Repository ID                 | No       |
| stageEnvironmentId    | Cloud Manager Stage Environment ID          | No       |
| imsOrgId              | IMS Organization ID                         | Yes      |
| technicalAccountId    | IMS Technical Account ID                    | Yes      |
| technicalAccountEmail | IMS Technical Account Email                 | Yes      |
| clientId              | IMS Client ID                               | Yes      |
| clientSecret          | IMS Client Secret                           | Yes      |

## Secrets
Store all sensitive values as GitHub Actions secrets in your repository or organization settings. Do not commit secrets to your repository.

## How It Works
1. Sets up Node.js and caches dependencies in the action directory
2. Installs the AIO CLI and Cloud Manager plugin
3. Creates a config.json file with your credentials
4. Runs the pipeline update using the AIO CLI
5. Cleans up sensitive files after execution

## License
Apache-2.0 license

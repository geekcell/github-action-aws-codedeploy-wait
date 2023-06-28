[![Geek Cell GmbH](https://raw.githubusercontent.com/geekcell/.github/main/geekcell-github-banner.png)](https://www.geekcell.io/)

<!-- action-docs-description -->
## Description

Wait for an AWS CodeDeploy deployment to finish. Will poll the CodeDeploy API until the deployment is finished or failed.
<!-- action-docs-description -->

## Usage

#### Advanced Example
``` yaml
## Create new CodeDeploy deployment
- name: Deploy Amazon ECS
  id: deploy-ecs
  uses: aws-actions/amazon-ecs-deploy-task-definition@v1
  with:
    cluster: my-cluster
    service: my-service
    task-definition: task-definition.yaml

    codedeploy-appspec: appspec.yaml
    codedeploy-application: my-application
    codedeploy-deployment-group: my-deployment-group

## Wait for ECS Blue Deployment
- name: Wait for blue instances to be ready
  uses: geekcell/github-action-aws-codedeploy-wait@v1.0.0
  with:
    codedeploy-deployment-id: steps.deploy-ecs.outputs.codedeploy-deployment-id

## Run smoke tests
- name: Run tests
  run: yarn cypress run

## Shift traffic if tests passed
- name: Shift Traffic
  run: aws deploy continue-deployment --deployment-id ${{ needs.deployment.outputs.codedeploy-deployment-id }}
```

<!-- action-docs-inputs -->
## Inputs

| parameter | description | required | default |
| --- | --- | --- | --- |
| codedeploy-deployment-id | The ID of the CodeDeploy deployment to check. | `true` |  |
| sleep-between-requests | How many seconds to sleep between requests to the CodeDeploy API to check the status. | `false` | 5 |
<!-- action-docs-inputs -->

<!-- action-docs-outputs -->

<!-- action-docs-outputs -->

<!-- action-docs-runs -->
## Runs

This action is a `composite` action.
<!-- action-docs-runs -->

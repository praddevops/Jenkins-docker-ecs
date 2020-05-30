# Jenkins-docker-ecs
Jenkins pipeline to deploy new image to AWS ECS service

### ECS 
* Your AWS account must be setup with an ECS cluster named `main`, a service with name `node-app` that uses task-definition named `node-app` (Terraform code here: https://github.com/praddevops/ecs-terraform)

### App code is located in src/main/node-app. Any changes made will trigger the pipeline which builds new image and updates the ECS service with new image

## CICD pipeline:

Jenkins version: 2.234

Jenkins Plugin Requirements(in addition to default plugins): AnsiColor, Pipeline Utility Steps

### Following credentials should be present in Jenkins

* `aws_access_key_id` (Credential type: secret text): "AWS Access Key ID"
* `aws_access_key` (Credential type: secret text): "AWS Access Secret Key"
* `dockerhub_username` (Credential type: secret text): "Dockerhub username"
* `dockerhub_pw` (Credential type: secret text): "Dockerhub repo password"

### Jenkins Troubleshooting

* If pipeline fails due to `org.jenkinsci.plugins.scriptsecurity.sandbox.RejectedAccessException: Scripts not permitted to use....`, go to Manage Jenkins-->In process Script Approval to approve the scripts 

## How it works

  Jenkins-deploy-ECS contains Application code (location: src/main/node-app) for an app called `node-app` (App source code: https://www.digitalocean.com/community/tutorials/how-to-build-a-node-js-application-with-docker) and Jenkinsfile. Jenkins job polls scm every 15 minutes and rebuilds a new docker image (Dockerfile is in 'build' directory) if there were new commits, and pushes the new tagged image to Dockerhub. In ECS deploy stage, Jenkins job retrieves current revision of task-definition of the `node-app` service and creates new revision with latest docker image tag. Finally, new revision is registered in ECS and updates the `node-app` service with new revision.

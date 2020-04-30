# Jenkins-docker-ecs
Jenkins pipeline to deploy new image to AWS ECS service

### App code is located in src/main/node-app. Any changes made will trigger the pipeline which builds new image and update the ECS service with new image

## CICD pipeline:

Jenkins version: 2.234

### Jenkins Troubleshooting

* If pipeline fails due to `org.jenkinsci.plugins.scriptsecurity.sandbox.RejectedAccessException: Scripts not permitted to use....`, go to Manage Jenkins-->In process Script Approval to approve the scripts 
# Jenkins-docker-ecs
Jenkins pipeline to deploy new image to AWS ECS service

### App code is located in src/main/node-app. Any changes made will trigger the pipeline which builds new image and updates the ECS service with new image

## CICD pipeline:

Jenkins version: 2.234

### Following credential should be present in Jenkins

* aws_access_key_id (Credential type: secret text): AWS_ACCESS_KEY_ID
* aws_access_key (Credential type: secret text): AWS_ACCESS_SECRET_KEY
* dockerhub_username (Credential type: secret text): DOCKERHUB USERNAME
* dockerhub_pw (Credential type: secret text): DOCKERHUB REPO PASSWORD

### Jenkins Troubleshooting

* If pipeline fails due to `org.jenkinsci.plugins.scriptsecurity.sandbox.RejectedAccessException: Scripts not permitted to use....`, go to Manage Jenkins-->In process Script Approval to approve the scripts 
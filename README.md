# devops
Spring Boot project with simple controller and tests. 
Main goal is to practice DEVOPS ( using Git, Jenkins, Artifactory, Sonar, ELK and Jira).

Prepare for running CI:
- start Artifactory
- start Jenkins
- start TomCat 8.5.35

Use Jenkins job Artifactory - Devops to start installation of snapshot or release to Artifactory and to deploy war to Tomcat.

Job parameters:
- branch (choose branch to build)
- tag (create snapshot or release and upload to Artifactory)
- deploy (deploy war to Tomcat)


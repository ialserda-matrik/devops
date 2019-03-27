# devops
Spring Boot project with simple controller and tests. 
Main goal is to practice DEVOPS ( using Git, Jenkins, Artifactory, Sonar, ELK and Jira).

### Pre Requisite

- Configure Tomcat:

  - httpPort: 8080
  
     define this in the jenkins job which does the deployement to Tomcat
  
  - Script account: jenkins / welcome
  
    define this in the jenkins job which does the deployement to Tomcat

- Configure Artifactory:

  - httpPort: 8081
  
    define this in the root pom and the jenkins job which does the deployement to Artifactory and Tomcat


### Prepare for running CI:
- start Artifactory
- start Jenkins
- start TomCat 8.5.35


### Jenkin Jobs

- ArtifactoryDev
  
  Build a certain branch and optional make a release of it and push  the war file to Artifactory.
  Optional deploy the war file of this branch from workspace to Tomcat.
  
  Job parameters:
  - branch (choose branch to build)
  - tag (create snapshot or release and upload to Artifactory)
  - deploy (deploy war to Tomcat)
  
- ArtifactoryQA

  Build tagged version from Git and deploy from workspace to Tomcat.
  
  Job parameters:
    - tag (release tag to deploy)
  
- ArtifactoryProd

  Build tagged version from Artifactory and deploy to Tomcat.

  Job parameters:
  - tag (release tag to deploy)


### Make a new release
- Configure the right artifact version snapshot number in the root pom in the development branch.
- Commit and push the development branch to remote.
- Make release branch from development branch using gitFlow. Set version ( use pattern vMajor.Minor.Build ) to snapshot version without SNAPSHOT text.
- Push release branch to remote.
- Start Jenkins job ArtifactoryDev and choose release branch, enable tag checkbox and optional enable deploy checkbox.
- Pull deploy changes from remote/release branch into local release branch.
- Merge local release branch into master and developer branch. Solve any merge conflicts. Now the developer en master branch have updated version numbers that points to a new release number.
- Remove release branch local and remote.
### JENKINS PIPELINES
---------------------------------------
A Jenkinsfile can be written using two types of syntax - Declarative and Scripted.
In jenkins console we can write a pipeline as well without use of vscode.
So in the jenkins console we also have types of pipelines
  
  * FREESTYLE PROJECT
     
     *A type of project that allows you to build, test, and deploy software using a variety of different options and configurations
  
  * PIPELINE
     
     * A suite of plugins which supports implementing and integrating continuous delivery pipelines into Jenkins. A continuous delivery pipeline is an automated expression of your process for getting software from version control right through to your users and customers.
  
  * MULTI-CONFIGURATION PROJECT
     
     * we can create only one job with many configurations. Each configuration will be executed as a separate job. This is exactly what we need to simplify our scheduled tests, which can be used in conjunction with TestComplete or TestExecute. 
  
  * FOLDER
     
     * This plugin allows users to create "folders" to organize jobs.   

  * MULTIBRANCH PIPELINE
     
     * A multi-branch pipeline is a concept of automatically creating Jenkins pipelines based on Git branches. It can automatically discover new branches in the source control (Github) and automatically create a pipeline for that branch.
 
  * ORGANIZATION FOLDER
     
     *Organization Folders enable Jenkins to monitor an entire GitHub Organization, Bitbucket Team/Project, GitLab organization, or Gitea organization and automatically create new Multibranch Pipelines for repositories which contain branches and pull requests containing a Jenkinsfile .


### Declarative Pipeline GAME OF LIFE
---------------------------------------
1. Declarative Pipeline presents a more simplified and opinionated syntax on top of the Pipeline sub-systems.
2. The basic statements and expressions which are valid in Declarative Pipeline follow the same rules as Groovy’s syntax with the following exceptions:
3. ![pre](images/basic%20structure%20of%20pipeline.png)
4. So we will be creating our pipeline through following this method.
5. Now lets create a pipeline for "game of life". Pipeline should be written by the help of jenkins pipeline steps 
6. ![refer here]https://www.jenkins.io/doc/book/pipeline/syntax/#agent
7. So here we have written a declarative pipelie of game of life in that we made some mistakes so please check the previous commits also 
8. ![refer here]https://github.com/NADEEMSHAI/Jenkins/blame/main/Jenkinsfile
9. Here the process of pipeline written
     
     * I had forked the gameoflife into my gitrepo.
     * Next i need to specify the agent in that labels to determine that jenkinsfile will run on that node only.
     * After i used trigger to tell that when should it run.
     * Parametes is a job what i want jenkins to do with the code.
     * So i have to give needed tools to run this code.
     * So there are other which you can define here i need that it so ill go with stages in that stage in that steps.
     * Steps is the real job were work we will done before that it just a infra.
     * So i given the git link in https to code get clone and if you have rather than master branch you need to specify that branch also like main,dev,test.
     * So after code get clone i have to write a next stage to determine that what should do with that code.
     * I need to do mvn package. So the work was done 
     * ![pre](images/j2.png)
     * ![pre](images/j1.png)
  
10. So above steps i have just done mvn package after that i need to do the package in to artifacts.
11. ![refer here]https://github.com/NADEEMSHAI/Jenkins/commit/f063d415aef40c33f0a7f3bd8f71f2a0921070ee
12. So here i had build the artifacts and also junit test. Here also i have made more commits please the all commit and changes 
13. ![pre](images/j3.png)
14. So here you can see the artifacts build sucessfully.


### Declarative Pipeline for SPRING PET CLINIC
------------------------------------------------------

1. Now we are writing the pipeline for spring pet clinic in the same method. For spc we need latest version of maven and java-17.
2. So let us first setup the tools. For that we need to download the mvn latest version 3.9.0 which is zip file and untar it after that set up the path of maven latest. Install java-17.

```
cd /tmp
wget https://dlcdn.apache.org/maven/maven-3/3.9.3/binaries/apache-maven-3.9.3-bin.tar.gz
sudo mkdir /usr/share/maven
sudo tar -xvzf apache-maven-3.9.3-bin.tar.gz -C /usr/share/maven
# add /usr/share/maven/apache-maven-3.9.3/bin to the PATH variable
# add to ~/.bashrc or /etc/environment
mvn --version
```
3. We need to add the tools in jenkins console like java versions as well as maven.
4. ![pre](images/j6.png)
5. ![pre](images/j7.png)
6. So we have set up the maven path and java after that we need to write the pipeline
7. ![pre](images/j4.png) 
8. so we have successfully build that pipeline.
9.  ![pre](images/j5.png)
10. Let us put the artifact in Jfrog. For that we need to create a free acc of Jfrog and link to jenkins.
11. This is the JFROG artifact jenkins pipeline configuration ![refer here]https://directdevops.blog/2019/10/17/artifactory-configuration/ 


### JFROG INTEGRATION WITH JENKINS
----------------------------------------

1. Lets us create a Jfrog account with Gmail as well as a repositary of maven.
    * ![pre](images/j8.png)
    * ![pre](images/j9.png)
    * we need to create a user and password for that go to settings > user management > tick the adiminstrater box.
    *  ![pre](images/j10.png)
    * create a group add user into the group. 
    * ![pre](images/j11.png)
    * Genrate access token.
    * ![PRE](images/J12.png)
    * Take the url of jforg portal to access.
    * ```
      https://nadeemjfrog.jfrog.io/
    ```
2. Goto the Jenkins console and add the token in credentails part just like ssh key added.
    * ![pre](images/j13.png)
    * ![pre](images/j14.png)
    * Now go to manage jenkins > system > scorll to Jfrog section here give instance id (anyting) and url of Jfrog.
    * ![pre](images/j15.png)
    * Here you need to tick the box of " Use the Credentials Plugin " after that untick onces then you can able to see " credentials " in that you can select that token which we added in credentials plugin.
    * If you observer their is an option to " Test Connection " click and test weather it configured correctly or not. 
  

### Lets Build SPC With Artifacts Stored In Jfrog
---------------------------------------------------------

1. This is a git repositary for example to write a pipeline spc with artifacts stored in jfrog.
   ![refe here]https://github.com/jfrog/project-examples/blob/master/jenkins-examples/pipeline-examples/declarative-examples/jenkins-with-jfrog-pipelines/Jenkinsfile
2. Here we no need to mention the shell script sh command mvn package because we want to just build and package in Jfrog.
3. We need to write some of below steps which we needed only.
    * rtServer 
    * rtMavenResolver
    * rtMavenDeployer
    * rtMavenRun
    * rtPublishBuildInfo
    * rtDockerPush
4. 




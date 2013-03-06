Juju charm using Jenkins
---------------------------------

This charm builds an environment of continuous integration using Jenkins to build projects.

The charm automatically install Ant, Junit, openJDK, Unzip, Git, Jenkins and Jenkins CLI. For Jenkins install the following plugins: ant, promoted-builds, mask-passwords, client-git, git, github, github-api, github-oauth, github-plugin-sqs.

You have to create a repository called builder in github where you can put all dependencies that you will use to create a job in Jenkins. To install the dependencies and other things you can create a script in bash with the name "script". 

The builder that is cloned from the git repository should contain a file called config.xml where is the settings to create a job. The Charm creates the job based on this .xml file.

To install this charm the machine using the HP Cloud  must be of the type standard.medium, that should be added at the time of service deployment.

Example:

juju deploy n3phele -- constraints "instance-type = standard.medium"
---------------------------------------------------------------------------------------

Additional configurations:

The charm has some configurations that can be added as:


Add to jenkins plugins:

juju set n3phele plugins = "plugin name"


Add the github URL of builder repository:

juju set n3phele  builder= "git URL of builder"

*This configuration clone the repository using the url builder passed as parameter. 
In the folder builder, should contain the config.xml and dependencies, if have,
as may contain a shell script to execute.


Create a job with config.xml file in builder:

juju set n3phele job = "job name"

To access the service give the command:
--------------------------------------------

juju expose n3phele

After that Jenkins will be accessible via http://public-adress:8080/


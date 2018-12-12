# build-help-portal

* The dockerfile in md2html/ pulls the markdown from the content-help-site git repo and pushes the generated html to help-site git repo

* The dockerfile in apache/ creates a container with the help-site content pulled from git to enable the website to be accessible at port localhost:8080

##PROCESS

cd * Install Docker
  * https://docs.docker.com/install/linux/docker-ce/ubuntu/#prerequisites


* Clone the Build Help Portal repository
  * https://github.com/ggeorgelewis/build-help-portal.git   

* Execute the build process that generates help-site html from markdown available in content-help-portal and pushes it to the help-portal git repo

  * cd mdhtml2/
        * sudo docker build --build-arg GITHUB_TOKEN=YOURTOKENHERE --build-arg GITHUB_USERNAME=YOURUSERNMAME --build-arg GITHUB_EMAIL=YOURMEMAIL@DOMAIN.com -t build-help-site  .  
        * run the container
            * sudo docker run -dit --name build-help-site-live build-help-site        
        * copy the files
            * cd ../apache2
            * sudo docker cp build-help-site-live:/build/_site help-portal/        


* To Host the help-portal on an apache webserver build the apache/dockerfile to create a container hosting the website on apache ubuntu
    
  * cd apache2/
      * sudo docker build -t help-site  .  
 
  * run the container to make the website accessible
      * sudo docker run -dit --name host-help-site-running -p 8080:80 host-help-site 
 
  * Visit the website at http://localhost:8080 or http://serverIP:8080
 
##Save Image
* To save the docker image as a tar.gz file follow the following instructions 
  * 
  *  https://docs.docker.com/engine/reference/commandline/save/
  
  
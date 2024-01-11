1) Tools used:
  ✓ Git - For version control for tracking changes in the code files
  ✓ Maven – For Continuous Build
  ✓ Jenkins - For continuous integration and continuous deployment
  ✓ Docker - For deploying containerized applications
  ✓ Ansible - Configuration management tools

2)Cloud Provider: Amazon Web Services

3)Resources used:
   t2.small  --> As Jenkins Server and Ansible Server.
   t2.micro  --> As Ansible worker node where container is deployed

4) I have installed Jenkins, docker and ansible on t2.small aws ubuntu server.

5) Written the Cicd pipeline using Jenkins to checkout , build, containerize push the container on dockerhub and deploy it on ansible slave machine.

6) You can access the project through http://44.211.81.246:8084/

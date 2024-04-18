1) ECR: Elastic Container resigtry 
   - ECR is conatiner regitry similar to docker hub
   - Its fully managed docker container resistery 
   - ECR vs DockerHub
        - ECR support by defult private repository (We can create public repo also )
        - Access is managed by IAM and repositry policy permission
    
    - Steps to User ECR
       1) You need to login aws ecr using below command
          - aws ecr get-login-password --region ca-central-1 | docker login --username AWS --password-stdin 908566580291.dkr.ecr.ca-central-1.amazonaws.com
       2) You can build your image using command:  docker build -t demo-repositry .
       3) after that you need to tag you docker image using command
           - docker tag demo-repository:latest 908566580291.dkr.ecr.ca-central-1.amazonaws.com/demo-repository:latest
       4) once above operation done you can push image using
           - docker push 908566580291.dkr.ecr.ca-central-1.amazonaws.com/demo-repository:latest

 2) EKS : Elastic Kubernetes Service
      - Managed service
      - 
      

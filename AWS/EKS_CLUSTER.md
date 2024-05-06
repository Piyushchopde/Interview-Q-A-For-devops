- Step 1: During creation of EKS Cluster first you need to create 2 roles one for EKS Cluster Service Role amd Secound is for EKS Work Node 

- Step 2: EKS-Cluster-Service-role is Allow access to other AWS service that requried to operate Cluster managed by EKS and we need to Attched Policy  AmazonEKSClusterPolicy

- Step 3: EKS_Woker-Node-Role we need to attched AmazonEKSWorkerNodePolicy , AmazonEC2ContainerRegistryReadOnly, CloudWatchLogsFullAccess , AmazonEKS_CNI_Policy

- Step 4 : After created Policy we need to go EKS Service and create cluster In cluster configuration you need to mensition about Name,K8S Version,Attch Cluster service role,Use VPC, Subnets ,Cluster IP address family ,enable configuration logging then review and create cluster

- Step 5 : once you created cluster you need to add NodeGroup In Compute section Node Goup is present add node group and provide node group configuration ,Node IAM Role ,AMI Type,Capacity type, Instance types,Disk size,Minumum size and maximun size and create node group cluster under EKS Cluser 



Referance : https://medium.com/@mycloudjourney/provision-aws-eks-from-the-aws-console-8c253595a546

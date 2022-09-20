In first place, i'll ennumerate the AWS resources that would be part of the arquitecture. 
 to create a versioned IaC of all the components with Terraform, "A must" is to have a contingency environment within another region, it should be turned on in case there occurs problems in the regions used in our main environment. the switching strategy should be handled(my choice) ArgoCD and the Terraform plan. Each plan must consider at least 2 AZ and to have each AZ one piece of each resource below descripted.
 Route 53 to handle the request trought our diferent landings, it must to have attached the SSL certificates, I recommend to have a single wildcard certificate with 3 sublevels.
Cloudfront to handle the static content for faster reponse also reduce the resources usage.
ALB for to balance the traffic trough our target services
EKS Service so the services are distributed into a microservices schema with high availability. 
I'll choose two types of nodes for the EKS cluster, On Demand and Spot nodes, the ondemand will ensure that we allways count with a starter infrastructure as our system and the Spot nodes will scale horizontally depending what our troughput requires
VPCs, the EKS should be contained in multiple Availability zones so we can avoid posibles outages of the AZs of AWS. 
Redis. For caching our Application services containers inside EKS.
Volumes. we should define EFS and EBS for RWX PV provisioning and EBS for RWO provisioning volumes. StorageClasses aws-ebs and aws-efs. ie. ebs for redis and efs for our microservices.
Aurora MySQL DB because the features that comes within. HA, Reliability and Durability, as the most valuable. Then the administration is simplest thant RDS, and the failover strategy is predefined and is a main feature of Aurora.
ECR for to storage the versioned images of the microservices.
Secret manager and Parameter Store, so we can have separated the sensitive data and the variables respectively.

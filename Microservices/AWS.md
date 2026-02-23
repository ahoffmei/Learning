# AWS Microservice Overview

## Overview
Focusing on the microservices that matter most for common web dev environments. 

## Other Things
### Managed vs Unmannged services 
- Unmanaged Service: Services that are pretty much just built on top of a VM under the hood. Something like and EC2 instance or something. 
- Managed Service: Services that have some sort of backend abstraction. Something like S3 where it handles the functionality for you. Something like S3. 

### Regional vs global 


### Observability
Monitoring is important. You can get most of that from a cloud provider like AWS. 
Datadog, not AWS, is allegedly better observability than the major cloud providers. 


### Regional vs Global 
- Content Delivery Networks (CDN) is an example of a global service. A CDN is a distribution of services
- EC2 is inherently regional, since you need it hosted on a specific region.   

---
# Services 
---

# S3 
Simple storage service of (object store). At it's core it's a mechanism to read and write files. Main benefit is that it manages the amount of storage you need.  
Benefit also for scaling to the amount you score. In the nature of cloud computing, don't pay for more storage than you need 
- Used for storing frequently accessed data in an availability zone

General Use Cases
- Archiving 
- Backup/Recovery 
- Media 

## S3 Glacier 
Archive access frequency . Used for data that is contained for years+. TODO More detail. 

## S3 Intelligent-Tiering
Unknown or changing access frequency. Optimizes cost by moving data to most cost-effective access-tier based on access. TODO More detail. 


# Lambda 
FaaS (Functions as a Service). If you want a function to trigger in the cloud on a certain action. 

General Use Cases:
- Do something when an object hits S3, like process an image. 
- Process an API request quickly???

Common Triggers (Need a trigger to run the lambda function): 
- HTTP request 
- S3 Upload
- DB Changes 

# ECS (Elastic Cloud Service)
Basically a glorified VM. Can also run docker containers on the cloud.  

Needs to be run on something though. 

## EC2 
Loads a container agent onto the EC2 machines. You can then handle multiple docker image on your EC2 machines. 

EC2 is technically it's own thing, so you can technically just remote into your EC2 instance and setup your own docker image, but we don't need. 

## AWS Fargate 
More serverless. You don't need to care about the hardware, it automatically scales services for you.  

## Key Terms  
- Task : Lowest level building block of ECS - runtime instances
- Task Definitions: Templates for you tasks, where yhou can specify docker images. 
- Container (EC2 Only): Virtualize instance that runs your task (so like docker). In turn, one of the benefits of fargate is that you automatically get task scaling, you don't care as much about 
- Cluster 
    - For EC2 this is a group of containers which run tasks 
    - For Fargate, it's just a group of tasks. They abstract the hardware part away. 
- Service: Task management syste that ensures X amount of tasks are up and running

## When to ECS+EC2 vs Fargate
Use EC2 + ECS when you either 
1. Have existing EC2 hardware that you want to leverage 
2. Have sustained and predictable tasks with high utilization (services)
3. Great for control 

Fargate when 
1. Spend less time on setup and maintenance
2. ADhoc jobs with variable utilization. Again ties into the serverless part. 
3. Great for flexibility.

In general use EC2 when you need services or Fargate for ad hoc stuff. 



# AWS Databases 
## Amazon Relational Database Service (AWS RDS)
Fully managed, web based distributed regional database engine. Simplifies setup of databases such as MySQL, PostgreSQL, Orcacle, etc... 
Good for handling backups, provisioning, patches, etc... 

## DynamoDB 
Just a Relational Database Server (RDS) based database service 
NoSql Database service 

## Redshift
AWS data warehouse platform. Think databricks. 

## AWS Athena 
Serverless. Good for handling data in a S3 bucket. Write a SQL Query and use it to search your bucket(s) for instance insight. 

---
# Non AWS Services 
---
# Vercel
AWS wrapper basically, making development, deployment, etc... easier to integrate. 
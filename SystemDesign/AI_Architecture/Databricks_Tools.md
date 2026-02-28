# Databricks 

--> more into specific tools/components on google drive 

## Technical Vision: 
- Can either do batch or stream processing (stream processing is for sensors and IOT while batch processing is logs, media, files, etc...)
- Batch data is then sent to next stage 

- Apache Spark + mlflow for processing 
- Medalion architecture: 
    - Bronze
    - Silver
    - Gold?????? what are these --> Delta lake

Serving Layer 
- Feeds to models, Opetaional databases, or data warehouses 

Analytics Layer 
- Users, analytics tools, and such can access it. 


## Main Components
Users:  
- Web Databricks Interface
- User and access management 
- Queries and Code 
- Also CLI access 
- ML and AI access 
- Workflow orchestration 
- Unity Catalog 

4 types of processing power:
- All purpose compute 
- classic job compute: Clusters for workload orchestration
- SQL warehouse compute
- Serverless : rent processing from databricks
 
Also has analytics tools, applications, etc.. top view this 
- Can access via SDK or API 

The web AI is pretty much 

Delta Lake --> tools for data engineers pretty much 

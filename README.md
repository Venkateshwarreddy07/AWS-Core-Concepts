# AWS-Compute-Concepts

COMPUTE SERVICES :

		○ EC2, Auto Scaling Groups, Elastic Load Balancer (ELB)
		○ AWS Lambda (Serverless compute)
		○ AWS Batch, Elastic Beanstalk
                Amazon ECS, EKS, Fargate!
		### **Amazon EC2 (Elastic Compute Cloud)**  

**Amazon EC2**

    EC2 is a scalable compute service that allows you to launch and manage virtual servers (instances) in the cloud. It provides complete control over the underlying infrastructure, enabling customization based on your application requirements.



### **Key Features**

    1. **Flexible Compute Options**: 
    - Choose from a wide variety of instance types optimized for different workloads (e.g., general-purpose, compute-optimized, memory-optimized, storage-optimized).
    2. **Customizable**: 
    - Full control over OS, software, and configurations.
    3. **Persistent Resources**: 
    - Ideal for applications that need to be always running or have stateful operations.
    4. **Scalability**: 
    - Supports manual, scheduled, or dynamic auto-scaling to adjust resources based on demand.
    5. **Pricing Models**: 
    - On-Demand, Reserved Instances, Spot Instances, and Savings Plans to optimize costs.


### **How It Works**
    1. **Launch**:  
     - Launch an EC2 instance with a specific OS and configuration through the AWS Management Console, CLI, or SDK.
    2. **Setup**:  
    - Install your application, libraries, and dependencies.
    3. **Scaling**:  
    - Manually configure or set up auto-scaling to handle varying traffic loads.
    4. **Integration**:  
     - Use Elastic Load Balancer (ELB) for load distribution, Elastic Block Store (EBS) for persistent storage, and VPC for networking.


### **Real-Time Example: Hosting a Web Application**

    **Scenario**: Deploying a WordPress Website  
    You need to host a WordPress site that requires persistent storage, consistent traffic, and a relational database.  

    **Architecture**:  
    1. **EC2 Instance**:  
    - Host the WordPress application and web server (e.g., Apache, Nginx).  
    2. **EBS Volume**:  
    - Store the WordPress files persistently.  
    3. **RDS**:  
    - Use Amazon RDS for the MySQL database.  
    4. **Elastic Load Balancer**:  
    - Distribute traffic across multiple EC2 instances for fault tolerance.  
    5. **Auto Scaling**:  
    - Automatically add or remove instances based on traffic load.  



### **Why and When to Use EC2 Over Lambda**

    - **Long-Running Processes**  
    - EC2 is suited for applications or tasks that need to run continuously or exceed Lambda's 15-minute execution limit.  
    - **Custom Compute Needs**  
    - Applications requiring specific OS configurations, GPUs, high memory, or CPU resources.  
    - **Consistent High Traffic**  
     - For high, predictable workloads, EC2 can be more cost-effective as it is not billed per request.  
    - **Persistent Applications**  
    - Services like web servers, gaming servers, or database applications that need to run 24/7.  



### **Comparison of EC2 vs. Lambda**   

    | **Criteria**             | **Lambda**                                    | **EC2**                                       |
    |--------------------------|-----------------------------------------------|-----------------------------------------------|
    | **Use Case**             | Event-driven tasks                           | Persistent, stateful applications             |
    | **Scalability**          | Automatic scaling                            | Manual or auto-scaling (requires setup)       |
    | **Control**              | Managed by AWS                               | Full control of OS, instance type, and setup |
    | **Billing**              | Pay-per-request and duration (milliseconds)  | Pay for uptime (hourly or per second)         |
    | **Customization**        | Limited                                      | Full control over configurations              |

    In summary, **Lambda is ideal for event-driven and short-lived tasks**, while **EC2 is better for long-running, resource-intensive, or stateful applications requiring full control**.

   AWS Lambda (Serverless Compute) :
   
     AWS Lambda is a compute service that enables you to run code without provisioning or managing servers. With Lambda, you focus only on writing your application logic while AWS automatically handles the infrastructure, scaling, patching, and server maintenance.

Key Features

	1. Event-Driven Execution: Lambda functions are triggered by events from AWS services (e.g., S3 uploads, DynamoDB updates, API Gateway requests) or external sources.
	2. Scalability: Automatically scales based on the number of requests.
	3. Pay-as-You-Go: Billed only for the compute time used, measured in milliseconds.
	4. Integrations: Supports a wide range of AWS services for building serverless architectures.
	5. Runtime Environment: Supports multiple languages (Node.js, Python, Java, Go, Ruby, .NET, and custom runtimes).

How It Works

	1. Trigger Event: An event (e.g., an S3 object upload) triggers the Lambda function.
	2. Execution: Lambda runs the code based on the event input in a pre-configured runtime environment.
	3. Response: Lambda performs the task (e.g., processing data, invoking another AWS service) and sends a response if required.
	4. Scale Automatically: Lambda handles concurrent execution of multiple invocations.

Real-Time Example: Image Processing Pipeline

    Scenario: Automatic Thumbnail Generation

     You have a web application where users upload images to an S3 bucket. Each uploaded image should automatically generate a thumbnail.
    Architecture:

	1. Trigger:
		○ The user uploads an image to an S3 bucket.
	2. Lambda Function:
		○ S3 triggers the Lambda function when a new object is created.
		○ The function reads the uploaded image, resizes it to create a thumbnail, and stores the thumbnail back in the S3 bucket.
	3. Workflow:
		○ Use AWS SDK in the Lambda function to process the image with a library like PIL (Python) or Sharp (Node.js).


why and when we use lambda over ec2  

    • Long-Running Processes
    Lambda has a maximum execution time of 15 minutes. Use EC2 for tasks requiring longer runtimes.
    • Complex Compute Needs
    Applications needing custom OS configurations, GPUs, or high memory/CPU.
    • Consistent High Traffic
    For high, consistent workloads, EC2 instances can be more cost-effective since Lambda billing is event-driven.
    • Persistent Applications
    EC2 is better for always-on services like web servers or database applications.

Concept of AWS Batch

    AWS Batch is a fully managed service designed to run batch computing jobs at any scale. It dynamically provisions compute resources, such as EC2 or Spot Instances, based on the volume and resource requirements of submitted jobs. AWS Batch is ideal for high-performance computing (HPC), machine learning, or any workload requiring a large volume of parallel computing tasks.

Key Features of AWS Batch:

	1. Job Management
		○ AWS Batch defines jobs and organizes them into job queues. Jobs can specify dependencies to run in a specific order.
	2. Compute Environment
		○ It manages a compute environment with EC2 instances or AWS Fargate for container-based jobs.
	3. Scaling
		○ Automatically scales resources to match the job queue demands, optimizing costs.
	4. Containerized Workloads
		○ Supports containerized workloads using Docker and works seamlessly with Amazon Elastic Container Registry (ECR).

Real-Time Example of AWS Batch

     Use Case: Genomic Analysis for Medical Research
	• Scenario:
     A pharmaceutical company needs to analyze the human genome data to identify disease markers. The workload involves processing hundreds of terabytes of data using genome sequencing algorithms.
	• Why AWS Batch?
		○ Each genome sequence analysis is a separate batch job.
		○ AWS Batch can scale resources dynamically to handle thousands of sequences simultaneously.
		○ With Spot Instances, the company minimizes computational costs.
		○ Job dependencies ensure workflows (data preprocessing, sequencing, result aggregation) run sequentially and reliably.

When to Use AWS Batch

    AWS Batch is suitable for:
	• Data Processing: ETL pipelines, log analysis, or image processing.
	• Scientific Simulations: Weather simulations, fluid dynamics, or molecular modeling.
	• Rendering Workloads: 3D rendering for films or visual effects.
	• Machine Learning: Training and inference workloads in batch mode.
	• Massive Parallel Computing: Financial modeling, risk analysis, or Monte Carlo simulations.

Secondary Options to AWS Batch

	1. Amazon ECS/Fargate
		○ Run containers with specific tasks, ideal for smaller-scale parallel workloads.
	2. AWS Step Functions
		○ Orchestrate and sequence long-running workflows, especially for serverless or low-code environments.
	3. Amazon EMR (Elastic MapReduce)
		○ Specifically designed for big data frameworks like Hadoop or Spark for data processing at scale.
	4. AWS Lambda
		○ Works well for lightweight, short-lived parallel workloads but is limited by execution time and resource caps.
	5. Kubernetes on AWS (Amazon EKS)
		○ Provides fine-grained control for containerized jobs in a batch processing scenario.

Comparison of Secondary Options

    Feature	AWS Batch	ECS/Fargate	Step Functions	Lambda	EMR	EKS
    Use Case	Batch jobs	Microservices, tasks	Workflow orchestration	Lightweight tasks	Big data processing	Custom container jobs
    Scalability	Automatic	Moderate	Based on orchestration	Limited	Very high	High
    Ease of Use	Managed	Moderate	High	High	Complex	Moderate
    Cost Efficiency	High with Spot	Moderate	Based on integration	Low-cost	Costly for small jobs	Moderate to high
    Job Dependencies	Supported	Manual	Built-in	Limited	Requires frameworks	Requires orchestration

Conclusion:

    AWS Batch is a powerful service for managing large-scale, compute-intensive workloads, especially those that are parallelizable. For simpler, real-time tasks or smaller-scale workloads, alternatives like Lambda, ECS, or Step Functions might be better suited. However, AWS Batch shines in cost optimization, scalability, and job orchestration for massive batch-processing jobs.


Elastic Beanstalk (EB) Concept:

    AWS Elastic Beanstalk is a Platform as a Service (PaaS) solution designed to simplify application deployment and management. It abstracts the underlying infrastructure, allowing developers to focus on writing code instead of provisioning and configuring resources. Elastic Beanstalk automatically handles capacity provisioning, load balancing, scaling, and application health monitoring.
Key Features

	1. Managed Service: Automatically provisions AWS resources such as EC2, RDS, ELB, Auto Scaling Groups, and S3 for the application.
	2. Multiple Programming Languages Supported: Java, .NET, Python, Ruby, Node.js, PHP, Go, and Docker.
	3. Customization: Developers can customize the environment with .ebextensions or by directly accessing the EC2 instances.
	4. Monitoring: Integrated with CloudWatch for performance metrics and logs.
	5. Ease of Use: Minimal configuration required; deploy code with ZIP files, WAR files, or Docker containers.

Real-Time Example

    Scenario: A Web Application for an E-Commerce Site
    Imagine you are deploying an e-commerce website built with a Java Spring Boot application.
	• Elastic Beanstalk Deployment:
		1. You upload your WAR file (Java application) through the Elastic Beanstalk console or CLI.
		2. Elastic Beanstalk automatically provisions EC2 instances, attaches an Elastic Load Balancer, sets up Auto Scaling policies, and configures the runtime environment.
		3. As traffic to your site increases during a sale, the Auto Scaling feature dynamically scales the number of instances to handle the load.
		4. You can monitor the health of the application using the EB dashboard or CloudWatch logs.

Use Cases

	1. Simplified Deployment for Developers: For teams that want to focus on coding rather than infrastructure setup.
	2. Rapid Prototyping: For quickly deploying applications during the development phase.
	3. Microservices Architecture: Deploying Docker containers with minimal setup.
	4. Startup Applications: Quick and cost-effective deployment for small to medium-scale applications.

Secondary Options for Elastic Beanstalk

    If Elastic Beanstalk doesn't fit your use case, consider the following alternatives:
	1. AWS Fargate
		○ For containerized workloads.
		○ Provides serverless compute for running Docker containers without managing the underlying instances.
	2. AWS Lambda
		○ Ideal for serverless applications or microservices.
		○ Automatically scales and charges only for execution time.
	3. AWS ECS or EKS
		○ ECS (Elastic Container Service) and EKS (Elastic Kubernetes Service) for container orchestration.
		○ More control over the environment compared to Beanstalk.
	4. Amazon Lightsail
		○ Simplified hosting service for small websites or applications with a predictable cost structure.
	5. AWS CloudFormation or CDK
		○ For fully customizable deployments, where you define your infrastructure as code.

When to Use Elastic Beanstalk?

	• When you need a managed environment for web applications with minimal configuration.
	• If you prefer to retain some control over the environment (e.g., access to EC2 instances).
	• For applications that don’t require fine-grained control over underlying infrastructure.
 



Amazon ECS, EKS, and Fargate
	      
       • Concepts:
		○ ECS (Elastic Container Service): A container orchestration service to run Docker containers. Best for applications with predictable workloads in AWS-managed clusters.
		○ EKS (Elastic Kubernetes Service): A managed Kubernetes service that enables containerized application deployment and scaling.
		○ Fargate: A serverless compute engine for ECS and EKS, where AWS manages the underlying infrastructure.
	• Real-Time Example:
		○ ECS: A company runs a microservices-based e-commerce website using ECS to manage Docker containers, each hosting a specific service (e.g., inventory, payments, user profiles).
		○ EKS: A startup uses EKS to deploy and scale Kubernetes clusters for an AI application requiring fine-grained workload balancing.
		○ Fargate: A development team leverages Fargate for a CI/CD pipeline to build and test containers without managing server instances.
	• Use Cases:
		○ ECS: Applications fully integrated with AWS services (e.g., ALB, CloudWatch).
		○ EKS: Multi-cloud or hybrid Kubernetes workloads.
		○ Fargate: Serverless container workloads without infrastructure management.
	• Secondary Options: AWS Batch, Lambda, Google Kubernetes Engine (GKE), Azure Kubernetes Service (AKS).




# S3
## Difference between pre-signed URLs, signed URLs, and signed cookies is S3
pre-signed URLs, signed URLs, and signed cookies are not the same. They are used in different scenarios to control access to your Amazon S3 objects or content distributed via Amazon CloudFront. Here's an explanation of each and the scenarios in which they are typically used:

### Pre-signed URLs
- **Purpose**: Provide temporary access to a specific S3 object.
- **Use Case**: Allow someone to download or upload a specific file without needing their own AWS credentials.
- **Example Scenarios**:
  - Temporarily sharing a private file with a user without making it publicly accessible.
  - Allowing a user to upload a file directly to your S3 bucket without having AWS credentials.
- **Generation**: Using AWS SDKs or AWS CLI.
  - **AWS CLI Command**: `aws s3 presign s3://your_bucket_name/your_object_key --expires-in seconds`

### Signed URLs
- **Purpose**: Control access to individual objects in CloudFront distributions.
- **Use Case**: Restrict access to specific files based on certain criteria such as time, IP address, or custom policies.
- **Example Scenarios**:
  - Providing temporary access to a video file hosted on CloudFront.
  - Granting access to a specific document in a secure manner for a limited time.
- **Generation**: Using AWS SDKs or custom applications with AWS security keys.

### Signed Cookies
- **Purpose**: Control access to multiple objects in a CloudFront distribution.
- **Use Case**: Allow access to multiple files, such as all the files in a private website, using a single policy.
- **Example Scenarios**:
  - Restricting access to an entire website hosted on CloudFront based on time or user attributes.
  - Allowing a user to browse multiple resources or media files without generating individual signed URLs for each.
- **Generation**: Using AWS SDKs or custom applications with AWS security keys.

### When to Use Each

#### Pre-signed URLs
- **Best For**: Granting temporary access to a single S3 object.
- **Example**: You have an application that allows users to download files. You can generate a pre-signed URL for each download request.

#### Signed URLs
- **Best For**: Controlling access to specific objects served by CloudFront with more granular control over each request.
- **Example**: You have a video streaming service and want to provide access to a specific video file for a limited period.

#### Signed Cookies
- **Best For**: Controlling access to multiple objects or entire paths served by CloudFront using a single policy.
- **Example**: You host a private website on CloudFront and want to allow users to access all resources (e.g., HTML, CSS, images) under a certain path for a limited period after they log in.

### Summary

| Feature          | Pre-signed URLs                                  | Signed URLs                                        | Signed Cookies                                    |
|------------------|--------------------------------------------------|---------------------------------------------------|--------------------------------------------------|
| **Purpose**      | Temporary access to a specific S3 object         | Control access to individual objects in CloudFront | Control access to multiple objects in CloudFront |
| **Use Case**     | Single file download/upload                      | Granular control for individual file access        | Access to multiple files or entire paths          |
| **Generation**   | AWS SDKs or CLI                                  | AWS SDKs or custom applications                    | AWS SDKs or custom applications                    |
| **Example**      | Share a file temporarily                         | Provide access to a specific video file            | Allow browsing of a private website               |

By understanding these different methods and when to use each, you can more effectively manage access to your content on AWS.
#### Synchronize Data to S3: 
Use the AWS CLI's s3 sync command to transfer the on-premises data to an S3 bucket. This initial synchronization allows ample time for the bulk of the data to be transferred to AWS without impacting daily operations.
# Dynamodb 
Certainly! Here are the key points about Amazon DynamoDB primary keys:

1. **Partition Key (Simple Primary Key):**
   - Consists of a single attribute.
   - DynamoDB uses the partition key's value as input to an internal hash function to determine the physical partition where the item is stored.
   - Ideal for scenarios where items are uniquely identified by a single attribute and do not require sorting within the partition.

2. **Partition Key and Sort Key (Composite Primary Key):**
   - Consists of two attributes: a partition key and a sort key.
   - The partition key determines the partition, and the sort key is used to order items within the partition.
   - Suitable for scenarios where items need to be grouped by the partition key and sorted by the sort key within each partition.
   - Supports efficient querying and retrieval of range-based data.

These two primary key structures in DynamoDB cater to different data access patterns and query requirements, enabling optimized performance and scalability for various application needs.
# NACL
When you create Network Access Control Lists (NACLs), you can specify both allow and deny rules. This is useful if you want to explicitly deny certain types of traffic to your application. For example, you can define IP addresses (as CIDR ranges), protocols, and destination ports that are denied access to the entire subnet. If your application is used only for TCP traffic, you can create a rule to deny all UDP traffic or vice versa. This option is useful when responding to DDoS attacks because it lets you create your own rules to mitigate the attack when you know the source IPs or other signatures.

# NLB
A Network Load Balancer operates at the connection level (Layer 4), routing connections to targets (Amazon EC2 instances, microservices, and containers) within Amazon VPC based on IP protocol data. Ideal for load balancing of both TCP and UDP traffic, Network Load Balancer is capable of handling millions of requests per second while maintaining ultra-low latencies. Network Load Balancer is optimized to handle sudden and volatile traffic patterns while using a single static IP address per Availability Zone.
For UDP traffic, the load balancer selects a target using a flow hash algorithm based on the protocol, source IP address, source port, destination IP address, and destination port. A UDP flow has the same source and destination, so it is consistently routed to a single target throughout its lifetime. Different UDP flows have different source IP addresses and ports so that they can be routed to different targets.

# AWS WAF
AWS Web Application Firewall (WAF) cannot directly protect a Network Load Balancer (NLB). AWS WAF is designed to protect web applications by filtering and monitoring HTTP and HTTPS traffic, and it is typically used in conjunction with an Application Load Balancer (ALB) or Amazon CloudFront, which handle HTTP/HTTPS traffic at Layer 7 of the OSI model.
# Neptune DB
Neptune DB is designed for graph application and loading CSV formatted data. Amazon QuickSight can directly use Neptune DB as a source.
# ENI
You can create and configure network interfaces in your account and attach them to instances in your VPC. Your account might also have requester-managed network interfaces, which are created and managed by AWS services to enable you to use other resources and services.
You can create a network interface, attach it to an instance, detach it from an instance, and attach it to another instance. The attributes of a network interface follow it as it's attached or detached from an instance and reattached to another instance. When you move a network interface from one instance to another, network traffic is redirected to the new instance.
Each instance has a default network interface, called the primary network interface. You cannot detach a primary network interface from an instance. You can create and attach additional network interfaces.

# Spot Fleet
A Spot Fleet is a set of Spot Instances and optionally On-Demand Instances that are launched based on criteria that you specify. The Spot Fleet selects the Spot capacity pools that meet your needs and launches Spot Instances to meet the target capacity for the fleet. By default, Spot Fleets are set to maintain target capacity by launching replacement instances after Spot Instances in the fleet are terminated. You can submit a Spot Fleet as a one-time request, which does not persist after the instances have been terminated. You can include On-Demand Instance requests in a Spot Fleet request.
 ### Allocation Strategy Options

The Spot Fleet uses various strategies to fulfill the Spot Fleet request efficiently:

- **Lowest Price**: Launches instances in the AZs with the lowest Spot price first, helping to minimize costs.
- **Diversified Instances across AZs**: Spreads instances across all selected AZs to maintain high availability and reduce the impact of interruptions in any single AZ.
- **Capacity-Optimized**: Launches instances in the AZs with the most available capacity. This helps to optimize for capacity availability while still considering price.
- **Capacity-Optimized with Prioritized Spot Pools**: Prioritizes instances in the Spot pools that have the most available capacity while also considering your price limits and instance type preferences.

# Amazon Aurora

1. **Auto-Failover and High Availability**:
   - Amazon Aurora supports automatic failover within the same AWS Region. In the event of a primary instance failure, Aurora automatically promotes a read replica to become the new primary, ensuring minimal downtime.
   - Failover typically occurs within 30 seconds or less, providing quick recovery and high availability for applications.
   - Aurora's architecture with multiple copies of data across different Availability Zones (AZs) within a Region enhances fault tolerance and reliability.

2. **Multi-Region Replication and Global Database**:
   - Aurora supports cross-Region replication, allowing you to create read replicas in different AWS Regions for disaster recovery and geographical data locality.
   - Aurora Global Database extends this capability further by enabling a single Aurora database to span multiple AWS Regions.
   - Global Database manages replication across Regions automatically, ensuring data consistency and enabling low-latency access to data globally.

3. **Performance and Scalability**:
   - Aurora is designed for high performance and scalability, offering fast read/write operations and low latency.
   - It uses a distributed, SSD-backed storage layer that automatically scales up to 64TB per database cluster without performance degradation.
   - Compute resources (CPU and memory) can be scaled independently of storage, allowing you to adjust performance based on workload demands.
# Step Functions
AWS Step Functions lets you coordinate multiple AWS services into serverless workflows so you can build and update apps quickly. Using Step Functions, you can design and run workflows that stitch together services, such as AWS Lambda, AWS Fargate, and Amazon SageMaker, into feature-rich applications.

**AWS Step Functions offer**:

 - Seamless workflow orchestration with state management, enabling easy tracking and resumption of workflows.
 - Automated retry and error handling, ensuring reliable processing of large batches with minimal manual intervention.
 - Scalable and concurrent execution capabilities, supporting multiple operations simultaneously for efficient workload management.
# AWS Network Firewall
AWS Network Firewall is a stateful, managed, network firewall and intrusion detection and prevention service for your virtual private cloud (VPC) that you created in Amazon Virtual Private Cloud (Amazon VPC). With Network Firewall, you can filter traffic at the perimeter of your VPC. This includes filtering traffic going to and coming from an internet gateway, NAT gateway, or over VPN or AWS Direct Connect.

Once AWS Network Firewall is deployed, you will see a firewall endpoint in each firewall subnet. Firewall endpoint is similar to interface endpoint and it shows up as vpce-id in your VPC route table target selection. You have multiple deployment models for Network Firewall.

For a centralized egress deployment model, an AWS Transit Gateway is a prerequisite. AWS Transit Gateway acts as a network hub and simplifies the connectivity between VPCs. For this model, we have a dedicated, central egress VPC which has a NAT gateway configured in a public subnet with access to IGW.

# Amazon WorkDocs
Amazon WorkDocs is a fully managed, secure content creation, storage, and collaboration service. With Amazon WorkDocs, you can easily create, edit, and share content, and because it’s stored centrally on AWS, access it from anywhere on any device. Amazon WorkDocs makes it easy to collaborate with others, and lets you easily share content, provide rich feedback, and collaboratively edit documents. You can use Amazon WorkDocs to retire legacy file share infrastructure by moving file shares to the cloud. Amazon WorkDocs lets you integrate with your existing systems, and offers a rich API so that you can develop your own content-rich applications. Amazon WorkDocs is built on AWS, where your content is secured on the world's largest cloud infrastructure.

# Cloudfront
Amazon CloudFront is a web service that speeds up the distribution of your static and dynamic web content, such as .html, .css, .js, and image files, to your users. CloudFront delivers your content through a worldwide network of data centers called edge locations. When a user requests content that you're serving with CloudFront, the request is routed to the edge location that provides the lowest latency (time delay) so that content is delivered with the best possible performance.
You create a CloudFront distribution to tell CloudFront where you want the content to be delivered from and the details about how to track and manage content delivery. Then CloudFront uses computers—edge servers—that are close to your viewers to deliver that content quickly when someone wants to see it or use it.

In general, if you’re using an Amazon S3 bucket as the origin for a CloudFront distribution, you can either allow everyone to have access to the files there or you can restrict access. To restrict access to content that you serve from Amazon S3 buckets, follow these steps:

 - Create a special CloudFront user called an origin access control (OAC) and associate it with your distribution.

 - Configure your S3 bucket permissions so that CloudFront can use the OAC to access the files in your bucket and serve them to your users. Make sure that users can’t use a direct URL to the S3 bucket to access a file there.

After you take these steps, users can only access your files through CloudFront, not directly from the S3 bucket.
You can configure a single CloudFront web distribution to serve different types of requests from multiple origins. For example, if you are building a website that serves static content from an Amazon Simple Storage Service (Amazon S3) bucket and dynamic content from a load balancer, you can serve both types of content from a CloudFront web distribution.

Follow these steps to configure a CloudFront web distribution to serve static content from an S3 bucket and dynamic content from a load balancer:
 - Open your web distribution from the CloudFront console.
 - Choose the Origins tab.
 - Create one origin for your S3 bucket and another origin for your load balancer.
 - Note: If you're using a custom origin server or an S3 website endpoint, you must enter the origin's domain name into the Origin Domain Name field.
 - From your distribution, choose the Behaviors tab.
 - Create a behavior that specifies a path pattern to route all static content requests to the S3 bucket. For example, you can set the "images/*.jpg" path pattern to route all requests for ".jpg" files in the images directory to the S3 bucket.
 - Edit the Default (*) path pattern behavior and set its Origin as your load balancer.
# RDS

Database sharding is the process of storing a large database across multiple machines. A single machine, or database server, can store and process only a limited amount of data. Database sharding overcomes this limitation by splitting data into smaller chunks, called shards, and storing them across several database servers. All database servers usually have the same underlying technologies, and they work together to store and process large volumes of data.

Amazon RDS Proxy is a fully managed, highly available database proxy for Amazon Relational Database Service (RDS) that makes applications more scalable, more resilient to database failures, and more. Amazon RDS Proxy sits between your application and your relational database to efficiently manage connections to the database and improve the scalability of the application. Amazon RDS Proxy can be enabled for most applications with no code changes.
Your Amazon RDS Proxy instance maintains a pool of established connections to your RDS database instances, reducing the stress on database compute and memory resources that typically occurs when new connections are established. RDS Proxy also shares infrequently used database connections so that fewer connections access the RDS database.
With RDS Proxy, you can build applications that can transparently tolerate database failures without needing to write complex failure-handling code. The proxy automatically routes traffic to a new database instance while preserving application connections. It also bypasses Domain Name System (DNS) caches to reduce failover times by up to 66% for Aurora Multi-AZ databases

# API Gateway
### Proxy Integration in API Gateway - Summary

1. **HTTP Proxy Integration:**
   - **Direct Passthrough:** Forwards the entire client request to the backend HTTP service and returns the backend's response to the client without modification.
   - **Simplified Setup:** Ideal for exposing existing HTTP endpoints with minimal configuration and no custom transformations.

2. **Lambda Proxy Integration:**
   - **Standardized JSON Handling:** Converts the client request to a JSON format for Lambda, allowing the function to process the request and return a customized response.
   - **Enhanced Control and Flexibility:** Suitable for implementing custom logic, interacting with other AWS services, and handling complex request and response transformations.
# AWS Client VPN
AWS Client VPN is a managed client-based VPN service that enables you to securely access your AWS resources and resources in your on-premises network. With Client VPN, you can access your resources from any location using an OpenVPN-based VPN client.
The administrator is responsible for setting up and configuring the service. This involves creating the Client VPN endpoint, associating the target network, configuring the authorization rules, and setting up additional routes (if required).
The client is the end user. This is the person who connects to the Client VPN endpoint to establish a VPN session. The client establishes the VPN session from their local computer or mobile device using an OpenVPN-based VPN client application.
The following are the key components for using AWS Client VPN.
-Client VPN endpoint — Your Client VPN administrator creates and configures a Client VPN endpoint in AWS. Your administrator controls which networks and resources you can access when establishing a VPN connection.
-VPN client application — The software application that you use to connect to the Client VPN endpoint and establish a secure VPN connection.
-Client VPN endpoint configuration file — A configuration file that's provided to you by your Client VPN administrator. The file includes information about the Client VPN endpoint and the certificates required to establish a VPN connection. You load this file into your chosen VPN client application.
# AWS CDK
AWS CDK allows developers to write infrastructure as code using familiar programming languages like Python and TypeScript, which they are already comfortable with.
# EC2Rescue
EC2Rescue can help you diagnose and troubleshoot problems on Amazon EC2 Linux and Windows Server instances. You can run the tool manually, or you can run the tool automatically by using Systems Manager Automation and the AWSSupport-ExecuteEC2Rescue document. The AWSSupport-ExecuteEC2Rescue document is designed to perform a combination of Systems Manager actions, AWS CloudFormation actions, and Lambda functions that automate the steps normally required to use EC2Rescue.

# AWS AppSync
AWS AppSync is a fully managed service that makes it easy to develop GraphQL APIs by handling the heavy lifting of securely connecting to data sources like Amazon DynamoDB, Lambda, and more. Adding caches to improve performance, subscriptions to support real-time updates, and client-side data stores that keep offline clients in sync are just as easy. Once deployed, AWS AppSync automatically scales your GraphQL API execution engine up and down to meet API request volumes.
AppSync can also be used for real-time collaboration. You can broadcast data from the backend to all connected clients (one-to-many) or between clients (many-to-many), such as in a second screen scenario where you broadcast the same data to all clients, who can then reply.

# CloudFront
You can use CloudFront with the on-premises website as the origin. CloudFront is a highly available, scalable service that can cache frequently accessed files on the website and can significantly make the load times faster.
# RPO and RTO
**RPO (Recovery Point Objective)**: The maximum acceptable amount of data loss measured in time; essentially, it indicates how much data can be lost during a disruption. 

**RTO (Recovery Time Objective)**: The maximum acceptable amount of time it should take to restore services after a disruption; it defines the target time to recover from an outage.

# Redshift
Amazon Redshift periodically takes snapshots of that cluster, usually every eight hours or following every 5 GB per node of data changes, or whichever comes first. Automated snapshots are enabled by default when you create a cluster.Amazon Redshift only has cross-region backup feature (using snapshots); it can't replicate directly to another cluster in another region.

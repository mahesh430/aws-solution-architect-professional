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

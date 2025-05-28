Provide your solution here:

Cloudfront, S3, Route53, API Gateway, EKS, RDS Aurora, RDS Proxy, Network Load Balancer, Elastic Cache, SNS

AWS Services and Their Roles in the System:
1. CloudFront
Role: AWS's global Content Delivery Network (CDN).

Purpose:

Caches and delivers static/dynamic content (e.g., web assets, APIs) with low latency.

Integrates with S3 (for static hosting) or API Gateway (for APIs).

Provides DDoS protection and HTTPS via AWS Shield and ACM certificates.

2. S3 (Simple Storage Service)
Role: Scalable object storage.

Purpose:

Stores static files (HTML, JS, images) for web apps (often paired with CloudFront).

Hosts logs, backups, or raw data for processing.

3. Route 53
Role: DNS and domain management service.

Purpose:

Routes user requests to CloudFront, ALB, or API Gateway via DNS records (A/AAAA, CNAME, Alias).

Supports health checks and failover for high availability.

4. API Gateway
Role: Fully managed API management layer.

Purpose:

Exposes REST/HTTP APIs to external users, integrates with backend services (e.g., EKS, Lambda).

Handles authentication, throttling, and request/response transformations.

5. EKS (Elastic Kubernetes Service)
Role: Managed Kubernetes service.

Purpose:

Hosts containerized microservices (e.g., Order Service, User Service).

Scales dynamically and deploys across Availability Zones for resilience.

6. RDS Aurora
Role: High-performance managed relational database.

Purpose:

Stores transactional data (e.g., user accounts, orders) with MySQL/PostgreSQL compatibility.

Offers multi-AZ replication for failover and read replicas for scalability.

7. RDS Proxy
Role: Database connection pool manager.

Purpose:

Reduces overhead on Aurora by managing persistent connections (critical for serverless apps like Lambda).

Improves security (IAM authentication) and failover handling.

8. Network Load Balancer (NLB)
Role: Layer 4 (TCP/UDP) traffic distributor.

Purpose:

Routes traffic to EKS pods or EC2 instances based on IP/port.

Handles high-throughput, low-latency workloads (e.g., gaming, APIs).

9. ElastiCache
Role: Managed Redis/Memcached service.

Purpose:

Caches frequently accessed data (e.g., session stores, database query results) to reduce Aurora load.

Improves application performance (sub-millisecond latency).

10. SNS (Simple Notification Service)
Role: Pub/sub messaging service.

Purpose:

Sends alerts (Amazon Alert™) or triggers workflows (e.g., order confirmations via email/SMS).

Integrates with Lambda, SQS, or HTTP endpoints.


Elaboration on why each cloud service is used and what are the alternatives considered ?

Answer:

1. CloudFront
Why Used:

Performance: Global CDN with edge locations reduces latency for users worldwide.

Security: Integrated DDoS protection (AWS Shield) and HTTPS via ACM.

Cost-Effective: Pay-as-you-go pricing with no upfront commitments.

3. Route 53
Why Used:

Reliability: 100% SLA uptime, global DNS resolution.

4. API Gateway
Why Used:

API Gateway: Handles API design, authentication, and authorization integrate with HTTP endpoints, and other services. Manages API lifecycle, monitoring, and security.

5. EKS
Why Used:

Containerization: Kubernetes-based container orchestration for microservices. Easy to scale, manage, and secure. integrate with AWS services.
- Easy to create new services and applications -> Flexible and scalable architecture. This system will be resilient to failures, scalable as our task need
Alternatives:

Serverless: Elastic Container Service (ECS) or AWS EC2 Autoscaling Group (ASG)

ECS and Lambda both is manage by AWS and provide similar features, but ECS is more flexible and scalable for container orchestration. Scalable base on cloudwatch metrixs.

6. RDS Aurora and RDS Proxy
Why Used:
Relational Database Service: MySQL-compatible database for mission-critical applications. Serverless architecture. Dont have to worry about database management and maintenance. When the peak of traffic comes, the database will automatically scale up to handle the load by Read and Write instaces. 

RDS Proxy: Provides a proxy layer for RDS instances, allowing for more granular control over database access and performance.


# Plans for scaling when the product grows beyond your current setup ?

Could consider Scaling Horizontal and Vertical for EKS clusters for backend. 

With high traffic, we can consider 2-3 NLBs because 1 NLB can handle 1000s of requests but will be timeout relate to the number of requests. additional NLBs can distribute traffic across multiple instances, ensuring high availability and scalability.

Aurora with RDS proxy already can scale up to handle the load by Read and Write instaces.If need we could consider Data Sharding and Replication.



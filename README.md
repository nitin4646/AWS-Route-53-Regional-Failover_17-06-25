# AWS-Route-53-Regional-Failover

Below steps are used for implementation:

🔹 What is Route 53 Regional Failover?

Amazon Route 53 Regional Failover is a DNS-based routing strategy used to automatically redirect traffic between AWS regions if one region becomes unhealthy. It helps achieve disaster recovery (DR) or high availability (HA) by shifting traffic to a standby region when the primary region fails.

🔹 How It Works

Primary Region (Active)
Your main application (EC2, ALB, API Gateway, etc.) runs here.
Route 53 health checks monitor endpoints (e.g., ALB DNS name, EC2 public IP, API Gateway).
If healthy → DNS queries resolve to this region.
Secondary Region (Passive / Standby)
A backup application stack deployed in another region.
Route 53 only routes traffic here if the primary health check fails.
Health Check + Failover Routing Policy
Health checks detect outages (HTTP(S), TCP, CloudWatch Alarms).
Failover routing policy switches traffic from primary to secondary automatically.

🔹 Failover Types

Active-Passive (most common)
Primary region handles all traffic; secondary is idle until failover.

Active-Active
Both regions serve traffic, and failover just redistributes to healthy endpoints.

🔹 Steps to Configure Regional Failover in Route 53

Deploy your app in two regions (Primary + Secondary).

Create health checks for your application endpoints.

Set up Route 53 hosted zone records:

Create a Primary record (Failover = Primary).

Create a Secondary record (Failover = Secondary).

Attach health checks to the Primary record.

DNS Resolution:

If Primary region is healthy → DNS resolves to Primary endpoint.

If Primary fails → Route 53 automatically returns Secondary endpoint.

🔹 Example Use Case

👉 Let’s say you have an e-commerce app:

Primary Region = us-east-1 (Virginia)

Secondary Region = ap-south-1 (Mumbai)

Route 53 Setup:

www.example.com → ALB in us-east-1 (Primary, with health check).

www.example.com → ALB in ap-south-1 (Secondary, no health check).

If us-east-1 goes down, Route 53 health check fails → traffic shifts to ap-south-1 automatically.


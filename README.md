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

---
description: Design cloud infrastructure using Terraform, Pulumi, or CloudFormation with VPC, compute, database, and storage
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert cloud architect specializing in Infrastructure as Code. Your task is to design and implement complete cloud infrastructure using IaC tools following the Well-Architected Framework.

## Steps

1. **Determine requirements**: Identify the cloud provider (AWS, GCP, Azure), IaC tool preference (Terraform, Pulumi, CloudFormation/CDK), application architecture (monolith, microservices, serverless), expected traffic, and compliance requirements.

2. **Network layer (VPC)**:
   - Create VPC with CIDR block allowing room for growth (e.g., /16)
   - Define public subnets (for ALB, NAT Gateway) across 2-3 availability zones
   - Define private subnets (for app servers, databases) across matching AZs
   - Set up NAT Gateway in each AZ for private subnet egress (or single for cost savings)
   - Configure route tables: public subnets route to Internet Gateway, private to NAT
   - Enable VPC Flow Logs for network monitoring
   - Add VPC endpoints for AWS services (S3, DynamoDB, ECR) to avoid NAT costs

3. **Security groups and NACLs**:
   - ALB security group: allow 80/443 from 0.0.0.0/0
   - App security group: allow app port only from ALB security group
   - Database security group: allow DB port only from app security group
   - Use security group references (not CIDR) for internal communication
   - Apply principle of least privilege; deny all by default

4. **Compute layer**:
   - **EC2/ASG**: Launch template with AMI, instance type, user data; auto-scaling policies based on CPU/request count; target tracking scaling
   - **ECS/Fargate**: Task definitions, service with desired count, capacity providers
   - **EKS**: Managed node groups, Fargate profiles, cluster autoscaler
   - **Lambda**: Function definitions, API Gateway integration, layers for dependencies

5. **Load balancing**:
   - Application Load Balancer with HTTPS listener and SSL certificate from ACM
   - Target groups with health check configuration
   - Path-based or host-based routing rules
   - Enable access logging to S3, connection draining, and sticky sessions if needed

6. **Database and storage**:
   - **RDS**: Multi-AZ deployment, automated backups, encryption at rest, parameter groups, subnet groups in private subnets
   - **ElastiCache**: Redis/Memcached cluster in private subnets for session/cache
   - **S3**: Buckets with versioning, encryption (SSE-S3 or SSE-KMS), lifecycle rules, access logging, block public access by default
   - **DynamoDB**: On-demand or provisioned capacity, global secondary indexes, point-in-time recovery

7. **State management and organization**:
   - Use remote state backend (S3+DynamoDB for Terraform, Pulumi Cloud for Pulumi)
   - Separate state files per environment (dev/staging/prod) and per layer (network/compute/data)
   - Use workspaces or directory structure for environment isolation
   - Lock state files during operations to prevent concurrent modifications
   - Tag all resources with Environment, Team, Project, ManagedBy labels

8. **Output**: Write all IaC files organized by module/component, provide a deployment order, and include a diagram description of the architecture. Add estimated cost considerations for the chosen resources.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->

---
title: "Container Insights on EKS"
sidebar_position: 50
sidebar_custom_props: { "module": true }
description: "Collect, aggregate and summarize metrics and logs from workloads on Amazon Elastic Kubernetes Service with Container Insights."
---
# Enabling CloudWatch Container Insights on Amazon EKS

### What is CloudWatch Container Insights?

**CloudWatch Container Insights** is a powerful monitoring tool that helps you collect, aggregate, and visualize metrics and logs from your containerized applications and microservices. It provides detailed information on resource utilization, including CPU, memory, disk, and network, as well as diagnostic data such as container restart failures. This allows you to quickly identify and troubleshoot performance issues in your containerized environment.

**Key benefits of CloudWatch Container Insights**:
- **Comprehensive monitoring**: Get real-time insights into resource utilization (CPU, memory, etc.) across all your containers and services.
- **Troubleshooting assistance**: Diagnoses container issues such as restarts and failures, allowing for quicker resolution.
- **Automatic dashboards**: Pre-configured CloudWatch dashboards display metrics at the cluster, node, pod, and service levels.
- **CloudWatch Logs Insights integration**: Enables advanced querying of logs for deeper analysis.
- **CloudWatch Alarms**: Set alarms based on the metrics you collect to proactively monitor and respond to changes in container health.

---

### Prerequisites

Before you begin, make sure you have the following tools installed and configured:

1. **AWS CLI** – Install the AWS CLI by following the [installation guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).
2. **eksctl** – Install `eksctl` using the [installation instructions](https://eksctl.io/introduction/#installation).
3. **kubectl** – Install `kubectl` by following the [Kubernetes official guide](https://kubernetes.io/docs/tasks/tools/install-kubectl/).
4. **IAM Role Permissions** – Attach the AWS managed policy `CloudWatchAgentServerPolicy` to your worker node IAM role to allow access to CloudWatch:

   ```bash
   aws iam attach-role-policy \
   --role-name my-worker-node-role \
   --policy-arn arn:aws:iam::aws:policy/CloudWatchAgentServerPolicy
### Installing the CloudWatch Observability EKS Add-on

To install the **CloudWatch Observability EKS add-on**, follow these steps:

1. **Install the Add-on Using `eksctl`:**

   ```bash
   eksctl create addon --name cloudwatch-observability \
   --cluster <cluster-name> \
   --region <region> \
   --service-account-role-arn arn:aws:iam::<account-id>:role/<worker-node-role-name>

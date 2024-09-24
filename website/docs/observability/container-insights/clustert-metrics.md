---
title: "Cluster metrics"
sidebar_position: 10
---

# Guide: Viewing and Analyzing EKS Cluster Metrics with CloudWatch Container Insights

## Introduction
This guide will help you navigate and analyze metrics from your Amazon EKS clusters using AWS CloudWatch **Container Insights**. You will learn how to access key performance metrics and use them to monitor the health and performance of your Kubernetes clusters.

## 1. Accessing Cluster Metrics via CloudWatch Container Insights

Once Container Insights is enabled on your EKS cluster, you can easily view your cluster’s key metrics in the CloudWatch console.

### Step 1: Navigate to CloudWatch Console
1. Sign in to the [AWS Management Console](https://aws.amazon.com/console/).
2. In the services search bar, type **CloudWatch**, then click on it.
3. On the left-hand side, expand **Container Insights**, and select **Performance Monitoring**.

![CloudWatch Console](./images/cloudwatch-console.png)

### Step 2: Select the EKS Cluster
1. Once in the **Performance Monitoring** section, you will see a list of available Kubernetes clusters. Select your Amazon EKS cluster.

![Cluster Selection](./images/cluster-selection.png)

### Step 3: View Cluster Overview
1. After selecting the cluster, you'll see an **Overview** dashboard. This shows you real-time metrics for:
   - **CPU utilization** (cluster-wide, by pod, by node)
   - **Memory usage**
   - **Network traffic**

![Cluster Overview](./images/cluster-overview.png)

## 2. Analyzing CPU, Memory, and Network Metrics

### Step 1: Analyzing CPU Utilization
1. In the **Overview** dashboard, click on the **CPU Utilization** section to dive deeper into CPU metrics.
2. You’ll see breakdowns for CPU usage by node, pod, and container.

![CPU Utilization](./images/cpu-utilization.png)

### Step 2: Analyzing Memory Utilization
1. Click on the **Memory Utilization** tab to view the memory usage of your cluster.
2. You can see the memory consumption by each node, pod, and container.
3. Look for any **high memory usage** nodes or pods to identify potential bottlenecks.

![Memory Utilization](./images/memory-utilization.png)

### Step 3: Analyzing Network Traffic
1. Select the **Network Traffic** tab to view data on incoming and outgoing network traffic in your cluster.
2. Use this to monitor spikes in network activity that could affect cluster performance.

![Network Traffic](./images/network-traffic.png)

## 3. Drill Down into Pod-Level and Node-Level Metrics

You can also drill down to get detailed metrics for individual nodes and pods.

### Step 1: View Pod-Level Metrics
1. In the **Performance Monitoring** section, click on the **Pods** tab.
2. This page will display key metrics like:
   - Pod CPU and memory usage
   - Pod restarts (which can indicate crashes)
   - Pod status (Running, Pending, etc.)

![Pod-Level Metrics](./images/pod-level-metrics.png)

### Step 2: View Node-Level Metrics
1. Similarly, click on the **Nodes** tab to view performance metrics for individual nodes in your cluster.
2. Use this page to identify any resource exhaustion or underperforming nodes.

![Node-Level Metrics](./images/node-level-metrics.png)

## 4. Setting Alarms for Cluster Metrics

CloudWatch allows you to set alarms on specific metrics, enabling you to monitor your cluster more proactively.

### Step 1: Create a New Alarm
1. In the CloudWatch dashboard, go to **Alarms** > **Create Alarm**.
2. Choose a metric to set an alarm for (e.g., **CPU utilization**).
3. Set a threshold for the metric. For example, set an alarm when CPU utilization exceeds 80%.

![Create Alarm](./images/create-alarm.png)

### Step 2: Configure Alarm Actions
1. Choose actions to take when the alarm is triggered, such as sending a notification via Amazon SNS or automatically scaling your EKS cluster.

![Alarm Actions](./images/alarm-actions.png)

## 5. Viewing and Analyzing Logs in CloudWatch Logs Insights

In addition to metrics, CloudWatch collects logs from your EKS cluster. These logs can help you troubleshoot performance issues.

### Step 1: Access Logs Insights
1. From the CloudWatch Console, click **Logs Insights** in the left-hand panel.
2. In the query editor, select your EKS log group.

![Logs Insights](./images/logs-insights.png)

### Step 2: Use Queries to Analyze Logs
1. Use basic queries like:
   ```bash
   fields @timestamp, @message
   | filter @message like /error/
   | sort @timestamp desc

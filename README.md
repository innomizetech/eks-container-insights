# Helm Chart for CloudWatch Container Insights

[CloudwatchContainerInsights](https://epsagon.com/how-to/streaming-eks-metrics-and-logs-to-cloudwatch/) is provides you with a single pane to view the performance of your Elastic Container Service (ECS), Elastic Kubernetes Service (EKS), and the Kubernetes platform running on an EC2 cluster. This tool collects, summarizes, and aggregates logs and metrics from your microservices and containerized applications. 

CloudWatch collects metrics like memory, CPU, disk space, and network statistics, while Container Insights offers diagnostics, such as container restart failures. With the combination of both, you can even set CloudWatch alarms on the metrics collected by Container Insights.

## Installing the Container Insight's Chart

### Default values:

    namespace: amazon-cloudwatch

    clusterName: devshared

    regionName: eu-west-2

### Installing steps:    
    - With default values: 
        helm install [release-name] eks-container-insights/
    - Installing with override values: 
        helm install [release-name] eks-container-insights/  --set regionName="test-region" --set namespace="test-namespace" --set="test-cluster"



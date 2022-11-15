# Helm Chart for CloudWatch Container Insights

[CloudwatchContainerInsights](https://epsagon.com/how-to/streaming-eks-metrics-and-logs-to-cloudwatch/) is provides you with a single pane to view the performance of your Elastic Container Service (ECS), Elastic Kubernetes Service (EKS), and the Kubernetes platform running on an EC2 cluster. This tool collects, summarizes, and aggregates logs and metrics from your microservices and containerized applications. 

CloudWatch collects metrics like memory, CPU, disk space, and network statistics, while Container Insights offers diagnostics, such as container restart failures. With the combination of both, you can even set CloudWatch alarms on the metrics collected by Container Insights.

## Installing the Container Insight's Chart

### Prerequisite
    An EKS cluster
    IAM Policy "CloudWatchAgentServerPolicy" attached to EC2 instance

### Default values:
Since CloudWatch Container Insights required some input parameters like namespace, cluster name, region, you must deploy the helm chart
with your values. Otherwise below values will be used as default.

    namespace: amazon-cloudwatch

    clusterName: devshared

    regionName: eu-west-2

### Installing steps

#### Installing using helm manifest files
    git clone https://github.com/innomizetech/eks-container-insights.git
    git checkout master
    - With default values: 
        helm install [release-name] eks-container-insights/        
    - Installing with override values: 
        helm install [release-name] eks-container-insights/  --set regionName="your-region" --set namespace="your-namespace" --set clusterName="your-cluster"

#### Installing using helm publish chart
    helm repo add eks-container-insights https://innomizetech.github.io/eks-container-insights
    helm repos list
        NAME                    URL
        eks-container-insights  https://innomizetech.github.io/eks-container-insights
    helm repo update
    helm install amazon-cloudwatch eks-container-insights/amazon-cloudwatch  --set regionName="your-region" --set namespace="amazon-cloudwatch" --set clusterName="your-cluster" 

### Expected Output
#### Cloudwatch Agent and Fluentd pods running.
    $ kubectl get all -n amazon-cloudwatch
    NAME                           READY   STATUS    RESTARTS   AGE
    pod/cloudwatch-agent-2fq46     1/1     Running   0          79m
    pod/fluentd-cloudwatch-4c4dq   1/1     Running   0          79m

    NAME                                DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
    daemonset.apps/cloudwatch-agent     1         1         1       1            1           <none>          79m
    daemonset.apps/fluentd-cloudwatch   1         1         1       1            1           <none>          79m
#### Amazon CloudWatch -> Log groups. Expected to have following logs:
    /aws/containerinsights/your-cluster/application
    /aws/containerinsights/your-cluster/dataplane
    /aws/containerinsights/your-cluster/host
    /aws/containerinsights/your-cluster/performance
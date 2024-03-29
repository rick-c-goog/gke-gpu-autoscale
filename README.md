DCGM Setup,

https://cloud.google.com/stackdriver/docs/managed-prometheus/exporters/nvidia-dcgm

kubectl edit operatorconfig -n gmp-public
```

Add the following section right above line start with metadata:

features:
      targetStatus:
        enabled: true


Go to restart collector:
kubectl rollout restart ds collector -n gmp-system

Setup Custom Metric Stackdriver adapter:

kubectl apply -f https://raw.githubusercontent.com/GoogleCloudPlatform/k8s-stackdriver/master/custom-metrics-stackdriver-adapter/deploy/production/adapter_new_resource_model.yaml

Cloud Monitoring Metric Name for HPA:
prometheus.googleapis.com/DCGM_FI_DEV_GPU_UTIL/gauge

HPA:

https://docs.nvidia.com/ai-enterprise/natural-language/0.1.0/scaling.html#autoscaling-the-triton-inference-server-deployment-with-kubernetes
# Eamli Service Configurations

## API Server Config

### Resources

The Helm chart creates the following resources:
* Ingress/Route
* Service
* Horizontal Pod Autoscaler
* NetworkPolicy
* Deployment
* Job (Database seeder)
* IAM (Service account, role & role binding)
* Secrets (DB password)

### Requirements
* Kubernetes version 1.13.0 or later
* Helm version 3.0.0 or later
* Service account with permission to install charts onto the cluster
* Database server

### Parameters

| Parameter                                         | Description                                |
| ------------------------------------------------- | ------------------------------------------ |
| `replicaCount`                                    | Specified number of identical pods to be available |
| `isOpenshift`                                     | Marks the chart as being installed onto an Openshift cluster |
| `image.repository`                                | Image repository address from which the helm chart will pull the image |
| `image.pullPolicy`                                | The image PullPolicy affect when the kubelet attempts to pull the specified image |
| `image.tag`                                       | The tag determines which version of the image to pull |
| `imagePullSecrets`                                | Secrets to be used to authentication, when pulling down images |
| `nameOverride`                                    | Overrides the default name for resources |
| `fullnameOverride`                                | Overrides the default full name (`{release/name}`) for resources |
| `serviceAccount.annotations`                      | Arbitrary non-identifying metadata |
| `serviceAccount.name`                             | Identifying name used for the service account |
| `serviceAccount.rules`                             | List of rules that apply to the service account |
| `podAnnotations`                                  | Arbitrary non-identifying metadata |
| `podSecurityContext`                              | Pod-level security attributes and common container settings |
| `securityContext`                                 | Defines privilege and access control settings for a Pod or Container |
| `service.type`                                    | How the Service is exposed (ExternalName/ClusterIP/NodePort/LoadBalancer) |
| `service.port`                                    | Port that traffic should be forwarded onto on the pod/s |
| `ingress.enabled`                                 | If enabled, creates the Ingress/Route definition |
| `ingress.host`                                    | Ingress/Route hostname/ip to process the incoming http traffic |
| `ingress.annotations`                             | Arbitrary non-identifying metadata |
| `ingress.tls.enabled`                             | Enable TLS for the service, to force HTTPS |
| `ingress.tls.secretName`                          | Name of the K8s Secret that contains the TLS certificate |
| `resources.limits.cpu`                            | Maximum amount of compute CPU allowed |
| `resources.limits.memory`                         | Maximum amount of compute Memory allowed |
| `resources.requests.cpu`                          | Minimum amount of compute CPU required |
| `resources.requests.memory`                       | Minimum amount of compute Memory required |
| `autoscaling.enabled`                             | Enable autoscaling on the deployment |
| `autoscaling.minReplicas`                         | MinReplicas is the lower limit for the number of replicas to which the autoscaler can scale down |
| `autoscaling.maxReplicas`                         | Upper limit for the number of pods that can be set by the autoscaler |
| `autoscaling.targetCPUUtilizationPercentage`      | Target average CPU utilization over all pods |
| `autoscaling.targetMemoryUtilizationPercentage`   | Target average Memory utilization over all pods |
| `nodeSelector`                                    | Selector which must match a node's labels for the pod to be scheduled on that node |
| `tolerations`                                     | Tolerates any taint that matches any listed values |
| `affinity`                                        | Determines how the pods should be schedule |
| `environment.name`                                | Name of the environment the application is running in |
| `environment.gunicorn.autoReload`                 | If value set, watches for file changes, and reloads server on change |
| `environment.gunicorn.jsonLoggin`                 | Pretty print json logs to console. |
| `environment.gunicorn.logLevel`                   | Level of debug printed to stdout, from very minal at Emergency to very verbose at Debug level. Available values: Emergency, Alert, Critical, Error, Warning, Notice, Informational, Debug |
| `environment.gunicorn.workerCount`                | How many separate process will be spun up to handle in-bound HTTP requests (Maximum is typically 2 x (number of cpu cores) + 1) |
| `environment.gunicorn.threadCount`                | The number of threads spun up per worker thread (Typically 1 should be enough) |
| `environment.seeder.demoEnabled`                  | If enabled, preloads the database with demo data |

## CoreModelServer Config

### Resources

The Helm chart creates the following resources:
* Ingress/Route
* Service
* Horizontal Pod Autoscaler
* NetworkPolicy
* Deployment
* Job (Database seeder)
* IAM (Service account, role & role binding)
* Secrets (DB password)

### Requirements
* Kubernetes version 1.13.0 or later
* Helm version 3.0.0 or later
* Service account with permission to install charts onto the cluster

### Parameters

| Parameter                                         | Description                                |
| ------------------------------------------------- | ------------------------------------------ |
| `replicaCount`                                    | Specified number of identical pods to be available |
| `image.repository`                                | Image repository address from which the helm chart will pull the image |
| `image.pullPolicy`                                | The image PullPolicy affect when the kubelet attempts to pull the specified image |
| `image.tag`                                       | The tag determines which version of the image to pull |
| `imagePullSecrets`                                | Secrets to be used to authentication, when pulling down images |
| `nameOverride`                                    | Overrides the default name for resources |
| `fullnameOverride`                                | Overrides the default full name (`{release/name}`) for resources |
| `serviceAccount.annotations`                      | Arbitrary non-identifying metadata |
| `serviceAccount.name`                             | Identifying name used for the service account |
| `serviceAccount.rules`                             | List of rules that apply to the service account |
| `podAnnotations`                                  | Arbitrary non-identifying metadata |
| `podSecurityContext`                              | Pod-level security attributes and common container settings |
| `securityContext`                                 | Defines privilege and access control settings for a Pod or Container |
| `service.type`                                    | How the Service is exposed (ExternalName/ClusterIP/NodePort/LoadBalancer) |
| `service.port`                                    | Port that traffic should be forwarded onto on the pod/s |
| `ingress.enabled`                                 | If enabled, creates the Ingress/Route definition |
| `ingress.host`                                    | Ingress/Route hostname/ip to process the incoming http traffic |
| `ingress.annotations`                             | Arbitrary non-identifying metadata |
| `ingress.tls.enabled`                             | Enable TLS for the service, to force HTTPS |
| `ingress.tls.secretName`                          | Name of the K8s Secret that contains the TLS certificate |
| `resources.limits.cpu`                            | Maximum amount of compute CPU allowed |
| `resources.limits.memory`                         | Maximum amount of compute Memory allowed |
| `resources.requests.cpu`                          | Minimum amount of compute CPU required |
| `resources.requests.memory`                       | Minimum amount of compute Memory required |
| `autoscaling.enabled`                             | Enable autoscaling on the deployment |
| `autoscaling.minReplicas`                         | MinReplicas is the lower limit for the number of replicas to which the autoscaler can scale down |
| `autoscaling.maxReplicas`                         | Upper limit for the number of pods that can be set by the autoscaler |
| `autoscaling.targetCPUUtilizationPercentage`      | Target average CPU utilization over all pods |
| `autoscaling.targetMemoryUtilizationPercentage`   | Target average Memory utilization over all pods |
| `nodeSelector`                                    | Selector which must match a node's labels for the pod to be scheduled on that node |
| `tolerations`                                     | Tolerates any taint that matches any listed values |
| `affinity`                                        | Determines how the pods should be schedule |
| `environment.name`                                | Name of the environment the application is running in |

## Executor Config

### Resources

The Helm chart creates the following resources:
* Service
* Horizontal Pod Autoscaler
* NetworkPolicy
* Deployment
* Job (Database seeder)
* IAM (Service account, role & role binding)
* Secrets (DB password)

### Requirements
* Kubernetes version 1.13.0 or later
* Helm version 3.0.0 or later
* Service account with permission to install charts onto the cluster

### Parameters

| Parameter                                         | Description                                |
| ------------------------------------------------- | ------------------------------------------ |
| `replicaCount`                                    | Specified number of identical pods to be available |
| `image.repository`                                | Image repository address from which the helm chart will pull the image |
| `image.pullPolicy`                                | The image PullPolicy affect when the kubelet attempts to pull the specified image |
| `image.tag`                                       | The tag determines which version of the image to pull |
| `imagePullSecrets`                                | Secrets to be used to authentication, when pulling down images |
| `nameOverride`                                    | Overrides the default name for resources |
| `fullnameOverride`                                | Overrides the default full name (`{release/name}`) for resources |
| `serviceAccount.annotations`                      | Arbitrary non-identifying metadata |
| `serviceAccount.name`                             | Identifying name used for the service account |
| `serviceAccount.rules`                             | List of rules that apply to the service account |
| `podAnnotations`                                  | Arbitrary non-identifying metadata |
| `podSecurityContext`                              | Pod-level security attributes and common container settings |
| `securityContext`                                 | Defines privilege and access control settings for a Pod or Container |
| `service.type`                                    | How the Service is exposed (ExternalName/ClusterIP/NodePort/LoadBalancer) |
| `service.port`                                    | Port that traffic should be forwarded onto on the pod/s |
| `resources.limits.cpu`                            | Maximum amount of compute CPU allowed |
| `resources.limits.memory`                         | Maximum amount of compute Memory allowed |
| `resources.requests.cpu`                          | Minimum amount of compute CPU required |
| `resources.requests.memory`                       | Minimum amount of compute Memory required |
| `autoscaling.enabled`                             | Enable autoscaling on the deployment |
| `autoscaling.minReplicas`                         | MinReplicas is the lower limit for the number of replicas to which the autoscaler can scale down |
| `autoscaling.maxReplicas`                         | Upper limit for the number of pods that can be set by the autoscaler |
| `autoscaling.targetCPUUtilizationPercentage`      | Target average CPU utilization over all pods |
| `autoscaling.targetMemoryUtilizationPercentage`   | Target average Memory utilization over all pods |
| `nodeSelector`                                    | Selector which must match a node's labels for the pod to be scheduled on that node |
| `tolerations`                                     | Tolerates any taint that matches any listed values |
| `affinity`                                        | Determines how the pods should be schedule |
| `environment.apiServerURL`                        | Addressable endpoint for Eamli API Server |
| `environment.elastisearchURL`                     | Addressable endpoint for Elasticsearch |
| `environment.coreModelServerURL`                  | Addressable endpoint for Eamli CoreModelServer |

## Product Server Config

The product server provides authentication server for authenticating requests through the Eamli services.

### Resources

The Helm chart creates the following resources:
* Service
* Horizontal Pod Autoscaler
* NetworkPolicy
* Deployment
* Job (Database seeder)
* IAM (Service account, role & role binding)
* Secrets (DB password)

### Requirements
* Kubernetes version 1.13.0 or later
* Helm version 3.0.0 or later
* Service account with permission to install charts onto the cluster

### Parameters

| Parameter                                         | Description                                |
| ------------------------------------------------- | ------------------------------------------ |
| `replicaCount`                                    | Specified number of identical pods to be available |
| `image.repository`                                | Image repository address from which the helm chart will pull the image |
| `image.pullPolicy`                                | The image PullPolicy affect when the kubelet attempts to pull the specified image |
| `image.tag`                                       | The tag determines which version of the image to pull |
| `imagePullSecrets`                                | Secrets to be used to authentication, when pulling down images |
| `nameOverride`                                    | Overrides the default name for resources |
| `fullnameOverride`                                | Overrides the default full name (`{release/name}`) for resources |
| `serviceAccount.annotations`                      | Arbitrary non-identifying metadata |
| `serviceAccount.name`                             | Identifying name used for the service account |
| `serviceAccount.rules`                             | List of rules that apply to the service account |
| `podAnnotations`                                  | Arbitrary non-identifying metadata |
| `podSecurityContext`                              | Pod-level security attributes and common container settings |
| `securityContext`                                 | Defines privilege and access control settings for a Pod or Container |
| `service.type`                                    | How the Service is exposed (ExternalName/ClusterIP/NodePort/LoadBalancer) |
| `service.port`                                    | Port that traffic should be forwarded onto on the pod/s |
| `ingress.enabled`                                 | If enabled, creates the Ingress/Route definition |
| `ingress.host`                                    | Ingress/Route hostname/ip to process the incoming http traffic |
| `ingress.annotations`                             | Arbitrary non-identifying metadata |
| `ingress.tls.enabled`                             | Enable TLS for the service, to force HTTPS |
| `ingress.tls.secretName`                          | Name of the K8s Secret that contains the TLS certificate |
| `resources.limits.cpu`                            | Maximum amount of compute CPU allowed |
| `resources.limits.memory`                         | Maximum amount of compute Memory allowed |
| `resources.requests.cpu`                          | Minimum amount of compute CPU required |
| `resources.requests.memory`                       | Minimum amount of compute Memory required |
| `autoscaling.enabled`                             | Enable autoscaling on the deployment |
| `autoscaling.minReplicas`                         | MinReplicas is the lower limit for the number of replicas to which the autoscaler can scale down |
| `autoscaling.maxReplicas`                         | Upper limit for the number of pods that can be set by the autoscaler |
| `autoscaling.targetCPUUtilizationPercentage`      | Target average CPU utilization over all pods |
| `autoscaling.targetMemoryUtilizationPercentage`   | Target average Memory utilization over all pods |
| `nodeSelector`                                    | Selector which must match a node's labels for the pod to be scheduled on that node |
| `tolerations`                                     | Tolerates any taint that matches any listed values |
| `affinity`                                        | Determines how the pods should be schedule |
| `environment.gunicorn.workerCount`                | The number of worker processes for handling requests |
| `environment.gunicorn.threadCount`                | The number of worker threads for handling requests |
| `environment.gunicorn.logLevel`                   | The granularity of Error log outputs |
| `environment.gunicorn.timeout`                    | Workers silent for more than this many seconds are killed and restarted |
| `environment.elasticsearch.host`                  | Host at which the Elasticsearch server is reachable at |
| `environment.elasticsearch.port`                  | Port on which the Elasticsearch server is reachable at |
| `environment.corsAllowedOrigin`                   | CORS header definition |
| `demo.enabled`                                    | If enabled, will load the database with dummy data |

## Source Data Server Config

### Resources

The Helm chart creates the following resources:
* Service
* Horizontal Pod Autoscaler
* NetworkPolicy
* Deployment
* Job (Database seeder)
* IAM (Service account, role & role binding)
* Secrets (DB password)

### Requirements
* Kubernetes version 1.13.0 or later
* Helm version 3.0.0 or later
* Service account with permission to install charts onto the cluster

### Parameters

| Parameter                                         | Description                                |
| ------------------------------------------------- | ------------------------------------------ |
| `replicaCount`                                    | Specified number of identical pods to be available |
| `image.repository`                                | Image repository address from which the helm chart will pull the image |
| `image.pullPolicy`                                | The image PullPolicy affect when the kubelet attempts to pull the specified image |
| `image.tag`                                       | The tag determines which version of the image to pull |
| `imagePullSecrets`                                | Secrets to be used to authentication, when pulling down images |
| `nameOverride`                                    | Overrides the default name for resources |
| `fullnameOverride`                                | Overrides the default full name (`{release/name}`) for resources |
| `serviceAccount.annotations`                      | Arbitrary non-identifying metadata |
| `serviceAccount.name`                             | Identifying name used for the service account |
| `serviceAccount.rules`                             | List of rules that apply to the service account |
| `podAnnotations`                                  | Arbitrary non-identifying metadata |
| `podSecurityContext`                              | Pod-level security attributes and common container settings |
| `securityContext`                                 | Defines privilege and access control settings for a Pod or Container |
| `service.type`                                    | How the Service is exposed (ExternalName/ClusterIP/NodePort/LoadBalancer) |
| `service.port`                                    | Port that traffic should be forwarded onto on the pod/s |
| `ingress.enabled`                                 | If enabled, creates the Ingress/Route definition |
| `ingress.host`                                    | Ingress/Route hostname/ip to process the incoming http traffic |
| `ingress.annotations`                             | Arbitrary non-identifying metadata |
| `ingress.tls.enabled`                             | Enable TLS for the service, to force HTTPS |
| `ingress.tls.secretName`                          | Name of the K8s Secret that contains the TLS certificate |
| `resources.limits.cpu`                            | Maximum amount of compute CPU allowed |
| `resources.limits.memory`                         | Maximum amount of compute Memory allowed |
| `resources.requests.cpu`                          | Minimum amount of compute CPU required |
| `resources.requests.memory`                       | Minimum amount of compute Memory required |
| `autoscaling.enabled`                             | Enable autoscaling on the deployment |
| `autoscaling.minReplicas`                         | MinReplicas is the lower limit for the number of replicas to which the autoscaler can scale down |
| `autoscaling.maxReplicas`                         | Upper limit for the number of pods that can be set by the autoscaler |
| `autoscaling.targetCPUUtilizationPercentage`      | Target average CPU utilization over all pods |
| `autoscaling.targetMemoryUtilizationPercentage`   | Target average Memory utilization over all pods |
| `nodeSelector`                                    | Selector which must match a node's labels for the pod to be scheduled on that node |
| `tolerations`                                     | Tolerates any taint that matches any listed values |
| `affinity`                                        | Determines how the pods should be schedule |
| `environment.name`                                | Name of the environment the application is running in |
| `environment.gunicorn.workerCount`                | The number of worker processes for handling requests |
| `environment.gunicorn.threadCount`                | The number of worker threads for handling requests |
| `environment.gunicorn.logLevel`                   | The granularity of Error log outputs |
| `environment.gunicorn.timeout`                    | Workers silent for more than this many seconds are killed and restarted |
| `environment.elasticsearch.host`                  | Host at which the Elasticsearch server is reachable at |
| `environment.elasticsearch.port`                  | Port on which the Elasticsearch server is reachable at |
| `environment.corsAllowedOrigins`                  | CORS header definition |

## Webapp UI Config

### Resources

The Helm chart creates the following resources:
* Service
* Horizontal Pod Autoscaler
* NetworkPolicy
* Deployment
* IAM (Service account, role & role binding)

### Requirements
* Kubernetes version 1.13.0 or later
* Helm version 3.0.0 or later
* Service account with permission to install charts onto the cluster

### Parameters


| Parameter                                         | Description                                |
| ------------------------------------------------- | ------------------------------------------ |
| `replicaCount`                                    | Specified number of identical pods to be available |
| `image.repository`                                | Image repository address from which the helm chart will pull the image |
| `image.pullPolicy`                                | The image PullPolicy affect when the kubelet attempts to pull the specified image |
| `image.tag`                                       | The tag determines which version of the image to pull |
| `imagePullSecrets`                                | Secrets to be used to authentication, when pulling down images |
| `nameOverride`                                    | Overrides the default name for resources |
| `fullnameOverride`                                | Overrides the default full name (`{release/name}`) for resources |
| `serviceAccount.annotations`                      | Arbitrary non-identifying metadata |
| `serviceAccount.name`                             | Identifying name used for the service account |
| `serviceAccount.rules`                             | List of rules that apply to the service account |
| `podAnnotations`                                  | Arbitrary non-identifying metadata |
| `podSecurityContext`                              | Pod-level security attributes and common container settings |
| `securityContext`                                 | Defines privilege and access control settings for a Pod or Container |
| `service.type`                                    | How the Service is exposed (ExternalName/ClusterIP/NodePort/LoadBalancer) |
| `service.port`                                    | Port that traffic should be forwarded onto on the pod/s |
| `ingress.enabled`                                 | If enabled, creates the Ingress/Route definition |
| `ingress.host`                                    | Ingress/Route hostname/ip to process the incoming http traffic |
| `ingress.annotations`                             | Arbitrary non-identifying metadata |
| `ingress.tls.enabled`                             | Enable TLS for the service, to force HTTPS |
| `ingress.tls.secretName`                          | Name of the K8s Secret that contains the TLS certificate |
| `resources.limits.cpu`                            | Maximum amount of compute CPU allowed |
| `resources.limits.memory`                         | Maximum amount of compute Memory allowed |
| `resources.requests.cpu`                          | Minimum amount of compute CPU required |
| `resources.requests.memory`                       | Minimum amount of compute Memory required |
| `autoscaling.enabled`                             | Enable autoscaling on the deployment |
| `autoscaling.minReplicas`                         | MinReplicas is the lower limit for the number of replicas to which the autoscaler can scale down |
| `autoscaling.maxReplicas`                         | Upper limit for the number of pods that can be set by the autoscaler |
| `autoscaling.targetCPUUtilizationPercentage`      | Target average CPU utilization over all pods |
| `autoscaling.targetMemoryUtilizationPercentage`   | Target average Memory utilization over all pods |
| `nodeSelector`                                    | Selector which must match a node's labels for the pod to be scheduled on that node |
| `tolerations`                                     | Tolerates any taint that matches any listed values |
| `affinity`                                        | Determines how the pods should be schedule |
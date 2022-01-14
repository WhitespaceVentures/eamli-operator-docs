# Eamli Service Configurations

## Stack Config

### Resources

The Helm chart creates the following resources:
* APIServer
* CoreModelServer
* Executor
* ProductServer
* SourceData
* WebApp

### Parameters

| Parameter                                         | Description                                |
| ------------------------------------------------- | ------------------------------------------ |
| `license.accept`                                  | Flag, to confirm you accept the eamli [EULA](https://eamli.com/eula) |
| `postgresql.host`                                 | Address of the PostgreSQL instance, reachable from within the cluster |
| `postgresql.port`                                 | Port to use for sending requests to the PostgreSQL instance |
| `postgresql.adminUsername`                        | PostgreSQL admin username, to generate users and databases with |
| `postgresql.adminDB`                              | Default PostgreSQL database |
| `ingress.enabled`                                 | If enabled, creates the Ingress/Route definition |
| `ingress.host`                                    | Ingress/Route hostname/ip to process the incoming http traffic |
| `ingress.annotations`                             | Arbitrary non-identifying metadata |
| `ingress.tls.enabled`                             | Enable TLS for the service, to force HTTPS |
| `ingress.tls.secretName`                          | Name of the K8s Secret that contains the TLS certificate |
| `apiserver`                                       | see [API Server Config](https://whitespaceventures.github.io/eamli-operator-docs/Config.html#api-server-config) |
| `coremodelserver`                                 | see [Core Model Server Config](https://whitespaceventures.github.io/eamli-operator-docs/Config.html#coremodelserver-config) |
| `executor`                                        | see [Executor Config](https://whitespaceventures.github.io/eamli-operator-docs/Config.html#executor-config) |
| `productserver`                                   | see [Product Server Config](https://whitespaceventures.github.io/eamli-operator-docs/Config.html#product-server-config) |
| `sourcedata`                                      | see [Source Data Config](https://whitespaceventures.github.io/eamli-operator-docs/Config.html#source-data-server-config) |
| `webapp`                                          | see [Webapp UI Config](https://whitespaceventures.github.io/eamli-operator-docs/Config.html#webapp-ui-config) |

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
* Database server

### Required Resources
The operator requires 400m CPU and 128Mi memory.

### Parameters

| Parameter                                         | Description                                |
| ------------------------------------------------- | ------------------------------------------ |
| `replicaCount`                                    | Specified number of identical pods to be available |
| `image.repository`                                | Image repository address from which the helm chart will pull the image |
| `image.pullPolicy`                                | The image PullPolicy affect when the kubelet attempts to pull the specified image |
| `image.tag`                                       | The tag determines which version of the image to pull |
| `serviceAccount.annotations`                      | Arbitrary non-identifying metadata |
| `serviceAccount.rules`                             | List of rules that apply to the service account |
| `podAnnotations`                                  | Arbitrary non-identifying metadata |
| `podSecurityContext`                              | Pod-level security attributes and common container settings |
| `securityContext`                                 | Defines privilege and access control settings for a Pod or Container |
| `autoscaling.enabled`                             | Enable autoscaling on the deployment |
| `autoscaling.minReplicas`                         | MinReplicas is the lower limit for the number of replicas to which the autoscaler can scale down |
| `autoscaling.maxReplicas`                         | Upper limit for the number of pods that can be set by the autoscaler |
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
* Database server

### Required Resources
The operator requires 200m CPU and 256Mi memory.

### Parameters

| Parameter                                         | Description                                |
| ------------------------------------------------- | ------------------------------------------ |
| `replicaCount`                                    | Specified number of identical pods to be available |
| `image.repository`                                | Image repository address from which the helm chart will pull the image |
| `image.pullPolicy`                                | The image PullPolicy affect when the kubelet attempts to pull the specified image |
| `image.tag`                                       | The tag determines which version of the image to pull |
| `serviceAccount.annotations`                      | Arbitrary non-identifying metadata |
| `serviceAccount.rules`                             | List of rules that apply to the service account |
| `podAnnotations`                                  | Arbitrary non-identifying metadata |
| `podSecurityContext`                              | Pod-level security attributes and common container settings |
| `securityContext`                                 | Defines privilege and access control settings for a Pod or Container |
| `autoscaling.enabled`                             | Enable autoscaling on the deployment |
| `autoscaling.minReplicas`                         | MinReplicas is the lower limit for the number of replicas to which the autoscaler can scale down |
| `autoscaling.maxReplicas`                         | Upper limit for the number of pods that can be set by the autoscaler |
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
* Database server

### Required Resources
The operator requires 200m CPU and 256Mi memory.

### Parameters

| Parameter                                         | Description                                |
| ------------------------------------------------- | ------------------------------------------ |
| `replicaCount`                                    | Specified number of identical pods to be available |
| `image.repository`                                | Image repository address from which the helm chart will pull the image |
| `image.pullPolicy`                                | The image PullPolicy affect when the kubelet attempts to pull the specified image |
| `image.tag`                                       | The tag determines which version of the image to pull |
| `serviceAccount.annotations`                      | Arbitrary non-identifying metadata |
| `serviceAccount.rules`                             | List of rules that apply to the service account |
| `podAnnotations`                                  | Arbitrary non-identifying metadata |
| `podSecurityContext`                              | Pod-level security attributes and common container settings |
| `securityContext`                                 | Defines privilege and access control settings for a Pod or Container |
| `autoscaling.enabled`                             | Enable autoscaling on the deployment |
| `autoscaling.minReplicas`                         | MinReplicas is the lower limit for the number of replicas to which the autoscaler can scale down |
| `autoscaling.maxReplicas`                         | Upper limit for the number of pods that can be set by the autoscaler |
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
* Database server

### Required Resources
The operator requires 200m CPU and 256Mi memory.

### Parameters

| Parameter                                         | Description                                |
| ------------------------------------------------- | ------------------------------------------ |
| `replicaCount`                                    | Specified number of identical pods to be available |
| `image.repository`                                | Image repository address from which the helm chart will pull the image |
| `image.pullPolicy`                                | The image PullPolicy affect when the kubelet attempts to pull the specified image |
| `image.tag`                                       | The tag determines which version of the image to pull |
| `serviceAccount.annotations`                      | Arbitrary non-identifying metadata |
| `serviceAccount.rules`                             | List of rules that apply to the service account |
| `podAnnotations`                                  | Arbitrary non-identifying metadata |
| `podSecurityContext`                              | Pod-level security attributes and common container settings |
| `securityContext`                                 | Defines privilege and access control settings for a Pod or Container |
| `autoscaling.enabled`                             | Enable autoscaling on the deployment |
| `autoscaling.minReplicas`                         | MinReplicas is the lower limit for the number of replicas to which the autoscaler can scale down |
| `autoscaling.maxReplicas`                         | Upper limit for the number of pods that can be set by the autoscaler |
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
* Database server

### Required Resources
The operator requires 100m CPU and 128Mi memory.

### Parameters

| Parameter                                         | Description                                |
| ------------------------------------------------- | ------------------------------------------ |
| `replicaCount`                                    | Specified number of identical pods to be available |
| `image.repository`                                | Image repository address from which the helm chart will pull the image |
| `image.pullPolicy`                                | The image PullPolicy affect when the kubelet attempts to pull the specified image |
| `image.tag`                                       | The tag determines which version of the image to pull |
| `serviceAccount.annotations`                      | Arbitrary non-identifying metadata |
| `serviceAccount.rules`                             | List of rules that apply to the service account |
| `podAnnotations`                                  | Arbitrary non-identifying metadata |
| `podSecurityContext`                              | Pod-level security attributes and common container settings |
| `securityContext`                                 | Defines privilege and access control settings for a Pod or Container |
| `autoscaling.enabled`                             | Enable autoscaling on the deployment |
| `autoscaling.minReplicas`                         | MinReplicas is the lower limit for the number of replicas to which the autoscaler can scale down |
| `autoscaling.maxReplicas`                         | Upper limit for the number of pods that can be set by the autoscaler |
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

### Required Resources
The operator requires 100m CPU and 64Mi memory.

### Parameters

| Parameter                                         | Description                                |
| ------------------------------------------------- | ------------------------------------------ |
| `replicaCount`                                    | Specified number of identical pods to be available |
| `image.repository`                                | Image repository address from which the helm chart will pull the image |
| `image.pullPolicy`                                | The image PullPolicy affect when the kubelet attempts to pull the specified image |
| `image.tag`                                       | The tag determines which version of the image to pull |
| `serviceAccount.annotations`                      | Arbitrary non-identifying metadata |
| `serviceAccount.rules`                             | List of rules that apply to the service account |
| `podAnnotations`                                  | Arbitrary non-identifying metadata |
| `podSecurityContext`                              | Pod-level security attributes and common container settings |
| `securityContext`                                 | Defines privilege and access control settings for a Pod or Container |
| `autoscaling.enabled`                             | Enable autoscaling on the deployment |
| `autoscaling.minReplicas`                         | MinReplicas is the lower limit for the number of replicas to which the autoscaler can scale down |
| `autoscaling.maxReplicas`                         | Upper limit for the number of pods that can be set by the autoscaler |
| `nodeSelector`                                    | Selector which must match a node's labels for the pod to be scheduled on that node |
| `tolerations`                                     | Tolerates any taint that matches any listed values |
| `affinity`                                        | Determines how the pods should be schedule |

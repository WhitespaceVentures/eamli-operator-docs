# Eamli Service Configurations

## API Reference

### Eamli

| Parameter         | Type                      | Required | Default          | Description |
| ----------------- | ------------------------- | -------- | ---------------- | ----------- |
| `license`         | [License][17]             | Y        | `{}`             | Provides a section for accepting the eamli licensing agreement |
| `ingress`         | [Ingress][14]             | Y        | `{}`             | Defines how eamli is exposed to public traffic |
| `apiserver`       | [EamliAPIServer][2]       | N        | `{}`             | API definition, for controlling the Eamli API Server within the cluster |
| `productserver`   | [EamliProductServer][5]   | N        | `{}`             | API definition, for controlling the Eamli Product Server within the cluster |
| `sourcedata`      | [EamliSourceData][7]      | N        | `{}`             | API definition, for controlling the Eamli Source Data within the cluster |
| `webapp`          | [EamliWebApp][9]          | N        | `{}`             | API definition, for controlling the Eamli Web App within the cluster |

### EamliAPIServer

| Parameter                 | Type                              | Required | Default          | Description |
| ------------------------- | --------------------------------- | -------- | ---------------- | ----------- |
| `replicaCount`            | Integer                           | N        | `1`              | Number of pods to create for this deployment |
| `image`                   | [Image][13]                       | N        | `{}`             | Defines the container image to be used for this service |
| `podAnnotations`          | [PodAnnotations][25]              | N        | `{}`             | Annotations to attach metadata to the pods. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `horizontalpodautoscaler` | [HorizontalPodAutoscaler][12]     | N        | `{}`             | The HorizontalPodAutoscaler defines how pods should scale for load. |
| `resources`               | [ResourceRequirements][23]        | N        | `{}`             | Specify how much of each resource a container needs. See [https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) |
| `nodeSelector`            | [NodeSelector][18]                | N        | `{}`             | Selector which must match a node's labels for the pod to be scheduled on that node. |
| `nodeName`                | String                            | N        | `""`             | Request to schedule pod onto a specific node. |
| `affinity`                | [Affinity Rules][19]              | N        | `{}`             | Pod's scheduling constraints. |
| `schedulerName`           | String                            | N        | `""`             | Pod will be dispatched by the specified scheduler. |
| `tolerations`             | [Tolerations][20]                 | N        | `{}`             | Pod's tolerations. |
| `environment`             | [EamliAPIServerEnvironment][3]    | N        | `{}`             | Defines the environment variables that are exposed to the service |

### EamliAPIServerEnvironment

| Parameter         | Type                      | Required | Default          | Description |
| ----------------- | ------------------------- | -------- | ---------------- | ----------- |
| `gunicorn`        | [Gunicorn][11]            | N        | `{}`             | Collection of Gunicorn settings that are exposed for tweaking service runtimes |
| `seeder`          | [APIServerSeeder][4]      | N        | `1`              | Configuration of how the API Server data is seeded |

### EamliAPIServerSeeder

| Parameter         | Type                  | Required | Default          | Description |
| ----------------- | --------------------- | -------- | ---------------- | ----------- |
| `demo`            | Boolean               | N        | `false`          | If set to true, demo data will be loaded onto the platform. |

### EamliProductServer

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `replicaCount`            | Integer                               | N        | `1`              | Number of pods to create for this deployment |
| `image`                   | [Image][13]                           | N        | `{}`             | Defines the container image to be used for this service |
| `podAnnotations`          | [PodAnnotations][25]                  | N        | `{}`             | Annotations to attach metadata to the pods. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `horizontalpodautoscaler` | [HorizontalPodAutoscaler][12]         | N        | `{}`             | The HorizontalPodAutoscaler defines how pods should scale for load. |
| `resources`               | [ResourceRequirements][23]            | N        | `{}`             | Specify how much of each resource a container needs. See [https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) |
| `nodeSelector`            | [NodeSelector][18]                | N        | `{}`             | Selector which must match a node's labels for the pod to be scheduled on that node. |
| `nodeName`                | String                            | N        | `""`             | Request to schedule pod onto a specific node. |
| `affinity`                | [Affinity Rules][19]              | N        | `{}`             | Pod's scheduling constraints. |
| `schedulerName`           | String                            | N        | `""`             | Pod will be dispatched by the specified scheduler. |
| `tolerations`             | [Tolerations][20]                 | N        | `{}`             | Pod's tolerations. |
| `environment`             | [EamliProductServerEnvironment][6]    | N        | `{}`             | Defines the environment variables that are exposed to the service |

### EamliProductServerEnvironment

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `gunicorn`                | [Gunicorn][11]                        | N        | `{}`             | Collection of Gunicorn settings that are exposed for tweaking service runtimes |
| `corsAllowedOrigin`       | String                                | N        | `*`              | The Access-Control-Allow-Origin response header indicates whether the response can be shared with requesting code from the given origin |

### EamliSourceData

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `replicaCount`            | Integer                               | N        | `1`              | Number of pods to create for this deployment |
| `image`                   | [Image][13]                           | N        | `{}`             | Defines the container image to be used for this service |
| `podAnnotations`          | [PodAnnotations][25]                  | N        | `{}`             | Annotations to attach metadata to the pods. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `horizontalpodautoscaler` | [HorizontalPodAutoscaler][12]         | N        | `{}`             | The HorizontalPodAutoscaler defines how pods should scale for load. |
| `resources`               | [ResourceRequirements][23]            | N        | `{}`             | Specify how much of each resource a container needs. See [https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) |
| `nodeSelector`            | [NodeSelector][18]                | N        | `{}`             | Selector which must match a node's labels for the pod to be scheduled on that node. |
| `nodeName`                | String                            | N        | `""`             | Request to schedule pod onto a specific node. |
| `affinity`                | [Affinity Rules][19]              | N        | `{}`             | Pod's scheduling constraints. |
| `schedulerName`           | String                            | N        | `""`             | Pod will be dispatched by the specified scheduler. |
| `tolerations`             | [Tolerations][20]                 | N        | `{}`             | Pod's tolerations. |
| `environment`             | [EamliSourceDataEnvironment][8]       | N        | `{}`             | Defines the environment variables that are exposed to the service |

### EamliSourceDataEnvironment

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `gunicorn`                | [Gunicorn][11]                        | N        | `{}`             | Collection of Gunicorn settings that are exposed for tweaking service runtimes |
| `corsAllowedOrigin`       | String                                | N        | `*`              | The Access-Control-Allow-Origin response header indicates whether the response can be shared with requesting code from the given origin |

### EamliWebApp

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `replicaCount`            | Integer                               | N        | `1`              | Number of pods to create for this deployment |
| `image`                   | [Image][13]                           | N        | `{}`             | Defines the container image to be used for this service |
| `podAnnotations`          | [AodAnnotations][25]                  | N        | `{}`             | Annotations to attach metadata to the pods. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `horizontalpodautoscaler` | [HorizontalPodAutoscaler][12]         | N        | `{}`             | The HorizontalPodAutoscaler defines how pods should scale for load. |
| `resources`               | [ResourceRequirements][23]            | N        | `{}`             | Specify how much of each resource a container needs. See [https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) |
| `nodeSelector`            | [NodeSelector][18]                | N        | `{}`             | Selector which must match a node's labels for the pod to be scheduled on that node. |
| `nodeName`                | String                            | N        | `""`             | Request to schedule pod onto a specific node. |
| `affinity`                | [Affinity Rules][19]              | N        | `{}`             | Pod's scheduling constraints. |
| `schedulerName`           | String                            | N        | `""`             | Pod will be dispatched by the specified scheduler. |
| `tolerations`             | [Tolerations][20]                 | N        | `{}`             | Pod's tolerations. |

### Gunicorn

| Parameter                 | Type                                  | Required | Default            | Description |
| ------------------------- | ------------------------------------- | -------- | ------------------ | ----------- |
| `jsonLogging`             | Boolean                               | N        | `false`            | Enable to set logs to print in JSON format |
| `logLevel`                | String                                | N        | `"INFO"`           | The granularity of Error log outputs |
| `workerCount`             | String                                | N        | `1`                | The number of worker processes for handling requests |
| `threadCount`             | String                                | N        | `""`               | The number of worker threads for handling requests |
| `timeout`                 | String                                | N        | `""`               | Workers silent for more than this many seconds are killed and restarted |

### HorizontalPodAutoscaler

| Parameter     | Type                                  | Required | Default          | Description |
| ------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `enabled`     | boolean                               | N        | `false`          | Flag to enable autoscaling of the service pods |
| `spec`        | [HorizontalPodAutoscalerSpec][21]     | N        | `""`             | See [https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) |

### Image

| Parameter                 | Type                      | Required | Default          | Description |
| ------------------------- | ------------------------- | -------- | ---------------- | ----------- |
| `repository`              | String                    | N        | `""`             | Container image source |
| `tag`                     | String                    | N        | `""`             | Tag of the container image |

### Ingress

| Parameter         | Type                  | Required | Default          | Description |
| ----------------- | --------------------- | -------- | ---------------- | ----------- |
| `host`            | String                | Y        | `""`             | Ingress/Route hostname/ip to process the incoming http traffic |
| `annotations`     | [Annotations][25]     | N        | `{}`             | Arbitrary non-identifying metadata |
| `tls`             | [IngressTLS][15]      | N        | `{}`             | TLS details for securing traffic to the cluster |

### IngressTLS

| Parameter         | Type                  | Required | Default          | Description |
| ----------------- | --------------------- | -------- | ---------------- | ----------- |
| `hosts`           | List                  | N        | `[]`             | List of host names that match the TLS certificate |
| `secretName`      | String                | N        | `""`             | Name of the kubernetes secret that contains the TLS certificate. The secret needs to be within the same namespace as the eamli operator |

### License

| Parameter         | Type                  | Required | Default          | Description |
| ----------------- | --------------------- | -------- | ---------------- | ----------- |
| `accept`          | Boolean               | Y        | `false`          | Flag, to confirm you accept the eamli [EULA](https://eamli.com/eula) |


[1]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#eamli> "Eamli"
[2]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#eamliapiserver> "EamliAPIServer"
[3]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#eamliapiserverenvironment> "EamliAPIServerEnvironment"
[4]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#eamliapiserverseeder> "EamliAPIServerSeeder"
[5]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#eamliproductserver> "EamliProductServer"
[6]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#eamliproductserverenvironment> "EamliProductServerEnvironment"
[7]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#eamlisourcedata> "EamliSourceData"
[8]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#eamlisourcedataenvironment> "EamliSourceDataEnvironment"
[9]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#eamliwebapp> "EamliWebApp"
[11]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#gunicorn> "Gunicorn"
[12]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#horizontalpodautoscaler> "HorizontalPodAutoscaler"
[13]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#image> "Image"
[14]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#ingress> "Ingress"
[15]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#ingresstls> "IngressTLS"
[17]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#license> "License"
[18]: <https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector> "NodeSelector"
[19]: <https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity> "Affinity"
[20]: <https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/> "Tolerations"
[21]: <https://pkg.go.dev/k8s.io/api/autoscaling/v1#HorizontalPodAutoscalerSpec> "HorizontalPodAutoscalerSpec"
[22]: <https://pkg.go.dev/k8s.io/api@v0.23.4/core/v1#NodeSelectorTerm> "NodeSelectorTerm"
[23]: <https://pkg.go.dev/k8s.io/api@v0.23.4/core/v1#ResourceRequirements> "ResourceRequirements"
[24]: <https://pkg.go.dev/k8s.io/api@v0.23.4/core/v1#Toleration> "Toleration"
[25]: <https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/> "Annotations"

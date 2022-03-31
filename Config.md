# Eamli Service Configurations

## API Reference

### Eamli

| Parameter         | Type                  | Required | Default          | Description |
| ----------------- | --------------------- | -------- | ---------------- | ----------- |
| `license`         | [license][17]         | Y        | `{}`             | Provides a section for accepting the eamli licensing agreement |
| `ingress`         | [ingress][14]         | Y        | `{}`             | Defines how eamli is exposed to public traffic |
| `keycloak`        | [keycloak][16]        | Y        | `{}`             | Defines how the eamli services will interact with the [Keycloak](https://www.keycloak.org/) instance |
| `postgresql`      | [postgresql][19]      | Y        | `{}`             | Defines how the eamli services will interact with the [PostgreSQL](https://www.postgresql.org/) instance |
| `elasticsearch`   | [elasticsearch][10]   | Y        | `{}`             | Defines how the eamli services will interact with the [Elasticsearch](https://www.elastic.co/) instance |
| `apiserver`       | [apiserver][2]        | N        | `{}`             | API definition, for controlling the Eamli API Server within the cluster |
| `productserver`   | [productserver][5]    | N        | `{}`             | API definition, for controlling the Eamli Product Server within the cluster |
| `sourcedata`      | [sourcedata][7]       | N        | `{}`             | API definition, for controlling the Eamli Source Data within the cluster |
| `webapp`          | [webapp][9]           | N        | `{}`             | API definition, for controlling the Eamli Web App within the cluster |

### EamliAPIServer

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `replicaCount`            | Integer                               | N        | `1`              | Number of pods to create for this deployment |
| `image`                   | [image][13]                           | N        | `{}`             | Defines the container image to be used for this service |
| `podAnnotations`          | [pod-annotations][25]                 | N        | `{}`             | Annotations to attach metadata to the pods. See https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/ |
| `horizontalpodautoscaler` | [horizontal-pod-autoscaler][12]       | N        | `{}`             | The HorizontalPodAutoscaler defines how pods should scale for load. |
| `resources`               | [resource-requirements][23]           | N        | `{}`             | Specify how much of each resource a container needs. See https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/ |
| `nodeSelector`            | [node-selector][18]                   | N        | `{}`             | The simplest recommended form of node selection constraint. |
| `tolerations`             | [tolerations][20]                     | N        | `{}`             | Define how pods should be scheduled for this service. |
| `environment`             | [eamli-api-server-environment][3]     | N        | `{}`             | Defines the environment variables that are exposed to the service |

### EamliAPIServerEnvironment

| Parameter         | Type                      | Required | Default          | Description |
| ----------------- | ------------------------- | -------- | ---------------- | ----------- |
| `gunicorn`        | [gunicorn][11]            | N        | `{}`             | Collection of Gunicorn settings that are exposed for tweaking service runtimes |
| `seeder`          | [api-server-seeder][4]    | N        | `1`              | Configuration of how the API Server data is seeded |

### EamliAPIServerSeeder

| Parameter         | Type                  | Required | Default          | Description |
| ----------------- | --------------------- | -------- | ---------------- | ----------- |
| `demo`            | Boolean               | N        | `false`          | If set to true, demo data will be loaded onto the platform. |

### EamliProductServer

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `replicaCount`            | Integer                               | N        | `1`              | Number of pods to create for this deployment |
| `image`                   | [image][13]                           | N        | `{}`             | Defines the container image to be used for this service |
| `podAnnotations`          | [pod-annotations][25]                 | N        | `{}`             | Annotations to attach metadata to the pods. See https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/ |
| `horizontalpodautoscaler` | [horizontal-pod-autoscaler][12]       | N        | `{}`             | The HorizontalPodAutoscaler defines how pods should scale for load. |
| `resources`               | [resource-requirements][23]           | N        | `{}`             | Specify how much of each resource a container needs. See https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/ |
| `nodeSelector`            | [node-selector][18]                   | N        | `{}`             | The simplest recommended form of node selection constraint. |
| `tolerations`             | [tolerations][20]                     | N        | `{}`             | Define how pods should be scheduled for this service. |
| `environment`             | [eamli-product-server-environment][6] | N        | `{}`             | Defines the environment variables that are exposed to the service |

### EamliProductServerEnvironment

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `gunicorn`                | [gunicorn][11]                        | N        | `{}`             | Collection of Gunicorn settings that are exposed for tweaking service runtimes |
| `corsAllowedOrigin`       | String                                | N        | `*`              | The Access-Control-Allow-Origin response header indicates whether the response can be shared with requesting code from the given origin |

### EamliSourceData

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `replicaCount`            | Integer                               | N        | `1`              | Number of pods to create for this deployment |
| `image`                   | [image][13]                           | N        | `{}`             | Defines the container image to be used for this service |
| `podAnnotations`          | [pod-annotations][25]                 | N        | `{}`             | Annotations to attach metadata to the pods. See https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/ |
| `horizontalpodautoscaler` | [horizontal-pod-autoscaler][12]       | N        | `{}`             | The HorizontalPodAutoscaler defines how pods should scale for load. |
| `resources`               | [resource-requirements][23]           | N        | `{}`             | Specify how much of each resource a container needs. See https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/ |
| `nodeSelector`            | [node-selector][18]                   | N        | `{}`             | The simplest recommended form of node selection constraint. |
| `tolerations`             | [tolerations][20]                     | N        | `{}`             | Define how pods should be scheduled for this service. |
| `environment`             | [eamli-source-data-environment][8]    | N        | `{}`             | Defines the environment variables that are exposed to the service |

### EamliSourceDataEnvironment

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `gunicorn`                | [gunicorn][11]                        | N        | `{}`             | Collection of Gunicorn settings that are exposed for tweaking service runtimes |
| `corsAllowedOrigin`       | String                                | N        | `*`              | The Access-Control-Allow-Origin response header indicates whether the response can be shared with requesting code from the given origin |

### EamliWebApp

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `replicaCount`            | Integer                               | N        | `1`              | Number of pods to create for this deployment |
| `image`                   | [image][13]                           | N        | `{}`             | Defines the container image to be used for this service |
| `podAnnotations`          | [pod-annotations][25]                 | N        | `{}`             | Annotations to attach metadata to the pods. See https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/ |
| `horizontalpodautoscaler` | [horizontal-pod-autoscaler][12]       | N        | `{}`             | The HorizontalPodAutoscaler defines how pods should scale for load. |
| `resources`               | [resource-requirements][23]           | N        | `{}`             | Specify how much of each resource a container needs. See https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/ |
| `nodeSelector`            | [node-selector][18]                   | N        | `{}`             | The simplest recommended form of node selection constraint. |
| `tolerations`             | [tolerations][20]                     | N        | `{}`             | Define how pods should be scheduled for this service. |

### Elasticsearch

| Parameter         | Type                  | Required | Default        | Description |
| ----------------- | --------------------- | -------- | -------------- | ----------- |
| `scheme`          | String                | N        | `"http"`       | The protocol used to communicate with the Elasticsearch instance |
| `host`            | String                | Y        | `""`           | The addressable endpoint where the Elasticsearch instance is available. Can be internal or external to the cluster |
| `port`            | Integer               | N        | `9200`         | Port to be used when communicating with Elasticsearch |
| `customCA`        | Boolean               | N        | `false`        | Where or not to use custom certificates to communicate with Elasticsearch. If set to true, expects a secret named `elasticseach-https-secret` within the same namespace as the eamli operator, containing the custom PEM file (See the [Prerequisites section](https://whitespaceventures.github.io/eamli-operator-docs/#Prerequisites)) |

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
| `spec`        | [horizontal-pod-autoscaler-spec][21]  | N        | `""`             | See https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/ |

### Image

| Parameter                 | Type                      | Required | Default          | Description |
| ------------------------- | ------------------------- | -------- | ---------------- | ----------- |
| `repository`              | String                    | N        | `""`             | Container image source |
| `tag`                     | String                    | N        | `""`             | Tag of the container image |

### Ingress

| Parameter         | Type                  | Required | Default          | Description |
| ----------------- | --------------------- | -------- | ---------------- | ----------- |
| `host`            | String                | Y        | `""`             | Ingress/Route hostname/ip to process the incoming http traffic |
| `annotations`     | [annotations][25]     | N        | `{}`             | Arbitrary non-identifying metadata |
| `tls`             | [ingress-tls][15]     | N        | `{}`             | TLS details for securing traffic to the cluster |

### IngressTLS

| Parameter         | Type                  | Required | Default          | Description |
| ----------------- | --------------------- | -------- | ---------------- | ----------- |
| `hosts`           | List                  | N        | `[]`             | List of host names that match the TLS certificate |
| `secretName`      | String                | N        | `""`             | Name of the kubernetes secret that contains the TLS certificate. The secret needs to be within the same namespace as the eamli operator |

### Keycloak

| Parameter                 | Type                  | Required | Default    | Description |
| ------------------------- | --------------------- | -------- | ---------- | ----------- |
| `host`                    | String                | Y        | `""`       | Public endpoint that the keycloak instance is available from |
| `user`                    | String                | Y        | `""`       | Admin user for the keycloak instance |
| `masterRealm`             | String                | Y        | `""`       | Primary (Default) realm to create the initial connection with |
| `adminSecretName`         | String                | Y        | `""`       | Name of the secret containing Keycloak Creditials |
| `adminSecretPasswordKey`  | String                | Y        | `""`       | Key within the secret that contains the keycloak admin password |

### License

| Parameter         | Type                  | Required | Default          | Description |
| ----------------- | --------------------- | -------- | ---------------- | ----------- |
| `accept`          | Boolean               | Y        | `false`          | Flag, to confirm you accept the eamli [EULA](https://eamli.com/eula) |

### NodeSelector

| Parameter     | Type                              | Required | Default          | Description |
| ------------- | --------------------------------- | -------- | ---------------- | ----------- |
| `enabled`     | boolean                           | N        | `false`          | Flag to enable node selector for the service pods |
| `spec`        | [node-selector-spec][22]          | N        | `""`             | See https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector |

### Postgresql

| Parameter             | Type                  | Required | Default    | Description |
| --------------------- | --------------------- | -------- | ---------- | ----------- |
| `internalServiceAddr` | String                | N        | `""`       | Address of a PostgreSQL instance that is within the cluster. For example postgres.svc.{NS}.cluster.internal |
| `externalAddr`        | String                | N        | `""`       | Address of a PostgreSQL instance that is external to the cluster. For example an AWS RDS instance |
| `externalIP`          | String                | N        | `""`       | IP of a PostgreSQL instance that is external to the cluster. For example an AWS RDS instance ||
| `port`                | Integer               | Y        | `5432`     | Port to use for sending requests to the PostgreSQL instance |
| `adminUsername`       | String                | Y        | `""`       | PostgreSQL admin username, to generate users and databases with |
| `adminDB`             | String                | Y        | `""`       | Default PostgreSQL database |

### Tolerations

| Parameter     | Type                              | Required | Default          | Description |
| ------------- | --------------------------------- | -------- | ---------------- | ----------- |
| `enabled`     | boolean                           | N        | `false`          | Flag to enable tolerations for the service pods |
| `spec`        | [toleration-spec][24]             | N        | `{}`             | See https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/ |


[1]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#Eamli> "Eamli"
[2]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#EamliAPIServer> "EamliAPIServer"
[3]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#EamliAPIServerEnvironment> "EamliAPIServerEnvironment"
[4]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#EamliAPIServerSeeder> "EamliAPIServerSeeder"
[5]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#EamliProductServer> "EamliProductServer"
[6]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#EamliProductServerEnvironment> "EamliProductServerEnvironment"
[7]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#EamliSourceData> "EamliSourceData"
[8]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#EamliSourceDataEnvironment> "EamliSourceDataEnvironment"
[9]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#EamliWebApp> "EamliWebApp"
[10]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#Elasticsearch> "Elasticsearch"
[11]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#Gunicorn> "Gunicorn"
[12]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#HorizontalPodAutoscaler> "HorizontalPodAutoscaler"
[13]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#Image> "Image"
[14]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#Ingress> "Ingress"
[15]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#IngressTLS> "IngressTLS"
[16]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#Keycloak> "Keycloak"
[17]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#License> "License"
[18]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#NodeSelector> "NodeSelector"
[19]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#Postgresql> "Postgresql"
[20]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#Tolerations> "Tolerations"
[21]: <https://pkg.go.dev/k8s.io/api/autoscaling/v1#HorizontalPodAutoscalerSpec> "HorizontalPodAutoscalerSpec"
[22]: <https://pkg.go.dev/k8s.io/api@v0.23.4/core/v1#NodeSelectorTerm> "NodeSelectorTerm"
[23]: <https://pkg.go.dev/k8s.io/api@v0.23.4/core/v1#ResourceRequirements> "ResourceRequirements"
[24]: <https://pkg.go.dev/k8s.io/api@v0.23.4/core/v1#Toleration> "Toleration"
[25]: <https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/> "Annotations"

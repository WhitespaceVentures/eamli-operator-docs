# Eamli Service Configurations

## API Reference

### Eamli

| Parameter         | Type                      | Required | Default          | Description |
| ----------------- | ------------------------- | -------- | ---------------- | ----------- |
| `license`         | [License][17]             | Y        | `{}`             | Provides a section for accepting the eamli licensing agreement |
| `eamlicore`       | [EamliCore][2]            | Y        | `{}`             | API definition, ingress and third-party resources |
| `eamliui`         | [EamliUI][3]              | N        | `{}`             | API definition, for the Eamli UI service |
| `keycloakrealm`   | [KeycloakRealm][4]        | N        | `{}`             | API definition, for the Keycloak Realm service |
| `productserver`   | [ProductServer][5]        | N        | `{}`             | API definition, for the Product Server service |
| `sourcedata`      | [SourceData][6]           | N        | `{}`             | API definition, for the Source Data service |
| `userservice`     | [UserService][7]          | N        | `{}`             | API definition, for the User Service service |

### EamliCore

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `Ingress`                 | [Ingress][13]                         | Y        |                  | Defines the container image to be used for this service |
| `Database`                | [ThirdPartyService][15]               | Y        |                  | Annotations to attach metadata to the service. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `Keycloak`                | [ThirdPartyService][15]               | Y        |                  | Annotations to attach metadata to the pods. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |

### EamliUI

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `image`                   | [Image][13]                           | N        | `{}`             | Defines the container image to be used for this service |
| `serviceAnnotations`      | [Annotations][25]                     | N        | `{}`             | Annotations to attach metadata to the service. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `podAnnotations`          | [Annotations][25]                     | N        | `{}`             | Annotations to attach metadata to the pods. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `resources`               | [ResourceRequirements][23]            | N        | `{}`             | Specify how much of each resource a container needs. See [https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) |

### KeycloakRealm

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `image`                   | [Image][13]                           | N        | `{}`             | Defines the container image to be used for this service |
| `serviceAnnotations`      | [Annotations][25]                     | N        | `{}`             | Annotations to attach metadata to the service. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `podAnnotations`          | [Annotations][25]                     | N        | `{}`             | Annotations to attach metadata to the pods. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `resources`               | [ResourceRequirements][23]            | N        | `{}`             | Specify how much of each resource a container needs. See [https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) |

### ProductServer

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `image`                   | [Image][13]                           | N        | `{}`             | Defines the container image to be used for this service |
| `serviceAnnotations`      | [Annotations][25]                     | N        | `{}`             | Annotations to attach metadata to the service. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `podAnnotations`          | [Annotations][25]                     | N        | `{}`             | Annotations to attach metadata to the pods. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `resources`               | [ResourceRequirements][23]            | N        | `{}`             | Specify how much of each resource a container needs. See [https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) |

### SourceData

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `image`                   | [Image][13]                           | N        | `{}`             | Defines the container image to be used for this service |
| `serviceAnnotations`      | [Annotations][25]                     | N        | `{}`             | Annotations to attach metadata to the service. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `podAnnotations`          | [Annotations][25]                     | N        | `{}`             | Annotations to attach metadata to the pods. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `resources`               | [ResourceRequirements][23]            | N        | `{}`             | Specify how much of each resource a container needs. See [https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) |

### UserService

| Parameter                 | Type                                  | Required | Default          | Description |
| ------------------------- | ------------------------------------- | -------- | ---------------- | ----------- |
| `image`                   | [Image][13]                           | N        | `{}`             | Defines the container image to be used for this service |
| `serviceAnnotations`      | [Annotations][25]                     | N        | `{}`             | Annotations to attach metadata to the service. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `podAnnotations`          | [Annotations][25]                     | N        | `{}`             | Annotations to attach metadata to the pods. See [https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| `resources`               | [ResourceRequirements][23]            | N        | `{}`             | Specify how much of each resource a container needs. See [https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) |

### Image

| Parameter                 | Type                      | Required | Default          | Description |
| ------------------------- | ------------------------- | -------- | ---------------- | ----------- |
| `repository`              | String                    | N        | `""`             | Container image source |
| `tag`                     | String                    | N        | `""`             | Tag of the container image |

### Ingress

| Parameter         | Type                  | Required | Default          | Description |
| ----------------- | --------------------- | -------- | ---------------- | ----------- |
| `enabled`         | boolean               | N        | false            | If enabled, operator will create a simple ingress definition |
| `className`       | string                | N        |                  | Class name used for the ingress |
| `host`            | string                | Y        |                  | Domain name of the eamli instance |

### Third-Party Service
Either one of `address` or `ip` and `port` is required

| Parameter         | Type                  | Required | Default          | Description |
| ----------------- | --------------------- | -------- | ---------------- | ----------- |
| `address`         | string                | N        |                  | Domain for the third-party service, addressable from within the cluster namespace |
| `ip`              | string                | N        |                  | IP address for the third-party service, addressable from within the cluster namespace |
| `port`            | string                | N        |                  | Connection port for the third-party service, addressable from within the cluster namespace |

### License

| Parameter         | Type                  | Required | Default          | Description |
| ----------------- | --------------------- | -------- | ---------------- | ----------- |
| `accept`          | Boolean               | Y        | `false`          | Flag, to confirm you accept the eamli [EULA](https://eamli.com/eula) |


[1]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#eamli> "Eamli"
[2]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#eamlcCore> "EamliCore"
[3]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#eamliui> "EamliUI"
[4]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#keycloakrealm> "KeycloakRealm"
[5]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#productserver> "ProductServer"
[6]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#sourcedata> "SourceData"
[7]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#userservice> "UserService"
[13]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#image> "Image"
[14]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#ingress> "Ingress"
[15]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#third-party-service> "ThirdPartyService"
[17]: <https://whitespaceventures.github.io/eamli-operator-docs/Config.html#license> "License"
[23]: <https://pkg.go.dev/k8s.io/api@v0.23.4/core/v1#ResourceRequirements> "ResourceRequirements"
[25]: <https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/> "Annotations"

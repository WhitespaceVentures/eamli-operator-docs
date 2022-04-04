# Elasticsearch quick start
Elasticsearch is used to store models definitions created by eamli.

## Elasticsearch operator
Elasticsearch provides an operator that you can install from the operator marketplace via the Openshift dashboard (See [https://operatorhub.io/operator/elastic-cloud-eck](https://operatorhub.io/operator/elastic-cloud-eck)).
For the purpose of the quickstart guide, we will spin up a minimal, single node, Elasticsearch instance within the same kubernetes cluster as the eamli operator (In production environments, you would want at minimum of 2 nodes, and potentionally install the operator and Elasticsearch Cluster, within its own namespace).

Start by goin to your Openshift "Administrator" dashboard, and navigate to Operators -> OperatorHub.

![Admin Console](/imgs/elasticsearch/overview.png)

Using the search box type in "Elasticsearch", select "Elasticsearch (ECK) Operator", and click "Install".

![Operator Hub](/imgs/elasticsearch/operatorhub.png)

Leave all the options as the defaults. This will install the Elasticsearch operator in the "openshift-operators" namespace, and be made available to all namespaces.

Now in the Elasticsearch (ECK) Operator dashboard, select the "Elasticsearch Cluster" tab, and click "Create Elasticsearch". Select "YAML view" and update the YAML with the following:

![Operator Dashboard](/imgs/elasticsearch/dashboard.png)

    apiVersion: elasticsearch.k8s.elastic.co/v1
    kind: Elasticsearch
    metadata:
      name: elasticsearch
      namespace: eamli
    spec:
      version: 8.1.0
      nodeSets:
      - name: eamli
        count: 1
        config:
          node.roles:
            - master
            - data
          node.store.allow_mmap: false
        podTemplate:
          spec:
            containers:
              - name: elasticsearch
                resources:
                  requests:
                    memory: 4Gi
                    cpu: 1
                  limits:
                    memory: 4Gi
                    cpu: 1

After a couple of minutes, you should see the pod and service come up

    $ oc -n eamli get pods
    ---
    NAME                      READY   STATUS    RESTARTS   AGE
    elasticsearch-es-eamli-0  1/1     Running   0          41h

    $ oc -n eamli get service
    ---
    NAME                             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)             AGE
    elasticsearch-es-eamli           ClusterIP   None             <none>        9200/TCP            41h
    elasticsearch-es-http            ClusterIP   172.21.70.36     <none>        9200/TCP            41h
    elasticsearch-es-internal-http   ClusterIP   172.21.222.130   <none>        9200/TCP            41h
    elasticsearch-es-transport       ClusterIP   None             <none>        9300/TCP            41h

    $ oc -n eamli get secrets
    ---
    NAME                                       TYPE                                  DATA   AGE
    elasticsearch-es-eamli-es-config           Opaque                                1      41h
    elasticsearch-es-eamli-es-transport-certs  Opaque                                3      41h
    elasticsearch-es-elastic-user              Opaque                                1      41h
    elasticsearch-es-http-ca-internal          Opaque                                2      41h
    elasticsearch-es-http-certs-internal       Opaque                                3      41h
    elasticsearch-es-http-certs-public         Opaque                                2      41h
    elasticsearch-es-internal-users            Opaque                                3      41h
    elasticsearch-es-remote-ca                 Opaque                                1      41h
    elasticsearch-es-transport-ca-internal     Opaque                                2      41h
    elasticsearch-es-transport-certs-public    Opaque                                1      41h
    elasticsearch-es-xpack-file-realm          Opaque                                3      41h

## Configuration for eamli

Now that we have an Elasticsearch instance available, we need to expose configuration for the eamli service

### Elasticsearch user credentials

The first thing we will need is the user credentials that will be used to access Elasticsearch. These can be found in the `elasticsearch-es-elastic-user` secret.
By default, the username will be `elastic`. Using these credentials, we can then create the eamli secret for connecting to Elasticsearch.

    $ PWD=$(oc -n eamli get secret elasticsearch-es-elastic-user -o go-template='{{index .data "elastic" | base64decode }}')
    $ oc kubectl -n eamli create secret generic eamli-elasticsearch-auth \
        --from-literal=ELS_SCHEME=https \
        --from-literal=ELS_HOST=elasticsearch-es-http \
        --from-literal=ELS_PORT=9200 \
        --from-literal=ELS_USER=elastic \
        --from-literal=ELS_PWD=$PWD \
        --from-literal=ELS_CUSTOM_AC=true

### Elasticsearch TLS certificates

The Elasticsearch instance that was created by the operator will use self signed certificates for handling TLS communication.
You can find certificate in the `elasticsearch-es-http-certs-public` secret, and then use this certificate to generate to create the PEM file for eamli to use

    $ CERT=$(oc -n eamli get secret elasticsearch-es-http-certs-public -o go-template='{{index .data "tls.crt" | base64decode }}')
    $ oc -n eamli create secret generic eamli-elasticsearch-tls \
        --from-literal=ca.pem="${CERT}"

### Elasticsearch host
You can access the Elasticsearch instance within the cluster at `elasticsearch-es-http.eamli.svc`

# Keycloak quick start
Keycloak is used to provide centralised IAM for eamli services.

## Keycloak operator
Keycloak provides an operator that you can install from the operator marketplace via the Openshift dashboard (See (https://www.keycloak.org/getting-started/getting-started-operator-kubernetes)[https://www.keycloak.org/getting-started/getting-started-operator-kubernetes])

Start by going to your Openshift "Administrator" dashboard, and navigate to Operators -> OperatorHub.

![Admin Console](/imgs/keycloak/overview.png)

Using the search box type in "keycloak", select "Keycloak Operator", and click "Install".

![Operator Hub](/imgs/keycloak/operatorhub.png)

Select "eamli" for the "Installed Namespace", and leave everything else as default, and click "Install".

Now in the Keycloak Operator dashboard, select the "Keycloak" tab, and click "Create Keycloak". Select "YAML view" and update the YAML with the following:

![Operator Dashboard](/imgs/keycloak/dashboard.png)

    apiVersion: keycloak.org/v1alpha1
    kind: Keycloak
    metadata:
      name: keycloak
      namespace: eamli
    spec:
      instances: 1
      keycloakDeploymentSpec:
        experimental:
          args:
            - "-Dkeycloak.profile.feature.token_exchange=enabled"
            - "-Dkeycloak.profile.feature.admin_fine_grained_authz=enabled"
            - "-Dkeycloak.migration.strategy=OVERWRITE_EXISTING"

After a couple of minutes, you should see the pod and service come up

    $ oc -n eamli get pods
    ---
    NAME                                   READY   STATUS      RESTARTS   AGE
    keycloak-0                             1/1     Running     2          5m22s
    keycloak-operator-786bcb4988-grj5g     1/1     Running     0          10m
    keycloak-postgresql-6db4c69d9f-46kbb   1/1     Running     0          5m22s

    $ oc -n eamli get service
    ---
    NAME                             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)             AGE
    keycloak                         ClusterIP   172.21.93.121    <none>        8443/TCP            5m43s
    keycloak-discovery               ClusterIP   None             <none>        8080/TCP            5m43s
    keycloak-monitoring              ClusterIP   172.21.194.237   <none>        9990/TCP            5m43s
    keycloak-operator-metrics        ClusterIP   172.21.18.202    <none>        8383/TCP,8686/TCP   8m59s
    keycloak-postgresql              ClusterIP   172.21.226.234   <none>        5432/TCP            5m43s

    $ oc -n eamli get secrets
    ---
    NAME                                       TYPE                                  DATA   AGE
    credential-keycloak                        Opaque                                2      6m7s
    keycloak-db-secret                         Opaque                                6      6m7s
    keycloak-operator-dockercfg-5z2jb          kubernetes.io/dockercfg               1      10m
    keycloak-operator-token-2bnmx              kubernetes.io/service-account-token   4      10m
    keycloak-operator-token-vwwbk              kubernetes.io/service-account-token   4      10m

## Configuration for eamli

Now that we have an Keycloak instance available, we need to expose configuration for the eamli service

### Keycloak user credentials

Eamli requires the user credentials that will be used to access Keycloak. These can be found in the `credential-eamli-keycloak` secret.
Using these credentials, we can then create the eamli secret for connecting to Keycloak. (By default Keycloak creates the `master` realm)

    $ USER=$(oc -n eamli get secret credential-keycloak -o go-template='{{index .data "ADMIN_USERNAME" | base64decode }}')
    $ PWD=$(oc -n eamli get secret credential-keycloak -o go-template='{{index .data "ADMIN_PASSWORD" | base64decode }}')
    $ oc kubectl -n eamli create secret generic eamli-keycloak-auth \
        --from-literal=KEYCLOAK_REALM=master \
        --from-literal=KEYCLOAK_URL=http://keycloak-discovery.eamli.svc \
        --from-literal=KEYCLOAK_USER=$USER \
        --from-literal=KEYCLOAK_PWD=$PWD

### Keycloak route

The Keycloak will be used to allow users to authenticate with eamli, so we need to create a publicily accessable endpoint that they can request.

Use the following snippet to create a new file called, `keycloak-route.yaml`, replacing the values in brackets (`{}`) with your unique values. (eg `spec.host: example.com`)

    apiVersion: route.openshift.io/v1
    kind: Route
    metadata:
      annotations:
        haproxy.router.openshift.io/balance: source
      name: keycloak
      namespace: eamli
    spec:
      host: {YOUR_DOMAIN}
      path: /auth
      port:
        targetPort: keycloak
      to:
        kind: Service
        name: keycloak
        weight: 100
      wildcardPolicy: None
      tls:
        termination: reencrypt
        key: |-
          {YOUR_DOMAIN_TLS_KEY}
        certificate: |-
          {YOUR_DOMAIN_TLS_CERT}
        caCertificate: |-
          {YOUR_DOMAIN_TLS_CA_CERT}

Save the file, then apply the route to the cluster

    $ oc -n eamli apply -f keycloak-route.yaml

### Keycloak host
You can access the Keycloak instance publicly at `https://{YOUR DOMAIN}/auth`

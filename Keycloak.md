# Keycloak Quick Start

[Keycloak](https://www.keycloak.org/) can be installed from its own community operator.

From the OpenShift admin console, navigate → Operators → OperatorHub, in the menu on the left side, then, focus on the search input box and type "keycloak". Select "Keycloak Operator provided by Red Hat", and click install.

You should install keycloak into the same namespace as you intend to install the Eamli opeartor.

Create the keycloak instance:

    $ cat <<EOF | oc -n eamli apply -f -
    apiVersion: keycloak.org/v1alpha1
    kind: Keycloak
    metadata:
      name: eamli-keycloak
    spec:
      instances: 1
      keycloakDeploymentSpec:
        experimental:
          args:
            - "-Dkeycloak.profile.feature.token_exchange=enabled"
            - "-Dkeycloak.profile.feature.admin_fine_grained_authz=enabled"
            - "-Dkeycloak.migration.strategy=OVERWRITE_EXISTING"
    EOF

And create the route to access the keycloak instance from a public domain. This should be the same domain, as you intend to host the Eamli service.
For example if you want Eamli to be served at `eamli.mysite.com`, you should set the host to the same value.

    $ cat <<EOF | oc -n eamli apply -f -
    apiVersion: route.openshift.io/v1
    kind: Route
    metadata:
      annotations:
        haproxy.router.openshift.io/balance: source
      name: eamli-keycloak
      namespace: eamli
    spec:
      host: [YOUR DOMAIN]
      path: /auth
      port:
        targetPort: keycloak
      tls:
        termination: reencrypt
      to:
        kind: Service
        name: keycloak
        weight: 100
      wildcardPolicy: None
    EOF

After a couple of minutes, you should see the pod and service come up

    $ oc -n eamli get pods
    ---
    NAME                                    READY   STATUS      RESTARTS
    keycloak-0                              1/1     Running     2
    keycloak-operator-6478f487f6-clwtw      1/1     Running     0
    keycloak-postgresql-78d4c4f778-hhr6x    1/1     Running     0

(You can expect the keycloak pod to be restarted, while waiting for the keycloak-postgresql pod is starting)

    $ oc -n eamli get service
    ---
    NAME                        TYPE        CLUSTER-IP      PORT(S)
    keycloak                    ClusterIP   172.21.23.16    8443/TCP
    keycloak-discovery          ClusterIP   None            8080/TCP
    keycloak-monitoring         ClusterIP   172.21.21.158   9990/TCP
    keycloak-operator-metrics   ClusterIP   172.21.254.94   8383/TCP,8686/TCP
    keycloak-postgresql         ClusterIP   172.21.11.67    5432/TCP

    $ oc get route -n eamli
    ---
    NAME            HOST/PORT     PATH    SERVICES   PORT       TERMINATION   WILDCARD
    eamli-keycloak  [YOUR DOMAIN] /auth   keycloak   keycloak   reencrypt     None

You should then be able to log into the admin console at: https://[YOUR_DOMAIN]/auth

To see the admin login details, you can run:

    $ oc -n eamli get secret credential-eamli-keycloak

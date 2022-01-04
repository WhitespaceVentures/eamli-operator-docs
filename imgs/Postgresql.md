# Postgresql Quick Start

While it is recommended that you configure your Postgresql in a highly available and secure fashion, to get you started quickly working with Eamli, you can use this guide for getting a basic Postgresql instance setup quickly.

We will be using the [bitnami](https://bitnami.com/) Postgresql [Helm chart](https://github.com/bitnami/charts/tree/master/bitnami/postgresql) to install an instance onto our cluster, living within the same namespace as our operator.

First, add the bitnami helm repo to our local registry

    $ helm repo add bitnami https://charts.bitnami.com/bitnami

Next, create a kubernetes secret, that will define the admin users password (change `MY_SUPER_SECRET_PWD` to a secure password value):

    $ oc -n eamli create secret generic postgresql-admin \
        --from-literal="postgresql-password=MY_SUPER_SECRET_PWD" \
        --from-literal="postgresql-postgres-password=MY_SUPER_SECRET_PWD"

To make sure the password was set correctly, run

    $ oc -n eamli get secret postgresql-admin -o yaml

You should see the secret yaml, with the password base64 encoded.

Finally, install the helm chart with:

    $ echo "
    global:
      postgresql:
        postgresqlUsername: postgres
        existingSecret: postgresql-admin
    containerSecurityContext:
      enabled: false
      runAsUser: null
    securityContext:
      enabled: false
      fsGroup: null
    " > psql_values.yaml

    $ helm -n eamli upgrade --install -f psql_values.yaml psql bitnami/postgresql

After a couple of minutes, you should see the pod and service come up

    $ oc -n eamli get pods
    ---
    NAME                    READY   STATUS      RESTARTS   AGE
    psql-postgresql-0       1/1     Running     0          3m25s

    $ oc -n eamli get service
    ---
    NAME                        TYPE        CLUSTER-IP      PORT(S)
    psql-postgresql             ClusterIP   172.21.55.252   5432/TCP
    psql-postgresql-headless    ClusterIP   None            5432/TCP

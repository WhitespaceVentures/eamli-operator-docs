# PostgreSQL quick start
PostgreSQL is used as the primary persistant storage for eamli.

## PostgreSQL operator
There is no official PostgreSQL operator, but thankful the guys over at [Crunchy Data](https://www.crunchydata.com/) have provided a great operator we can use, that is available directly from the Openshift OperatorHub (See [https://access.crunchydata.com/documentation/postgres-operator/v5/](https://access.crunchydata.com/documentation/postgres-operator/v5/)).

For the purpose of the quickstart guide, we will spin up a minimal, single node, PostgreSQL cluster within the same kubernetes cluster as the eamli operator (In production environments, you would want at minimum of 2 nodes, and potentionally install the operator and PostgreSQL cluster, within its own namespace).

Start by going to your Openshift "Administrator" dashboard, and navigate to Operators -> OperatorHub.

![Admin Console](/imgs/postgresql/overview.png)

Using the search box type in "crunchy", select "Crunchy Postgres for Kubernetes" (for the purpose of this quickstart we will use the "Community" edition), and click "Install".

![Operator Hub](/imgs/postgresql/operatorhub.png)

Leave all the options as the defaults. This will install the PostgreSQL operator in the "openshift-operators" namespace, and be made available to all namespaces.

Now in the Crunchy Postgres for Kubernetes dashboard, select the "PostgresClusters" tab, and click "Create PostgresCluster". Select "YAML view" and update the YAML with the following:

![Operator Dashboard](/imgs/postgresql/dashboard.png)

    apiVersion: postgres-operator.crunchydata.com/v1beta1
    kind: PostgresCluster
    metadata:
      name: postgres
      namespace: eamli
    spec:
      port: 5432
      backups:
        pgbackrest:
          restore:
            enabled: false
            repoName: "repo1"
          repos:
            - name: "repo1"
              volume:
                volumeClaimSpec:
                  accessModes:
                    - ReadWriteOnce
                  resources:
                    requests:
                      storage: 10Gi
      instances:
        - name: eamli
          dataVolumeClaimSpec:
            accessModes:
              - ReadWriteOnce
            resources:
              requests:
                storage: 10Gi
          replicas: 1
      postgresVersion: 13

After a couple of minutes, you should see the pod and service come up

    $ oc -n eamli get pods
    ---
    NAME                         READY   STATUS      RESTARTS   AGE
    postgres-backup-4sj7-9hn2m   0/1     Completed   0          42s
    postgres-eamli-6sf6-0        3/3     Running     0          3m
    postgres-repo-host-0         1/1     Running     0          3m

    $ oc -n eamli get service
    ---
    NAME                             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
    postgres-ha                      ClusterIP   172.21.47.79     <none>        5432/TCP   3m44s
    postgres-ha-config               ClusterIP   None             <none>        <none>     3m42s
    postgres-pods                    ClusterIP   None             <none>        <none>     3m44s
    postgres-primary                 ClusterIP   None             <none>        5432/TCP   3m44s
    postgres-replicas                ClusterIP   172.21.48.102    <none>        5432/TCP   3m43s

    $ oc -n eamli get secrets
    ---
    NAME                                       TYPE                                  DATA   AGE
    postgres-cluster-cert                      Opaque                                3      4m8s
    postgres-eamli-6sf6-certs                  Opaque                                4      4m7s
    postgres-instance-dockercfg-z4jbr          kubernetes.io/dockercfg               1      4m8s
    postgres-instance-token-k2kj8              kubernetes.io/service-account-token   4      4m8s
    postgres-instance-token-xsfqz              kubernetes.io/service-account-token   4      4m8s
    postgres-pgbackrest-dockercfg-sh9bn        kubernetes.io/dockercfg               1      4m5s
    postgres-pgbackrest-token-4g2zr            kubernetes.io/service-account-token   4      4m5s
    postgres-pgbackrest-token-m8hm5            kubernetes.io/service-account-token   4      4m5s
    postgres-pguser-postgres                   Opaque                                8      4m6s
    postgres-replication-cert                  Opaque                                3      4m9s
    postgres-ssh                               Opaque                                3      4m5s

## Configuration for eamli

Now that we have an PostgreSQL instance available, we need to expose configuration for the eamli service

### PostgreSQL user credentials

Eamli requires the user credentials that will be used to access PostgreSQL. These can be found in the `postgres-pguser-postgres` secret.
Using the password, create the eamli secret for connecting to PostgreSQL.

    $ HOST=$(oc -n eamli get secret postgres-pguser-postgres -o go-template='{{index .data "host" | base64decode }}')
    $ PWD=$(oc -n eamli get secret postgres-pguser-postgres -o go-template='{{index .data "password" | base64decode }}')
    $ oc kubectl -n eamli create secret generic eamli-database-auth \
        --from-literal=DB_INTERNAL_ADDRESS=$HOST \
        --from-literal=DB_PASSWORD=$PWD

#### eamli-database-auth config

| Parameter                     | Type    | Required | Default      | Description |
| ----------------------------- | ------- | -------- | ------------ | ----------- |
| `DB_INTERNAL_ADDRESS`         | String  | N        | `""`         | Domain of database instance within the same cluster as the operator |
| `DB_EXTERNAL_ADDRESS`         | String  | N        | `""`         | Domain of external database instance |
| `DB_EXTERNAL_IP`              | String  | N        | `""`         | IP address of external database instance |
| `DB_NAME`                     | String  | N        | `"postgres"` | Name of the admin database |
| `DB_PORT`                     | Integer | N        | `5432`       | Port used to connect to the database instance |
| `DB_USERNAME`                 | String  | N        | `"postgres"` | Admin user name |
| `DB_PASSWORD`                 | String  | Y        | `""`         | Admin user password |

### PostgreSQL host
You can access the PostgreSQL instance within the cluster at `postgres-primary.eamli.svc`

Alternatively if using an external database, you can access the instance from the cluster at `eamli-database.eamli.svc`

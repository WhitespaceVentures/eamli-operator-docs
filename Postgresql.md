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
      image: registry.developers.crunchydata.com/crunchydata/crunchy-postgres-gis:ubi8-14.7-3.3-0
      port: 5432
      users:
        - databases:
            - keycloak
          password:
            type: AlphaNumeric
          name: keycloak
        - databases:
            - productserver
          password:
            type: AlphaNumeric
          name: productserver
        - databases:
            - sourcedata
          password:
            type: AlphaNumeric
          name: sourcedata
        - databases:
            - userservice
          password:
            type: AlphaNumeric
          name: userservice
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
      postgresVersion: 14

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

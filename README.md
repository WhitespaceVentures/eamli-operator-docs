# eamli operator documentation

Welcome to the eamli operator documentation site.

eamli is a decision-intelligence service that eamli analyses millions of possibilities in ways humans can’t. Within seconds, eamli models the future so that you can see the impact of decisions before you make them.

## Introduction
The eamli operator provides a single interface for managing all the services that make up the eamli platform, and provides seamless upgrade process, to keep you always up to date.

## Prerequisites
* Red Hat OpenShift Container Platform 4.6 or newer installed on x86_64
* A user with cluster administrator role
* No storage is required to install the operator
* A PostgreSQL instance, reachable from within the cluster. For details on setting up a basic PostgreSQL instance see [here](https://whitespaceventures.github.io/eamli-operator-docs/Postgresql.html)
* A PostgreSQL secret, with the admin user details
```
$ oc -n eamli create secret generic postgresql-admin \
    --from-literal="postgresql-password=MY_SUPER_SECRET_PWD" \
    --from-literal="postgresql-postgres-password=MY_SUPER_SECRET_PWD"
```
* A Elasticsearch instance, reachable from within the cluster. For details on setuting up a basic Elasticsearch instance see [here](https://whitespaceventures.github.io/eamli-operator-docs/Elasticsearch.html)
* Keycloak Operator installed within the eamli target namespace, with a custom route defined. For details on setup see [here](https://whitespaceventures.github.io/eamli-operator-docs/Keycloak.html)
* An image pull secret, using your unique eamli details
```
kubectl create -n eamli secret docker-registry eamli-auth \
    --docker-server=registry.gitlab.com \
    --docker-username="jobbloggs" \
    --docker-password="MY_SUPER_SECRET_API_KEY" \
    --docker-email="jobbloggs@example.com"
```

## Resources Required
The operator requires 200m CPU and 256Mi memory.

For the minimum requirements for services, see the [service configuration](https://eamli.com/config) documentation

## Installing
Check out the [quick start guide](https://eamli.com/quickstart), for getting the eamli operator up and running

## Configuration
For full configuration options, see the [configuration guide](https://eamli.com/config)

## Limitations
Only `x86-64` platforms are supported by this operator.

## SecurityContextConstraints Requirements
The `restricted` security context constraint (SCC) is used for the operator.

You can also apply the [eamli SCC](https://whitespaceventures.github.io/eamli-operator-docs/SCC.html), to limit the permissions applied to eamli resources

## Quick start
To get started with the eamli operator check out the [Quickstart guide](/QuickStart.md) (Openshift)

## Terms
* [License agreement](https://eamli.com/eula)
* [Privacy policy](https://eamli.com/privacy-policy)

## Contact
If you need more help, please reach out to us at support@eamli.com

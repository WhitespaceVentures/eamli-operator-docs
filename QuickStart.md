# Openshift Quick Start

## Prerequisites

### Customer details

Before you begin, ensure you have recieved your unique customer details. You will need these to correctly set up your Eamli operator.

If you have not yet recieved your details, please reach out to support@eamli.com

### Public domain name

This can be your own custom domain, or one created by your provider. For example on IBM when you create an openshift cluster, you are given a public domain in the format of `https://cluster-id.region.containers.appdomain.cloud`.

### Namepsace

You will need to install a Kubernetes Secret, to allow the Eamli manager to pull its docker image.

From the Openshift console (as administrator)

* On the sidebar, select Administration -> Namespaces
* From the Namepsaces dashboard, click on the "Create Namepsace" in the top right corner
  * Name: `eamli`
* Once complete, click "Create".

### Pull secrets

You will need to install a Kubernetes Secret, to allow the Eamli manager to pull its docker image.

From the Openshift console (as administrator)

* On the sidebar, select Workloads -> Secrets
* Ensure the "Project", at the top of the secrets dashboard is set to `eamli`
* From the Secrets dashboard, click on the "Create" in the top right corner, and select "Image pull secret".
  * Secret name: `gitlab-auth`
  * Authentication type: `Image registry credentials`
  * Registry server address: `registry.gitlab.com`
  * Username: `[ unique customer username ]`
  * Password: `[ unique customer secret ]`
  * Eamli: `[ unique customer email ]`
* Once complete, click "Create".

![Create secret](/imgs/eamli-operator/CreateSecret.png)

### Postgresql

Postgresql is required to be setup prior to installing Eamli. If you already have an existing Postgres instance, you can use that. Otherwise, to setup a simple Postgesql instance, see the [Postgresql docs](/Postgresql.md), for getting setup using the community helm chart.

For this guide, we will assume the following:

* A Postgres service called `psql-postgresql-headless` is available in the same namespace as the service being deployed.
* It has an admin user called `postgres` with a default database named `postgres`
* A secret has been created named `postgresql-admin`, with the property `postgresql-password` and value of the postgres admin user's password.

If you’re unsure of how to configure any of the above, see the [Postgresql docs](/Postgresql.md).

### Elasticsearch

If you have an existing Elasticsearch installation, you can use that. Alternatively, we have provided steps on how to get a basic Elasticsearch up and running within your cluster with a community helm chart. See the [Elasticseasrch docs](/Elasticsearch.md) for details on this.

For this guide, we will assume the following:

* A Elasticsearch service called `elasticsearch-master-headless` is available in the same namespace as the service being deployed.

If you’re unsure of how to configure any of the above, see the [Elasticsearch docs](/Elasticsearch.md).

### Keycloak

Eamli requires Keycloak, to handle authentication. If you have an existing Keycloak instance installed, you can update it with the Eamli realms. Alternatively to install a new instance, check out the [Keycloak docs](/Keycloak.md), for getting setup.

For this guide, we will assume the following:

* A Keycloak service called `keycloak-discovery` is available in the same namespace as the service being deployed.
* A route exists, and is available at https://[YOUR_DOMAIN]/auth
* A secret named `keycloak-eamli-config`, with Eamli realm details set.

If you’re unsure of how to configure any of the above, see the [Keycloak docs](/Keycloak.md).

## Operator installation from Red Hat Marketplace

1. For information on registering your cluster and creating a namespace, see Red Hat
Marketplace Docs. This must be done prior to operator install.
2. On the main menu, click Workspace &gt; My Software &gt; product &gt; Install Operator.
3. On the Update Channel section, select an option.
4. On the Approval Strategy section, select either Automatic or Manual. The approval
strategy corresponds to how you want to process operator upgrades.
5. On the Target Cluster section:
o Click the checkbox next to the clusters where you want to install the Operator.
o For each cluster you selected, under Namespace Scope, on the Select Scope list,
select an option.
6. Click Install. It may take several minutes for installation to complete.
7. Once installation is complete, the status will change from installing to Up to date.
8. For further information, see the Red Hat Marketplace Operator documentation

## Verification of operator installation

1. Once status changes to Up to date, click the vertical ellipses and select Cluster Console.
2. Open the cluster where you installed the product
3. Go to Operators &gt; Installed Operators
4. Select the Namespace or Project you installed on
5. Verify status for product is Succeeded
6. Click the product name to open details

![Operator Hub](/imgs/eamli-operator/OperatorHub.png)

![Installing](/imgs/eamli-operator/Installing.png)

![Operator Dashboard](/imgs/eamli-operator/OperatorDashboard.png)

## Application installation

### Licence key

When you purchase Eamli, you will receive a welcome email from support@eamli.com, containing your unique customer details. These details are required to start the Eamli service installation.

### Eamli Custom Resources

While the Eamli operator comes bundled with a number of different operands, you will only ever need to interact with the `Stack` operand.

The `Stack` defines the entire Eamli platform, and is used to manage the other Eamli operands available.

### Creating the Eamli Stack

Click on the "Stack" tab, then click "Create Stack"

![Create Stack](/imgs/eamli-operator/CreateStack.png)

Use your unique customer details, to populate the "Client" section, and update all the other sections as required.

Alternatively, you can create the stack from your command line with:

    $ cat <<EOF | oc -n eamli apply -f -
    apiVersion: eamli.white.space/v1alpha1
    kind: Stack
    metadata:
      name: eamli-sample
    spec:
      isOpenshift: true
      client:
        username: "[ unique customer username ]"
        secret: "[ unique customer secret ]"
        email: "[ unique customer email ]"
      postgresql:
        host: "psql-postgresql-headless"
        port: "5432"
        adminUsername: "postgres"
        adminDB: "postgres"
      ingress:
        enabled: true
        host: "[YOUR DOMAIN]"
      apiserver:
        environment:
          seeder:
            demoEnabled: true
    EOF

Replacing the `spec.client` field values with your unique customer details, and updating the `spec.ingress.host` with your domain name

For more configuration options see the [config documentation](/Config.md).

Once applied, it will take a couple of minutes for all the Eamli services to be stood up.
If you have been following everything within this quick start guide, you can click on the Eamli Operator "All Instances" tab within the Openshift console, to see the status of all the services running.

![StackList](/imgs/eamli-operator/StackList.png)

Alternative, from your console, run `oc -n eamli get pods`, you should see a similiar output as below:

    NAME                                                READY   STATUS      RESTARTS   AGE
    apiserver-7875d9b6cd-4pn74                          1/1     Running     0          41m
    apiserver-seeder-ufqxy-p97ll                        0/1     Completed   0          41m
    coremodelserver-85f8cbfddd-lp95f                    1/1     Running     0          35m
    coremodelserver-seeder-gwaoi-z27rm                  0/1     Completed   0          35m
    eamli-operator-controller-manager-79c8b4f69f-csf4r  2/2     Running     0          46m
    elasticsearch-master-0                              1/1     Running     0          19h
    executor-bc45ff765-mnv8s                            1/1     Running     0          35m
    executor-seeder-tjlhg-8wqfn                         0/1     Completed   0          40m
    keycloak-0                                          1/1     Running     0          14h
    keycloak-operator-6478f487f6-clwtw                  1/1     Running     0          18h
    keycloak-postgresql-78d4c4f778-hhr6x                1/1     Running     0          14h
    productserver-648b578f44-4w4k6                      1/1     Running     0          39m
    productserver-seeder-qirov-cgjrl                    0/1     Completed   0          39m
    psql-postgresql-0                                   1/1     Running     0          20h
    sourcedata-6c6dd75654-4ssrn                         1/1     Running     0          41m
    sourcedata-seeder-iiibm-ntc7f                       0/1     Completed   0          41m
    webapp-6c84c9d6c7-r9m5p                             1/1     Running     0          41m

## Eamli dashboard

Once you have installed the Eamli stack, you should be able to head over to https://[YOUR_DOMAIN], and should be redirected to log in.

![Login Screen](/imgs/eamli-operator/LoginScreen.png)

You can log in, using the default creditials

    U: durden-admin
    P: password

You will then be prompted to change the password. It will need to contain, a lowercase, uppercase, numeric and special characters.

Once logged in, you will see the Eamli dashboard, where you can see some key metrics, generated from the demo data.

![Home Screen](/imgs/eamli-operator/Homepage.png)

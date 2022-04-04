# Openshift Quick Start

## Prerequisites

### Customer details

Before you begin, ensure you have recieved your unique customer details. You will need these to correctly set up your Eamli operator. If you have not yet recieved your details, please reach out to support@eamli.com

### Public domain name

This is your own public domain, that you will use to serve the eamli platform on (eg `example.com`)

#### TLS certificate

If you want to serve eamli using TLS (`https://`), you will need to create a new TLS secret.

Download your domain TLS certificate and key files, and save them as `tls.cert` and `tls.key`. Then create a new TLS secret with:

    $ oc -n eamli create secret tls eamli-public-tls --cert=tls.cert --key=tls.key

### Namepsace

Create a new namespace for eamli an its related services to live in.

From the Openshift console (as administrator)

* On the sidebar, select Administration -> Namespaces
* From the Namepsaces dashboard, click on the "Create Namepsace" in the top right corner
  * Name: `eamli`
* Once complete, click "Create".

Alternatively from the command line:

     $ oc create ns eamli

![Create secret](/imgs/eamli-operator/CreateSecret.png)

Alternatively from the command line:

    $ oc -n eamli create secret docker-registry eamli-auth \
        --docker-server=registry.gitlab.com \
        --docker-username="`[ unique customer username ]`" \
        --docker-password="`[ unique customer secret ]`" \
        --docker-email="`[ unique customer email ]`"

### Elasticsearch

To create a new elasticsearch install, we have provided a quick start guide for getting you setup (See the [Elasticseasrch Quickstart](/Elasticsearch.md)).

Alternatively, if you already have an Elasticsearch instance available, see [Elasticsearch for eamli](/Postgresql.md#configuration-for-eamli) for configuring eamli to communicate with your instance.

Once setup, you should have a secret created in the `eamli` namespace named `eamli-elasticsearch-auth` with the connection details defined. If Elasticsearch is using its own certificates for TLS, you should also have the `eamli-elasticsearch-tls` secret defined.

### Keycloak

To install a new Keycloak instance, check out the [Keycloak Quickstart](/Keycloak.md), for getting setup.

Alternatively, if you already have an existing Keycloak instance available, see [Keycloak for eamli](/Keycloak.md#configuration-for-eamli) for configuring eamli to communicate with your instance.

Once setup, you should have a secret created in the `eamli` namespace named `eamli-keycloak-auth` with the connection details defined.

### Postgresql

To install a new PostgresSQL instance, check out the [Keycloak Quickstart](/Postgresql.md), for getting setup.

Alternatively, if you already have an existing PostgresSQL instance available, see [PostgresSQL for eamli](/Postgresql.md#configuration-for-eamli) for configuring eamli to communicate with your instance.

Once setup, you should have a secret created in the `eamli` namespace named `eamli-postgresql-auth` with the connection details defined.

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

### Pull secret

You will need to install a Kubernetes Secret, to allow the eamli oeprator to pull down the private images used within the eamli platform.

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

### Creating an eamli instance

Click on the "Eamli" tab, then click "Create Eamli", and fill out the sections as required.

Alternatively, you can create the stack from your command line with:

    $ cat <<EOF | oc -n eamli apply -f -
    apiVersion: eamli.com/v1alpha1
    kind: Eamli
    metadata:
      name: eamli
    spec:
      license:
        accept: true
      ingress:
        host: `[ public domain name ]`
        tls:
          - hosts:
            - `[ public domain name ]`
            secretName: eamli-public-tls
    EOF

For full configuration options see the [configuration](/Config.md) document.

Once applied, it will take a couple of minutes for all the eamli services to be stood up.
If you have been following everything within this quick start guide, you can click on the Eamli Operator "All Instances" tab within the Openshift console, to see the status of all the services running.

![StackList](/imgs/eamli-operator/StackList.png)

Alternative, from your console, run `oc -n eamli get pods`, you should see a similiar output as below:

    NAME                                                              READY   STATUS      RESTARTS   AGE
    afc56cdfe349220543bd109da2e20ae59ed778a853cb80d953d6499ce64xmdt   0/1     Completed   0          130m
    eamli-apiserver-6d4d96d57b-vn4wl                                  1/1     Running     0          127m
    eamli-apiserver-seeder-ctrwm                                      0/1     Completed   0          128m
    eamli-operator-controller-manager-7c99f78b6f-cw5nb                2/2     Running     0          129m
    eamli-productserver-6b65ffb989-vj6dp                              1/1     Running     0          126m
    eamli-productserver-seeder-22r4t                                  0/1     Completed   0          126m
    eamli-sourcedata-7d7c8ddd59-mbrkr                                 1/1     Running     0          126m
    eamli-sourcedata-seeder-5zpkl                                     0/1     Completed   0          127m
    eamli-webapp-946bff9f8-lpjvr                                      1/1     Running     0          128m
    gitlab-com-whitedotspace-eamli-eamli-operator-bundle-0-12-2       1/1     Running     0          130m

## Eamli dashboard

Once you have installed the Eamli stack, you should be able to head over to https://[YOUR_DOMAIN], and should be redirected to log in.

![Login Screen](/imgs/eamli-operator/LoginScreen.png)

You can log in, using the default creditials

    U: eamli-admin
    P: password

You will then be prompted to change the password. It will need to contain, a lowercase, uppercase, numeric and special characters.

Once logged in, you will be greeted with the Eamli dashboard.

![Home Screen](/imgs/eamli-operator/Homepage.png)

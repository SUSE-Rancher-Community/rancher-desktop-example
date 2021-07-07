# Rancher Desktop

## Prerequisite

1. [kubectl](https://kubernetes.io/docs/tasks/tools/)
2. [Helm](https://helm.sh/docs/intro/install/)

## Getting Started

First we need to install [Rancher Desktop](https://github.com/rancher-sandbox/rancher-desktop/releases).

``` bash
NOTE: Rancher Desktop runs on a Mac or Windows machine.
```

Start the Rancher Desktop application and make sure it's running.

Windows check and make sure the Rancher Desktop icon is in the task bar.

Mac make sure the Rancher Desktop icon is in the menu bar at the top.

Selecting the icon in either Mac or Windows you can check the status of Kubernetes.

## Context

By selecting the Rancher Desktop Icon you can see the context globally. Select the context for `rancher-desktop`. This is the context globally so we are ensuring you are using Rancher Desktop.

## Version

Select the Rancher Desktop Icon and select `Preferences` and you will see the Rancher Desktop window. Select the `Kubernetes Setting` tab. There will be a drop down here called `Kubernetes Version`. This will be the latest stable version of Kubernetes. In this dropdown select the previous minor version of Kubernetes.

```bash
NOTE: Semantic versioning goes MAJOR.Minor.patch (0.0.0)
```

So, if the latest version of Kubernetes is v1.20.x select a version that is v1.19.x, where `x` is any patch number. Rancher Desktop will pull down and install that version of Kubernetes.

## Upgrading

Rancher Desktop allows you to easily upgrade and test your apps with newer version of Kubernetes. In the previous step we downgraded Rancher Desktop's version of Kubernetes now we are going to install and app and upgrade.

If you do not have the chart for WordPress the following command will add it:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Installing a demo WordPress app:

```bash
helm install demowp bitnami/wordpress
```

Your output should be similar to this (but not exact):

```bash
NAME: demowp
LAST DEPLOYED: Wed Jun  30 10:40:50 2021
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
** Please be patient while the chart is being deployed **

Your WordPress site can be accessed through the following DNS name from within your cluster:

    demowp-wordpress.default.svc.cluster.local (port 80)

To access your WordPress site from outside the cluster follow the steps below:

1. Get the WordPress URL by running these commands:

  NOTE: It may take a few minutes for the LoadBalancer IP to be available.
        Watch the status with: 'kubectl get svc --namespace default -w demowp-wordpress'

   export SERVICE_IP=$(kubectl get svc --namespace default demowp-wordpress --template "{{ range (index .status.loadBalancer.ingress 0) }}{{.}}{{ end }}")
   echo "WordPress URL: http://$SERVICE_IP/"
   echo "WordPress Admin URL: http://$SERVICE_IP/admin"

2. Open a browser and access WordPress using the obtained URL.

3. Login with the following credentials below to see your blog:

  echo Username: user
  echo Password: $(kubectl get secret --namespace default demowp-wordpress -o jsonpath="{.data.wordpress-password}" | base64 --decode)
```

From the Rancher Desktop window select the `Kubernetes Setting` tab. Go to the drop down called `Kubernetes Version` again and select the latest stable version of Kubernetes. 

```bash
NOTE: This might take a few minutes.
```

Your WordPress app should be up and running.

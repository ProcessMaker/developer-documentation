---
description: Install open-source ProcessMaker Platform using Kubernetes.
---

# Kubernetes for Production Deployment

## Overview

This guide provides instructions to deploy ProcessMaker on a Kubernetes cluster using Helm. This tutorial assumes a basic familiarity with Kubernetes concepts and commands. It is recommended to have a good understanding of concepts such as pods, deployments, services, and ingress. This knowledge will be beneficial for troubleshooting and managing the deployed application.

## Prerequisites

Before proceeding with the installation, ensure that you have met the following prerequisites.&#x20;

{% hint style="info" %}
A running Kubernetes cluster: Ensure that you have a Kubernetes cluster set up and accessible. This can be a local development cluster, a cloud-based Kubernetes service, or any other Kubernetes environment of your choice.
{% endhint %}

<table data-full-width="false"><thead><tr><th width="152">Requirement</th><th width="328">Function</th><th width="101">Version</th><th>Installation Guide</th></tr></thead><tbody><tr><td>Kubernetes</td><td>Kubernetes is a container orchestration platform that manages the deployment, scaling, and management of containerized applications. </td><td>1.19+</td><td><a href="https://kubernetes.io/docs/tasks/tools/">Setting Up Kubernetes</a></td></tr><tr><td>Helm</td><td>Helm is a package manager for Kubernetes that simplifies the deployment and management of applications. It allows you to define and manage application charts, which encapsulate all the necessary resources and configurations for your application.</td><td>3.12.0+</td><td><a href="https://helm.sh/docs/intro/install/">Setting up Helm</a></td></tr></tbody></table>

Please follow the steps outlined below to successfully deploy ProcessMaker on your Kubernetes cluster.

## Repository Configuration

To begin, add the ProcessMaker chart repository to Helm by executing the following command:

```
helm repo add processmaker https://charts.processmaker.io
```

This command ensures that you can access the ProcessMaker chart for installation.

## Update Repository

Update the list of repositories to fetch the latest charts:

```shell
helm repo update
```

## Install ProcessMaker on the Kubernetes Cluster

The following command deploys ProcessMaker on the Kubernetes cluster in the default configuration. The Parameters section lists the parameters that can be configured during installation.

```shell
helm install my-app processmaker/processmaker --set appConfig.host=my-app.example.com
```

This command deploys ProcessMaker on your Kubernetes cluster with the release name <`my-app>.` Replace \<m`y-app>` with a name of your choice. Also, set the `appConfig.host` parameter to your desired application host URL, such as `my-app.example.com.`

## Verify the Installation

After the installation, you can verify the deployment by listing all releases using the following command:

```shell
helm list
```

This command displays a list of all Helm releases, including the ProcessMaker release you just installed.

## Uninstall the ProcessMaker Deployment

If you need to uninstall or delete the ProcessMaker deployment, use the following command:

```shell
helm delete my-app
```

This command removes all the Kubernetes components associated with the ProcessMaker chart and deletes the release.

## Additional Configuration Options

The ProcessMaker chart provides various configuration options that you can customize during the installation. To explore all configurable options along with detailed descriptions, you have the following options:

1. **Review the `values.yaml` file:** You can inspect the chart's `values.yaml` file, which contains all the available configuration options and their default values.
2. **Use the `helm show values` command:** Run the following command to view the configurable options with their descriptions:

```
helm show values processmaker/processmaker
```

This command displays a detailed list of configuration options that can be customized during the installation.

{% hint style="info" %}
For further insights into the `values.yaml` file, we recommend exploring the following resources to deepen your understanding. [Configuration Values](https://artifacthub.io/packages/helm/processmaker/processmaker)
{% endhint %}

## Conclusion

In conclusion, this guide offers a step-by-step approach to installing ProcessMaker on Kubernetes using Helm. By following the instructions outlined in this guide, users can quickly and efficiently set up ProcessMaker, leveraging the power and flexibility of Kubernetes orchestration.

## Quick Start with Process Templates

Explore our ready-to-go Process Templates to kick-start your automation across several use cases and industries. Deploy into your Platform instance to spin up new processes and use as-is with all necessary assets included.

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><mark style="color:blue;">How to import Process Templates</mark></td><td></td><td></td><td><a href="https://processmaker.gitbook.io/processmaker/designing-processes/viewing-processes/manage-process-templates/import-and-configure-a-process-template">https://processmaker.gitbook.io/processmaker/designing-processes/viewing-processes/manage-process-templates/import-and-configure-a-process-template</a></td><td><a href="../../.gitbook/assets/Untitled.png">Untitled.png</a></td></tr><tr><td><mark style="color:blue;">Download Process Templates</mark></td><td></td><td></td><td><a href="https://www.processmaker.com/resources/customer-success/templates/">https://www.processmaker.com/resources/customer-success/templates/</a></td><td><a href="../../.gitbook/assets/all processes.png">all processes.png</a></td></tr></tbody></table>

---

copyright:
  years: 2017, 2020
lastupdated: "2020-03-19"

keywords: certificates, SSL, automation, deployments, cert, notification

subcollection: certificate-manager

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:script: data-hd-video='script'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}



# Tutorial: Automating deployments
{: #automating-deployments}

With {{site.data.keyword.cloudcerts_short}}, you can ensure that your certificates never expire by configuring automatic [renewal](/docs/certificate-manager?topic=certificate-manager-ordering-certificates) and deployment. By receiving notifications for incoming certificate lifecycle events - specifically the `cert_about_to_expire_renew_required` and `cert_renewed` event types, you can create a script that can deploy a recently renewed certificate before your current certificate expires. Your deployment can be accomplished in a number of ways depending on your SSL/TLS termination endpoint.
{: shortdesc}

This tutorial focuses on deploying renewed ordered certificates. [Refer to the API documentation](/apidocs/certificate-manager#renew-a-certificate){: external} to learn more about the `renew` API.
{: tip}

## Create a Callback URL notification channel 
{: #auto-deploy-create-url}

In order to automate deployments, you must use a Callback URL notification channel to listen for lifecycle events. The endpoint Callback URL can point to any server that can receive and respond to requests. For example: 

- An {{site.data.keyword.openwhisk}} action.
- An application that runs inside a Kubernetes cluster or elsewhere.
- A Cloud Foundry application.
- A Continuous Integration (CI) system.

To learn about creating notification channels, see [Configuring notifications](/docs/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).  
{: note}

## Listening for lifecycle events
{: #auto-deploy-listen}

In order to automate your deployment process, you need to know where in the certificate lifecycle that you are. So, in order to keep track, be sure to listen for the events that are listed in the following table. Then, you need to decrypt the information to obtain the certificate data.

| Lifecycle events | Description |
|:------------------|:------------|
| `cert_about_to_expire_renew_required` | An alert that is sent when a certificate is about to expire to remind you renew it. Depending on the setting that you selected you can either wait for the certificate to be auto-renewed or you can manually renew it. |
| `cert_renewed` | An alert that is sent when a certificate has been renewed. |
{: caption="Table 1. Life cycle events and what their alerts mean" caption-side="top"}

To learn about the various available certificate lifecycle event types see [Configuring notifications](/docs/certificate-manager?topic=certificate-manager-configuring-notifications). 
{: note}


## Deploy to SSL/TLS termination endpoints 
{: #auto-deploy-endpoints}

The way in which you download and deploy your renewed certificates is different depending on the termination endpoint that you use.
{: shortdesc}

### Option 1: Download the certificate by using {{site.data.keyword.cloudcerts_short}} API
{: #download-using-api}

To get the certificate from from {{site.data.keyword.cloudcerts_short}}:

1. Assign the deploying entity the `Writer` service access policy for the {{site.data.keyword.cloudcerts_short}} service.

  1. In the {{site.data.keyword.cloud_notm}} dashboard, click **Manage > Access (IAM) > Service IDs**.
  2. Select a service ID or create a new one. Click the set of credentials to open the management screen.
  3. Click **Access Policies > Assign access > Assign access to resources**.
  4. Select {{site.data.keyword.cloudcerts_short}} from the list of services. Provide the needed information and click the **Writer** check box. Be sure to save your changes.

2. Download the renewed certificate by making a `Get` request to the [certificate endpoint](/apidocs/certificate-manager#get-a-certificate){: external}.

  ```
  curl -H "Authorization: <IAM_token>" https://<region>.certificate-manager.cloud.ibm.com/api/v2/certificate/<certificate_ID>
  ```
  {: pre}

  <table>
    <caption>Table 3. Understanding the cURL command variables</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>IAM-token</code></td>
      <td>You can obtain an IAM token by making an [API call](/docs/iam?topic=iam-manapikey#manapikey) or by using the {{site.data.keyword.cloud_notm}} CLI to run <code>ibmcloud iam oauth-tokens</code>.</td>
    </tr>
    <tr>
      <td><code>region</code></td>
      <td>The region in which your {{site.data.keyword.cloudcerts_short}} service instance exists. Options include: <code>us-south</code>, <code>eu-gb</code>, <code>eu-de</code>, <code>jp-tok</code>, <code>au-syd</code>.</td>
    </tr>
    <tr>
      <td><code>certificate ID</code></td>
      <td>Your URL encoded certificate CRN.</td>
    </tr>
  </table>

3. Now that the certificate data is available, automate its deployment to your specific termination endpoint. There are a few ways in which you can accomplish the deployment. 

  If the termination endpoint is a Kubernetes cluster you can use either of:

  - [`kubectl` CLI](https://kubernetes.io/docs/concepts/configuration/secret/){: external}.
  - [Kubernetes Secret API](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.16/#secret-v1-core){: external} directly.
  - {{site.data.keyword.containershort}}'s CLI plug-in or [API](https://containers.cloud.ibm.com/global/swagger-global-api/#/alb-beta/UpdateALBSecret){: external} 

  If you're deploying to a different type of termination  endpoint, you might need to [convert](https://www.sslshopper.com/ssl-converter.html){: external} the certificate to a format other than PEM. Your endpoint might also offer an API with which you can integrate.
  {: tip}

### Option 2: Download and deploy by using ALB commands
{: #deploy-to-clusters-alb}

If your application runs on IBM Cloud Kubernetes service, you can use the {{site.data.keyword.containershort}} ALB commands to download and deploy your certificate at the same time. When you use an ALB command to deploy a certificate that is stored in a {{site.data.keyword.cloudcerts_short}} service instance, the certificate is downloaded and also creates a Kubernetes secret in your specified cluster.

To learn more about ALB commands, see [the ALB documentation](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_alb_cert_deploy).  
{: note}


1. Be sure that your Kubernetes cluster and your {{site.data.keyword.cloudcerts_short}} service instance are located in the same {{site.data.keyword.cloud_notm}} account.

2. Be sure that you have the latest version of the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/reference/ibmcloud?topic=cloud-cli-install-ibmcloud-cli) and the [{{site.data.keyword.containershort}} CLI plug-in](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli).

3. Assign the deploying entity the `Writer` service access policy for the {{site.data.keyword.cloudcerts_short}} service and the `Administrator` platform policy for the cluster that you're working with.

  1. In the {{site.data.keyword.cloud_notm}} dashboard, click **Manage > Access (IAM) > Service IDs**.
  2. Select a service ID or create a new one. Click the set of credentials to open the management screen.
  3. Click **Access Policies > Assign access > Assign access to resources**.
  4. Select {{site.data.keyword.cloudcerts_short}} from the list of services. Provide the needed information and click the **Writer** check box. 
  5. Click **Save**.
  6. In the list of services, select the Kubernetes cluster. Provide the needed information and click the **Administrator** check box.
  7. Click **Save**.

4. Using your command prompt, log in to IBM Cloud.

  ```
  ibmcloud login 
  ```
  {: codeblock}

5. Set the context for your cluster.

  1. Get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

  2. Copy the output beginning with `export` and paste it into your console to set the `KUBECONFIG` environment variable.

6. Download and deploy your certificate.

  ```
  ibmcloud ks alb cert deploy --cert-crn ${cert_Crn} --cluster ${Cluster_ID_Or_Name} --secret-name ${secretName}
  ```
  {: codeblock}

  <table>
    <caption>Table 4. Understanding the ALB command variables</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>cert_Crn</code></td>
      <td>The CRN of the renewed certificate.</td>
    </tr>
    <tr>
      <td><code>Cluster_ID_Or_Name</code></td>
      <td>The ID or name of your Kubernetes cluster.</td>
    </tr>
    <tr>
      <td><code>secret_Name</code></td>
      <td>The name of the Kubernetes Secret that is used by your Ingress resource.</td>
    </tr>
  </table>

  Your Ingress resource must reference the secret name that you have provided in the command.  
  {: important}
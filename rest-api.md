---
copyright:
  years: 2017
lastupdated: "2017-12-14"
---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Managing certificates by using the API
{: #managing-certificates-api}

The {{site.data.keyword.cloudcerts_full}} service provides REST endpoints to import, get, and delete certificates. Using {{site.data.keyword.iamshort}}, you can also [assign policies for a specific certificate](#assigning-advanced-policies).
{: shortdesc}

## Testing APIs
{: #testing}

You can test REST endpoints by using Swagger or by running cURL requests in the command line.  
Swagger is available in the US-South {{site.data.keyword.Bluemix_notm}} region only.
{: shortdesc}

## Prerequisites
{: #prereq-api}

You must complete the following tasks before you can use {{site.data.keyword.cloudcerts_full}}.
{: shortdesc}

* Install the [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/get_started.html#getting-started) to obtain the  required data.

* When you work with the {{site.data.keyword.cloudcerts_short}} API, you can use the following variables in your calls.


<table>
<caption> Table 1. Command components explained </caption>
  <tr>
    <th> Component </th>
    <th> Explanation </th>
  </tr>
  <tr>
    <td> <code> IAM-token </code> </td>
    <td> You can obtain your {{site.data.keyword.iamshort}} (IAM) access token by logging in to {{site.data.keyword.Bluemix_notm}} and running the <code>bx iam oauth-tokens</code> command. </td>
  </tr>
  <tr>
    <td> <code> certificateId </code> </td>
    
    <td> You can find your certificate ID by using one of the following choices: <ul><li> From the GUI, select the certificate from the row in the Certificates table. <li> From the API, [list your available certificates](/docs/services/certificate-manager/rest-api.html#list-certificates).</ul> </td> 
  </tr>
  <tr>
    <td> <code> instanceId </code> </td>
    <td> The [Cloud Resource Name (CRN)-based instance ID](/docs/overview/crn.html#format) that is assigned to your service instance after it is created. You can retrieve the instance ID in the following ways:
    <ul>
      <li>In the Manage page of the service.</li>
      <li>Run the <code>bx resource service-instance</code> command, replacing <i>&lt;Instance_Name&gt;</i> with the name of your service instance.
      <pre>bx resource service-instance &lt;Instance_Name&gt; --id</pre>
      </li>
      <li>Call the {{site.data.keyword.Bluemix_notm}} Resource Controller <code>[GET /resource_instances](https://console.bluemix.net/apidocs/700-resource-controller-api?&language=node#resource-instances-1)</code> REST endpoint, which requires the <code>Authorization</code> header with your account administrator's IAM token.</li>
    </ul>
  </td>
  </tr>
  <tr>
    <td>  <code> account-id </code> </td>
    <td> The account ID of the user that manages the {{site.data.keyword.Bluemix_notm}} account. You can find your account ID by running the <code>bx info</code> command. </td>
  </tr>
  <tr>
    <td>  <code> cluster-url </code> </td>
    <td> The URL of the service in the {{site.data.keyword.Bluemix_notm}} region in which it was created. You can find the URL in the Swagger UI. </td>
  </tr>
  <tr>
    <td>  <code> name (Optional) </code> </td>
    <td> The display name for the imported certificate. </td>
  </tr>
  <tr>
    <td> <code> description (Optional) </code> </td>
    <td> The description for the imported certificate. </td>
  </tr>
  <tr>
    <td> <code> certificate </code> </td>
    <td> The certificate data, escaped. </td>
  </tr>
  <tr>
    <td> <code> privateKey </code> </td>
    <td> The private key data, escaped. </td>
  </tr>
  <tr>
    <td> <code> intermediate (Optional) </code> </td>
    <td> The intermediate certificate data, escaped. </td>
  </tr>
  <tr>
    <td> <code> user-id </code> </td>
    <td>The ID of the user that you want to assign an access policy to. To find the user ID, see [Retrieving the user ID](#retrieve-user-id). </td>
  </tr>
</table>

## Importing a certificate
{: #import-certificate}  

Import a certificate in Privacy-enhanced Electronic Mail (PEM) format with its private key. You can also import an intermediate certificate.
{: shortdesc}


Run the following `curl` command:

  ```
  curl -X POST \
  https://<cluster-url>/api/v1/<instanceId>/certificates/import \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<description>",
	"data":{
		"content": "<certificate>",
		"priv_key": "<privateKey>",
		"intermediate": "<intermediate>"
	}
  }'
  ```
  {: pre}

Replace _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_, _&lt;description&gt;_, _&lt;certificate&gt;_,  _&lt;privateKey&gt;_, and _&lt;intermediate&gt;_ with the appropriate values. The _&lt;name&gt;_, _&lt;description&gt;_, and _&lt;intermediate&gt;_ values are optional.

## Updating certificate metadata
{: #update-certificate-metadata}  

Update a certificate’s optional `name`, `description`, or both, properties.

**Note**: Update operations are limited to five actions per minute.  
{: shortdesc}


Run the following `curl` command:

  ```
  curl -X POST \
  https://<cluster-url>/api/v1/<instanceId>/certificates/<certificateId> \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<description>"
  }'
  ```
  {: pre}

Replace _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;certificateId&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_, and _&lt;description&gt;_ with the appropriate values.

## Listing all of your certificates
{: #list-certificates}  

Retrieve a list of all of your available certificates.
{: shortdesc}

Run the following `curl` command:

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v1/<instanceId>/certificates/
  ```
  {: pre}

Replace _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, and _&lt;instanceId&gt;_ with the appropriate values.

## Downloading a certificate
{: #get-certificate}  

Use a retrieved certificate ID to download the certificate data.
{: shortdesc}

Run the following `curl` command:

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v1/<instanceId>/certificates/<certificateId>
  ```
  {: pre}

Replace _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, and _&lt;certificateId&gt;_ with the appropriate values.

## Deleting a certificate
{: #delete-certificate}  

Use a retrieved certificate ID to delete the certificate and its data.
{: shortdesc}

Run the following `curl` command:

  ```
  curl -H "Authorization: Bearer <IAM-token>" -X DELETE https://<cluster-url>/api/v1/<instanceId>/certificates/<certificateId>
  ```
  {: pre}

Replace _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, and _&lt;certificateId&gt;_ with the appropriate values.

## Assigning advanced policies
{: #assigning-advanced-policies}

You can choose to allow certain users to perform certain actions on specific certificates. You might want to allow users to view only a subset of the available service instance certificates.
{: shortdesc}

To assign the policy, send a request to {{site.data.keyword.iamshort}} by running the following `curl` command. Repeat the command for each certificate.

```
curl -X POST \
    https://iampap.<region>.bluemix.net/acms/v1/scopes/a%2<account-id>/users/<user-id>/policies \
    -H 'accept: application/json' \
    -H 'authorization: Bearer <Account-Admin-IAM-token>' \
    -H 'cache-control: no-cache' \
    -H 'content-type: application/json' \
    -d '{
        "roles": [
        {
            "id": "crn:v1:bluemix:public:iam::::role:Viewer"
        }
    ],
    "resources": [
        {
            "serviceName”: "cloudcerts",
            "serviceInstance": "<instanceId>",
            "resourceType": "certificate",
            "resource": "<certificateId>"
        }
    ]
}'
```
{: pre}

Replace _&lt;account-id&gt;_, _&lt;user-id&gt;_, _&lt;instanceId&gt;_ and _&lt;certificateId&gt;_ with the appropriate values.
Replace  _&lt;Account-Admin-IAM-token&gt;_ with the account administrator's IAM token.
Replace _&lt;region&gt;_ with your region, for example, `ng` for US-South.

**Note**: In the preceeding cURL request, <code>instanceId</code> is not CRN-based, it is GUID-based.  
For example, in the following <code>instanceId</code> CRN, the instance value is **58866f34-55ca-4477-8c32-fda435f01f97**.

```
crn:v1:staging:public:cloudcerts:us-south:a/d0c8a917589e40076a61e56b23056d16:58866f34-55ca-4477-8c32-fda435f01f97::
```

### Retrieving the user ID
{: #retrieve-user-id}

Retrieve the user ID.
{: shortdesc}

To retrieve the user ID, complete the following steps:

1. Ask the user to [provide the IAM token](/docs/services/certificate-manager/rest-api.html#prereq-api). The IAM token structure is in the following format: `<value_1>.<value_2>.<value_3>`
2. Copy the value of _&lt;value_2&gt;_ and run the following `echo` command:

   ```
   echo -n "<value_2>" | base64 --decode
   ```
   {: pre}

   The result is a JSON object similar to the following output:

   ```
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

3. Copy the value of the `id` property.

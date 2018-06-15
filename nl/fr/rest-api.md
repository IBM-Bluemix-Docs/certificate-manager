---
copyright:
  years: 2017, 2018
lastupdated: "2018-03-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Gestion des certificats via l'API
{: #managing-certificates-by-using-api}

Le service {{site.data.keyword.cloudcerts_full}} fournit des noeuds finaux REST permettant d'importer, d'obtenir et de supprimer des certificats. Avec {{site.data.keyword.iamshort}}, vous pouvez également [affecter des règles pour un certificat donné](#assigning-advanced-policies).
{: shortdesc}

## Test d'API
{: #testing}

Vous pouvez tester des noeuds finaux REST en utilisant Swagger ou en exécutant des demandes cURL en ligne de commande.  
Swagger est disponible uniquement dans la région {{site.data.keyword.Bluemix_notm}} du Sud des Etats-Unis.
{: shortdesc}

## Conditions préalables
{: #prereq-api}

Vous devez effectuer les tâches suivantes avant de pouvoir utiliser {{site.data.keyword.cloudcerts_full}} :
{: shortdesc}

* Installez l'[interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/get_started.html#getting-started) pour obtenir les données requises.

* Lorsque vous gérez l'API {{site.data.keyword.cloudcerts_short}}, vous pouvez utiliser les variables suivantes dans vos appels.


<table>
<caption> Tableau 1. Explication des composants de la commande </caption>
  <tr>
    <th> Composant </th>
    <th> Explication </th>
  </tr>
  <tr>
    <td> <code> IAM-token </code> </td>
    <td> Vous pouvez obtenir votre jeton d'accès {{site.data.keyword.iamshort}} (IAM) en vous connectant à {{site.data.keyword.Bluemix_notm}} et en exécutant la commande <code>bx iam oauth-tokens</code>. </td>
  </tr>
  <tr>
    <td> <code> certificateId </code> </td>
    <td> [ID certificat CRN (Cloud Resource Name)](/docs/overview/crn.html#format) affecté à votre certificat une fois celui-ci importé. Pour obtenir votre ID de certificat, utilisez l'une des options suivantes : <ul><li> Dans l'onglet de gestion du service, affichez les informations du certificat en sélectionnant celui-ci dans le tableau Certificats.<li> Via l'API : [répertoriez les certificats dont vous disposez](/docs/services/certificate-manager/rest-api.html#list-certificates).</ul> </td>
  </tr>
  <tr>
    <td> <code> instanceId </code> </td>
    <td> [ID d'instance CRN (Cloud Resource Name)](/docs/overview/crn.html#format) qui est affecté à votre instance de service une fois celle-ci créée. Vous pouvez extraire l'ID d'instance en procédant comme suit :
    <ul>
      <li>Sur la page Gérer du service.</li>
      <li>Exécutez la commande <code>bx resource service-instance</code> en remplaçant <i>&lt;Instance_Name&gt;</i> par le nom de votre instance de service.
      <pre>bx resource service-instance &lt;Instance_Name&gt; --id</pre>
      </li>
      <li>Appelez le noeud final REST <code>[GET /resource_instances](https://console.bluemix.net/apidocs/700-resource-controller-api?&language=node#resource-instances-1)</code> de {{site.data.keyword.Bluemix_notm}} Resource Controller, qui requiert l'en-tête <code>Authorization</code> avec le jeton IAM de votre administrateur de compte.</li>
    </ul>
  </td>
  </tr>
  <tr>
    <td>  <code> account-id </code> </td>
    <td> ID de compte que l'utilisateur qui gère le compte {{site.data.keyword.Bluemix_notm}}. Pour connaître votre ID de compte, exécutez la commande <code>bx info</code>. </td>
  </tr>
  <tr>
    <td>  <code> cluster-url </code> </td>
    <td> URL du service dans la région {{site.data.keyword.Bluemix_notm}} dans laquelle il a été créé. L'URL est définie dans l'interface utilisateur Swagger. </td>
  </tr>
  <tr>
    <td>  <code> name (Optional) </code> </td>
    <td> Nom d'affichage du certificat importé. </td>
  </tr>
  <tr>
    <td> <code> description (Optional) </code> </td>
    <td> Description du certificat importé. </td>
  </tr>
  <tr>
    <td> <code> certificate </code> </td>
    <td> Données de certificat, avec caractères d'échappement. </td>
  </tr>
  <tr>
    <td> <code> privateKey </code> </td>
    <td> Données de clé privée, avec caractères d'échappement. </td>
  </tr>
  <tr>
    <td> <code> intermediate (Optional) </code> </td>
    <td> Données de certificat intermédiaire, avec caractères d'échappement. </td>
  </tr>
  <tr>
    <td> <code> user-id </code> </td>
    <td>ID de l'utilisateur auquel vous souhaitez affecter une règle d'accès. Pour connaître l'ID utilisateur, voir [Extraction de l'ID utilisateur](#retrieve-user-id). </td>
  </tr>
</table>

## Importation d'un certificat
{: #import-certificate}  

Importez un certificat au format PEM (Privacy-enhanced Electronic Mail) avec sa clé privée. Vous pouvez également importer un certificat intermédiaire.
{: shortdesc}


Exécutez la commande `curl` suivante :

  ```
  curl -X POST \
  https://<cluster-url>/api/v2/<instanceId>/certificates/import \
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

Remplacez _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_, _&lt;description&gt;_, _&lt;certificate&gt;_, _&lt;privateKey&gt;_ et _&lt;intermediate&gt;_ par les valeurs appropriées. Les valeurs _&lt;name&gt;_, _&lt;description&gt;_ et _&lt;intermediate&gt;_ sont facultatives.

## Mise à jour des métadonnées de certificat
{: #update-certificate-metadata}  

Mettez à jour la propriété `name` et/ou la propriété `description` facultatives d'un certificat.

**Remarque** : les opérations de mise à jour sont limitées à cinq actions par minute.  
{: shortdesc}

Exécutez la commande `curl` suivante :

  ```
  curl -X POST \
  https://<cluster-url>/api/v2/certificate/<certificateId> \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<description>"
  }'
  ```

{: pre}

Remplacez _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;certificateId&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_ et_&lt;description&gt;_ par les valeurs appropriées.

## Affichage de tous vos certificats
{: #list-certificates}  

Extrayez une liste de tous les certificats disponibles.
{: shortdesc}

Exécutez la commande `curl` suivante :

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v2/<instanceId>/certificates/
  ```

  {: pre}

Remplacez _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_ et _&lt;instanceId&gt;_ par les valeurs appropriées.

## Téléchargement d'un certificat
{: #get-certificate}  

Utilisez un ID de certificat extrait pour télécharger les données de certificat.
{: shortdesc}

Exécutez la commande `curl` suivante :

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v2/certificate/<certificateId>
  ```

{: pre}

Remplacez _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_ et _&lt;certificateId&gt;_ par les valeurs appropriées.

## Suppression d'un certificat
{: #delete-certificate}  

Utilisez un ID de certificat extrait pour supprimer le certificat et ses données.
{: shortdesc}

Exécutez la commande `curl` suivante :

  ```
  curl -H "Authorization: Bearer <IAM-token>" -X DELETE https://<cluster-url>/api/v2/certificate/<certificateId>
  ```

  {: pre}

Remplacez _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_ et _&lt;certificateId&gt;_ par les valeurs appropriées.

## Affectation de règles avancées
{: #assigning-advanced-policies}

Vous pouvez choisir de permettre à certains utilisateurs d'exécuter certaines actions sur des certificats spécifiques. Vous pouvez également autoriser des utilisateurs à visualiser uniquement un sous-ensemble des certificats d'instance de service disponibles.
{: shortdesc}

Pour affecter la règle, envoyez une demande à {{site.data.keyword.iamshort}} en exécutant la commande `curl` ci-après. Répétez la commande pour chaque certificat.

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

Remplacez _&lt;account-id&gt;_, _&lt;user-id&gt;_, _&lt;instanceId&gt;_ et _&lt;certificateId&gt;_ par les valeurs appropriées.
Remplacez _&lt;Account-Admin-IAM-token&gt;_ par le jeton IAM de l'administrateur de compte.
Remplacez _&lt;region&gt;_ par votre région, par exemple, `ng` pour le Sud des Etats-Unis.

**Remarque** : dans la demande cURL précédente, <code>instanceId</code> et <code>certificateId</code> ne sont pas basés sur le nom de ressource de cloud mais sur l'identificateur global unique.  
Par exemple, dans le nom de ressource de cloud <code>certificateId</code> suivant, la valeur pour instanceId est **58866f34-55ca-4477-8c32-fda435f01f97** et celle pour certificateId **e20cb664efcbfa2c2f57801230d246a6**.

```
crn:v1:staging:public:cloudcerts:us-south:a/d0c8a917589e40076a61e56b23056d16:58866f34-55ca-4477-8c32-fda435f01f97:certificate:e20cb664efcbfa2c2f57801230d246a6
```

### Extraction de l'ID utilisateur
{: #retrieve-user-id}

Récupérez l'ID utilisateur.
{: shortdesc}

Pour récupérer l'ID utilisateur, procédez comme suit :

1. Demandez à l'utilisateur de [fournir le jeton IAM](/docs/services/certificate-manager/rest-api.html#prereq-api). La structure de jeton IAM est au format suivant :
`<value_1>.<value_2>.<value_3>`
2. Copiez la valeur _&lt;value_2&gt;_ et exécutez la commande `echo` suivante :

   ```
   echo -n "<value_2>" | base64 --decode
   ```
   {: pre}

   Le résultat est un objet JSON similaire à la sortie suivante :

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

3. Copiez la valeur de la propriété `id`.

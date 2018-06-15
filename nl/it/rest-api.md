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

# Gestione certificati utilizzando l'API 
{: #managing-certificates-by-using-api}

Il servizio {{site.data.keyword.cloudcerts_full}} fornisce gli endpoint REST per importare, ottenere ed eliminare i certificati. Utilizzando {{site.data.keyword.iamshort}}, puoi anche [assegnare le politiche a un certificato specifico](#assigning-advanced-policies).
{: shortdesc}

## Verifica API
{: #testing}

Puoi verificare gli endpoint REST utilizzando Swagger o eseguendo le richieste cURL nella riga di comando.  
Swagger è disponibile solo nella regione {{site.data.keyword.Bluemix_notm}} Stati Uniti Sud.
{: shortdesc}

## Prerequisiti
{: #prereq-api}

Devi completare le seguenti attività prima di poter utilizzare {{site.data.keyword.cloudcerts_full}}.
{: shortdesc}

* Installa la [CLI {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/get_started.html#getting-started) per ottenere i dati necessari.

* Quando utilizzi l'API {{site.data.keyword.cloudcerts_short}}, puoi utilizzare le seguenti variabili nelle tue chiamate.


<table>
<caption> Tabella 1. Componenti del comando spiegati </caption>
  <tr>
    <th> Componente </th>
    <th> Spiegazione </th>
  </tr>
  <tr>
    <td> <code> IAM-token </code> </td>
    <td> Puoi ottenere il tuo token di accesso {{site.data.keyword.iamshort}} (IAM) accedendo a {{site.data.keyword.Bluemix_notm}} ed eseguendo il comando <code>bx iam oauth-tokens</code>. </td>
  </tr>
  <tr>
    <td> <code> certificateId </code> </td>
    <td> L'[ID del certificato basato su CRN (Cloud Resource Name)](/docs/overview/crn.html#format) assegnato al tuo certificato dopo l'importazione. Puoi trovare il tuo ID del certificato utilizzando una delle seguenti scelte: <ul><li> Nella scheda di gestione del servizio, visualizza le informazioni sul certificato selezionandolo nella scheda dei certificati. <li> Tramite l'API: [elenca i tuoi certificati disponibili](/docs/services/certificate-manager/rest-api.html#list-certificates).</ul> </td>
  </tr>
  <tr>
    <td> <code> instanceId </code> </td>
    <td> L'[ID dell'istanza basato su CRN (Cloud Resource Name)](/docs/overview/crn.html#format) assegnato alla tua istanza del servizio dopo la creazione. Puoi richiamare l'ID dell'istanza nei seguenti modi:
    <ul>
      <li>Nella pagina di gestione del servizio.</li>
      <li>Esegui il comando <code>bx resource service-instance</code>, sostituendo <i>&lt;Instance_Name&gt;</i> con il nome della tua istanza del servizio.
      <pre>bx resource service-instance &lt;Instance_Name&gt; --id</pre>
      </li>
      <li>Richiama il controller della risorsa {{site.data.keyword.Bluemix_notm}} <code>[GET /resource_instances](https://console.bluemix.net/apidocs/700-resource-controller-api?&language=node#resource-instances-1)</code> endpoint REST, che richiede l'intestazione <code>Authorization</code> con il token IAM del tuo amministratore dell'account.</li>
    </ul>
  </td>
  </tr>
  <tr>
    <td>  <code> account-id </code> </td>
    <td> L'ID dell'account dell'utente che gestisce l'account {{site.data.keyword.Bluemix_notm}}. Puoi trovare il tuo ID account eseguendo il comando <code>bx info</code>. </td>
  </tr>
  <tr>
    <td>  <code> cluster-url </code> </td>
    <td> L'URL del servizio nella regione {{site.data.keyword.Bluemix_notm}} in cui è stato creato. Puoi trovare l'URL nella IU Swagger. </td>
  </tr>
  <tr>
    <td>  <code> name (facoltativo) </code> </td>
    <td> Il nome di visualizzazione del certificato importato. </td>
  </tr>
  <tr>
    <td> <code> description (facoltativo) </code> </td>
    <td> La descrizione del certificato importato. </td>
  </tr>
  <tr>
    <td> <code> certificate </code> </td>
    <td> I dati del certificato, con escape. </td>
  </tr>
  <tr>
    <td> <code> privateKey </code> </td>
    <td> I dati della chiave privata, con escape. </td>
  </tr>
  <tr>
    <td> <code> intermediate (facoltativo) </code> </td>
    <td> I dati del certificato intermedio, con escape. </td>
  </tr>
  <tr>
    <td> <code> user-id </code> </td>
    <td>L'ID dell'utente a cui desideri assegnare una politica di accesso. Per trovare l'ID utente, consulta [Richiamo di un ID utente](#retrieve-user-id). </td>
  </tr>
</table>

## Importazione di un certificato
{: #import-certificate}  

Importa un certificato nel formato Privacy-enhanced Electronic Mail (PEM) con la relativa chiave privata. Puoi anche importare un certificato intermedio.
{: shortdesc}


Immetti il seguente comando `curl`:

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

Sostituisci _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_, _&lt;description&gt;_, _&lt;certificate&gt;_,  _&lt;privateKey&gt;_ e _&lt;intermediate&gt;_ con i valori appropriati. I valori _&lt;name&gt;_, _&lt;description&gt;_ e _&lt;intermediate&gt;_ sono facoltativi.

## Aggiornamento dei metadati del certificato
{: #update-certificate-metadata}  

Aggiorna le proprietà facoltative `name`, `description`, o entrambe, del certificato.

**Nota**: le operazioni di aggiornamento sono limitate a cinque azioni al minuto.  
{: shortdesc}

Immetti il seguente comando `curl`:

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

Sostituisci _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;certificateId&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_ e _&lt;description&gt;_ con i valori appropriati.

## Elenco di tutti i tuoi certificati
{: #list-certificates}  

Richiama un elenco di tutti i tuoi certificati disponibili.
{: shortdesc}

Immetti il seguente comando `curl`:

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v2/<instanceId>/certificates/
  ```

  {: pre}

Sostituisci _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_ e _&lt;instanceId&gt;_ con i valori appropriati.

## Scaricamento di un certificato
{: #get-certificate}  

Utilizza un ID del certificato richiamato per scaricare i dati del certificato.
{: shortdesc}

Immetti il seguente comando `curl`:

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v2/certificate/<certificateId>
  ```

{: pre}

Sostituisci _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_ e_&lt;certificateId&gt;_ con i valori appropriati.

## Eliminazione di un certificato
{: #delete-certificate}  

Utilizza un ID del certificato richiamato per eliminare il certificato e i relativi dati.
{: shortdesc}

Immetti il seguente comando `curl`:

  ```
  curl -H "Authorization: Bearer <IAM-token>" -X DELETE https://<cluster-url>/api/v2/certificate/<certificateId>
  ```

  {: pre}

Sostituisci _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_ e_&lt;certificateId&gt;_ con i valori appropriati.

## Assegnazione delle politiche avanzate
{: #assigning-advanced-policies}

Puoi scegliere di permettere ad alcuni utenti di eseguire alcune azioni in certificati specifici. Potresti voler consentire agli utenti di visualizzare solo un sottoinsieme di certificati dell'istanza del servizio disponibili.
{: shortdesc}

Per assegnare la politica, invia una richiesta a {{site.data.keyword.iamshort}} immettendo il seguente comando `curl`. Ripeti il comando per ogni certificato.

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

Sostituisci _&lt;account-id&gt;_, _&lt;user-id&gt;_, _&lt;instanceId&gt;_ e _&lt;certificateId&gt;_ con i valori appropriati.
Sostituisci _&lt;Account-Admin-IAM-token&gt;_ con il token IAM dell'amministratore dell'account.
Sostituisci _&lt;region&gt;_ con la tua regione, ad esempio, `ng` per Stati Uniti Sud.

**Nota**: nella precedente richiesta cURL, <code>instanceId</code> e <code>certificateId</code> non sono basati su CRN ma su GUID.  
Ad esempio, nel seguente CRN <code>certificateId</code>, il valore instanceId è **58866f34-55ca-4477-8c32-fda435f01f97** e certificateId è **e20cb664efcbfa2c2f57801230d246a6**.

```
crn:v1:staging:public:cloudcerts:us-south:a/d0c8a917589e40076a61e56b23056d16:58866f34-55ca-4477-8c32-fda435f01f97:certificate:e20cb664efcbfa2c2f57801230d246a6
```

### Richiamo dell'ID utente
{: #retrieve-user-id}

Richiamo dell'ID utente.
{: shortdesc}

Per richiamare l'ID utente, completa la seguente procedura:

1. Chiedi all'utente di [fornire il token IAM](/docs/services/certificate-manager/rest-api.html#prereq-api). La struttura del token IAM è nel seguente formato: `<value_1>.<value_2>.<value_3>`
2. Copia il valore di _&lt;value_2&gt;_ ed immetti il seguente comando `echo`:

   ```
   echo -n "<value_2>" | base64 --decode
   ```
   {: pre}

   Il risultato è un oggetto JSON simile al seguente output:

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

3. Copia il valore della proprietà `id`.

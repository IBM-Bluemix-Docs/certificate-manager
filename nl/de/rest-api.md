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

# Zertifikate mithilfe der API verwalten
{: #managing-certificates-api}

Der {{site.data.keyword.cloudcerts_full}}-Service bietet REST-Endpunkte zum Importieren, Abrufen und Löschen von Zertifikaten. Unter Verwendung von {{site.data.keyword.iamshort}} können Sie auch [Richtlinien für ein bestimmtes Zertifikat zuweisen](#assigning-advanced-policies).
{: shortdesc}

## APIs testen
{: #testing}

Sie können REST-Endpunkte mithilfe von Swagger oder durch Ausführen von cURL-Anforderungen in der Befehlszeile testen.  
Swagger ist nur in der {{site.data.keyword.Bluemix_notm}}-Region 'Vereinigte Staaten (Süden)' verfügbar.
{: shortdesc}

## Voraussetzungen
{: #prereq-api}

Sie müssen die folgenden Tasks ausführen, bevor Sie {{site.data.keyword.cloudcerts_full}} verwenden können.
{: shortdesc}

* Installieren Sie die [{{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle](/docs/cli/reference/bluemix_cli/get_started.html#getting-started), um die erforderlichen Daten anzufordern.

* Wenn Sie mit der {{site.data.keyword.cloudcerts_short}}-API arbeiten, können Sie die folgenden Variablen in Ihren Aufrufen verwenden.


<table>
<caption> Tabelle 1. Erläuterung von Befehlskomponenten </caption>
  <tr>
    <th> Komponente </th>
    <th> Erläuterung </th>
  </tr>
  <tr>
    <td> <code> IAM-token </code> </td>
    <td> Sie können Ihr IAM-Zugriffstoken ({{site.data.keyword.iamshort}}) anfordern, indem Sie sich bei {{site.data.keyword.Bluemix_notm}} anmelden und den Befehl <code>bx iam oauth-tokens</code> ausführen. </td>
  </tr>
  <tr>
    <td> <code> zertifikat-ID </code> </td>
    <td> Sie können Ihre Zertifikat-ID auf einem der folgenden Wege ermitteln: <ul><li> Über die Benutzerschnittstelle: Wählen Sie das Zertifikat in der Zeile in der Zertifikatstabelle aus. <li> Über die API: [Listen Sie die verfügbaren Zertifikate auf](/docs/services/certificate-manager/rest-api.html#list-certificates).</ul> </td>
  </tr>
  <tr>
    <td> <code> instanz-ID </code> </td>
    <td> Die [CRN-basierte Instanz-ID](/docs/overview/crn.html#format) (CRN = Cloudressourcenname), die Ihrer Serviceinstanz nach ihrer Erstellung zugewiesen wurde. Sie können die Instanz-ID auf folgende Art und Weise abrufen:
<ul>
      <li>Auf der Seite 'Verwalten' des Service.</li>
      <li>Ausführung des Befehls <code>bx resource service-instance</code>, wobei <i>&lt;instanzname&gt;</i> durch den Namen Ihrer Serviceinstanz zu ersetzen ist.
      <pre>bx resource service-instance &lt;instanzname&gt; --id</pre>
      </li>
      <li>Aufruf des {{site.data.keyword.Bluemix_notm}} Resource Controller-REST-Endpunkts <code>[GET /resource_instances](https://console.bluemix.net/apidocs/700-resource-controller-api?&language=node#resource-instances-1)</code>. Dies setzt einen <code>Authorization</code>-Header mit dem IAM-Token Ihres Kontoadministrators voraus.</li>
    </ul>
  </td>
  </tr>
  <tr>
    <td>  <code> konto-ID </code> </td>
    <td> Die Konto-ID des Benutzers, der das {{site.data.keyword.Bluemix_notm}}-Konto verwaltet. Sie können Ihre Konto-ID ermitteln, indem Sie den Befehl <code>bx info</code> ausführen. </td>
  </tr>
  <tr>
    <td>  <code> cluster-URL </code> </td>
    <td> Die URL des Service in der {{site.data.keyword.Bluemix_notm}}-Region, in der er erstellt wurde. Sie finden die URL auf der Swagger-Benutzerschnittstelle. </td>
  </tr>
  <tr>
    <td>  <code> name (optional) </code> </td>
    <td> Der Anzeigename für das importierte Zertifikat. </td>
  </tr>
  <tr>
    <td> <code> beschreibung (optional) </code> </td>
    <td> Die Beschreibung für das importierte Zertifikat. </td>
  </tr>
  <tr>
    <td> <code> zertifikat </code> </td>
    <td> Die Zertifikatsdaten (mit Escapezeichen). </td>
  </tr>
  <tr>
    <td> <code> privater_schlüssel </code> </td>
    <td> Die Daten des privaten Schlüssels (mit Escapezeichen). </td>
  </tr>
  <tr>
    <td> <code> zwischenzertifikat (optional) </code> </td>
    <td> Die Zwischenzertifikatsdaten (mit Escapezeichen). </td>
  </tr>
  <tr>
    <td> <code> benutzer-ID </code> </td>
    <td>Die ID des Benutzers, dem sie eine Zugriffsrichtlinie zuweisen wollen. Informationen zum Ermitteln der Benutzer-ID finden Sie unter [Benutzer-ID abrufen](#retrieve-user-id). </td>
  </tr>
</table>

## Zertifikat importieren
{: #import-certificate}  

Importieren Sie ein Zertifikat im PEM-Format (PEM = Privacy-enhanced Electronic Mail) mit dem zugehörigen privaten Schlüssel. Sie haben außerdem die Möglichkeit, ein Zwischenzertifikat zu importieren.
{: shortdesc}


Führen Sie den folgenden Befehl `curl` aus:

  ```
  curl -X POST \
  https://<cluster-URL>/api/v1/<instanz-ID>/certificates/import \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<beschreibung>",
	"data":{
		"content": "<zertifikat>",
		"priv_key": "<privater_schlüssel>",
		"intermediate": "<zwischenzertifikat>"
	}
  }'
  ```
  {: pre}

Ersetzen Sie _&lt;cluster-URL&gt;_, _&lt;instanz-ID&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_, _&lt;beschreibung&gt;_, _&lt;zertifikat&gt;_, _&lt;privater_schlüssel&gt;_ und _&lt;zwischenzertifikat&gt;_ durch die entsprechenden Werte. Die Werte _&lt;name&gt;_, _&lt;beschreibung&gt;_ und _&lt;zwischenzertifikat&gt;_ sind optional.

## Zertifikatsmetadaten aktualisieren
{: #update-certificate-metadata}  

Aktualisieren Sie die optionale Eigenschaft `name` oder `beschreibung` (oder beide) für ein Zertifikat.

**Hinweis**: Aktualisierungsoperationen sind auf fünf Aktionen pro Minute begrenzt.  
{: shortdesc}


Führen Sie den folgenden Befehl `curl` aus:

  ```
  curl -X POST \
  https://<cluster-URL>/api/v1/<instanz-ID>/certificates/<zertifikat-ID> \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<beschreibung>"
  }'
  ```
  {: pre}

Ersetzen Sie _&lt;cluster-URL&gt;_, _&lt;instanz-ID&gt;_, _&lt;zertifikat-ID&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_ und _&lt;beschreibung&gt;_ durch die entsprechenden Wert.

## Alle eigenen Zertifikate auflisten
{: #list-certificates}  

Rufen Sie eine Liste aller Zertifikate ab, die Ihnen zur Verfügung stehen.
{: shortdesc}

Führen Sie den folgenden Befehl `curl` aus:

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-URL>/api/v1/<instanz-ID>/certificates/
  ```
  {: pre}

Ersetzen Sie _&lt;IAM-token&gt;_, _&lt;cluster-URL&gt;_ und _&lt;instanz-ID&gt;_ durch die entsprechenden Werte.

## Zertifikat herunterladen
{: #get-certificate}  

Verwenden Sie eine abgerufene Zertifikat-ID, um die Zertifikatsdaten herunterzuladen.
{: shortdesc}

Führen Sie den folgenden Befehl `curl` aus:

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-URL>/api/v1/<instanz-ID>/certificates/<zertifikat-ID>
  ```
  {: pre}

Ersetzen Sie _&lt;IAM-token&gt;_, _&lt;cluster-URL&gt;_, _&lt;instanz-ID&gt;_ und _&lt;zertifikat-ID&gt;_ durch die entsprechenden Werte.

## Zertifikat löschen
{: #delete-certificate}  

Verwenden Sie eine abgerufene Zertifikat-ID, um das Zertifikat und seine Daten zu löschen.
{: shortdesc}

Führen Sie den folgenden Befehl `curl` aus:

  ```
  curl -H "Authorization: Bearer <IAM-token>" -X DELETE https://<cluster-URL>/api/v1/<instanz-ID>/certificates/<zertifikat-ID>
  ```
  {: pre}

Ersetzen Sie _&lt;IAM-token&gt;_, _&lt;cluster-URL&gt;_, _&lt;instanz-ID&gt;_ und _&lt;zertifikat-ID&gt;_ durch die entsprechenden Werte.

## Erweiterte Richtlinien zuweisen
{: #assigning-advanced-policies}

Sie können bestimmten Benutzern die Ausführung bestimmter Aktionen bei spezifischen Zertifikaten ermöglichen. Sie können bei bestimmten Benutzern die Anzeige auf einen Teil der verfügbaren Serviceinstanzzertifikate einschränken.
{: shortdesc}

Um die Richtlinie zuzuweisen, senden Sie eine Anforderung an {{site.data.keyword.iamshort}}, indem Sie den folgenden Befehl `curl` ausführen. Wiederholen Sie den Befehl für jedes Zertifikat.

```
curl -X POST \
    https://iampap.<region>.bluemix.net/acms/v1/scopes/a%2<konto-ID>/users/<benutzer-ID>/policies \
    -H 'accept: application/json' \
    -H 'authorization: Bearer <konto-admin-IAM-token>' \
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
            "serviceInstance": "<instanz-ID>",
            "resourceType": "certificate",
            "resource": "<zertifikat-ID>"
        }
    ]
}'
```
{: pre}

Ersetzen Sie _&lt;konto-ID&gt;_, _&lt;benutzer-ID&gt;_, _&lt;instanz-ID&gt;_ und _&lt;zertifikat-ID&gt;_ durch die entsprechenden Werte.
Ersetzen Sie _&lt;konto-admin-IAM-token&gt;_ durch das IAM-Token des Kontoadministrators.
Ersetzen Sie _&lt;region&gt;_ durch Ihre Region (z. B. `ng` für Vereinigte Staaten (Süden)).

**Hinweis**: In der vorangegangenen cURL-Anforderung ist <code>instanz-ID</code> nicht CRN-basiert, sie ist GUID-basiert.  
Beispiel: Im folgenden <code>instanz-ID</code>-CRN ist **58866f34-55ca-4477-8c32-fda435f01f97** der Instanzwert.

```
crn:v1:staging:public:cloudcerts:us-south:a/d0c8a917589e40076a61e56b23056d16:58866f34-55ca-4477-8c32-fda435f01f97::
```

### Benutzer-ID abrufen
{: #retrieve-user-id}

Rufen Sie die Benutzer-ID ab.
{: shortdesc}

Führen Sie die folgenden Schritte aus, um die Benutzer-ID abzurufen:

1. Bitten Sie den Benutzer, [das IAM-Token anzugeben](/docs/services/certificate-manager/rest-api.html#prereq-api). Die Struktur des IAM-Tokens hat folgendes Format: `<value_1>.<value_2>.<value_3>`
2. Kopieren Sie den Wert von _&lt;wert_2&gt;_ und führen Sie den folgenden Befehl `echo` aus:

   ```
   echo -n "<wert_2>" | base64 --decode
   ```
   {: pre}

   Das Ergebnis ist ein JSON-Objekt, das folgender Ausgabe ähnlich ist:

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

3. Kopieren Sie den Wert der Eigenschaft `id`.

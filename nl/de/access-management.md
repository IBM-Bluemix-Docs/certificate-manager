---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-07"

keywords: certificates, SSL, 

subcollection: certificate-manager

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}

# Zugriffsrollen für den Service verwalten
{: #managing-service-access-roles}

Sie können Services in {{site.data.keyword.Bluemix_notm}} dadurch schützen, dass bestimmten Aktionen nur von Benutzern ausgeführt werden können, die bestimmte Zugriffsrollen haben.
{: shortdesc}

## Zugriffsrollen für die Plattform
{: #platform-access-roles}

Mithilfe von Plattformzugriffsrollen können Sie es Benutzern ermöglichen, Aufgaben für Plattformressourcen durchzuführen, wie z. B. das Erstellen und Löschen von Instanzen in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto.

<table>
<caption> Tabelle 1. Aktionen, die Plattformzugriffsrollen zugeordnet werden</caption>
  <tr>
    <th> Aktion </th>
    <th> Rolle </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudcerts_short}}-Instanzen anzeigen</td>
    <td> Administrator, Operator, Bearbeiter, Anzeigeberechtigter </td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudcerts_short}}-Instanz erstellen</td>
    <td> Administrator, Bearbeiter </td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudcerts_short}}-Instanz löschen</td>
    <td> Administrator, Bearbeiter </td>
  </tr>
</table>

## Zugriffsrollen für den Service
{: #service-access-roles}

Mithilfe von Servicezugriffsrollen können Sie es Benutzern ermöglichen, Aufgaben in {{site.data.keyword.cloudcerts_short}}-Instanzen durchzuführen, wie z. B. das Importieren, Herunterladen, Bearbeiten oder Löschen von Zertifikaten.

<table>
<caption> Tabelle 1. Aktionen, die Servicezugriffsrollen zugeordnet werden</caption>
  <tr>
    <th> Aktion </th>
    <th> Rolle </th>
  </tr>
  <tr>
    <td>Zertifikate auflisten</td>
    <td> Manager, Schreibberechtigter, Leseberechtigter </td>
  </tr>
  <tr>
    <td>Zertifikat und privaten Schlüssel herunterladen </td>
    <td> Manager, Schreibberechtigter </td>
  </tr>
  <tr>
    <td>Metadaten des Zertifikats aktualisieren</td>
    <td> Manager, Schreibberechtigter </td>
  </tr>
  <tr>
    <td>Zertifikate, private Schlüssel und Zwischenzertifikate importieren oder erneut importieren </td>
    <td> Manager </td>
  </tr>
  <tr>
    <td>Zertifikat und privaten Schlüssel löschen </td>
    <td> Manager </td>
  </tr>
      <tr>
        <td>Alle Benachrichtigungskanäle auflisten </td>
        <td> Manager, Schreibberechtigter, Leseberechtigter </td>
      </tr>
   <tr>
     <td>Benachrichtigungskanal hinzufügen, aktualisieren oder löschen </td>
     <td> Manager </td>
   </tr>
     <tr>
       <td>Benachrichtigungskanal testen </td>
       <td> Manager, Schreibberechtigter, Leseberechtigter </td>
     </tr>
</table>

Weitere Informationen zu Benutzerrollen und Berechtigungen finden Sie unter [Benutzerrollen](/docs/iam?topic=iam-userroles#userroles).

## Zugriffsrichtlinien für Benutzer konfigurieren
{: #configuring-access-policies}

Sie können Zugriffsrichtlinien für eine {{site.data.keyword.cloudcerts_short}}-Instanz (und damit für alle Zertifikate in dieser Instanz) konfigurieren oder Richtlinien für einzelne Zertifikate (Ressourcen) innerhalb einer Instanz festlegen.
{: shortdesc}

Führen Sie die folgenden Schritte aus, um Zugriffsrichtlinien zu konfigurieren:

1. Navigieren Sie zu **Verwalten > Konto > Benutzer**. Eine Liste der Benutzer, die über Zugriff auf Ihr {{site.data.keyword.Bluemix_notm}}-Konto verfügen, wird angezeigt.
2. Klicken Sie auf den Namen des Benutzers, dem Sie eine Zugriffsrichtlinie zuweisen möchten. Wenn der Benutzer nicht angezeigt wird, klicken Sie auf **Benutzer einladen**, um [den Benutzer zu Ihrem {{site.data.keyword.Bluemix_notm}}-Konto hinzuzufügen](/docs/iam?topic=iam-iamuserinv#iamuserinv).
3. Klicken Sie auf **Zugriff zuweisen**.
4. Klicken Sie auf **Zugriff auf Ressourcen zuweisen**.
5. Wählen Sie im Menü **Services** die Option **Zertifikatmanager** aus.
6. Wählen Sie im Menü **Serviceinstanz** eine {{site.data.keyword.cloudcerts_short}}-Instanz aus oder verwenden Sie den Standardwert `Alle Instanzen`.
7. (Optional) Konfigurieren Sie den Zugriff auf ein bestimmtes Zertifikat:
    1. [Rufen Sie die Zertifikats-ID ab](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#get-certificate-id).
    2. Geben Sie `certificate` im Feld **Ressourcentyp** ein.
    3. Geben Sie die Zertifikats-ID im Feld **Ressourcen-ID** ein.
8. Weisen Sie dem Benutzer eine [Plattformzugriffsrolle](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#platform-access-roles) zu.
9. Weisen Sie dem Benutzer eine [Servicezugriffsrolle](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#service-access-roles) zu.
10. Klicken Sie auf **Zuweisen**, um dem Benutzer die Zugriffsrichtlinie zuzuweisen.

**Beispiele für die Rollenzuordnung**

* Jedem Benutzer mindestens die Rolle eines Anzeigeberechtigten zuweisen, sodass jeder Benutzer Serviceinstanzen anzeigen kann.
* Einem Benutzer die Rolle eines Administrators oder Bearbeiters zuweisen, falls dieser Benutzer Instanzen erstellen und löschen soll.
* Einem Benutzer mindestens die Rolle eines Leseberechtigten zuweisen, falls dieser Benutzer Zertifikate innerhalb einer Instanz anzeigen soll.

### ID eines Zertifikats abrufen
{: #get-certificate-id}

Führen Sie die folgenden Schritte aus, um die ID eines Zertifikats abzurufen:

1. Wählen Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard Ihre {{site.data.keyword.cloudcerts_short}}-Instanz aus.
2. Wählen Sie im Navigationsbereich der Servicedetailseite **Verwalten** aus.
3. Wählen Sie ein Zertifikat aus.
4. Suchen Sie in den Zertifikatsdetails den Zertifikats-CRN.
5. Kopieren Sie die Zertifikats-ID. Der CRN enthält verschiedene Werte, die durch einen Doppelpunkt (`:`) voneinander getrennt sind. Die Zertifikats-ID ist der letzte Wert im CRN, z. B. `e20cb664efcbfa2c2f57801230d246a6`.

---

copyright:
  years: 2017
lastupdated: "2017-12-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Produktinformation
{: #about-cloud-certs}

Im Folgenden finden Sie Informationen zu {{site.data.keyword.cloudcerts_full}}.

## Was ist {{site.data.keyword.cloudcerts_short}}?
{: #what-is-cloud-certs}

{{site.data.keyword.cloudcerts_short}} unterstützt Sie bei der Verwaltung der SSL-Zertifikate für Ihre {{site.data.keyword.IBM_notm}} Cloud-basierten Apps und Services.
{: shortdesc}

Sie können SSL-Zertifikate, die Sie von Ihren Apps und Services empfangen, importieren und sicher speichern und Sie erhalten eine zentrale Übersicht über die Zertifikate, die Sie verwenden.

Sie können Ihre Zertifikate auf folgende Art und Weise verwalten:

* Ablaufdaten Ihrer Zertifikate überwachen, um sicherzustellen, dass Sie sie rechtzeitig verlängern
* Zertifikatstypen über verschiedene Bereitstellungen hinweg anzeigen und die Einhaltung der Richtlinien der Organisation sicherstellen
* Zertifikate suchen, die ersetzt werden müssen, wenn neue Konformitäts- und Sicherheitsanforderungen in Kraft treten
* Mechanismen einrichten, die steuern, wer auf Ihre Zertifikate zugreifen und wer sie verwalten kann

## Verfügbarkeit
{: #availability}

{{site.data.keyword.cloudcerts_short}} steht nur in er Region 'Vereinigte Staaten (Süden)' zur Verfügung. 

## Schutz privater Schlüssel
{: #private-key-security}

Wenn Sie ein Zertifikat und den entsprechenden privaten Schlüssel in {{site.data.keyword.cloudcerts_short}} importieren, verwendet der Service einen AES 256-Algorithmus zum Verschlüsseln des privaten Schlüssels (AES = Advanced Encryption Standard). {{site.data.keyword.cloudcerts_short}} speichert diesen eindeutigen verschlüsselten Schlüssel zur Verwendung mit Ihrer Serviceinstanz.

## Identitäts- und Zugriffsmanagement
{: #identity-access-management}

Sie können Services in {{site.data.keyword.Bluemix_notm}} dadurch schützen, dass bestimmten Aktionen nur von Benutzern ausgeführt werden können, die bestimmte Rollen haben.
{: shortdesc}

<table>
<caption> Tabelle 1. Aktionen, die Benutzerrollen zugeordnet werden</caption>
  <tr>
    <th> Aktion </th>
    <th> Rolle </th>
  </tr>
  <tr>
    <td>Zertifikate auflisten</td>
    <td> Administrator, Operator, Bearbeiter, Anzeigeberechtigter</td>
  </tr>
  <tr>
    <td>Zertifikat und privaten Schlüssel herunterladen</td>
    <td> Administrator, Operator </td>
  </tr>
  <tr>
    <td>Zertifikatsdaten aktualisieren</td>
    <td> Administrator, Bearbeiter</td>
  </tr>
  <tr>
    <td>Zertifikate, private Schlüssel und Zwischenzertifikate hochladen</td>
    <td> Administrator, Bearbeiter</td>
  </tr>
  <tr>
    <td>Zertifikat und privaten Schlüssel löschen</td>
    <td> Administrator, Bearbeiter</td>
  </tr>
</table>

Weitere Informationen zu Benutzerrollen und Berechtigungen finden Sie unter [Benutzerrollen](/docs/admin/patterns.html#userroles).

### Benutzerrollen zuweisen
{: #assigning-user-roles}

Führen Sie die folgenden Schritte aus, um eine Benutzerrolle auf der Konto- oder Ressourcengruppenebene zuzuweisen.
Wenn der Benutzer nicht Teil Ihrer Organisation ist, senden Sie zunächst eine Einladung an den Benutzer.

1. Wechseln Sie zu **Verwalten > Konto > Benutzer**.
2. Wählen Sie **Richtlinie zuweisen** im Menü **Aktionen** aus.
3. Klicken Sie auf **Zugriff auf Ressourcen zuweisen** oder **Zugriff in einer Ressourcengruppe zuweisen**.
4. Wählen Sie **Certificate Manager** unter **Services** aus.
5. Optional: Wählen Sie eine **Region** oder den Standardwert **Alle Regionen** aus.
6. Optional: Wählen Sie eine **Serviceinstanz** oder den Standardwert **Alle Instanzen** aus.
7. Wählen Sie unter **Rollen auswählen > Zugriffsrollen für Plattform zuweisen** die gewünschte Zugriffsebene aus.

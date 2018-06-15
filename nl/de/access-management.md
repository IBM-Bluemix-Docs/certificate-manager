---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Zugriffsrollen für den Service verwalten
{: #managing-service-access-roles}

Sie können Services in {{site.data.keyword.Bluemix_notm}} dadurch schützen, dass bestimmten Aktionen nur von Benutzern ausgeführt werden können, die bestimmte Zugriffsrollen haben.
{: shortdesc}

### Zugriffsrollen für die Plattform
{: #platform-access-roles}

Mithilfe von Plattformzugriffsrollen können Sie es Benutzern ermöglichen, Aufgaben für Plattformressourcen durchzuführen, wie z. B. das Erstellen und Löschen von Instanzen in Ihrem IBM Cloud-Konto.

<table>
<caption> Tabelle 1. Aktionen, die Plattformzugriffsrollen zugeordnet werden</caption>
  <tr>
    <th> Aktion </th>
    <th> Rolle </th>
  </tr>
  <tr>
    <td>Certificate Manager-Instanzen anzeigen</td>
    <td> Administrator, Operator, Bearbeiter, Anzeigeberechtigter </td>
  </tr>
  <tr>
    <td>Certificate Manager-Instanz erstellen</td>
    <td> Administrator, Bearbeiter </td>
  </tr>
  <tr>
    <td>Certificate Manager-Instanz löschen</td>
    <td> Administrator, Bearbeiter </td>
  </tr>
</table>

Traditionell ermöglichen Plattformrollen auch den Zugriff auf bestimmte Aktionen für Zertifikate innerhalb von Instanzen. Diese Definition ist veraltet und wird in naher Zukunft entfernt.

### Zugriffsrollen für den Service
{: #service-acceess-roles}

Mithilfe von Servicezugriffsrollen können Sie es Benutzern ermöglichen, Aufgaben in Certificate Manager-Instanzen durchzuführen, wie z. B. das Importieren, Herunterladen, Bearbeiten oder Löschen von Zertifikaten.

<table>
<caption> Tabelle 1. Aktionen, die Servicezugriffsrollen zugeordnet werden</caption>
  <tr>
    <th> Aktion </th>
    <th> Rolle </th>
  </tr>
  <tr>
    <td>Zertifikate auflisten</td>
    <td> Manager, Schreibberechtigter, Leseberechtigter</td>
  </tr>
  <tr>
    <td>Zertifikat und privaten Schlüssel herunterladen </td>
    <td> Manager, Schreibberechtigter </td>
  </tr>
  <tr>
    <td>Zertifikatsdaten aktualisieren</td>
    <td> Manager, Schreibberechtigter </td>
  </tr>
  <tr>
    <td>Zertifikate, private Schlüssel und Zwischenzertifikate hochladen </td>
    <td> Manager  </td>
  </tr>
  <tr>
    <td>Zertifikat und privaten Schlüssel löschen </td>
    <td> Manager </td>
  </tr>
</table>


Weitere Informationen zu Benutzerrollen und Berechtigungen finden Sie unter [Benutzerrollen](/docs/iam/users_roles.html#userroles).

### Benutzerzugriffsrollen zuweisen
{: #assigning-user--access-roles}

Führen Sie die folgenden Schritte aus, um eine Zugriffsrolle auf der Konto- oder Ressourcengruppenebene zuzuweisen.
Wenn der Benutzer nicht Teil Ihrer Organisation ist, senden Sie zunächst eine Einladung an den Benutzer.

1. Wechseln Sie zu **Verwalten > Konto > Benutzer**.
2. Wählen Sie **Richtlinie zuweisen** im Menü **Aktionen** aus.
3. Klicken Sie auf **Zugriff auf Ressourcen zuweisen** oder **Zugriff in einer Ressourcengruppe zuweisen**.
4. Wählen Sie **Certificate Manager** unter **Services** aus.
5. Optional: Wählen Sie eine **Region** oder den Standardwert **Alle Regionen** aus.
6. Optional: Wählen Sie eine **Serviceinstanz** oder den Standardwert **Alle Instanzen** aus.
7. Wählen Sie unter **Rollen auswählen > Zugriffsrollen für Plattform/Service zuweisen** die gewünschte Zugriffsebene aus.

**Beispiele:**
* Jedem Benutzer mindestens die Rolle eines Anzeigeberechtigten zuweisen, sodass jeder Benutzer Serviceinstanzen anzeigen kann. 
* Einem Benutzer die Rolle eines Administrators oder Bearbeiters zuweisen, falls dieser Benutzer Instanzen erstellen soll. 
* Einem Benutzer mindestens die Rolle eines Leseberechtigten zuweisen, falls dieser Benutzer Zertifikate innerhalb einer Instanz anzeigen soll.

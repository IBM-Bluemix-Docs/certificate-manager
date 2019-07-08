---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-15"

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

# Lernprogramm zur Einführung
{: #getting-started}

{{site.data.keyword.cloudcerts_full}} unterstützt Sie beim Abrufen, Speichern und Verwalten von SSL-Zertifikaten für Ihre cloudbasierten {{site.data.keyword.IBM_notm}} Apps.  
Erstellen Sie zunächst eine neue {{site.data.keyword.cloudcerts_short}}-Serviceinstanz, indem Sie die folgenden Schritte ausführen.
{: shortdesc}

Gehen Sie wie folgt vor, um eine Instanz über die {{site.data.keyword.cloud_notm}}-Konsole zu erstellen:

1.	Wählen Sie **{{site.data.keyword.cloudcerts_short}}** im {{site.data.keyword.cloud_notm}}-Katalog aus.
2.	Geben Sie Ihrer Serviceinstanz einen Namen oder verwenden Sie den voreingestellten Namen.
3.	Klicken Sie auf **Erstellen**.
4.	Um die Zertifikate Ihrer Organisation in **{{site.data.keyword.cloudcerts_short}}** zu importieren, klicken Sie auf **Zertifikat importieren**.
5.	Um ein neues Zertifikat zu bestellen, klicken Sie auf **Zertifikat bestellen**.

<br/>
Gehen Sie wie folgt vor, um eine Instanz über die [{{site.data.keyword.cloud_notm}}-CLI](https://cloud.ibm.com/docs/cli?topic=cloud-cli-ibmcloud-cli) zu erstellen:

1. Melden Sie sich bei {{site.data.keyword.cloud_notm}} an und folgen Sie den Anweisungen auf dem Bildschirm.

   ```
   ibmcloud login
   ```

2. Erstellen Sie eine Instanz.

   ```
   ibmcloud resource service-instance-create "Meine Zertifikatmanager-Instanz" cloudcerts free us-south
   ```

   - Ersetzen Sie **Meine Zertifikatmanager-Instanz** durch den entsprechenden Instanznamen.
   - Ersetzen Sie **us-south** entweder durch **us-south** (Dallas), **eu-gb** (London), **eu-de** (Frankfurt) oder **jp-tok** (Tokio).

<br/>
[Erfahren Sie mehr ](/docs/services/certificate-manager?topic=certificate-manager-about-certificate-manager#about-certificate-manager) zu den Vorteilen von {{site.data.keyword.cloudcerts_short}} und [ zur Bereitstellung von Benutzerfeedback in {{site.data.keyword.IBM_notm}} Developer](/docs/services/certificate-manager?topic=certificate-manager-troubleshooting#getting-help-and-support), um zur Entwicklung und Verbesserung von {{site.data.keyword.cloudcerts_short}} beizutragen. Informationen zu den Neuerungen im Service finden Sie unter [Releaseinformationen](/docs/services/certificate-manager?topic=certificate-manager-release-notes#release-notes).
{: note}

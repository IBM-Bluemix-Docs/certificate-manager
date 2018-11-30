---

copyright:
  years: 2018
lastupdated: "2018-11-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Releaseinformationen
{: #release-notes}

Für den {{site.data.keyword.cloudcerts_long}}-Service stehen die folgenden Features und Änderungen zur Verfügung.

## 14. November 2018
{: 14November2018}

- **Erneut importieren**  
  Sie können ein Zertifikat aktualisieren, indem Sie eine neue Version mit derselben Domäne wie das vorhandene Zertifikat, jedoch einem neuen Ablaufdatum, importieren. Beim erneuten Importieren eines Zertifikats wird die vorhandene Version des Zertifikats als Sicherungskopie beibehalten. Weitere Informationen finden Sie in [Zertifikat erneut importieren](/docs/services/certificate-manager/managing-certificates.html#reimport-certificate).

- **1000 Zertifikate pro Instanz**  
  Es können bis zu 1000 Zertifikate pro Instanz importiert werden.

## 28. Oktober 2018
{: 28October2018}

- **Ankündigungsbanner**  
  Serviceankündigungen, z. B. zu nicht mehr verwendeten APIs, werden auf der Registerkarte **Verwalten** angezeigt.

## 12. September 2018
{: 12September2018}

- **Der Zertifikatsname ist obligatorisch**  
  Beim Importieren eines Zertifikats muss ein Wert für den Namen des Zertifikats angegeben werden.  

- **Nicht mehr verwendete APIs**  
  Die in Version 2 vorhandenen APIs **Zertifikat importieren** und **Metadaten eines Zertifikats aktualisieren** werden nicht mehr unterstützt und werden am 1. Dezember 2018 entfernt. Führen Sie ein Upgrade auf die APIs der Version 3 durch. Weitere Informationen finden Sie in der [API-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/apidocs/certificate-manager).

- **Slack-Benachrichtigungen werden gruppiert**  
  Die Benachrichtigungen in Slack werden nach ihrem Ablaufdatum gruppiert.

## 02. September 2018
{: 2September2018}

- **Allgemeine Verfügbarkeit (GA) von {{site.data.keyword.cloudcerts_long_notm}}**  
  Der {{site.data.keyword.cloudcerts_short}}-Service ist in {{site.data.keyword.cloud_notm}} allgemein verfügbar.

## 22. August 2018
{: 22August2018}

- **Live-Unterstützung am Standort London**  
  Die Betaversion von {{site.data.keyword.cloudcerts_long_notm}} ist am Standort London verfügbar.

## 15. August 2018
{: 15August2018}

- **Nicht mehr verwendete APIs der Version 1 entfernt**  
  APIs der Version 1 sind nicht mehr verfügbar. Falls Sie Ihre API noch nicht aktualisiert haben, nehmen Sie die Aktualisierung so bald wie möglich vor. Weitere Informationen finden Sie in der [API-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/apidocs/).

- **Plattformrollen durch Servicerollen ersetzt**  
  Der Zugriff auf {{site.data.keyword.cloudcerts_short}}-Instanzen kann mithilfe von Servicerollen gesteuert werden. [Weitere Informationen zum Zugriffsmanagement finden Sie hier](access-management.html).

## 12. Juli 2018
{: 12July2018}

- **Callback-Benachrichtigungen**  
  Callback-Unterstützung für Benachrichtigungen wurde hinzugefügt. Sie können Benachrichtigungen entweder an Slack senden oder eine beliebige Callback-URL verwenden, um Benachrichtigungen zu posten. So können Sie zum Beispiel Benachrichtigungen an PagerDuty senden, automatisch eine Problemmeldung in GitHub öffnen oder Verlängerungsscripts auslösen. [Weitere Informationen zu Benachrichtigungen finden Sie hier](notifications-dashboard.html).

## 12. Juni 2018
{: 12June2018}

- **Slack-Benachrichtigungen**  
  Slack-Benachrichtigungen wurden hinzugefügt, um Sie rechtzeitig über ablaufende Zertifikate zu informieren. [Weitere Informationen zu Benachrichtigungen finden Sie hier](notifications-dashboard.html).

## 8. Januar 2018
{: 8January2018}

- **Nicht mehr verwendete APIs**  
  APIs der Version 1 werden nicht mehr verwendet und am 8. September 2018 entfernt. Führen Sie ein Upgrade auf die APIs der Version 2 durch. Weitere Informationen finden Sie in der [API-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/apidocs/certificate-manager).

## 19. Dezember 2017
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} als Betaservice verfügbar**  
  Der {{site.data.keyword.cloudcerts_short}}-Service ist als Betaservice in {{site.data.keyword.cloud_notm}} verfügbar.

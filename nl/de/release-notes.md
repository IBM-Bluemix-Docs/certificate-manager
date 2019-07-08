---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-10"

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

# Releaseinformationen
{: #release-notes}

Für den {{site.data.keyword.cloudcerts_long}}-Service stehen die folgenden Features und Änderungen zur Verfügung.


## 10. Juni 2019
{: 10June2019}

- **Bestellte "Let's Encrypt"-Zertifikate verlängern**  
  Jetzt können Sie "Let's Encrypt"-Zertifikate verlängern, die Sie mit {{site.data.keyword.cloudcerts_short}} bestellt haben. [Weitere Informationen zum Bestellen von Zertifikaten](/docs/services/certificate-manager?topic=certificate-manager-order-certificates).


## 6. Mai 2019
{: 6May2019}

- **"Let's Encrypt"-Zertifikate bestellen**  
  Sie können jetzt "Let's Encrypt"-Zertifikat bestellen. [Weitere Informationen zum Bestellen von Zertifikaten](/docs/services/certificate-manager?topic=certificate-manager-order-certificates).

## 18. Februar 2019
{: 18February2019}

- **Live-Unterstützung am Standort Tokio**  
  {{site.data.keyword.cloudcerts_long_notm}} ist am Standort Tokio verfügbar.

## 13. Januar 2019
{: 13January2019}
- **Callback-Nutzdaten - Version 3**  
  [Informationen finden Sie in der API-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/certificate-manager).

## 6. Januar 2019
{: 6January2019}
- **Nicht mehr verwendete APIs**  
  Die APIs der Version 2 **List certificates** und **Search certificates repository** werden nicht mehr verwendet und irgendwann entfernt. Führen Sie ein Upgrade auf die APIs der Version 3 durch. Weitere Informationen finden Sie in der [API-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/certificate-manager).

## 9. Dezember 2018
{: 9December2018}
- **Zusätzliche Zertifikatsformate**    
{{site.data.keyword.cloudcerts_short}} unterstützt die folgenden Zertifikatsformate: RSA, DSA, ECDSA, ECDH.

## 5. Dezember 2018
{: 5December2018}
- **Benachrichtigung über erneuten Import**    
Beim erneuten Import eines verlängerten Zertifikats für ein ablaufendes Zertifikat erhalten Sie eine Benachrichtigung darüber, dass das Zertifikat erneut importiert wurde. Sie und Ihr Team werden so daran erinnert, dass das verlängerte Zertifikat bei SSL/TLS-Abschlusspunkten bereitgestellt werden muss. Diese Benachrichtigung ist nur für neu erstellte Benachrichtigungskanäle möglich.

- **{{site.data.keyword.cloudcerts_short}} ist am Standort Frankfurt verfügbar.**     
Der Service ist mit den EU-Richtlinien konform.

## 2. Dezember 2018
{: 2December2018}
- **Callback- und Slack-Nutzdaten - Version 2**  
  [Informationen finden Sie in der API-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/certificate-manager).

## 14. November 2018
{: 14November2018}

- **Erneut importieren**  
  Sie können ein Zertifikat aktualisieren, indem Sie eine neue Version mit derselben Domäne wie das vorhandene Zertifikat, jedoch einem neuen Ablaufdatum, importieren. Beim erneuten Importieren eines Zertifikats wird die vorhandene Version des Zertifikats als Sicherungskopie beibehalten. Weitere Informationen finden Sie in [Zertifikat erneut importieren](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate).

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
  Die in Version 2 vorhandenen APIs **Zertifikat importieren** und **Metadaten eines Zertifikats aktualisieren** werden nicht mehr unterstützt und werden am 1. Dezember 2018 entfernt. Führen Sie ein Upgrade auf die APIs der Version 3 durch. Weitere Informationen finden Sie in der [API-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/certificate-manager).

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
  APIs der Version 1 sind nicht mehr verfügbar. Falls Sie Ihre API noch nicht aktualisiert haben, nehmen Sie die Aktualisierung so bald wie möglich vor. Weitere Informationen finden Sie in der [API-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/).

- **Plattformrollen durch Servicerollen ersetzt**  
  Der Zugriff auf {{site.data.keyword.cloudcerts_short}}-Instanzen kann mithilfe von Servicerollen gesteuert werden. [Weitere Informationen zum Zugriffsmanagement finden Sie hier](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles).

## 12. Juli 2018
{: 12July2018}

- **Callback-Benachrichtigungen**  
  Callback-Unterstützung für Benachrichtigungen wurde hinzugefügt. Sie können Benachrichtigungen entweder an Slack senden oder eine beliebige Callback-URL verwenden, um Benachrichtigungen zu posten. So können Sie zum Beispiel Benachrichtigungen an PagerDuty senden, automatisch eine Problemmeldung in GitHub öffnen oder Verlängerungsscripts auslösen. [Weitere Informationen zu Benachrichtigungen finden Sie hier](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#callback).

## 12. Juni 2018
{: 12June2018}

- **Slack-Benachrichtigungen**  
  Slack-Benachrichtigungen wurden hinzugefügt, um Sie rechtzeitig über ablaufende Zertifikate zu informieren. [Weitere Informationen zu Benachrichtigungen finden Sie hier](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#setup-callback).

## 8. Januar 2018
{: 8January2018}

- **Nicht mehr verwendete APIs**  
  APIs der Version 1 werden nicht mehr verwendet und am 8. September 2018 entfernt. Führen Sie ein Upgrade auf die APIs der Version 2 durch. Weitere Informationen finden Sie in der [API-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/certificate-manager).

## 19. Dezember 2017
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} als Betaservice verfügbar**  
  Der {{site.data.keyword.cloudcerts_short}}-Service ist als Betaservice in {{site.data.keyword.cloud_notm}} verfügbar.

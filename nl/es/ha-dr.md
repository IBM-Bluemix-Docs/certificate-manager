---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-13"

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

# Alta disponibilidad y recuperación tras desastre
{: #ha-dr}

Alta disponibilidad y recuperación en caso de error para {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

* El servicio {{site.data.keyword.cloudcerts_short}} es un servicio regional de alta disponibilidad. En cada ubicación soportada, el servicio se presenta en varias zonas de disponibilidad sin puntos de anomalía.
* Se realiza una copia de seguridad diaria de los datos almacenados en la base de datos de {{site.data.keyword.cloudcerts_short}}. Si es necesario la recuperación de una ubicación, los datos están disponibles para ser restaurados.

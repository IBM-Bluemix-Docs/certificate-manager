---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL, 

subcollection: certificate-manager

---

{:external: target="_blank" .external}
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

# Haute disponibilité et reprise après incident
{: #ha-dr}

Haute disponibilité et reprise après incident pour {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

* Le service {{site.data.keyword.cloudcerts_short}} est un service régional, à haute disponibilité. Dans chaque emplacement pris en charge, le service existe dans des zones de disponibilité multiples, sans point de défaillance unique.
* Les données qui sont stockées dans la base de données {{site.data.keyword.cloudcerts_short}} font l'objet d'une sauvegarde quotidienne. Si le rétablissement d'un emplacement est nécessaire, les données sont disponibles pour restauration.

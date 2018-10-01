---

copyright:
  years: 2018,
lastupdated: "2018-10-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Frequently asked questions (FAQs)
{: #faq}

Frequently asked questions about {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

## What type of certificates can I store in {{site.data.keyword.cloudcerts_short}}?
{: #supported-certificate-types}

{{site.data.keyword.cloudcerts_short}} supports PEM formatted certificates only.

## Can I upload password-protected private keys?
{: #password-protected-private-keys}

{{site.data.keyword.cloudcerts_short}} does not support importing certificates with password-protected private keys.

## Can I receive email notifications for expiring certificates?
{: #email-notifications}

Callback and Slack notifications only are supported.

## Can I version control my certificates?
{: #certificate-versioning}

You cannot re-import or change the version a certificate. Instead, you can import another copy of the certificate, with a renewed expiration date.

## Can I make specific certificates visible only to specific users?
{: #access-policies}

Certificates can be protected by using IAM access policies to achieve granular access control, see [Managing service access roles](access-management.html).

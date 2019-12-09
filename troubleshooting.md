---

copyright:
  years: 2017, 2019
lastupdated: "2019-12-09"

keywords: certificates, ssl, tls, private key, support, help, error

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:troubleshoot: data-hd-content-type='troubleshoot'} 
{:support: data-reuse='support'}

# Troubleshooting
{: #troubleshooting}

If you have problems when you are using {{site.data.keyword.cloudcerts_full}}, consider these techniques for troubleshooting and getting help.
{: shortdesc}

## Getting help and support
{: #getting-help-and-support}



You can get help in the following ways:

- By searching for information in this documentation site
- By asking questions through a forum
- You can also open a support ticket.

When you are using the forums to ask a question, be sure to tag your question so that it is seen by the {{site.data.keyword.cloudcerts_full_notm}} development team.

- If you have technical questions about the service, post your question on [Stack Overflow](https://stackoverflow.com/search?q=ibm-certificate-manager+ibm-cloud){: external} and tag your question with `ibm-cloud` and `ibm-certificate-manager`.  
- For questions about the service and getting started instructions, post your question on [IBM Developer Answers](https://developer.ibm.com/answers){: external}. Include the `ibm-certificate-manager` and `ibm-cloud` tags.

For more information about opening a support ticket or support levels and ticket severities, see [how do I get the support that I need?](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support)




## I receive an error when I try to upload a certificate and private key 
{: #import-cert-private-key}
{: troubleshoot} 
{: support}

{: tsSymptoms}
You're trying to upload a certificate and private key but receive the following error message.

```
The private key doesn't match the certificate that you're trying to import. Ensure that they match and try again.
```
{: screen}

{: tsCauses}
The private key might be encrypted or the certificate and key might not be a match.

{: tsResolve}
Depending on whether your private key is encrypted, choose one of the following options:

* The private key is encrypted. Make sure that you decrypt the private key before you upload it.

   ```
   openssl rsa -in [file1.key] -out [file2.key]
   ```
   {: codeblock}

* The private key is not encrypted. Make sure the certificate and the private key match by comparing the results of the following command, where `<certificate-file>` is the name of your certificate file and `<key-file>` is the name of your private key file:

   ```
   openssl x509 -modulus -noout -in <certificate-file>.pem | openssl md5; openssl rsa -modulus -noout -in <key-file>.key | openssl md5
   ```
   {: codeblock}



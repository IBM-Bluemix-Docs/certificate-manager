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

# 시작하기 튜토리얼
{: #getting-started}

{{site.data.keyword.cloudcerts_full}}는 {{site.data.keyword.cloud_notm}} 기반 앱에 대한 SSL 인증서를 얻고, 저장하고, 관리하는 데 도움이 됩니다.  
다음 단계를 완료하여 새 {{site.data.keyword.cloudcerts_short}} 서비스 인스턴스를 작성하여 시작하십시오.
{: shortdesc}

{{site.data.keyword.cloud_notm}} 콘솔에서 인스턴스를 작성하려면 다음을 수행하십시오.

1.	{{site.data.keyword.cloud_notm}} 카탈로그에서 **{{site.data.keyword.cloudcerts_short}}**를 선택하십시오.
2.	서비스 인스턴스에 이름을 제공하거나 사전 설정된 이름을 사용하십시오.
3.	**작성**을 클릭하십시오.
4.	조직의 인증서를 **{{site.data.keyword.cloudcerts_short}}**에 가져오려면 **인증서 가져오기**를 클릭하십시오.
5.	새 인증서를 주문하려면 **인증서 주문**을 클릭하십시오.

<br/>
[{{site.data.keyword.cloud_notm}} CLI](https://cloud.ibm.com/docs/cli?topic=cloud-cli-ibmcloud-cli)에서 인스턴스를 작성하려면 다음을 수행하십시오.

1. {{site.data.keyword.cloud_notm}}에 로그인한 후 화면의 지시사항에 따르십시오.

   ```
   ibmcloud login
   ```

2. 인스턴스를 작성하십시오.

   ```
   ibmcloud resource service-instance-create "My Certificate Manager instance" cloudcerts free us-south
   ```

   - **My Certificate Manager instance**를 선택한 인스턴스 이름으로 바꾸십시오.
   - **us-south**를 **us-south**(댈러스), **eu-gb**(런던), **eu-de**(프랑크푸르트) 또는 **jp-tok**(도쿄)로 바꾸십시오.

<br/>
또한 {{site.data.keyword.cloudcerts_short}}에서 얻은 내용에 대해 [자세히 알아보고](/docs/services/certificate-manager?topic=certificate-manager-about-certificate-manager#about-certificate-manager) [{{site.data.keyword.IBM_notm}} Developer에 사용자 피드백을 제공하여](/docs/services/certificate-manager?topic=certificate-manager-troubleshooting#getting-help-and-support) {{site.data.keyword.cloudcerts_short}}가 개발됨에 따라 이를 향상시킬 수 있습니다. 서비스의 새로운 기능에 대해 알아보려면 [릴리스 정보](/docs/services/certificate-manager?topic=certificate-manager-release-notes#release-notes)를 참조하십시오.
{: note}

---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-21"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Certificate Manager 정보
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_short}}는 {{site.data.keyword.IBM_notm}} 클라우드 기반 앱 및 서비스에 대한 SSL 인증서를 관리하는 데 도움을 줍니다.
{: shortdesc}

앱 및 서비스에 대해 얻은 SSL 인증서를 가져와서 안전하게 저장하고 사용 중인 인증서를 중앙에서 볼 수 있습니다.

다음과 같은 방법으로 인증서를 관리할 수 있습니다.

* 제시간에 인증서를 갱신하는지 확인하도록 인증서가 만료되기 전에 알림을 받습니다.
* 배치에서 인증서의 유형을 보고 인증서가 조직 정책을 충족하는지 확인합니다.
* 새로운 준수 또는 보안 요구사항이 발행될 때 대체해야 하는 인증서를 찾습니다.
* 인증서에 액세스하고 인증서를 관리할 수 있는 사용자에 대한 제어를 설정합니다.

## 개인 키 보안
{: #private-key-security}

인증서와 해당 개인 키를 {{site.data.keyword.cloudcerts_short}}로 가져올 때 서비스에서 고급 암호화 표준(AES) 256 알고리즘을 사용하여 개인 키를 암호화합니다. {{site.data.keyword.cloudcerts_short}}가 서비스 인스턴스에 사용하도록 이 암호화된 고유 키를 저장합니다.

## 가용성
{: #availability}

{{site.data.keyword.cloudcerts_short}}는 미국 남부 지역에서만 사용할 수 있습니다.

## 통합
{: #integrations}
<table>
<caption> 표 1. Certificate Manager를 사용하는 IBM Cloud 서비스</caption>
  <tr>
    <th> 서비스 </th>
    <th> 설명 </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>Certificate Manager에서 Kubernetes 클러스터 사용자 정의 도메인 인증서를 저장한 다음 [Kubernetes 서비스 플러그인 명령](/docs/containers/cs_cli_reference.html)을 사용하여 IBM Cloud CLI에 배치하십시오. [이 통합을 자세히 보십시오](https://www.ibm.com/blogs/bluemix/2018/01/use-ibm-cloud-certificate-manager-ibm-cloud-container-service-deploy-custom-domain-tls-certificates/).</td>
  </tr>
  <tr>
    <td>IBM Cloud Security Advisor</td>
    <td>Security Advisor는 IBM Cloud 계정의 Certificate Manager 인스턴스에 만료되거나 만료 예정인 인증서 표시를 포함한 IBM Cloud 서비스의 인사이트를 중앙에서 관리합니다. [Security Advisor에 대해 자세히 보십시오](/docs/services/security-advisor/index.html#index).</td>
  </tr><tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>{{site.data.keyword.cloudaccesstrailfull}} 서비스를 사용하여 {{site.data.keyword.Bluemix}}에서 사용자 및 애플리케이션이 {{site.data.keyword.cloudcerts_long}} 서비스와 상호 작용하는 방식을 추적하십시오. [{{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla)에 대해 자세히 알아보십시오.
    <p>이벤트를 생성하는 조치의 목록을 가져오려면 [{{site.data.keyword.cloudaccesstrailshort}} 이벤트](/docs/services/certificate-manager/at_events.html#at_events)를 참조하십시오.</p></td>
  </tr>
</table>

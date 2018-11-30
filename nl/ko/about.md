---

copyright:
  years: 2017, 2018
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
# {{site.data.keyword.cloudcerts_short}} 정보
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_long}}는 {{site.data.keyword.IBM_notm}} 클라우드 기반 앱 및 서비스에 대한 SSL 인증서를 관리하는 데 도움을 줍니다.
{: shortdesc}

앱 및 서비스에 대해 얻은 SSL 인증서를 가져와서 안전하게 저장하고 사용 중인 인증서를 중앙에서 볼 수 있습니다.

다음과 같은 방법으로 인증서를 관리할 수 있습니다.

* 제시간에 인증서를 갱신하는지 확인하도록 인증서가 만료되기 전에 알림을 받습니다.
* 배치에서 인증서의 유형을 보고 인증서가 조직 정책을 충족하는지 확인합니다.
* 새로운 준수 또는 보안 요구사항이 발행될 때 대체해야 하는 인증서를 찾습니다.
* 인증서에 액세스하고 인증서를 관리할 수 있는 사용자에 대한 제어를 설정합니다.

![상위 레벨 서비스 아키텍처 다이어그램](images/high-level-architecture.png)
<caption>그림 1. 상위 레벨 서비스 아키텍처. </caption>

## 개인 키 보안
{: #private-key-security}

인증서와 해당 개인 키를 {{site.data.keyword.cloudcerts_short}}로 가져올 때 서비스에서 고급 암호화 표준(AES) 256 알고리즘을 사용하여 개인 키를 암호화합니다. {{site.data.keyword.cloudcerts_short}}가 서비스 인스턴스에 사용하도록 이 암호화된 고유 키를 저장합니다.

## 통합
{: #integrations}

<table>
<caption>표 1. {{site.data.keyword.cloudcerts_short}}를 사용하는 {{site.data.keyword.cloud_notm}} 서비스</caption>
  <tr>
    <th> 서비스 </th>
    <th> 설명 </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>{{site.data.keyword.cloudcerts_short}}에서 Kubernetes 클러스터 사용자 정의 도메인 인증서를 저장한 다음 {{site.data.keyword.cloud_notm}} CLI에 대한 [Kubernetes Service 플러그인 명령](/docs/containers/cs_cli_reference.html)을 사용하여 배치하십시오. [이 통합에 대해 자세히 보기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/blogs/bluemix/2018/01/use-ibm-cloud-certificate-manager-ibm-cloud-container-service-deploy-custom-domain-tls-certificates/).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>{{site.data.keyword.security-advisor_short}}는 {{site.data.keyword.cloud_notm}} 서비스에 대한 정보를 중앙에서 관리합니다. 정보에는 {{site.data.keyword.cloud_notm}} 계정의 {{site.data.keyword.cloudcerts_short}} 인스턴스에 있는 만료된 인증서 및 만료 예정인 인증서의 표시가 포함됩니다. [{{site.data.keyword.security-advisor_short}}에 대해 자세히 알아보십시오](/docs/services/security-advisor/index.html#index).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}} 서비스를 사용하여 {{site.data.keyword.cloud_notm}}에서 사용자 및 애플리케이션이 {{site.data.keyword.cloudcerts_long_notm}} 서비스와 상호 작용하는 방식을 추적하십시오. [{{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla)에 대해 자세히 알아보십시오.
    <p>이벤트를 생성하는 조치의 목록을 가져오려면 [{{site.data.keyword.cloudaccesstrailshort}} 이벤트](/docs/services/certificate-manager/at_events.html#at_events)를 참조하십시오.</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>사용자 정의 도메인 인증서를 {{site.data.keyword.cloudcerts_short}} 서비스에 저장한 후, 인증서 CRN을 사용하여 {{site.data.keyword.apiconnect_short}}의 사용자 정의 도메인과 바인딩하십시오. [{{site.data.keyword.apiconnect_short}}에 대해 자세히 알아보십시오](/docs/api-management/index.html#index).</p></td>
  </tr>
</table>

## 위치
{: #availability}

{{site.data.keyword.cloudcerts_short}}는 댈러스 및 런던에서 사용할 수 있습니다.



## 한계
{: #limits}

인스턴스당 최대 1000개의 인증서를 업로드할 수 있습니다. 

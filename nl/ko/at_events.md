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

# {{site.data.keyword.cloudaccesstrailshort}} 이벤트  
{: #at_events}

{{site.data.keyword.cloudaccesstrailfull}} 서비스를 사용하여 {{site.data.keyword.Bluemix_notm}}에서 사용자 및 애플리케이션이 {{site.data.keyword.cloudcerts_long_notm}} 서비스와 상호 작용하는 방식을 추적하십시오.
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 서비스는 {{site.data.keyword.Bluemix_notm}}에서 서비스의 상태를 변경하는 사용자 시작 활동을 레코드합니다. 추가 정보는 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)의 내용을 참조하십시오. 예를 들어, 인증서를 가져오면 {{site.data.keyword.cloudaccesstrailshort}} 이벤트가 생성됩니다.

다음 표에는 API 메소드가 호출될 때 이벤트를 생성하는 API 메소드가 나열되어 있습니다.

<table>
  <caption>표 1. 이벤트를 생성하는 조치</caption>
  <tr>
    <th>조치</th>
	  <th>설명</th>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.import`</td>
	  <td>인증서를 가져옵니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.reimport`</td>
	  <td>인증서를 다시 가져옵니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.download`</td>
	  <td>인증서를 다운로드합니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.read`</td>
	  <td>인증서를 나열합니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.read`</td>
	  <td>인증서 메타데이터를 나열합니다. 인증서의 세부사항을 표시합니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.search`</td>
	  <td>인증서를 검색합니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.search`</td>
	  <td>인증서 메타데이터를 검색합니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.delete`</td>
	  <td>인증서를 삭제합니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.update`</td>
	  <td>인증서 메타데이터를 업데이트합니다(예: 인증서의 설명 변경).</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels.list`</td>
	  <td>알림 채널을 나열합니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.create`</td>
	  <td>알림 채널을 작성합니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.state`</td>
	  <td>알림 채널을 사용하지 않거나 사용합니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.update`</td>
	  <td>알림 채널의 엔드포인트를 업데이트합니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.delete`</td>
	  <td>알림 채널을 삭제합니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.test`</td>
	  <td>알림 채널을 테스트합니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification.sent`</td>
	  <td>알림 채널 엔드포인트에 알림이 전송되었습니다.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels-publickey.read`</td>
	  <td>공개 키가 요청되었습니다.</td>
  </tr>
</table>

## 이벤트 확인 위치
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} 이벤트는 이벤트가 생성되는 {{site.data.keyword.Bluemix_notm}} 위치에서 사용 가능한 {{site.data.keyword.cloudaccesstrailshort}} **계정 도메인**에서 사용할 수 있습니다.

{{site.data.keyword.cloudaccesstrailshort}} 이벤트는 {{site.data.keyword.cloudcerts_short}} 서비스가 프로비저닝되는 동일한 위치에서 자동으로 {{site.data.keyword.cloudaccesstrailshort}} 서비스에 전달됩니다.

## 추가 정보
{: #info}

*requestData_str* 필드에는 사용자가 읽을 수 있는 인증서의 이름이 포함되어 있습니다.

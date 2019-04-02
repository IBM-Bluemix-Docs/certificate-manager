---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-07"

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

# 알림 구성
{: #configuring-notifications}

인증서는 일반적으로 지정된 시간 동안에만 유효합니다. 사용하는 인증서가 만료되면 앱이 작동 중단될 수 있습니다. 작동 중단이 발생하지 않도록 {{site.data.keyword.cloudcerts_full}}를 구성하여 만료될 예정인 인증서에 대한 알림을 전송하면 제시간에 갱신하도록 안내를 받을 수 있습니다.

만료되는 인증서 대신 인증서의 갱신된 버전을 {{site.data.keyword.cloudcerts_short}}로 다시 가져오면 SSL/TLS 종단점에 이 인증서를 배치하는 것을 잊지 않도록 경보 메시지가 표시됩니다. 다시 가져온 인증서에 대한 이 알림은 [채널 버전 2](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions)의 채널에만 전송됩니다.
{: shortdesc}

**알림을 받는 시기**  
{{site.data.keyword.cloudcerts_full_notm}}에 업로드한 인증서의 만기 날짜에 따라 인증서가 만료되기 90일, 60일, 30일, 10일 및 1일 전에 알림을 받습니다. 또한 만료된 인증서에 대해 매일 알림을 받습니다. 매일 제공되는 알림은 인증서가 만료된 후 첫 날에 시작됩니다.

인증서를 갱신하고 이전 인증서 대신 이 인증서를 {{site.data.keyword.cloudcerts_full_notm}}로 다시 가져와야 알림 전송이 중지됩니다. 인증서를 다시 가져오면 인증서를 다시 가져왔고 이를 다시 배치해야 함을 상기시키는 알림을 받습니다.

**알림을 구성하기 위한 내 옵션**  
Slack 웹훅을 사용하여 Slack에 알림을 전송하거나 원하는 콜백 URL을 사용할 수 있습니다.

## Slack 웹훅 설정
{: #setup-callback}

Slack 웹훅을 설정하려면 다음 단계를 완료하십시오.

1. [Slack](https://slack.com/)에 등록하고 작업공간을 설정하십시오.
2. 알림을 게시할 Slack 채널을 작성하십시오.
3. Slack 채널에 대한 [웹훅을 설정](https://api.slack.com/incoming-webhooks)하십시오.

## 콜백 URL 설정
{: #callback}

팀을 위해 갱신 프로세스를 트리거하려면 콜백 URL을 사용하여 사용하는 도구에 대한 알림을 게시할 수 있습니다. 예를 들어, PagerDuty에 보고서에 대한 알림을 전송하거나, GitHub에서 문제를 자동으로 열거나, 갱신 스크립트를 트리거할 수 있습니다.  
{: shortdesc}

**중요:** 콜백 URL 엔드포인트는 {{site.data.keyword.cloudcerts_short}}와 함께 사용될 다음 요구사항을 충족해야 합니다.
* 엔드포인트는 HTTPS 프로토콜을 사용해야 합니다.
* 엔드포인트는 HTTP 헤더를 요구하면 안 됩니다. 이 요구사항에는 권한 헤더가 포함되어 있습니다.
* 엔드포인트에서는 성공적으로 알림이 전달되었음을 나타내기 위해 `200 OK` 상태 코드를 리턴해야 합니다.

### 알림 형식
{: #notification_format}

콜백 URL로 전송되는 알림은 다음 형식으로 인스턴스 비대칭 키를 사용하여 서명된 JSON 문서입니다.

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

페이로드를 디코딩 및 확인하고 나면 컨텐츠는 [채널 버전에 따른](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions) JSON 문자열입니다.

## 알림 채널 구성
{: #adding-channel}

Slack 웹훅 또는 콜백 URL을 작성한 후 {{site.data.keyword.cloudcerts_short}}에 이를 추가하여 만료되는 인증서와 다시 가져온 인증서에 대한 알림을 받기 시작합니다. {{site.data.keyword.cloudcerts_short}}는 엔드포인트를 암호화하고 안전하게 보관합니다.
{: shortdesc}

알림 채널을 추가하려면 다음 단계를 완료하십시오.

1. 서비스 세부사항 페이지의 탐색에서 **설정**을 클릭하십시오.
2. **알림** 탭을 여십시오.
3. **알림 채널 추가**를 클릭하십시오.
4. 사용할 알림 채널의 유형을 선택하십시오.
5. 알림을 전송할 웹훅 또는 콜백 URL을 입력하십시오.
6. **저장**을 클릭하십시오. 구성의 요약이 표시됩니다.

   **예제 출력**

   <table>
   <caption>표 1. 알림 채널에 대한 정보 </caption>
   <thead>
    <th> 컴포넌트 </th>
    <th> 설명 </th>
   </thead>
   <tbody>
   <tr>
    <td>유형</td>
    <td>알림 채널 유형: <i>Slack</i> 또는 <i>콜백 URL</i></td>
   </tr>
   <tr>
    <td>엔드포인트</td>
    <td>알림이 전송되는 알림 채널 엔드포인트입니다.</td>
   </tr>
   <tr>
    <td>인에이블먼트 전환</td>
    <td>알림 채널 상태입니다. 사용 안함으로 설정되면 알림이 전송되지 않습니다.</td>
   </tr>
   <tr>
    <td>테스트 연결 단추</td>
    <td>테스트 알림을 구성한 채널에 전송합니다. </td>
   </tr>
    <tr>
      <td>점으로 구성된 메뉴</td>
      <td>채널에 수행할 수 있는 사용 가능한 조치: <i>편집</i> 또는 <i>삭제</i></td>
    </tr>
    </tbody>
    </table>

    Slack 웹훅을 저장할 때 {{site.data.keyword.cloudcerts_short}}는 구성한 Slack 채널에 자동으로 확인 알림을 전송합니다. 이 알림을 받았는지 확인하려면 Slack 채널을 검사하십시오.
    {: tip}
7. (선택사항) 더 많은 알림 채널을 추가하려면 단계를 반복하십시오.

## 알림 채널 테스트
{: #testing-channel}

알림 채널이 올바르게 구성되었는지 확인하도록 알림 채널을 테스트할 수 있습니다.
{: shortdesc}

시작하기 전에 [알림 채널을 구성](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel)하십시오.

알림 채널을 테스트하려면 다음 단계를 완료하십시오.

1. 서비스 세부사항 페이지의 탐색에서 **설정**을 클릭하십시오.
2. 알림 채널을 찾고 **테스트 연결**을 클릭하십시오.
3. 구성한 채널에서 알림을 받았는지 확인하십시오.

## 알림 채널 업데이트
{: #updating-channel}

알림 채널 구성을 업데이트하거나, 알림을 사용 또는 사용 안함으로 설정하거나, {{site.data.keyword.cloudcerts_short}}에서 알림 채널을 삭제할 수 있습니다.
{: shortdesc}

시작하기 전에 [알림 채널을 구성](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel)하십시오.

알림 채널을 업데이트하려면 다음 단계를 완료하십시오.

1. 서비스 세부사항 페이지의 탐색에서 **설정**을 클릭하십시오.
2. **알림** 탭을 선택하십시오.
3. 다음 옵션 중에서 선택하십시오.
   * 채널에 대한 알림을 사용 안함 또는 사용으로 설정하려면 스위치를 **사용 안함** 또는 **사용**으로 설정하십시오.
   * 채널에 대한 설정을 업데이트하려면 조치 메뉴에서 **편집**을 선택하십시오.
   * 알림 채널을 삭제하려면 조치 메뉴에서 **삭제**를 선택하십시오.

## 콜백 URL에 대한 HTTP 페이로드 확인
{: #verify-callback}

{{site.data.keyword.cloudcerts_short}}에서 콜백 URL로 전송된 모든 HTTP 페이로드는 비대칭 키 쌍을 사용하여 JWT 표준에 따라 자동으로 서명됩니다.  
{: shortdesc}

모든 {{site.data.keyword.cloudcerts_short}} 인스턴스에 대해 기타 {{site.data.keyword.cloudcerts_short}} 인스턴스에서 공유되지 않는 개인 및 공개 키가 생성됩니다. 개인 키는 HTTP 페이로드를 서명하는 데 사용되고 공개 키를 사용하여 페이로드가 {{site.data.keyword.cloudcerts_short}}로 생성되고 서드파티에 의해 변경되지 않는지 확인할 수 있습니다.

공개 키를 다운로드하려면 다음 단계를 완료하십시오.

1. 서비스 세부사항 페이지의 탐색에서 **설정**을 클릭하십시오.
2. **알림** 탭을 여십시오.
3. **다운로드 키** 단추를 클릭하십시오. 키는 PEM 파일로 다운로드됩니다.

## 채널 버전
{: #channel-versions}

Certificate Manager가 향상됨에 따라 수시로 알림 페이로드 구조의 형식을 수정할 수 있습니다. 역호환성을 보장하기 위해 기존 채널로 전송되는 페이로드는 변경되지 않습니다.   

기존 알림 채널(Slack 또는 콜백 URL)이 있는 경우 새로운 버전의 페이로드를 가져오려면 다음을 수행하십시오.
1. 콜백 URL의 경우 구현 시 새 페이로드를 허용할 수 있는지 확인하십시오.
2. 새 알림 채널을 작성합니다(새 채널은 항상 최신 채널 버전으로 작성됨).
3. 새 채널이 올바르게 작동하는지 테스트하십시오.
4. 이전 채널을 삭제하십시오.

채널 버전은 [API 문서](https://cloud.ibm.com/apidocs/certificate-manager#notification-channel-versions)를 참조하십시오.

## 예제
{: #examples}

* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 1 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/blogs/bluemix/2018/08/use-certificate-manager-avoid-outages-using-callback-urls/)  
   인증서 만료 알림을 위해 GitHub 문제를 작성하는 방법에 대해 알아봅니다.
* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 2 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/blogs/bluemix/2018/10/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2/)  
   인증서 만료 알림을 위해 PagerDuty 인시던트 문제를 작성하는 방법에 대해 알아봅니다.

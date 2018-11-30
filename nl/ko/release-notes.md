---

copyright:
  years: 2018
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

# 릴리스 정보
{: #release-notes}

{{site.data.keyword.cloudcerts_long}} 서비스에 대한 다음 기능 및 변경사항이 사용 가능합니다.

## 2018년 11월 14일
{: 14November2018}

- **다시 가져오기**  
  기존 인증서와 동일한 도메인을 포함하지만 새 만료 날짜가 있는 새 버전을 다시 가져오기하여 인증서를 업데이트할 수 있습니다. 인증서를 다시 가져오면 기존 인증서 버전은 백업으로 유지됩니다. [인증서 다시 가져오기](/docs/services/certificate-manager/managing-certificates.html#reimport-certificate)를 참조하십시오.

- **인스턴스당 1000개 인증서**  
  인스턴스당 최대 1000개 인증서를 가져올 수 있습니다. 

## 2018년 10월 28일
{: 28October2018}

- **공지사항 배너**  
  API 사용 중단 및 기타 뉴스와 같은 서비스 공지사항은 **관리** 탭에 표시됩니다. 

## 2018년 9월 12일
{: 12September2018}

- **인증서 이름이 필수임**  
  인증서를 가져올 때 인증서 이름의 값을 반드시 제공해야 합니다.  

- **더 이상 사용되지 않는 API**  
  **인증서 가져오기** 및 **인증서 메타데이터 업데이트** v2 API는 더 이상 사용되지 않으며 2018년 12월 1일에 제거됩니다. v3 API로 업그레이드해야 합니다. 자세한 정보는 [API 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/apidocs/certificate-manager)를 참조하십시오.

- **그룹화된 Slack 알림**  
  Slack의 알림이 만기 날짜별로 그룹화됩니다.

## 2018년 9월 2일
{: 2September2018}

- **{{site.data.keyword.cloudcerts_long_notm}}는 GA(Generally Available)임**  
  {{site.data.keyword.cloudcerts_short}} 서비스가 {{site.data.keyword.cloud_notm}}에서 GA(Generally Available)입니다.

## 2018년 8월 22일
{: 22August2018}

- **런던에서 사용**  
  {{site.data.keyword.cloudcerts_long_notm}} 베타는 런던 위치에서 사용 가능합니다. 

## 2018년 8월 15일
{: 15August2018}

- **더 이상 사용되지 않는 v1 API 제거**  
  버전 1 API는 더 이상 사용할 수 없습니다. API를 아직 업데이트하지 않은 경우 가능한 한 빨리 업데이트해야 합니다. 자세한 정보는 [API 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/apidocs/)를 참조하십시오.

- **플랫폼 역할이 서비스 역할로 바뀜**  
  서비스 역할을 사용하여 {{site.data.keyword.cloudcerts_short}} 인스턴스에 대한 액세스를 제어할 수 있습니다. [액세스 관리에 대해 자세히 보십시오](access-management.html).

## 2018년 7월 12일
{: 12July2018}

- **콜백 알림**  
  알림에 대한 콜백 지원이 추가되었습니다. Slack으로 알림을 보내거나 콜백 URL을 사용하여 알림을 게시하도록 선택할 수 있습니다. 예를 들어, PagerDuty에 알림을 전송하거나, GitHub에서 문제를 자동으로 열거나, 갱신 스크립트를 트리거할 수 있습니다. [알림에 대해 자세히 보십시오](notifications-dashboard.html).

## 2018년 6월 12일
{: 12June2018}

- **Slack 알림**  
  인증서 만료를 놓치지 않도록 Slack 알림이 추가되었습니다. [알림에 대해 자세히 보십시오](notifications-dashboard.html).

## 2018년 1월 8일
{: 8January2018}

- **더 이상 사용되지 않는 API**  
  버전 1 API는 더 이상 사용되지 않으며 2018년 9월 8일에 제거됩니다. v2 API로 업그레이드해야 합니다. 자세한 정보는 [API 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/apidocs/certificate-manager)를 참조하십시오.

## 2017년 12월 19일
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}}가 베타 서비스로 사용 가능**  
  {{site.data.keyword.cloudcerts_short}} 서비스가 {{site.data.keyword.cloud_notm}}에서 베타 서비스로 사용 가능합니다.

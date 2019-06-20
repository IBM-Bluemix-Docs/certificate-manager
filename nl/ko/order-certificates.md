---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-04"

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

# 인증서 주문
{: #ordering-certificates}

{{site.data.keyword.cloudcerts_long}}를 사용하여 지원되는 외부 인증 기관에서 서명된 앱 및 서비스에 대한 공용 SSL/TLS 인증서를 주문할 수 있습니다. {{site.data.keyword.cloudcerts_short}}를 사용하면 SSL/TLS 개인 키에 대한 추가 보안 이외에 공용 인증서를 쉽게 주문할 수 있습니다. 인증서가 발행된 후 인증서를 통합 서버에 배치하거나 다른 위치에서 사용하도록 다운로드할 수 있습니다.  
{: shortdesc}

인증서를 주문할 때 SSL/TLS에 대한 개인 키가 {{site.data.keyword.cloudcerts_short}}에서 직접 생성되고 안전하게 저장됩니다. 발행된 인증서에 대한 모든 요청 및 액세스는 [액세스 제어](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles)를 통해 관리하고 [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events)를 사용하여 자동으로 감사할 수 있습니다.  

{{site.data.keyword.cloudcerts_short}}는 ACME(Automatic Certificate Management Environment) v2 프로토콜을 ACME 클라이언트로 구현합니다. ACME 프로토콜을 사용하면 사용자 개입 없이 브라우저에서 신뢰된 인증서를 자동으로 얻을 수 있습니다.

## 인증서 특성
{{site.data.keyword.cloudcerts_short}}를 통해 주문된 인증서에는 다음과 같은 특성이 있습니다.

- 무료
- 유효성 기간 - 90일
- 단일 도메인, 다중 도메인(SAN) 또는 와일드카드 인증서
- 도메인의 유효성이 검증됨 - 인증서를 발행하기 전에 인증 기관에서 사용자가 인증서를 요청 중인 도메인을 소유하고 있는지 확인합니다.

EV(Extended Validation) 또는 OV(Organization Validated) 인증서가 필요한 경우 다른 위치에서 얻을 수 있으며 {{site.data.keyword.cloudcerts_short}}로 가져와서 라이프사이클을 관리할 수 있습니다.

## 지원되는 인증 기관
{: #supported-certificate-authorities}

인증 기관(CA)은 디지털 인증서를 발행하는 엔티티입니다. CA는 인증서의 요청자와 인증서에 의존하는 클라이언트 모두에 대한 신뢰할 수 있는 서드파티 역할을 합니다.
{: shortdesc}

### Let's Encrypt
[Let’s Encrypt](https://letsencrypt.org)는 90일 동안 유효한 도메인 유효성 검증 인증서를 제공하는 자동화된 무료 ACME 기반 CA입니다. ISRG(Internet Security Research Group)에서 제공되는 서비스입니다.

## 인증서 주문 설정
{: #setup}

인증서가 사용자에게 발행되기 전에 먼저 {{site.data.keyword.cloudcerts_short}}에서 사용자가 요청에 나열한 모든 도메인을 제어하는지 확인해야 합니다. {{site.data.keyword.cloudcerts_short}}는 DNS 유효성 검증을 사용하여 제어를 확인합니다.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}}는 DNS(Domain Name System) 서비스에 추가할 수 있는 DNS TXT 레코드 양식의 인증 확인을 전송합니다. 인증서에서 요청하는 각 도메인에 대해 별도의 DNS TXT 레코드를 받습니다. DNS TXT 레코드를 추가한 후 {{site.data.keyword.cloudcerts_short}} 및 Let’s Encrypt에서 해당 레코드가 DNS 서비스에 있는지 확인합니다. 인증 확인을 완료하면 {{site.data.keyword.cloudcerts_short}} 인스턴스에 사용할 수 있는 Let’s Encrypt 인증서가 발행됩니다.

{{site.data.keyword.cloudcerts_short}}는 알림 설정에서 제공하는 콜백 URL에 TXT 레코드를 전송하며, 이를 통해 도메인 유효성 검증 프로세스를 쉽게 자동화할 수 있습니다.

인증서 주문을 시작하려면 {{site.data.keyword.cloudcerts_short}}에서 콜백 URL을 알림 채널로 등록하십시오. 그런 다음 TXT 인증 확인을 포함하는 알림 이벤트를 처리하도록 코드를 업데이트하십시오. [콜백 URL 알림 채널을 설정하는 방법을 알아보십시오](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

## 인증 확인에 응답
{: #responding-to-challenge}

알림 채널은 다음과 같은 구조의 알림을 수신합니다.

```javascript
{
"instance_crn: '"<INSTANCE_CRN>"
"certificate_manager_url": "certificate_manager_url",
    "event_type": "cert_domain_validation_required" | "cert_domain_validation_completed", // The first event is for adding the required challenge TXT record and the second is for clearing that same TXT record once the challenge has finished.
    "certificateCRN": "<CERTIFICATE_CRN>", // The ordered certificate CRN
    "userToken": "<USER_TOKEN>", /// The IAM token holding the identity of user who ordered the certificate
    "domain_validation_method": "dns-01", // Specifies the domain validation method, currently only DNS validation is available.
    "domain": "<ORDERED_DOMAIN>", // The requested domain, a different challenge is sent for each domain in the order (primary and each of the alternative domains).
    "challenge": {
        "txt_record_name": "<TXT_REC_NAME>", // TXT record name - usually used with conjunction with the domain.
        "txt_record_val": "<TXT_REC_VALUE>" // TXT record value
    },
    "version": "<CHANNEL_VERSION>" // notification channel version that supports order related notifications - 4 and above
}
```
{: screen}

DNS TXT 인증 확인이 콜백 URL에 전송되면 10분 이내에 인증 확인에 응답해야 합니다. {{site.data.keyword.cloudcerts_short}}가 인증 확인이 완료되었는지 확인합니다. {{site.data.keyword.cloudcerts_short}}에서 사용자가 인증 확인에 응답했음을 확인하면 TXT 레코드를 제거할 수 있음을 알리는 두 번째 알림이 전송됩니다.

인증서 주문에 대한 자주 묻는 질문을 보려면 [FAQ 페이지를 검토](/docs/services/certificate-manager?topic=certificate-manager-faq#faq)하십시오.
{: tip}

## 인증서 주문
{: #ordering-certificate}

1. {{site.data.keyword.cloudcerts_short}}의 관리 탭으로 이동하십시오.
2. **인증서 주문**을 클릭하고 다음 세부사항을 제공하십시오.

    1. 인증서 이름을 제공하십시오.
    2. 인증 기관을 선택하십시오.
    3. 기본 도메인 및 대체 도메인을 입력하십시오.
    4. 적절한 알고리즘 및 키 알고리즘을 선택하십시오.
    5. **주문**을 클릭하십시오.

주문이 **보류** 상태가 됩니다. 도메인 유효성 검증 인증 확인에 응답하고 {{site.data.keyword.cloudcerts_short}}에서 사용자가 요청된 도메인을 소유하고 있음을 확인하면 인증서가 발행되고 상태가 **유효**로 변경됩니다. 인증서가 준비되었거나 문제점이 발생한 경우 Slack 및/또는 콜백 URL 채널에서 사용자에게 알립니다.

## 인증서 갱신
{: #renew-certificate}

인증서가 곧 만료되는 경우 {{site.data.keyword.cloudcerts_short}}를 통해 인증서를 갱신하도록 요청할 수 있습니다. 인증서가 갱신될 때 필요한 경우 인증서의 이전 버전이 보관됩니다. 

갱신은 인증서 주문과 유사하게 작동합니다. 인증서 갱신을 요청하면 {{site.data.keyword.cloudcerts_short}}에서 콜백 URL에 DNS txt 인증 확인을 전송하므로 사용자가 인증서를 갱신 중인 도메인을 소유하고 있음을 다시 증명할 수 있습니다.

인증서를 갱신하려면 다음 단계를 완료하십시오.
  1. 갱신할 인증서의 행에서 메뉴를 클릭하십시오.
  2. **인증서 갱신**을 클릭하십시오.
  3. 선택사항: **인증서 키 다시 입력** 선택란을 선택하여 인증서 키를 다시 입력하도록 선택할 수 있습니다. 이렇게 하면 인증서가 새로운 키 쌍으로 갱신됩니다.
  
  인증서 키를 다시 입력할 때 새 인증서 및 키를 사용 중인 모든 위치에 배치해야 합니다.
  {: note}
    
  4. **갱신**을 클릭하십시오.
  
  {{site.data.keyword.cloudcerts_short}}를 통해 주문한 인증서만 갱신할 수 있습니다.
  {: note}

갱신이 **갱신 보류** 상태가 됩니다. 도메인 유효성 검증 인증 확인에 응답하고 {{site.data.keyword.cloudcerts_short}}에서 사용자가 요청된 도메인을 소유하고 있음을 확인하면 사용자가 갱신된 인증서를 얻고 상태가 **유효**로 변경됩니다. 갱신된 인증서가 준비되었거나 문제점이 발생한 경우 Slack 및/또는 콜백 URL 채널에서 사용자에게 알립니다.

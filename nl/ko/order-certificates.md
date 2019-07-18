---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL, dns,

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

# 인증서 주문
{: #ordering-certificates}

{{site.data.keyword.cloudcerts_long}}를 사용하여 지원되는 외부 인증 기관에서 서명된 앱 및 서비스에 대한 공용 SSL/TLS 인증서를 주문할 수 있습니다. {{site.data.keyword.cloudcerts_short}}를 사용하면 SSL/TLS 개인 키에 대한 추가 보안 이외에 공용 인증서를 쉽게 주문할 수 있습니다. 인증서가 발행된 후 인증서를 통합 서버에 배치하거나 다른 위치에서 사용하도록 다운로드할 수 있습니다.  
{: shortdesc}

인증서를 주문할 때 SSL/TLS에 대한 개인 키가 {{site.data.keyword.cloudcerts_short}}에서 직접 생성되고 안전하게 저장됩니다. 발행된 인증서에 대한 모든 요청 및 액세스는 [액세스 제어](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles)를 통해 관리하고 [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events)를 사용하여 자동으로 감사할 수 있습니다.  

{{site.data.keyword.cloudcerts_short}}는 ACME(Automatic Certificate Management Environment) v2 프로토콜을 ACME 클라이언트로 구현합니다. ACME 프로토콜을 사용하면 사용자 개입 없이 브라우저에서 신뢰된 인증서를 자동으로 얻을 수 있습니다.

## 인증서 특성
{: #certificate-characteristics}

{{site.data.keyword.cloudcerts_short}}를 통해 인증서를 주문하는 경우 인증서는 다음과 같습니다.

- 무료임
- 90일 동안 유효함
- 단일 도메인, 다중 도메인(SAN) 또는 와일드카드임
- 유효성 검증된 도메인임

도메인 유효성 검증에는 인증서를 요청하는 도메인을 소유하고 있는지 확인하는 일이 포함됩니다. EV(Extended Validation) 또는 OV(Organization Validated) 인증서가 필요한 경우 다른 위치에서 얻을 수 있으며 {{site.data.keyword.cloudcerts_short}}로 가져와서 라이프사이클을 관리할 수 있습니다.


## 지원되는 인증 기관
{: #supported-certificate-authorities}

인증 기관(CA)은 디지털 인증서를 발행하는 엔티티입니다. CA는 인증서의 요청자와 인증서에 의존하는 클라이언트 모두에 대한 신뢰할 수 있는 서드파티 역할을 합니다.
{: shortdesc}

### Let's Encrypt
{: #lets-encrypt}
[Let’s Encrypt](https://letsencrypt.org)는 90일 동안 유효한 도메인 유효성 검증 인증서를 제공하는 자동화된 무료 ACME 기반 CA입니다. ISRG(Internet Security Research Group)에서 제공되는 서비스입니다.

## 인증서 주문 설정
{: #setup}

인증서가 사용자에게 발행되기 전에 먼저 {{site.data.keyword.cloudcerts_short}}에서 사용자가 요청에 나열한 모든 도메인을 제어하는지 확인해야 합니다. 이렇게 하려면 {{site.data.keyword.cloudcerts_short}}는 DNS 유효성 검증을 사용합니다.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}}는 DNS(Domain Name System) 서비스에 추가할 수 있는 DNS TXT 레코드 양식의 인증 확인을 전송합니다. 인증서에서 요청하는 각 도메인에 대해 별도의 DNS TXT 레코드를 받습니다. DNS TXT 레코드를 추가한 후 {{site.data.keyword.cloudcerts_short}} 및 Let’s Encrypt에서 해당 레코드가 DNS 서비스에 있는지 확인합니다. 인증 확인을 완료하면 {{site.data.keyword.cloudcerts_short}} 인스턴스에 사용할 수 있는 Let’s Encrypt 인증서가 발행됩니다.

도메인 소유권을 확인하는 방법은 {{site.data.keyword.cis_full_notm}} 또는 다른 DNS 제공자 중 어느 것을 사용하는지에 따라 다릅니다.


### {{site.data.keyword.cis_full_notm}}
{: #cis}

{{site.data.keyword.cis_short}}에서 도메인을 관리하는 경우 다음 단계를 완료하여 소유권을 확인하십시오.

1. **{{site.data.keyword.cloud_notm}} >관리 > 액세스(IAM) > 권한**으로 이동하십시오.
2. **작성**을 클릭하고 소스 및 대상 서비스를 지정하십시오. 소스 서비스는 다음 단계에서 설정하는 역할에 따라 대상 서비스에 대한 액세스를 부여받습니다.
  * 소스: {{site.data.keyword.cloudcerts_short}}
  * 대상: Internet Services
3. 소스 및 대상에 대한 서비스 인스턴스를 지정하십시오.
4. **독자** 역할을 지정하여 {{site.data.keyword.cloudcerts_short}}가 {{site.data.keyword.cis_short_notm}} 인스턴스 및 해당 도메인을 볼 수 있게 하십시오. 그런 다음 **권한 부여**를 클릭하십시오.

  테스트를 목적으로, UI를 통해 모든 도메인을 관리할 수 있는 **관리자** 서비스 액세스 역할을 지정할 수 있습니다. 이렇게 하는 경우 5단계를 완료하지 않아도 됩니다. 프로덕션 환경에서 **독자** 서비스 액세스 역할을 지정하고 5단계에 표시된 API를 사용하여 특정 도메인을 제어하는 것이 좋습니다.
  {: note}
   
5. 특정 도메인을 제어하려면 {{site.data.keyword.cloudcerts_short}}가 {{site.data.keyword.cis_short_notm}} 인스턴스에 있는 개별 도메인의 DNS 레코드를 관리할 수 있도록 API를 사용하여 **관리자** 역할을 지정하십시오. 텍스트 파일에 명령을 복사하여 필수 매개변수를 쉽게 편집하도록 할 수 있습니다.
   
  

  
  ```
  curl -X POST https://iam.cloud.ibm.com/acms/v1/policies \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <token>' \
  -d '{ "type": "authorization", "subjects": [ { "attributes": [ { "name": "serviceName", "value": "cloudcerts" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Certificate-Manager-GUID-based-instanceID>" } ] } ], "roles": [ { "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Manager" } ], "resources": [ { "attributes": [ { "name": "serviceName", "value": "internet-svcs" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Cloud-Internet-Services-GUID-based-instanceID>" }, { "name": "domainId", "value": "<domainID>" }, { "name": "cfgType", "value": "reliability" }, { "name": "subScope", "value": "dnsRecord" } ] } ] }'
  ```
  {: codeblock} 
  

  <table>
    <tr>
      <th>변수</th>
      <th>설명</th>
    </tr>
    <tr>
      <td><code>token</code></td>
      <td>올바른 IAM 토큰입니다. {{site.data.keyword.cloud_notm}} CLI: <code>ibmcloud iam oauth-tokens</code>를 사용하여 값을 찾을 수 있습니다.</td>
    </tr>
    <tr>
      <td><code>accountID</code></td>
      <td>{{site.data.keyword.cloudcerts_short}} 및 {{site.data.keyword.cis_short_notm}} 인스턴스가 있는 계정의 ID입니다. <b>{{site.data.keyword.cloud_notm}} > 관리 > 계정 > 계정 설정</b>으로 이동하거나 {{site.data.keyword.cloud_notm}} CLI: <code>ibmcloud account show</code>를 사용하여 값을 찾을 수 있습니다.</td>
    </tr>
    <tr>
      <td><code>Certificate-Manager-GUID-based-instanceID</code></td>
      <td>{{site.data.keyword.cloudcerts_short}}의 인스턴스에 대한 GUID 기반 ID입니다. 값을 찾으려면 {{site.data.keyword.cloud_notm}} CLI: <code>ibmcloud resource service-instance "Instance name"</code>을 사용하십시오.</td>
    </tr>
    <tr>
      <td><code>Cloud-Internet-Services-GUID-based-instanceID</code></td>
      <td>{{site.data.keyword.cis_short_notm}}의 인스턴스에 대한 GUID 기반 ID입니다. 값을 찾으려면 {{site.data.keyword.cloud_notm}} CLI: <code>ibmcloud resource service-instance "Instance name"</code>을 사용하십시오.</td>
    </tr>
    <tr>
      <td><code>domainID</code></td>
      <td>{{site.data.keyword.cis_short_notm}}에 있는 도메인의 ID입니다. 값을 찾으려면 {{site.data.keyword.cloud_notm}} CLI를 사용하여 <code>ibmcloud cis domains</code>를 실행하십시오. 다중 도메인을 관리하려면 <code>resources</code> 배열을 수정하십시오.</td>
    </tr>
  </table>

이제 [인증서를 주문](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificate)할 수 있습니다.


### 다른 DNS 제공자
{: #other_provider}

서드파티 DNS 제공자를 사용하는 경우 도메인에 대한 제어를 확인하기 위해 {{site.data.keyword.cloudcerts_short}}가 TXT 레코드를 제공된 콜백 URL 알림 채널로 보내며, 이를 통해 도메인 유효성 검증 프로세스를 자동화할 수 있습니다.

먼저 도메인 유효성 검증을 위한 IBM Cloud Function 조치를 구현한 다음 콜백 URL 알림 채널에 해당 엔드포인트를 제공합니다. 시작하려면 [콜백 URL 알림 채널 설정](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions)을 참조하십시오.

콜백 URL 알림 채널을 사용하여 도메인 유효성 검증 설정에 대한 자세한 정보는 [이 블로그 게시물](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains){: external}을 참조하십시오.
{: tip}


#### 인증 확인에 응답
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

인증서 주문에 대해 자주 묻는 질문을 보려면 [FAQ 페이지를 검토](/docs/services/certificate-manager?topic=certificate-manager-faq)하십시오.
{: tip}

## 인증서 주문
{: #ordering-certificate}

인증서를 주문하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.cloudcerts_short}}의 관리 탭으로 이동하십시오.
2. **인증서 주문**을 클릭하십시오. 
3. DNS 제공자({{site.data.keyword.cis_full_notm}} 또는 다른 DNS 제공자)를 선택하십시오.
4. **{{site.data.keyword.cis_full_notm}}**를 선택한 경우 다음 세부사항을 제공하십시오.
   1. 필수 설정 지시사항 완료
   2. 인증서 이름 및 선택적으로 설명 제공
   3. 인증 기관 선택
   4. 서비스 액세스 역할을 지정한 {{site.data.keyword.cis_full_notm}} 인스턴스 선택
   5. 필요한 인증서 유형 선택
   6. 도메인 선택
   7. 적절한 알고리즘 및 키 알고리즘 선택
   8. **주문** 클릭
5. **다른 DNS 제공자**를 선택한 경우 다음 세부사항을 제공하십시오.
   1. 필수 설정 지시사항 완료
   2. 인증서 이름 및 선택적으로 설명 제공
   3. 인증 기관을 선택하십시오.
   4. 기본 도메인 및 대체 도메인 입력
   5. 적절한 알고리즘 및 키 알고리즘 선택
   6. **주문** 클릭

주문이 **보류** 상태가 됩니다. 도메인 유효성 검증 인증 확인에 응답하고 {{site.data.keyword.cloudcerts_short}}에서 사용자가 요청된 도메인을 소유하고 있음을 확인하면 인증서가 발행되고 상태가 **유효**로 변경됩니다. 인증서가 준비되었거나 문제점이 발생한 경우 Slack 및/또는 콜백 URL 알림 채널에서 사용자에게 알립니다.

## 인증서 갱신
{: #renew-certificate}

인증서가 곧 만료되는 경우 {{site.data.keyword.cloudcerts_short}}를 통해 인증서를 갱신하도록 요청할 수 있습니다. 인증서가 갱신될 때 필요한 경우 인증서의 이전 버전이 보관됩니다. 

갱신은 인증서 주문과 유사하게 작동합니다. 인증서 갱신을 요청하면 {{site.data.keyword.cloudcerts_short}}에서 콜백 URL에 DNS txt 인증 확인을 전송하므로 사용자가 인증서를 갱신 중인 도메인을 소유하고 있음을 다시 증명할 수 있습니다.

인증서를 갱신하려면 다음 단계를 완료하십시오.
  1. 갱신할 인증서의 행에서 메뉴를 클릭하십시오.
  2. **인증서 갱신**을 클릭하십시오.
  3. 선택사항: **인증서 키 다시 입력** 선택란을 선택하여 인증서 키를 다시 입력하도록 선택할 수 있습니다. 이렇게 하면 인증서가 새로운 키 쌍으로 갱신됩니다. 인증서 키를 다시 입력할 때 새 인증서 및 키를 사용 중인 모든 위치에 배치해야 합니다.
  4. **갱신**을 클릭하십시오.


{{site.data.keyword.cloudcerts_short}}를 통해 주문한 인증서만 갱신할 수 있습니다.
{: note}

갱신이 **갱신 보류** 상태가 됩니다. 도메인 유효성 검증 인증 확인에 응답하고 {{site.data.keyword.cloudcerts_short}}에서 사용자가 요청된 도메인을 소유하고 있음을 확인하면 사용자가 갱신된 인증서를 얻고 상태가 **유효**로 변경됩니다. 갱신된 인증서가 준비되었거나 문제점이 발생한 경우 Slack 및/또는 콜백 URL 알림 채널에서 사용자에게 알립니다.

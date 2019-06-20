---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-15"

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
{:faq: data-hd-content-type='faq'}

# 자주 묻는 질문(FAQ)
{: #faq}

{{site.data.keyword.cloudcerts_long}}에 대해 자주 묻는 질문입니다.
{: shortdesc}

## 내 인증서는 어떤 형식이어야 합니까?
{: #supported-certificate-types}
{: faq}

{{site.data.keyword.cloudcerts_short}}는 PEM 형식의 인증서만 지원합니다.

## 어떤 유형의 공개 키 알고리즘이 지원됩니까?
{: #supported-pk-algorithms}
{: faq}

{{site.data.keyword.cloudcerts_short}}는 다음과 같은 공개 키 알고리즘을 사용하여 생성된 공개 키로 인증서를 지원합니다.

* RSA(Rivest-Shamir-Adleman)
* 디지털 서명 알고리즘(DSA)
* ECDSA(Elliptic Curve Digital Signature Algorithm)
* ECDH(Elliptic Curve with Diffie-Hellman) 키 계약 프로토콜


## 비밀번호로 보호되는 개인 키를 업로드할 수 있습니까?
{: #password-protected-private-keys}
{: faq}

{{site.data.keyword.cloudcerts_short}}에서는 비밀번호로 보호되는 개인 키로 인증서 가져오기를 지원하지 않습니다.

## 인증서와 개인 키를 업로드하려고 시도하는데 다음 오류가 발생했습니다. `오류: 개인 키가 가져오려는 인증서와 일치하지 않습니다. 일치하는지 확인하고 다시 시도하십시오.`
{: #import-cert-private-key}
{: faq}

개인 키가 암호화되었는지 여부에 따라 다음 옵션 중 하나를 선택하십시오.

* 개인 키가 암호화되어 있습니다. 업로드하기 전에 개인 키를 복호화해야 합니다.

   ```
   openssl rsa -in [file1.key] -out [file2.key]
   ```
   {: pre}

* 개인 키가 암호화되어 있지 않습니다. 다음 명령의 결과를 비교하여 인증서와 개인 키가 일치하는지 확인하십시오. 여기서 `<certificate-file>`은 인증서 파일의 이름이며 `<key-file>`은 개인 키 파일의 이름입니다.

   ```
   openssl x509 -modulus -noout -in <certificate-file>.pem | openssl md5; openssl rsa -modulus -noout -in <key-file>.key | openssl md5
   ```
   {: pre}

## 인증서 만료에 대해 이메일 알림을 받을 수 있습니까?
{: #email-notifications}
{: faq}

콜백 및 Slack 알림만 지원됩니다.


## 내 인증서의 버전을 제어할 수 있습니까?
{: #certificate-versioning}
{: faq}

기존 인증서와 동일한 도메인을 포함하지만 새 만료 날짜가 있는 새 버전의 인증서를 다시 가져오기 하여 인증서를 업데이트할 수 있습니다. 인증서를 다시 가져오면 기존 인증서 버전은 백업으로 유지됩니다. [인증서 다시 가져오기](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate)를 참조하십시오.



## 특정 사용자에게만 특정 인증서가 표시되도록 할 수 있습니까?
{: #access-policies}
{: faq}

세분화된 액세스 제어를 위해 IAM 액세스 정책을 사용하여 인증서를 보호할 수 있습니다. [서비스 액세스 역할 관리](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles)를 참조하십시오.



## 발행된 인증서를 해지하는 방법은 무엇입니까?
{: #revoke-certificate}
{: faq}

현재 {{site.data.keyword.cloudcerts_short}}에는 사용할 수 있는 해지 API가 없습니다. 그러나 Let's Encrypt API를 사용하여 인증서 개인 키를 통해 인증서를 해지할 수 있습니다. [Let's Encrypt 문서](https://letsencrypt.org/docs/revoking/)에서 Let's Encrypt 인증서를 해지하는 방법을 알아볼 수 있습니다.



## 내 인증서 주문 상태가 오랫동안 보류 상태입니다.
{: #certificate-order-status}
{: faq}

느린 DNS 네트워크에서는 주문을 완료하는 데 최대 20분 정도가 걸릴 수 있습니다.

## 이 서비스에서 사용자가 내 주문에서 요청하는 도메인을 소유하고 있는지 유효성 검증하려고 시도하는 데 얼마나 걸립니까?
{: #certificate-order-validation}
{: faq}

도메인 유효성 검증 인증 확인을 전송한 후 {{site.data.keyword.cloudcerts_short}}는 최대 10분 동안 사용자가 요청한 도메인을 소유하고 있는지 유효성 검증하려고 시도합니다. DNS가 10분 이내에 TXT 레코드 인증 확인으로 업데이트되지 않으면 주문이 실패합니다.

## {{site.data.keyword.cloudcerts_short}} 공용 API를 사용하여 내 인증서 주문의 상태를 어떻게 확인합니까?
{: #certificate-order-status-api}
{: faq}

`Get certificate metadata` API를 사용하여 인증서 주문 상태를 폴링할 수 있습니다.

## 내 인증서가 완료되면 알림을 받을 수 있습니까?
{: #certificate-order-notification}
{: faq}

알림 채널을 구성한 경우 인증서가 발행되거나 주문에 실패하면 사용자에게 알립니다. 알림 채널의 버전이 v4 이상이어야 합니다.

## 내 주문이 실패했습니다. 이유는 무엇입니까?
{: #certificate-order-failure}
{: faq}

인증서 메타데이터, UI 및 주문 실패 시 받은 알림에서 오류 코드 및 메시지를 찾을 수 있습니다.

## 내 기존 Slack 알림 채널에서 인증서 주문 이벤트를 수신하지 않는 이유는 무엇입니까?
{: #missing-notification-for-ordered-certificate}
{: faq}

Certificate Manager 설정 탭에서 Slack 알림 채널을 최신 버전으로 업그레이드하십시오.

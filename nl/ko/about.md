---

copyright:
  years: 2017
lastupdated: "2017-12-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 정보
{: #about-cloud-certs}

{{site.data.keyword.cloudcerts_full}}에 대해 알아봅니다.

## {{site.data.keyword.cloudcerts_short}}의 개념
{: #what-is-cloud-certs}

{{site.data.keyword.cloudcerts_short}}는 {{site.data.keyword.IBM_notm}} 클라우드 기반 앱 및 서비스에 대한 SSL 인증서를 관리하는 데 도움을 줍니다.
{: shortdesc}

앱 및 서비스에 대해 얻은 SSL 인증서를 가져와서 안전하게 저장하고 사용 중인 인증서를 중앙에서 볼 수 있습니다.

다음과 같은 방법으로 인증서를 관리할 수 있습니다.

* 인증서의 만기 날짜를 모니터하여 제시간에 인증서를 갱신하는지 확인합니다.
* 배치에서 인증서의 유형을 보고 인증서가 조직 정책을 충족하는지 확인합니다.
* 새로운 준수 또는 보안 요구사항이 발행될 때 대체해야 하는 인증서를 찾습니다.
* 인증서에 액세스하고 인증서를 관리할 수 있는 사용자에 대한 제어를 설정합니다.

## 가용성
{: #availability}

{{site.data.keyword.cloudcerts_short}}는 미국 남부 지역에서만 사용할 수 있습니다.

## 개인 키 보안
{: #private-key-security}

인증서와 해당 개인 키를 {{site.data.keyword.cloudcerts_short}}로 가져올 때 서비스에서 고급 암호화 표준(AES) 256 알고리즘을 사용하여 개인 키를 암호화합니다. {{site.data.keyword.cloudcerts_short}}가 서비스 인스턴스에 사용하도록 이 암호화된 고유 키를 저장합니다.

## ID 및 액세스 관리
{: #identity-access-management}

지정된 역할이 있는 사용자만 특정 조치를 완료할 수 있도록 하여 {{site.data.keyword.Bluemix_notm}} 내에서 서비스의 보안 설정할 수 있습니다.
{: shortdesc}

<table>
<caption> 표 1. 사용자 역할에 맵핑된 조치</caption>
  <tr>
    <th> 조치 </th>
    <th> 역할</th>
  </tr>
  <tr>
    <td>인증서 나열</td>
    <td> 관리자, 운영자, 편집자, 뷰어 </td>
  </tr>
  <tr>
    <td>인증서 및 개인 키 다운로드</td>
    <td> 관리자, 운영자 </td>
  </tr>
  <tr>
    <td>인증서 데이터 업데이트</td>
    <td> 관리자, 편집자 </td>
  </tr>
  <tr>
    <td>인증서, 개인 키 및 중간 인증서 업로드</td>
    <td> 관리자, 편집자 </td>
  </tr>
  <tr>
    <td>인증서 및 개인 키 삭제 </td>
    <td> 관리자, 편집자 </td>
  </tr>
</table>

사용자 역할 및 권한에 대한 자세한 정보는 [사용자 역할](/docs/admin/patterns.html#userroles)을 참조하십시오.

### 사용자 역할 지정
{: #assigning-user-roles}

계정 레벨 또는 리소스 그룹 레벨에서 사용자를 지정하려면 다음 단계를 완료하십시오.
사용자가 조직의 일부가 아니면 해당 사용자에게 초대장을 전송하여 시작하십시오.

1. **관리 > 계정 > 사용자**로 이동하십시오.
2. **조치** 메뉴에서 **정책 지정**을 선택하십시오.
3. **리소스에 대한 액세스 권한 지정** 또는 **리소스 그룹 내의 액세스 권한 지정**을 클릭하십시오.
4. **서비스**에서 **Certificate Manager**를 선택하십시오.
5. 선택사항: **지역**을 선택하거나 기본값인 **모든 지역**을 사용하십시오.
6. 선택사항: **서비스 인스턴스**를 선택하거나 기본값인 **모든 인스턴스**를 사용하십시오.
7. **역할 선택 > 플랫폼 액세스 역할 지정**에서 적절한 액세스 레벨을 선택하십시오.

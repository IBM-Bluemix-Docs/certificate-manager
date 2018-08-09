---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-20"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 서비스 액세스 역할 관리
{: #managing-service-access-roles}

지정된 액세스 역할이 있는 사용자만 특정 조치를 완료할 수 있도록 하여 {{site.data.keyword.Bluemix_notm}} 내에서 서비스의 보안을 설정할 수 있습니다.
{: shortdesc}


## 플랫폼 액세스 역할
{: #platform-access-roles}

플랫폼 액세스 역할을 사용하여 사용자가 플랫폼 리소스에서 태스크(예: {{site.data.keyword.Bluemix_notm}} 계정에서 인스턴스 작성 또는 삭제)를 완료하도록 할 수 있습니다.

<table>
<caption> 표 1. 플랫폼 액세스 역할에 맵핑된 조치</caption>
  <tr>
    <th> 조치 </th>
    <th> 역할 </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudcerts_short}}의 인스턴스 보기</td>
    <td> 관리자, 운영자, 편집자, 뷰어 </td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudcerts_short}}의 인스턴스 작성</td>
    <td> 관리자, 편집자 </td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudcerts_short}}의 인스턴스 삭제</td>
    <td> 관리자, 편집자 </td>
  </tr>
</table>

플랫폼 역할은 인스턴스 내 인증서에 대한 특정 조치에 액세스를 제공합니다. 이 조치는 더 이상 사용되지 않습니다.


## 서비스 액세스 역할
{: #service-access-roles}

서비스 액세스 역할을 사용하여 사용자가 {{site.data.keyword.cloudcerts_short}} 인스턴스에서 태스크(예: 인증서 가져오기, 다운로드, 편집 또는 삭제)를 완료하도록 할 수 있습니다.

<table>
<caption> 표 2. 서비스 액세스 역할에 맵핑된 조치</caption>
  <tr>
    <th> 조치 </th>
    <th> 역할 </th>
  </tr>
  <tr>
    <td>인증서 나열</td>
    <td> 관리자, 작성자, 독자 </td>
  </tr>
  <tr>
    <td>인증서 및 개인 키 다운로드 </td>
    <td> 관리자, 작성자 </td>
  </tr>
  <tr>
    <td>인증서 데이터 업데이트</td>
    <td> 관리자, 작성자 </td>
  </tr>
  <tr>
    <td>인증서, 개인 키 및 중간 인증서 업로드 </td>
    <td> 관리자  </td>
  </tr>
  <tr>
    <td>인증서 및 개인 키 삭제 </td>
    <td> 관리자 </td>
  </tr>
      <tr>
        <td>모든 알림 채널 나열</td>
        <td> 관리자, 작성자, 독자 </td>
      </tr>
   <tr>
     <td>알림 채널 추가, 업데이트 또는 삭제</td>
     <td> 관리자 </td>
   </tr>
     <tr>
       <td>알림 채널 테스트</td>
       <td> 관리자, 작성자, 독자 </td>
     </tr>
</table>


사용자 역할 및 권한에 대한 자세한 정보는 [사용자 역할](/docs/iam/users_roles.html#userroles)을 참조하십시오.


## 사용자에 대한 액세스 정책 구성
{: #configuring-access-policies}

{{site.data.keyword.cloudcerts_short}} 인스턴스에 대한 액세스 정책을 구성할 수 있거나(즉, 해당 인스턴스의 모든 인증서용) 인스턴스 내의 개별 인증서(리소스)에 대한 정책을 설정할 수 있습니다.
{: shortdesc}

1.  **관리 > 계정 > 사용자**로 이동하십시오. {{site.data.keyword.Bluemix_notm}} 계정에 대한 액세스 권한이 있는 사용자의 목록이 표시됩니다.
2.  액세스 정책을 지정할 사용자의 이름을 클릭하십시오. 사용자가 표시되지 않으면 **사용자 초대**를 클릭하여 [사용자를 {{site.data.keyword.Bluemix_notm}} 계정에 추가](/docs/iam/iamuserinv.html#iamuserinv)를 수행하십시오.
3.  **액세스 지정**을 클릭하십시오.
4.  **리소스에 액세스 지정**을 클릭하십시오.
5.  **서비스** 드롭 다운 메뉴에서 **인증서 관리자**를 선택하십시오.
6.  **서비스 인스턴스** 메뉴에서 {{site.data.keyword.cloudcerts_short}} 인스턴스를 선택하거나 기본값 `All instances`를 사용하십시오.
7.  선택사항: 특정 인증서에 대한 액세스 권한을 구성하십시오.
    1. [인증서 ID를 검색](#get-certificate-id)하십시오.
    2. **리소스 유형** 필드에 `certificate`를 입력하십시오.
    3. **리소스 ID** 필드에 인증서 ID를 입력하십시오.
8.  [플랫폼 액세스 역할](#platform-access-roles)을 사용자에게 지정하십시오.
9.  [서비스 액세스 역할](#service-access-roles)을 사용자에게 지정하십시오.
10. **지정**을 클릭하여 액세스 정책을 사용자에게 지정하십시오.

**역할 할당의 예:**
* 모든 사용자가 서비스 인스턴스를 볼 수 있도록 모든 사용자에게 최소한 뷰어 역할을 지정하십시오.
* 사용자가 인스턴스를 작성/삭제하도록 하려면 사용자에게 관리자 또는 편집자 역할을 지정하십시오.
* 사용자가 인스턴스 내 인증서를 보도록 하려면 최소한 독자 역할을 지정하십시오.

### 인증서 ID 검색
{: #get-certificate-id}

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.cloudcerts_short}} 인스턴스를 선택하십시오.
2. 서비스 세부사항 페이지의 탐색에서 **관리**를 선택하십시오.
3. 인증서를 선택하십시오.
4. 인증서 세부사항에서 인증서 CRN을 찾으십시오.
5. 인증서 ID를 복사하십시오. CRN에는 모두 콜론(`:`)으로 구분된 서로 다른 값이 포함되어 있습니다. 인증서 ID는 CRN의 마지막 값입니다(예: `e20cb664efcbfa2c2f57801230d246a6`).

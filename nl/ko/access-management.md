---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-13"

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

### 플랫폼 액세스 역할
{: #platform-access-roles}

플랫폼 액세스 역할을 사용하여 사용자가 플랫폼 리소스에서 태스크(예: IBM Cloud 계정에서 인스턴스 작성 또는 삭제)를 완료하도록 할 수 있습니다.

<table>
<caption> 표 1. 플랫폼 액세스 역할에 맵핑된 조치</caption>
  <tr>
    <th> 조치 </th>
    <th> 역할 </th>
  </tr>
  <tr>
    <td>Certificate Manager의 인스턴스 보기</td>
    <td> 관리자, 운영자, 편집자, 뷰어 </td>
  </tr>
  <tr>
    <td>Certificate Manager의 인스턴스 작성</td>
    <td> 관리자, 편집자 </td>
  </tr>
  <tr>
    <td>Certificate Manager의 인스턴스 삭제</td>
    <td> 관리자, 편집자 </td>
  </tr>
</table>

역사적으로 플랫폼 역할은 인스턴스 내 인증서에 대한 특정 조치에 액세스를 제공합니다. 이 정의는 더 이상 사용되지 않으며 가까운 시일 내에 제거됩니다.

### 서비스 액세스 역할
{: #service-acceess-roles}

서비스 액세스 역할을 사용하여 사용자가 Certificate Manager 인스턴스에서 태스크(예: 인증서 가져오기, 다운로드, 편집 또는 삭제)를 완료하도록 할 수 있습니다.

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
    <td> 관리자 </td>
  </tr>
  <tr>
    <td>인증서 및 개인 키 삭제 </td>
    <td> 관리자 </td>
  </tr>
</table>


사용자 역할 및 권한에 대한 자세한 정보는 [사용자 역할](/docs/iam/users_roles.html#userroles)을 참조하십시오.

### 사용자 액세스 역할 지정
{: #assigning-user--access-roles}

계정 레벨 또는 리소스 그룹 레벨에서 액세스 역할을 지정하려면 다음 단계를 완료하십시오.
사용자가 조직의 일부가 아니면 해당 사용자에게 초대장을 전송하여 시작하십시오.

1. **관리 > 계정 > 사용자**로 이동하십시오.
2. **조치** 메뉴에서 **정책 지정**을 선택하십시오.
3. **리소스에 대한 액세스 권한 지정** 또는 **리소스 그룹 내의 액세스 권한 지정**을 클릭하십시오.
4. **서비스**에서 **Certificate Manager**를 선택하십시오.
5. 선택사항: **지역**을 선택하거나 기본값인 **모든 지역**을 사용하십시오.
6. 선택사항: **서비스 인스턴스**를 선택하거나 기본값인 **모든 인스턴스**를 사용하십시오.
7. **역할 선택 > 플랫폼/서비스 액세스 역할 지정**에서 적합한 액세스 레벨을 선택하십시오.

**예:**
* 모든 사용자가 서비스 인스턴스를 볼 수 있도록 모든 사용자에게 최소한 뷰어 역할을 지정하십시오. 
* 사용자가 인스턴스를 작성하도록 하려면 사용자에게 관리자 또는 편집자 역할을 지정하십시오. 
* 사용자가 인스턴스 내 인증서를 보도록 하려면 최소한 독자 역할을 지정하십시오.

---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL,

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

# 대시보드에서 인증서 관리
{: #managing-certificates-from-the-dashboard}

{{site.data.keyword.cloudcerts_full}} 서비스 대시보드를 사용하여 {{site.data.keyword.IBM_notm}} 클라우드 기반 앱 또는 서비스에 사용하기 위해 서드파티 발행자로부터 얻는 인증서를 관리할 수 있습니다.
{: shortdesc}

## 지원 인증서 형식 및 공개 키 알고리즘
{: supported-formats-and-algorithms}

### 인증서 형식
* PEM

### 공개 키 알고리즘
* RSA(Rivest-Shamir-Adleman)
* 디지털 서명 알고리즘(DSA)
* ECDSA(Elliptic Curve Digital Signature Algorithm)
* ECDH(Elliptic Curve with Diffie-Hellman) 키 계약 프로토콜

## 인증서 가져오기
{: #importing-a-certificate}

인증서를 관리할 수 있도록 인증서를 가져오십시오.
{: shortdesc}

**시작하기 전에**

* 일치하는 개인 키와 함께 만료되지 않는 유효한 인증서를 작성하십시오(키는 선택사항).
* 파일을 PEM(Privacy-enhanced Electronic Mail) 형식으로 변환하십시오.
* 가져올 수 있도록 개인 키를 암호화되지 않은 상태로 유지하십시오.

인증서를 가져오려면 **인증서 가져오기**를 클릭하고 다음 세부사항을 제공하십시오.

1. 인증서 이름을 제공하십시오.
2. **찾아보기**를 클릭하여 PEM 형식의 인증서 파일을 선택하십시오.
3. 선택사항: **찾아보기**를 클릭하여 PEM 형식의 인증서 개인 키를 선택하십시오.
4. 해당되는 경우 PEM 형식의 중간 인증서 파일을 제공하십시오.
5. 선택사항: 설명을 입력하십시오.
6. **가져오기**를 클릭하십시오.

인증서를 가져온 후 다음 정보가 인증서 테이블에 표시됩니다. 인증서에 대한 자세한 정보를 보기 위해, 인증서 테이블에서 해당 인증서 행을 펼칠 수 있습니다.

<table>
<caption> 표 1. 가져온 인증서에 대한 정보 </caption>
  <tr>
    <th> 컴포넌트 </th>
    <th> 설명 </th>
  </tr>
  <tr>
    <td>이름</td>
    <td>의미 있는 표시 이름입니다. 최대 길이는 256자입니다. </td>
  </tr>
  <tr>
    <td>설명</td>
    <td>(선택사항) 인증서에 대한 설명 텍스트입니다. 최대 길이는 1024자입니다.</td>
  </tr>
  <tr>
    <td>도메인</td>
    <td>인증서가 유효한 도메인입니다. </td>
  </tr>
  <tr>
    <td>발행자</td>
    <td>인증서를 발행한 인증 기관(CA)입니다.</td>
  </tr>
  <tr>
    <td>알고리즘</td>
    <td>인증서 서명 알고리즘입니다.</td>
  </tr>
  <tr>
    <td>키 알고리즘</td>
    <td>공개 키 알고리즘</td>
  </tr>
  <tr>
    <td>만료 기한</td>
    <td>인증서가 더 이상 유효하지 않게 될 때까지 남은 일 수입니다. </td>
  </tr>
  <tr>
    <td>유효 기간 시작</td>
    <td>인증서가 유효하게 된 날짜입니다(협정 세계시(UTC) 시간대).</td>
  </tr>
  <tr>
    <td>만료 날짜</td>
    <td>인증서가 더 이상 유효하지 않은 날짜입니다(협정 세계시(UTC) 시간대).</td>
  </tr>
  <tr>
    <td>상태</td>
    <td>인증서의 상태입니다. </td>
  </tr>
  <tr>
    <td>인증서 ID</td>
    <td>가져오기 시 인증서에 제공되는 생성된 ID입니다.</td>
  </tr>
</table>

</br>

## 인증서 다시 가져오기
{: #reimport-certificate}

인증서가 곧 만료되는 경우, 기존 인증서와 동일한 도메인을 포함하지만 새 만료 날짜가 있는 새 버전을 가져와 인증서를 업데이트할 수 있습니다. 인증서를 다시 가져오면, 필요한 경우 다운로드할 수 있도록 기존 인증서 버전은 백업으로 유지됩니다.
{: shortdesc}

### 인증서 다시 가져오기
{: #reimporting-certificate}

인증서를 다시 가져오려면 다음 단계를 완료하십시오.

1. 해당 인증서의 행을 펼치십시오.
2. **인증서 다시 가져오기**를 클릭하십시오.
3. **찾아보기**를 클릭하여 PEM 형식의 새 인증서 파일을 선택하십시오.
4. (선택사항) **찾아보기**를 클릭하여 PEM 형식의 새 인증서 개인 키를 선택하십시오.
5. (선택사항) **찾아보기**를 클릭하여 PEM 형식의 새 중간 인증서 파일을 제공하십시오.
6. **다시 가져오기**를 클릭한 후 **완료**를 클릭하십시오.

인증서 가져오기는 분당 5개의 조치로 제한됩니다.
{: note}

### 인증서의 이전 버전 다운로드
{: #downloading-certificate}

인증서의 이전 버전을 다운로드하려면 다음 단계를 완료하십시오.

1. 해당 인증서의 행을 펼치십시오.
2. **이전 버전** 링크를 클릭하십시오.

## 인증서 주문
{: #order-certificates}

인증서를 주문하기 전에 [먼저 필수 설정을 완료하십시오](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates).  
인증서를 주문하려면 **인증서 주문**을 클릭하거나 **{{site.data.keyword.cis_full_notm}}** 또는 **다른 DNS 제공자**를 선택하고 다음 세부사항을 제공하십시오.

1. 인증서 이름.
2. 인증 기관.
3. 필수 도메인.
4. 적절한 알고리즘 및 키 알고리즘.
5. **주문**을 클릭하십시오.

인증서 주문은 {{site.data.keyword.cloudcerts_short}} 인스턴스당 5개의 주문/분, IBM 사용자 계정당 100개의 주문/시간 및 동일한 도메인에 대해 주당 5개의 인증서로 제한됩니다.
{: note}

## 인증서 갱신
{: #renew-certificates}

인증서를 갱신하려면 다음 단계를 완료하십시오.
  1. 갱신할 인증서의 행에서 메뉴를 클릭하십시오.
  2. **인증서 갱신**을 클릭하십시오.
  3. 선택사항: **인증서 키 다시 입력** 선택란을 선택하여 인증서 키를 다시 입력하도록 선택할 수 있습니다. 이렇게 하면 인증서가 새로운 키 쌍으로 갱신됩니다.
  
    인증서 키를 다시 입력할 때 새 인증서 및 키를 사용 중인 모든 위치에 배치해야 합니다.
    {: note}
    
  4. **갱신**을 클릭하십시오.
  
  {{site.data.keyword.cloudcerts_short}}를 통해 주문한 인증서만 갱신할 수 있습니다.
  {: note}

인증서 갱신은 인증서당 5개의 갱신 요청/분, IBM 사용자 계정당 100개의 갱신/시간으로 제한됩니다.
{: note}


## 인증서 검색
{: #searching-certificates}

여러 인증서를 관리하는 경우 검색 표시줄을 사용하여 필요한 인증서를 찾을 수 있습니다.
{: shortdesc}

* 인증서 이름, 인증서 도메인 또는 인증서 발행자를 검색하려면 검색 표시줄에 검색어를 입력하고 Enter를 누르십시오.
* 모든 인증서를 보려면 검색 표시줄에서 **X** 아이콘을 클릭하십시오.

## 인증서 다운로드
{: #downloading-certificates}

앱이나 서비스에 인증서를 배치할 준비가 되면 인증서 및 연관된 개인 키를 다운로드할 수 있습니다.
{: shortdesc}

인증서를 다운로드하려면 다음 단계를 완료하십시오.

1. 다운로드할 인증서에 대한 선택란을 선택하십시오.
2. **인증서 다운로드**를 클릭하십시오. 서비스로 가져온 항목에 따라 인증서의 PEM 파일, 연관된 개인 키 및 연관된 중간 인증서를 포함하는 압축된 파일을 수신합니다.

만료된 인증서는 다운로드할 수 없습니다.
{: note}

## 인증서 삭제
{: #deleting-certificates}

인증서 추적을 중지하려는 경우 인증서를 삭제할 수 있습니다.
{: shortdesc}  

인증서를 삭제하려면 다음 단계를 완료하십시오.

1. 삭제할 인증서에 대한 선택란을 선택하십시오.
2. **휴지통** 아이콘을 클릭하십시오.

## 인증서 메타데이터 업데이트
{: #updating-certificates-metadata}

인증서의 이름과 설명을 업데이트할 수도 있습니다.
{: shortdesc}

인증서를 업데이트하려면 다음 단계를 완료하십시오.

1. 행을 선택하여 해당 인증서에 대한 세부사항을 여십시오.
2. 이름 또는 설명을 업데이트하십시오.
3. 변경사항을 저장하십시오.

분당 최대 5개의 업데이트 조치를 수행할 수 있습니다.
{: note}

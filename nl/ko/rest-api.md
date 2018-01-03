---
copyright:
  years: 2017
lastupdated: "2017-12-14"
---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# API를 사용하여 인증서 관리
{: #managing-certificates-api}

{{site.data.keyword.cloudcerts_full}} 서비스는 인증서를 가져오고 삭제하기 위한 REST 엔드포인트를 제공합니다. {{site.data.keyword.iamshort}}를 사용하여 [특정 인증서에 대한 정책을 지정](#assigning-advanced-policies)할 수도 있습니다.
{: shortdesc}

## API 테스트
{: #testing}

Swagger를 사용하거나 명령행에서 cURL 요청을 실행하여 REST 엔드포인트를 테스트할 수 있습니다.  
Swagger는 미국 남부 {{site.data.keyword.Bluemix_notm}} 지역에서만 사용할 수 있습니다.
{: shortdesc}

## 전제조건
{: #prereq-api}

{{site.data.keyword.cloudcerts_full}}를 사용하기 전에 다음 태스크를 완료해야 합니다.
{: shortdesc}

* [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/get_started.html#getting-started)를 설치하여 필수 데이터를 얻으십시오.

* {{site.data.keyword.cloudcerts_short}} API에 대해 작업할 때 호출에서 다음 변수를 사용할 수 있습니다.


<table>
<caption> 표 1. 명령 컴포넌트 설명 </caption>
  <tr>
    <th> 컴포넌트</th>
    <th> 설명 </th>
  </tr>
  <tr>
    <td> <code> IAM-token </code> </td>
    <td> {{site.data.keyword.Bluemix_notm}}에 로그인하고 <code>bx iam oauth-tokens</code> 명령을 실행하여 IAM({{site.data.keyword.iamshort}}) 액세스 토큰을 얻을 수 있습니다.</td>
  </tr>
  <tr>
    <td> <code> certificateId </code> </td>
    <td> 다음 선택사항 중 하나를 사용하여 인증서 ID를 찾을 수 있습니다. <ul><li> GUI에서 인증서 테이블의 행에서 인증서를 선택하십시오. <li> API에서 [사용 가능한 인증서를 나열](/docs/services/certificate-manager/rest-api.html#list-certificates)하십시오.</ul> </td>
  </tr>
  <tr>
    <td> <code> instanceId </code> </td>
    <td> 작성된 후 서비스 인스턴스에 지정된 [CRN(Cloud Resource Name) 기반 인스턴스 ID](/docs/overview/crn.html#format)입니다. 다음과 같은 방법으로 인스턴스 ID를 검색할 수 있습니다.
    <ul>
      <li>서비스의 관리 페이지에서</li>
      <li><i>&lt;Instance_Name&gt;</i>을 서비스 인스턴스의 이름으로 대체하여 <code>bx resource service-instance</code> 명령을 실행하십시오.
      <pre>bx resource service-instance &lt;Instance_Name&gt; --id</pre>
      </li>
      <li>계정 관리자의 IAM 토큰이 포함된 <code>Authorization</code> 헤더가 필요한 {{site.data.keyword.Bluemix_notm}} Resource Controller <code>[GET /resource_instances](https://console.bluemix.net/apidocs/700-resource-controller-api?&language=node#resource-instances-1)</code> REST 엔드포인트를 호출하십시오.</li>
    </ul>
  </td>
  </tr>
  <tr>
    <td>  <code> account-id </code> </td>
    <td> {{site.data.keyword.Bluemix_notm}} 계정을 관리하는 사용자의 계정 ID입니다. <code>bx info</code> 명령을 실행하여 계정 ID를 찾을 수 있습니다. </td>
  </tr>
  <tr>
    <td>  <code> cluster-url </code> </td>
    <td> 작성된 {{site.data.keyword.Bluemix_notm}} 지역의 서비스 URL입니다. Swagger UI에서 URL을 찾을 수 있습니다. </td>
  </tr>
  <tr>
    <td>  <code> name(선택사항) </code> </td>
    <td> 가져온 인증서에 대한 표시 이름입니다. </td>
  </tr>
  <tr>
    <td> <code> description(선택사항) </code> </td>
    <td> 가져온 인증서에 대한 설명입니다. </td>
  </tr>
  <tr>
    <td> <code> certificate </code> </td>
    <td> 이스케이프된 인증서 데이터입니다. </td>
  </tr>
  <tr>
    <td> <code> privateKey </code> </td>
    <td> 이스케이프된 개인 키 데이터입니다. </td>
  </tr>
  <tr>
    <td> <code> intermediate(선택사항) </code> </td>
    <td> 이스케이프된 중간 인증서 데이터입니다. </td>
  </tr>
  <tr>
    <td> <code> user-id </code> </td>
    <td>액세스 정책을 지정할 사용자의 ID입니다. 사용자 ID를 찾으려면 [사용지 ID 검색](#retrieve-user-id)을 참조하십시오. </td>
  </tr>
</table>

## 인증서 가져오기
{: #import-certificate}  

PEM(Privacy-enhanced Electronic Mail) 형식의 인증서를 해당 개인 키와 함께 가져옵니다. 중간 인증서를 가져올 수도 있습니다.
{: shortdesc}


다음 `curl` 명령을 실행하십시오.

  ```
  curl -X POST \
  https://<cluster-url>/api/v1/<instanceId>/certificates/import \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<description>",
	"data":{
		"content": "<certificate>",
		"priv_key": "<privateKey>",
		"intermediate": "<intermediate>"
	}
  }'
  ```
  {: pre}

_&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_, _&lt;description&gt;_, _&lt;certificate&gt;_,  _&lt;privateKey&gt;_ 및 _&lt;intermediate&gt;_를 적절한 값으로 대체하십시오. _&lt;name&gt;_, _&lt;description&gt;_ 및 _&lt;intermediate&gt;_ 값은 선택사항입니다.

## 인증서 메타데이터 업데이트
{: #update-certificate-metadata}  

인증서의 선택적 `name` 특성, `description` 특성 또는 둘 다를 업데이트합니다.

**참고**: 업데이트 오퍼레이션은 분당 5개의 조치로 제한됩니다.  
{: shortdesc}


다음 `curl` 명령을 실행하십시오.

  ```
  curl -X POST \
  https://<cluster-url>/api/v1/<instanceId>/certificates/<certificateId> \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<description>"
  }'
  ```
  {: pre}

_&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;certificateId&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_ 및 _&lt;description&gt;_을 적절한 값으로 대체하십시오.

## 모든 인증서 나열
{: #list-certificates}  

사용 가능한 모든 인증서의 목록을 검색합니다.
{: shortdesc}

다음 `curl` 명령을 실행하십시오.

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v1/<instanceId>/certificates/
  ```
  {: pre}

_&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_ 및 _&lt;instanceId&gt;_를 적절한 값으로 대체하십시오.

## 인증서 다운로드
{: #get-certificate}  

검색된 인증서 ID를 사용하여 인증서 데이터를 다운로드합니다.
{: shortdesc}

다음 `curl` 명령을 실행하십시오.

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v1/<instanceId>/certificates/<certificateId>
  ```
  {: pre}

_&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_ 및 _&lt;certificateId&gt;_를 적절한 값으로 대체하십시오.

## 인증서 삭제
{: #delete-certificate}  

검색된 인증서 ID를 사용하여 인증서 및 해당 데이터를 삭제합니다.
{: shortdesc}

다음 `curl` 명령을 실행하십시오.

  ```
  curl -H "Authorization: Bearer <IAM-token>" -X DELETE https://<cluster-url>/api/v1/<instanceId>/certificates/<certificateId>
  ```
  {: pre}

_&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_ 및 _&lt;certificateId&gt;_를 적절한 값으로 대체하십시오.

## 고급 정책 지정
{: #assigning-advanced-policies}

특정 사용자가 특정 인증서에 대해 특정 조치를 수행할 수 있도록 선택할 수 있습니다. 사용자가 사용 가능한 서비스 인스턴스 인증서의 서브세트만 볼 수 있도록 할 수도 있습니다.
{: shortdesc}

정책을 지정하려면 다음 `curl` 명령을 실행하여 {{site.data.keyword.iamshort}}에 요청을 전송하십시오. 각 인증서에 대해 명령을 반복하십시오.

```
curl -X POST \
    https://iampap.<region>.bluemix.net/acms/v1/scopes/a%2<account-id>/users/<user-id>/policies \
    -H 'accept: application/json' \
    -H 'authorization: Bearer <Account-Admin-IAM-token>' \
    -H 'cache-control: no-cache' \
    -H 'content-type: application/json' \
    -d '{
        "roles": [
        {
            "id": "crn:v1:bluemix:public:iam::::role:Viewer"
        }
    ],
    "resources": [
        {
            "serviceName”: "cloudcerts",
            "serviceInstance": "<instanceId>",
            "resourceType": "certificate",
            "resource": "<certificateId>"
        }
    ]
}'
```
{: pre}

_&lt;account-id&gt;_, _&lt;user-id&gt;_, _&lt;instanceId&gt;_ 및 _&lt;certificateId&gt;_를 적절한 값으로 대체하십시오.
_&lt;Account-Admin-IAM-token&gt;_을 계정 관리자의 IAM 토큰으로 대체하십시오.
_&lt;region&gt;_을 지역으로 대체하십시오(예: 미국 남부의 경우 `ng`).

**참고**: 선행 cURL 요청에서 <code>instanceId</code>는 CRN 기반이 아니라 GUID 기반입니다.  
예를 들어, 다음 <code>instanceId</code> CRN에서 인스턴스 값은 **58866f34-55ca-4477-8c32-fda435f01f97**입니다.

```
crn:v1:staging:public:cloudcerts:us-south:a/d0c8a917589e40076a61e56b23056d16:58866f34-55ca-4477-8c32-fda435f01f97::
```

### 사용자 ID 검색
{: #retrieve-user-id}

사용자 ID를 검색합니다.
{: shortdesc}

사용자 ID를 검색하려면 다음 단계를 완료하십시오.

1. 사용자에게 [IAM 토큰을 제공](/docs/services/certificate-manager/rest-api.html#prereq-api)하도록 요청하십시오. IAM 토큰 구조는 다음 형식으로 되어 있습니다. `<value_1>.<value_2>.<value_3>`
2. _&lt;value_2&gt;_의 값을 복사하고 다음 `echo` 명령을 실행하십시오.

   ```
   echo -n "<value_2>" | base64 --decode
   ```
   {: pre}

   결과는 다음 출력과 유사한 JSON 오브젝트입니다.

   ```
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

3. `id` 특성의 값을 복사하십시오.

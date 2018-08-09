---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-05"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 만료되는 인증서를 위한 알림 구성
{: #configuring-notifications-for-expiring-certificates}

인증서는 일반적으로 지정된 시간 동안에만 유효합니다. 사용하는 인증서가 만료되면 앱이 작동 중단될 수 있습니다. 작동 중단이 발생하지 않기 위해, 만료될 예정인 인증서에 대한 일림을 전송하도록 {{site.data.keyword.cloudcerts_full}}를 구성하여 제시간에 인증서를 갱신할 수 있습니다.
{: shortdesc}

**알림을 받는 시기** </br>
{{site.data.keyword.cloudcerts_full}}에 업로드한 인증서의 만기 날짜에 따라 인증서가 만료되기 90일, 60일, 30일, 10일 및 1일 전에 알림을 받습니다. 또한 인증서가 만료된 후 첫 번째 날부터 만료된 인증서에 대한 알림을 매일 받습니다.  

알림을 더 이상 받지 않으려면 인증서를 갱신하고, 이 인증서를 {{site.data.keyword.cloudcerts_full}}에 업로드하고, 만료된 인증서를 삭제해야 합니다. 

**알림을 구성하기 위한 내 옵션** </br>
Slack 웹훅을 사용하여 Slack에 알림을 전송하거나 원하는 콜백 URL을 사용할 수 있습니다. 

## Slack 웹훅 설정
{: #setup-callback}

1. [Slack](https://slack.com/)에 등록하고 작업공간을 설정하십시오. 
2. 알림을 게시할 Slack 채널을 작성하십시오. 
3. Slack 채널에 대한 [웹훅을 설정](https://api.slack.com/incoming-webhooks)하십시오. 

## 콜백 URL 설정
{: #callback}

팀을 위해 갱신 프로세스를 트리거하는 데 매일 사용하는 도구에 대한 알림을 게시하도록 콜백 URL을 사용하려고 할 수 있습니다. 예를 들어, pager duty에 보고서에 대한 알림을 전송하거나, Github에서 문제를 자동으로 열거나, 갱신 스크립트를 트리거할 수 있습니다.  
{: shortdesc}

**중요:** 콜백 URL 엔드포인트는 {{site.data.keyword.cloudcerts_short}}와 함께 사용될 다음 요구사항을 충족해야 합니다.  
* 엔드포인트는 HTTPS 프로토콜을 사용해야 합니다.
* 엔드포인트는 HTTP 헤더를 요구하면 안 됩니다. 이 요구사항에는 권한 헤더가 포함되어 있습니다.

### 콜백 URL을 사용하여 자동으로 GitHub 문제 열기 
{: #sample}

다음 샘플 코드는 {{site.data.keyword.cloudcerts_short}} 알림이 전송될 때 만료되는 인증서에 대한 GitHub 문제를 작성하는 방법을 보여줍니다. {{site.data.keyword.openwhisk}}에서 이 코드를 실행하거나 다른 환경에서 코드를 사용할 수 있습니다.   
{: shortdesc}

{{site.data.keyword.openwhisk}}에서 이 코드를 실행하려면 다음을 수행하십시오.

1. [{{site.data.keyword.openwhisk}}에서 조치](/docs/openwhisk/index.html#getting-started)를 작성하십시오.
2. 다음 코드를 사용하여 GitHub 문제를 자동으로 작성하십시오. 

```

    const {promisify} = require('bluebird');
    const request = promisify(require('request'));
    const jwtVerify = promisify(require('jsonwebtoken').verify);
    const jwtDecode = require('jsonwebtoken').decode;

    const personal_github_token = "<PERSONAL_GITHUB_TOKEN>";

    /**
     * Returns the expiration data as short date string
     * @param time
     * @returns {string}
    */
    function calcDays(time) {
        const date = new Date(time);
        return date.toDateString();
    }

    /**
     * Creates the issue body string
     * @param data
     * @returns {string}
     */
    function createBody(data) {
        return `The following certificates will expire at ${calcDays(data.expiry_date)}:
     ${data.expiring_certificates.reduce((accumulator, currentValue) => {
            return accumulator + `
    > Domain(s): ${currentValue.domains}
    CRN: ${currentValue.cert_crn}
    `;
        }, "")}`
    }

    /**
     * Gets the notification body and creates a Github issue
     * @param params
     * @returns {Promise}
     */
    async function githubIssueCreator(params) {
        // Decode message to get information
        const data = jwtDecode(params.data);
        try {
            // Create request options to get the public key for verification
            const keysOptions = {
                method: 'GET',
                url: `https://<CERTIFICATE_MANAGER_CLUSTER_BASE_URL>/api/v1/instances/${encodeURIComponent(data.instance_crn)}/notifications/publicKey`
            };

            // Send request to get the public key
            const keysResponse = await request(keysOptions);

            // Verify the data using the acquired public key
            await jwtVerify(params.data, JSON.parse(keysResponse.body).publicKey);

            // Create request options to send a new issue to Github
            // Based on Github API - https://developer.github.com/v3/issues/#create-an-issue
            const gitOptions = {
                method: 'POST',
                url: 'https://api.github.com/repos/<REPO_OWNER>/<REPO_NAME>/issues',
                headers:
                    {
                        'cache-control': 'no-cache',
                        'content-type': 'application/json',
                        authorization: 'Token 55fbe9a7e6776c9425a528783cc9755b5a0f2bb5'
                    },
                json:
                    {
                        title: "Certificates about to expire",
                        body: createBody(data),
                        labels: ['certificates']
                    }
            };
            // Send request to Github
            await request(gitOptions);
        } catch (err) {
            console.log(err);
            return Promise.reject({
                statusCode: 500,
                headers: {'Content-Type': 'application/json'},
                body: {message: 'Error processing your request'},
            });
        }

    }


    exports.main = githubIssueCreator;

```
{: codeblock}
    
기타 REST API 명령은 [API 문서](https://console.bluemix.net/apidocs/cloudcerts)를 참조하십시오.
{: tip}


## 알림 채널 구성
{: #adding-channel}

Slack 웹훅 또는 콜백 URL을 작성한 후 {{site.data.keyword.cloudcerts_short}}에 이를 추가하여 만료되는 인증서에 대한 알림을 받기 시작합니다. {{site.data.keyword.cloudcerts_short}}는 엔드포인트를 암호화하고 안전하게 보관합니다.
{: shortdesc}

알림 채널을 추가하려면 다음을 수행하십시오.

1. 서비스 세부사항 페이지의 탐색에서 **설정**을 클릭하십시오. 
2. **알림** 탭을 여십시오.
3. **알림 채널 추가**를 클릭하십시오. 
4. 사용할 알림 채널의 유형을 선택하십시오. 
5. 알림을 전송할 웹훅 또는 콜백 URL을 입력하십시오.
6. **저장**을 클릭하십시오. 구성의 요약이 표시됩니다. 

   출력 예제: 
   <table>
   <caption> 알림 채널에 대한 정보</caption>
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
    <td>테스트 알림을 구성한 채널에 전송합니다.</td>
   </tr>
    <tr>
      <td>점으로 구성된 메뉴</td>
      <td>채널에 수행할 수 있는 사용 가능한 조치: <i>편집</i> 또는 <i>삭제</i></td>
    </tr>
    </tbody>
    </table>
   
    Slack 웹훅을 저장할 때 {{site.data.keyword.cloudcerts_short}}는 구성한 Slack 채널에 자동으로 확인 알림을 전송합니다. 이 알림을 받았는지 확인하려면 Slack 채널을 검사하십시오.
    {: tip}
7. 선택사항: 더 많은 알림 채널을 추가하려면 이 단계를 반복하십시오. 

## 알림 채널 테스트
{: #testing-channel}

알림 채널이 올바르게 구성되었는지 확인하도록 알림 채널을 테스트할 수 있습니다.
{: shortdesc}

시작하기 전에 [알림 채널을 구성](#adding-channel)하십시오. 

알림 채널을 테스트하려면 다음을 수행하십시오. 

1. 서비스 세부사항 페이지의 탐색에서 **설정**을 클릭하십시오. 
2. 알림 채널을 찾고 **테스트 연결**을 클릭하십시오.
3. 구성한 채널에서 알림을 받았는지 확인하십시오. 


## 알림 채널 업데이트
{: updating-channel}

알림 채널 구성을 업데이트하거나, 알림을 사용 또는 사용 안함으로 설정하거나, {{site.data.keyword.cloudcerts_short}}에서 알림 채널을 삭제할 수 있습니다.
{: shortdesc}

시작하기 전에 [알림 채널을 구성](#adding-channel)하십시오. 

1. 서비스 세부사항 페이지의 탐색에서 **설정**을 클릭하십시오. 
2. **알림** 탭을 선택하십시오.  
3. 다음 옵션 중에서 선택하십시오. 
   - 채널에 대한 알림을 사용 안함 또는 사용으로 설정하려면 스위치를 **사용 안함** 또는 **사용**으로 설정하십시오. 
   - 채널에 대한 설정을 업데이트하려면 조치 메뉴에서 **편집**을 선택하십시오.
   - 알림 채널을 삭제하려면 조치 메뉴에서 **삭제**를 선택하십시오. 
   
   
## 콜백 URL에 대한 HTTP 페이로드 확인
{: #verify-callback}

{{site.data.keyword.cloudcerts_short}}에서 콜백 URL로 전송된 모든 HTTP 페이로드는 비대칭 키 쌍을 사용하여 JWT 표준에 따라 자동으로 서명됩니다.  
{: shortdesc}

모든 {{site.data.keyword.cloudcerts_short}} 인스턴스에 대해 기타 {{site.data.keyword.cloudcerts_short}} 인스턴스에서 공유되지 않는 개인 및 공개 키가 생성됩니다. 개인 키는 HTTP 페이로드를 서명하는 데 사용되고 공개 키를 사용하여 페이로드가 {{site.data.keyword.cloudcerts_short}}로 생성되고 써드파티에 의해 변경되지 않는지 확인할 수 있습니다.

공용 키를 다운로드하려면 다음을 수행하십시오.

1. 서비스 세부사항 페이지의 탐색에서 **설정**을 클릭하십시오.
2. **알림** 탭을 여십시오.
3. **다운로드 키** 단추를 클릭하십시오. 키는 PEM 파일로 다운로드됩니다.

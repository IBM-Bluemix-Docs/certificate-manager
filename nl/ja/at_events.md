---

copyright:
  years: 2018
lastupdated: "2018-06-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# {{site.data.keyword.cloudaccesstrailshort}} イベント  
{: #at_events}

ユーザーおよびアプリケーションが {{site.data.keyword.Bluemix}} 内の {{site.data.keyword.cloudcerts_long}} サービスとどのように対話するのかを {{site.data.keyword.cloudaccesstrailfull}} サービスを使用してトラッキングします。{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} サービスは、{{site.data.keyword.Bluemix_notm}} 内のサービスの状態を変更するユーザー開始アクティビティーを記録します。詳しくは、[{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla)を参照してください。例えば、証明書をインポートすると、{{site.data.keyword.cloudaccesstrailshort}} イベントが生成されます。

次の表に、呼び出されたときにイベントを生成する API メソッドのリストを示します。

<table>
  <caption>イベントを生成するアクション</caption>
  <tr>
    <th>アクション</th>
	  <th>説明</th>
  </tr>
  <tr>
    <td>cloudcerts.instance.create</td>
	  <td>{{site.data.keyword.cloudcerts_short}} インスタンスをプロビジョンします。</td>
  </tr>
  <tr>
    <td>cloudcerts.instance.delete</td>
	  <td>{{site.data.keyword.cloudcerts_short}} インスタンスを削除します。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.import</td>
	  <td>サード・パーティーの認証局によって発行された証明書をインポートします。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.read</td>
	  <td>証明書をダウンロードします。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.list</td>
	  <td>証明書をリストします。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.list</td>
	  <td>証明書メタデータをリストします。証明書の詳細を表示します。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.search</td>
	  <td>証明書を検索します。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.search</td>
	  <td>証明書メタデータを検索します。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.delete</td>
	  <td>証明書を削除します。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.update</td>
	  <td>証明書を更新します。例えば、証明書の説明を変更します。</td>
  </tr>
</table>


 	
 


## イベントの検索先
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} イベントは、イベントが生成される {{site.data.keyword.Bluemix_notm}} 地域内にある {{site.data.keyword.cloudaccesstrailshort}} **アカウント・ドメイン**で使用可能です。

{{site.data.keyword.cloudaccesstrailshort}} イベントは、{{site.data.keyword.cloudcerts_short}} サービスがプロビジョンされている同じ地域内の {{site.data.keyword.cloudaccesstrailshort}} サービスに自動的に転送されます。


## 追加情報
{: #info}

「*requestData_str*」フィールドには、証明書の、人が判読できる名前が含まれます。




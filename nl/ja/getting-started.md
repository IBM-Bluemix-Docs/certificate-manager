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

# 入門チュートリアル
{: #getting-started}

{{site.data.keyword.cloudcerts_full}} は、{{site.data.keyword.cloud_notm}} ベース・アプリ用の SSL 証明書の取得、保管、管理を支援します。  
最初に、以下のステップを実行して、新しい {{site.data.keyword.cloudcerts_short}} サービス・インスタンスを作成します。
{: shortdesc}

{{site.data.keyword.cloud_notm}} コンソールからインスタンスを作成するには、以下のようにします。

1.	{{site.data.keyword.cloud_notm}} カタログで、**{{site.data.keyword.cloudcerts_short}}** を選択します。
2.	サービス・インスタンスに名前を付けます。または、事前設定された名前を使用します。
3.	**「作成」**をクリックします。
4.	組織の証明書を **{{site.data.keyword.cloudcerts_short}}** にインポートするには、**「証明書のインポート (Import Certificate)」**をクリックします。
5.	新規証明書を注文するには、**「証明書の注文 (Order Certificate)」**をクリックします。

<br/>
[{{site.data.keyword.cloud_notm}} CLI](https://cloud.ibm.com/docs/cli?topic=cloud-cli-ibmcloud-cli) からインスタンスを作成するには、以下のようにします。

1. {{site.data.keyword.cloud_notm}} にログインして、画面の指示に従います。

   ```
   ibmcloud login
   ```

2. インスタンスを作成します。

   ```
   ibmcloud resource service-instance-create "My Certificate Manager instance" cloudcerts free us-south
   ```

   - **「My Certificate Manager instance」**を、選択したインスタンス名で置き換えます。
   - **us-south** を **us-south** (ダラス)、**eu-gb** (ロンドン)、**eu-de** (フランクフルト)、または **jp-tok** (東京) で置き換えます。

<br/>
{{site.data.keyword.cloudcerts_short}} によって可能な内容についての[詳細を確認したり](/docs/services/certificate-manager?topic=certificate-manager-about-certificate-manager#about-certificate-manager)、開発段階にある {{site.data.keyword.cloudcerts_short}} を強化するために、[{{site.data.keyword.IBM_notm}} Developer でユーザー・フィードバックを提供したり](/docs/services/certificate-manager?topic=certificate-manager-troubleshooting#getting-help-and-support)します。 サービスの新しい内容を確認するには、[リリース・ノート](/docs/services/certificate-manager?topic=certificate-manager-release-notes#release-notes)を参照してください。
{: note}

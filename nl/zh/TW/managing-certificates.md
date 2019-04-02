---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-07"

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

# 從儀表板管理憑證
{: #managing-certificates-from-the-dashboard}

您可以使用 {{site.data.keyword.cloudcerts_full}} 服務儀表板，來管理您從協力廠商發證者取得以與 {{site.data.keyword.IBM_notm}} 雲端型應用程式或服務搭配使用的憑證。在您匯入憑證及金鑰之後，服務就會對其進行加密及儲存。
{: shortdesc}

## 匯入憑證
{: #importing-a-certificate}

匯入憑證以便可以進行管理。
{: shortdesc}

## 支援的憑證格式及公開金鑰演算法
{: supported-formats-and-algorithms}

### 憑證格式
* PEM

### 公開金鑰演算法
* Rivest-Shamir-Adleman (RSA)
* 數位簽章演算法 (DSA)
* 橢圓曲線數位簽章演算法 (ECDSA)
* 橢圓曲線及 Diffie-Hellman 金鑰協定通訊協定 (ECDH)

**開始之前**

* 建立有效、使用相符私密金鑰（金鑰為選用的）的未到期憑證。
* 將檔案轉換成「隱私權加強電子郵件 (PEM)」格式。
* 將私密金鑰保持未加密，確保可以將它匯入。

若要匯入憑證，請按一下**匯入憑證**，並提供下列詳細資料：

1. 輸入顯示名稱。
2. 按一下**瀏覽**來選取 PEM 格式的憑證檔案。
3. 選用項目：按一下**瀏覽**來選取 PEM 格式的憑證私密金鑰。
4. 適用時，提供 PEM 格式的中繼憑證檔。
5. 選用項目：輸入說明。
6. 按一下**匯入**。

在您匯入憑證之後，會在「憑證」表格中顯示下列資訊。若要檢視憑證的相關資訊，您可以在「憑證」表格中展開憑證的列。

<table>
<caption> 表 1. 所匯入憑證的相關資訊</caption>
  <tr>
    <th> 元件</th>
    <th> 說明</th>
  </tr>
  <tr>
    <td>名稱</td>
    <td>有意義的顯示名稱。長度上限為 256 個字元。</td>
  </tr>
  <tr>
    <td>說明</td>
    <td>（選用）憑證的說明文字。長度上限為 1024 個字元。</td>
  </tr>
  <tr>
    <td>網域</td>
    <td>憑證有效的網域。</td>
  </tr>
  <tr>
    <td>發證者</td>
    <td>已發出憑證的憑證管理中心 (CA)。</td>
  </tr>
  <tr>
    <td>演算法</td>
    <td>憑證簽章演算法。</td>
  </tr>
  <tr>
    <td>金鑰演算法</td>
    <td>公開金鑰演算法</td>
  </tr>
  <tr>
    <td>到期於</td>
    <td>憑證不再有效之前的剩餘天數。</td>
  </tr>
  <tr>
    <td>有效起始時間</td>
    <td>憑證生效的日期（UTC 時區）。</td>
  </tr>
  <tr>
    <td>到期日期</td>
    <td>憑證不再有效的日期（UTC 時區）。</td>
  </tr>
  <tr>
    <td>憑證 ID</td>
    <td>匯入時提供給憑證的已產生 ID。</td>
  </tr>
</table>

</br>

## 重新匯入憑證
{: #reimport-certificate}

如果您的憑證即將到期，您可以藉由匯入新版憑證來更新憑證，此新版憑證具有與現有憑證相同的網域，但具有新的到期日。重新匯入憑證時，憑證的現有版本會保留作為備份，必要時可以下載該備份。
{: shortdesc}

### 重新匯入憑證
{: #reimporting-certificate}

若要重新匯入憑證，請完成下列步驟：

1. 展開憑證的列。
2. 按一下**重新匯入憑證**。
3. 按一下**瀏覽**來選取 PEM 格式的新憑證檔案。
4. （選用）按一下**瀏覽**來選取 PEM 格式的新憑證私密金鑰。
5. （選用）按一下**瀏覽**來提供 PEM 格式的新中繼憑證檔案。
6. 按一下**重新匯入**，然後按一下**完成**。

重新匯入憑證限制為每分鐘只能執行五個動作。
{: note}

### 下載舊版的憑證
{: #downloading-certificate}

若要擷取舊版憑證，請完成下列步驟：

1. 展開憑證的列。
2. 按一下**舊版**鏈結。

## 搜尋憑證
{: #searching-certificates}

如果您管理許多憑證，則可以使用搜尋列來找到必要憑證。
{: shortdesc}

* 若要搜尋憑證名稱、憑證網域或憑證發證者，請在「搜尋列」中鍵入搜尋詞彙，然後按 Enter 鍵。
* 若要檢視所有憑證，請按一下「搜尋列」中的 **X** 圖示。

## 下載憑證
{: #downloading-certificates}

當您準備好將憑證部署至應用程式或服務時，可以下載憑證及相關聯私密金鑰。
{: shortdesc}

若要下載憑證，請完成下列步驟：

1. 選取您要下載之憑證的勾選框。
2. 按一下**下載憑證**。根據匯入至服務的內容，您會收到包含憑證之 PEM 檔案的壓縮檔、相關聯私密金鑰及相關聯中繼憑證。

## 刪除憑證
{: #deleting-certificates}

如果您要停止追蹤憑證，則可以刪除它。
{: shortdesc}  

若要刪除憑證，請完成下列步驟：

1. 選取您要刪除之憑證的勾選框。
2. 按一下**垃圾桶**圖示。

## 更新憑證 meta 資料
{: #updating-certificates-metadata}

您也可以更新憑證的名稱及說明。
{: shortdesc}

若要更新憑證，請完成下列步驟：

1. 選取列，以開啟該憑證的詳細資料。
2. 更新名稱或說明。
3. 儲存變更。

您每分鐘最多可以執行五個更新動作。
{: note}

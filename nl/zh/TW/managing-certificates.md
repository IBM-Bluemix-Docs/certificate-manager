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

# 在 GUI 中管理憑證
{: #managing-certificates-ui}

您可以使用 {{site.data.keyword.cloudcerts_full}} 服務 GUI，來管理您從協力廠商發證者取得以與 {{site.data.keyword.IBM_notm}} 雲端型應用程式或服務搭配使用的憑證。在您匯入憑證及金鑰之後，服務就會對其進行加密及儲存。
{: shortdesc}

## 匯入憑證
{: #importing-a-certificate}

為了協助您管理憑證，您可以上傳它們。
{: shortdesc}

開始之前：

* 使用相符的私密金鑰，建立有效且未到期的憑證。
* 將檔案轉換成「隱私權加強電子郵件 (PEM)」格式。
* 將私密金鑰保持未加密，確保可以將它匯入。

若要匯入憑證，請按一下**匯入憑證**，並提供下列詳細資料：

1. 選用項目：輸入顯示名稱。
2. 按一下**瀏覽**，並選取 PEM 格式的憑證檔。
3. 按一下**瀏覽**，並選取 PEM 格式的憑證私密金鑰。
4. 適用時，提供 PEM 格式的中繼憑證檔。
5. 選用項目：輸入說明。
6. 按一下**匯入**。  

**附註**：若要更新所匯入的憑證，請從憑證管理中心 (CA) 取得新憑證，並將新的憑證匯入至 {{site.data.keyword.cloudcerts_short}}。部署新的憑證之後，即可刪除舊的憑證。

在您匯入憑證之後，會在「憑證」表格中顯示下列資訊。若要檢視其他憑證資訊，您可以選取表格列中的憑證。

<table>
<caption> 表 1. 所匯入憑證的相關資訊</caption>
  <tr>
    <th> 元件</th>
    <th> 說明</th>
  </tr>
  <tr>
    <td>名稱</td>
    <td>選用項目：顯示名稱。</td>
  </tr>
  <tr>
    <td>說明</td>
    <td>選用項目：憑證的說明文字。</td>
  </tr>
  <tr>
    <td>網域</td>
    <td>憑證有效的網域。</td>
  </tr>
  <tr>
    <td>發證者</td>
    <td>已發出憑證的 CA。</td>
  </tr>
  <tr>
    <td>演算法</td>
    <td>用來建立憑證的加密類型。</td>
  </tr>
  <tr>
    <td>金鑰演算法</td>
    <td>演算法所使用的金鑰類型及大小。</td>
  </tr>
  <tr>
    <td>到期於</td>
    <td>憑證不再有效之前的剩餘天數。</td>
  </tr>
  <tr>
    <td>發出日期</td>
    <td>發出憑證的日期。</td>
  </tr>
  <tr>
    <td>有效起始時間</td>
    <td>憑證變成有效的日期。</td>
  </tr>
  <tr>
    <td>到期日期</td>
    <td>憑證不再有效的日期。</td>
  </tr>
  <tr>
    <td>憑證 ID</td>
    <td>匯入時提供給憑證的已產生 ID。</td>
  </tr>
</table>

## 搜尋憑證
{: #searching-certificates}
 
如果您管理許多憑證，則可以使用搜尋列來找到必要憑證。
{: shortdesc}
 
-   若要搜尋憑證名稱、憑證網域或憑證發證者，請在「搜尋列」中鍵入搜尋詞彙，然後按 Enter 鍵。
-   若要檢視所有憑證，請按一下「搜尋列」中的 **X** 圖示。

## 下載憑證
{: #downloading-certificates}

當您準備好將憑證部署至應用程式或服務時，可以下載憑證及相關聯私密金鑰。
{: shortdesc}

若要下載憑證，請執行下列動作：

1. 選取您要下載之憑證的勾選框。
2. 按一下**下載憑證**。根據匯入至服務的內容，您會收到包含憑證之 PEM 檔案的壓縮檔、相關聯私密金鑰及相關聯中繼憑證。


## 刪除憑證
{: #deleting-certificates}

如果您要停止追蹤憑證，則可以刪除它。
{: shortdesc}  

若要刪除憑證，請執行下列動作：

1. 選取您要刪除之憑證的勾選框。
2. 按一下**垃圾桶**圖示。

## 更新憑證 meta 資料
{: #updating-certificates-metadata}

您也可以更新憑證的名稱及說明。
{: shortdesc}

若要更新憑證，請執行下列動作：

1. 選取列，以開啟該憑證的詳細資料。
2. 更新名稱或說明。
3. 儲存變更。

**附註**：您每分鐘最多可以執行 5 個更新動作。

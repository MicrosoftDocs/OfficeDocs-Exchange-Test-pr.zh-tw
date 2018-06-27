---
title: 'Exchange 2013 中的 Exchange 系統管理中心: Exchange 2013 Help'
TOCTitle: Exchange 2013 中的 Exchange 系統管理中心
ms:assetid: a9aea11a-6ba3-4f4a-a76e-79072e7cfc7d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150562(v=EXCHG.150)
ms:contentKeyID: 50473947
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 中的 Exchange 系統管理中心

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-17_

Exchange 系統管理中心 (EAC) 是 Microsoft Exchange Server 2013 中的 Web 管理主控台，可針對內部部署、線上和混合 Exchange 部署最佳化。EAC 取代了 Exchange 管理主控台 (EMC) 和 Exchange 控制台 (ECP)，這兩個介面用來管理 Exchange Server 2010。

Web 式 EAC 的優點之一是讓您可從 ECP IIS 虛擬目錄內分割網際網路與內部網路存取。利用此功能，您可以控制是否允許使用者從組織外部透過網際網路存取 EAC，同時讓終端使用者存取 Outlook Web App 選項。如需詳細資訊，請參閱[關閉 Exchange 系統管理中心存取](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md)。

在尋找本主題的 Exchange Online 版本嗎？請參閱[Exchange Online 中的 Exchange 系統管理中心](https://technet.microsoft.com/zh-tw/library/jj200743\(v=exchg.150\))。

尋找本主題的 Exchange Online Protection 版本嗎？請參閱[Exchange Online Protection 中的 Exchange 系統管理中心](https://technet.microsoft.com/zh-tw/library/jj723141\(v=exchg.150\))。

內容

存取 EAC

EAC 中常見的使用者介面元素

支援的瀏覽器

## 存取 EAC

由於 EAC 現在是 Web 管理主控台，因此您將需要使用 ECP 虛擬目錄 URL 才能從網頁瀏覽器存取它。在大多數情況下，EAC 的 URL 類似於下：

  - **內部 URL：`https://<CASServerName>/ecp`**   內部 URL 用來從組織防火牆內存取 EAC。

  - **外部 URL：`https://mail.contoso.com/ecp`**   外部 URL 用來從組織防火牆外存取 EAC。有些組織可能想要關閉 EAC 的外部存取。如需詳細資料，請參閱[關閉 Exchange 系統管理中心存取](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md)。

若要尋找 EAC 的內部或外部 URL，您可以使用 [Get-EcpVirtualDirectory](https://technet.microsoft.com/zh-tw/library/dd351058\(v=exchg.150\)) Cmdlet。如需詳細資料，請參閱[尋找內部和外部 Url 的 Exchange 系統管理中心](find-the-internal-and-external-urls-for-the-exchange-admin-center-exchange-2013-help.md)。

如果您屬於共存案例，也就是 Exchange Server 2010 和 Exchange Server 2013 位於同一個組織內，而且您的信箱仍位於 Exchange 2010 信箱伺服器上，則瀏覽器將預設為 Exchange 2010 ECP。您可以藉由將 Exchange 版本新增至 URL 來存取 EAC。例如，若要存取虛擬目錄裝載於用戶端存取伺服器 CAS15-NA 上的 EAC，請使用下列 URL：`https://CAS15-NA/ecp/?ExchClientVer=15`。相反地，如果您要存取 Exchange 2010 ECP，而且您的信箱位於 Exchange 2013 信箱伺服器上，則使用下列 URL：`https://CAS14-NA/ecp/?ExchClientVer=14`

## EAC 中常見的使用者介面元素

本節描述整個 EAC 中常見的使用者介面元素。

![Exchange 系統管理中心](images/JJ150562.cd617bc0-19ef-47d2-bba1-4e9546b12e0c(EXCHG.150).gif "Exchange 系統管理中心")

## 跨單位導覽

跨單位導覽可讓您在 Exchange Online 與內部部署 Exchange 部署之間輕鬆切換。如果您沒有 Exchange Online 組織，則連結會將您導向 Office 365 註冊頁面。若要深入了解，請參閱 [Exchange Server 混合部署](https://technet.microsoft.com/zh-tw/library/jj200581\(v=exchg.150\))。

## 功能窗格

這是您在 EAC 中執行大部分工作時的第一個導覽層級。功能窗格類似 Exchange 2010 中 EMC 的主控台樹狀結構。不過在 Exchange 2013 中，功能窗格與伺服器角色相反，是依功能區域組織，能以較少的點選次數找到您需要的項目。

  - **收件者：**這是您管理信箱、群組、資源信箱、連絡人、共用信箱以及信箱遷移與移動的所在位置。

  - **權限：**這是您管理系統管理員角色、使用者角色和 Outlook Web App 原則的所在位置。

  - **規範管理：**這是您管理就地 eDiscovery、就地保留、稽核、資料遺失防護 (DLP)、保留原則、保留標記和日誌規則的所在位置。

  - **組織：**這是您管理 Exchange 組織相關工作的所在位置，包括同盟共用、Outlook App 和通訊清單。

  - **保護：**這是您管理組織的反惡意程式碼保護的所在位置。

  - **郵件流程：**這是您管理規則、傳遞回報、公認的網域、電子郵件地址原則，以及傳送和接收連接器的所在位置。

  - **行動電話：**這是您管理可連線到組織之行動裝置的所在位置。您可以管理行動裝置存取和行動裝置信箱原則。

  - **公用資料夾：**在 Exchange 2010 中，您必須使用 \[公用資料夾管理主控台\] (位於 \[工具箱\] 中的 EMC 外部) 來管理公用資料夾。在 Exchange 2013 中，公用資料夾可以直接從 \[公用資料夾\] 功能區內進行管理。

  - **整合通訊：**這是您管理 UM 撥號對應表和 UM IP 閘道的所在位置。

  - **伺服器：**這是您管理信箱伺服器和用戶端存取伺服器、資料庫、資料庫可用性群組 (DAG)、虛擬目錄及憑證的所在位置。

  - **混合：**這是您設立及設定混合組織的所在位置。

## 索引標籤

索引標籤是您的第二個導覽層級。每一個功能區都包含不同的索引標籤，各自代表一項完整功能。此規則唯一的例外是 \[混合\] 功能區。您必須先使用混合組態精靈啟用組織進行混合部署。

## 工具列

按一下大部分的索引標籤時，會看到一個工具列。工具列上的圖示會執行特定動作。下表描述最常見的圖示及其動作。若要顯示與圖示關聯的動作，只要將游標置於圖示上方即可。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>圖示</th>
<th>名稱</th>
<th>動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="加入圖示" alt="加入圖示" /></p></td>
<td><p>新增</p></td>
<td><p>使用此圖示來建立新的物件。這些圖示中有些擁有一個關聯的向下箭號，您可以按一下以顯示所能建立的其他物件。例如，在 [收件者] &gt; [信箱] 中，按一下向下箭號會顯示 [使用者信箱] 和 [連結的信箱] 作為額外選項。</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編輯圖示" alt="編輯圖示" /></p></td>
<td><p>編輯</p></td>
<td><p>使用此圖示來編輯物件。</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif" title="刪除圖示" alt="刪除圖示" /></p></td>
<td><p>刪除</p></td>
<td><p>使用此圖示來刪除物件。部分刪除圖示擁有一個向下箭號，您可以按一下以顯示額外選項。</p></td>
</tr>
<tr class="even">
<td><p><img src="images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif" title="搜尋圖示" alt="搜尋圖示" /></p></td>
<td><p>搜尋</p></td>
<td><p>使用此圖示來開啟搜尋方塊，您可在此處輸入想要尋找之物件的搜尋字詞。如需其他搜尋選項，請參閱<a href="https://technet.microsoft.com/zh-tw/library/jj156853(v=exchg.150)">[收件者 &gt;]進階的搜尋</a>。</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="重新整理圖示" alt="重新整理圖示" /></p></td>
<td><p>重新整理</p></td>
<td><p>使用此圖示來重新整理清單檢視。</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="更多選項圖示" alt="更多選項圖示" /></p></td>
<td><p>更多選項</p></td>
<td><p>使用此圖示來檢視更多可對該索引標籤之物件執行的動作。例如，在 [收件者] &gt; [信箱] 中按一下此圖示，會顯示下列選項：[停用]、[新增/移除欄位]、[將資料匯出到 CSV 檔案]、[連線信箱] 和 [進階搜尋]。</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif" title="向上箭號圖示" alt="向上箭號圖示" />   <img src="images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif" title="向下箭號圖示" alt="向下箭號圖示" /></p></td>
<td><p>向上鍵和向下鍵</p></td>
<td><p>使用這些圖示向上或向下移動物件的優先順序。例如在 [郵件流程] &gt; [電子郵件地址原則] 中，按一下向上箭號即可提高電子郵件地址原則的優先順序。您也可以使用這些箭號來導覽公共資料夾階層，以及在清單檢視中向上或向下移動規則。</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif" title="複製圖示" alt="複製圖示" /></p></td>
<td><p>複製</p></td>
<td><p>使用此圖示來複製物件，以便在不變更原始物件的情況下改變其內容。例如在 [權限] &gt; [管理員角色] 中，從清單檢視中選取一個角色，然後按一下此圖示，即可依據現有的角色群組來建立新的角色群組。</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif" title="[移除] 圖示" alt="[移除] 圖示" /></p></td>
<td><p>移除</p></td>
<td><p>使用此圖示來移除清單中的項目。例如，在 [公用資料夾權限] 對話方塊中，您可以選取使用者並按一下此圖示，從允許存取公用資料夾的使用者清單中移除該使用者。</p></td>
</tr>
</tbody>
</table>


## 清單檢視

當您選取索引標籤時，大部分情況下會看見清單檢視。EAC 中的清單檢視已設計為移除 ECP 中存在的限制。ECP 過去限制顯示最多 500 個物件，如果您要檢視未列於詳細資料窗格中的物件，就必須使用搜尋和篩選選項來尋找這些特定物件。在 Exchange 2013 中，從 EAC 清單檢視內可檢視的限制約為 20,000 個物件 (用於內部部署)，而在 Exchange Online 則約為 10,000 個物件。此外，也包括分頁功能，所以你可以將結果分頁顯示。在 \[收件者\] 清單檢視中，您也可以設定頁面大小並將資料匯出到 CSV 檔案。

## 詳細資料窗格

當您從清單檢視中選取物件時，該物件的相關資訊就會顯示在詳細資料窗格中。在部分情況下 (例如收件者物件)，詳細資料窗格可以進行快速管理工作。例如，如果您瀏覽至 \[收件者\] \> \[信箱\]，並從清單檢視中選取一個信箱，則詳細資料窗格會顯示一個選項讓您可以啟用或停用該信箱的封存。詳細資料窗格也可用來大量編輯數個物件。只要按住 CTRL 鍵、選取您要大量編輯的物件，然後使用詳細資料窗格中的選項即可。例如，選取多個信箱可讓您大量更新使用者的連絡人和組織資訊、自訂屬性、信箱配額、Outlook Web App 設定，以及其他項目。

## 通知

EAC 包含一個通知檢視器，會顯示長時間執行之程序的狀態，並會在程序完成時發出通知。此外，對於特別長時間執行的程序 (例如移動要求)，您可以選擇加入以接收電子郵件通知。

## 自有磚與說明

\[自有磚\] 可讓您登出 EAC，然後以不同使用者的身分登入。您可以從\[說明\]![說明圖示](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "說明圖示") 下拉式功能表執行下列動作：

  - **說明：**按一下 ![說明圖示](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "說明圖示") 即可檢視線上說明內容。

  - **停用說明泡泡圖**   \[說明泡泡圖\] 會在您建立或編輯物件時，顯示欄位的內容說明。您可以關閉 \[說明泡泡圖\]，或是在停用的狀態下將它開啟。

  - **著作權和隱私權：**按一下隱私權或著作權連結，即可閱讀 Exchange 2013 的著作權和隱私權資訊。

## 支援的瀏覽器

為獲得 EAC 的最佳經驗，請使用標示為 "Premium" 的其中一種作業系統與瀏覽器的組合。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不支援上表中未列出的其他作業系統和瀏覽器組合，包括觸控式。</td>
</tr>
</tbody>
</table>


  - **Premium：**所有操作功能都受到支援且經過完整測試。

  - **支援：**具有與 Premium 相同的操作功能支援。但是，支援的瀏覽器將不會有瀏覽器與作業系統組合不支援的功能。

  - **不支援：**不支援瀏覽器和作業系統或未經過測試。


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Web 瀏覽器</p></td>
<td><p>Windows XP 及 Windows Server 2003</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows 7 和 Windows Server 2008</p></td>
<td><p>Windows 8 和 Windows Server 2012</p></td>
<td><p>Mac OSX</p></td>
<td><p>Linux</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>Premium</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>Premium</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10 或更新版本</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="odd">
<td><p>Firefox 11 或更新版本</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>支援</p></td>
</tr>
<tr class="even">
<td><p>Safari 5.1 或更新版本</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
<td><p>Premium</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="odd">
<td><p>Chrome 18 或更新版本</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>不支援</p></td>
</tr>
</tbody>
</table>


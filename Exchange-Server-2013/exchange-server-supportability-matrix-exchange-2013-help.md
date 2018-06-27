---
title: 'Exchange Server Supportability Matrix: Exchange 2013 Help'
TOCTitle: Exchange Server Supportability Matrix
ms:assetid: dbac2d40-da8b-469f-a265-1d1f948fe446
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff728623(v=EXCHG.150)
ms:contentKeyID: 54652609
ms.date: 03/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server Supportability Matrix

 

_**適用版本：**Exchange Server 2007, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2018-03-20_

Exchange Server 支援性一覽表提供集中來源，可讓 Microsoft Exchange 系統管理員輕鬆找到所有 Microsoft Exchange 版本的任何組態或必要元件可用支援等級的相關資訊。

## 版本型號

下表列出每個 Exchange 支援版本的版本型號。版本型號以 X 字元識別。

若是 Exchange 2013 之前的 Exchange 版本，則每個更新彙總套件對整個產品而言都是累積性的。因此，如果您將更新彙總套件套用至 Exchange Server 2010，這等於套用了該更新彙總套件中所包含的所有修正。此套件包含每一個舊版的更新彙總套件所包含的所有修正。當建立舊版 Exchange 的更新或 Hotfix 建立時，更新中包含或 Hotfix 中包含的一或多個二進位檔就會累積。它們會一直累積關於檔案內容的更新，不過，它們不是隨著整個 Exchange 產品而累積。如需詳細資訊，請參閱＜[Exchange 2010 服務](https://go.microsoft.com/fwlink/p/?linkid=298627)＞。

在 Exchange 2013 中，我們改變了提供 Hotfix 和 Service Pack 的方式。不同於舊版 Exchange 所用的優先順序導向 Hotfix 發行和更新彙總模型，Exchange 2013 和更新版本現在遵守排程傳遞模型。在此模型中，累計更新每三個月發行一次。Exchange 2013 和更新版本的累計更新 (CU) 已發行為該 Exchange 版本的完全更新，類似於產品升級或 Service Pack 發行。如需新服務模型的詳細資訊，請參閱 [更新 Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>服務版本型號</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>累計更新</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>更新彙總套件</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>個別傳遞的安全性 Hotfix</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


## 支援週期

如需特定版本 Exchange 或 MicrosoftWindows 伺服器或用戶端作業系統支援週期的相關資訊，請參閱 [Microsoft 支援週期](https://go.microsoft.com/fwlink/p/?linkid=55839) 頁面。如需 Microsoft 支援週期的相關資訊，請參閱 [Microsoft 支援週期原則常見問題集](https://go.microsoft.com/fwlink/p/?linkid=158902)。

## Exchange Server 2007 週期結束

Exchange 2007 的支援已於 2017 年 4 月 11 日結束 (根據 [Microsoft 週期原則](https://go.microsoft.com/fwlink/p/?linkid=833210))。在此提醒，該日期之後，便不會有任何新的安全性更新、非安全性更新、免費或付費協助支援選項或線上技術內容更新。此外，隨著 Office 365 採用加速和雲端使用量增加，將無法使用 Office 產品的自訂支援選項。這包括 Exchange Server，以及 Office 套件、SharePoint Server、Office Communications Server、Lync Server、商務用 Skype Server、Project Server 和 Visio。Exchange 2007 的停止支援日期已到，我們鼓勵客戶完成其移轉和升級計劃。我們建議客戶利用 Microsoft 和 Microsoft 認證合作夥伴所提供的部署優點，包括適用於雲端移轉的 [Microsoft FastTrack](https://go.microsoft.com/fwlink/p/?linkid=238431)，以及適用於內部部署升級的[軟體保證部署和規劃服務](https://go.microsoft.com/fwlink/p/?linkid=833211)。

## 支援的作業系統平台

下表識別每個 Exchange 版本可在哪些作業系統平台上執行。支援的平台以 X 字元識別。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>下表中未列出的 Windows Server 和 Windows 用戶端版本不支援使用任何版本或發行的 Exchange。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>作業系統平台</th>
<th>Exchange 2016 CU3 和更新版本</th>
<th>Exchange 2016 CU2 和更新版本</th>
<th>Exchange 2013 SP1 和更新版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Vista SP2</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 SP2</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows 7 SP1</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
</tr>
<tr class="odd">
<td><p>Windows 8</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>Windows 8.1</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Windows 10</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p></p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


1只適用於 Exchange 管理工具

## 支援的 Active Directory 環境

下表識別每個 Exchange 版本可以與哪些 Active Directory 環境通訊。支援的環境以 X 字元識別。Active Directory 伺服器泛指可寫入的通用類別目錄伺服器或可寫入的網域控制站。不支援唯讀通用類別目錄伺服器和唯讀網域控制站。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>作業系統環境</th>
<th>Exchange 2016 CU3 和更新版本</th>
<th>Exchange 2016 CU2 和更新版本</th>
<th>Exchange 2013 SP1 和更新版本</th>
<th>Exchange 2010 SP3 RU5 或更新版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2003 SP2 Active Directory 伺服器</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 SP2 Active Directory 伺服器</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1 Active Directory 伺服器</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012 Active Directory 伺服器</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2 Active Directory 伺服器</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016 Active Directory 伺服器</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>樹系功能等級</th>
<th>Exchange 2016 CU3 和更新版本</th>
<th>Exchange 2016 CU2 和更新版本</th>
<th>Exchange 2013 SP1 和更新版本</th>
<th>Exchange 2010 SP3 RU5 或更新版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2003 樹系功能等級</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 樹系功能等級</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1 樹系功能層級</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012 樹系功能等級</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2 樹系功能等級</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016 樹系功能等級</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 支援在 Web 上與 Outlook Web App 或 Outlook Web Access 高階版本搭配使用的網頁瀏覽器

下表識別支援哪些網頁瀏覽器在 Web 上與 Outlook Web App 或 Outlook 高階版本搭配使用。支援的瀏覽器以 X 字元識別。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>瀏覽器</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 和更新版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Microsoft Edge 的目前版本</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Internet Explorer 的目前版本或前一版</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Firefox</p></td>
<td><p>Firefox 的目前版本或前一版</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="odd">
<td><p>Firefox 3.0.1 或更新版本</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Firefox 12 或更新版本</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Safari</p></td>
<td><p>Safari 的目前版本</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="even">
<td><p>Safari 3.1 或更新版本</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Safari 5.0 或更新版本</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome</p></td>
<td><p>Chrome 的目前版本</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="odd">
<td><p>Chrome 3.0.195 或更新版本</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome 18 或更新版本</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## 支援在 Web 上與 Outlook Web App 或 Outlook 基本版本搭配使用的網頁瀏覽器

下表識別支援哪些網頁瀏覽器在 Web 上與 Outlook Web App 或 Outlook 輕量 (基本) 版本搭配使用。支援的瀏覽器以 X 字元識別。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>支援在行動瀏覽器中使用 Outlook Web App Basic (Outlook Web App Light)。然而，如果行動瀏覽器中發生轉譯或驗證問題，請判斷問題能否透過在支援瀏覽器的完整用戶端中使用 Outlook Web App Light 加以重現。例如，在 Safari、Chrome 或 Internet Explorer 中測試 Outlook Web App Light 的使用。如果問題無法在完整用戶端中重現，我們建議您連絡行動裝置廠商以取得協助。在這類情況中，我們會視需要與廠商共同作業。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>瀏覽器</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Microsoft Edge 的目前版本</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Internet Explorer 的目前版本或前一版</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X<span></span></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Safari</p></td>
<td><p>Safari 的目前版本</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Firefox</p></td>
<td><p>Firefox 的目前版本或前一版</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome</p></td>
<td><p>Chrome 的目前版本</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="odd">
<td><p>Opera</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## 支援在 Web 上使用 S/MIME 與 Outlook Web App 或 Outlook 搭配的網頁瀏覽器

下表識別支援哪些網頁瀏覽器在 Web 上使用 S/MIME 與Outlook Web App 或 Outlook 高階版本搭配。支援的瀏覽器以 X 字元識別。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>瀏覽器</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 和更新版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Microsoft Edge 的目前版本</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Internet Explorer 的目前版本或前一版</p></td>
<td><p>N/A </p></td>
<td><p>N/A </p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## 用戶端

下表識別每個 Exchange 版本支援使用的信箱用戶端。支援的用戶端以 X 字元識別。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 和更新版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>X4</p></td>
<td><p>X2</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2016</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Office 365 的 Mac 版 Outlook</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Phone 7.5</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Phone 8</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Phone 8.1</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Mobile 10</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Entourage 2008 (EWS)</p></td>
<td><p>X3</p></td>
<td><p>X3</p></td>
<td><p>X3</p></td>
</tr>
</tbody>
</table>


1需要 Outlook 2007 Service Pack 3 和最新的公用更新。

2需要 Outlook 2010 Service Pack 1 和最新的公用更新。

3僅 EWS。Exchange 2010 沒有 DAV 支援。

4支援最新的 Office 服務套件和公用更新。

## 工具

下表識別可搭配 Microsoft Exchange 組織間複寫工具 (Exscfg.exe; Exssrv.exe) 使用的 Microsoft Exchange 版本。此工具用於在 Exchange 組織之間複寫公用資料夾資訊 (包括空閒/忙碌資訊)。如需詳細資訊，請參閱＜[Microsoft Exchange Server 組織間複寫](https://go.microsoft.com/fwlink/?linkid=22455)＞。支援的版本以 X 字元識別。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>工具</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 和更新版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織間複寫工具</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Microsoft .NET Framework

下表識別可與每個 Exchange 版本一起使用的 Microsoft.NET Framework 版本。支援的版本以 X 字元識別。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>下表中未列出的 .NET Framework 版本，在任何版本或發行的 Exchange 上皆不受支援。</strong>這包括 .NET Framework 次要和修補程式等級的版本。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您將 Exchange 從不受支援的 CU 升級至目前的 CU，且沒有中繼 CU 可供使用，則您應先升級至受 Exchange 支援的最新版 .NET，然後立即升級至目前的 CU。這個方法仍需將 Exchange 伺服器維持在最新版本以及最新支援的 CU。<br />
Microsoft 未主張使用此方法升級即不會失敗，您仍可能需要連絡 Microsoft 支援服務。</td>
</tr>
</tbody>
</table>



<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>.NET Framework</th>
<th>Exchange 2016 CU8</th>
<th>Exchange 2016 CU5 - CU7</th>
<th>Exchange 2013 CU19</th>
<th>Exchange 2013 CU16 - CU18</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>.NET Framework 3.5</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 3.5 SP1</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>.NET Framework 4.0</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1,2</p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 4.5</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1,2 </p></td>
</tr>
<tr class="odd">
<td><p>.NET Framework 4.6.2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 4.7.1</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


1 如果您使用 Windows Server 2012，則必須先安裝 .NET Framework 3.5 之後才能使用 Exchange 2010 SP3。

2Exchange 2010 只會使用 .NET .NET Framework 3.5 和 .NET .NET Framework 3.5 SP1 程式庫。如果.NET .NET Framework 4.5 程式庫未安裝在電腦上，則不會使用這些程式庫。我們支援安裝任何主要或次要版本的.NET .NET Framework 4.5 (例如，.NET .NET Framework 4.5.1, .NET .NET Framework 4.5.2，依此類推)，只要.NET .NET Framework 3.5 或.NET .NET Framework 3.5 SP1 也安裝在電腦上。

## Windows 管理架構

下表識別 Windows Management Framework 的版本，其包含可搭配每個 Exchange 版本使用的 Windows PowerShell 命令列介面。支援的版本以 X 字元識別。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows PowerShell</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows PowerShell 2.0</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows 管理架構</p></td>
<td><p>您要安裝 Exchange 的 Windows Server 版本中所內建的 Windows 管理架構版本。</p></td>
<td><p>您要安裝 Exchange 的 Windows Server 版本中所內建的 Windows 管理架構版本。</p></td>
<td><p>您要安裝 Exchange 的 Windows Server 版本中所內建的 Windows 管理架構版本。1</p></td>
</tr>
</tbody>
</table>


1Windows Management Framework 3.0 和 Windows Management Framework 4.0 可以用來在執行 Exchange 2010 SP3 RU5 或更新版本的電腦上執行作業系統相關管理工作。不過，Exchange 2010 Cmdlet 和 Exchange 2010 指令碼需要 Windows PowerShell 2.0。不支援使用 Exchange 2010 Cmdlet 和指令碼與 Windows Management Framework 3.0 或 Windows Management Framework 4.0 搭配。

## Microsoft Management Console

下表識別可搭配每個 Exchange 版本使用的 Microsoft Management Console (MMC) 版本。支援的版本以 X 字元識別。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>MMC</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 或更新版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MMC 3.0</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Windows Installer

下表識別和每一個 Exchange 版本搭配使用的 Windows Installer 版本。支援的版本以 X 字元識別。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows Installer</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 和更新版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Installer 4.5</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Installer 5.0</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


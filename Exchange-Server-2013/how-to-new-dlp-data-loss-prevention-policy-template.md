---
title: '從範本建立 DLP 原則: Exchange Online Help'
TOCTitle: 從範本建立 DLP 原則
ms:assetid: 4432ef8b-6108-48d3-b2af-43ef5b40d2bc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150515(v=EXCHG.150)
ms:contentKeyID: 50472274
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 從範本建立 DLP 原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-01-14_

在 Microsoft Exchange Server 2013 中，您可使用資料遺失防護 (DLP) 原則範本來協助達成組織的郵件原則及規範需要。這些範本包含預先建立的規則，可協助您管理與數個通用法律及監管要求關聯的郵件資料。若要查看由 Microsoft 提供的所有範本，請查看 [Exchange 中提供的 DLP 原則範本](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)。提供的 DLP 範本範例可協助您管理：

  - Gramm-Leach-Bliley Act (GLBA) 資料

  - 支付卡行業資料安全標準 (PCI DSS)

  - 美國個人識別資訊 (U.S. PII)

您可以自訂任何這些 DLP 範本或使用這些做為-是。DLP 原則範本是內建置於包含新的條件或述詞和動作的傳輸規則。DLP 原則支援完整傳統傳輸規則的範圍和您可以新增其他規則之後已建立的 DLP 原則。如需原則範本的詳細資訊，請參閱[DLP 原則範本](dlp-policy-templates-exchange-2013-help.md)。若要深入了解傳輸規則功能，請參閱[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013) 或[Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\)) (Exchange Online)。一旦啟動強制執行原則之後，您可以了解如何透過檢閱下列主題觀察結果：

Exchange 2013: [檢視 DLP 原則偵測報告](view-dlp-policy-detection-reports-exchange-2013-help.md)

Exchange Online: [檢視 \[Exchange Online\] 的 DLP 原則偵測報告](https://technet.microsoft.com/zh-tw/library/dn904484\(v=exchg.150\))

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在生產環境中執行 DLP 原則之前，您應先在測試模式中啟用這些原則。在這類測試期間，建議您設定範例使用者信箱，然後傳送叫用測試原則的測試郵件，以便確認結果。</td>
</tr>
</tbody>
</table>


從範本建立 DLP 原則相關的其他管理工作，請參閱[DLP 程序](dlp-procedures-exchange-2013-help.md)Exchange Server 2013或[\[Exchange Online\] 的 DLP 程序](https://technet.microsoft.com/zh-tw/library/jj938003\(v=exchg.150\))Exchange Online。

## 開始之前有哪些須知？

  - 預估完成時間：30 分鐘

  - 請確保[規劃及部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)中所述設定該Exchange 2013 。

  - 在組織中設定管理員及使用者帳號，並驗證基本郵件流程。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「資料遺失防護 (DLP)」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用 EAC 自範本設定 DLP 原則

1.  在 EAC 中，瀏覽至 \[規範管理\] \> \[資料遺失防護\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若按一下 [新增]<img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="加入圖示" alt="加入圖示" /> 圖示旁的箭頭，並從下拉式功能表選取 [自範本新增 DLP 原則]，也可選取此動作。</td>
    </tr>
    </tbody>
    </table>


2.  在 \[自範本建立新的 DLP 原則\] 頁面完成下列欄位：
    
    1.  \[名稱\] 新增可區分此原則與其他原則的名稱。
    
    2.  **描述**   新增摘要此原則的選擇性描述。
    
    3.  \[選取範本\]  選取適當範本以開始建立新原則。
    
    4.  \[更多選項\]選擇模式或狀態。新原則在您指定啟用前將不會完全啟用。原則的預設模式為不發出通知的測試。
    
    5.  按一下 \[儲存\] 以完成建立原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>除了特定範本內的規則，組織可能有其他套用至郵件環境中法規資料的期望或公司原則。Exchange 2013 讓您可輕鬆變更基本範本新增動作，這樣 Exchange 郵件環境即能符合您自己的要求。</td>
</tr>
</tbody>
</table>


一旦原則已儲存在您的 Exchange 2013 環境中，即可在其中編輯規則修改原則。範例規則變更可能包含將特定人員排除在原則或傳送通知之外，以及若發現郵件具有敏感內容則會封鎖郵件。如需訊息編輯原則與規則的相關資訊，請參閱[管理 DLP 原則](manage-dlp-policies-exchange-2013-help.md)。

您必須瀏覽至設定於 **\[編輯 DLP 原則\]** 頁面的特定原則規則，且使用該頁面可用的工具來變更在 Exchange 2013中建立的 DLP 原則。

部分原則允許叫用郵件的其他 RMS 規則。新增動作以使用這些類型的規則前，必須將 RMS 設定於 Exchange 伺服器上。

針對任一 DLP 原則，您可變更規則、動作、期望、強制時間或是否強制原則內的其他規則，且可個別新增自訂條件。

## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[DLP 原則範本](dlp-policy-templates-exchange-2013-help.md)


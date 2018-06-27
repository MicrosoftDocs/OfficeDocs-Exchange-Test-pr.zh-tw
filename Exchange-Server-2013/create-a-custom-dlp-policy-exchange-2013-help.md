---
title: '建立自訂的 DLP 原則: Exchange Online Help'
TOCTitle: 建立自訂的 DLP 原則
ms:assetid: b3299a39-9663-41e4-b76e-9d2f7879d486
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150550(v=EXCHG.150)
ms:contentKeyID: 50472408
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立自訂的 DLP 原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-03-18_

自訂資料外洩防護 (DLP) 原則可讓您建立條件、 規則及動作，有助於符合貴組織的特定需求及其中可能未涵蓋的其中一個現有的 DLP 範本。

您可以在單一原則中使用的規則條件包括除了[在 Exchange 中的敏感資訊類型外觀](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)所述的敏感資訊類型的所有傳統傳輸規則。如需傳輸規則的詳細資訊，請參閱[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) 或[Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\)) (Exchange Online)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您應該啟用 DLP 原則以測試模式執行它們在實際執行環境之前。期間這類測試，建議您設定範例使用者信箱並傳送測試郵件之測試原則以確認結果。如需測試的詳細資訊，請參閱<a href="test-a-mail-flow-rule-exchange-2013-help.md">測試郵件流程規則</a>。</td>
</tr>
</tbody>
</table>


建立自訂的 DLP 原則相關的其他管理工作，請參閱[DLP 程序](dlp-procedures-exchange-2013-help.md)(Exchange 2013) 或[\[Exchange Online\] 的 DLP 程序](https://technet.microsoft.com/zh-tw/library/jj938003\(v=exchg.150\)) (Exchange Online)。

## 開始之前有哪些須知？

  - 預估完成時間：60 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「資料外洩防護 (DLP) 」項目。

  - 若要建立新的自訂 DLP 原則，您必須遵循Exchange 2013的安裝指示。如需部署的詳細資訊，請參閱[規劃及部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由於客戶環境中的差異，Microsoft 客戶支援服務 (CSS) 無法參與開發或測試的自訂規則運算式指令碼 （&quot;RegEx 指令碼&quot;）。RegEX 自訂指令碼開發、 測試及偵錯時，Office 365 客戶必須依賴內部 IT 資源。或者，Office 365 客戶可以選擇使用外部諮詢資源如 Microsoft 諮詢服務 (ATL-MCS-001)。不論指令碼開發資源 CSS EXO 與 EOP 支援工程師不可用來協助客戶指令碼查詢的自訂 RegEx 相關。</td>
</tr>
</tbody>
</table>


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


## 使用 EAC 來建立不含任何現有規則的自訂 DLP 原則

1.  在 EAC 中，瀏覽至 \[**相符性管理**\>**資料遺失保護**。您已設定的任何現有原則清單中顯示。

2.  按一下 \[會出現在 \[**新增**\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")圖示旁邊的箭號並選取**新的自訂原則**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您按一下 [<strong>新增</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="加入圖示" alt="加入圖示" />圖示，而不是箭號，您會建立以範本為基礎的新原則。如需使用範本的詳細資訊，請參閱<a href="how-to-new-dlp-data-loss-prevention-policy-template.md">從範本建立 DLP 原則</a>。</td>
    </tr>
    </tbody>
    </table>


3.  在 \[**新的自訂原則**\] 頁面上完成下列欄位：
    
    1.  **\[名稱\]** 新增可區分此原則與其他原則的名稱。
    
    2.  **描述**   新增摘要此原則的選擇性描述。
    
    3.  **選擇狀態**  選取模式或此原則的狀態。新的原則未完全啟用直到您指定它應該。原則的預設模式是不通知的測試。

4.  按一下 \[**儲存**\] 以完成建立新的原則參考資訊。原則會新增至您已設定，但沒有的所有原則尚未任何規則或這個新的自訂原則相關聯的動作清單。

5.  按兩下您剛才建立的原則或加以選取，並按一下 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

6.  在 \[編輯 DLP 原則\] 頁面按一下 \[規則\]。
    
    按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")新增新的空白規則。您可以建立使用除了敏感資訊類型的所有傳統傳輸規則的條件。
    
    若要避免混淆，提供每個組件的原則或規則的唯一名稱時您必須提供您自己的字元字串\] 選項。有數個選項的其他選項您可以使用：
    
    1.  按一下 \[已新增有關寄件者通知或允許覆寫規則**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")圖示旁的箭號。
    
    2.  若要移除規則，請將該規則反白後再按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。
    
    3.  按一下 \[**更多選項**![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示")新增其他條件和動作包括此原則強制執行或對其他規則的時間繫結限制此規則。

7.  按一下 \[儲存\] 以完成這項政策的修改並儲存變更。

DLP 原則範本是一種功能可協助您的 Microsoft Exchange 設計並套用您的郵件環境的完善原則及符合性系統。如需符合性功能的詳細資訊，請參閱[郵件原則及符合性](messaging-policy-and-compliance-exchange-2013-help.md) (Exchange 2013) 或[安全性及規範的 Exchange Online](https://technet.microsoft.com/zh-tw/library/jj200706\(v=exchg.150\))。

## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange 2013

[Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\)) Exchange Online

[與傳輸規則整合敏感資訊規則](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)


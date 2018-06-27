---
title: '建立傳輸保護規則: Exchange 2013 Help'
TOCTitle: 建立傳輸保護規則
ms:assetid: 3a857185-ee16-4ee7-9e57-8be95f7e753a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd302432(v=EXCHG.150)
ms:contentKeyID: 50472989
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立傳輸保護規則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

您可以使用傳輸保護規則，根據內容 (例如寄件者、收件者、郵件主旨及內容) 將持續的權限保護套用至郵件。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在建立傳輸規則在生產環境之前，我們建議在測試環境中建立及徹底測試這些。本主題中所建立的傳輸規則是範例。您可以使用適當的 transport rule predicates 與您的需求所依據的值來建立傳輸規則。</td>
</tr>
</tbody>
</table>


如需與資訊版權管理 (IRM) 相關的其他管理工作，請參閱[資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 2-5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「傳輸規則」項目。

  - 執行[Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx)的伺服器必須可以在組織中使用且包含現有的 RMS 範本。

  - 如果您設定傳輸保護規則來保護郵件使用 IRM，而且您也可以使用日誌記錄，請考慮啟用來允許儲存加密的郵件複製的日誌報告的日誌代理程式的日誌報告解密。深入了解，請參閱 ＜ [日誌報告解密](journal-report-decryption-exchange-2013-help.md)。

  - 如果規則不能套用至郵件因為 AD RMS 伺服器無法使用建立傳輸保護規則之後，郵件將佇列由 Mailbox server 上的傳輸服務。根據這些訊息的數量、 的額外硬碟空間可能會耗用 Mailbox server 上。Exchange會嘗試將 IRM 保護之郵件三倍。之後這些嘗試，如果 AD RMS 伺服器無法連線或郵件無法為 IRM 保護的未傳遞回報 (NDR) 傳送給寄件者。

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


## 您要執行的工作

## 使用 EAC 建立傳輸規則

1.  瀏覽至 \[郵件流程\]\>\[規則\]。

2.  在清單檢視中，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 \[新增規則\] 中，首先按一下 \[其它選項\]，接著完成下列欄位：
    
      - **名稱**   輸入傳輸規則名稱。
    
      - **如果，套用此規則**  選取條件和條件輸入任何必要的值。若要新增多個條件、 按一下 \[**新增條件**\]。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果您沒有選取任何條件建立傳輸保護規則時，Exchange 2013 伺服器與您組織中的傳輸服務所處理的所有訊息都是受 IRM 保護。IRM-保護所有郵件都需要更多資源。因此，我們建議您在規劃您的 Mailbox server 和 AD RMS 部署據此。</td>
        </tr>
        </tbody>
        </table>
    
      - \[執行下列動作\]   選擇 \[套用權限保護到具有下列條件的郵件\] 然後使用 \[選擇 RMS 範本\] 對話方塊來選擇範本。
    
      - \[除非\]   (選擇性) 按一下 \[新增例外狀況\] 來指定規則的例外。

4.  按一下 \[儲存\] 以建立傳輸規則。

## 使用命令介面建立傳輸保護規則

  - 若要建立傳輸保護規則，您必須具有現有的 RMS 範本 AD RMS 部署中。此範例會從 AD RMS 叢集擷取可用的範本。
    
        Get-RMSTemplate | format-list
    
    如需詳細的語法及參數資訊，請參閱 [Get-RMSTemplate](https://technet.microsoft.com/zh-tw/library/dd297960\(v=exchg.150\))。

  - 此範例會建立傳輸保護規則 Protect BusinessCriticalProject。規則會 IRM 保護郵件包含詞語 「 Business Critical"中**不要轉寄**範本 \[主旨\] 欄位。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此範例由<code>SubjectContainsWords</code>述詞。您可以使用傳輸規則述詞的任意組合表單條件和例外狀況規則。如需可用述詞的資訊，請參閱 ＜ <a href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">傳輸規則條件 （述詞）</a>。</td>
    </tr>
    </tbody>
    </table>
    
        New-TransportRule -Name "Protect-BusinessCriticalProject" -SubjectContainsWords "Business Critical" -ApplyRightsProtectionTemplate "Do Not Forward"
    
    如需詳細的語法及參數資訊，請參閱 [New-TransportRule](https://technet.microsoft.com/zh-tw/library/bb125138\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證是否成功建立傳輸保護規則，請執行以下其中一個操作：

  - 使用 EAC 來驗證規則已建立，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示") 來檢視規則屬性。

  - 使用[Get-TransportRule](https://technet.microsoft.com/zh-tw/library/aa998585\(v=exchg.150\))指令程式來擷取此規則。如需如何擷取規則，請參閱[範例](https://technet.microsoft.com/zh-tw/aa998585\(exchg.150\)#examples)**Get-TransportRule**中的範例。

  - 使用 Outlook, Outlook Web App或者行動裝置來傳送符合規則條件的測試郵件，並確認收件者收到的郵件受 IRM 保護。


---
title: '停用網際網路行事曆發佈: Exchange 2013 Help'
TOCTitle: 停用網際網路行事曆發佈
ms:assetid: f26dbf04-9dae-460f-a987-2ad3dfbc7b7e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ853047(v=EXCHG.150)
ms:contentKeyID: 50554107
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 停用網際網路行事曆發佈

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-02-15_

停用網際網路行事曆發佈的方法取決於您如何啟用它。如果您建立了網際網路行事曆發佈專用的共用原則，您可以停用該原則或將它一併刪除。如果您將網際網路行事曆發佈設定作為預設共用原則的共用規則，則只要從 \[匿名\] 網域中移除該共用規則即可。

如果您停用網際網路行事曆發佈，佈建為使用該共用原則的使用者將無法與原則中指定的 \[匿名\] 網際網路網域共用行事曆資訊。但是，在佈建為使用共用原則的使用者將其信箱的原則設定移除之前，您無法刪除或停用該共用原則。如需與變更使用者之共用原則設定相關的詳細資訊，請參閱[管理使用者信箱](manage-user-mailboxes-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您停用或刪除共用原則時，佈建為使用該原則的使用者將可繼續共用資訊，直到執行共用原則助理員為止。若要指定共用原則助理執行的頻率，請使用 <a href="https://technet.microsoft.com/zh-tw/library/aa998651(v=exchg.150)">Set-MailboxServer</a> 指令程式搭配 <em>SharingPolicySchedule</em> 參數。</td>
</tr>
</tbody>
</table>


若要完全停用網際網路行事曆發佈，您還應停用用於行事曆發佈的 Outlook Web App 虛擬目錄。執行此作業將禁止存取 Exchange 組織使用者和外部網際網路使用者先前共用的已發佈行事曆連結。本主題稍後會詳述此步驟。

若要深入瞭解網際網路行事曆發佈和共用原則，請參閱[共用](sharing-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：15 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「行事曆與共用權限」項目。

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


## 該怎麼做？

## 步驟 1：使用 EMC 或命令介面來停用網際網路行事曆發佈的共用原則

## 使用 EAC

1.  瀏覽至 \[組織\] \> \[共享\]。

2.  在清單檢視的 \[個人共用\] 下，執行下列其中一個步驟：
    
      - 如果您建立了專用於網際網路行事曆發佈的共用原則，請選取該原則，然後清除 \[開啟\] 欄位中的核取方塊來停用共用原則，或按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示") 來刪除之。
    
      - 如果您將網際網路行事曆發佈設定作為預設共用原則的共用規則，請執行下列步驟：
        
        1.  選取預設共用原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。
        
        2.  在 \[共用原則\] 中，選取 \[匿名\] 共用規則，然後按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示") 來移除共用規則。
        
        3.  按一下 \[儲存\]。

## 使用命令介面

此範例會停用名稱為 **Internet** 的專用網際網路行事曆發佈共用原則。

    Set-SharingPolicy -Identity "Internet" -Enabled $false

此範例會刪除名稱為 **Internet** 的專用網際網路行事曆發佈共用原則。

    Remove-SharingPolicy -Identity "Internet"

如需詳細的語法及參數資訊，請參閱 [Set-SharingPolicy](https://technet.microsoft.com/zh-tw/library/dd297931\(v=exchg.150\))。

## 如何才能了解此步驟是否正常運作？

若要驗證您是否已成功移除或更新共用原則，請執行下列命令介面命令並確認共用原則資訊。

    Get-SharingPolicy <policy name> | format-list

如果您移除了專用的網際網路行事曆發佈共用原則，便不會在 Cmdlet 結果中看到該原則。

如果您更新了預設共用原則，請確認 `Anonymous` 網域已從 *Domains* 參數中移除。

如需詳細的語法及參數資訊，請參閱 [Get-SharingPolicy](https://technet.microsoft.com/zh-tw/library/dd335081\(v=exchg.150\))。

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


## 步驟 2：使用命令介面停用 Outlook Web App 虛擬目錄匿名功能

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 來停用 Outlook Web App 虛擬目錄的「匿名」功能。</td>
</tr>
</tbody>
</table>


此範例會停用用戶端存取伺服器 CAS01 上 Outlook Web App 虛擬目錄的匿名功能。

    Set-OwaVirtualDirectory -Identity "CAS01" - AnonymousFeaturesEnabled -$false

如需詳細的語法及參數資訊，請參閱 [Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-tw/library/bb123515\(v=exchg.150\))。

## 如何才能了解此步驟是否正常運作？

若要驗證您是否已成功停用用戶端伺服器上 Outlook Web App 虛擬目錄的匿名功能，請執行下列命令介面命令，並確認 *AnonymousFeaturesEnabled* 參數為 `$false`。

    Get-OwaVirtualDirectory | format-list

如需詳細的語法及參數資訊，請參閱 [Get-OwaVirtualDirectory](https://technet.microsoft.com/zh-tw/library/aa998588\(v=exchg.150\))。

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


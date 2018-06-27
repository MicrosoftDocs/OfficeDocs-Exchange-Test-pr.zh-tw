---
title: '設定 目錄和重新顯示目錄: Exchange 2013 Help'
TOCTitle: 設定 目錄和重新顯示目錄
ms:assetid: c9ca7358-9a08-4f57-89d0-910e4438df8a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124549(v=EXCHG.150)
ms:contentKeyID: 50474222
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 目錄和重新顯示目錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

\[收取\]目錄和 \[重新顯示\] 目錄是用於信箱伺服器和 Edge Transport Server 上的傳輸服務，以將郵件檔案直接插入傳輸管線。您複製到 \[收取\] 或 \[重新顯示\] 目錄中，格式正確的電子郵件檔案會提交以供傳遞。收取目錄是由系統管理員用來進行郵件流程測試，或是由必須建立及提交專屬郵件的應用程式所使用。\[重新顯示\] 目錄會從非 SMTP 外部閘道伺服器接收郵件，並重新提交您從 Microsoft Exchange 伺服器的佇列中匯出的郵件。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱主題中的「傳輸服務」[郵件流程權限](mail-flow-permissions-exchange-2013-help.md)項目。

  - 您只能使用命令介面來執行此程序。

  - **Set-TransportService** Cmdlet 上的 *PickupDirectoryMaxMessagesPerMinute* 值是用於 \[收取\] 目錄和 \[重新顯示\] 目錄。

  - 變更 \[收取\] 目錄或 \[重新顯示\] 目錄的位置，並不會將舊位置中的現有郵件檔案複製到新的位置上。在變更組態後，新的 \[收取\] 目錄或 \[重新顯示\] 目錄位置會立即啟用，但現有的郵件檔案仍會留在舊的位置中。

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


## 您想要做什麼？

## 使用命令介面來設定 \[收取\] 目錄

若要設定 \[收取\] 目錄，請使用下面的語法。

    Set-TransportService <ServerIdentity> -PickupDirectoryPath <LocalFilePath> -PickupDirectoryMaxHeaderSize <Size> -PickupDirectoryMaxRecipientsPerMessage <Integer> -PickupDirectoryMaxMessagesPerMinute <Integer>

此範例會針對郵件伺服器 Exchange01 上的 \[收取\] 目錄進行下列變更：

  - 將 \[收取\] 目錄的位置設為 D:\\Pickup Directory。

  - 將郵件檔案允許的郵件標頭大小上限增加為 96 KB。

  - 將郵件檔案允許的收件者數上限增加為 250 個。

  - \[收取\] 或 \[重新顯示\] 目錄的郵件最大處理速率增加至每分鐘 200 封郵件。

<!-- end list -->

    Set-TransportService Exchange01 -PickupDirectoryPath "D:\Pickup Directory" -PickupDirectoryMaxHeaderSize 96KB -PickupDirectoryMaxRecipientsPerMessage 250 -PickupDirectoryMaxMessagesPerMinute 200

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>將 <em>PickupDirectoryPath</em> 參數的值設為 <code>$null</code>，則會停用 [收取] 目錄。</p></li>
<li><p><em>PickupDirectoryPath</em> 參數和 <em>ReplayDirectoryPath</em> 參數所指定的目錄不可相同。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 使用命令介面來設定 \[重新顯示\] 目錄

若要設定 \[重新顯示\] 目錄，請使用下面的語法。

    Set-TransportService <ServerIdentity> -ReplayDirectoryPath "C:\Replay Directory" <LocalFilePath> -PickupDirectoryMaxMessagesPerMinute <Integer>

此範例會針對郵件伺服器 Exchange01 上的 \[重新顯示\] 目錄進行下列變更：

  - 將 \[重新顯示\] 目錄的位置設為 D:\\Replay Directory。

  - \[收取\] 或 \[重新顯示\] 目錄的郵件最大處理速率增加至每分鐘 200 封郵件。

<!-- end list -->

    Set-TransportService Exchange01 -ReplayDirectoryPath "D:\Replay Directory" -PickupDirectoryMaxMessagesPerMinute 200

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>將 <em>ReplayDirectoryPath</em> 參數的值設為 <code>$null</code>，會停用 [重新顯示] 目錄。</p></li>
<li><p><em>PickupDirectoryPath</em> 參數和 <em>ReplayDirectoryPath</em> 參數所指定的目錄不可相同。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 如何知道這是否正常運作？

若要驗證是否已成功設定 \[收取\] 目錄和 \[重新顯示\] 目錄，請執行下列動作：

1.  執行下列命令：
    
        Get-TransportService <ServerIdentity> | Format-List Pickup*,Replay*

2.  請確認顯示的值是您所設定的值。


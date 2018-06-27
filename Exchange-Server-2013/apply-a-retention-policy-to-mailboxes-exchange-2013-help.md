---
title: '將保留原則套用至信箱: Exchange Online Help'
TOCTitle: 將保留原則套用至信箱
ms:assetid: 6ccc80db-d201-44f7-8d4b-473a89c14b2f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298052(v=EXCHG.150)
ms:contentKeyID: 50473407
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將保留原則套用至信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-10-01_

您可以使用保留原則，將一個或多個保留標記分組，然後套用至信箱以強制執行郵件保留設定。信箱不能有一個以上的保留原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>郵件會根據連結到原則的保留標記中所定義的設定而到期。這些設定包含如移動郵件到封存或永久刪除它們等動作。在套用保留原則到一個或多個信箱之前，我們建議您先測試原則，並檢查與它關聯的每個保留標記。</td>
</tr>
</tbody>
</table>


如需與通訊記錄管理 (MRM) 相關的其他管理工作，請參閱[通訊記錄管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「套用保留原則」項目。

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

## 使用 EAC 將保留原則套用至單一信箱

1.  瀏覽至 \[收件者\] \> \[信箱\]。

2.  在清單檢視中，選取您要套用保留原則的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[使用者信箱\] 中，按一下 \[信箱功能\]。

4.  在 \[保留原則\] 清單中，選取想要套用至信箱的原則，然後按一下 \[儲存\]。

## 使用 EAC 將保留原則套用至多個信箱

1.  瀏覽至 \[收件者\] \> \[信箱\]。

2.  在清單檢視中，使用 Shift 鍵或 Ctrl 鍵來選取多個信箱。

3.  在詳細資料窗格中，按一下 \[其他選項\]。

4.  在 \[保留原則\] 下方，按一下 \[更新\]。

5.  在 \[大量指派保留原則\] 中，選取想要套用至信箱的原則，然後按一下 \[儲存\]。

## 使用命令介面將保留原則套用至單一信箱

此範例會將保留原則 Rp-finance 套用 Morris 的信箱。

    Set-Mailbox "Morris" -RetentionPolicy "RP-Finance"

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 使用命令介面將保留原則套用至多個信箱

此範例會將新的保留原則 New-Retention-Policy 套用到已採用舊原則 Old-Retention-Policy 的所有信箱。

    $OldPolicy={Get-RetentionPolicy "Old-Retention-Policy"}.distinguishedName
    Get-Mailbox -Filter {RetentionPolicy -eq $OldPolicy} -Resultsize Unlimited | Set-Mailbox -RetentionPolicy "New-Retention-Policy"

此範例會將保留原則 RetentionPolicy-Corp 套用至 Exchange 組織中所有的信箱。

    Get-Mailbox -ResultSize unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Corp"

此範例會將保留原則 RetentionPolicy-Finance 套用至 Finance 組織單位中所有的信箱。

    Get-Mailbox -OrganizationalUnit "Finance" -ResultSize Unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Finance"

如需詳細的語法及參數資訊，請參閱 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\)) 與 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要驗證是否已套用保留原則，請執行 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\)) 指令程式以擷取該信箱或該組信箱的保留原則。

此範例會擷取 Morris 之信箱的保留原則。

    Get-Mailbox Morris | Select RetentionPolicy

此命令會擷取已套用 RP-Finance 保留原則的所有信箱。

    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionPolicy -eq "RP-Finance"} | Format-Table Name,RetentionPolicy -Auto


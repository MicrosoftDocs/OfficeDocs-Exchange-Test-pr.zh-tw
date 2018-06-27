---
title: '執行非擁有者信箱存取報告: Exchange Online Help'
TOCTitle: 執行非擁有者信箱存取報告
ms:assetid: dbbef170-e726-4735-abf1-2857db9bb52d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150575(v=EXCHG.150)
ms:contentKeyID: 50472396
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 執行非擁有者信箱存取報告

 

_**適用版本：**Exchange Online_

_**上次修改主題的時間：**2016-12-09_

非擁有者信箱存取 Exchange 系統管理中心 (EAC) 中報告列出已經由信箱擁有者以外的某人來存取信箱。非擁有者存取信箱時 Microsoft Exchange 記錄會儲存為隱藏資料夾要稽核的信箱的電子郵件信箱稽核記錄檔此動作的相關資訊。此記錄檔中的項目顯示為搜尋結果並包括非擁有者、 誰存取信箱及動作時，執行非擁有者，來存取信箱的清單和動作是否執行成功。根據預設，在信箱稽核記錄中的項目會保留期為 90 天。

當您啟用信箱稽核記錄信箱、 Microsoft Exchange 記錄特定動作的非擁有者，包括系統管理員和使用者呼叫*委派的使用者*，且已指派權限給信箱。您也可以將縮小使用者位於組織內外的搜尋。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「信箱稽核記錄」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 啟用信箱稽核記錄

您必須針對每一個您想要執行非擁有者信箱存取報告的信箱啟用信箱稽核記錄。如果信箱稽核記錄未啟用，您將不會在執行報表時收到任何結果。

若要啟用信箱稽核記錄針對單一信箱，請執行下列命令介面。

    Set-Mailbox <Identity> -AuditEnabled $true

例如，若要啟用信箱稽核名為 Florence Flipo 的使用者，請執行下列命令。

    Set-Mailbox "Florence Flipo" -AuditEnabled $true

若要針對組織內的所有使用者信箱啟用信箱稽核，請執行下列命令。

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}

    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

## 如何知道這是否正常運作？

執行下列命令來驗證您是否已成功設定信箱稽核記錄。

    Get-Mailbox | FL Name,AuditEnabled

已啟用提供驗證 *AuditEnabled* 屬性信箱稽核記錄的 `True` 值。

返回頁首

## 執行非擁有者信箱存取報告

1.  在 EAC 中，瀏覽至 \[規範管理\] \> \[稽核\]。

2.  按一下 \[**執行非擁有者信箱存取報告**。
    
    根據預設，Microsoft Exchange 會執行非擁有者存取的報告至兩個星期透過組織中所有信箱。在搜尋結果中所列的信箱已啟用信箱稽核記錄。

3.  若要檢視特定信箱的非擁有者存取，請從信箱清單中選取的信箱。在詳細資料窗格中檢視搜尋結果。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>要縮小搜尋結果吗？選取的開始日期、 結束日期] 或兩者，然後選取特定信箱搜尋。按一下 [<strong>搜尋</strong>] 重新執行 [報表]。</td>
</tr>
</tbody>
</table>


## 非擁有者存取的特定類型的搜尋

您也可以指定非擁有者存取\]，也稱為要搜尋的登入類型的類型。以下是您的選項：

  - **所有的非擁有者**  搜尋的系統管理員和委派的使用者組織內的存取。也包含存取您的組織外部的使用者。

  - **外部使用者**  搜尋貴組織的外部使用者存取。

  - **系統管理員和委派的使用者**：搜尋組織內的系統管理員和委派的使用者的存取。

  - **系統管理員**：搜尋組織內系統管理員的存取。

返回頁首

## 如何知道這是否正常運作？

若要確認您是否已成功執行非擁有者信箱存取報告，請檢查 \[搜尋結果\] 窗格。在此窗格中顯示您執行的報告的信箱。如果不有任何特定信箱的結果，很可能尚未被非擁有者存取\] 或 \[非擁有者存取尚未採取指定的日期範圍內的位置。如前所述，請先確認的稽核記錄已啟用存取您要搜尋之信箱的非擁有者。

返回頁首

## 項目會取得身分登入信箱稽核記錄？

當您執行非擁有者信箱存取報告時，從信箱稽核記錄項目會顯示在 EAC 中的搜尋結果中。每個報告項目會包含這項資訊：

  - 誰存取信箱及何時

  - 非擁有者所執行的動作

  - 受影響的郵件，並將其資料夾位置

  - 動作是否執行成功

下表列出所執行的動作非擁有者可以登入信箱的稽核記錄。在表格中，**是**表示以登入類型，可記錄動作並**無**指出無法記錄的動作。星號 （**\***） 會指出動作會記錄的信箱啟用信箱稽核記錄時的預設值。如果您想要追蹤預設未記錄的動作，您必須使用 PowerShell 來啟用這些動作的記錄。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>已指派完整存取權給使用者的信箱的系統管理員會被視為委派的使用者。</td>
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
<th>動作</th>
<th>描述</th>
<th>系統管理員</th>
<th>委派的使用者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Copy</strong></p></td>
<td><p>郵件已複製到另一個資料夾。</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><strong>Create</strong></p></td>
<td><p>在信箱的 [行事曆]、[連絡人]、[記事] 或 [工作] 資料夾中建立了項目，例如，建立了新的會議邀請。請注意，郵件或資料夾建立將不予稽核。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderBind</strong></p></td>
<td><p>存取信箱資料夾。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>實刪除</strong></p></td>
<td><p>郵件已經從 [可復原的項目] 資料夾清除。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
</tr>
<tr class="odd">
<td><p><strong>MessageBind</strong></p></td>
<td><p>在預覽窗格中檢視郵件或將它開啟。</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><strong>Move</strong></p></td>
<td><p>郵件已移到另一個資料夾。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><strong>移至刪除的項目</strong></p></td>
<td><p>郵件已經移至 [刪除的郵件] 資料夾。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>傳送為</strong></p></td>
<td><p>已使用 SendAs 權限傳送郵件。這表示，另一個使用者已傳送郵件，就像此郵件是來自信箱擁有者一樣。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
</tr>
<tr class="odd">
<td><p><strong>傳送代理者</strong></p></td>
<td><p>已使用 SendOnBehalf 權限傳送郵件。這表示，另一個使用者已代表信箱擁有者傳送郵件。此郵件會向收件者指示，此郵件是代表誰傳送，以及實際傳送郵件的人是誰。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>虛刪除</strong></p></td>
<td><p>郵件已經從 [刪除的郵件] 資料夾刪除。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
</tr>
<tr class="odd">
<td><p><strong>Update</strong></p></td>
<td><p>郵件已變更。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
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
<td>*  在啟用信箱的稽核時依預設稽核。</td>
</tr>
</tbody>
</table>


返回頁首


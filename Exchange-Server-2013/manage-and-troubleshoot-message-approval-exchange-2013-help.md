---
title: '管理及疑難排解郵件核准: Exchange Online Help'
TOCTitle: 管理及疑難排解郵件核准
ms:assetid: 860df43f-a05b-4da3-83f1-68d3123a923d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298110(v=EXCHG.150)
ms:contentKeyID: 52062566
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理及疑難排解郵件核准

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

當您嘗試移除的仲裁信箱，可能會收到下列錯誤：


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>因為使用核准工作流程為其成員資格限制或啟用的仲裁的現有收件者無法移除仲裁信箱 &lt;<em>mailbox</em>&gt;。您應停用在這些收件者的核准功能或這些收件者的指定不同的仲裁信箱，才能移除此仲裁信箱。</p></td>
</tr>
</tbody>
</table>


仲裁信箱可用來處理核准工作流程的仲裁收件者及通訊群組成員資格核准。 您可以使用 PowerShell 來尋找所有收件者所使用的仲裁信箱設定。找出收件者之後，您可設定它們使用不同的仲裁信箱，則您可以停用它們仲裁。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的 「 Aribtration 」 項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 步驟 1： 使用命令介面來尋找所有收件者使用您嘗試要刪除的仲裁信箱

執行下列命令：

    $AM = Get-Mailbox "<arbitration mailbox>" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}

例如，若要找出所有收件者使用 mailbox01 仲裁的仲裁信箱，請執行下列命令：

    $AM = Get-Mailbox "Arbitration Mailbox01" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>仲裁信箱會指定使用辨別的名稱 (DN)。如果您知道仲裁信箱的 DN，您可以執行單一命令 ︰ <code>Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq &lt;DN&gt;}</code>。</td>
</tr>
</tbody>
</table>


## 步驟 2： 使用命令介面來指定不同的仲裁信箱或停用收件者的仲裁

若要停止使用您嘗試要刪除的仲裁信箱仲裁收件者，您也可以指定不同的仲裁信箱，或您可以停用收件者的仲裁。

如果您選擇指定不同的仲裁信箱的收件者，請執行下列命令：

    Set-<RecipientType> <Identity> -ArbitrationMailbox <different arbitration mailbox>

例如，若要重新設定名為要使用的成員資格核准名為仲裁 Mailbox02 的仲裁信箱的所有員工的通訊群組，執行下列命令：

    Set-DistributionGroup "All Employees" -ArbitrationMailbox "Arbitration Mailbox02"

如果您選擇停用收件者的仲裁，執行下列命令：

    Set-<RecipientType> <Identity> -ModerationEanbled $false

例如，若要停用名為人力資源信箱仲裁，請執行下列命令：

    Set-Mailbox "Human Resources" -ModerationEanbled $false

## 如何知道這是否正常運作？

此程序成功如果您可以刪除的仲裁信箱而不會收到正在使用的錯誤。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。


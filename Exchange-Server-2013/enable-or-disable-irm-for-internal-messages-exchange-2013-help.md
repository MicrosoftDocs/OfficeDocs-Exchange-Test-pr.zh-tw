---
title: '啟用或停用內部郵件的 IRM: Exchange 2013 Help'
TOCTitle: 啟用或停用內部郵件的 IRM
ms:assetid: a6a17f57-5304-41f1-954d-7301857d54a1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124077(v=EXCHG.150)
ms:contentKeyID: 50473882
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用內部郵件的 IRM

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-12_

在 Microsoft Exchange Server 2013、 內部郵件的預設會啟用資訊版權管理 (IRM)。這可讓您建立傳輸保護規則和 Microsoft Outlook保護規則 IRM 保護的郵件傳輸規則中與 Microsoft Outlook 2010及更新版本的用戶端上。啟用內部郵件的 IRM 是針對其他所有Exchange Server 2013，例如停用傳輸解密、 日誌規則解密、 IRM in Microsoft OfficeOutlook Web App，以及 Microsoft Exchange ActiveSync中的 IRM 的 IRM 功能的必要條件。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>停用 IRM 的內部郵件會停用Exchange組織中所有的 IRM 功能。不受影響Outlook （例如，能夠讀取、 回覆、 轉寄，並建立受 IRM 保護的郵件使用Active Directory Rights Management Services (AD RMS) 伺服器） 的用戶端的 IRM 功能。</td>
</tr>
</tbody>
</table>


若欲瞭解更多與 IRM 相關的管理工作，請參閱 [資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「版權保護」項目。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來啟用或停用 IRM 的內部郵件。您必須使用命令介面。

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


## 使用命令介面對內部訊息啟用 IRM

本範例在 Exchange 組織中對內部訊息啟用 IRM。

    Set-IRMConfiguration -InternalLicensingEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))。

## 使用命令介面對內部訊息停用 IRM

本範例在 Exchange 組織中對內部訊息停用 IRM。

    Set-IRMConfiguration -InternalLicensingEnabled $false

如需詳細的語法及參數資訊，請參閱 [Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否已啟用或停用內部郵件的 IRM，請使用 [Get-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd776120\(v=exchg.150\)) Cmdlet 來檢查組態。


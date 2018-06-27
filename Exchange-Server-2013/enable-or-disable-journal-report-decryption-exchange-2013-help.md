---
title: '啟用或停用日誌報告解密: Exchange 2013 Help'
TOCTitle: 啟用或停用日誌報告解密
ms:assetid: 1dedbe73-2c1a-4b14-8799-5091aaec7965
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638092(v=EXCHG.150)
ms:contentKeyID: 50472777
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用日誌報告解密

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

啟用日誌報告解密允許要解密的權限保護之訊息的複本附加至日誌報告的日誌代理程式。啟用日誌報告解密之前，您必須在您的[Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx)伺服器上設定超級使用者群組新增同盟傳遞信箱。

如需與資訊版權管理 (IRM) 相關的其他管理工作，請參閱[資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：1 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「版權保護」項目。

  - 超級使用者授與擁有者群組的成員可以使用授權時所要求的授權從 AD RMS 叢集。這可讓其解密建立該 AD RMS 叢集的所有與 RMS 受保護的內容。

  - AD RMS 叢集必須安裝在 Active Directory 樹系中。

  - 同盟傳遞信箱已新增到 AD RMS 超級使用者群組。如需詳細資訊，請參閱[至 AD RMS 超級使用者群組新增同盟信箱](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

  - 您無法使用 Exchange 系統管理中心 (EAC) 若要啟用日誌報告解密。您必須使用命令介面。

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

## 使用命令介面來啟用日誌報告解密

此範例會啟用 Exchange 組織的日誌報告解密。

    Set-IRMConfiguration -JournalReportDecryptionEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))。

## 使用命令介面來停用日誌報告解密

此範例會停用 Exchange 組織的日誌報告解密。

    Set-IRMConfiguration -JournalReportDecryptionEnabled $false

如需詳細的語法及參數資訊，請參閱 [Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要檢查您已啟用或停用日誌報告解密，請執行 **Get-IRMConfiguration** 指令程式並檢查 *JournalDecryptionEnabled* 屬性的值。

如需如何檢查 IRM 組態的範例，請參閱 **Get-IRMConfiguration** 中的[Examples](https://technet.microsoft.com/zh-tw/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples)。


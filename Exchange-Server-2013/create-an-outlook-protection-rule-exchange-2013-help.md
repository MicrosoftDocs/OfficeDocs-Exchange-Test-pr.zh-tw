---
title: '建立 Outlook 保護規則: Exchange 2013 Help'
TOCTitle: 建立 Outlook 保護規則
ms:assetid: da64750d-faaf-44de-ad8c-888eba7fbdbf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638196(v=EXCHG.150)
ms:contentKeyID: 50474369
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立 Outlook 保護規則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

使用 Microsoft Outlook保護規則，您可以藉由套用在Outlook 2010Active Directory Rights Management Services (AD RMS) 範本之前傳送的郵件保護使用資訊版權管理 (IRM) 的郵件。

若欲瞭解更多與 IRM 相關的管理工作，請參閱 [資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「版權保護」項目。

  - 您必須在您執行 Microsoft Exchange Server 2013的伺服器相同的Active Directory樹系中部署[AD RMS](https://technet.microsoft.com/en-us/library/hh831364.aspx)伺服器。

  - 如果您設定Outlook保護規則 IRM 保護的郵件，請考慮啟用停用傳輸解密允許傳輸代理程式，包括要解密並存取郵件的傳輸規則代理程式。如果您使用日誌記錄，您也應該考量啟用日誌報告解密來允許儲存加密的郵件複製的日誌報告的日誌代理程式。如需詳細資訊，請參閱[日誌報告解密](journal-report-decryption-exchange-2013-help.md)。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來建立Outlook保護規則。您必須使用命令介面。

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


## 使用命令介面來建立 Outlook 保護規則

此範例會建立Outlook保護規則 Project Contoso。此規則會保護與 AD RMS 範本 Business Critical ContosoPMs 通訊群組傳送的郵件。

    New-OutlookProtectionRule -Name "Project Contoso" -SentTo "DL-ContosoPMs@contoso.com" -ApplyRightsProtectionTemplate "Business Critical"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您使用Outlook保護規則<code>SentTo</code>述詞與指定通訊群組、 僅限的郵件寄至通訊群組中 [收件者]、 [副本] 或 [密件副本] 欄位會受 IRM 保護。預設傳送給通訊群組的個別成員的郵件無法套用 IRM 保護。</td>
</tr>
</tbody>
</table>


您也可以使用`FromDepartment`和`SentToScope`述詞將 IRM 保護套用至指定的部門或傳送至指定的範圍 （內部郵件的`InOrganization` 、 `All`所有收件者） 的訊息中的使用者傳送的郵件。

如需詳細的語法及參數資訊，請參閱[New-OutlookProtectionRule](https://technet.microsoft.com/zh-tw/library/dd298182\(v=exchg.150\))。

## 如何知道這是否正常運作？

確認您成功建立 Outlook 保護規則，請執行下列動作：

  - 執行[Get-OutlookProtectionRule](https://technet.microsoft.com/zh-tw/library/dd298004\(v=exchg.150\)) cmdlet 以確保已建立規則並檢視規則的屬性。如需以擷取 Outlook 保護規則的範例，請參閱在**Get-OutlookProtectionRule**的[範例](https://technet.microsoft.com/zh-tw/dd298004\(exchg.150\)#examples)。

  - 使用Outlook 2010建立測試郵件符合的規則條件，並且確定用戶端上觸發規則。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>可能需要一些時間讓可供在 Outlook 中使用 Outlook 保護規則。</td>
    </tr>
    </tbody>
    </table>


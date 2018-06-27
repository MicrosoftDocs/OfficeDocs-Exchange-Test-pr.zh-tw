---
title: '建立共用的信箱: Exchange Online Help'
TOCTitle: 建立共用的信箱
ms:assetid: d34bc827-1e83-4a7f-a219-8ba9c19fe24b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150570(v=EXCHG.150)
ms:contentKeyID: 50474278
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立共用的信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013, Office 365 Enterprise_

_**上次修改主題的時間：**2016-12-09_

**預估完成時間：5 分鐘**

共用的信箱方便來監視及傳送電子郵件的常見的帳戶，例如 info@contoso.com 或 support@contoso.com 公司群組。當群組中的人員回覆郵件傳送至共用信箱時、 電子郵件看起來所共用信箱傳送不是從個別使用者。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用 Office 365 企業版，您應該在 Office 365 系統管理中心建立共用的信箱。
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=834766">建立 Office 365 中的共用的信箱</a></p></li>
</ul></td>
</tr>
</tbody>
</table>


如果貴組織使用 Exchange 混合式環境，您應該使用內部部署 Exchange 系統管理中心 (EAC) 來建立及管理共用的信箱。若要深入了解共用信箱，請參閱[共用信箱](shared-mailboxes-exchange-2013-help.md)。

## 使用 EAC 建立共用信箱

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「使用者信箱」項目。

1.  移至 \[收件者\] \> \[共用\] \> \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  填入必要欄位：
    
      - **顯示名稱**
    
      - **電子郵件地址**

3.  若要授與 \[完整存取\] 或 \[以下列傳送\] 權限，請按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，然後選取要對其授與權限的使用者。您可以使用 **CTRL** 鍵選取多位使用者。搞不清楚要使用何種權限嗎？請參閱本主題稍後的Which permission should you use?。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>[完整存取] 權限可讓使用者開啟信箱，以及在信箱中建立與修改項目。[以下列傳送 ] 權限可讓任何人 (信箱擁有者除外) 從該共用信箱傳送電子郵件。這兩者是成功共用信箱作業的必要權限。</td>
    </tr>
    </tbody>
    </table>


4.  按一下 \[儲存\] 儲存您的變更，並建立共用信箱。

## 使用 EAC 來編輯共用信箱委派

1.  移至 \[收件者\] \> \[共用\] \> \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  按一下 \[信箱委派\]

3.  若要授與或移除 \[完整存取\] 或 \[以下列傳送\] 權限，請按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 或 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")，然後選取要對其授與權限的使用者。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>[完整存取] 權限可讓使用者開啟信箱，以及在信箱中建立與修改項目。[以下列傳送 ] 權限可讓任何人 (信箱擁有者除外) 從該共用信箱傳送電子郵件。這兩者是成功共用信箱作業的必要權限。</td>
    </tr>
    </tbody>
    </table>


4.  按一下 **\[儲存\]** 以儲存變更。

## 使用共用的信箱

若要了解使用者可存取和使用共用的信箱的方式，請參閱下列：

  - [開啟與使用 Outlook 2016 和 Outlook 2013 中的共用信箱](https://go.microsoft.com/fwlink/p/?linkid=834764)

  - [開啟與使用企業網路上的 Outlook 中的共用信箱](https://go.microsoft.com/fwlink/p/?linkid=834766)

## 使用命令介面建立共用信箱

這個範例會建立共用信箱「銷售部門」，並對於安全性群組 MarketingSG 授與「完整存取」和「代理傳送者」權限。屬於安全性群組成員的使用者被授與信箱的權限。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此範例假設您已建立安全性群組 MarketingSG，且該安全性群組擁有郵件功能。請參閱<a href="manage-mail-enabled-security-groups-exchange-2013-help.md">管理擁有郵件功能的安全性群組</a>。</td>
</tr>
</tbody>
</table>


    New-Mailbox -Shared -Name "Sales Department" -DisplayName "Sales Department" -Alias Sales | Set-Mailbox -GrantSendOnBehalfTo MarketingSG | Add-MailboxPermission -User MarketingSG -AccessRights FullAccess -InheritanceType All

如需詳細的語法及參數資訊，請參閱 [New-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997663\(v=exchg.150\))。

## 應該使用哪些權限？

以下是可與共用信箱搭配使用的權限。

  - **完整存取權**   「完整存取權」權限可讓使用者開啟共用信箱，做為該信箱的擁有者。在存取登入共用信箱後，使用者可以建立行事曆項目；讀取、檢視、刪除和變更電子郵件；建立工作和行事曆連絡人。不過，除非具有「完整存取權」權限的使用者也有「傳送為」或「代理傳送者」權限，否則無法從共用信箱傳送電子郵件。

  - **傳送為**   「傳送為」權限可讓使用者在傳送郵件時模擬共用信箱。例如，如果 Kweku 登入共用信箱 Marketing Department 並傳送一封電子郵件，看起來就像是 Marketing Department 傳送該電子郵件。

  - **代理傳送者**   「代理傳送者」權限可讓使用者代表共用信箱傳送電子郵件。例如，如果 John 登入共用信箱 Reception Building 32 並傳送一封電子郵件，看起來該電子郵件就像由「John 代表 Reception Building 32」傳送。您無法使用 EAC 授與「代理傳送者」權限，您必須使用 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\)) Cmdlet 搭配 *GrantSendonBehalf* 參數。

## 其他資訊

如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

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


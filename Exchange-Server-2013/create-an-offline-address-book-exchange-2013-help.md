---
title: '建立離線通訊錄: Exchange Online Help'
TOCTitle: 建立離線通訊錄
ms:assetid: b57bb4ce-5b6e-4702-a2f8-04bf3898a861
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124339(v=EXCHG.150)
ms:contentKeyID: 50474060
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewOabWizardForm.OabIntroductionWizardPage
ms.translationtype: MT
---

# 建立離線通訊錄

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-04-24_

離線通訊錄 (OAB) 的Exchange Server 2013是允許存取資訊時從伺服器中斷連線的 Outlook 使用者通訊錄下載的複本。Exchange 系統管理員可以決定叢書離線、 工作及他們也可以設定的通訊錄所依據的方法的使用者可提供使用的地址分散式 （web 式發佈或公用資料夾通訊群組）。

如需與 OAB 相關的其他管理工作，請參閱[離線通訊錄程序](offline-address-book-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md)主題中的「離線通訊錄」項目。

  - 根據 Exchange Online 的預設，「通訊清單」角色並未指派給任何角色群組。若要使用任何需要「通訊清單」角色的指令程式，您需將此角色新增至角色群組。如需詳細資訊，請參閱＜[管理角色群組](manage-role-groups-exchange-2013-help.md)＞主題的＜將角色新增至角色群組＞一節。

  - 您無法使用 Exchange 系統管理中心 (EAC) 執行此程序。您必須使用命令介面。

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


## 使用命令介面建立以 Web 式發佈的 OAB

此範例會使用預設虛擬目錄，針對 Outlook 2007 或更新版本用戶端建立使用 Web 式發佈且名為 OAB\_Contoso 的 OAB。

    New-OfflineAddressBook -Name "OAB_Contoso" -AddressLists "\Default Global Address List" -VirtualDirectories $Null -GlobalWebDistributionEnabled $True

如需詳細的語法及參數資訊，請參閱 [New-OfflineAddressBook](https://technet.microsoft.com/zh-tw/library/bb123692\(v=exchg.150\))。


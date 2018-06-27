---
title: '適用於 Outlook 的應用程式: Exchange Online Help'
TOCTitle: 適用於 Outlook 的應用程式
ms:assetid: 28b6f2a1-a235-4023-b561-6fd304962775
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ943753(v=EXCHG.150)
ms:contentKeyID: 52062528
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 適用於 Outlook 的應用程式

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2017-03-13_

**摘要：** 增益集的 Outlook 與 Windows 及 MacIntosh 電腦上行動裝置上及 Outlook Web App 和 Outlook web 上的 Outlook 搭配使用的概觀。

Outlook的增益集是透過新增資訊或您的使用者可以使用不必離開 Outlook 的工具來擴充 Outlook 用戶端實用性的應用程式。增益集由協力廠商開發人員建置及可安裝檔案或 URL 或來自 Office 市集。根據預設，所有的使用者可以安裝新增寫 Exchange 系統管理員可以使用角色來控制使用者能夠安裝的增益集。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需增益集的 Outlook 使用者觀點，查看在 Office.com [說明] 主題<a href="https://go.microsoft.com/fwlink/p/?linkid=282387">已安裝的增益集</a> 。該主題提供之增益集的概觀及也會顯示您的增益集部分可能依預設安裝的 outlook。</td>
</tr>
</tbody>
</table>


## Office 市集的增益集及自訂增益集

Outlook 用戶端支援增益集提供 Office 市集透過各種的不同。Outlook 也支援自訂增益集，您可建立並散佈給使用者您組織中。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>到 Office 市集的存取不支援的信箱或組織中特定區域 （英文）。如果您未看見<strong>來自 Office 市集新增</strong>是<strong>Exchange 系統管理中心</strong>底下<strong>組織</strong>中的選項 &gt;<strong>增益集</strong>&gt; <img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="加入圖示" alt="加入圖示" />，您可以從 URL 或檔案的位置的 outlook 安裝增益集。如需詳細資訊，請連絡您的服務提供者。</td>
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
<td>預設會安裝某些增益集的 Outlook。預設的增益集 Outlook 僅啟用版中的內容。例如，郵件內文中的德文郵寄地址不會啟用的 Bing 地圖服務增益集。</td>
</tr>
</tbody>
</table>


## 增益集存取和安裝

根據預設，所有的使用者可以安裝且移除新增寫 Exchange 系統管理員可用於管理的增益集和使用者的存取控制項數目。系統管理員可以停用使用者安裝增益集，就不會下載來自 Office 市集 （但是它們是載入的 「 端 」 從檔案或 URL）。系統管理員也可以停用使用者安裝 Office 市集增益集和從代表其他使用者安裝的增益集。它也可將使用者指派給角色，讓他們在組織中安裝增益集的組織或使用者的子集。

若要防止使用者安裝不來自 Office 市集，移除**「 我的自訂應用程式**角色它們。 若要停用使用者安裝的增益集來自 Office 市集、 移除**我市集應用程式**角色它們。如需詳細資訊，請參閱[指定系統管理員和使用者可安裝和管理適用於 Outlook 增益集](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md)。

若要在組織中安裝部分或所有使用者的增益集，請參閱[安裝或移除 Outlook for 貴組織的應用程式](install-or-remove-add-ins-for-outlook-for-your-organization-exchange-2013-help.md)。

如有需要，您可以在組織中限制特定使用者能使用增益集的可用性。如需詳細資訊，請參閱[管理 outlook 的應用程式的使用者存取](manage-user-access-to-add-ins-for-outlook-exchange-online-help.md)。

## 使用 Outlook 的增益集的一般管理工作

有幾個 Exchange 系統管理員管理組織中的常見案例。

**如果您想要讓使用者安裝的所有 Outlook 用戶端上的 Outlook 增益集進行下列變更給 Exchange 系統管理中心中的角色：**

  - 若要防止使用者安裝 Office 市集的增益集，移除**「 我的服務商場**角色它們。

  - 若要防止使用者從非 Office 市集的來源載入增益集，移除**「 我的自訂應用程式**角色它們。

  - 若要防止使用者安裝的所有增益集，移除這兩個以上的角色它們。

請參閱[指定系統管理員和使用者可安裝和管理適用於 Outlook 增益集](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md)如需詳細資訊。

**如果您的使用者是目前能夠存取增益集，您想要移除該存取使用`Get-App`指令程式來查看哪些增益集的每位使用者都已安裝。**

接下來，使用`Remove-App`指令程式來移除一或多個使用者的所有增益集。

如需詳細資訊，請參閱[Get-App](https://technet.microsoft.com/zh-tw/library/jj218673\(v=exchg.150\))和[Remove-App](https://technet.microsoft.com/zh-tw/library/jj218709\(v=exchg.150\)) for Exchange 2013。Exchange Online 或 Exchange 2016、 移[以下](https://go.microsoft.com/fwlink/p/?linkid=844721)。

## 允許系統管理員和使用者安裝的增益集

您可以指定哪些系統管理員在組織中的已安裝和管理適用於 Outlook 增益集的權限。您也可以指定您組織中的哪些使用者有權限安裝和管理自己使用的增益集。如需詳細資訊，請參閱[指定系統管理員和使用者可安裝和管理適用於 Outlook 增益集](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md)。


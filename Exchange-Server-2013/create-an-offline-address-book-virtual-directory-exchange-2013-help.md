---
title: '建立離線通訊錄虛擬目錄: Exchange Online Help'
TOCTitle: 建立離線通訊錄虛擬目錄
ms:assetid: 2c70e21f-2b12-414a-9e8c-65634a767c72
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996917(v=EXCHG.150)
ms:contentKeyID: 50472764
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立離線通訊錄虛擬目錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-16_

OAB 虛擬目錄是通訊的 oab。根據預設，在安裝 Microsoft Exchange Server 2013時新增名為 OAB 虛擬目錄建立預設內部網站在網際網路資訊服務 (IIS) 中。如果您有連線至MicrosoftOutlook從組織防火牆外的用戶端的使用者，您可以新增的外部網站。或者，當您在命令介面中執行**New-OABVirtualDirectory**指令程式，新建立虛擬目錄名稱 OAB 中的本機Exchange伺服器上的預設 IIS 網站。

建立 OAB 虛擬目錄並非一般工作。Exchange 允許將一個 OAB 虛擬目錄命名為 OAB，且您應僅可於現有 OAB 虛擬目錄出現問題且前一個 OAB 虛擬目錄遭移除時才可建立 OAB 虛擬目錄。

如需與 OAB 相關的其他管理工作，請參閱[離線通訊錄程序](offline-address-book-procedures-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在建立 OAB 虛擬目錄之前，請確定您的使用者會察覺可讓您的變更。此程序可能會中斷 OAB 下載程序的使用者。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md)主題中的「離線通訊錄」項目。

  - 本機 Exchange 伺服器需安裝用戶端存取伺服器角色。

  - 需有預設的 IIS 網站 (例如 /w3svc/1/root)。

  - 名為 OAB 的虛擬目錄不存在。

  - 雖然 Web 式發佈預設為啟用不需要進一步設定，但仍建議您為 OAB 發佈點啟用安全通訊端層 (SSL)。

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


## 使用命令介面來建立 OAB 虛擬目錄

若要使用的所有預設設定都建立 OAB 虛擬目錄，您可以執行**New-OABVirtualDirectory**指令程式不含任何參數。使用下列程序來建立自訂設定 OAB 虛擬目錄。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建立 OAB 虛擬目錄時，建議您啟用 SSL。</td>
</tr>
</tbody>
</table>


此範例會在名為 CASServer01 並已啟用 SSL 且具有外部 URL 的用戶端存取伺服器上，建立 OAB 虛擬目錄。

    New-OABVirtualDirectory -Server CASServer01 -RequireSSL $true -ExternalURL "https://www.contoso.com/OAB"

建立新的 OAB 虛擬目錄後，您必須編輯上每個使用 Web 式發佈重新連線至 OAB 虛擬目錄的 OAB 的設定。如需詳細資訊，請參閱[變更離線通訊錄產生排程](change-the-offline-address-book-generation-schedule-exchange-2013-help.md)。

如需詳細的語法及參數資訊，請參閱 [New-OabVirtualDirectory](https://technet.microsoft.com/zh-tw/library/bb123735\(v=exchg.150\))。


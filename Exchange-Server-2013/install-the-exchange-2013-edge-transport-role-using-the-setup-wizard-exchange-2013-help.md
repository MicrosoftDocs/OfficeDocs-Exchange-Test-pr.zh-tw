---
title: '使用設定精靈安裝 Exchange 2013 Edge Transport role: Exchange 2013 Help'
TOCTitle: 使用設定精靈安裝 Exchange 2013 Edge Transport role
ms:assetid: b8e51b0b-201e-4c64-92c8-3ac0db04b6e2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn635117(v=EXCHG.150)
ms:contentKeyID: 61204231
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用設定精靈安裝 Exchange 2013 Edge Transport role

 

_**適用版本：**Exchange Server, Exchange Server 2013_

_**上次修改主題的時間：**2014-06-19_

本主題說明如何使用 Microsoft Exchange Server 2013 安裝精靈將 Exchange 2013 Edge Transport server role 安裝在電腦上。Exchange 2013 Service Pack 1 (SP1) 或更新版本提供 Edge Transport role。如需規劃與部署 Exchange 2013 的相關資訊，請參閱[規劃及部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)。

建議將 Edge Transport role 安裝在組織內部 Active Directory 樹系外的周邊網路中。雖然可以將 Edge Transport server role 安裝在加入網域的電腦上，但這樣只會啟用 Windows 功能和設定的網域管理。Edge Transport role 本身不使用 Active Directory。反之，它使用 Active Directory 輕量型目錄服務 (AD LDS) Windows 功能和儲存組態和收件者資訊。如需 Edge Transport role 的詳細資訊，請參閱＜[Edge Transport Server](edge-transport-servers-exchange-2013-help.md)＞。

如果您要在電腦上安裝 Exchange 2013 Mailbox 或 Client Access role，請參閱＜[使用安裝精靈安裝 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)＞。Edge Transport role 不能與 Mailbox 或 Client Access server role 安裝在相同的電腦上。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您是否曾聽過 Exchange Server 部署助理？這是一項免費的線上工具，該工具會詢問您一些問題並特別為您建立一份自訂的部署檢查清單，以協助您在組織中快速部署 Exchange 2013。若想要深入了解，請移至 <a href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 部署助理</a>。</td>
</tr>
</tbody>
</table>


如需要在安裝後完成之工作的相關資訊，請參閱 [Exchange 2013 後續安裝工作](exchange-2013-post-installation-tasks-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：40 分鐘

  - 在安裝 Exchange 2013前，請確認已閱讀版本資訊。如需詳細資訊，請參閱＜[Exchange 2013 版本資訊](release-notes-for-exchange-2013-exchange-2013-help.md)＞。

  - 您安裝 Exchange 2013 的電腦必須有支援的作業系統 (例如 Windows Server 2008 R2 SP1、Windows Server 2012 R2 或 Windows Server 2012)、有足夠的磁碟空間，且符合其他需求。如需系統需求的相關資訊，請參閱 [Exchange 2013 系統需求](exchange-2013-system-requirements-exchange-2013-help.md)。

  - 若要執行 Exchange 2013 安裝程式，您必須安裝 Microsoft .NET Framework 4.5、Windows Management Framework 及其他必要軟體。若要了解所有伺服器角色的必要條件，請參閱 [Exchange 2013 必要條件](exchange-2013-prerequisites-exchange-2013-help.md)。

  - 您必須在電腦上設定主要 DNS 尾碼。例如，如果電腦的完整網域名稱是 edge.contoso.com，則電腦的 DNS 尾碼是 contoso.com。如需詳細資訊，請參閱＜[主要 DNS 尾碼遺漏](primary-dns-suffix-is-missing-exchange-2013-help.md)＞。

  - Exchange 2007 和 Exchange 2010 Hub Transport Server 需要更新，您才能在它們與 Exchange 2013 Edge Transport Server 之間建立 EdgeSync 訂閱。如果您未安裝此更新，EdgeSync 訂閱將無法正常運作。如需詳細資訊，請參閱＜[Exchange 2013 系統需求](exchange-2013-system-requirements-exchange-2013-help.md)＞的＜支援的共存案例＞一節。

  - 請確定您使用的帳戶是您安裝 Edge Transport role 的電腦上的本機 Administrators 群組的成員。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在伺服器上安裝 Exchange 之後，就不得變更伺服器名稱。在安裝 Exchange 伺服器角色之後，就不支援重新命名伺服器。</td>
</tr>
</tbody>
</table>


## 安裝 Exchange Server 2013

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要下載最新版本的 Exchange 2013，請參閱＜<a href="updates-for-exchange-2013-exchange-2013-help.md">更新 Exchange 2013</a>＞。</td>
</tr>
</tbody>
</table>


1.  登入要在其上安裝 Exchange 2013 的電腦。

2.  瀏覽至Exchange 2013安裝檔案的網路位置。

3.  連按兩下 `Setup.exe` 來啟動 Exchange 2013 安裝程式
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您啟用使用者存取控制 (UAC)，必須以滑鼠右鍵按一下 <code>Setup.exe</code>，並選取 [以管理員的身分執行]。</td>
    </tr>
    </tbody>
    </table>


4.  在 \[檢查更新?\] 頁面上，選擇您是否要安裝程式連線到網際網路，並下載 Exchange 2013 的產品及安全更新。如果您選取 \[連線到網際網路並檢查更新\]，安裝程式將下載並套用更新，然後才會繼續進行。若您選擇 \[現在不要檢查更新\]，可於之後手動下載並安裝更新。我們建議您下載並立即安裝更新。按 **\[下一步\]** 繼續。

5.  
    
    將 Exchange 安裝到組織的程序會從 **\[簡介\]** 頁面開始。它會引導您完成安裝。接著會列出實用部署內容的幾個連結。建議您造訪這些連結再繼續安裝。按 **\[下一步\]** 繼續。

6.  
    
    在 **\[授權合約\]** 頁面上，檢閱軟體授權條款。如果您同意條款，請選取 \[我接受授權合約中的條款\]，然後按 \[下一步\]。

7.  
    
    在 \[建議設定\] 頁面上，選取您是否要使用建議的設定。如果您選取 **\[使用建議的設定\]**，Exchange 會自動將錯誤報告及有關電腦硬體和您如何使用 Exchange 的相關資訊傳送到 Microsoft。如果您選取 \[不使用建議設定\]，這些設定將維持停用，但是您可以在安裝程式完成後隨時啟用這些設定。如需這些設定以及傳送到 Microsoft 的資訊如何加以使用的詳細資訊，請按一下 \[?\]。

8.  
    
    在 **\[伺服器角色選取\]** 頁面上，選取 **\[Edge Transport\]**。請記住，您不可以將 Mailbox 或 Client Access server role 新增至已安裝 Edge Transport role 的電腦。如果安裝任何伺服器角色，都會自動安裝管理工具。
    
    選取 **\[自動安裝 Exchange Server 安裝所需的 Windows Server 角色及功能\]** 讓安裝精靈安裝所需的 Windows 必要元件。可能需要重新開機以完成部分 Windows 功能的安裝。若您未選擇此選項，則必須手動安裝 Windows 功能。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此選項只會安裝 Exchange 需要的 Windows 功能。您必須手動安裝其他必要條件。如需詳細資訊，請參閱＜<a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 必要條件</a>＞。</td>
    </tr>
    </tbody>
    </table>
    
    按 **\[下一步\]** 繼續。

9.  在 \[安裝空間與位置\] 頁面上，接受預設安裝位置，或按一下 \[瀏覽\] 選擇新位置。確定要安裝 Exchange 的位置有足夠的磁碟空間。按 **\[下一步\]** 繼續。

10. 
    
    在 **\[整備檢查\]** 頁面上，檢視狀態以判斷組織及伺服器角色必要條件檢查是否成功完成。如果沒有順利完成，則您必須先解決所有回報的錯誤，才能安裝 Exchange 2013。解決某些必要條件錯誤時，您不需要結束安裝程式。解決回報的錯誤後，按一下 **\[返回\]**，然後按 **\[下一步\]** 再次執行必要條件檢查。請務必同時檢閱所有回報的警告。如果所有整備檢查都已順利完成，請按 **\[下一步\]** 安裝 Exchange 2013。

11. 
    
    在 **\[完成\]** 頁面上，按一下 **\[完成\]**。

12. Exchange 2013 完成後請重新啟動電腦。

13. 執行 [Exchange 2013 後續安裝工作](exchange-2013-post-installation-tasks-exchange-2013-help.md) 中提供的工作以完成部署。

## 如何才能了解這是否正常運作？

若要確認您是否已成功安裝 Exchange 2013，請參閱 [確認 Exchange 2013 安裝](verify-an-exchange-2013-installation-exchange-2013-help.md).

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。


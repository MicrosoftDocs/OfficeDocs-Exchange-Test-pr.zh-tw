---
title: '使用安裝精靈安裝 Exchange 2013: Exchange 2013 Help'
TOCTitle: 使用安裝精靈安裝 Exchange 2013
ms:assetid: da690d47-3384-4430-a69e-0cd4d3bf80a7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124778(v=EXCHG.150)
ms:contentKeyID: 50474370
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.ExSetupUI.SetupWizardForm.IntroductionPage
ms.translationtype: HT
---

# 使用安裝精靈安裝 Exchange 2013

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-06-19_

本主題說明如何使用 Microsoft Exchange Server 2013 安裝精靈將 Exchange 2013 Mailbox 和 Client Access role 安裝在電腦上。如需規劃與部署 Exchange 2013 的相關資訊，請參閱[規劃及部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)。

如果您要在電腦上安裝 Exchange 2013 Edge Transport role，請參閱＜[使用設定精靈安裝 Exchange 2013 Edge Transport role](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md)＞。Edge Transport role 不能與 Mailbox 或 Client Access server role 安裝在相同的電腦上。

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


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在執行 Exchange 2013 的電腦上安裝任何伺服器角色之後，就無法使用 Exchange 2013 安裝精靈，將任何的其他伺服器角色新增至此電腦。如果想要將多個伺服器角色新增至電腦，則必須使用 [控制台] 的 [新增或移除程式]，或從 [命令提示字元] 視窗使用 Setup.exe。</td>
</tr>
</tbody>
</table>


如需要在安裝後完成之工作的相關資訊，請參閱 [Exchange 2013 後續安裝工作](exchange-2013-post-installation-tasks-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：60 分鐘

  - 在安裝 Exchange 2013前，請確認已閱讀版本資訊。如需詳細資訊，請參閱 [Exchange 2013 版本資訊](release-notes-for-exchange-2013-exchange-2013-help.md)。

  - 每個組織的 Active Directory 樹系中至少都要有一部 Client Access Server 與一部 Mailbox Server。此外，每個含有 Mailbox Server 的 Active Directory 網站也至少要包含一部 Client Access Server。如果您要分離您的伺服器角色，建議您先安裝 Mailbox server role。

  - 您安裝 Exchange 2013 的電腦必須有支援的作業系統 (例如 Windows Server 2008 R2 Service Pack 1 (SP1) 或 Windows Server 2012)、有足夠的磁碟空間、為 Active Directory 網域的成員，且符合其他需求。如需系統需求的相關資訊，請參閱 [Exchange 2013 系統需求](exchange-2013-system-requirements-exchange-2013-help.md)。

  - 若要執行 Exchange 2013 安裝程式，您必須安裝 Microsoft .NET Framework 4.5、Windows Management Framework 3.0 及其他必要軟體。若要了解所有伺服器角色的必要條件，請參閱 [Exchange 2013 必要條件](exchange-2013-prerequisites-exchange-2013-help.md)。

  - 如果您尚未準備 Active Directory 架構，則必須確定使用的帳戶委派了 Schema Admins 群組的成員資格。如果是安裝組織中的第一部 Exchange 2013 伺服器，您使用的帳戶必須具有 Enterprise Admins 群組的成員資格。如果已準備好架構，並且不是安裝組織中的第一部 Exchange 2013 伺服器，則您使用的帳戶必須屬於 Exchange 2013 組織管理角色群組的成員。
    
    身為「委派安裝」角色群組成員的系統管理員，可部署先前已由「組織管理」管理角色群組的成員提供的 Exchange 2013 伺服器。

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

如果是安裝組織中的第一部 Exchange 2013 伺服器，而且尚未執行 Active Directory 準備步驟，您必須使用具有 Enterprise Administrators 群組成員資格的帳戶。若您先前尚未備妥 Active Directory 架構，則帳戶也必須是 Schema Admins 群組的成員。如需如何準備 Active Directory 的 Exchange 2013，請參閱[準備 Active Directory 及網域](prepare-active-directory-and-domains-exchange-2013-help.md)。如果您已經執行架構和 Active Directory 準備步驟，您使用的帳戶必須是 Delegated Setup 管理角色群組或 Organization Management 角色群組的成員。

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

3.  通過連按兩下 `Setup.exe`，啟動Exchange 2013
    
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


4.  在 \[檢查更新?\] 頁面上，選擇您是否要安裝程式連線到網際網路，並下載 Exchange 2013 的產品及安全更新。如果您選取 \[連線到網際網路並檢查更新\]，安裝程式將下載並套用更新，然後才會繼續進行。若您選擇 \[現在不要檢查更新\]，可於之後手動下載並安裝更新。我們建議您下載並立即安裝更新。按 \[下一步\] 繼續。

5.  
    
    將 Exchange 安裝到組織的程序會從 \[簡介\] 頁面開始。它會引導您完成安裝。接著會列出實用部署內容的幾個連結。建議您造訪這些連結再繼續安裝。按 \[下一步\] 繼續。

6.  
    
    在 \[授權合約\] 頁面上，檢閱軟體授權條款。如果您同意條款，請選取 \[我接受授權合約中的條款\]，然後按 \[下一步\]。

7.  
    
    在 \[建議設定\] 頁面上，選取您是否要使用建議的設定。如果您選取 **\[使用建議的設定\]**，Exchange 會自動將錯誤報告及有關電腦硬體和您如何使用 Exchange 的相關資訊傳送到 Microsoft。如果您選取 \[不使用建議設定\]，這些設定將維持停用，但是您可以在安裝程式完成後隨時啟用這些設定。如需這些設定以及傳送到 Microsoft 的資訊如何加以使用的詳細資訊，請按一下 \[?\]。

8.  
    
    在 \[伺服器角色選取\] 頁面上，選擇是否要在此電腦上安裝 \[信箱角色\]、\[用戶端存取角色\] 或兩個角色，或是否只要在此電腦上安裝 \[管理工具\]。如果選擇不在此安裝期間安裝其他伺服器角色，可以稍後再安裝。組織必須安裝至少一個信箱角色和至少一個用戶端存取伺服器角色。這些可以安裝在同一部電腦上或不同電腦上。如果安裝任何伺服器角色，都會自動安裝管理工具。
    
    選取 **\[自動安裝 Exchange Server 安裝所需的 Windows Server 角色及功能\]** 讓安裝精靈安裝所需的 Windows 必要元件。可能需要重新開機以完成部分 Windows 功能的安裝。若您未選擇此選項，則必須手動安裝 Windows 功能。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此選項只會安裝 Exchange 需要的 Windows 功能。您必須手動安裝其他必要條件。如需詳細資訊，請參閱 <a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 必要條件</a>。</td>
    </tr>
    </tbody>
    </table>
    
    按 **\[下一步\]** 繼續。

9.  在 \[安裝空間與位置\] 頁面上，接受預設安裝位置，或按一下 \[瀏覽\] 選擇新位置。確定要安裝 Exchange 的位置有足夠的磁碟空間。按 \[下一步\] 繼續。

10. 
    
    如果這是組織中的第一部 Exchange 伺服器，請在 \[Exchange 組織\] 頁面上輸入 Exchange 組織的名稱。Exchange 組織名稱只能包含下列字元：
    
      - A 到 Z
    
      - a 到 z
    
      - 0 到 9
    
      - 空格 (非前導或尾隨)
    
      - 連字號或橫線
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>組織名稱不能包含 64 個以上的字元。組織名稱不能是空白。</td>
        </tr>
        </tbody>
        </table>
    
    如果要使用 Active Directory 分割權限模式，請選取 **\[將 Active Directory 分割權限資訊安全模型套用至 Exchange 組織\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>大部分組織不需要套用 Active Directory 分割權限模式。如果您需要分別管理 Active Directory 安全性主體和 Exchange 組態，角色型存取控制 (RBAC) 分割權限可能適用於您。如需詳細資訊，請按一下[?]。</td>
    </tr>
    </tbody>
    </table>
    
    按 \[下一步\] 繼續。

11. 如果您要安裝信箱角色，請在 \[惡意程式碼防護設定\] 頁面上，選擇是否要啟用或停用惡意程式碼掃描。如果您停用惡意程式碼掃描，未來仍可加以啟用。按 \[下一步\] 繼續。

12. 
    
    在 \[整備檢查\] 頁面上，檢視狀態以判斷組織及伺服器角色必要條件檢查是否成功完成。如果沒有順利完成，則您必須先解決所有回報的錯誤，才能安裝 Exchange 2013。解決某些必要條件錯誤時，您不需要結束安裝程式。解決回報的錯誤後，按一下 **\[返回\]**，然後按 **\[下一步\]** 再次執行必要條件檢查。請務必同時檢閱所有回報的警告。如果所有整備檢查都已順利完成，請按 \[下一步\] 安裝 Exchange 2013。

13. 
    
    在 \[完成\] 頁面上，按一下 \[完成\]。

14. Exchange 2013 完成後請重新啟動電腦。

15. 執行 [Exchange 2013 後續安裝工作](exchange-2013-post-installation-tasks-exchange-2013-help.md) 中提供的工作以完成部署。

## 如何知道這是否正常運作？

若要驗證是否已成功安裝 Exchange 2013，請參閱 [確認 Exchange 2013 安裝](verify-an-exchange-2013-installation-exchange-2013-help.md).

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。


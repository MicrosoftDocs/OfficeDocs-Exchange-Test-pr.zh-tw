---
title: '安裝 Exchange 2013 管理工具: Exchange 2013 Help'
TOCTitle: 安裝 Exchange 2013 管理工具
ms:assetid: 71fcbe4c-783b-4f77-aabb-a21aa7a4ef23
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232090(v=EXCHG.150)
ms:contentKeyID: 50554010
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 安裝 Exchange 2013 管理工具

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-01-28_

使用 Microsoft Exchange Server 2013 管理工具，您可以遠端配置並管理您的 Exchange 組織。Exchange 2013 管理工具包括 Exchange 管理命令介面與 Exchange 工具箱。本主題將說明如何使用 Setup.exe 或自動安裝模式來安裝 Exchange 2013 管理工具。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您不需要執行此程序以遠端使用 Exchange 管理中心 (EAC)。EAC 為網路主控台，主機位於執行 Exchange 2013 Client Access 伺服器角色的電腦上。如需有關遠端存取 EAC 的詳細資訊，請參閱 <a href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的 Exchange 系統管理中心</a>。</td>
</tr>
</tbody>
</table>


如需管理 Exchange 2013 的詳細資訊，請參閱 [Exchange 2013 中的 Exchange 系統管理中心](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)和 [使用 PowerShell 與 Exchange 2013 (Exchange 管理命令介面)](https://technet.microsoft.com/zh-tw/library/bb123778\(v=exchg.150\))。

## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘

  - 在安裝 Exchange 2013前，請確認已閱讀版本資訊。如需詳細資訊，請參閱 [Exchange 2013 版本資訊](release-notes-for-exchange-2013-exchange-2013-help.md)。

  - 您安裝管理工具的電腦必須有支援的作業系統 (例如 Windows Server 2012 或 Windows 8)、足夠的磁碟空間、是 Active Directory 網域的成員，並且滿足其他需求。如需系統需求的相關資訊，請參閱 [Exchange 2013 系統需求](exchange-2013-system-requirements-exchange-2013-help.md)。

  - 若要執行 Exchange 2013 安裝程式，您必須安裝 Microsoft .NET Framework 4.5、Windows Management Framework 3.0 以及其他必要軟體。若要了解所有伺服器角色的必要條件，請參閱 [Exchange 2013 必要條件](exchange-2013-prerequisites-exchange-2013-help.md)。

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


## 使用安裝程式來安裝 Exchange 2013 管理工具

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


4.  在 **\[檢查更新\]** 頁面上，選擇您是否想要安裝程式連接至網際網路，並且下載 Exchange 2013 的產品與安全更新。如果您選取 \[連線到網際網路並檢查更新\]，安裝程式將下載並套用更新，然後才會繼續進行。若您選擇 \[現在不要檢查更新\]，可於之後手動下載並安裝更新。我們建議您下載並立即安裝更新。按 **\[下一步\]** 繼續。

5.  
    
    將 Exchange 安裝到組織的程序會從 \[簡介\] 頁面開始。它會引導您完成安裝。接著會列出實用部署內容的幾個連結。建議您造訪這些連結再繼續安裝。按 \[下一步\] 繼續。

6.  
    
    在 **\[授權合約\]** 頁面上，檢閱軟體授權條款。如果您同意條款，請選取 **\[我接受授權合約中的條款\]**，然後按 **\[下一步\]**。

7.  
    
    在 \[建議設定\] 頁面上，選取您是否要使用建議的設定。如果您選取 \[使用建議設定\]，Exchange 會自動將錯誤報告以及您的電腦硬體和您使用 Exchange 的方式相關的資訊傳送到 Microsoft。如果您選取 \[不使用建議設定\]，這些設定將維持停用，但是您可以在安裝程式完成後隨時啟用這些設定。如需這些設定以及傳送到 Microsoft 的資訊如何加以使用的詳細資訊，請按一下 \[?\]。

8.  
    
    在 \[伺服器角色選取\] 頁面上，驗證選取了 \[管理工具\]。
    
    選取 \[自動安裝 Exchange Server 安裝所需的 Windows Server 角色及功能\] 讓安裝程式精靈安裝所需的 Windows 必要條件。可能需要重新開機以完成部分 Windows 功能的安裝。若您未選擇此選項，則必須手動安裝 Windows 功能。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此選項指會安裝 Exchange 需要的 Windows 功能。您必須手動安裝其他必要條件。如需詳細資訊，請參閱 <a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 必要條件</a>。</td>
    </tr>
    </tbody>
    </table>
    
    按 **\[下一步\]** 繼續。

9.  在 \[安裝空間與位置\] 頁面上，接受預設安裝位置，或按一下 \[瀏覽\] 選擇新位置。確定要安裝 Exchange 的位置有足夠的磁碟空間。按 **\[下一步\]** 繼續。

10. 
    
    如果這是您首次在組織內執行 Exchange 2013 安裝程式，在 **\[Exchange 組織\]** 頁面上，輸入您 Exchange 組織的名稱。Exchange 組織名稱只能包含下列字元：
    
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
    
    如果要使用 Active Directory 分割權限模式，請選取 \[將 Active Directory 分割權限安全性模型套用至 Exchange 組織\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>大部份組織不需要套用 Active Directory 分割權限模式。如果您需要分別管理 Active Directory 安全性主體和 Exchange 組態，角色型存取控制 (RBAC) 分割權限可能對您適用。如需詳細資訊，請按一下[?]。</td>
    </tr>
    </tbody>
    </table>
    
    按 \[下一步\] 繼續。

11. 
    
    在 **\[整備檢查\]** 頁面上，檢視狀態以判斷組織及伺服器角色必要條件檢查是否成功完成。如果沒有順利完成，則您必須先解決所有回報的錯誤，才能安裝 Exchange 2013。解決某些必要條件錯誤時，您不需要結束安裝程式。解決回報的錯誤後，按一下 **\[返回\]**，然後按 **\[下一步\]** 再次執行必要條件檢查。請務必同時檢閱所有回報的警告。如果所有整備檢查都已順利完成，請按 **\[下一步\]** 安裝 Exchange 2013。

12. 
    
    在 \[完成\] 頁面上，按一下 \[完成\]。

13. Exchange 2013 完成後請重新啟動電腦。

## 使用自動安裝模式安裝 Exchange 2013 管理工具

1.  登入您想要安裝 Exchange 2013 管理工具的電腦。

2.  瀏覽至Exchange 2013安裝檔案的網路位置。

3.  在命令提示字元中，執行下列命令。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若您已啟用使用者存取控制 (UAC)，必須從更高的命令提示字元安裝 <code>Setup.exe</code>。</td>
    </tr>
    </tbody>
    </table>
    
        Setup.exe /Role:ManagementTools /IAcceptExchangeServerLicenseTerms

如需詳細資訊，請參閱[使用自動模式安裝 Exchange 2013](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)。


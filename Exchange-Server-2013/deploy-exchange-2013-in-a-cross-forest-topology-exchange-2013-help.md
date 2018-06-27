---
title: '部署跨樹系拓撲中的 Exchange 2013: Exchange 2013 Help'
TOCTitle: 部署跨樹系拓撲中的 Exchange 2013
ms:assetid: 65be650f-d435-4f60-9ff0-5cb88a726abb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998597(v=EXCHG.150)
ms:contentKeyID: 51409188
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 部署跨樹系拓撲中的 Exchange 2013

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

本主題說明如何部署Exchange 2013在跨樹系拓撲中使用 Microsoft Forefront Identity Manager 2010 R2 SP1。若要部署Exchange 2013跨樹系拓撲中，必須先安裝Exchange 2013每個樹系中，並再連線樹系\]，讓使用者可以看見跨樹系的地址及可用性的資料。

下圖說明兩個 Exchange 2013 樹系之間的使用者同步處理。

**Exchange 2013 跨樹系同步處理的範例**

![Exchange 2010 多重樹系範例](images/Aa998597.df0ba5dd-cb96-4542-98bd-2a425defe317(EXCHG.150).gif "Exchange 2010 多重樹系範例")

本主題沒有*未*說明如何部署Exchange 2013專用的Exchange樹系 （或資源樹系） 中的拓撲。如需如何部署Exchange 2013資源樹系拓撲中的詳細資訊，請參閱 ＜ [部署 Exchange 資源樹系拓撲中的 Exchange 2013](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md)。

## 開始之前有哪些須知？

若要在 Exchange 2013 中執行下列程序，請確認下列內容：

  - 您已正確設定網域名稱系統 (DNS) 名稱解析為跨樹系組織中。若要確認已正確設定 DNS，請使用 Ping 工具來測試連線至每個樹系從您的組織中的其他樹系以及您要執行之 GALSync 代理程式的伺服器。

  - 使用 PowerShell 2.0 版 RTM WindowsExchange 2013樹系與通訊 GALSync 管理代理程式 (MA)。請務必Windows PowerShell v1.0 未安裝在這部電腦上依要控制台中，然後按一下 \[程式和功能。

  - 請確保 Windows Update 並未安裝 Windows 遠端管理。

  - 安裝Windows PowerShell 和Windows遠端管理。如需詳細資訊，請參閱 Microsoft 知識庫文章 968930、 [Windows 管理架構核心套件 （Windows PowerShell 2.0 和 WinRM 2.0）](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)。

  - 下載 Forefront Identity Manager 2010 R2 SP1。請參閱[Microsoft Forefront Identity Manager 2010 R2 SP1 的下載](https://go.microsoft.com/fwlink/p/?linkid=279868)。

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


## 在跨樹系拓撲中使用 Forefront Identity Manager 2010 R2 SP1 來部署 Exchange 2013

1.  每個樹系中，分別安裝Exchange 2013 。若要安裝Exchange 2013、 執行一般如果您已安裝Exchange 2013單一樹系拓撲中的相同步驟。如需詳細步驟，請參閱下列主題：
    
      - [部署 Exchange 2013 的新安裝](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [使用安裝精靈安裝 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>本主題假設您不需要現有Exchange 2007或Exchange 2010拓撲。如果您需要現有Exchange拓撲且想要升級，請參閱<a href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">從 Exchange 2010 升級至 Exchange 2013</a>或<a href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">從 Exchange 2007 升級至 Exchange 2013</a>。</td>
        </tr>
        </tbody>
        </table>


2.  每個樹系中，使用Active Directory使用者及電腦建立其中 FIM 2010 R2 SP1 會建立每個信箱的連絡人來自其他樹系的容器。我們建議您命名為此容器**FromFIM**。若要建立容器，選取您要建立容器、 網域上按一下滑鼠右鍵、 選取 \[**新增**的網域 \>**組織單位**。**新物件-的組織單位**中輸入**FromFIM**，，然後按一下 \[**確定\]**。

3.  使用 Forefront 識別管理員建立每個樹系 GALSync 管理代理程式。這可讓同步中每個樹系的使用者，建立一般 GAL。如需詳細步驟，請參閱下列資源：
    
      - [設定全域通訊清單 (GAL) 同步化與 Forefront Identity Manager (FIM) 2010](https://go.microsoft.com/fwlink/p/?linkid=279869)
    
      - [使用管理代理程式](https://go.microsoft.com/fwlink/p/?linkid=279870)
    
      - [Forefront Identity Manager 2010 R2 說明文件導讀](https://go.microsoft.com/fwlink/p/?linkid=279871)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>雖然資源討論Exchange 2010、 Exchange 2013支援 FIM 2010 R2 SP1。請確定您設定<strong>延伸模組</strong>FIM 2010 R2 SP1 中的Exchange 2013。</td>
    </tr>
    </tbody>
    </table>
    
    1.  在 \[**設定延伸模組**\] 頁面上的 \[**設定分割區的顯示名稱**、 旁邊**的佈建**、 選取**Exchange 2013**。您會看到 \[ **Exchange 2013 RPS URI** \] 欄位。輸入Exchange 2013用戶端存取伺服器的 URI 以確定可運作的遠端 PowerShell 連線。**Exchange 2013 RPS URI**應該是下列格式： http://CAS\_Server\_FQDN/Powershell。按一下 \[**確定\]**。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>請確保用於連線至 Exchange 2013 樹系的系統管理員認證也可以建立至該樹系的遠端 PowerShell 連線。<br />
        下圖顯示了如何為 Exchange 2013 選取提供。</td>
        </tr>
        </tbody>
        </table>
        
        **為 Exchange 2013 提供 GalSync 管理代理程式**
        
        ![管理代理程式 Exchange 2010 佈建](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "管理代理程式 Exchange 2010 佈建")  

4.  在每個樹系中建立 SMTP 傳送連接器。如需詳細步驟，請參閱[設定跨樹系傳送連接器](configure-a-cross-forest-send-connector-exchange-2013-help.md)。

5.  每個樹系中，啟用可用性服務，讓每個樹系中的使用者可以檢視有關使用者的空閒/忙碌資料其他樹系中。如需詳細資訊，請參閱[Exchange 2013 中的可用性服務](availability-service-in-exchange-2013-exchange-2013-help.md)。

6.  如果您希望在郵件轉送到您組織中任何樹系，您必須設定該樹系中的網域為授權網域。如需詳細步驟，請參閱[將 Exchange 設定為接受多個授權網域的郵件](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md)。


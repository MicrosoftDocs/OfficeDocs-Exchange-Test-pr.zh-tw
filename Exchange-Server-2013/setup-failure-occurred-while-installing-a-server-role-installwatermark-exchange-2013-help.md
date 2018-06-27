---
title: '安裝伺服器 role_InstallWatermark 時所發生的安裝程式失敗: Exchange 2013 Help'
TOCTitle: 安裝伺服器 role_InstallWatermark 時所發生的安裝程式失敗
ms:assetid: ad89ebd5-f9bb-40c1-8811-09b145c2b341
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.installwatermark(v=EXCHG.150)
ms:contentKeyID: 50473961
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安裝伺服器 role\_InstallWatermark 時所發生的安裝程式失敗

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安裝程式無法繼續因為先前的安裝程式失敗時發生安裝的伺服器角色。

Exchange 2007 的安裝程式要求失敗的伺服器角色安裝都必須有成功重新安裝或移除安裝程序，才可以繼續任何其他設定工作。

若要解決此問題，只是失敗的伺服器角色、 重新安裝或移除伺服器角色。

若要重新安裝從命令列的失敗的伺服器角色

1.  開啟命令提示字元視窗，然後瀏覽至安裝檔案。

2.  執行下列命令：
    
        Setup /roles:<Failed Server Role>
    
    選取一或多個以逗號分隔的清單中的下列角色：
    
    ClientAccess （或 CA 或 C）
    
    EdgeTransport （或 ET 或 E）
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Edge Transport server role 不能共存與任何其他伺服器角色相同的電腦上。</td>
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
    <td>您必須部署在周邊網路及外部Active Directory樹系的邊際傳輸伺服器角色。</td>
    </tr>
    </tbody>
    </table>
    
    HubTransport （HT 或 H）
    
    信箱 （或 MB 或 M）
    
    UnifiedMessaging （或 UM 或 U）
    
    ManagementTools （細明體或 T）
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您指定 ManagementTools，您將會安裝Exchange管理主控台、 Exchange管理命令介面、 Exchange說明檔、 Exchange Best Practices Analyzer 工具、 Exchange cmdlet 和Exchange疑難排解助理員。如果您在安裝任何其他伺服器角色、 將會自動安裝管理工具。</td>
    </tr>
    </tbody>
    </table>
    
    例如，若要將 Hub Transport server role 新增至現有的信箱伺服器，輸入下列︰ **%LocalExchangeInstallationDir%\\bin\\Setup.com /role:HubTransport /Mode:Install**

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果任何 Exchange Server 2007 伺服器角色先前安裝成功，精靈會維護模式中執行安裝程式。如果先前已成功不安裝任何 Exchange 2007 伺服器角色，將從停止其中啟動 [安裝精靈]。</td>
</tr>
</tbody>
</table>


在維護模式中使用 \[Exchange Server 2007 安裝精靈\] 以重新安裝失敗的伺服器角色

1.  登入您要重新安裝伺服器角色的伺服器。

2.  開啟 \[控制台\]，然後按兩下 \[**新增或移除程式\]**。

3.  在 \[**變更或移除程式**\] 頁面上選取 \[ **Microsoft Exchange Server**，並再按一下 \[**變更**。

4.  中Exchange Server 2007安裝精靈\] 中 \[ **Exchange 維護模式**\] 頁面上按一下 \[**下一步**\]。

5.  在 \[**伺服器角色選取**\] 頁面上選取您想要安裝的伺服器角色的核取方塊\] 和 \[**下一步**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Edge Transport server role 不能共存與任何其他伺服器角色相同的電腦上。</td>
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
    <td>您必須部署在周邊網路及外部Active Directory樹系的邊際傳輸伺服器角色。</td>
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
    <td>如果您選取 [管理工具]，您將會安裝Exchange管理主控台、 Exchange管理命令介面Exchange cmdlet 和Exchange說明檔。如果您在安裝任何其他伺服器角色的管理工具將會自動安裝。</td>
    </tr>
    </tbody>
    </table>


6.  若您選取 \[**集線傳輸角色**，且如果您要安裝Exchange 2007樹系中的現有Exchange Server 2003或Exchange 2000 Server組織**郵件流程設定**\] 頁面上選取 bridgehead 伺服器Exchange 2003成員的現有組織或您要建立路由群組連接器的Exchange 2000路由群組中。

7.  **整備檢查**\] 索引標籤上檢視的狀態來決定是否組織和伺服器角色必要條件檢查順利完成。他們已順利完成時，按一下 \[安裝Exchange 2007\[**安裝**\]。

8.  在 \[**完成**\] 頁面上，按一下 \[**完成**\]。

若要使用 Exchange Server 2007 安裝精靈來重新安裝失敗的伺服器角色時沒有其他伺服器角色是先前成功安裝

1.  請遵循"方式來執行自訂安裝使用 Exchange Server 2007 安裝"([https://go.microsoft.com/fwlink/?LinkId=86648](https://go.microsoft.com/fwlink/?linkid=86648)) 中的 Exchange Server 2007 產品文件中的指引。

若要移除的失敗的伺服器角色

1.  請依照下列 Exchange Server 2007 產品文件 」 如何至移除 Exchange 2007 伺服器角色"([https://go.microsoft.com/fwlink/?LinkId=86649](https://go.microsoft.com/fwlink/?linkid=86649)) 中的指示。

## 相關資訊

如需如何以自動模式安裝 Exchange 2007 的詳細資訊，請參閱 「 方式來安裝 Exchange 2007 在自動模式 」 ([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476))。


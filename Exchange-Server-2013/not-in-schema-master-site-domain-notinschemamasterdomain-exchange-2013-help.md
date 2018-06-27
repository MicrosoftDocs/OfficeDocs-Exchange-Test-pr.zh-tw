---
title: '結構描述中未 master site/domain_NotInSchemaMasterDomain: Exchange 2013 Help'
TOCTitle: 結構描述中未 master site/domain_NotInSchemaMasterDomain
ms:assetid: 5e44eb33-4c30-4c3d-ba68-5c30bef1731f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.notinschemamasterdomain(v=EXCHG.150)
ms:contentKeyID: 50473283
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 結構描述中未 master site/domain\_NotInSchemaMasterDomain

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式無法繼續因為執行安裝程式的電腦不是在同一個 Active Directory® directory service 站台或網域中指派網域架構主機角色，也稱為彈性單一主機操作或 FSMO 的伺服器。

Exchange 2007 的安裝程式需要做為網域架構主機位於相同的網站和網域正在執行 Exchange 安裝程式的本機電腦之網域控制站。

網域架構主機控制所有更新及修改 Active Directory 架構。

若要解決此問題，請執行 Exchange Server 2007 安裝程式使用從相同的網站和網域的**/prepareschema**和**/prepareAD**參數網域架構主機。

如需**/prepareschema**和**/prepareAD**安裝參數的詳細資訊，請參閱 Exchange 2007 產品文件主題"如何以準備 Active Directory 及網域 」 (<https://go.microsoft.com/fwlink/?linkid=78453>)

您可以使用架構主機工具來識別角色。不過，Schmmgmt.dll DLL 必須註冊才能進行結構描述工具可作為 MMC 嵌入式管理單元。

檢視目前的架構主機

1.  在命令提示字元處輸入**regsvr32 schmmgmt.dll**
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>下列對話方塊顯示時<strong>RegSvr32</strong>具有已成功登錄：<br />
    在 schmmgmt.dll DllRegisterServer 成功。</td>
    </tr>
    </tbody>
    </table>


2.  若要開啟新的管理主控台，按一下 \[**開始\]**、 按一下 \[**執行**\]，然後輸入**mmc**。

3.  在 \[主控台\] 功能表上按一下 \[**新增/移除嵌入式管理單元**\]。

4.  按一下 \[**新增**\] 以開啟 \[**新增獨立嵌入式管理單元**\] 對話方塊。

5.  選取**Active Directory 架構**\]，然後再按一下 \[**新增**\]。

6.  「 Active Directory 架構 」 會顯示在 \[新增/移除嵌入式管理單元中按一下 \[**關閉**\] 和 \[返回主控台的**\[確定\]** 。

7.  選取**Active Directory 架構**以便在右側顯示的**類別**和**屬性**的區段。

8.  以滑鼠右鍵按一下 \[ **Active Directory 架構**，然後按一下 \[**作業主圖形**。

9.  顯示目前的架構主機

找出目前的架構主機之後，請決定架構主機位於哪一個子網路。然後，使用下列方法之一來安裝 Exchange：

  - 修改 Exchange 伺服器，將它移到架構主機所在的網站上的子網路。然後安裝 Exchange。

  - 暫時的 Exchange 伺服器上，強制將網站成員資格變更，並安裝 Exchange。Exchange 安裝之後，回到其原始網站的 Exchange 伺服器。

若要強制網站成員資格

1.  在您要安裝 Exchange 伺服器上，啟動 \[登錄編輯程式。若要這樣做，按一下 \[**開始\]**、 按一下 \[**執行**\]、 輸入**regedit**，然後按一下 \[**確定\]**。

2.  尋找下列登錄子機碼：
    
    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\Netlogon\\Parameters**

3.  建立下列的新**字串**值：
    
    數值名稱： **SiteName**
    
    值類型： **REG\_SZ**
    
    數值資料： **\< site\_that\_contains\_the\_schema\_master \>**

4.  結束登錄編輯程式，並再重新啟動 Netlogon 服務。此動作會強制參與您所指定的網站中的 Exchange 伺服器。

5.  安裝 Exchange。

6.  移除您在步驟 3 中新增登錄項目。

7.  重新啟動 Netlogon 服務。此巨集指令會將 Exchange 返回原始網站。


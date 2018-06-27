---
title: 'IIS 7 元件不 installed_LonghornIIS7HttpCompressionStaticNotInstalled: Exchange 2013 Help'
TOCTitle: IIS 7 元件不 installed_LonghornIIS7HttpCompressionStaticNotInstalled
ms:assetid: 87fb8068-8c11-45cd-b18c-7d4ba97dedda
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.longhorniis7httpcompressionstaticnotinstalled(v=EXCHG.150)
ms:contentKeyID: 50473633
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS 7 元件不 installed\_LonghornIIS7HttpCompressionStaticNotInstalled

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2015-03-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2010 安裝程式或 Microsoft Exchange Server 2007 安裝程式無法安裝 Client Access Server (CAS) 角色或 Mailbox server role 在 Microsoft Windows Server 2008 電腦上或在 Windows Server 2008 R2 電腦上因為未安裝所需的 Internet Information Server (IIS) 7 元件。

Exchange 2010 安裝程式與 Exchange 2007 安裝需要執行 Windows Server 2008 電腦或在其您在已安裝的 CAS 角色的 Windows Server 2008 R2 電腦已安裝下列 IIS 7 元件。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>CAS 伺服器角色所需的 IIS 7 元件</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>動態內容壓縮</p></td>
</tr>
<tr class="even">
<td><p>靜態內容壓縮</p></td>
</tr>
<tr class="odd">
<td><p>基本驗證</p></td>
</tr>
<tr class="even">
<td><p>Windows 驗證</p></td>
</tr>
<tr class="odd">
<td><p>IIS 7 摘要式驗證</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET</p></td>
</tr>
<tr class="odd">
<td><p>用戶端憑證對應</p></td>
</tr>
<tr class="even">
<td><p>瀏覽目錄</p></td>
</tr>
<tr class="odd">
<td><p>HTTP 錯誤</p></td>
</tr>
<tr class="even">
<td><p>HTTP 記錄</p></td>
</tr>
<tr class="odd">
<td><p>HTTP 重新導向</p></td>
</tr>
<tr class="even">
<td><p>追蹤</p></td>
</tr>
<tr class="odd">
<td><p>ISAPI 篩選</p></td>
</tr>
<tr class="even">
<td><p>要求監視器</p></td>
</tr>
<tr class="odd">
<td><p>靜態內容</p></td>
</tr>
</tbody>
</table>


Exchange 2010 安裝程式與 Exchange 2007 安裝需要執行 Windows Server 2008 電腦或在其您在已安裝 Mailbox server role 的 Windows Server 2008 R2 電腦已安裝下列 IIS 7 元件。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>信箱伺服器角色所需的 IIS 7 元件</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>基本驗證</p></td>
</tr>
<tr class="even">
<td><p>Windows 驗證</p></td>
</tr>
</tbody>
</table>


若要解決此問題，請遵循適當的步驟所需的 IIS 7 元件的電腦上安裝目的地，然後再次執行 Microsoft Exchange 安裝程式。

使用 Windows Server 2008 伺服器管理員安裝 IIS 7 元件 CAS 伺服器角色

1.  依序按一下 \[開始\]、\[系統管理工具\] 及 \[伺服器管理員\]。

2.  在功能窗格\] 中展開 \[**角色**\]、 用滑鼠右鍵按一下 \[**網頁伺服器 (IIS)** ，然後按一下 \[**新增角色服務**。

3.  在 \[**選取角色服務**\] 窗格中，捲動到**IIS**。

4.  在 \[**安全性**\] 區域中，按一下以選取下列核取方塊：
    
      - **基本驗證**
    
      - **摘要驗證**
    
      - **Windows 驗證**

5.  在 \[**效能**\] 區域中，按一下以選取下列核取方塊：
    
      - **靜態壓縮**
    
      - **動態壓縮**

6.  在 \[**選取角色服務**\] 窗格中，按一下 \[**下一步**，和 \[**安裝**在 \[**確認安裝選項**\] 窗格中。

7.  按一下 \[**關閉**結束 \[新增角色服務精靈\]。

使用 Windows Server 2008 伺服器管理員安裝 Mailbox server role IIS 7 元件

1.  依序按一下 \[開始\]、\[系統管理工具\] 及 \[伺服器管理員\]。

2.  在功能窗格\] 中展開 \[**角色**\]、 用滑鼠右鍵按一下 \[**網頁伺服器 (IIS)** ，然後按一下 \[**新增角色服務**。

3.  在 \[**選取角色服務**\] 窗格中，捲動到**IIS**。

4.  在 \[**安全性**\] 區域中，按一下以選取下列核取方塊：
    
      - **基本驗證**
    
      - **Windows 驗證**

5.  在 \[**選取角色服務**\] 窗格中，按一下 \[**下一步**，和 \[**安裝**在 \[**確認安裝選項**\] 窗格中。

6.  按一下 \[**關閉**結束 \[新增角色服務精靈\]。


---
title: '簡化 Outlook Web App URL: Exchange 2013 Help'
TOCTitle: 簡化 Outlook Web App URL
ms:assetid: 5fb6a873-f3cf-4f82-87d1-2ff6e47a0080
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998359(v=EXCHG.150)
ms:contentKeyID: 54652588
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 簡化 Outlook Web App URL

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-07-16_

**摘要：** 使用本文中的程序簡化 URL，以存取 Exchange 2013 中的 OWA 您組織的使用者。

您可以簡化使用者用來存取其Exchange Server 2013信箱MicrosoftOutlook Web App URL。

為了簡化Outlook Web App存取的使用者，您可能要設定Outlook Web App Web\] 頁面上，通常是在 IIS 中，若要自動將使用者重新導向至 https 的預設網站。此程序中"使用 IIS 管理員來簡化 Outlook Web App URL 並強制重新導向至 SSL"\] 區段中會要求重新導向的 http://*server*至 https://*server*/owa。若要協助保護用戶端與伺服器之間傳送的資訊、 預設的網站會設為安裝時需要安全通訊端層 (SSL)。

設定時重新導向從最上層的目錄中Windows Server 2008，這些設定傳播到較低層級目錄。例如，設定時重新導向至 /owa 虛擬目錄的預設網站，您設定的設定也會出現在所有的虛擬目錄，例如 /Autodiscover、 /Exchange，以及 /Public HTTP 重新導向頁面。因此，您必須將重新導向移除一個您想要重新導向以外的所有虛擬目錄。

## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱在 \[Outlook Web App 權限\] 區段中的[用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的"IIS Manager"項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 步驟 1： 使用 IIS 管理員來簡化 Outlook Web App URL 並強制重新導向至 SSL

1.  啟動 \[IIS 管理員\]。

2.  依序展開 \[本機電腦、 依序展開 \[**網站**\] 和 \[ **Default Web Site**。

3.  在 \[預設網站首頁\] 窗格底端，按一下 \[**功能檢視**\] 如果不已選取此選項。

4.  在 \[ **IIS** \] 區段中，按兩下 \[ **HTTP 重新導向**。

5.  選取 \[**將此目的地的要求重新導向**\] 核取方塊。

6.  輸入 /owa 虛擬目錄的絕對路徑。例如，輸入**https://mail.contoso.com/owa**。

7.  在**重新導向行為**\] 下選取 \[**僅將此目錄 （不子目錄） 中的內容要求重新導向**\] 核取方塊。

8.  **狀態碼**清單中，按一下 \[**已找到 (302)**。

9.  在 \[動作\] 窗格中，按一下 \[**套用\]**。

10. 按一下 \[**預設的網站**。

11. 在 \[預設網站首頁\] 窗格中按兩下 \[ **SSL 設定**\]。

12. 在 \[ **SSL 設定**\] 中，清除**需要 SSL**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您未清除 [<strong>需要 SSL</strong>，將不會將使用者重新導向輸入時，就不安全的 URL。而是他們將取得拒絕存取錯誤。</td>
    </tr>
    </tbody>
    </table>


## 步驟 2： 將重新導向移除虛擬目錄

若要移除的虛擬目錄的重新導向，請執行下列步驟：

1.  開啟 \[命令提示字元\] 視窗。

2.  瀏覽至 \[\<*Window directory*\> \\System32\\Inetsrv。

3.  執行下列命令：
    
    1.  `appcmd set config "Default Web Site/autodiscover" /section:httpredirect /enabled:false -commit:apphost`
    
    2.  `appcmd set config "Default Web Site/ecp" /section:httpredirect /enabled:false -commit:apphost`
    
    3.  `appcmd set config "Default Web Site/ews" /section:httpredirect /enabled:false -commit:apphost`
    
    4.  `appcmd set config "Default Web Site/owa" /section:httpredirect /enabled:false -commit:apphost`
    
    5.  `appcmd set config "Default Web Site/oab" /section:httpredirect /enabled:false -commit:apphost`
    
    6.  `appcmd set config "Default Web Site/powershell" /section:httpredirect /enabled:false -commit:apphost`
    
    7.  `appcmd set config "Default Web Site/rpc" /section:httpredirect /enabled:false -commit:apphost`
    
    8.  `appcmd set config "Default Web Site/rpcwithcert" /section:httpredirect /enabled:false -commit:apphost`
    
    9.  `appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:httpredirect /enabled:false -commit:apphost`

4.  執行命令`iisreset/noforce`來完成。

當您設定從一個最上層的目錄重新導向時，可能是 \<*drive*\> \\Program Files\\Microsoft\\Exchange Server\\ \<*version*\> \\ClientAccess\\oab 下建立 web.config 檔案。如果已發生此事件，您稍後移除重新導向Outlook可能會凍結當使用者按一下 \[**傳送及接收**。若要避免發生這種情形之後移除重新導向，請從 \<*drive*\> \\Program Files\\Microsoft\\Exchange Server\\ \<*version*\> \\ClientAccess\\oab 刪除 web.config 檔案。

## 如何知道這是否正常運作？

若要確認您已順利簡體中文Outlook Web App URL 並導向至 SSL 連線，請執行下列動作：

1.  開啟網頁瀏覽器並Outlook Web App、 使用的格式輸入新的 URL http://\< ；*URL*\>。

2.  您應該重新導向至 SSL 連線到登入頁面Outlook Web App 。


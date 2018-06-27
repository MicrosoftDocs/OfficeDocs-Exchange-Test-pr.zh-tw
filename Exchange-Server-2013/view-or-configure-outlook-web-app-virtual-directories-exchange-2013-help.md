---
title: '檢視或設定 Outlook Web App 虛擬目錄: Exchange 2013 Help'
TOCTitle: 檢視或設定 Outlook Web App 虛擬目錄
ms:assetid: 90babcf6-4486-4e01-9819-6d3ca4ed756c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298140(v=EXCHG.150)
ms:contentKeyID: 50473739
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視或設定 Outlook Web App 虛擬目錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-08-12_

可以使用 EAC 或命令介面檢視或設定 Outlook Web App 虛擬目錄的內容。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange Online 中，系統管理員無法檢視或設定 Outlook Web App 虛擬目錄。</td>
</tr>
</tbody>
</table>


如果使用命令介面來檢視 Outlook Web App 虛擬目錄的內容，則傳回的資訊只會是可用資訊的子集。例如，如果使用 **Get-OWAVirtualDirectory** 指令程式來檢視內容，則 Exchange 會傳回下列資訊：

  - 虛擬目錄名稱

  - 伺服器名稱

  - Exchange 伺服器版本

透過使用可用參數，還可以在特定伺服器上擷取特定虛擬目錄的資訊。如需 **Get-OWAVirtualDirectory** 指令程式參數的相關資訊，請參閱 [Get-OwaVirtualDirectory](https://technet.microsoft.com/zh-tw/library/aa998588\(v=exchg.150\))。

如果使用 EAC 來檢視 Outlook Web App 虛擬目錄的屬性，則可以檢視您正在檢視之虛擬目錄的大部分屬性。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「Outlook Web App 虛擬目錄」項目。

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


## 您要執行的工作

## 使用 EAC 檢視或設定 Outlook Web App 虛擬目錄屬性

1.  在 EAC 中，按一下 \[伺服器\] \> \[虛擬目錄\]。
    
    您可使用下拉式清單選取伺服器和虛擬目錄類型。根據預設，會顯示所有的伺服器和虛擬目錄。

2.  在結果窗格中，按一下您想檢視或編輯的虛擬目錄，然後一下 \[編輯\]。

3.  
    
    在 **\[一般\]** 索引標籤上，您可以檢視 Outlook Web App 預設網站的屬性，並指定外部 URL 和內部 URL。檢視或選取以下選項：
    
      - **伺服器**   (唯讀)**\[伺服器\]** 會顯示主控 Outlook Web App 虛擬目錄的伺服器名稱。
    
      - **版本**   (唯讀)**\[版本\]** 會顯示虛擬目錄所在的 Exchange 伺服器版本。
    
      - **網站**   (唯讀)\[網站\] 會顯示網站名稱。
    
      - **Outlook Web 應用程式版本**    (唯讀)**\[Outlook Web App 版本\]** 會顯示 Exchange 伺服器版本。
    
      - **修改日期**   (唯讀)\[修改日期\] 會顯示虛擬目錄上次修改的日期及時間。
    
      - \[內部 URL\]   在此文字方塊中，指定用於從內部網路存取此網站的 URL。Exchange 2013 安裝期間會自動設定內部 URL。網際網路對向或非網際網路對向伺服器的預設內部 URL 設定是 https://\<Computer Name\>/owa。
    
      - \[外部 URL\] 在此文字方塊中，指定用於從網際網路存取網站的 URL。\[外部 URL\] 預設為空白。對於面對網際網路的 Client Access Server，**\[外部 URL\]** 應該設定為在 DNS 中針對該 Active Directory 站台發佈的值。對於未顯現在網際網路上的 Exchange 2013 伺服器，\[外部 URL\] 設定則應保持空白。

4.  
    
    在 \[驗證\] 索引標籤上，指定驗證方法、簽入格式和簽入網域。
    
      - \[使用一或多個標準驗證方法\] 選擇此選項以使用下列一個或多個標準驗證方法：
        
        **整合式 Windows 驗證**   此方法要求使用者必須具備有效的 Windows Server 2008 或 Windows Server 2012 使用者帳戶名稱及密碼，才能存取資訊。系統不會提示使用者其帳戶名稱和密碼。不過，伺服器會透過安裝在用戶端電腦上的 Windows 安全性套件進行交涉。整合式 Windows 驗證使伺服器不需提示使用者輸入資訊，且不需透過網路傳輸未加密的資料即可驗證使用者。為了讓這個方法運作，用戶端電腦必須是與執行 Exchange 之伺服器位於相同網域的成員，或是含有 Exchange 伺服器之網域所信任網域的成員。
        
        **Windows 網域伺服器的摘要驗證** 這個方法會將密碼以雜湊值的形式，透過網路來傳輸，以增加安全性。摘要驗證只能在 Windows Server 2008 和 Windows Server 2012 網域中使用，供具有儲存在 Active Directory 中之帳戶的使用者使用。如需摘要驗證的相關資訊，請參閱 Windows Server 文件。
        
        **基本驗證 (密碼以純文字格式傳送)** 這個方法是以 HTTP 規格來定義的簡易型驗證機制，可以在將使用者的認證傳送到伺服器之前，先將使用者的登入名稱及密碼編碼。為提高密碼的安全性，您應在用戶端電腦與安裝 Client Access server role 的伺服器之間，使用安全通訊端層 (SSL) 加密。
    
      - **使用表單型驗證** 表單型驗證提供 Outlook Web App 虛擬目錄的增強的安全。表單型驗證建立 Outlook Web App 的簽入頁。您可以設定表單型驗證所使用的簽入提示類型。例如，您可以設定表單型驗證來要求使用者在 Outlook Web App 簽入頁面上，以網域\\使用者名稱的格式來提供其網域及使用者名稱資訊。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>表單型驗證不提供安全通道，除非啟用 SSL。</td>
        </tr>
        </tbody>
        </table>
        
        選取下列其中一項：
        
        **網域\\使用者名稱**   此項需要使用者以網域\\使用者名稱的格式輸入其網域和使用者名稱。例如，如果使用者名稱為 Kweku 且位於 Contoso 網域，那麼簽入名稱將為 contoso\\kweku。
        
        **使用者主體名稱 (UPN)** 如果已指定使用者主體名稱 (UPN) 簽入格式，Outlook Web App 簽入頁面上的 **\[使用者名稱\]** 方塊會指引使用者輸入其電子郵件地址，例如 kweku@contoso.com。如果使用者的 UPN 與電子郵件地址不同，使用者將無法使用 **PrincipalName** 簽入提示存取 Outlook Web App。只有在使用者的 UPN 與其電子郵件地址相符時，使用 **PrincipalName** 簽入提示是最好的做法。
        
        **僅使用者名稱** 使用者僅輸入其使用者名稱即可，不需輸入網域名稱，例如 Kweku。如果您使用 \[僅使用者名稱\] 簽入提示進行表單型驗證，則也必須指定 \[登入網域\] 屬性。**\[登入網域\]** 屬性決定當使用者嘗試登入 Outlook Web App 時，所要使用的預設網域。例如，如果預設網域為 Contoso，而簽入 Outlook Web App 的網域使用者名稱為 Kweku，那麼只需輸入 Kweku 作為使用者名稱。伺服器將會使用預設網域 Contoso。如果使用者不是 Contoso 網域的成員，就必須輸入網域及使用者名稱。

5.  
    
    使用 **\[功能\]** 索引標籤，為虛擬目錄上的 Outlook Web App 使用者指定您想要啟用或停用的功能。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>個別使用者的功能設定會覆寫虛擬目錄設定。使用 <strong>Set-CASMailbox</strong> 指令程式，或使用 Outlook Web App 信箱原則，可以變更個別使用者的分割設定。如需詳細資訊，請參閱 <a href="outlook-web-app-mailbox-policies-exchange-2013-help.md">Outlook Web App 信箱原則</a>。</td>
    </tr>
    </tbody>
    </table>
    
    使用核取方塊來啟用或停用功能。最常用的功能預設為顯示。若要查看所有可啟用或停用的功能，請按一下 \[其他選項\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>使用 <strong>[高階用戶端]</strong> 核取方塊來啟用或停用標準版 Outlook Web App 的方式已過時，將會從設定中移除。標準版 Outlook Web App 一律會啟用。</td>
    </tr>
    </tbody>
    </table>


6.  
    
    在 \[檔案存取\] 索引標籤上，勾選核取方塊來設定使用者的檔案存取和檢視選項。檔案存取可讓使用者開啟或檢視已附加到電子郵件的檔案內容。
    
    檔案存取可根據使用者是否登入公用或私人電腦進行控制。供使用者選取私人電腦存取或公用電腦存取的選項只有在使用表單型驗證時才可以使用。所有其他形式的驗證預設為私人電腦存取。
    
      - \[直接檔案存取\]   如果您要啟用直接檔案存取，請選取此核取方塊。直接檔案存取可讓使用者開啟電子郵件附加檔案。
    
      - \[WebReady 文件檢視\]   若要將支援的文件轉換為 HTML，並且在網頁瀏覽器中顯示，請選取此核取方塊。
    
      - \[在有轉換程式可用時強制執行 WebReady 文件檢視\]   若要強制先將文件轉換為 HTML，並且在網頁瀏覽器中顯示，再讓使用者在檢視應用程式中開啟這些文件，請選取此核取方塊。只有啟用 \[直接檔案存取\] 之後，才能在檢視應用程式中開啟文件。

7.  按一下 \[儲存\] 以更新原則。

## 使用命令介面設定 Outlook Web App 虛擬目錄內容

本範例啟用 Contoso 伺服器之預設 Outlook Web App 虛擬目錄上的表單型驗證。

    set-OwaVirtualDirectory -Identity "Contoso\owa (default web site)" -FormsAuthentication $true

如需語法及參數的相關資訊，請參閱 [Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-tw/library/bb123515\(v=exchg.150\))。

## 使用命令介面檢視 Outlook Web App 虛擬目錄內容

此範例讓您檢視所有網際網路資訊服務 (IIS) 網站上之所有 Outlook Web App 虛擬目錄的屬性，而這類網站位在 Exchange 組織中所有已安裝用戶端存取伺服器角色的電腦上。

    Get-OWAVirtualDirectory

此範例讓您在本機Outlook Web App 伺服器的預設 IIS 網站上檢視 Exchange 虛擬目錄的屬性。

    Get-OWAVirtualDirectory -identity "<Exchange Server Name>\owa (default web site)"

此範例讓您在特定 Outlook Web App 伺服器的 IIS 網站上檢視所有 Exchange 虛擬目錄的屬性。

    Get-OWAVirtualDirectory -server <Exchange Server Name>

此範例讓您檢視所有 IIS 網站上每個 Outlook Web App 虛擬目錄的屬性值，而這類網站位在 Exchange 組織中的所有用戶端存取伺服器上。

    Get-OWAVirtualDirectory | format-list

如需語法及參數的相關資訊，請參閱 [Get-OwaVirtualDirectory](https://technet.microsoft.com/zh-tw/library/aa998588\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否已成功編輯 Outlook Web App 虛擬目錄：

1.  在 EAC 中，按一下 **\[伺服器\]** \> **\[虛擬目錄\]**，然後再選擇指定的 Outlook Web App 虛擬目錄。

2.  按一下 \[編輯\] 按鈕以檢視虛擬目錄的屬性。

3.  按一下 \[儲存\] 或 \[取消\] 關閉內容頁面。


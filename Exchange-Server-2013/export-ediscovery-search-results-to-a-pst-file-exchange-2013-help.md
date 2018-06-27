---
title: '將 eDiscovery 搜尋結果匯出至 PST 檔: Exchange Online Help'
TOCTitle: 將 eDiscovery 搜尋結果匯出至 PST 檔
ms:assetid: bc47f5f9-d056-4b69-b669-ae65fad541c8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn440164(v=EXCHG.150)
ms:contentKeyID: 59637247
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將 eDiscovery 搜尋結果匯出至 PST 檔

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2017-09-07_

您可以使用Exchange 系統管理中心 (EAC) 中的 eDiscovery 匯出工具為 「 就地 eDiscovery 搜尋結果匯出至 Outlook 資料檔案，也稱為 PST 檔案。系統管理員可以分散給您的組織，像是人力資源管理員或記錄管理員內其他人或敵對顧問法律案例中的搜尋結果。搜尋結果匯出至 PST 檔案之後，您或其他使用者可以開啟其檢閱或列印郵件搜尋結果中傳回在 Outlook 中。也可以與協力廠商 eDiscovery 及報告應用程式中開啟 PST 檔案。本主題顯示如何達成此目的，以及疑難排解您可能會有任何問題。

## 開始之前有哪些須知？

  - 預估完成時間：時間會因要匯出的搜尋結果數量和大小而有所不同。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的 「 就地 eDiscovery 」 項目。

  - 您用來將搜尋結果匯出至 PST 檔案的電腦必須符合下列系統需求：
    
      - 32 或 64 位元版本的 Windows 7 或更新版本
    
      - Microsoft.NET Framework 4.7
    
      - 支援的瀏覽器：
        
          - Internet Explorer 10 及更新版本
            
            或
        
          - Mozilla Firefox 或 Google Chrome。如果您使用其中一個這些瀏覽器，請務必安裝*ClickOnce*延伸。若要安裝 ClickOnce 增益集，請參閱[Mozilla ClickOnce 附加元件](https://addons.mozilla.org/en-us/firefox/search/?q=clickonce%26cat=1%2c0%26appver=%26platform=)或[Google Chrome 的 ClickOnce](https://chrome.google.com/webstore/search/clickonce?_category=extensions)。

  - 您必須附加到您想要匯出的帳戶作用中信箱。

  - 確定本機的內部網路設定 Internet Explorer 中正確設定。請確定該**https://\*.outlook.com**新增至近端內部網路區域。

  - 請確定 \[受信任的網站\] 區域中未列出下列 URL：
    
      - https://\*.outlook.com
    
      - https://r4.res.outlook.com
    
      - https://\*.res.outlook.com

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


## 使用Exchange 系統管理中心就地 eDiscovery 搜尋結果匯出至 PST

1.  移至 \[規範管理\] \> \[就地 eDiscovery 和保留\]。

2.  在清單檢視中，選取您要匯出其結果的就地 eDiscovery 搜尋，然後按一下 \[匯出成 PST 檔案\]。
    
    ![匯出到 PST 檔案](images/Dn440164.1ebee2ac-89b3-49fa-b70c-a07c9a65f958(EXCHG.150).gif "匯出到 PST 檔案")  

3.  在 \[eDiscovery PST 匯出工具\] 視窗中，執行下列作業：
    
      - 按一下 \[瀏覽\] 以指定您要下載 PST 檔案的位置。
    
      - 按一下 \[啟用重複資料刪除\] 核取方塊，以排除重複的郵件。郵件只會有一個執行個體包含在 PST 檔案中。
    
      - 按一下 \[包含無法搜尋的項目\] 核取方塊，以包含無法搜尋的信箱項目 (例如，Exchange 搜尋無法為其附件檔案類型建立索引的郵件)。無法搜尋的項目會被匯出成個別的 PST 檔案。
        
        <table>
        <colgroup>
        <col style="width: 100%" />
        </colgroup>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果信箱包含許多無法搜尋的項目，在您匯出 eDiscovery 搜尋結果時包含無法搜尋的項目會花較長的時間。若要減少匯出搜尋結果所花的時間，並避免大型 PST 匯出檔案，請考慮下列建議：
        <ul>
        <li><p>建立分別搜尋較少來源信箱的多個 eDiscovery 搜尋。</p></li>
        <li><p>如果您要匯出特定日期範圍內的所有信箱內容 (透過不在搜尋準則中指定任何關鍵字的方式)，搜尋結果會自動包含該日期範圍內所有無法搜尋的項目。因此，請勿選取 <strong>[包含無法搜尋的項目]</strong> 核取方塊。</p></li>
        </ul></td>
        </tr>
        </tbody>
        </table>


4.  按一下 \[開始\] 來將搜尋結果匯出成 PST 檔案。
    
    包含匯出程序狀態資訊的視窗便會隨即顯示。

## 其他資訊

  - 您可以減少匯出無法搜尋之項目的 PST 匯出 fileby 的大小。若要這樣做，建立或編輯搜尋、 指定未來、 開始日期，然後從 \[**關鍵字**\] 方塊中移除任何關鍵字。這會產生任何所傳回的搜尋結果中。當您複製或匯出搜尋結果並選取**包含無法搜尋的項目**\] 核取方塊時，只有無法搜尋的項目會複製到探索信箱或匯出至 PST 檔案。

  - 如果啟用重複資料刪除，則所有的搜尋結果會匯出成單一 PST 檔案。如果未啟用重複資料刪除，則會為每個包含在搜尋中的信箱匯出個別的 PST 檔案。就像前面所說的，無法搜尋的項目會被匯出成個別的 PST 檔案。

  - 除了包含搜尋結果的 PST 檔案，還會匯出其他兩個檔案：
    
      - 包含 PST 匯出要求相關資訊的組態檔 (.txt 檔案格式)，例如所匯出的 eDiscovery 搜尋名稱、匯出的日期和時間、是否啟用重複資料刪除和無法搜尋的項目、搜尋查詢以及所搜尋的來源信箱。
    
      - 搜尋結果記錄 (.csv 檔案格式)，內容包含搜尋結果中傳回的各個郵件項目。每個項目可識別郵件所在的來源信箱。如果已啟用重複資料刪除，這可協助您識別所有包含重複郵件的信箱。

  - 每個匯出檔案的檔案名稱第一部分會是搜尋的名稱。另外，每個 PST 檔案及結果記錄的檔案名稱都會加上匯出要求的日期和時間。

  - 如需重複資料刪除和無法搜尋之項目的詳細資訊，請參閱：
    
      - [Estimate, preview, and copy search results](in-place-ediscovery-exchange-2013-help.md)
    
      - [Exchange eDiscovery 中項目\] 無法搜尋](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

  - 若要從 SharePoint 或 SharePoint Online 中的 eDiscovery 中心匯出 eDiscovery 搜尋結果，請參閱[匯出 eDiscovery 內容並建立報告](https://go.microsoft.com/fwlink/p/?linkid=324757)。

## 疑難排解


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>問題</th>
<th>可能的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>無法匯出成 PST 檔案。</p></td>
<td><ul>
<li><p>附加至帳戶沒有作用中信箱。若要匯出 PST，您必須具備作用中的帳戶。</p></li>
<li><p>您的 Internet Explorer 版本已過期。嘗試更新 IE 版本 10 或更新版本。或嘗試在不同的瀏覽器。</p></li>
<li><p>在 [<strong>篩選依據準則</strong>的查詢輸入的搜尋準則不正確。例如，而不是電子郵件地址輸入使用者名稱。如需關於如何篩選依據準則，請參閱<a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">修改就地 eDiscovery 搜尋</a>。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>無法匯出特定電腦上的搜尋結果。匯出的運作如預期般在不同的電腦上。</p></td>
<td><p>在 [<strong>認證管理員</strong>儲存了錯誤的 Windows 認證。清除您的認證，然後再次登入。</p></td>
</tr>
<tr class="odd">
<td><p>eDiscovery PST 匯出工具不會開始。</p></td>
<td><p>近端內部網路區域設定不正確設定 Internet Explorer 中。請確定 *。 outlook.com、 *。 office365.com、 *。 sharepoint.com 和 *。 onmicrosoft.com 會新增至 [近端內部網路區域信任的網站。</p>
<p>若要將這些網站新增至 [信任的區域 IE 中，請參閱<a href="https://windows.microsoft.com/en-us/windows/security-zones-adding-removing-websites#1tc=windows-7">安全性區域： 新增或移除網站</a>。</p></td>
</tr>
</tbody>
</table>


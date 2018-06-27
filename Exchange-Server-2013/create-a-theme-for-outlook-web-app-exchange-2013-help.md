---
title: '建立 Outlook Web App 的佈景主題: Exchange 2013 Help'
TOCTitle: 建立 Outlook Web App 的佈景主題
ms:assetid: 7e1fa13c-3de3-45c2-b1fa-e74fc8487bda
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201700(v=EXCHG.150)
ms:contentKeyID: 54652594
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立 Outlook Web App 的佈景主題

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

*佈景主題*定義背景色彩、 字型、 醒目提示色彩、 圖示和MicrosoftOutlook Web App所使用的標頭。每一個佈景主題是一組媒體檔案和MicrosoftExchange中的伺服器安裝目錄 \\Client Access\\OWA\\prem\\*version*\\resources\\themes 中儲存的階層式樣式表 (.css) 檔案。每一個佈景主題會儲存在其專屬的 \\themes 子目錄。

預設佈景主題是 \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base 中找到。每一個佈景主題\] 資料夾包含定義佈景主題所需的所有檔案。這些檔案包含 CSS 檔案、 圖形和佈景主題的名稱會定義.xml 檔案。從一個佈景主題的所有檔案都複製到新的資料夾及依需要修改這些檔案所建立額外的佈景主題。

根據預設，在您安裝 Exchange Server 2013 時會安裝多個主題，如下所示：

  - CSS (.css) 檔定義色彩、漸層及字型。

  - 圖像 (.png) 檔案提供圖示及其他圖形元素。如果您編輯任何圖示，並不會變更其大小。如果您變更圖形的任何項目大小、，測試以確認該元素仍相互整合正常變更。

這些檔案儲存在 \\Client Access\\OWA\\prem\\*\<version\>*\\resources\\themes 的安裝目錄中的用戶端存取伺服器上。每一個佈景主題已儲存的佈景主題的子目錄。您可以藉由複製現有的佈景主題及修改複本建立額外的佈景主題。

建立主題之後，您可能也想要[自訂 Outlook Web App 登入、語言選擇與錯誤頁面](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Light 版 Outlook Web App 不支援主題。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您有支援Outlook Web App的多部伺服器，您必須將您的自訂佈景主題複製至每部伺服器。您也應該建立您的自訂佈景主題的備份複本。如果您重新安裝或升級Exchange、 佈景主題] 資料夾中的所有檔案會都被覆寫。您必須將複製到您的佈景主題回適當的資料夾後再重新安裝或升級已完成。<br />
在您開始建立自訂主題之前，備份將會變更的所有檔案。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 完成這項工作預估時間： 60 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「Outlook Web App 虛擬目錄」項目。

  - 您需要有本機伺服器系統管理員權限，才能執行這些程序。

  - 您需要變更預設的色彩、 文字編輯器和圖形編輯器來變更的圖像。如果您必須符合特定色彩與您找不到相符項目為其在[色彩表](https://go.microsoft.com/fwlink/p/?linkid=280679)，您可以使用編輯工具映像的範例色彩，並判斷其 HTML RGB 值。

  - 建議的最佳作法是，只要是變更或建立 Outlook Web App 主題，就使用下列指導方針：
    
      - 如果決定編輯現有的主題，請在開始編輯之前，先備份原始檔案。
    
      - 不要刪除資料夾 \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base 或任何的檔案。

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


## 該怎麼做？

## 步驟 1： 建立新的 Outlook Web App 佈景主題

若要開始，要先建立新主題的資料夾，然後將現有主題中的檔案複製到新資料夾中。

1.  使用委派了本機 Administrators 群組成員資格的帳戶，登入主控 Outlook Web App 虛擬目錄的 Exchange Server。

2.  開啟 Windows 檔案總管，找到 Exchange 伺服器安裝目錄。

3.  在 \\Client Access\\OWA\\prem\\*version*\\resources\\themes，建立新的資料夾，並命名，例如 Fourth Coffee。

4.  將其他主題中的所有檔案複製到新資料夾中。

## 步驟 2： 命名新的佈景主題

若要設定新主題的顯示名稱，請執行下列工作：

1.  開啟自訂主題資料夾中剛才建立的 themeinfo.xml 複本。

2.  尋找佈景主題`displayname`值，並將值變更為您想要使用的名稱。例如`displayname = "Fourth Coffee Theme"`。

3.  儲存及關閉 themeinfo.xml。

## 步驟 3： 變更排序順序在新的佈景主題 （選用）

如果您想，您可以藉由編輯 themeinfo.xml 檔案變更新的佈景主題的排序順序。排序順序會決定在**變更佈景主題**\] 面板中 \[設定\] 功能表中的佈景主題位置。

若要使用 themeinfo.xml 檔案變更新主題的排序順序，請執行下列工作：

1.  開啟自訂主題資料夾中 themeinfo.xml 的複本。

2.  找出佈景主題`sortorder`值，並變更以反映您想要在新的佈景主題\] 清單中顯示的值。佈景主題會依遞增順序數值的順序排列。根據預設，基底的佈景主題是第一個和其`sortorder`值是"0"。例如`sortorder="<number>"`。

3.  儲存及關閉 themeinfo.xml。

## 步驟 4： 修改新的佈景主題

既然您已透過將檔案複製並具備名為您的佈景主題，您就可以進行自訂。可以自訂Outlook Web App佈景主題中的下列元素：

  - 影像檔，用於定義標頭區域和圖示。

  - CSS 檔，用於定義字型和色彩。

## 影像檔

佈景主題圖像儲存在 \\themes*\\\<theme name\>*\\images\\ 中的兩個資料夾中。\\Images\\0 資料夾包含將使用中 （如英文）、 以從左至右語言的圖像及讀取從右至左的語言會使用 \\images\\rtl 資料夾中的圖像。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>\images\rtl 資料夾中有些影像與 \images\0 資料夾中的影像相同，但為鏡像影像。</td>
</tr>
</tbody>
</table>


若要自訂主題，可使用影像編輯工具來開啟和修改下列影像：

  - Headerbgmain.png
    
      - 這是主要的標頭映像。建議您將圖像不會超過 30 像素為單位的標頭高度。預設佈景主題不使用背景影像，所以此影像中是透明。具有自訂背景影像的佈景主題的範例，請參閱**藍圖**佈景主題資料夾中的影像。

  - Headerbgright.png
    
      - 這會做為背後的標頭的並排顯示圖像。預設佈景主題不使用磁磚效果背景影像，所以此影像中是透明。如有自訂磁磚效果背景影像，請參閱映像的**藍圖**佈景主題資料夾中的佈景主題的範例。

  - sprite1.mouse.png
    
      - 這包含大部分的佈景主題中所使用的圖像。您可以變更色彩以符合您的佈景主題、 影像及也變更預設Outlook Web App文字標誌。
    
      - 為了避免發生問題，請勿變更小精靈中個別圖示的大小，並確保已儲存為透明的 .png 檔案。

  - themepreview.png
    
      - 此影像將用來表示 Outlook Web App 的 \[設定\] 功能表中 **\[變更主題\]** 面板中的主題。

## 色彩和字型

階層式樣式表 (.css) 檔案定義的色彩和字型佈景主題中所使用並儲存在多個資料夾下 \\themes\\*\<theme name\>*。\\*\<theme name\>*\\0 資料夾包含將使用中 （如英文）、 以從左至右語言的.css 檔案與讀取從右至左的語言將使用中的.css 檔案 \\*\<theme name\>*\\rtl 資料夾。也有特定語言的資料夾 （例如 \\ja、 \\ko、 \\zhs 及 \\zht） 包含.css 檔案與這些語言搭配使用。

修改以啟動 \\*\<theme name\>*\\images\\0 資料夾。有四個整個每個可自訂的佈景主題的色彩。

  - BrandColor: \#0072C 6

  - NavBarHoverColor: \# 4C9CD7

  - UnreadColor: \# 2A8DD4

  - FocusColor: \#DFEDFA

您可以使用 \[記事本\] 之類的文字編輯器來搜尋並個值的所有執行個體取代為您在下列兩個檔案中的佈景主題色彩： owa2styles.mouseCSS 和 owa2styles2.mouseCSS。這就是您新的佈景主題包含這些.css 檔案中的每個資料夾中。

## 步驟 5： 設定的預設 Outlook Web App 佈景主題

設定新的預設主題，只會影響尚未透過 Outlook Web App 的 \[設定\] 功能表變更其主題的使用者。

若要強制所有使用者採用預設主題，除了設定預設主題，您還必須禁止選擇主題。

## 使用命令介面設定 Outlook Web App 的預設主題

此範例會設定 Outlook Web App 的預設主題，其中伺服器名稱為 `fourthcoffee`、虛擬目錄名稱為 `owa`、網站名稱為 `default web site`，且主題位於名為 `Custom` 的資料夾內。

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom 

如需詳細的語法及參數資訊，請參閱 [Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-tw/library/bb123515\(v=exchg.150\))。

## 使用命令介面停用 Outlook Web App 的主題選取功能

此範例會停用 Outlook Web App 中的主題選取功能，其中伺服器名稱為 `fourthcoffee`、虛擬目錄名稱為 `owa`，且網站名稱為 `default web site`。

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -themeselectionenabled $false 

您也可以同時完成這兩個命令，如下列範例所示：

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom -themeselectionenabled $false

如需詳細的語法及參數資訊，請參閱 [Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-tw/library/bb123515\(v=exchg.150\))。

## 步驟 6： 執行 iisreset/noforce 儲存的變更

如果您新增或變更佈景主題、 變更的佈景主題的名稱或變更佈景主題的排序順序，您必須停止及啟動網際網路資訊服務 (IIS)，變更才會生效。若要這樣做，開啟命令提示字元\] 視窗的伺服器上您已在其中建立新的佈景主題，並執行命令**iisresest /nforce**。

## 如何才能了解此工作是否正常運作？

1.  登入Outlook Web App您已在其中建立新的佈景主題之伺服器上使用的虛擬目錄。如果您正在測試Exchange伺服器主控Outlook Web App虛擬目錄上的預設網站的變更，您可以開啟Internet Explorer然後輸入 URL https://localhost/owa 測試您的佈景主題。

2.  選取 \[設定\] 功能表 \> **\[變更主題\]** 並選取自訂主題，切換至您的自訂主題。

## 如果您沒有看到最近所做的變更且已執行 iisreset/noforce

1.  在 Internet Explorer 工具列上，選取 \[設定\] 功能表 \> **\[網際網路選項\]**。

2.  在 \[**一般**\] 索引標籤的 \[**瀏覽歷程記錄**\] 下選取**刪除**，然後驗證會檢查**網際網路暫存檔及網站檔案**。然後選取 \[**刪除**\] 以移除這些檔案。

3.  選取 **\[確定\]**，關閉 **\[網際網路選項\]**。

4.  選取 **\[重新整理\]** 以查看變更。

您可能必須重複這些步驟以檢視您的變更每次您對佈景主題檔案進行變更。如果您正在進行數項變更，您可以讓Outlook Web App保持開啟，並重複執行**iisreset/noforce**伺服器與清除暫存檔從Internet Explorer視上。


---
title: '自訂 Outlook Web App 登入、語言選擇與錯誤頁面: Exchange 2013 Help'
TOCTitle: 自訂 Outlook Web App 登入、語言選擇與錯誤頁面
ms:assetid: d8d9f735-7181-428f-9049-b9886dce5159
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee633483(v=EXCHG.150)
ms:contentKeyID: 54652607
ms.date: 01/12/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自訂 Outlook Web App 登入、語言選擇與錯誤頁面

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

本主題說明如何自訂 Outlook Web App 中登入、語言選擇與錯誤頁面的色彩和影像。

Outlook Web App 登入、語言選擇與錯誤頁面是根據主題資源資料夾中的圖形和 .css 檔案來建立。對於所有主題，Outlook Web App 只使用一組登入、語言選擇與錯誤頁面。所有使用者都會看到對這些頁面所做的任何修改。您可以在 Exchange 安裝目錄中的 V15\\FrontEnd\\HttpProxy\\owa\\auth\\version\\themes\\resources 中找到主題資源資料夾。您將需要文字編輯器來變更預設的色彩，以及圖形編輯器來變更影像。如果必須搭配特定的色彩，但在[色彩表](https://go.microsoft.com/fwlink/p/?linkid=280679)上找不到相符的色彩，可以使用影像編輯工具來取樣色彩並判定其 HTML RGB 值。

如果您有多部支援 Outlook Web App 的伺服器，且希望它們全都使用相同的登入、語言與錯誤頁面，則必須將修改的檔案複製到每部伺服器中。您也應該建立自訂檔案的備份副本。如果您重新安裝或升級 Exchange，將會覆寫主題資料夾中的所有檔案。在重新安裝或升級完成之後，您必須將自訂檔案複製回適當的資料夾。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在您開始建立自訂的登入與登出頁面之前，請先將所有您會變更的檔案備份。</td>
</tr>
</tbody>
</table>


如需建立自訂主題的詳細資訊，請參閱[建立 Outlook Web App 的佈景主題](create-a-theme-for-outlook-web-app-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：45 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中「Outlook Web App 權限」下方的「圖形編輯器」項目。

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

## 自訂登入頁面的色彩

1.  登入 Exchange 伺服器，使用 Windows 檔案總管移至 Exchange Server 安裝目錄，然後尋找 \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<version\>\\themes\\resources。

2.  使用文字編輯器 (如記事本) 開啟 logon.css。

3.  搜尋預設的色彩值 \#0072c6，並將之取代為您想要使用之色彩的 HTML RGB 值。您可以在下列位置查到 HTML RGB 值：[色彩表](https://go.microsoft.com/fwlink/p/?linkid=280679)。

4.  儲存後關閉檔案。

## 自訂錯誤頁面的色彩

1.  登入 Exchange 伺服器，使用 Windows 檔案總管移至 Exchange Server 安裝目錄，然後尋找 \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<version\>\\themes\\resources。

2.  使用文字編輯器 (如記事本) 開啟 errorFE.css。

3.  搜尋預設的色彩值 \#0072c6，並將之取代為您想要使用之色彩的 HTML RGB 值。您可以在下列位置查到 HTML RGB 值：[色彩表](https://go.microsoft.com/fwlink/p/?linkid=280679)。

4.  儲存後關閉檔案。

## 自訂語言選擇頁面的色彩

1.  登入 Exchange 伺服器，使用 Windows 檔案總管移至 Exchange Server 安裝目錄，然後尋找 \\V15\\Client Access\\OWA\\version\\Owa2\\resources\\styles。

2.  使用文字編輯器 (如記事本) 開啟 LanguageSelection.css。

3.  搜尋預設的色彩值 \#0072c6，並將之取代為您想要使用之色彩的 HTML RGB 值。您可以在下列位置查到 HTML RGB 值：[色彩表](https://go.microsoft.com/fwlink/p/?linkid=280679)。

4.  儲存後關閉檔案。

## 自訂登入與錯誤頁面上的影像

使用影像編輯工具來開啟及編輯用於建立登入與錯誤頁面的影像。

1.  登入 Exchange 伺服器，使用 Windows 檔案總管移至 Exchange Server 安裝目錄，然後尋找 \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<version\>\\themes\\resources。

2.  使用圖形編輯器來開啟及修改下列檔案：
    
      - owa\_text\_blue.png，以變更 “Outlook Web App” 文字標誌。
    
      - olk\_logo\_white.png，以變更左列中的應用程式標誌。
    
      - olk\_logo\_white\_cropped.png，以變更錯誤頁面左側面板中的影像。
    
      - sign\_in\_arrow.png，以變更 \[登入\] 按鈕左側的圖示。
    
      - olk\_exchange\_text\_blue.png，以變更 tnarrow 配置上的 “Outlook Mobile” 標誌。
    
      - tnarrow 中會使用 olk\_logo\_white\_small.png。
    
      - tnarrow 中會使用 olk\_exchange\_text\_stacked\_white\_small.png。

3.  搜尋預設的色彩值 \#0072c6，並將之取代為您想要使用之色彩的 HTML RGB 值。您可以在下列位置查到 HTML RGB 值：[色彩表](https://go.microsoft.com/fwlink/p/?linkid=280679)。

4.  儲存後關閉檔案。

## 如何知道這是否正常運作？

在 Internet Explorer 中開啟 Outlook Web App 登入頁面。如果要在 Outlook Web App 虛擬目錄所在的伺服器上測試對預設網站的變更，可以開啟 Internet Explorer 並輸入 URL https://localhost/owa 來測試。

如果看不到您的變更，請執行下列動作：

1.  在工具列上，依序選取 **\[選項\]** \> **\[網際網路選項\]** \> **\[一般\]**。

2.  在 **\[瀏覽歷程記錄\]** 下方，選取 **\[刪除\]**。

3.  選取 **\[網際網路暫存檔與網站檔案\]**，然後選取 **\[刪除\]**。

4.  當 Internet Explorer 完成刪除時，選取 **\[確定\]** 來關閉 **\[網際網路選項\]**。

5.  重新整理瀏覽器視窗。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要查看變更的效果，可將正在編輯的 .css 檔保持開啟，並且在每次儲存變更之後重新整理瀏覽器視窗。</td>
</tr>
</tbody>
</table>


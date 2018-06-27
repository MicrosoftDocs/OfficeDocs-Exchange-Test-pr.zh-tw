---
title: 'Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync
ms:assetid: 5fafaff3-eb37-4fdb-95f0-e56c45ea5884
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998357(v=EXCHG.150)
ms:contentKeyID: 50473313
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

瞭解 Exchange Server 2013 的 Exchange ActiveSync 用戶端通訊協定。您將瞭解 Exchange ActiveSync 的功能 (包括安全性功能)、您可以管理的事物、如何使其安全，以及如何避免在同步至 Windows Phone 7 時發生問題。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這個主題適用於系統管理員。想要設定 Windows Phone、iOS 或 Android 裝置來存取 Office 365 或 Exchange Server 信箱嗎？請參閱下列主題：
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=615415">在 Windows Phone 上設定電子郵件</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=615414">在 iPhone、iPad 或 iPod Touch 上設定電子郵件</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/?linkid=615417">在 Android 電話或平板電腦上設定電子郵件</a></p></li>
</ul></td>
</tr>
</tbody>
</table>


Exchange ActiveSync 為讓您同步行動裝置與 Exchange 信箱的用戶端通訊協定。在您安裝 Microsoft Exchange 2013 時，Exchange ActiveSync 依據設啟動。

**目錄**

Exchange ActiveSync 概觀

Exchange ActiveSync 中的功能

管理 Exchange ActiveSync

Windows Phone 7 同步處理

## Exchange ActiveSync 概觀

Exchange ActiveSync 是針對配合高延遲與低頻寬網路使用而最佳化的 Microsoft Exchange 同步處理通訊協定。以 HTTP 及 XML 為基礎的通訊協定，可讓行動電話存取在執行 Microsoft Exchange 之伺服器上的組織資訊。Exchange ActiveSync 可讓行動電話使用者存取他們的電子郵件、行事曆、連絡人及工作，並讓他們在離線工作時可繼續存取這項資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange ActiveSync 不支援共用的信箱或代理人存取。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Windows Phone 7 行動電話只支援所有 Exchange ActiveSync 信箱原則設定的子集。如需完整清單，請參閱 Windows Phone 7 同步處理。</td>
</tr>
</tbody>
</table>


## Exchange ActiveSync 中的功能

Exchange ActiveSync 提供下列功能：

  - 支援 HTML 郵件

  - 待處理標幟的支援

  - 電子郵件的交談群組

  - 同步或不同步整個交談的能力

  - 與使用者的 Exchange 信箱同步短訊息服務 (SMS) 郵件

  - 檢視郵件回覆狀態的支援

  - 快速郵件擷取的支援

  - 會議出席者資訊

  - 增強型 Exchange 搜尋

  - PIN 碼重設

  - 透過密碼原則增強的裝置安全性

  - 透過無線傳輸提供的自動探索

  - 支援在使用者離座、休假或不在辦公室時設定自動回覆功能

  - 工作同步處理的支援

  - Direct Push

  - 連絡人的可用性資訊的支援

## 管理 Exchange ActiveSync

依預設，會啟用 Exchange ActiveSync。擁有 Exchange 信箱的所有使用者都可以與 Microsoft Exchange 伺服器同步處理其行動裝置。

您可以執行下列 Exchange ActiveSync 工作：

  - 為使用者啟用及停用 Exchange ActiveSync

  - 設定密碼最小長度、裝置鎖定及密碼嘗試失敗次數上限等原則

  - 啟動遠端抹除，將遺失或被竊行動電話上的所有資料清除

  - 執行各種報告以供檢視或匯出至各種格式

  - 控制哪些類型的行動裝置可透過裝置存取規則與您的組織同步

## Exchange ActiveSync 中的安全性

您可以設定 Exchange ActiveSync 針對 Exchange 伺服器與行動裝置間的通訊使用安全通訊端層 (SSL) 加密。

## 在 Exchange ActiveSync 中管理行動裝置存取

可控制哪些行動裝置可進行同步。可在新的行動裝置連接至您的組織時進行監控，或者建立判斷允許連接的行動裝置類型規則。無論您選擇何種方法來指定可進行同步的行動裝置，皆可隨時核准或拒絕任何來自特定使用者的特定行動裝置存取。

## Exchange ActiveSync 中的裝置安全性功能

除了為 Exchange 伺服器與行動裝置間的通訊設定安全性選項的能力之外，Exchange ActiveSync 還提供下列功能以增強行動裝置的安全性：

  - **遠端抹除**   如果行動裝置遺失、失竊或遭入侵，您可以使用 Exchange Server 從 Outlook Web App 電腦或從任何 Web 瀏覽器發出遠端抹除命令。此命令會清除該行動裝置中所有的資料。

  - **裝置密碼原則**   Exchange ActiveSync 可讓您設定數個裝置密碼選項。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>iOS7 指紋辨識器技術無法做為裝置密碼。如果您選擇使用 iOS7 指紋辨識器，而貴組織的行動裝置信箱原則要求裝置密碼，您仍必須建立和輸入裝置密碼。</td>
    </tr>
    </tbody>
    </table>
    
    裝置密碼選項包含下列：
    
      - **密碼長度下限 (字元數)**   此選項會指定行動裝置的密碼長度。預設長度是 4 個字元，但最多可包含 18 個字元。
    
      - **最小字元集數**   使用此文字方塊可指定英數字元密碼的複雜性，並可強制使用者使用下列字元集中的多種不同字元集：小寫英文字母、大寫英文字母、符號及數字。
    
      - **需要英數字元密碼**   此選項決定密碼強度。除了數字之外，您可以強制在密碼中使用字元或符號。
    
      - **停止活動時間 (秒)**   此選項決定行動裝置閒置多久之後，會提示使用者輸入密碼將行動裝置解除鎖定。
    
      - **強制密碼歷程記錄**   選取此核取方塊可強制行動電話禁止使用者重複使用其之前的密碼。您所設定的數字將決定不允許使用者重複使用的過去密碼數。
    
      - **啟用密碼復原**   選取這個核取方塊，可啟用行動裝置的密碼復原。 系統管理員可使用 **Get-ActiveSyncDeviceStatistics** Cmdlet 來查詢使用者的復原密碼。
    
      - **失敗後抹除裝置 (嘗試次數)**   此選項可讓您指定是否要在密碼嘗試失敗多次之後清除電話的記憶體。

  - **裝置加密原則**   您可以為一組使用者強制執行多個行動裝置加密原則。其中包括下列原則：
    
      - **需要加密裝置**   選取這個核取方塊，可要求加密行動裝置。這會將行動裝置的所有資訊加密，以增加安全性。
    
      - **需要儲存卡加密**   選取這個核取方塊，可要求加密行動裝置的卸除式儲存卡。如此會加密行動裝置儲存卡上的所有資訊來增強安全性。

## Windows Phone 7 同步處理

如果您的組織中有 Windows Phone 7 行動裝置，則在設定某些行動裝置信箱原則屬性時，這些裝置會遇到同步處理問題。若要讓 Windows Phone 7 行動電話與 Exchange 信箱同步處理，請將 **AllowNonProvisionableDevices** 屬性設為 True，或只設定下列行動裝置信箱原則屬性：

  - PasswordRequired

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - DeviceWipeThreshold

  - AllowSimplePassword

  - PasswordExpiration

  - PasswordHistory

  - DisableRemovableStorage

  - DisableIrDA

  - DisableDesktopSync

  - BlockRemoteDesktop

  - BlockInternetSharing


---
title: '管理裝置的 iOS Outlook 與 Exchange Server for android （英文）: Exchange 2013 Help'
TOCTitle: 管理裝置的 iOS Outlook 與 Exchange Server for android （英文）
ms:assetid: 16ce7d24-be74-4466-b126-828a67f69b6e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt465748(v=EXCHG.150)
ms:contentKeyID: 70076141
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理裝置的 iOS Outlook 與 Exchange Server for android （英文）

 

_**適用版本：**Exchange Server 2010, Exchange Server 2013_

_**上次修改主題的時間：**2018-04-01_

**摘要：** 本文說明如何 Exchange Active Sync 可協助您管理行動裝置的 iOS Outlook 及 Android 中 Exchange 內部部署組織。

Microsoft 建議用來存取內部部署環境中的 Exchange 信箱的行動裝置管理 Exchange ActiveSync。Exchange ActiveSync 是讓行動電話存取組織的資訊在執行 Microsoft Exchange 伺服器上的 Microsoft Exchange 同步處理通訊協定。

本文著重在特定的 Exchange ActiveSync 功能和執行 Outlook for android （英文） 與 iOS 的行動裝置的案例。使用[Exchange ActiveSync](exchange-activesync-exchange-2013-help.md)中的 Microsoft Exchange 同步處理通訊協定的完整資訊。此外，為[Office 部落格](https://go.microsoft.com/fwlink/p/?linkid=623922)細部密碼強制執行與執行 iOS 的 Outlook 及 Android 裝置搭配使用 Exchange ActiveSync 的其他優點的詳細資訊。

## PIN 鎖定及裝置加密

如果貴組織的 Exchange ActiveSync 原則需要讓使用者可以同步處理電子郵件中的行動裝置上的密碼，Outlook 會強制執行這項原則層級的裝置。這項措施不同 iOS 裝置及 Android 裝置，根據可用 Apple 和 Google 所提供的控制項。

IOS 裝置上 Outlook 進行檢查以確認密碼或 PIN 已正確設定。事件中未設定密碼，Outlook 會提示使用者建立 iOS 設定\] 中的密碼。密碼為安裝程式，直到使用者將無法存取的 iOS Outlook。

8.0 或更新版本的 iOS 上只有執行 iOS 的 outlook。這些裝置時都會隨附內建的加密，Outlook 會使用啟用密碼後要加密 Outlook 儲存在本機上 iOS 裝置的所有資料。因此，PIN iOS 裝置將會加密這必要的 ActiveSync 原則影響。

Android 裝置上 Outlook 會強制執行螢幕鎖定規則。此外，Google 提供控制項可讓 Outlook for android （英文) 至遵守 Exchange 有關密碼長度和複雜性，並允許數目畫面-unlock 之前清除電話的嘗試。如果它未啟用，引導使用者完成此程序的逐步解說，outlook for Android 也將鼓勵儲存加密。

iOS 及 Android 裝置不支援這些密碼安全性設定將不能夠連線至 Exchange 信箱。

## 遠端清除 Exchange activesync

Exchange ActiveSync 可讓系統管理員從遠端清除裝置，例如 if 他們成為洩漏。與 Outlook for iOS android （英文）、 遠端抹除執行 hit highlight Outlook 應用程式本身，並不完整的裝置抹除。

遠端抹除命令要求管理員之後，請清除發生內 Outlook 應用程式的下一個連線至 Exchange 的秒數。Outlook 應用程式將會重設與所有 Outlook 電子郵件、 行事曆、 連絡人及檔案資料將會都移除從裝置，以及從 Outlook 的服務。清除不會影響的任何使用者的個人應用程式與 Outlook 以外的資訊。

遠端抹除命令之後的 iOS Outlook 及 android （英文） 顯示為使用者的行動裝置下單一的行動裝置關聯 Exchange 中，會移除資料，並從執行 Outlook （iPhone、 iPad、 Android） 相關聯的所有裝置刪除同步關係該使用者。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由於背後的 iOS Outlook 及 Android 的雲端架構、 遠端裝置抹除的結果會不報告回至 Exchange。即使抹除成功時，則狀態會顯示為<strong>擱置</strong>。此為已知的問題和開發解決方案。</td>
</tr>
</tbody>
</table>


## 裝置識別碼及存取控制

由於的雲端架構的 iOS Outlook 及 android （英文）、 Outlook 連線顯示為每位使用者的單一的行動裝置識別碼 (ID) Exchange 中。這表示每個使用者的行動裝置存取控制項會套用至與此裝置識別碼相關聯的所有裝置這項實作建立不同的兩個條件從如何傳統 Exchange ActiveSync 裝置存取控制項運作。

  - **封鎖：** 封鎖規則封鎖所有裝置上的 Outlook 和支援的作業系統。您無法封鎖個別裝置或作業系統。

  - **隔離：** 隔離程序的運作方式根據個別使用者，而不是每個裝置上。一旦使用者已從隔離區釋出的裝置，他們可以安裝及設定相同數目的其他裝置為他們想要在 Outlook。因為已從隔離區釋放使用者，任何新的裝置相關聯的使用者不會被隔離。

備妥行動裝置信箱原則時，套用至所有相關裝置。因此，如果您強制執行特定信箱的 PIN 鎖定，連線至該信箱的所有裝置都需要 PIN。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>因為裝置識別碼不由任何<em>實體裝置</em>識別碼，他們可以變更不另行通知。在這種情況下，它會導致非預期的後果時裝置識別碼用於為現有允許' 裝置可能會意外封鎖或隔離由 Exchange 管理使用者的裝置。因此，我們建議系統管理員只能設定行動裝置原則允許/封鎖根據裝置類型或裝置型號的裝置。</td>
</tr>
</tbody>
</table>


## 裝置管理與 Exchange ActiveSync 常見問題集

下列被常見問題密碼、 Pin、 及加密原則執行 iOS 的 Outlook 及 Android 的裝置。

## IOS 上的原生郵件應用程式強制執行密碼長度和複雜性需求的 Exchange ActiveSync 原則。為什麼要選擇不 Outlook？

Outlook 會利用 microsoft 提供的協力廠商應用程式開發人員控制項。我們會繼續為 Apple 可提供更多控制項供開發人員提高這項功能。

## 為什麼要選擇沒有 iOS 的 Outlook 及 Android 強制執行在裝置層級，而不是應用程式層級的 Pin？

之後評估 iOS 及 android （英文） 中可用的功能、 Microsoft 相信裝置層級 PIN 將客戶、 類讀者閱讀和安全性的最佳的體驗。應用程式層級 PIN 表示使用者必須輸入存取電子郵件、 可能取捨兩個不同的 Pin。進一步、 裝置層級 PIN 表示我們可以利用原生裝置加密上 iOS、 TouchID 及 Android 智慧鎖定等功能。遠端抹除仍會實作在應用程式層級，這表示使用者的個人應用程式及資料不會受到影響時清除 Outlook。

## Outlook for Android 的支援裝置加密嗎？

是，Outlook for android （英文) 支援透過 Exchange 行動裝置信箱原則的裝置加密。不過，Android 7.0 之前的可用性和實作此程序而有所不同 Android 作業系統版本和裝置製造商以允許使用者取消加密程序期間。Google Android 7.0 所引進的變更，Outlook for Android 是現在可以強制執行 Android 7.0 裝置上的加密或更新版本。與執行這些作業系統的裝置的使用者將無法取消不在加密程序。

即使 Android 裝置未加密而攻擊者在擁有的裝置，只要裝置 PIN 已啟用，Outlook 資料庫保持無法存取。這是 true 即使有啟用 USB 偵錯及 Android SDK 安裝。如果攻擊者嘗試將根略過來存取此資訊的 pin 碼的裝置，rooting 程序擦去所有裝置儲存區，並移除所有 Outlook 資料。如果裝置是未加密的情事前被竊, 會在使用者為根目錄的攻擊者存取 Outlook 資料庫時會啟用偵錯裝置上的 USB 有可能會與著裝置插入 Android sdk （英文） 的電腦已安裝。


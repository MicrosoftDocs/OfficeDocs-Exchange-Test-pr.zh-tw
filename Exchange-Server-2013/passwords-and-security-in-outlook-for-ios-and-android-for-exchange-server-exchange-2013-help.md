---
title: 'Passwords and Security in Outlook for iOS and Android for Exchange Server: Exchange 2013 Help'
TOCTitle: Passwords and Security in Outlook for iOS and Android for Exchange Server
ms:assetid: e5565beb-7ef3-47c4-8daf-6d8f1d22dceb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt465750(v=EXCHG.150)
ms:contentKeyID: 70076146
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Passwords and Security in Outlook for iOS and Android for Exchange Server

 

_**適用版本：**Exchange Server 2010, Exchange Server 2013_

_**上次修改主題的時間：**2018-04-01_

**摘要：** 本文說明密碼和安全性的 iOS Outlook 及 Android 與 Exchange Server 中運作的方式。

IOS 及 Android 的 Outlook 應用程式執行 Exchange 內部部署環境中的第一次 Outlook 就會產生隨機的 AES 128 機碼。此機碼 」 稱為 「*裝置機碼*並儲存只在使用者的裝置上。

## 建立帳戶和密碼保護

當使用者登入 Exchange 時、 使用者名稱、 密碼和唯一的 AES 128 裝置機碼傳送從使用者的裝置 Outlook 服務透過 TLS 連線，裝置機碼執行階段 compute 記憶體中的保留位置。確認後與 Exchange 伺服器的密碼，Outlook 服務使用的裝置金鑰加密密碼和加密的密碼會儲存在服務中。裝置機碼同時，會清除從記憶體和從未儲存在 Outlook 服務 （索引鍵只會儲存在使用者的裝置）。

下一步\] 當使用者嘗試連線至 Exchange 擷取信箱資料、 裝置機碼是一次傳遞從裝置 Outlook 服務透過 TLS 安全連線，它用來解密 runtime compute 記憶體中的密碼。一旦解密、 password 是從未儲存在服務或寫入至本機存放區磁碟機和裝置機碼一次清除從記憶體。

Outlook 服務已解密的密碼執行階段後，服務可再連線至 Exchange server 同步處理電子郵件、 行事曆及其他信箱資料\]。只要使用者會繼續開啟並定期使用 Outlook、 Outlook cservice 會保持作用的連線到 Exchange 伺服器的記憶體中保留一份使用者已解密的密碼。

## 帳戶閒置時間和清除密碼中從記憶體

後三天份的閒置時間、 Outlook 服務會從記憶體中清除已解密的密碼。已解密的密碼排清、 Outlook 服務無法存取使用者的信箱。加密的密碼保持儲存在 Outlook 服務，但不是再次解密可能沒有裝置機碼，才可從使用者的裝置。

有三種方法的使用者帳戶會變得不在作用中：

  - 會在使用者解除安裝 outlook iOS 及 android （英文）。

  - 背景應用程式重新整理已停用的設定選項，然後強制結束套用至 Outlook。

  - 沒有可用的裝置，防止 Outlook 與 Exchange 同步處理的網際網路連線。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outlook 將不會變成非作用中只是因為使用者無法開啟應用程式的一段時間，例如週末或在休假上。只要背景應用程式重新整理已啟用 （這是 Outlook for iOS 及 Android 的預設值），推入通知和背景同步處理的電子郵件的功能將會視為活動。</td>
</tr>
</tbody>
</table>


**清除加密密碼\] 和 \[訊息從硬碟的快取**

Outlook 服務清除或刪除，非使用中帳戶每週。使用者帳戶會變成非使用中之後，Outlook 服務會清除加密的密碼及的所有使用者的快取的信箱內容停止服務。

**裝置及服務的安全性組合**

每位使用者的唯一裝置機碼從未儲存在 Outlook 服務，和使用者的 Exchange 密碼永遠不會儲存在裝置上。此架構表示順序為惡意的人來存取使用者的密碼，他們就需要未經授權的存取 Outlook 服務及實體存取該使用者的裝置。

來強制執行 PIN 原則與您組織中的裝置上的加密，惡意廠商者也必須通過只是要取得的存取權的裝置金鑰的裝置加密。所有對使用者注意到裝置已洩漏且無法要求裝置的遠端清除之前進行這。

## 密碼安全性常見問題集

下列是常見問題集有關安全性設計及 Outlook 的 iOS 及 Android 的設定。

## 使用者認證儲存在 Outlook 服務如果我封鎖 Outlook 無法存取我的 Exchange 伺服器吗？

如果您已選擇封鎖的 iOS Outlook 及 Android 存取您的內部部署 Exchange 伺服器，Exchange 會被拒絕初始的連線。Outlook 服務將不會儲存使用者認證並呈現在嘗試連線失敗的認證便會立即清除從記憶體。

## 如何唯一裝置機碼和使用者密碼傳輸時會加密 Outlook 服務？

Outlook 應用程式與 Outlook 服務之間的所有通訊都會透過加密的 TLS 連線。IOS 的 Outlook 及 Android 都能夠與 Outlook 服務和其他人則是 nothing 連線。

## 如何從 Outlook 的服務移除使用者的認證和信箱資訊？

有三種方式移除 Outlook 服務的資訊：

  - 做法 1： 啟動遠端抹除針對每一個使用者已用來連線至 Exchange 的應用程式。

  - 選項 2： 已刪除的 iOS Outlook 及 Android 的所有使用者。所有的資料會從 Outlook 服務中移除，大約 3-7 天。

  - 選項 3： 讓使用者從 Outlook 應用程式中移除其帳戶並再刪除其裝置中的應用程式。在應用程式，有使用者移至 \[**設定**\]，然後點選 \[**帳戶設定**\]，然後**選取 \[帳戶\]**，並再點選 \[**刪除的帳戶**。

## 應用程式會在關閉或解除安裝，但仍查看其連線至 「 我的 Exchange server。如何為這種情況？

Outlook 服務解密 runtime compute 記憶體中的使用者密碼並再連線至 Exchange 會使用已解密的密碼。由於 Outlook 服務連線至 Exchange 代表裝置才能擷取及快取信箱資料，它可以繼續的一段簡短時間直到此服務會偵測 Outlook 不再要求的資料。

如果使用者從其裝置解除安裝應用程式但未先使用 \[**刪除帳戶**\] 選項，Outlook 服務會保持在最連線至 Exchange 伺服器之前所述上方 」 帳戶閒置時間及清除的帳戶會成為非使用中密碼從記憶體。 」若要停止此活動，只是從上面的常見問題集、 追蹤選項 1 」 或 「 選項 3 或封鎖[封鎖 Outlook for iOS 及 android （英文）](https://technet.microsoft.com/zh-tw/library/mt759239\(v=exchg.150\))中所述的應用程式。

## 是使用者密碼的 iOS Outlook 及 Android 中比時使用其他 Exchange ActiveSync 用戶端不安全？

\[否\]。EAS 用戶端通常儲存使用者認證在本機使用者的裝置上。這表示竊或洩漏裝置可能會導致惡意的廠商取得的存取權的使用者密碼。具有安全性設計的 iOS Outlook 及 android （英文）、 惡意廠商就需要未經授權的存取 Outlook 雲端服務**和**可以實體存取使用者的裝置。

## 如果使用者嘗試使用 Outlook for iOS 及 Android 刪除其資料從 Outlook 的服務後發生什麼情況？

如果 （例如由停用在裝置上的背景應用程式重新整理或擁有其裝置的連線中斷從網際網路一段時間內） 的使用者帳戶會變成非作用中、 Outlook 應用程式將會重新連線至 Outlook 服務應用程式已啟動，下一次和密碼加密及快取處理程序的電子郵件會重新啟動。這是所有透明給使用者。

## 如何維謢暫時快取的信箱資料的安全時儲存在 Outlook 服務？

您可以閱讀有關我們資料目前如何保護在[Azure 信任中心](https://azure.microsoft.com/support/trust-center/)。如先前所述，我們要從 Azure 移至 Office 365。在[Office 365 信任中心](https://go.microsoft.com/fwlink/p/?linkid=525776)討論這些服務的安全性。


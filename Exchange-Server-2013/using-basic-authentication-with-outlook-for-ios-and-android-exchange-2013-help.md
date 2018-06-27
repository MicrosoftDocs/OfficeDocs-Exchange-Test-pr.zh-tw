---
title: 'Outlook for iOS and Android: Exchange 2013 Help'
TOCTitle: Outlook for iOS and Android
ms:assetid: 3a66817c-30da-4965-a6db-2955b5365b0f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt465744(v=EXCHG.150)
ms:contentKeyID: 70061442
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook for iOS and Android

 

_**適用版本：**Exchange Server 2010, Exchange Server 2013_

_**上次修改主題的時間：**2018-04-02_

**摘要：** 本文包含架構及安全性資訊系統管理員的 iOS Outlook 及 Android in Exchange 2013 內部部署環境。

IOS 及 Android 的 Outlook 應用程式的設計目的在於結合電子郵件、 行事曆、 連絡人及其他檔案，讓使用者在組織中的執行多從其行動裝置。 本文提供架構的概觀及應用程式儲存設計，讓 Exchange 系統管理員可以部署及維護其 Exchange 組織中的 Outlook for iOS 及 android （英文）。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://support.office.com/en-us/article/outlook-for-ios-and-android-help-center-cd84214e-a5ac-4e95-9ea3-e07f78d0cde6">IOS 及 Android 說明中心 Outlook</a>是提供給使用者，包括使用特定裝置上的應用程式與疑難排解資訊的說明。</td>
</tr>
</tbody>
</table>


## 適用於 iOS 和 Android 架構的 Outlook

Outlook iOS 及 android （英文） 所組成的行動裝置及後端，又稱為*Outlook 服務*進行安全且擴充度佳的雲端服務安裝的前端應用程式。處理 Outlook 服務中的資訊可讓進階的功能和增強的 Outlook 經驗，以及改善的效能和穩定性的功能。此架構依賴的大量處理、 最小化從使用者的裝置所需的資源的 \[Outlook\] 服務。

Outlook 服務為使用者提供的範例包括：

  - 具有焦點的收件匣的分類。

  - 按一下取消郵寄清單的功能。

  - 改善搜尋的速度和效率。

  - 轉寄並不需要先下載這些行動裝置傳送的大型檔案的能力。

## 資料快取

為了改善效能電子郵件、 行事曆及檔案資料從每個使用者信箱的子集快取中的 Outlook 服務。Microsoft Azure上目前執行此服務。我們將 Outlook 服務移至 Office 365 中，並已完成推出的移動計劃。

Outlook 服務中的資訊目前快取在美國或在歐洲、 視連線的用戶端的 IP 位址。當我們將 Outlook 服務移至 Office 365 時，我們會對齊至 Office 365 信任中心的原則與地區的資料中心策略。在 Office 365 客戶的國家或地區、 客戶的系統管理員輸入服務的初始安裝期間，會決定該客戶資料的主要儲存區位置。如需詳細資訊，請參閱[Office 365 信任中心](https://go.microsoft.com/fwlink/p/?linkid=525776)。

## 資料快取常見問題集

下列被常見問題的 iOS Outlook 及 android （英文） 中的資料存放區。

## 使用者的信箱資料中有多少快取中的 Outlook 服務？

大約 1 個月的電子郵件、 行事曆和連絡人的資料。快取的程序由帳戶、 其他因素，之間的信箱在指定的資料夾 （例如預設收件匣\] 資料夾相較於由使用者所建立的資料夾），信箱內的相對重要性大小演算法和頻率使用者存取指定的資料夾。

Outlook 服務儲存附件資料，如下所示： 當使用者要求在 Outlook 中開啟的電子郵件附件時、 服務擷取附件從 Exchange 伺服器，並可暫時儲存它。在那個時候附件傳送至使用者的行動裝置上的應用程式。資料早於 1 個月會定期排清不在服務\]，指向附件只會提供 Exchange 伺服器上。

## 如何從 Outlook 的服務中移除我資訊？

您必須從 Outlook 的服務移除您資訊的三個選項。

  - 做法 1： 啟動遠端抹除針對每一個使用者已使用 iOS Outlook 相關應用程式及 Android 連線至 Office 365 或 Exchange。

  - 選項 2： 已刪除的 Outlook 應用程式的所有使用者。大約 3-7 天內將會移除所有資料。

  - 選項 3： 讓每個使用者的 Outlook 應用程式中移除其帳戶及再刪除與其行動裝置中的應用程式。若要移除帳戶，具備使用者遵循下列步驟：
    
    1.  在 \[Outlook 應用程式，在 \[**設定**\] 中點選 \[**帳戶設定**\]。
    
    2.  點選 \[**選取帳戶**，，然後點選 \[以選取帳戶\] 的 \[**移除帳戶**。
    
    3.  點選 \[**裝置與遠端資料**。

## 如何維謢暫時快取的信箱資料的安全時儲存在 Outlook 服務？

您可以閱讀有關我們資料目前如何保護在[Azure 信任中心](https://azure.microsoft.com/support/trust-center/)。如先前所述，我們要從 Azure 移至 Office 365。在[Office 365 信任中心](https://go.microsoft.com/fwlink/p/?linkid=525776)討論這些服務的安全性。


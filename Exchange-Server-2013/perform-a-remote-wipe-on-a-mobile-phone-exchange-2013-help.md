---
title: '在行動電話上執行遠端清除: Exchange Online Help'
TOCTitle: 在行動電話上執行遠端清除
ms:assetid: 67ba838e-031d-4a98-b277-170683b6f520
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998614(v=EXCHG.150)
ms:contentKeyID: 52062341
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在行動電話上執行遠端清除

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2013-02-06_

您的使用者執行公司的機密資訊在其口袋每天。如果其中一個失去與其行動電話，您的資料可以最後中作業的另一個人。如果您的使用者的其中一個失去與其行動電話，您可以使用 Exchange 系統管理中心 (EAC) 或 Exchange 管理命令介面來清除其初始狀態的所有公司電話和使用者資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題也提供如何使用MicrosoftOutlook Web App電話上執行遠端清除的指示。使用者必須要登入Outlook Web App執行遠端清除。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「行動裝置」項目。

  - 此程序會清除行動電話上的所有資料，包括已安裝的應用程式、相片和個人資訊。

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

## 使用 EAC 清除使用者的電話

您可以使用 EAC 來清除使用者的電話，或取消尚未完成的遠端清除。

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  選取使用者，在 **\[行動裝置\]** 下，選擇 **\[檢視詳細資料\]**。

3.  在 **\[行動裝置詳細資料\]** 頁面上，選取遺失的行動裝置，然後選取 **\[清除資料\]**。

4.  選取 **\[儲存\]**。

## 使用命令介面清除使用者的電話

您可以在命令介面中使用 **Clear-MobileDevice** 指令程式來清除使用者的電話。

下列命令會清除名為 WM\_TonySmith 的裝置，並將確認訊息傳送到 admin@contoso.com。

    Clear-MobileDevice -Identity WM_TonySmith -NotificationEmailAddresses "admin@contoso.com"

## 使用 Outlook Web App 清除使用者的電話

使用者可以利用 Outlook Web App 來清除自己的電話。

1.  在 Outlook Web App 中，選取 **\[設定\]\> \[電話\] \> \[行動裝置\]**。

2.  選取行動電話。

3.  按一下或點選 **\[清除裝置\]** 圖示。

## 如何才能了解這是否正常運作？

有幾個方法可驗證遠端清除已完成。

  - 執行**Clear-MobileDevice** cmdlet 搭配*–NotificationEmailAddresses*參數設定。完成遠端抹除之後就會提供的電子郵件地址傳送的訊息。

  - 在 EAC 中，檢查行動裝置的狀態。狀態會從**擦去擱置中**變更為**擦去成功**。

  - 在Outlook Web App、 核取狀態的行動裝置。狀態會從**擦去擱置中**變更為**擦去成功**。


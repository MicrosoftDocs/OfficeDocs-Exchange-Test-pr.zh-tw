---
title: '設定行動電話存取電子郵件: Exchange Online Help'
TOCTitle: 設定行動電話存取電子郵件
ms:assetid: 8d6e2cea-265a-43d9-a074-076f35658436
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123704(v=EXCHG.150)
ms:contentKeyID: 52062367
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定行動電話存取電子郵件

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-12_

您可以設定行動電話，例如Windows電話，使用MicrosoftExchange ActiveSync。您應該在組織中的每個行動電話上執行此程序。

## 必要條件

  - 您已檢閱所要設定之行動電話的製造商文件。

  - 您的組織中已啟用 Exchange ActiveSync。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>針對特定裝置的資訊設定 Microsoft Exchange 式電話或平板電腦上的電子郵件請參閱<a href="https://support.office.com/en-us/article/set-up-a-mobile-device-using-office-365-for-business-7dabb6cb-0046-40b6-81fe-767e0b1f014f">設定行動裝置使用 Office 365 企業版</a>。</td>
</tr>
</tbody>
</table>


## 設定行動電話以使用 Exchange ActiveSync

大部分的行動電話與裝置是能夠設定要使用 Exchange ActiveSync 行動裝置的電子郵件用戶端使用自動探索。在大部分的行動電話上設定電子郵件帳戶，您將需要兩項資訊。

  - 使用者的電子郵件地址

  - 使用者的密碼

如果行動電話無法連絡 Exchange 伺服器自動透過自動探索，您需要手動設定行動電話。手動安裝需要使用者的電子郵件地址和密碼，以及 Exchange ActiveSync 伺服器名稱。在大多數的組織中的 Exchange ActiveSync 伺服器名稱是沒有 /owa，例如 mail.contoso.com 的 Outlook Web App 伺服器名稱相同。

## Windows Phone 同步處理

如果您正在設定同步處理與使用Exchange ActiveSyncExchange信箱Windows電話行動電話、 支援的行動裝置信箱原則設定的子集。[Windows Phone 和裝置支援行動裝置信箱原則](supported-mobile-device-mailbox-policies-for-windows-phones-and-devices-exchange-2013-help.md)詳細說明這些原則設定。

如果您設定的行動裝置信箱原則設定不支援您所使用的 Windows Phone 版本，還必須將 **AllowNonProvisionableDevices** 原則設定設定為 true，或為 Windows Phone 行動電話建立個別的行動裝置信箱原則。


---
title: 'Exchange ActiveSync 中的資訊版權管理: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync 中的資訊版權管理
ms:assetid: ebf04460-4d61-4b00-86b9-85ec1dbbd6a1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff657743(v=EXCHG.150)
ms:contentKeyID: 50474530
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange ActiveSync 中的資訊版權管理

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

資訊工作者通常會使用電子郵件交換敏感資訊。為了安全這項資訊、 組織可以使用資訊版權管理 (IRM) 套用至訊息內容的持續性的保護。行動裝置會逐漸要用來存取電子郵件，因為很重要的行動裝置使用者可以建立和取用受 IRM 保護的內容。

**目錄**

Mobile IRM protection in Exchange 2013

Requirements

Security

Enabling IRM in Exchange ActiveSync

要尋找與 IRM 相關的管理工作嗎？ 請參閱 [資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## Exchange 2013 中的 Mobile IRM 保護

中Exchange 2013、 IRM in Microsoft Exchange ActiveSync允許讓使用者存取任何支援的Exchange ActiveSync裝置上豐富的 IRM 功能而不需要設定 AD RMS 權限或裝置連線到電腦並啟用 irm。此外，不需要執行Windows行動裝置。Exchange ActiveSync是由 Microsoft 授權給行動裝置製造商、 原始設備製造商 (Oem) 及其他人。目前Exchange ActiveSync使用人均的清單，依序展開 \[ [Microsoft 技術授權](https://go.microsoft.com/fwlink/p/?linkid=198562)頁面的 「 Exchange ActiveSync 通訊協定 」 區段。

行動裝置使用者在 Exchange ActiveSync 中使用 IRM 時可以：

  - 建立受 IRM 保護的郵件。

  - 讀取受 IRM 保護的郵件。

  - 回覆及轉寄受 IRM 保護的郵件。

回到頁首

## 需求

適用下列需求：

  - 貴組織中的用戶端存取伺服器必須執行Exchange 2010 SP1 或更新版本。

  - AD RMS 伺服器必須部署在您的組織中。

  - 必須啟用內部郵件的 IRM。此為所有的 IRM 功能中Exchange 2010的先決條件。如需詳細資訊，請參閱[啟用或停用內部郵件的 IRM](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)。

  - 必須在Exchange ActiveSync信箱原則啟用 IRM。您可以啟用或停用 IRM 的不同使用者使用不同Exchange ActiveSync信箱原則。

  - 支援Exchange ActiveSync通訊協定版本 14.1，包括Windows電話裝置可支援 IRM Exchange ActiveSync中。裝置的行動裝置的電子郵件應用程式必須支援Exchange ActiveSync版本 14.1 中所定義的 RightsManagementInformation 標籤。

回到頁首

## 安全性

當您在Exchange ActiveSync中啟用 IRM 時，用戶端存取伺服器會再提供支援的行動裝置存取郵件解密受 IRM 保護的郵件。在 \[同步處理時受 IRM 保護之訊息位於行動裝置上未加密的格式。IRM 保護會強制執行的行動裝置上的 IRM 能夠電子郵件用戶端應用程式。

IRM 在Exchange ActiveSync不解密受 IRM 保護之用戶端存取伺服器上的附件。存取受 IRM 保護的檔案會用來建立或檢視檔案的應用程式來強制執行。例如， Windows電話，在 IRM 保護 Microsoft Office檔案是施行的強制[Microsoft Office Mobile](https://go.microsoft.com/fwlink/p/?linkid=205121)。若要存取受 IRM 保護之Office檔案，使用者必須裝置連線到電腦並啟用Office行動電話與 RMS 伺服器。

在 Exchange ActiveSync 中啟用 IRM 時，我們建議您使用下表所列出的 Exchange ActiveSync 原則設定以協助您保護行動裝置。

### Exchange ActiveSync 原則設定

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>使用新增 Exchange ActiveSync 信箱原則精靈進行設定</th>
<th>使用 New-ActiveSyncMailboxPolicy 指令程式進行設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>需要使用者輸入密碼以存取行動裝置上的資訊。</p></td>
<td><p>選取 [需要密碼] 核取方塊。</p></td>
<td><p>將 <em>DevicePasswordEnabled</em> 參數設為 <code>$true</code>。</p></td>
</tr>
<tr class="even">
<td><p>啟用行動裝置的加密。</p></td>
<td><p>選取 [需要密碼] 核取方塊，然後選取 [需要加密裝置] 核取方塊。</p></td>
<td><p>將 <em>RequireDeviceEncryption</em> 參數設為 <code>$true</code>。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您將 <em>RequireDeviceEncryption</em> 參數設為 <code>$true</code> 時，不支援裝置加密的行動裝置將無法連線。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p>不允許非可預備行動裝置與 Exchange 伺服器同步。</p></td>
<td><p>清除 [允許非可預備行動裝置] 核取方塊。</p></td>
<td><p>將 <em>AllowNonProvisionableDevices</em> 參數設為 <code>$false</code>。</p></td>
</tr>
</tbody>
</table>


若要深入瞭解，請參閱[行動裝置信箱原則](mobile-device-mailbox-policies-exchange-2013-help.md)。

回到頁首

## 在 Exchange ActiveSync 中啟用 IRM

若要在 Exchange ActiveSync 中啟用 IRM，請執行下列工作：

1.  將同盟信箱 （ Exchange 2013及Exchange 2010安裝程式所建立的系統信箱） 新增至 AD RMS 中超級使用者群組。這可讓Exchange 2013和Exchange 2010伺服器存取受 IRM 保護的郵件。如需詳細資訊，請參閱[至 AD RMS 超級使用者群組新增同盟信箱](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

2.  啟用用戶端存取伺服器上的 IRM Exchange管理命令介面中使用[Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))指令程式。這讓 IRM Exchange ActiveSync與 IRM 貴組織的 Microsoft OfficeOutlook Web App中。如需詳細資訊，請參閱[啟用或停用用戶端存取伺服器上的資訊版權管理](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md)。

回到頁首


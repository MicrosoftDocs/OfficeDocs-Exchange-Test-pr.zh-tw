---
title: '建立或修改行動裝置信箱原則: Exchange 2013 Help'
TOCTitle: 建立或修改行動裝置信箱原則
ms:assetid: b4a37a81-25e3-40ff-a18a-a62ae4493635
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124315(v=EXCHG.150)
ms:contentKeyID: 50474052
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立或修改行動裝置信箱原則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-16_

行動裝置信箱原則可讓您將一組通用的安全性與行動裝置設定套用至使用者群組。您可以建立多個行動裝置信箱原則。在組織中的每個收件者必須指派給他們的行動裝置信箱原則。當您安裝 Microsoft Exchange Server 2013時，會建立預設的行動裝置信箱原則和新的使用者會自動指派至此原則。若要指派特定使用者的行動裝置信箱原則，請參閱[新增或移除使用者從行動裝置信箱原則](add-or-remove-users-from-a-mobile-mailbox-policy-exchange-2013-help.md)。

如需有關行動裝置信箱原則的其他資訊，請參閱[行動裝置信箱原則](mobile-device-mailbox-policies-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱主題中的「行動裝置信箱原則」[用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)項目。

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

## 建立新的行動裝置信箱原則

您可以使用 EAC 或命令介面建立新的行動裝置信箱原則。

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱主題中的「行動裝置信箱原則」[用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)項目。

## 使用 EAC 建立新的行動裝置信箱原則

您可以使用 EAC 建立新的行動裝置信箱原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您只能在 EAC 中設定行動裝置信箱原則設定的子集。若要設定的所有行動裝置信箱原則設定，您必須使用命令介面。</td>
</tr>
</tbody>
</table>


1.  在 EAC 中，按一下 \[行動電話\] \> \[行動裝置信箱原則\]，然後按一下 \[新增\]。

2.  使用各種不同的核取方塊和下拉式清單設定行動裝置信箱原則的設定。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>選取 [<strong>這是預設原則</strong>將新的行動裝置信箱原則設定預設行動裝置信箱原則。您的行動裝置信箱原則的預設原則之後，請所有新使用者會指派此原則會自動建立的時。</td>
    </tr>
    </tbody>
    </table>


3.  按一下 \[儲存\]。

## 使用命令介面建立新的行動裝置信箱原則

您可以使用 New-MobileDeviceMailboxPolicy Cmdlet 建立新的行動裝置信箱原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有兩個指令程式可以用來建立新的行動裝置信箱原則。<strong>New-ActiveSyncMailboxPolicy</strong>指令程式和<strong>New-MobileDeviceMailboxPolicy</strong> cmdlet 執行相同的工作。在 Microsoft Exchange Server 的未來版本，將會移除<strong>New-ActiveSyncMailboxPolicy</strong>指令程式。我們建議您更新您的指令碼和使用<strong>New-MobileDeviceMailboxPolicy</strong>指令程式的程序。</td>
</tr>
</tbody>
</table>


1.  在命令介面中，執行下列命令。
    
        New-MobileDeviceMailboxPolicy -Name:"Management" -AllowBluetooth:$true -AllowBrowser:$true -AllowCamera:$true -AllowPOPIMAPEmail:$false -PasswordEnabled:$true -AlphanumericPasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:10 -AllowWiFi:$true -AllowStorageCard:$true -AllowPOPIMAPEmail:$false

## 如何才能了解這是否正常運作？

若要確認是否已成功建立行動裝置信箱原則，請使用下列其中一個選項：

1.  在 EAC 中，按一下 \[行動電話\] \> \[行動裝置信箱原則\]，並確認您的新原則是否顯示在 \[清單\] 檢視中。

2.  在命令介面中，執行下列命令。
    
        Get-MobileDeviceMailboxPolicy -Identity <PolicyName> 

## 編輯現有的行動裝置信箱原則

如果您要編輯行動裝置信箱原則，可以使用 EAC 或命令介面。

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱主題中的「行動裝置信箱原則」[用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)項目。

## 使用 EAC 編輯行動裝置信箱原則

您可以使用 EAC 編輯行動裝置信箱原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您只可以編輯在 EAC 中的行動裝置信箱原則設定的子集。若要編輯所有的行動裝置信箱原則設定，您需要使用命令介面。</td>
</tr>
</tbody>
</table>


1.  在 EAC 中，按一下 \[行動電話\] \> \[行動裝置信箱原則\]。

2.  從 \[清單\] 檢視中選取原則，然後按一下 \[編輯\] 按鈕。

3.  使用 \[一般\] 和 \[安全性\] 索引標籤編輯行動裝置信箱原則設定。

4.  按一下 \[儲存\] 以更新原則。

## 使用命令介面編輯行動裝置信箱原則設定

您可以使用命令介面編輯行動裝置信箱原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有兩個指令程式可以用來編輯行動裝置信箱原則。Set-ActiveSyncMailboxPolicy指令程式和Set-MobileDeviceMailboxPolicy cmdlet 執行相同的工作。在 Microsoft Exchange Server 的未來版本，將會移除<strong>Set-ActiveSyncMailboxPolicy</strong>指令程式。我們建議您更新您的指令碼和使用<strong>Set-MobileDeviceMailboxPolicy</strong>指令程式的程序。</td>
</tr>
</tbody>
</table>


1.  在命令介面中，執行下列命令。
    
        Set-MobileDeviceMailboxPolicy -Identity:Default -DevicePasswordEnabled:$true -AlphanumericDevicePasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:ThreeDays -AllowWiFi:$false -AllowStorageCard:$true -AllowPOPIMAPEmail:$false -IsDefault:$true -AllowTextMessaging:$true -Confirm:$true

## 如何才能了解這是否正常運作？

若要確認是否已成功編輯行動裝置信箱原則，請執行下列其中一個動作：

1.  在 EAC 中，按一下 \[**行動裝置**\> \[**行動裝置信箱原則**\]，然後選擇 \[特定的原則。在 \[詳細資料\] 窗格中，您會看到數列出的原則設定。

2.  在命令介面中，執行下列命令。
    
        Get-MobileDeviceMailboxPolicy -Identity <PolicyName>


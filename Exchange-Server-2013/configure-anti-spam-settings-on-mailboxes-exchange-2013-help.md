---
title: '在信箱上設定反垃圾郵件設定: Exchange 2013 Help'
TOCTitle: 在信箱上設定反垃圾郵件設定
ms:assetid: 868d7fd8-e817-46ba-9b67-edf2f50b9494
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123559(v=EXCHG.150)
ms:contentKeyID: 50473626
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在信箱上設定反垃圾郵件設定

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-11-17_

您可以在不同的套用至 Exchange 組織中信箱的其餘部分的反垃圾郵件設定的個別信箱上設定特定的反垃圾郵件設定。當您在信箱上設定反垃圾郵件設定時，該設定會覆寫對應全組織內容篩選或組織設定反垃圾郵件設定。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 2016 年 11 月 1，Microsoft 停止產生 Exchange 和 Outlook 中 SmartScreen 篩選器的垃圾郵件定義更新。現有的 SmartScreen 垃圾郵件定義將會保留，但其效果可能會隨著時間降低。如需詳細資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=835894">Outlook 和 Exchange 中 SmartScreen 的取代支援</a>。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 每項程序的預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [反垃圾郵件和反惡意程式的權限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主題中的「反垃圾郵件功能」條目，和[收件者權限](recipients-permissions-exchange-2013-help.md)主題中「反垃圾郵件」條目。

  - 預設在 Mailbox Server 的 Transport 服務中未啟用反垃圾郵件功能。通常只有在您的 Exchange 組織接受內送郵件之前未進行任何事前的反垃圾郵件篩選的情況下，您才會在 Mailbox Server 上啟用反垃圾郵件功能。如需詳細資訊，請參閱[啟用信箱伺服器上的反垃圾郵件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - 您只能使用命令介面來執行此程序。

  - 垃圾電子郵件資料夾 SCL 閾值的行為不同 SCL 刪除、 拒絕和隔離的值。如需詳細資訊，請參閱[垃圾郵件信賴等級閾值](spam-confidence-level-threshold-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用命令介面設定單一信箱的反垃圾郵件功能

若要設定單一信箱的反垃圾郵件設定，請使用下列語法。

    Set-Mailbox <MailboxIdentity> -AntispamBypassEnabled <$true | $false> -RequireSenderAuthenticationEnabled <$true | $false> -SCLDeleteEnabled <$true | $false | $null> -SCLDeleteThreshold <0-9 | $null> -SCLJunkEnabled <$true | $false | $null > -SCLJunkThreshold <0-9 | $null> -SCLQuarantineEnabled <$true | $false | $null > -SCLQuarantineThreshold <0-9 | $null> -SCLRejectEnabled <$true | $false | $null > -SCLRejectThreshold <0-9 | $null>

此範例提供如何設定一位名叫 Jeff Phillips 的信箱使用者略過所有反垃圾郵件篩選器的說明，以及如何將符合或超出 5 封垃圾郵件資料夾 SLC 閾值的郵件傳遞到他的 Microsoft Outlook 垃圾郵件資料匣中。

    Set-Mailbox "Jeff Phillips" -AntispamBypassEnabled $true -SCLJunkEnabled $true -SCLJunkThreshold 4

## 如何才能了解這是否正常運作？

若要確認您是否已成功設定單一信箱的反垃圾郵件功能，請執行下列動作：

1.  執行下列命令：
    
        Get-Mailbox <MailboxIdentity> | Format-List SCL*,Bypass*,*SenderAuth*

2.  請確認顯示的值是您所設定的值。

## 使用命令介面設定多個信箱的反垃圾郵件功能

若要設定多個信箱的所有反垃圾郵件設定，請使用下列語法。

    Get-Mailbox [<Filter>]| Set-Mailbox <Anti-Spam Settings>

此範例會將 Contoso.com 網域中使用者容器內所有信箱的 SCL 隔離閾值啟用為 7。

    Get-Mailbox -OrganizationalUnit Contoso.com/Users | Set-Mailbox -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7

## 如何才能了解這是否正常運作？

若要確認您是否已成功設定多個信箱的反垃圾郵件功能，請執行下列動作：

1.  執行下列命令：
    
        Get-Mailbox [<Filter>] | Format-List Name,SCL*,*SenderAuth*

2.  請確認顯示的值是您所設定的值。

## 在您的組織中使用命令介面設定所有信箱的垃圾郵件閾值

執行下列命令：

    Set-OrganizationConfig -SCLJunkThreshold <Integer>

此範例會將組織的垃圾郵件閾值設定為 5。

    Set-OrganizationConfig -SCLJunkThreshold 5

## 如何才能了解這是否正常運作？

若要確認您是否已成功為組織中所有信箱設定垃圾郵件閾值，請執行下列動作：

1.  執行下列命令：
    
        Get-OrganizationConfig | Format-List SCLJunkThreshold

2.  請確認顯示的值是您所設定的值。


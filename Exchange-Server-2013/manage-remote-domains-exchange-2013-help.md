---
title: '管理遠端網域: Exchange 2013 Help'
TOCTitle: 管理遠端網域
ms:assetid: 41a86907-bd9e-40d0-94d3-6deb95a0bffa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997639(v=EXCHG.150)
ms:contentKeyID: 52062285
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewRemoteDomainWizardForm.NewRemoteDomainWizardPage
ms.translationtype: MT
---

# 管理遠端網域

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-13_

遠端網域都是可以在 Microsoft Exchange 組織外部的 SMTP 網域。您可以建立遠端網域項目以定義您的 Exchange 組織與特定的外部網域之間傳送的郵件設定。特定的外部網域的遠端網域項目中的設定會覆寫通常是套用至所有外部收件者的預設值遠端網域中的設定。遠端網域設定為 Exchange 組織的 global。

如果您移除遠端網域項目、 訊息傳輸設定不再套用到傳送至遠端網域的郵件。移除遠端網域項目不會停用遠端網域的郵件流程。移除遠端網域項目後，預設值遠端網域的組態設定套用至新的訊息傳送至該網域。您無法移除預設遠端網域。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「遠端網域」項目。

  - 您只能使用命令介面來執行此程序。

  - 您無法建立遠端網域的位址空間設定為在組織中公認的網域。例如，如果您的組織接受郵件 fabrikam.com，您無法建立 fabrikam.com 的遠端網域。

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

## 使用命令介面來建立遠端網域

若要建立新的遠端網域項目，請使用下列語法。

    New-RemoteDomain -Name <Descriptive Name> -DomainName <SMTP address space>

此範例能針對傳送給 contoso.com 網域的郵件建立遠端網域項目。

    New-RemoteDomain -Name Contoso -DomainName contoso.com

此範例能針對傳送給 fabrikam.com 網域和所有子網域的郵件建立遠端網域項目。

    New-RemoteDomain -Name Fabrikam -DomainName *.fabrikam.com

## 如何才能了解這是否正常運作？

若要確認您是否已成功建立遠端網域，請執行下列動作：

1.  執行 **Get-RemoteDomain** 命令並確認遠端網域已列出。

2.  執行命令`Get-RemoteDomain <Remote Domain Name> | Format-List`確認新的遠端網域設定。將測試郵件傳送至新的遠端網域項目中所指定的地址空間中的收件者，並確認訊息設定符合新的遠端網域項目所指定。

## 使用命令介面來設定遠端網域

您在遠端網域項目使用**Set-RemoteDomain**指令程式設定的設定。有許多不同的與自動回覆、 郵件格式和編碼方式，與其他郵件設定。如需詳細資訊，請參閱[Set-RemoteDomain](https://technet.microsoft.com/zh-tw/library/aa997857\(v=exchg.150\))。

若要針對特定案例設定遠端網域，請參閱以下主題：

  - [設定遠端網域外出回覆](configure-remote-domain-out-of-office-replies-exchange-2013-help.md)

  - [設定遠端網域的自動回覆](configure-remote-domain-automatic-replies-exchange-2013-help.md)

  - [設定遠端網域郵件報告](configure-remote-domain-message-reporting-exchange-2013-help.md)

## 使用命令介面來移除遠端網域

若要移除遠端網域項目，請使用下列語法。

    Remove-RemoteDomain <RemoteDomainName>

此範例會移除名為 Contoso 的遠端網域項目。

    Remove-RemoteDomain Contoso

## 如何才能了解這是否正常運作？

若要確認您是否已成功移除遠端網域，請執行下列動作：

1.  執行 **Get-RemoteDomain** 命令並確認遠端網域未列出。

2.  執行命令`Get-RemoteDomain Default | Format-List`確認預設遠端網域設定。將測試郵件傳送至已移除的遠端網域中所指定的地址空間中的收件者，並確認訊息設定符合所指定的預設值遠端網域。


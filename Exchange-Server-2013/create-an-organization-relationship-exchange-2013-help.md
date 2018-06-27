---
title: '建立組織關聯性: Exchange 2013 Help'
TOCTitle: 建立組織關聯性
ms:assetid: 5ea61b96-c8ca-44fc-b8b5-ca4341af36a6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657451(v=EXCHG.150)
ms:contentKeyID: 50473293
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立組織關聯性

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

設定與外部商業夥伴共用行事曆資訊的組織關聯性。您可以設定兩個同盟的Exchange 2013組織之間或同盟的Exchange 2013組織和同盟的Exchange 2010組織之間的組織關係。您也可以在內部部署 Exchange 組織與 Office 365 組織之間設定組織關聯性。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建立組織關係是建立 Exchange 組織中同盟共用的數個步驟之一，且需要內部部署 Exchange 組織的同盟信任組態。</td>
</tr>
</tbody>
</table>


若要深入了解同盟共用，請參閱[共用](sharing-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「 行事曆與共用權限？[收件者權限](recipients-permissions-exchange-2013-help.md)主題中的一節。

  - 您必須為內部部署 Exchange 組織設定作用中同盟信任。如需詳細資訊，請參閱[設定同盟信任](configure-a-federation-trust-exchange-2013-help.md)。

  - 您想要在組織關係中設定外部組織也必須與Azure AD驗證系統建立同盟信任。您要設定組織關聯性時使用的外部 Exchange 組織的主要同盟的網域。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 使用 EAC 建立組織關係

1.  在內部部署組織中的 Exchange 2013 伺服器上，瀏覽至 \[組織\] \> \[共用\]。

2.  在 \[組織共用\] 下，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 \[新增組織關係\] 的 \[關係名稱\] 方塊中，輸入組織關係的易記名稱。

4.  在 \[要共用的網域\] 方塊中，輸入您要對其顯示行事曆的 Office 365 或 Exchange 內部部署組織的同盟網域或同盟子網域。如果您需要為外部組織輸入多個網域，請以逗號分隔網域。例如，**contoso.com, service.contoso.com**。

5.  選取 \[啟用行事曆空閒/忙碌資訊共用\] 核取方塊，以開啟與您所列之網域的行事曆共用。設定行事曆空閒/忙碌資訊的共用層級，並設定哪些使用者可共用行事曆空閒/忙碌資訊。
    
    若要設定空閒/忙碌存取層級，請選擇下列其中一項：
    
      - **僅行事曆空閒/忙碌的時間資訊**
    
      - **行事曆空閒/忙碌的時間、主題與地點資訊**
    
    若要設定哪些使用者將共用行事曆空閒/忙碌資訊，請選取下列其中一項：
    
      - **組織中的所有人**
    
      - **指定的安全性群組**
        
        若要指定安全性群組，請按一下 \[瀏覽\]。

6.  按一下 \[儲存\] 以建立組織關係。

## 使用命令介面建立組織關係

本範例會使用下列條件，建立與 Contoso, Ltd 的組織關係：

  - 啟用與 contoso.com、northamerica.contoso.com 和 europe.contoso.com 的組織關係。

  - 已啟用空閒/忙碌資訊存取。

  - 要求的組織會收到目標組織的空閒/忙碌時間、主旨和位置資訊。

<!-- end list -->

    New-OrganizationRelationship -Name "Contoso" -DomainNames "contoso.com","northamerica.contoso.com","europe.contoso.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel LimitedDetails

本範例會嘗試使用 **Get-FederationInformation** 指令程式所提供的網域名稱，自動探索來自外部 Exchange 組織 Contoso.com 的組態資訊。如果要使用這個方法建立您組織的關係，首先您必須確認已經以 **Set-FederatedOrganizationIdentifier** 指令程式建立組織識別碼。

    Get-FederationInformation -DomainName Contoso.com | New-OrganizationRelationship -Name "Contoso" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -LimitedDetails

如需詳細的語法及參數資訊，請參閱 [Get-FederationInformation](https://technet.microsoft.com/zh-tw/library/dd351221\(v=exchg.150\)) 與 [New-OrganizationRelationship](https://technet.microsoft.com/zh-tw/library/ee332357\(v=exchg.150\))。

本範例會建立與 Fourth Coffee 的組織關係。在這個範例中，將會提供與外部 Exchange 組織的連線設定。適用下列條件：

  - 組織關係建立於 Fourth Coffee 的同盟網域 fourthcoffee.com。

  - Exchange Web 服務應用程式 URL 是 mail.fourthcoffee.com。

  - 自動探索 URL 是 https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity。

  - 已啟用空閒/忙碌資訊存取。

  - 要求組織只會收到空閒/忙碌資訊的時間。

<!-- end list -->

    New-OrganizationRelationship -Name "Fourth Coffee" -DomainNames "fourthcoffee.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -AvailabilityOnly -TargetAutodiscoverEpr "https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity" -TargetApplicationUri "mail.fourthcoffee.com"

如需詳細的語法及參數資訊，請參閱 [New-OrganizationRelationship](https://technet.microsoft.com/zh-tw/library/ee332357\(v=exchg.150\))。

## 如何知道這是否正常運作？

成功完成 \[新組織關係\] 精靈，首先表明組織關係的建立如預期般運作。

若要進一步驗證是否已成功建立組織關係，請執行下列命令介面命令來驗證組織關係資訊：

    Get-OrganizationRelationship | format-list

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


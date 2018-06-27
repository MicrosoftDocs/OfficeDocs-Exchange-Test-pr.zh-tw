---
title: '在 Active Directory 中設定 Exchange 郵件路由設定: Exchange 2013 Help'
TOCTitle: 在 Active Directory 中設定 Exchange 郵件路由設定
ms:assetid: d01f8545-c201-4a96-be39-ed4c7008afcf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ674705(v=EXCHG.150)
ms:contentKeyID: 50474260
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Active Directory 中設定 Exchange 郵件路由設定

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

根據預設 Microsoft Exchange Server 2013參考來協助您決定最低成本路由路徑的 Active Directory 中的 IP 站台連結物件。不過，如果您決定 Active Directory IP 站台連結成本和流量流程模式不最佳的路由 Exchange 中的郵件，您可以設定只能由 Exchange 用來協助最佳化郵件流程的 Active Directory 中。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「Active Directory 站台及站台連結管理」項目。

  - 您只能使用命令介面來執行此程序。

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

## 使用命令介面在 Active Directory IP 站台連結上設定 Exchange 特定成本

決定您要設定 Exchange 成本的 Active Directory IP 站台連結的名稱。較低的成本值表示更慣用的路由。您可以檢查路由表格記錄檔的內容及檢視**ADTopologyPath ID** \] 區段中檢視兩個 Active Directory 站台之間的計算結果的最低成本路由路徑的詳細資料。

若要設定 Active Directory 站台連結的 Exchange 特定成本，請執行下列命令：

``` 
 Set-AdSiteLink <ADSiteLinkIdentity> -ExchangeCost <Integer | $null>
```

此範例會對於名稱為 IPSiteLinkAB 的 IP 站台連結設定 Exchange 特定成本 10。

    Set-AdSiteLink IPSiteLinkAB -ExchangeCost 10

此範例會從名稱為 IPSiteLinkAB 的 IP 站台連結清除 Exchange 成本。

    Set-AdSiteLink IPSiteLinkAB -ExchangeCost $null

## 如何才能了解這是否正常運作？

若要確認您是否對於 Active Directory 站台連結成功設定 Exchange 成本，請執行下列操作：

1.  執行下列命令：
    
        Get-AdSiteLink | Format-List Name,ExchangeCost

2.  確認已針對 Active Directory 站台連結設定 Exchange 成本。

## 使用命令介面，將 Active Directory 站台設定為中樞站台

當中樞站台存在沿著郵件的最低成本路由路徑時，必須透過中樞站台路由傳送郵件。檢查路由表格記錄檔的內容及檢視**ADTopologyPath ID** \] 區段中，確認選取的網站存在沿著兩個 Active Directory 站台之間的最低成本路由路徑中的資料。如果這不是案例，您需要將 Exchange 特定成本指派給將所選網站會經歷的最低成本路由路徑 IP 站台連結。

若要設定 Active Directory 作為中樞站台，請執行下列命令：

    Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true

此範例將名稱為站台 A 的 Active Directory 站台設定為中樞站台。

    Set-AdSite "Site A" -HubSiteEnabled $true

此範例從名稱為站台 B 的 Active Directory 站台移除中樞站台內容。

    Set-AdSite "Site B" -HubSiteEnabled $false

## 如何才能了解這是否正常運作？

若要確認您是否成功設定 Active Directory 站台成為中樞站台，請執行下列操作：

1.  執行下列命令：
    
        Get-AdSite | Format-List Name,HubSiteEnabled

2.  確認 Active Directory 站台的 *HubSiteEnabled* 值是 `True`。


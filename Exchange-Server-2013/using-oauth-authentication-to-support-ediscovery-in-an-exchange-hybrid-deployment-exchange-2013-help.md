---
title: '在 Exchange 混合式部署中使用 OAuth 驗證來支援 eDiscovery: Exchange 2013 Help'
TOCTitle: 在 Exchange 混合式部署中使用 OAuth 驗證來支援 eDiscovery
ms:assetid: b069f8db-fbe1-4047-ad97-d00172ee6a12
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn497703(v=EXCHG.150)
ms:contentKeyID: 61290502
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Exchange 混合式部署中使用 OAuth 驗證來支援 eDiscovery

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

若要在 Exchange 2013 混合組織中順利執行跨單位 eDiscovery 搜尋，您必須在您的 Exchange 內部部署組織與 Exchange Online 組織之間設定 OAuth (Open Authorization)，以便能使用就地 eDiscovery 搜尋內部部署與雲端信箱。OAuth 驗證在 Exchange 混合部署支援下列的 eDiscovery 案例：

  - 搜尋將「Exchange Online 封存」用於雲端封存信箱的內部部署信箱。

  - 在相同的 eDiscovery 搜尋中，搜尋內部部署和雲端信箱。

如需設定 OAuth 驗證以支援 eDiscovery 的逐步指示，請參閱[設定 Exchange 與 Exchange Online 組織之間的 OAuth 驗證](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)。

## 什麼是 OAuth 驗證？

OAuth 驗證是伺服器對伺服器的驗證通訊協定，可讓應用程式相互驗證。使用 OAuth 驗證時，不會在電腦之間傳遞使用者認證和密碼。取而代之是經由交換安全性權杖來進行驗證和授權，這樣可授與一段時間的權限來存取一組特定的資源。

OAuth 驗證通常涉及三方：一個授權伺服器以及兩個需要彼此通訊的領域。安全性權杖是由授權伺服器 (也稱為安全性權杖伺服器) 發行給兩個需要通訊的領域；這些權杖會確認源自其中一個領域的通訊應受到另一個領域的信任。在內部部署 Exchange 組織和 Exchange Online 之間使用 OAuth 驗證時，由 Office 365 組織中的 Microsoft Azure Active Directory 存取控制服務 (ACS) 提供授權伺服器的功能。例如，在跨部門部署 eDiscovery 搜尋期間，Azure ACS 會發出權杖來驗證 Exchange 內部部署組織的管理員或法務人員能夠存取 Exchange Online 組織中的信箱，反之亦然。

## 混合式部署 eDiscovery 案例

下表識別 Exchange 混合式部署中需要 OAuth 驗證的 eDiscovery 案例。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>eDiscovery 案例</th>
<th>需要 OAuth 驗證嗎？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>從 Exchange 內部部署組織起始的相同 eDiscovery 搜尋中，搜尋 Exchange 內部部署信箱和 Exchange Online 信箱。例如，在單一 eDiscovery 搜尋中搜尋組織中的所有信箱。</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>搜尋使用 Exchange Online 封存作為雲端式封存信箱的 Exchange 內部部署信箱。使用「就地 eDiscovery 時」會同時搜尋主要和封存信箱。</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>從管理員或法務人員所起始的 eDiscovery 搜尋中，搜尋 Exchange 內部部署組織中的 Exchange Online 信箱。</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>使用由管理員或法務人員從 Exchange 內部部署組織所起始的 eDiscovery 搜尋中，搜尋內部部署信箱。</p></td>
<td><p>否</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>之前討論過，如果內部部署信箱是以雲端式封存信箱來設定，則需要 OAuth 驗證。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p>從登入 Office 365 使用者帳戶的 Office 365 承租人管理員或法務人員在 Exchange Online 或 SharePoint Online 的 eDiscovery 中心所起始的 eDiscovery 搜尋中，搜尋 Exchange Online 信箱。</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


## 設定 OAuth 驗證來支援 eDiscovery

如前所述，請參閱＜[設定 Exchange 與 Exchange Online 組織之間的 OAuth 驗證](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)＞，以取得在 Exchange 混合式部署中設定 OAuth 驗證來支援 eDiscovery 的相關指示。

如果 Exchange 混合式部署未設定 OAuth，則您無法使用 eDiscovery 在相同的 eDiscovery 搜尋中搜尋 Exchange 內部部署和 Exchange Online 信箱。您必須從內部部署組織所起始的 eDiscovery 搜尋來搜尋內部部署信箱。同樣地，您只有從 Exchange Online 組織所起始的 eDiscovery 搜尋或使用 SharePoint Online 的 eDiscovery 中心，才能搜尋 Exchange Online 信箱。此外，如果主要內部部署信箱的相對應封存信箱位於 Exchange Online 或 Exchange Online 封存組織中，則您無法搜尋主要內部部署信箱。

## 其他資訊

  - 您也可以使用 OAuth 驗證來允許其他應用程式 (例如 SharePoint 2013 和 Lync Server 2013) 向 Exchange 2013 驗證。如需詳細資訊，請參閱 [設定 SharePoint 2013 與 Lync 2013 的 OAuth 驗證](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md)。

  - 您可以設定 Exchange 2013 和 SharePoint 2013 之間的伺服器對伺服器驗證，讓管理員和法務人員可以使用 SharePoint 2013 的 eDiscovery 中心來搜尋 Exchange 2013 信箱。如需詳細資訊，請參閱 [設定 Exchange for SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)。

  - 您可以設定 Exchange 混合部署中Exchange 2013使用混合組態精靈\]。自訂的逐步說明混合部署設定檢查清單請參閱[Exchange Server Deployment Assistant](https://go.microsoft.com/fwlink/p/?linkid=277105)。


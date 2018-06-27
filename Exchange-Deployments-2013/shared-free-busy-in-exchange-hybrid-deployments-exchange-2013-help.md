---
title: 'Exchange 混合式部署中的共用空閒/忙碌: Exchange 2013 Help'
TOCTitle: Exchange 混合式部署中的共用空閒/忙碌
ms:assetid: bd3884de-80ee-4ff2-a8a3-eacd5aa3e51b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ650274(v=EXCHG.150)
ms:contentKeyID: 50474709
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 混合式部署中的共用空閒/忙碌

 

_<strong>適用版本：</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2016-04-29_

混合式部署的其中一個主要優勢，就是能讓內部部署組織的使用者與 Exchange Online 組織的使用者共用空閒/忙錄 (行事曆可用性) 資訊。這兩個組織中的使用者可以檢視彼此的行事曆，就好像他們都在相同實體組織中一樣。這會使排程會議和資源更容易且有效率。

混合部署中需要有下列幾個元件，才能啟用您的內部部署 Exchange 組織和 Exchange Online 之間的共用空閒/忙碌功能。

  - **同盟信任**   內部部署組織與 Office 365 服務組織都需要與 Azure AD 驗證系統建立同盟信任。同盟信任是與 Azure AD 驗證系統的一對一關係，它會為您的 Exchange 組織定義參數。系統作為您的內部部署組織與 Office 365 服務組織之間的信任代理人使用時，會使用這些參數在內部部署組織與 Exchange Online 組織使用者之間交換空間/忙碌資訊。
    
    建立帳戶時會自動為 Office 365 服務組織設定與系統的同盟信任。混合組態精靈會自動確認內部部署組織與 Azure AD 驗證系統之間是否存有同盟信任。如果存在，即使用現有的同盟信任支援混合式部署。如果不存在，則精靈會建立內部部署組織與 Azure AD 驗證系統的同盟信任。此精靈還會將混合組態精靈中選取的任何網域新增到內部部署組織同盟信任。
    
    若要深入了解，請參閱 [共用](https://technet.microsoft.com/zh-tw/library/dd638083\(v=exchg.150\))。

  - **組織關聯性**   內部部署和 Exchange Online 組織兩者皆須建立組織關聯性，且會由混合組態精靈自動設定。組織關聯性會為組織定義共用的空閒/忙錄資訊層級。
    
    依預設，對於內部部署和 Exchange Online 組織關聯性的空閒/忙碌資料存取的共用層級均為 \[空閒/忙碌存取的時間，再加上主旨與位置\]。若想修改內部部署和 Exchange Online 組織使用者之間的空閒/忙碌資訊共用存取，可於混合組態精靈完成之後，手動設定組織關聯性存取層級。
    
    若要深入了解，請參閱 [共用](https://technet.microsoft.com/zh-tw/library/dd638083\(v=exchg.150\))。

為您的組織設定混合式部署時，混合組態精靈會在所有案例中自動設定共用空閒/忙碌行事曆存取。為內部部署組織建立與 Azure AD 驗證系統的同盟信任，以及為其設定與 Exchange Online 組織的組織關係，是混合式部署的需求。若不想在混合式部署中允許內部部署和 Exchange Online 組織使用者之間進行空閒/忙碌資訊共用，可於混合組態精靈完成之後，使用 Exchange 管理命令介面 和 [Set-HybridConfiguration](https://technet.microsoft.com/zh-tw/library/hh529932\(v=exchg.150\)) Cmdlet 來手動停用空閒/忙碌資訊共用功能。

下表中所示的混合式部署功能，在同盟信任和組織關係上有相依性。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>訊息區</th>
<th>Feature</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>電子郵件用戶端</p></td>
<td><ul>
<li><p>郵件追蹤</p></li>
<li><p>郵件提示</p></li>
<li><p>多信箱搜尋</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>法規符合性</p></td>
<td><ul>
<li><p>Exchange Online 封存</p></li>
<li><p>Exchange In-place eDiscovery</p></li>
</ul></td>
</tr>
</tbody>
</table>


---
title: '組織關係: Exchange 2013 Help'
TOCTitle: 組織關係
ms:assetid: 4c48db61-3370-462b-a3f8-2a6311c6e4ee
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657445(v=EXCHG.150)
ms:contentKeyID: 50473078
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 組織關係

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-02-20_

設定組織關係，可與外部企業合作夥伴共用行事曆資訊。Exchange 系統管理員可設定與 Office 365 組織或其他 Exchange 內部部署組織之間的組織關係。如果您要與另一個內部部署 Exchange 組織共用行事曆，則雙方的內部部署 Exchange 系統管理員都必須設定與雲端的驗證關係 (也稱為「同盟」)，且必須符合最低軟體需求。

組織關係是企業之間的一對一關係，可讓雙方組織的使用者檢視行事曆可用性資訊。在設定組織關係時，您必須設定您那一方的關係，並指定外部組織的使用者可檢視的資訊層級。外部組織可在他們那一方進行相同或不同的設定。例如，假設 Contoso 建立了與 Tailspin Toys 的組織關係，則 Tailspin Toys 的使用者可將 Contoso 使用者的電子郵件地址新增至會議邀請，以排程讓這些使用者參加的會議。Tailspin Toys 使用者將可檢視獲邀之 Contoso 使用者能否與會的情形。不過，必須在 Tailspin Toys 的系統管理員設定與 Contoso 的組織關係後，Contoso 才能檢視 Tailspin Toys 使用者能否與會的情形。

您可以指定三種存取層級：

  - 沒有存取權

  - 只存取可與會時間 (空閒/忙碌資訊)

  - 可存取空閒/忙碌資訊，包括時間、主旨與地點

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果使用者不要將其空閒/忙碌資訊與他人共用，他們可變更 Outlook 中的預設權限項目。若要執行此動作，使用者可移至 <strong>[行事曆內容]</strong> &gt; <strong>[權限]</strong> 索引標籤，選取 <strong>[預設]</strong> 權限，然後選取 <strong>[權限層級]</strong> 清單中的 <strong>[無]</strong>。內部或外部使用者將看不見其空閒/忙碌資訊，即使有組織關係存在亦然。此時會套用使用者所設定的權限。</td>
</tr>
</tbody>
</table>


下列主題將協助您設定及管理組織關係，作為組織共用機制的一部分：

[建立組織關聯性](create-an-organization-relationship-exchange-2013-help.md)

[修改組織關聯性](modify-an-organization-relationship-exchange-2013-help.md)

[移除組織關係](remove-an-organization-relationship-exchange-2013-help.md)

要尋找更多關於同盟共用的資訊嗎？請參閱[共用](sharing-exchange-2013-help.md)。


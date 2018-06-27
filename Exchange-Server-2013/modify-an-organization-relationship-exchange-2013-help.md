---
title: '修改組織關聯性: Exchange 2013 Help'
TOCTitle: 修改組織關聯性
ms:assetid: 3713ef83-f01a-41bb-b127-62ca242dd7a4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673055(v=EXCHG.150)
ms:contentKeyID: 50472969
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 修改組織關聯性

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-01-01_

組織關係可讓您的 Exchange 組織中的使用者，與 Office 365 組織或其他內部部署 Exchange 組織共用行事曆的空閒/忙碌資訊。您可能會想要變更組織關係的設定 (例如變更名稱、暫時停用行事曆共用、變更存取層級，或變更將共用行事曆的安全性群組)。

與其他組織共用行事曆之前，您必須設定與雲端之間的驗證關係 (也稱為「同盟」)，且必須符合最低軟體需求。若要深入了解同盟共用，請參閱[共用](sharing-exchange-2013-help.md)。

如需與同盟相關的其他管理工作，請參閱[同盟程序](federation-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的*Calendar and Sharing Permissions* 項目。

  - 您必須為內部部署 Exchange 組織設定作用中同盟信任。

  - 您想要在組織關係中設定外部組織也必須與Azure AD驗證系統建立同盟信任。

  - 本主題中的程序會對名為 Contoso 的組織關係進行變更。這些範例將說明如何：
    
      - 將名為 service.contoso.com 的網域新增至外部組織。
    
      - 停用組織關聯性的空閒/忙碌資訊共用。
    
      - 將空閒/忙碌資訊存取層級從*Calendar free/busy information with time, subject, and location*變更為*Calendar free/busy information with time only*。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 使用 EAC 將網域新增至組織關係

1.  在內部部署組織中的 Exchange 2013 伺服器上，瀏覽至 \[組織\] \> \[共用\]。

2.  在清單檢視的 \[組織共用\] 下方，選取組織關聯性 Contoso，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[組織關係\] 中，\[一般\] 並不會變更組織關係的 \[名稱\]

4.  在 \[要共用的網域\] 方塊中輸入網域 **service.contoso.com**，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

5.  按一下\[儲存\] 來更新組織關係。

## 使用 EAC 來停用組織關係的空閒/忙碌資訊共用

1.  移至 \[組織\] \> \[共用\]。

2.  在清單檢視的 \[組織共用\] 下方，選取組織關聯性 Contoso，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[組織關係\] 中，按一下 \[共用\]。

4.  選取 \[僅限行事曆空閒/忙碌的時間資訊\]。

5.  按一下\[儲存\] 來更新組織關係。

## 使用 EAC 來變更組織關係的空閒/忙碌資訊存取層級

1.  移至 \[組織\] \> \[共用\]。

2.  在清單檢視的 \[組織共用\] 下方，選取組織關聯性 Contoso，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[組織關係\] 中，按一下 \[共用\]。

4.  選取 \[僅限行事曆空閒/忙碌的時間資訊\]。

5.  按一下\[儲存\] 來更新組織關係。

## 使用命令介面修改組織關係

  - 本範例將網域名稱 service.contoso.com 新增至組織關係 Contoso。
    
        $domains = (Get-OrganizationRelationship Contoso).DomainNames
        $domains += 'service.contoso.com'
        Set-OrganizationRelationship -Identity Contoso -DomainNames $domains

  - 本範例停用組織關係 Contoso。
    
        Set-OrganizationRelationship -Identity Contoso -Enabled $false

  - 這個範例會啟用組織關聯性 WoodgroveBank 的行事曆可用性資訊存取，並將存取層級設定為 `AvailabilityOnly` (只含時間的行事曆空閒/忙碌資訊)。
    
        Set-OrganizationRelationship -Identity Contoso -FreeBusyAccessEnabled $true -FreeBusyAccessLevel AvailabilityOnly

如需詳細的語法及參數資訊，請參閱 [Get-OrganizationRelationship](https://technet.microsoft.com/zh-tw/library/ee332343\(v=exchg.150\)) 與 [Set-OrganizationRelationship](https://technet.microsoft.com/zh-tw/library/ee332326\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您已成功更新組織關聯性，請執行下列命令介面命令並確認組織關聯性資訊。

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


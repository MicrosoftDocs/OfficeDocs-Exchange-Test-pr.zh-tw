---
title: '停用或重新啟用 Exchange 組織的同盟共用: Exchange 2013 Help'
TOCTitle: 停用或重新啟用 Exchange 組織的同盟共用
ms:assetid: d36490d8-0268-47b9-a6d4-e56427f1b02e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657497(v=EXCHG.150)
ms:contentKeyID: 50474325
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 停用或重新啟用 Exchange 組織的同盟共用

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-02-17_

有時候您可能需要暫時停用您組織的同盟共用。您只要停用同盟信任的組織識別碼 (OrgID)，不需要刪除現有的同盟信任，也不需要刪除未來可能需要的組織關係和共用原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>對於 Office 365 的混合部署，停用內部部署伺服器的同盟信任也將停用混合功能，例如共用行事曆空閒/忙碌資訊、郵件提示和訊息追蹤。不過，如果停用內部部署組織的同盟信任，則不會停用安全郵件傳輸。</td>
</tr>
</tbody>
</table>


若要了解同盟信任相關資訊，請參閱[同盟](federation-exchange-2013-help.md)。若要深入了解同盟共用，請參閱[共用](sharing-exchange-2013-help.md)。

若欲瞭解更多與同盟共用相關的管理工作，請參閱 [同盟程序](federation-procedures-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此 Exchange Server 2013 功能與中國的 21Vianet 所運作的 Office 365 不完全相容，部分功能可能受限。如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解 21Vianet 運作的 Office 365</a>。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) 主題中的 *Federation and certificates* 權限項目。

  - 其他同盟 Exchange 組織的任何現有組織關係和共用原則將不予修改，並且不會產生作用。設定為向網際網路收件者提供行事曆資訊存取權的共用原則將不受影響。

  - 您無法使用 Exchange 系統管理中心 (EAC) 停用或啟用同盟信任的 OrgID。您必須使用命令介面。

## 使用命令介面停用或重新啟用同盟共用

這個範例停用 OrgID，並停用 Exchange 組織的同盟及同盟共用。

    Set-FederatedOrganizationIdentifier -Enabled $false

這個範例啟用 OrgID，並重新啟用 Exchange 組織的同盟及同盟共用。

    Set-FederatedOrganizationIdentifier -Enabled $true

如需詳細的語法及參數資訊，請參閱 [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/zh-tw/library/dd351037\(v=exchg.150\))。

## 如何知道這是否正常運作？

成功完成 **Set-OrganizationIdentifier** Cmdlet，即表示已停用或啟用 OrgID。

若要進一步確認成功，請執行下列命令介面，並確認 *Enabled* 參數的傳回值

    Get-FederatedOrganizationIdentifier

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


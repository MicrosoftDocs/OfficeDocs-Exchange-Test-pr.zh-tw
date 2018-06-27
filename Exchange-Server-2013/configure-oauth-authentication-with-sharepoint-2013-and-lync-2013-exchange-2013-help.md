---
title: '設定 SharePoint 2013 與 Lync 2013 的 OAuth 驗證: Exchange 2013 Help'
TOCTitle: 設定 SharePoint 2013 與 Lync 2013 的 OAuth 驗證
ms:assetid: ca3c78a3-80cc-4df2-859f-0106bbd57a07
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ649094(v=EXCHG.150)
ms:contentKeyID: 50474224
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 SharePoint 2013 與 Lync 2013 的 OAuth 驗證

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-03-03_

Exchange Server 2013允許其他應用程式使用 OAuth 對 Exchange 進行驗證。應用程式必須設定為 Exchange 2013 中的夥伴應用程式。

在 Exchange 2013 中，僅支援使用 `Configure-EnterpriseApplication.ps1` 指令碼進行 SharePoint 2013 及 Lync Server 2013 等夥伴應用程式的 OAuth 組態。將工作自動化之後，指令碼將更容易設定夥伴應用程式的認證，並減少組態錯誤。指令碼可執行下列工作：

1.  設定企業夥伴應用程式自行發出 OAuth 權杖，以便向 Exchange 成功驗證。

2.  將角色存取控制 (RBAC) 角色指派給夥伴應用程式，以授權該應用程式呼叫特定的 Exchange Web 服務 API。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 夥伴應用程式必須發佈 Exchange 2013 的授權中繼資料文件，才能建立此應用程式的直接信任，並接受驗證要求。

  - 本主題中的範例使用 `\Scripts` 目錄的下列預設位置：`C:\Program Files\Microsoft\Exchange Server\V15\Scripts`.

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [共用和協同作業的權限](sharing-and-collaboration-permissions-exchange-2013-help.md) 主題中的「夥伴應用程式 - 設定」項目。

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


## 設定夥伴應用程式的 OAuth 驗證

此程序使用 `Configure-EntepririseApplication.ps1` 指令碼設定夥伴應用程式的 OAuth 驗證。資源的存取權限取決於使用 RBAC 對於夥伴應用程式及/或其模擬的使用者所指派的權限。

從 Exchange 設定 OAuth 驗證後，夥伴應用程式即可使用 Exchange 2013 資源。如果 Exchange 2013 也需要存取夥伴應用程式所提供的資源，則必須也設定夥伴應用程式中的 OAuth 驗證。

此範例會設定 SharePoint 2013的 OAuth 驗證。

    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://sharepoint.contoso.com/_layouts/15/metadata/json/1 -ApplicationType SharePoint

此範例會設定 Lync Server 2013的 OAuth 驗證。

    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://lync.contoso.com/metadata/json/1 -ApplicationType Lync

## 如何知道這是否正常運作？

若要確認您是否已成功設定企業夥伴應用程式向 Exchange 2013 進行驗證，請執行命令介面中的 [Get-PartnerApplication](https://technet.microsoft.com/zh-tw/library/jj218721\(v=exchg.150\)) cmdlet 來擷取組態。您也可以執行 [Test-OAuthConnectivity](https://technet.microsoft.com/zh-tw/library/jj218623\(v=exchg.150\)) cmdlet，針對使用者測試夥伴應用程式的 OAuth 連線。

## 其他資訊

  - 在混合式部署中，您可以在內部部署 Exchange 2013 組織和 Exchange Onlin 組織之間使用 OAuth 驗證。如需詳細資訊，請參閱[在 Exchange 混合式部署中使用 OAuth 驗證來支援 eDiscovery](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md)。

  - 在內部部署中，您可以在 Exchange 2013 與 SharePoint 2013 之間設定伺服器對伺服器驗證，以便系統管理員和法務人員可以利用 SharePoint 2013 中的 eDiscovery 中心搜尋 Exchange 2013 信箱。如需詳細資訊，請參閱[設定 Exchange for SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)。


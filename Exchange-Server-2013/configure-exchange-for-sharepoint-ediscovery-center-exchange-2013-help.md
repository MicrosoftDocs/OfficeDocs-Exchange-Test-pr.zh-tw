---
title: '設定 Exchange for SharePoint eDiscovery Center: Exchange 2013 Help'
TOCTitle: 設定 Exchange for SharePoint eDiscovery Center
ms:assetid: 795c1a3b-295c-4ee5-ade9-52cf3fda3f19
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ218665(v=EXCHG.150)
ms:contentKeyID: 50473540
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Exchange for SharePoint eDiscovery Center

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange Server 2013 包含可搭配 Microsoft SharePoint Server 2013 和 Microsoft Lync Server 2013 使用的功能，也稱為*協力應用程式*。若要確保這些協力應用程式可以存取其他資源，您必須設定伺服器對伺服器驗證。

這個主題會說明如何設定Exchange 2013和SharePoint 2013之間的伺服器對伺服器驗證讓使用者可以使用SharePoint 2013中的 eDiscovery 中心搜尋Exchange Server 2013信箱內容。若要完全啟用此功能，您必須完成SharePoint 2013中的其他步驟。如需詳細資訊，請參閱[在 SharePoint 2013 中的設定 eDiscovery](https://go.microsoft.com/fwlink/?linkid=257727)。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：30 分鐘。

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

  - 支援將 Exchange 2013 和 SharePoint 2013 安裝在不同網域或樹系中。Exchange 和 SharePoint 樹系之間不需要有 Windows 信任關係，因為在該環境中，Exchange 和 SharePoint 將仰賴 OAuth 2.0 通訊協定來彼此信任。

  - 必須設定 SharePoint 2013 站點使用安全通訊端層 (SSL)。

  - 必須執行SharePoint 2013每台伺服器上安裝[Exchange Web Services Managed API](https://go.microsoft.com/fwlink/?linkid=257726) 。安裝之後要重設 Internet Information Server (IIS)。

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


## 該怎麼做？

## 步驟 1：將 Exchange 2013 的伺服器對伺服器驗證設定在執行 SharePoint Server 2013 的伺服器上

執行以下命令將 Exchange 2013 建立為 SharePoint 2013 中受到信任的安全性權杖發行者。

    New-SPTrustedSecurityTokenIssuer -Name Exchange -MetadataEndPoint https://<Exchange Server Name or FQDN>/autodiscover/metadata/json/1

## 步驟 2：將 SharePoint 2013 的伺服器對伺服器授權設定在執行 Exchange 2013 的伺服器上

在 Exchange 2013 伺服器上執行此步驟。您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[共用和協同作業的權限](sharing-and-collaboration-permissions-exchange-2013-help.md)主題中的「協力廠商應用程式 - 設定」項目。

執行此命令以設定 SharePoint 夥伴應用程式。

    cd c:\'Program Files'\Microsoft\'Exchange Server'\V15\Scripts
    .\Configure-EnterprisePartnerApplication.ps1 -AuthMetadataUrl <path to SharePoint AuthMetadataUrl> -ApplicationType SharePoint

## 步驟 3：將經過授權的使用者新增至探索管理角色群組

將必須使用 SharePoint 2013 執行 eDiscovery 搜尋的使用者新增至 Exchange 2013 中的探索管理角色群組。如需詳細資訊，請參閱[Exchange 中指派 eDiscovery 權限](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>將使用者新增至「探索管理」角色群組，讓他們能使用就地 eDiscovery 來搜尋所有 Exchange 2013 信箱及存取使用者信箱中的潛在敏感電子郵件內容。根據預設，此權限並未指派給任何使用者，包括組織管理角色群組的成員。在指派此權限給任何使用者前，請洽詢您組織的法務與人力資源部門。</td>
</tr>
</tbody>
</table>


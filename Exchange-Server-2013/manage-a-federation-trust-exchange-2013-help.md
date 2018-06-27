---
title: '管理同盟信任: Exchange 2013 Help'
TOCTitle: 管理同盟信任
ms:assetid: 0439839f-2052-4bc9-9d30-aa6e7d51b733
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673036(v=EXCHG.150)
ms:contentKeyID: 50472477
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理同盟信任

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-01-01_

同盟信任會建立 Microsoft Exchange 2013組織和Azure Active Directory驗證系統之間的信任關係，並且支援與其他同盟 Exchange 組織的同盟共用。一般而言，您不應該有可管理或會在建立之後修改的同盟信任。不過，可能需要新增或移除同盟的網域或重設用來設定同盟信任的組織識別碼 (OrgID) 的網域的情況。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>修改現有同盟信任，尤其是用於定義 OrgID 的共用網域，可能會干擾同盟 Exchange 組織間的同盟共享，或 Office 365 組織部署的混合式部署。</td>
</tr>
</tbody>
</table>


如需與同盟相關的其他管理工作，請參閱[同盟程序](federation-procedures-exchange-2013-help.md)。

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

  - 預估完成時間：30 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) 主題中的 *Federation and certificates* 權限項目。

  - 您將需要為每個新增到同盟信任的新同盟網域新增 TXT 記錄到公用 DNS 。請檢閱將 TXT 記錄新增至裝載公用 DNS 記錄之組織的需求。

  - 本主題目的為，依照下列設定設定現有同盟信任：
    
      - **Contoso.com** 為同盟信任的主要共享網域。（此網域將不會變更。）
    
      - 同盟網域 **service.contoso.com** 及**sales.contoso.com** 皆包含在現有同盟信任內。
    
      - **Marketing.contoso.com** 是 Exchange 組織中公認的網域。

  - 本主題同時涵蓋其他同盟管理工作，例如檢視並管理用於同盟信任的憑證，以及檢視命令介面的同盟信任參數。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 使用 EAC 來管理同盟信任

1.  在內部部署組織中的 Exchange 2013 伺服器上，瀏覽至 \[組織\] \> \[共用\]。

2.  在 \[同盟信任\] 區段上，按一下 \[修改\]。

3.  在\[啟用共用的網域\]中略過 \[步驟 1\]，因為主要共享網域並未變更。

4.  在\[步驟 2\]中選取 \[service.contoso.com\] 後，再按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")，即可從同盟信任中移除網域。

5.  在\[步驟 2\] 中按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

6.  在\[選取公認的網域\]中，從公認的網域清單中選取 \[marketing.contoso.com\]後，再按一下 \[確定\] 來新增網域到同盟信任。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>將為 [marketing.contoso.com] 網域建立同盟信任網域證明字串。您必須在此網域的公用 DNS 建立不同的 TXT 記錄。</td>
    </tr>
    </tbody>
    </table>


7.  使用為 \[marketing.contoso.com\] 網域建立的同盟信任網域證明字串，在此公用 DNS 伺服器上建立 TXT 記錄。視您的公用 DNS 主機的更新排程而定，DNS 變更的複寫可能需要 15 分鐘或更長的時間。

8.  建立並複製 TXT 記錄後，按一下 \[更新\]。

## 使用命令介面來管理同盟信任

1.  此範例會從同盟信任中移除 service.contoso.com 網域。
    
        Remove-FederatedDomain -DomainName service.contoso.com

2.  這個範例會將網域 marketing.contoso.com 新增至同盟信任。
    
        Add-FederatedDomain -DomainName marketing.contoso.com

如需詳細的語法及參數資訊，請參閱 [Remove-FederatedDomain](https://technet.microsoft.com/zh-tw/library/dd298128\(v=exchg.150\)) 與 [Add-FederatedDomain](https://technet.microsoft.com/zh-tw/library/dd351208\(v=exchg.150\))。

執行下列命令介面命令以管理同盟信任的其他層面：

1.  **檢視同盟 OrgID 與同盟網域**
    
    這個範例會顯示 Exchange 組織的 OrgID 和相關的資訊，包括同盟網域與狀態。
    
        Get-FederatedOrganizationIdentifier

2.  **檢視同盟信任憑證**
    
    此範例會顯示同盟信任「Azure AD 驗證」所使用的前一個、現行和下一個憑證。
    
        Get-FederationTrust "Azure AD authentication" | Select Org*certificate

3.  **檢查同盟憑證狀態**
    
    這個範例顯示組織中所有信箱與用戶端存取伺服器上的同盟憑證的狀態。
    
        Test-FederationTrustCertificate

4.  **設定同盟信任，將憑證作為下一個憑證**
    
    此範例會設定同盟信任「Azure AD 驗證」，以使用含有指紋的憑證作為下一個憑證。將憑證部署到組織中所有的 Exchange 伺服器之後，可以使用 *PublishCertificate* 參數設定信任使用此一同盟憑證做為目前憑證。
    
        Set-FederationTrust "Azure AD authentication" -Thumbprint AC00F35CBA8359953F4126E0984B5CCAFA2F4F17

5.  **設定同盟信任使用下一個憑證作為目前的憑證**
    
    本範例設定同盟信任 Azure AD 驗證至下一個憑證作為目前的憑證，並將它發佈至Azure AD驗證系統。
    
        Set-FederationTrust "Azure AD authentication" -PublishFederationCertificate
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在設定同盟信任使用下一個憑證做為目前同盟憑證之前，請確定您組織中所有的 Exchange 伺服器上已部署了憑證。使用 <a href="https://technet.microsoft.com/zh-tw/library/dd335228(v=exchg.150)">Test-FederationTrustCertificate</a> 指令程式檢查憑證的部署狀態。</td>
    </tr>
    </tbody>
    </table>


6.  **重新整理同盟中繼資料和Azure AD驗證系統中的憑證**
    
    此範例會重新整理同盟中繼資料和Azure AD驗證系統的同盟信任 Azure AD 驗證的憑證。
    
        Set-FederationTrust "Azure AD authentication" -RefreshMetadata

如需詳細的語法及參數資訊，請參閱下列主題：

  - [Get-FederatedOrganizationIdentifier](https://technet.microsoft.com/zh-tw/library/dd298149\(v=exchg.150\))

  - [Get-FederationTrust](https://technet.microsoft.com/zh-tw/library/dd351262\(v=exchg.150\))

  - [Test-FederationTrustCertificate](https://technet.microsoft.com/zh-tw/library/dd335228\(v=exchg.150\))

  - [Set-FederationTrust](https://technet.microsoft.com/zh-tw/library/dd298034\(v=exchg.150\))

## 如何知道這是否正常運作？

成功完成的 \[啟用共享網域\] 精靈是您的第一個指示，代表已如預期設定同盟信任。

若要進一步確認完成，請執行下列操作：

1.  執行下列命令介面命令，確認同盟信任資訊。
    
        Get-FederationTrust | format-list

2.  執行下列命令介面命令，確認可以從您的組織擷取同盟資訊。例如，確認 sales.contoso.com 與 marketing.contoso.com 網域皆以 *DomainNames* 參數被傳回。
    
        Get-FederationInformation -DomainName <your primary sharing domain>

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


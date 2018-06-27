---
title: '更新同盟憑證: Exchange 2013 Help'
TOCTitle: 更新同盟憑證
ms:assetid: 0f390713-3058-44d0-9c07-3c982616e790
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt779252(v=EXCHG.150)
ms:contentKeyID: 74429220
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更新同盟憑證

 

_**上次修改主題的時間：**2017-02-28_

本主題說明如何更新同盟信任中所使用的自我簽署的同盟憑證：

  - 如果的同盟憑證尚未過期，請遵循 \[更新工作的同盟憑證\] 區段中的步驟。

  - 如果已經有到期的同盟憑證，請遵循取代過期的同盟憑證\] 區段中的步驟。

如需同盟信任和同盟的詳細資訊，請參閱[同盟](federation-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的 「 同盟與憑證 」 項目。

  - 本主題中的程序使用Exchange 管理命令介面。若要了解如何在內部部署 Exchange 組織中開啟 Exchange 管理命令介面，請參閱[開啟命令介面。](https://technet.microsoft.com/zh-tw/library/dd638134\(v=exchg.150\))。

  - 若要查看是否您現有的同盟憑證已過期， Exchange 管理命令介面中執行下列命令：
    
        Get-ExchangeCertificate -Thumbprint (Get-FederationTrust).OrgCertificate.Thumbprint | Format-Table -Auto Thumbprint,NotAfter

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 更新工作的同盟憑證

如果同盟憑證尚未過期，您可以使用新的同盟憑證更新現有的同盟信任。

## 步驟 1： 建立新的同盟憑證

建立新的同盟憑證Exchange 管理命令介面中執行下列命令：

    $SKI = [System.Guid]::NewGuid().ToString("N"); New-ExchangeCertificate -DomainName 'Federation' -FriendlyName "Exchange Delegation Federation" -Services Federation -SubjectKeyIdentifier $SKI -PrivateKeyExportable $true

如需詳細語法及參數的資訊，請參閱 [New-ExchangeCertificate](https://technet.microsoft.com/zh-tw/library/aa998327\(v=exchg.150\))。

命令輸出中包含新憑證指紋的值。您需要這個值中的其餘步驟，以及您可以直接從Exchange 管理命令介面視窗複製值：

1.  以滑鼠右鍵按一下 \[ Exchange 管理命令介面 \] 視窗中的任何地方，並在出現的對話方塊中選取**標示**。

2.  選取憑證指紋值，並按 ENTER。

其他程序本主題中，我們將使用的同盟憑證指紋值： `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`。您的憑證指紋值可能會不同。

## 步驟 2： 設定新的憑證作為同盟的憑證

若要使用Exchange 管理命令介面為同盟憑證設定新的憑證，使用下列語法：

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint <Thumbprint> -RefreshMetaData

本範例會使用憑證指紋值`6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`步驟 1 中。

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint 6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73 -RefreshMetaData

如需詳細的語法及參數資訊，請參閱[Set-FederationTrust](https://technet.microsoft.com/zh-tw/library/dd298034\(v=exchg.150\))。

**請注意：** 命令輸出中包含您需要更新證明網域擁有權的 DNS 的 TXT 記錄一則警告訊息。會進行的下一個步驟。

## 步驟 3： 更新同盟證明網域擁有權的外部 DNS 的 TXT 記錄

您可以安全地執行此步驟，因為證明網域擁有權 TXT 記錄只會檢查期間啟用 (步驟 5)。不過，您要更新的 TXT 記錄後，才可以繼續下一個步驟您需要允許以傳播更新的 TXT 記錄的時間 （依據的存留時間或 TTL 值的 DNS 記錄）。

1.  尋找的所需的 TXT 記錄所需的值Exchange 管理命令介面中執行下列命令：
    
        Get-FederatedDomainProof -DomainName <Domain> | Format-List Thumbprint,Proof
    
    例如，如果您的同盟的網域是 contoso.com，執行下列命令：
    
        Get-FederatedDomainProof -DomainName contoso.com | Format-List Thumbprint,Proof
    
    命令輸出看起來如下：
    
    `Thumbprint : <new certificate thumbprint>`（例如`6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`）
    
    `Proof      : <new hash text>`（例如`znMfbkgSbOQSsWFdsW+gm3to0nZSdE3zbcPPHGVAqdgsLFGsCPuLHiyVbKoPmgyZKX90NH2g1PbCZH0YTQF6oA==`）
    
    `Thumbprint : <old certificate thumbprint>`（例如`CC9BC204BB4DC60D06FC1F10F3C373DC785DA2A5`）
    
    `Proof      : <old hash text>`（例如`m4gZX7OLr9iOWYJMVjEklQpoSkPb5hSbcFjD7Q3/vsqmdJ2Z+HcSt7j5pzBKFmEW2s27JYr3xsK2POzAI/8Ffw==`）
    
    請注意命令輸出傳回資訊的兩個證明網域擁有權的記錄： 一個用於新的憑證，另一個可用於您要取代目前的憑證。您可以分清哪個是以指紋值，並在外部 （公用） DNS 的 TXT 記錄目前證明網域擁有權的已設定的雜湊文字值。

2.  更新同盟證明網域擁有權的外部 DNS 的 TXT 記錄。指示會隨您的 DNS 提供者，但您可以編輯目前 TXT 記錄以新的雜湊文字值取代目前的雜湊文字值。如需詳細資訊，請參閱 Exchange Online\] 區段中的[Office 365 的外部網域名稱系統記錄](https://go.microsoft.com/fwlink/p/?linkid=265522)。

## 步驟 4： 確認新的同盟憑證至Exchange的所有伺服器的通訊

Exchange自動分散每個新的同盟憑證到所有伺服器，但是我們需要我們可以繼續之前先確認分配。

若要使用Exchange 管理命令介面確認新的同盟憑證的散佈，執行下列命令：

    $Servers = Get-ExchangeServer; $Servers | foreach {Get-ExchangeCertificate -Server $_ | Where {$_.Services -match 'Federation'}} | Format-List Identity,Thumbprint,Services,Subject

**請注意：** 在Exchange 2010、 **Test-FederationCertificate**指令程式的輸出包含伺服器名稱。此指令程式以Exchange 2013或更新版本的輸出不包括伺服器名稱。

## 步驟 5： 啟動新的同盟憑證

若要使用Exchange 管理命令介面啟動新的同盟憑證，請執行下列命令：

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -PublishFederationCertificate

如需詳細的語法及參數資訊，請參閱[Set-FederationTrust](https://technet.microsoft.com/zh-tw/library/dd298034\(v=exchg.150\))。

**請注意：** 命令輸出中包含您需要更新證明網域擁有權 （其已執行步驟 3 中） 部署 DNS 中的 TXT 記錄一則警告訊息。

## 如何才能了解這是否正常運作？

若要確認您是否已更新成功現有的同盟信任與新的同盟憑證，使用下列步驟：

  - 在Exchange 管理命令介面中，執行下列命令來確認已使用新的憑證：
    
        Get-FederationTrust | Format-List *priv*
    
      - **OrgPrivCertificate**屬性應該包含新的同盟憑證的指紋。
    
      - **OrgPrevPrivCertificate**屬性應該包含舊 （取代） 的同盟憑證的指紋。

  - 在Exchange 管理命令介面、 *\<user's email address\>*取代為您組織中使用者的電子郵件地址並執行下列命令來確認同盟信任正常運作：
    
        Test-FederationTrust -UserIdentity <user's email address>

## 取代過期的同盟憑證

如果已經已過期的同盟憑證，您需要移除所有的同盟的網域從同盟信任，然後移除並重新建立同盟信任。

1.  如果您有多個同盟的網域時，您需要讓您可以在上一次移除識別主要網域共用的網域。若要使用Exchange 管理命令介面識別主要的共用的網域和所有的同盟的網域，執行下列命令：
    
        Get-FederatedOrganizationIdentifier | Format-List AccountNamespace,Domains
    
    **AccountNamespace**屬性的值包含主要的共用的網域中格式`FYDIBOHF25SPDLT<primary shared domain>`。例如，在值`FYDIBOHF25SPDLT.contoso.com`contoso.com 是主要的共用的網域。

2.  移除每個同盟的網域的主要的共用的網域不在Exchange 管理命令介面中執行下列命令：
    
        Remove-FederatedDomain -DomainName <domain> -Force

3.  您已移除的所有其他同盟的網域之後，移除主要的共用的網域Exchange 管理命令介面中執行下列命令：
    
        Remove-FederatedDomain -DomainName <domain> -Force

4.  移除同盟信任Exchange 管理命令介面中執行下列命令：
    
        Remove-FederationTrust "Microsoft Federation Gateway"

5.  重新建立同盟信任。指示，請參閱[建立同盟信任](https://technet.microsoft.com/zh-tw/library/dd335198\(v=exchg.150\))。


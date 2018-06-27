---
title: '建立 um 憑證: Exchange 2013 Help'
TOCTitle: 建立 um 憑證
ms:assetid: 66807ee7-3d3f-482d-a3ac-d4e9baca3271
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn205141(v=EXCHG.150)
ms:contentKeyID: 54652587
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立 um 憑證

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-29_

您可以使用 EAC 或命令介面中的 \[新增 Exchange 憑證\] 精靈來建立自我簽署的憑證或內部公開金鑰基礎結構 (PKI) 憑證的憑證要求。整合通訊 (UM)，您可以使用這些憑證的其中一個 Microsoft Exchange 整合通訊服務和 Microsoft Exchange Unified Messaging Call Router 服務。您可以使用這兩個服務的相同的憑證或不同的每個服務。您也可以購買及匯入 UM 服務的協力廠商商業憑證。如果您使用自我簽署的憑證 um，您可能需要在主體替代名稱 (SAN) 中包含用戶端存取和信箱伺服器的名稱。

根據預設，當您安裝Exchange Server 2013、 兩個自我簽署的憑證建立 ︰ **Microsoft Exchange 伺服器驗證憑證**和**Microsoft Exchange**。**Microsoft Exchange**自我簽署的憑證可供使用 UM 以加密資料，但您必須將憑證指派給 UM 及 UM 呼叫路由器服務。您將憑證指派給整合通訊服務之後，它可以複製到並匯入至 VoIP 閘道、 IP Pbx 及已啟用 SIP 的 Pbx。不過，而不是使用預設的自我簽署的憑證，您可能需要建立專屬的整合通訊的另一個。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>整合 UM 與 Microsoft Lync Server 時，無法使用自我簽署憑證。</td>
</tr>
</tbody>
</table>


如需與管理整合通訊憑證相關的其他管理工作，請參閱[部署 UM 程序的憑證](deploying-certificates-for-um-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的「憑證管理」項目及[整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 服務」項目。您必須使用該電腦上的本機 Administrators 群組成員帳戶登入。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用 EAC 建立 UM 的憑證要求

1.  在 EAC 中，瀏覽至 **\[伺服器\]** \> **\[憑證\]**，然後按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 **\[新增 Exchange 憑證\]** 頁面，選取 **\[建立向憑證授權單位索取憑證的要求\]**，然後按 **\[下一步\]**。

3.  輸入好記的憑證名稱，然後按 **\[下一步\]**。

4.  如果您不需要萬用字元憑證，按一下 \[**下一步**\]。如果您需要萬用字元憑證，請選取 \[**萬用字元憑證要求\]。萬用字元憑證可以用來保護您使用單一憑證的根網域下的所有子網域**、 輸入之根網域名稱，然後再按 \[**下一步**。

5.  \[**存放區此伺服器上的憑證要求**，請按一下 \[**瀏覽\]**以移至您要儲存檔案的位置。您可以在 Exchange 組織中任何用戶端存取或 Mailbox server 上儲存的憑證要求。選取的位置、 按一下 \[**確定**\] 和 \[**下一步**。

6.  如果您要求萬用字元憑證，請跳至步驟 9。

7.  如果您沒有要求萬用字元憑證，必須指定您想要包含在您的憑證中的網域。如果您想要編輯的網域，按一下 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")，並再按 \[**下一步**。

8.  在您的選擇**架構下的下列網域將會包含在您的憑證。您可以新增其他網域這裡，或變更**、 您可以新增、 編輯、 移除或檢查會列在底下**網域**的網域名稱。然後按 \[**下一步**。

9.  下**指定組織的資訊。這必要的憑證授權單位所**，輸入下列內容：
    
      - **組織名稱**
    
      - **部門名稱**
    
      - **城市/位置**
    
      - **縣/市**
    
      - **國家/地區名稱**：在此選項中，請使用下拉式清單來選取國家或地區。

10. 在 **\[儲存憑證要求到下列檔案\]** 下，輸憑證檔的名稱，然後按一下 **\[完成\]**。

## 使用命令介面建立 UM 的憑證要求

此範例會使用易記名稱 `CertUM` 建立新的 Exchange 憑證要求，以供名為 `MyMailboxServer` 的 Mailbox Server 使用。

    New-ExchangeCertificate -FriendlyName 'CertUM' -GenerateRequest -PrivateKeyExportable $true -KeySize '2048' -DomainName '*.northwindtraders.com' -SubjectName 'C=US,S=wa,L=redmond,O=northwindtraders,OU=servers,CN= northwindtraders.com' -Server 'MyMailboxServer'

## 使用 EAC 建立 UM 的自我簽署憑證

1.  在 EAC 中，瀏覽至 **\[伺服器\]** \> **\[憑證\]**，然後按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 **\[新增 Exchange 憑證\]** 頁面，選擇 **\[建立自我簽署憑證\]**，然後選取 **\[下一步\]**。

3.  輸入好記的憑證名稱，然後選取 **\[下一步\]**。

4.  按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，選取要套用此憑證的 Exchange 伺服器，然後選取 **\[下一步\]**。

5.  指定要包含在憑證中的網域，然後選取 **\[下一步\]**。如果要新增服務的網域，請按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

6.  確認您包含的網域正確，然後選取 **\[完成\]**。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您使用 EAC 來建立自我簽署的憑證時，系統會提示您將不會啟用憑證的服務。建立憑證之後，您可以使用 EAC 或<strong>Enable-ExchangeCertificate</strong>指令程式在命令介面來啟用 Exchange 服務。如需如何將憑證指派給 UM 服務的詳細資訊，請參閱<a href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">將憑證指派給 UM 及 UM 呼叫路由器服務</a>。</td>
</tr>
</tbody>
</table>


## 使用命令介面建立 UM 的自我簽署憑證

此範例會使用易記名稱 `UMCert` 建立新的 Exchange 自我簽署憑證，以供名為 `MyMailboxServer` 的 Mailbox Server 使用。

    New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您指定服務時您想要使用<em>Services</em>參數啟用、 提示您要指派這些服務。在這個範例中，將會提示您若要啟用 UM 及 UM 呼叫路由器服務的憑證。如需如何啟用服務的憑證的詳細資訊，請參閱<a href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">將憑證指派給 UM 及 UM 呼叫路由器服務</a>。</td>
</tr>
</tbody>
</table>


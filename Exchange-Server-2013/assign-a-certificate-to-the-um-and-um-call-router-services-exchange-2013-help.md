---
title: '將憑證指派給 UM 及 UM 呼叫路由器服務: Exchange 2013 Help'
TOCTitle: 將憑證指派給 UM 及 UM 呼叫路由器服務
ms:assetid: 8a900e5f-9779-4213-92d7-ec157b15fbc5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn205140(v=EXCHG.150)
ms:contentKeyID: 54652595
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將憑證指派給 UM 及 UM 呼叫路由器服務

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-29_

您可以使用 EAC 或命令介面來指派給自我簽署、 內部公開金鑰基礎結構 (PKI) 或特定的 Exchange 服務的協力廠商商業憑證。當您使用**New-ExchangeCertificate**指令程式來指派憑證給 Exchange 服務與*Services*參數時，系統會提示您將憑證指派給 Exchange 服務。如果您可以使用 EAC 來建立憑證，新增 Exchange 憑證\] 精靈將不會提示您將憑證指派給 Exchange 服務。您要編輯之憑證的內容並選取您想要將它指派給哪些的服務，以指派憑證。

不同服務有不同的憑證需求。例如，某些服務可能只需要憑證的**主體名稱**或**主體替代名稱**\] 方塊中的伺服器名稱及其他服務可能需要完整的網域名稱 (FQDN)。請確定憑證名稱可支援您讓它以進行服務所需的用途。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您要將整合通訊 (UM) 與 Microsoft Lync Server 整合時，無法使用自我簽署的憑證。</td>
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

## 使用 EAC 將憑證指派給整合通訊和 UM Call Router 服務

1.  在 EAC 中，瀏覽至 **\[伺服器\]** \> **\[憑證\]**。

2.  在清單檢視中，選取您要指派給整合通訊和 UM Call Router 服務的憑證，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 *\<憑證名稱\>* 頁面上，選取 **\[服務\]**，然後選取 **\[UM\]** 和 **\[UM Call Router\]**。

4.  按一下 **\[儲存\]**。

## 使用命令介面將憑證指派給整合通訊和 UM Call Router 服務

此範例將憑證指派給整合通訊和 UM Call Router 服務。

    Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'


---
title: '匯入或匯出 UM 憑證: Exchange 2013 Help'
TOCTitle: 匯入或匯出 UM 憑證
ms:assetid: ee688c33-2e08-47e7-95fc-04ba10238341
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn205143(v=EXCHG.150)
ms:contentKeyID: 54652611
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 匯入或匯出 UM 憑證

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-12-18_

您可使用 EAC 或「命令介面」來匯入或匯出自我簽署、內部公開金鑰基礎結構 (PKI) 或協力廠商商業憑證。在整合通訊 (UM) 中，這其中一個憑證可同時用於 Microsoft Exchange Unified Messaging 服務與 Microsoft Exchange Unified Messaging Call Router 服務。這兩個服務可以使用相同的憑證，或者，每個服務使用不同的憑證。

您在執行以下操作時，匯入 Exchange 憑證將十分實用：

  - 匯入先前已匯出為檔案的憑證。

  - 匯入先前由內部憑證授權單位產生的 PKI 憑證。

  - 匯入協力廠商商業憑證。

您在執行以下操作時，從本機 Exchange 伺服器上的憑證儲存區匯出現有憑證將十分實用：

  - 匯出憑證使其可在另一部 Exchange 伺服器上匯入。

  - 匯出憑證使其可在 VoIP 閘道、IP PBX 或具有 SIP 功能的 PBX 上匯入。

  - 匯出憑證後即可備份憑證和其私密金鑰。

如需與管理「整合通訊」憑證相關的其他管理工作資訊，請參閱[部署 UM 程序的憑證](deploying-certificates-for-um-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的「憑證管理」項目及[整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 服務」項目。您必須使用該電腦上的本機 Administrators 群組成員帳戶登入。

  - 匯出憑證前，使用 **Get-ExchangeCertificate** 指令程式確認憑證上的 *PrivateKeyExportable* 屬性是否已設為 `$true`。

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

## 使用 EAC 匯出憑證

1.  在 EAC 中按一下 **\[伺服器\]** \> **\[憑證\]** \> **\[更多選項\]**![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示")，然後再按一下 **\[匯出 Exchange 憑證\]**。

2.  在 **\[匯出 Exchange 憑證\]** 頁面的 **\[要匯出的檔案\]** 方塊中，輸入憑證檔案的名稱。

3.  在 **\[密碼\]** 方塊中，輸入想要用於保護私密金鑰的密碼，然後按一下 **\[確定\]**。

## 使用命令介面匯出憑證

此範例說明如何在系統提示您輸入使用者名稱和密碼後，將指紋 (Thumbprint) 為 A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC 的憑證匯出至檔案。

    $file = Export-ExchangeCertificate -Thumbprint A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC -BinaryEncoded:$true -Password (Get-Credential).password

此範例會執行下列動作：

1.  使用 **Get-ExchangeCertificate** 指令程式尋找想要匯出的憑證。

2.  使用 **Export-ExchangeCertificate** 指令程式設定憑證密碼。

3.  輸入使用者名稱和密碼後，將憑證匯出至檔案。

<!-- end list -->

    $file = Get-ExchangeCertificate -DomainName umcorp.northwindtraders.com | Export-ExchangeCertificate -BinaryEncoded:$true -Password (Get-Credential).password

    Set-Content -Path "d:\umcerts\selfsigned.pfx" -Value $file.FileData =Encoding Byte

## 使用 EAC 匯入憑證

1.  在 EAC 中按一下 **\[伺服器\]** \> **\[憑證\]** \> **\[更多選項\]**![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示")，然後再按 **\[匯入 Exchange 憑證\]**。

2.  在 **\[匯入 Exchange 憑證\]** 頁面的 **\[要匯入的檔案\]** 方塊中，輸入憑證檔案的共用資料夾路徑和名稱。若憑證採用密碼保護，請在 **\[密碼\]** 方塊中輸入密碼，然後按 **\[下一步\]**。

3.  按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，以選取要套用憑證的伺服器，然後再按 **\[確定\]**。若您想要從清單檢視中移除伺服器，請按一下 **\[移除\]**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")，然後再按 **\[完成\]**。

## 使用命令介面匯入憑證

此範例說明如何在系統提示您輸入使用者名稱和密碼後，從 d:\\certificates\\exchange\\SelfSignedUMCert.pfx 憑證檔案匯入憑證。

    Import-ExchangeCertificate -FileData ([Byte[]]$(Get-Content -Path d:\certificates\exchange\SelfSignedUMCert.pfx -Encoding Byte -ReadCount 0)) -Password:(Get-Credential).password


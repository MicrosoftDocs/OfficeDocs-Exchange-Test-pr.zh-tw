---
title: '建立 UM IP 閘道器: Exchange Online Help'
TOCTitle: 建立 UM IP 閘道器
ms:assetid: 542d6b50-147b-4cec-b54d-61c7b8fc0fc7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998045(v=EXCHG.150)
ms:contentKeyID: 50473128
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMIPGatewayWizardForm.CreateUMIPGatewayWizardPage
ms.translationtype: MT
---

# 建立 UM IP 閘道器

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-16_

當您建立整合通訊 (UM) IP 閘道器時，會啟用 Exchange 伺服器連線至新 Voice over IP (VoIP) 閘道、 專用交換機 (PBX) 啟用工作階段初始通訊協定 (SIP)、 IP PBX 或工作階段邊界控制器 (SBC)。立即建立 UM IP 閘道器之後，您應建立新的 UM 群組搜尋及再建立與 UM IP 閘道的關聯的 UM 群組搜尋。您可以建立一個或多個 UM 群組搜尋產生關聯的 UM IP 閘道的一或多個 UM 撥號。

如需與 UM IP 閘道相關的其他管理工作，請參閱[UM IP 閘道程序](um-ip-gateway-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM IP 閘道」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。 如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

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

## 使用 EAC 建立 UM IP 閘道

1.  
    
    在 EAC 中，瀏覽至 **\[整合通訊\]** \> **\[UM IP閘道\]**，然後按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[新 UM IP 閘道\] 頁面上，輸入下列資訊：
    
      - **名稱**  使用此方塊可指定的 UM IP 閘道的唯一名稱。這是出現在 EAC 中的顯示名稱。如果您有已建立之後變更 UM IP 閘道器的顯示名稱，您必須先刪除現有的 UM IP 閘道器，並再建立另一個名稱為您想要的 UM IP 閘道。UM IP 閘道名稱是必要的但僅顯示用途使用。因為您的組織可能會使用多個 UM IP 閘道，我們建議您使用的 UM IP 閘道器有意義的名稱。UM IP 閘道名稱的最大長度是 64 個字元，而且它可以包含空格。不過，它不能包含任何下列字元："/ \\ \[\]:; |= , + \* ?\< \>。
    
      - \[地址\]   您可以使用 IP 位址或完整網域名稱 (FQDN) 設定 UM IP 閘道器。使用此方塊指定設定於 VoIP 閘道、SIP-enabled PBX、IP PBX 或 SBC 上的 IP 位址或 FQDN。此方塊僅接受有效且格式正確的 FQDN。
        
        您可以在此方塊中輸入字母與數字的字元。支援 IPv4 位址、 IPv6 位址及 Fqdn。如果您想要使用共同的 UM IP 閘道和撥號對應表的其中一個作業系統之間的傳輸層安全性 (相互 TLS) SIP 安全或安全模式，您必須設定 UM IP 閘道 fqdn。您也必須設定該連接埠 5061 上接聽並確認該任何 VoIP 閘道或 IP Pbx 也已設定為接聽連接埠 5061 上的相互 TLS 要求。若要設定 UM IP 閘道器，請執行下列命令： `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`。
        
        如果您使用 FQDN，您必須也請確定您已正確設定 VoIP 閘道的 DNS 主機記錄，讓主機名稱是正確解析為 IP 位址。此外，如果您使用 FQDN，而非 IP 位址、 UM IP 閘道的 DNS 設定變更，您必須停用及啟用以確定 UM IP 閘道的組態資訊正確更新的 UM IP 閘道。
    
      - \[UM 撥號對應表\]   按一下 \[瀏覽\] 可選取您想要與 UM IP 閘道器關聯的 UM 撥號對應表。當選取要與 UM IP 閘道器建立關聯的 UM 撥號對應表時，同時也會建立預設的 UM 群組搜尋，並將其與您所選取的 UM 撥號對應表建立關聯。若您並未選取 UM 撥號對應表，那麼必須以手動方式建立 UM 群組搜尋，然後將該 UM 群組搜尋與您建立的 UM IP 閘道器建立關聯。

3.  
    
    按一下 \[儲存\]。

## 使用命令介面建立 UM IP 閘道

此範例會建立名為 `MyUMIPGateway` 的 UM IP 閘道，讓 Exchange 伺服器開始接受來自 IP 位址為 10.10.10.1 之 VoIP 閘道、啟用 SIP 的 PBX、IP PBX 或 SBC 的來電。

    New-UMIPGateway -Name MyUMIPGateway -Address 10.10.10.1

此範例會建立名為 `MyUMIPGateway` 的 UM IP 閘道，讓 Exchange 伺服器開始接受來自 FQDN 為 MyUMIPGateway.contoso.com 且接聽通訊埠 5061 之 VoIP 閘道、啟用 SIP 的 PBX、IP PBX 或 SBC 的來電。

    New-UMIPGateway -Name MyUMIPGateway -Address "MyUMIPGateway.contoso.com" -Port 5061

此範例會建立名為 `MyUMIPGateway` 的 UM IP 閘道並禁止 UM IP 閘道接聽來電或傳送撥出電話，此外也會設定 IPv6 位址及允許 UM IP 閘道使用 IPv4 和 IPV6 位址。

    New-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false


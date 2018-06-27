---
title: '管理 UM IP 閘道器: Exchange Online Help'
TOCTitle: 管理 UM IP 閘道器
ms:assetid: 387e540f-8c59-42d2-a423-99fcf97e00aa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997283(v=EXCHG.150)
ms:contentKeyID: 50472865
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMIPGatewayGeneralPropertyPageControl
ms.translationtype: MT
---

# 管理 UM IP 閘道器

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-21_

建立整合通訊 (UM) IP 閘道器之後，您可以檢視或設定各種設定。例如，您可以設定的 IP 位址或完整的網域名稱 (FQDN)、 設定撥出電話設定，並啟用或停用郵件等待指示器。

如需與 UM IP 閘道相關的其他管理工作，請參閱[UM IP 閘道程序](um-ip-gateway-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM IP 閘道」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM IP 閘道器。如需詳細步驟，請參閱[建立 UM IP 閘道器](create-a-um-ip-gateway-exchange-2013-help.md)。

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

## 使用 EAC 來檢視或設定 UM IP 閘道內容

1.  在 EAC 中，瀏覽至 \[**整合通訊**\> **UM IP 閘道器**。在清單檢視中，選取您想要管理的 UM IP 閘道和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  
    
    使用 \[ **UM IP 閘道器**\] 頁面上檢視和設定 UM IP 閘道的設定。您可以檢視或設定下列設定：
    
      - **狀態**   這個僅供顯示的欄位可顯示 UM IP 閘道的狀態。
    
      - **名稱**  使用此方塊可指定的 UM IP 閘道的唯一名稱。這是出現在 EAC 中的顯示名稱。如果您有已建立之後變更 UM IP 閘道器的顯示名稱，您必須先刪除現有的 UM IP 閘道器，並再建立另一個 UM IP 閘道器具有適當的名稱。UM IP 閘道名稱是必要的但僅顯示用途使用。因為您的組織可能會使用多個 UM IP 閘道，我們建議您使用的 UM IP 閘道器有意義的名稱。UM IP 閘道名稱的最大長度是 64 個字元，而且它可以包含空格。
    
      - **地址**  您可以設定 UM IP 閘道 IP 位址或完整的網域名稱 (FQDN)。使用此方塊可指定的 IP 位址或 FQDN 上 VoIP 閘道、 已啟用 SIP 的 PBX、 IP PBX 或 SBC 設定。
        
        您可以在此方塊中輸入字母與數字的字元。支援 IPv4 位址、 IPv6 位址及 Fqdn。如果您使用 FQDN，您必須也要確認您已正確設定 VoIP 閘道的 DNS 主機記錄，讓主機名稱是正確解析為 IP 位址。此外，如果您使用 FQDN，而非 IP 位址、 UM IP 閘道的 DNS 設定變更，您必須停用及啟用以確定 UM IP 閘道的組態資訊正確更新的 UM IP 閘道。
        
        如果您想要使用共同的 UM IP 閘道和撥號對應表的其中一個作業系統之間的傳輸層安全性 (相互 TLS) SIP 安全或安全模式，您必須設定 UM IP 閘道 fqdn。您也必須設定該連接埠 5061 上接聽並確認該任何 IP 閘道或 IP Pbx 也已設定為接聽連接埠 5061 上的相互 TLS 要求。若要設定 UM IP 閘道器，請執行下列命令： `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`。
    
      - **允許通過這個 UM IP 閘道的撥出電話**  選取此核取方塊可接受與處理撥出電話的 UM IP 閘道。此設定不會影響來電轉接或從 VoIP 閘道的來電。
        
        預設會建立 UM IP 閘道之後，會啟用此設定。如果您停用此設定，與撥號對應表關聯的使用者將不能夠進行透過 VoIP 閘道、 IP PBX 或**地址**欄位中所定義的 SBC 撥出電話。
    
      - **允許郵件等待指示器**  選取此核取方塊以允許語音信箱簡訊通知傳送給使用者的 UM IP 閘道所採取的通話。此設定可讓可接收及傳送 SIP 通知郵件使用者的 UM IP 閘道。此設定預設為啟用，並允許郵件等待將通知傳送給使用者。
        
        表示新的或技術面貌訊息存在任何機制可以參照訊息等待指示器。新的語音郵件已經送達指示可以找到收件匣中如Outlook及Outlook Web App的用戶端。它可採取的短訊息服務 (SMS) 或文字郵件傳送到已登錄的行動電話，從 Exchange 伺服器對預先設定的數字或 lighted 桌上電話指示燈使用者撥出電話的表單。

## 使用命令介面來設定 UM IP 閘道內容

此範例會修改名為 `MyUMIPGateway` 之 UM IP 閘道的 IP 位址。

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

此範例會防止名為 `MyUMIPGateway` 的 UM IP 閘道接受傳入呼叫並防止傳出呼叫。

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com -Status 2 -OutcallsAllowed $false

此範例會使 UM IP 閘道可當成 VoIP 閘道模擬器使用，並且能與 **Test-UMConnectivity** 指令程式搭配使用。

    Set-UMIPGateway -Identity MyUMIPGateway -Simulator $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在您對 UM IP 閘道組態進行的所有變更複寫到與 UM IP 閘道位於相同 UM 撥號對應表中的所有 Exchange 伺服器之前，有一個延遲期。</td>
</tr>
</tbody>
</table>


此範例將防止名為 `MyUMIPGateway` 的 UM IP 閘道接受來電並阻止撥出電話、設定 IPv6 地址並且允許 UM IP 閘道使用IPv4 與 IPV6 地址。

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## 使用命令介面來檢視 UM IP 閘道內容

此範例會顯示 Active Directory 樹系中所有 UM IP 閘道的格式化清單。

    Get-UMIPGateway |Format-List

此範例會顯示名為 `MyUMIPGateway` 之 UM IP 閘道的內容。

    Get-UMIPGateway -Identity MyUMIPGateway

此範例會顯示全部的 VoIP 閘道，包括 Active Directory 樹系中的 IP 閘道模擬器。

    Get-UMIPGateway -IncludeSimulator $true


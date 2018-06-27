---
title: '安裝及設定 Address Book Policy Routing 代理程式: Exchange 2013 Help'
TOCTitle: 安裝及設定 Address Book Policy Routing 代理程式
ms:assetid: 20e8a43d-4508-4388-a2c9-aa3073593cc2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ907308(v=EXCHG.150)
ms:contentKeyID: 51409165
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安裝及設定 Address Book Policy Routing 代理程式

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-01-09_

通訊錄原則路由代理程式是在 Mailbox Server 上執行的傳輸代理程式，其控制您組織中的收件者解析方式。安裝及設定 ABP 路由代理程式時，指派給不同 GAL 的使用者會顯示為外部收件者，因為他們不能檢視外部收件者的連絡人卡片。

如需其他 ABP 相關的管理工作資訊，請參閱 [Address book 原則程序](address-book-policy-procedures-exchange-2013-help.md)。

在尋找此主題的 Exchange Online 版本？請參閱[開啟 \[通訊錄原則路由](https://technet.microsoft.com/zh-tw/library/jj891095\(v=exchg.150\))。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：15 分鐘。

  - 安裝及設定 ABP 路由代理程式之後，可能需要長達 30 分鐘，代理程式才能評估組織中的電子郵件。

  - 您無法使用 EAC 來執行此程序。您必須使用命令介面。

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

## 步驟 1：安裝 ABP 路由代理程式

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸代理程式」項目。

請執行下列命令，安裝 ABP 路由代理程式。這是您將需要使用的確切命令和語法。

    Install-TransportAgent -Name "ABP Routing Agent" -TransportAgentFactory "Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.AddressBookPolicyRoutingAgentFactory" -AssemblyPath $env:ExchangeInstallPath\TransportRoles\agents\AddressBookPolicyRoutingAgent\Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.dll

您會看到一則警告，需要重新啟動 Transport 服務，您的變更才會生效，但請先執行步驟 2，如此只需重新啟動一次 Transport 服務。

如需詳細的語法及參數資訊，請參閱 [Install-TransportAgent](https://technet.microsoft.com/zh-tw/library/aa997998\(v=exchg.150\))。

## 步驟 2：啟用傳輸路由代理程式

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸代理程式」項目。

安裝 ABP 路由代理程式之後，您需要執行下列命令啟用它：

    Enable-TransportAgent "ABP Routing Agent"

如需詳細的語法及參數資訊，請參閱 [Enable-TransportAgent](https://technet.microsoft.com/zh-tw/library/bb124921\(v=exchg.150\))。

## 步驟 3：重新啟動 Transport 服務，並驗證已安裝並啟用 ABP 路由代理程式

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸代理程式」項目。

1.  執行下列命令，重新啟動 Transport 服務。
    
        Restart-Service MSExchangeTransport

2.  重新啟動服務之後，執行下列指令程式驗證已安裝並啟用 ABP 路由代理程式。
    
        Get-TransportAgent
    
    如果列出 ABP 路由代理程式，則表示代理程式已正確安裝。

如需詳細的語法及參數資訊，請參閱 [Get-TransportAgent](https://technet.microsoft.com/zh-tw/library/bb123536\(v=exchg.150\))。

## 步驟 4：啟用 ABP 路由代理程式

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸組態」項目。

此程序的最後一個步驟是啟用組織的 ABP 路由。執行下列命令。

    Set-TransportConfig -AddressBookPolicyRoutingEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-TransportConfig](https://technet.microsoft.com/zh-tw/library/bb124151\(v=exchg.150\))。


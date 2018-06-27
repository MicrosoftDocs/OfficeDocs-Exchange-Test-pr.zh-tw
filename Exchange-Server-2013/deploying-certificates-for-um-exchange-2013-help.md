---
title: '部署 UM 憑證: Exchange 2013 Help'
TOCTitle: 部署 UM 憑證
ms:assetid: 95658f6f-eac2-4674-90e7-f2d3f25c5242
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee681661(v=EXCHG.150)
ms:contentKeyID: 52062576
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 部署 UM 憑證

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-29_

您可以使用相互傳輸層安全性 (相互 TLS) 若要啟用整合通訊 (UM) 以加密資料的 Microsoft Exchange 2013 伺服器與 VoIP 閘道、 IP Pbx、 工作階段邊界控制器 (Sbc) 之間傳送和 Microsoft Lync Server。憑證繫結兩個電子機碼 （公用及私人） 的憑證擁有者用來加密及數位簽署資訊的身分識別。

如果您使用 SIP 安全或 Exchange 2010 組織中的 「 安全 」 撥號，您需要匯入您的 Exchange 2013 Client Access server 執行 Microsoft Exchange UM 呼叫路由器服務和執行 Microsoft Exchange UM 服務的信箱伺服器所使用的憑證。您可以使用其中一個下列憑證 UM 及 UM 呼叫路由器服務：

  - 自我簽署 (Exchange) 憑證

  - 內部公開金鑰基礎結構 (PKI) 憑證

  - 協力廠商商業性憑證

根據預設，當您安裝整合通訊的自我簽署的憑證建立及使用。與 VoIP 閘道、 IP Pbx 和 Sbc 但時不顯示您正在整合 UM 和 Lync Server 可以使用此自我簽署的憑證。如果您正在部署與 Lync Server 搭配使用的憑證、 您需要使用 Exchange 憑證精靈\] 或 \[ **New-ExchangeCertificate**指令程式來取得由內部發行的憑證或 PKI 憑證授權單位 (CA) 或購買商業或協力廠商憑證的互相信任 Unified Messaging 和 Lync Server。

## 部署 VoIP 閘道、IP PBX 及 SBC 的憑證

若要啟用 UM 來加密 VoIP 閘道、IP PBX 及 SBC 之間傳送的資料，您必須執行下列操作：

  - 使用自我簽署的 UM 憑證、建立新的 Exchange 憑證要求並取得內部 PKI 憑證，或購買可用於 UM 和 VoIP 閘道、IP PBX 及 SBC 之間相互 TLS 的協力廠商商業性憑證。

  - 匯入要用於組織中所有 Client Access Server 及 Mailbox Server 上的憑證。

  - 啟用由 UM 服務使用的憑證。

  - 將憑證匯入 VoIP 閘道、IP PBX 及 SBC。

  - 將 UM 撥號對應表設定為「SIP 安全」或「安全」。

  - 設定組織中 Client Access Server 及 Mailbox Server 的 UM 啟動模式。

  - 以完整網域名稱 (FQDN) 建立必要的 UM IP 閘道。

  - 將 UM IP 閘道上的接聽通訊埠設定為使用 TLS 通訊埠 5061。

  - 重新啟動所有 Client Access Server 上的整合通訊呼叫路由器服務，並重新啟動所有 Mailbox Server 上的 Microsoft Exchange 整合通訊服務。

## 部署 Lync Server 的憑證

若要加密 UM 和 Lync Server 之間傳送的資料，您必須執行下列操作：

  - 建立新的 Exchange 憑證要求及取得內部的 PKI 憑證，或購買的協力廠商商業憑證。由 UM 和 Lync Server 必須互相信任憑證。

  - 匯入要用於組織中所有 Client Access Server 及 Mailbox Server 上的憑證。

  - 啟用由 UM 服務使用的憑證。

  - 在執行 Lync Server 的電腦上匯入憑證。

  - 將 SIP URI UM 撥號對應表設定為「SIP 安全」或「安全」。

  - 設定組織中 Client Access Server 及 Mailbox Server 的 UM 啟動模式。

  - 從 Lync Server 電腦執行 OcsUmUtil.exe。

  - 重新啟動所有用戶端存取伺服器上的 Unified Messaging Call Router 服務並重新啟動 Microsoft Exchange 整合通訊服務的所有信箱伺服器上您組織中。如需詳細資訊，請參閱[UM 服務程序](um-services-procedures-exchange-2013-help.md)。

  - 重新啟動屬於 Enterprise Edition 前端集區或重新啟動 Standard Edition 前端伺服器的所有 Lync 伺服器上的 Lync Server 前端服務。您可以使用**Stop-CsWindowsService**指令程式來停止 Lync Server 服務及**Start-CsWindowsService**指令程式來啟動 Lync Server 服務。
    
    **Start-CsWindowsService**和**Stop-CsWindowsService**指令程式會類似的一般的 Windows PowerShell cmdlet **Start-Service**與**Stop-Service**。如果您想，您可以使用**Start-Service**或**Stop-Service**指令程式來啟動及停止 Lync Server 服務。不過， **Start-CsWindowsServiceStop-CsWindowsService**指令程式會包含容易停止及啟動遠端電腦上的 Lync Server 服務的*ComputerName*參數。為達成此目的，您可以包含*ComputerName*參數，後面加上遠端電腦的完整的網域名稱 (FQDN)。**Start-Service**和**Stop-Service**指令程式不需要相較下的參數。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若想完全整合 UM 和 Lync Server，您還需在組織的任何 Client Access Server 或 Mailbox Server 上執行 ExchUcUtil.ps1 指令碼。</td>
    </tr>
    </tbody>
    </table>


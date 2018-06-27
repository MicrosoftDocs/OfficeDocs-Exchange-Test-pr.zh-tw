---
title: '設定 VoIP 安全性設定: Exchange Online Help'
TOCTitle: 設定 VoIP 安全性設定
ms:assetid: b5335654-c766-4f3f-883c-f31263e1d9c1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201721(v=EXCHG.150)
ms:contentKeyID: 50474061
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 VoIP 安全性設定

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2014-10-16_

您可以啟用 Voice over IP (VoIP) 安全性整合通訊 (UM) 撥號。預設會建立 UM 撥號對應表之後，它會使用非安全的模式或未加密。Exchange 伺服器可以接聽來電的單一或多個 UM 撥號對應表和可以具有不同的 VoIP 安全性設定的撥號接聽來電。在 Office 365 和 Exchange Online 安全模式，無法停用。

當您設定 UM 撥號對應表使用工作階段初始通訊協定 (SIP) 安全或安全模式時，為該 UM 撥號對應表接聽電話的 Exchange 伺服器會將 SIP 訊號流量 (適用 SIP 安全模式) 加密，或將即時傳輸通訊協定 (RTP) 媒體通道和 SIP 訊號流量 (適用安全模式) 兩者都加密。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>就內部部署與混合部署而言，當您在執行 Microsoft Exchange 整合通訊呼叫路由器服務的 Client Access Server 或在執行 Microsoft Exchange 整合通訊服務的 Mailbox Server 上設定 SipTCPListeningPort、SipTLSListeningPort 或 UMStartUpMode 時，您將需要正確設定 Windows 防火牆規則，以允許 SIP 和 RTP 網路流量。</td>
</tr>
</tbody>
</table>


如需與 UM 撥號對應表相關的其他管理工作，請參閱 [UM 撥號對應表規劃程序](um-dial-plan-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」項目。

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

## 使用 EAM 設定 UM 撥號對應表的 VoIP 安全性

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]，選取要變更其 VoIP 安全性的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\]頁面上，按一下 \[設定\]。

3.  在 \[一般\] 的 \[VoIP 安全性模式\] 下，選取下列其中一個選項：
    
      - **安全 SIP**
    
      - **不安全** (預設值)
    
      - **安全的**

4.  按一下 \[儲存\]。

## 使用命令介面設定 UM 撥號對應表的 VoIP 安全性

此範例會設定名為 `MySecureDialPlan` 的 UM 撥號對應表加密 SIP 與 RTP 流量。

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Secured

此範例會設定名為 `MySecureDialPlan` 的 UM 撥號對應表加密 SIP，但不加密 RTP 流量。

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity SIPsecured

此範例會設定名為 `MySecureDialPlan` 的 UM 撥號對應表不要加密 SIP 與 RTP 流量。

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Unsecured


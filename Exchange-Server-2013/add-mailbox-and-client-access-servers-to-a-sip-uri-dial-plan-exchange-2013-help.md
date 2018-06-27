---
title: '將信箱和用戶端存取伺服器新增至 SIP URI 撥號對應表: Exchange 2013 Help'
TOCTitle: 將信箱和用戶端存取伺服器新增至 SIP URI 撥號對應表
ms:assetid: 17fed308-ff0d-4e61-b9f9-e6680b6eccaa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996399(v=EXCHG.150)
ms:contentKeyID: 52062518
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將信箱和用戶端存取伺服器新增至 SIP URI 撥號對應表

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-16_

您可以將用戶端存取和信箱伺服器新增至 SIP URI 撥號對應表。用戶端存取和信箱伺服器無法與電話分機號碼或 E.164 撥號對應表產生關聯但伺服器會接聽所有來電。

如果您要部署 Microsoft Lync Server，讓輸出通話能夠正常運作，則必須手動新增所有 Client Access Server 及 Mailbox Server 至所有您針對 Lync Server 建立的 SIP URI 撥號對應表。

如需與 UM 撥號對應表相關的其他管理工作，請參閱 [UM 撥號對應表規劃程序](um-dial-plan-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」項目。

  - 執行這些程序之前，請確認已建立的 SIP URI 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

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

## 使用 EAC 來新增 Mailbox Server 至 SIP URI 撥號對應表

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  在清單檢視中，選取您要修改的信箱伺服器，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[Exchange Server\]** 頁面上，按一下 **\[整合通訊\]**。

4.  在 **\[UM 服務設定\]** \> **\[關聯的撥號對應表\]** 下，按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

5.  在 **\[選取 UM 撥號對應表\]** 視窗中選取 SIP URI 撥號對應表，然後依序按一下 **\[新增\]**、**\[確定\]** 和 **\[儲存\]**。

## 使用命令介面來新增 Mailbox Server 至 SIP URI 撥號對應表

此範例會將名為`MyMailboxServer`至名為`MySIPDialPlan` SIP URI 撥號對應表的信箱伺服器並防止接受新的來電。它也會設定為雙模式，可讓接受 TCP 與 TLS 要求之信箱伺服器的啟動模式。

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan -Status Disabled -UMStartupMode Dual

本範例會將名稱為 `MyMailboxServer` 的 Mailbox Server 新增至兩個名稱分別為 `MySIPDialPlan` 及 `MySIPDialPlan2` 的 SIP 撥號對應表，並設定下列項目：

  - 同時允許 IPv4 及 IPv6 位址。

  - 將來電最高數量設為 50。

  - 設定 Lync Server 的 SIP 存取服務。

<!-- end list -->

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -MaxCallsAllowed 50 -SipAccessService northamerica.lyncpoolna.contoso.com

## 使用 EAC 來新增 Client Access Server 至 SIP URI 撥號對應表

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  在清單檢視中，選取您要修改的 Client Access Server，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[Exchange Server\]** 頁面上，按一下 **\[整合通訊\]**。

4.  在 **\[UM 呼叫路由器設定\]** \> **\[關聯的撥號對應表\]** 下，按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

5.  在 **\[選取 UM 撥號對應表\]** 視窗中選取 SIP URI 撥號對應表，然後依序按一下 **\[新增\]**、**\[確定\]** 和 **\[儲存\]**。

## 使用命令介面來新增 Client Access Server 至 SIP URI 撥號對應表

此範例會將名為`MyClientAccessServer`至名為`MySIPDialPlan`SIP URI 撥號對應表的用戶端存取伺服器。它也會設定為雙模式，讓用戶端存取伺服器接受 TCP 與 TLS 要求的啟動模式。

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan -Server MyClientAccessServer -UMStartupMode Dual

本範例會將名稱為 `MyClientAccessServer` 的 Client Access Server 新增至兩個名稱分別為 `MySIPDialPlan` 及 `MySIPDialPlan2` 的 SIP 撥號對應表，並允許伺服器同時使用 IPv4 及 IPv6 位址。

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -Server MyClientAccessServer


---
title: '從 SIP URI 撥號對應表中移除 Mailbox 和 Client Access server: Exchange 2013 Help'
TOCTitle: 從 SIP URI 撥號對應表中移除 Mailbox 和 Client Access server
ms:assetid: 367441e1-1a0f-42c8-9fa8-8abe80b3d015
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997238(v=EXCHG.150)
ms:contentKeyID: 54652582
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 從 SIP URI 撥號對應表中移除 Mailbox 和 Client Access server

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-16_

您可以移除用戶端存取和信箱伺服器的 SIP URI 撥號對應表。當您正在部署 Microsoft Lync Server 時、 啟用傳出呼叫正確運作，您必須手動將所有用戶端存取和信箱伺服器加入您已建立 Lync Server 的 SIP URI 撥號。不過，您可能需要的 Client Access server 或信箱伺服器移除 Lync 部署，例如，如果您正在執行維護或離線伺服器。

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

## 使用 EAC 從 SIP URI 撥號對應表移除信箱伺服器

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  在清單檢視中，選取您要修改的信箱伺服器，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[Exchange Server\]** 頁面上，按一下 **\[整合通訊\]**。

4.  在 \[ **UM 服務設定**\>**關聯的撥號對應表**，找出移除，請按一下 \[**移除**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")、 的 SIP URI 撥號\] 和 \[**儲存**。如果您想要移除多個 SIP URI 撥號對應表、 按並按住 CTRL 鍵、 選取您要移除的撥號計劃和 \[**儲存**。

## 使用命令介面從 SIP URI 撥號對應表移除信箱伺服器

此範例會從名為 `MySIPDialPlan` 的 SIP URI 撥號對應表，移除名為 `MyMailboxServer` 的信箱伺服器。

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMService MyMailboxServer
    $s.dialplans-=$dp.identity
    Set-UMService -id MyMailboxServer -dialplans:$s.dialplans

在這個範例中，有三個 SIP URI 撥號對應表： SipDP1、 SipDP2 及 SipDP3。此範例會移除名為`MyMailboxServer` SipDP3 撥號對應表從信箱伺服器。

    Set-UMService -id MyMailboxServer -DialPlans SipDP1,SipDP2

在這個範例中，有兩個 SIP URI 撥號對應表： SipDP1 和 SipDP2。此範例會移除名為`MyMailboxServer` SipDP2 撥號對應表從信箱伺服器。

    Set-UMService -id MyMailboxServer -DialPlans SipDP1

此範例會從所有 SIP 撥號對應表移除名為 `MyMailboxServer` 的信箱伺服器。

    Set-UMService -id MyUMServer -DialPlans $null

## 使用 EAC 從 SIP URI 撥號對應表移除 Client Access Server

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  在清單檢視中，選取您要修改的 Client Access Server，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[Exchange Server\]** 頁面上，按一下 **\[整合通訊\]**。

4.  在 \[ **UM 呼叫路由器設定**\>**關聯的撥號對應表**，找出移除，請按一下 \[**移除**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")、 的 SIP URI 撥號\] 和 \[**儲存**。如果您想要移除多個 SIP URI 撥號對應表、 按並按住 CTRL 鍵、 選取您要移除的撥號計劃和 \[**儲存**。

## 使用命令介面從 SIP URI 撥號對應表移除 Client Access Server

此範例會從名為 `MySIPDialPlan` 的 SIP URI 撥號對應表，移除名為 `MyClientAccessServer` 的 Client Access Server。

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMCallRouterSettings MyClientAccessServer
    $s.dialplans-=$dp.identity
    Set-UMCallRouterSettings -id MyClientAccessServer -dialplans:$s.dialplans

在這個範例中，有三個 SIP URI 撥號對應表： SipDP1、 SipDP2 及 SipDP3。此範例會移除名為`MyClientAccessServer` SipDP3 撥號對應表從用戶端存取伺服器。

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1,SipDP2

在這個範例中，有兩個 SIP URI 撥號對應表： SipDP1 和 SipDP2。此範例會移除名為`MyClientAccessServer` SipDP2 撥號對應表從用戶端存取伺服器。

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1

此範例會從所有 SIP 撥號對應表移除名為 `MyClientAccessServer` 的 Client Access Server。

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans $null


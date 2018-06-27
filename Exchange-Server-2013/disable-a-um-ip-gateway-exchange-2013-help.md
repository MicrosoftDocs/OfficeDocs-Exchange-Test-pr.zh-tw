---
title: '停用 UM IP 閘道器: Exchange Online Help'
TOCTitle: 停用 UM IP 閘道器
ms:assetid: fe3a8797-1230-49cb-a839-ccec238266b6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125257(v=EXCHG.150)
ms:contentKeyID: 50474686
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 停用 UM IP 閘道器

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-13_

根據預設，當您建立整合通訊 (UM) IP 閘道器已啟用 UM IP 閘道器的狀態。建立 UM IP 閘道之後，您可以藉由設定其狀態為 \[停用來停用閘道的作業。停用 UM IP 閘道器、 Voice over IP (VoIP) 閘道後 IP 專用交換機 (PBX) 或其已設定為使用的工作階段邊界控制器 (SBC) 不再可處理傳入的整合通訊呼叫。

如需與 UM IP 閘道相關的其他管理工作，請參閱[UM IP 閘道程序](um-ip-gateway-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM IP 閘道」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認 UM IP 閘道器已建立已啟用。如需詳細步驟，請參閱[建立 UM IP 閘道器](create-a-um-ip-gateway-exchange-2013-help.md)和[啟用 UM IP 閘道](enable-a-um-ip-gateway-exchange-2013-help.md)。

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

## 使用 EAC 來停用 UM IP 閘道器

1.  在 EAC 中，瀏覽至 \[**整合通訊**\> **UM IP 閘道器**\]，選取您要停用 UM IP 閘道，然後按一下 \[**向下箭號**![向下箭號圖示](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "向下箭號圖示")。

2.  在 \[警告\] 頁面上按一下 \[是\]。

## 使用命令介面來停用 UM IP 閘道器

本範例會停用名為`MyUMIPGateway` UM IP 閘道並且阻止它接受來自 VoIP 閘道、 IP PBX 或 SBC 來電。

    Disable-UMIPGateway -Identity MyUMIPGateway

本範例會停用名為`MyUMIPGateway` UM IP 閘道並立即中斷所有目前電話的連線。

    Disable-UMIPGateway -Identity MyUMIPGateway -Immediate $true


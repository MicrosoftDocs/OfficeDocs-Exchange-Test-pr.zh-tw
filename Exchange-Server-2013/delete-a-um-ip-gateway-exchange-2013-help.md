---
title: '刪除 UM IP 閘道器: Exchange Online Help'
TOCTitle: 刪除 UM IP 閘道器
ms:assetid: 569d3741-67dd-4597-8d28-010011be0c12
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998214(v=EXCHG.150)
ms:contentKeyID: 50473134
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 刪除 UM IP 閘道器

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-21_

當您刪除整合通訊 (UM) IP 閘道時，Exchange 伺服器就無法再接受來自 Voice over IP (VoIP) 閘道、已啟用工作階段初始通訊協定 (SIP) 的 Private Branch eXchange (PBX)、IP PBX，或與 UM IP 閘道相關聯的工作階段邊界控制器 (SBC) 的來電。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您只能在完全了解用 VoIP 閘道、IP PBX 或 SBC 停用通訊所造成的影響時，才能刪除 UM IP 閘道。</td>
</tr>
</tbody>
</table>


如需與 UM IP 閘道相關的其他管理工作，請參閱[UM IP 閘道程序](um-ip-gateway-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

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

## 使用 EAC 刪除 UM IP 閘道

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM IP 閘道\]，選取要刪除的 UM IP 閘道，然後按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

2.  在 \[警告\] 頁面上按一下 \[是\]。

## 使用命令介面刪除 UM IP 閘道

本範例會刪除名為 `MyUMIPGateway` 的 UM IP 閘道。

    Remove-UMIPGateway -Identity MyUMIPGateway


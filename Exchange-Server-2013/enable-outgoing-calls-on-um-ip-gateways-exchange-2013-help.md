---
title: '啟用 UM IP 閘道器上的撥出電話: Exchange Online Help'
TOCTitle: 啟用 UM IP 閘道器上的撥出電話
ms:assetid: c3ad8e53-d37e-499e-b1f1-defb0ba1bd12
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673562(v=EXCHG.150)
ms:contentKeyID: 50474198
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用 UM IP 閘道器上的撥出電話

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-13_

您可以啟用整合通訊 (UM) IP 閘道的撥出電話撥出電話已停用。當您選取的 UM IP 閘道屬性上的 \[**允許通過這個 UM IP 閘道的撥出電話**\] 選項時，您可以設定以接受並傳送 over IP (VoIP) 閘道、 專用交換機 (PBX) 啟用工作階段初始通訊協定 (SIP)、 IP PBX 或工作階段邊界控制器 (SBC) 撥出電話語音的 UM IP 閘道。雖然**允許通過這個 UM IP 閘道的撥出電話**設定控制是否能夠啟動使用者的撥出電話的 UM IP 閘道，它不會影響來電轉接或來電 VoIP 閘道、 PBX 啟用 SIP、 IP PBX 或 SBC。

*Outdialing*是用來描述一個 UM 撥號對應表中的使用者會起始通話至另一個撥號對應表中已啟用 UM 的使用者或外部的電話號碼之情況的字詞。

若要允許撥出的已啟用 UM 的使用者，您必須：

  - 確認 UM IP 閘道器允許撥出電話。

  - 建立撥號規則群組建立撥號規則項目在 \[UM 撥號對應表關聯的 UM IP 閘道。

  - 新增至清單中 UM 上的 \[**撥號授權**撥號限制正確的撥號規則群組撥號計劃、 自動語音應答或 UM 信箱原則。

如需與 UM IP 閘道相關的其他管理工作，請參閱[UM IP 閘道程序](um-ip-gateway-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM IP 閘道」項目。

  - 執行這些程序之前，請確認已建立 UM 撥號對應表。 如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

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

## 使用 EAC 來啟用 UM IP 閘道的撥出電話

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM IP 閘道\]，選取要變更的 UM IP 閘道，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[ **UM IP 閘道器**\] 頁面上選取 \[**允許通過這個 UM IP 閘道的撥出電話**\] 旁的核取方塊。

3.  按一下 **\[儲存\]**。

## 使用命令介面來啟用 UM IP 閘道的撥出電話

此範例會啟用在名為`MyUMIPGateway`的 UM IP 閘道的撥出電話。

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $true


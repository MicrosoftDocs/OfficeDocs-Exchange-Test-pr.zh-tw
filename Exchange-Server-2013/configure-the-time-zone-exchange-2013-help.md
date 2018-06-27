---
title: '設定時間的時區: Exchange Online Help'
TOCTitle: 設定時間的時區
ms:assetid: 30d769e1-3657-4622-bc9a-643c63cf46d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997162(v=EXCHG.150)
ms:contentKeyID: 50553960
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定時間的時區

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-17_

根據預設，整合通訊 (UM) 自動語音應答使用 Mailbox server 建立的時區。不過，偶爾您可能必須變更為不同的時區時區 UM 自動語音應答。例如，如果您有兩個 UM 撥號對應表和每個撥號對應表代表不同的時區，您必須設定一個具有相同的時區為信箱伺服器的 UM 自動語音應答和其他 UM 自動語音應答有不同於信箱伺服器的時區。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 自動語音應答」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在執行這些程序之前，請確認已建立 UM 自動語音應答。 如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

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

## 使用 EAC 設定時區

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\] 頁面的 \[UM 自動語音應答\] 下，選取您想為其設定時區的 UM 自動語音應答，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 自動語音應答\] 頁面上，按一下 \[上班時間\]，然後在 \[時區\] 下方，從下拉式清單選取時區。

4.  若要儲存變更，請按一下 \[確定\]，再按 \[儲存\]。

## 使用命令介面設定時區

此範例會將名爲 `MyUMAutoAttendant` 的 UM 自動語音應答上的時區設定為太平洋時區。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -TimeZoneName Pacific


---
title: '新增自動語音應答的分機號碼: Exchange Online Help'
TOCTitle: 新增自動語音應答的分機號碼
ms:assetid: f2bd62ba-1e01-4cb7-862c-c750752e20e0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232200(v=EXCHG.150)
ms:contentKeyID: 50474575
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 新增自動語音應答的分機號碼

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-05_

您可以在整合通訊 (UM) 自動語音應答上設定的分機號碼或多個分機號碼。當您新增 UM 自動語音應答的分機號碼時，該號碼可供來電者撥打到自動語音應答。此外，您可能必須新增因為會有一個以上的分機號碼的來電者可以用來存取的自動語音應答的分機號碼。根據預設，當您建立自動語音應答不設定任何分機號碼。

您可以建立新的自動語音應答而設定的自動語音應答的分機號碼。您也可以建立一個以上的電話或分機號碼與單一自動語音應答關聯。您也可以在您建立 UM 自動語音應答或將它們新增之後設定的自動語音應答時新增分機號碼。在您的 UM 自動語音應答設定的分機號碼的數字數目必須符合 UM 撥號對應表關聯的 UM 自動語音應答上設定分機號碼的數字數目。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以新增，而不是新增分機號碼的工作階段初始通訊協定 (SIP) 位址。SIP 位址由某些 IP 專用交換機 (Pbx) 和 Office Communications Server 2007 R2 或 Microsoft Lync Server。</td>
</tr>
</tbody>
</table>


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

## 使用 EAC 新增 UM 自動語音應答的分機號碼或電話號碼

1.  在 EAC 中，瀏覽至 \[**整合通訊**\> **UM 撥號對應表**。在清單檢視中，選取您想要編輯並按一下 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")UM 撥號對應表。

2.  在 \[UM 撥號對應表\] 頁面的 \[UM 自動語音應答\]下方，選取您要新增分機號碼或電話號碼的 UM 自動語音應答。

3.  在工具列上，按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  在 \[UM 自動語音應答\] 頁面 \> \[一般\] 的 \[存取號碼\] 下方，於文字方塊中輸入您要使用的分機號碼或電話號碼，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

5.  按一下 \[儲存\]，新增號碼。

## 使用命令介面在 UM 自動語音應答上設定分機號碼

此範例會使用多個分機號碼設定名為 `MyUMAutoAttendant` 的 UM 自動語音應答。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -PilotIdentifierList "12345, 72000, 75000"


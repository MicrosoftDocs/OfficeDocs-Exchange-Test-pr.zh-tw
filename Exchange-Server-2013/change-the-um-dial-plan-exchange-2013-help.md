---
title: '變更 UM 撥號對應表: Exchange Online Help'
TOCTitle: 變更 UM 撥號對應表
ms:assetid: 4a6b6b6f-c61c-44e8-91dd-c5d28835f441
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee633465(v=EXCHG.150)
ms:contentKeyID: 50473068
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 變更 UM 撥號對應表

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-05_

您可能需要將移至不同的 UM 撥號對應啟用的整合通訊 (UM) 之使用者或變更與使用者關聯的撥號。例如，您可能會想要已啟用 UM 的使用者移至 SIP URI 撥號對應表的電話分機撥號對應表。

若要變更 UM 撥號對應表，您必須停用使用者的整合通訊及啟用使用者的整合通訊新的 UM 撥號對應表上。這是因為不同的撥號對應表可能會有不同的設定和需求，例如不同的副檔名長度或不同的 URI 類型。例如，SIP URI 撥號對應表需要 SIP 資源識別碼指派給每個已啟用 UM 的信箱，但是電話分機撥號對應表不。此外，每個 UM 信箱包含參照至 UM 撥號對應表和 UM 信箱原則。UM 信箱原則，接著，包含 UM 撥號對應表的參照。如果您變更以指到不同的撥號對應表已啟用 UM 之使用者的主要 proxy 位址，UM 信箱位於中不一致的狀態。

如需與啟用語音信箱之使用者相關的其他管理工作，請參閱[擁有郵件功能的語音使用者程序](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

  - 執行此程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行此程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 執行這些程序之前，請確認現有Exchange收件者已啟用整合通訊。如需詳細步驟，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

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


## 該怎麼做？

## 步驟 1： 建立新的 UM 撥號對應表

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要將已啟用 UM 的使用者遷移至整合的 Microsoft Office Communications Server 2007 R2 或移至 Microsoft Lync Server，則必須先建立 SIP URI 撥號對應表。</td>
</tr>
</tbody>
</table>


如需詳細指示，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

## 步驟 2： 停用使用者的整合通訊

如需詳細指示，請參閱[停用使用者的語音信箱](disable-voice-mail-for-a-user-exchange-2013-help.md)。

## 步驟 3： 整合通訊讓使用者在新的 UM 撥號對應表

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您正在將使用者移至具有Office Communications Server 2007 R2 或 Lync Server 的環境，您還必須在啟用 um 時加入使用者的 SIP 資源識別項。您也必須選取與 SIP 撥號對應表關聯的 UM 信箱原則。</td>
</tr>
</tbody>
</table>


如需詳細指示，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。


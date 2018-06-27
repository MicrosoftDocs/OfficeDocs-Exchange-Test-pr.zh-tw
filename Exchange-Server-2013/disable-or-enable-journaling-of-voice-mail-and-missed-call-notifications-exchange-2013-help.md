---
title: '停用或啟用語音信箱和未接的來電通知的日誌記錄: Exchange 2013 Help'
TOCTitle: 停用或啟用語音信箱和未接的來電通知的日誌記錄
ms:assetid: 5164a92e-69e6-4339-b80c-0cfbf0dc0198
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201690(v=EXCHG.150)
ms:contentKeyID: 50473105
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 停用或啟用語音信箱和未接的來電通知的日誌記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

在 Microsoft Exchange Server 2013 中，當您建立日誌規則來記錄 Exchange 組織中傳送給收件者或寄件者或由他們送出的電子郵件時，會包含整合通訊 (UM) 服務所產生的語音信箱及未接來電通知。使用本主題的程式為整個組織開啟或關閉此功能。

要尋找與日誌記錄相關的其他管理工作嗎？請參閱[管理日誌](manage-journaling-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 主題中的「日誌」項目。

  - 您只能使用命令介面來執行此程序。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用命令介面停用或啟用語音信箱和未接來電通知的日誌記錄

此範例會藉由將 *VoicemailJournalingEnabled* 參數設定為 `$false`，停用語音信箱和未接來電通知的日誌記錄。

    Set-TransportConfig -VoicemailJournalingEnabled $false

此範例會藉由將相同參數設定為 `$true`，啟用語音信箱和未接來電通知的日誌記錄。

    Set-TransportConfig -VoicemailJournalingEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-TransportConfig](https://technet.microsoft.com/zh-tw/library/bb124151\(v=exchg.150\))。

## 詳細資訊

[日誌](journaling-exchange-2013-help.md)

[管理日誌](manage-journaling-exchange-2013-help.md)


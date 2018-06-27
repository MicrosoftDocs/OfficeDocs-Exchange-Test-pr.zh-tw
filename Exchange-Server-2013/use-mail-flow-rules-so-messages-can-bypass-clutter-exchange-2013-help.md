---
title: '使用郵件流程規則讓郵件可以略過雜亂: Exchange Online Help'
TOCTitle: 使用郵件流程規則讓郵件可以略過雜亂
ms:assetid: 58e413f0-aa27-4307-bffd-4df03090a15e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn896639(v=EXCHG.150)
ms:contentKeyID: 64361124
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用郵件流程規則讓郵件可以略過雜亂

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

如果您想要確定您接收特定郵件，您可以建立可確保將這些訊息略過雜亂資料夾對 Exchange 傳輸規則。檢查出[排序低優先順序郵件 Outlook Web App 中的使用雜亂](https://go.microsoft.com/fwlink/p/?linkid=528411)上雜亂的詳細資訊。

與傳輸規則相關的其他管理工作，查看[Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\))和[New-TransportRule](https://technet.microsoft.com/zh-tw/library/bb125138\(v=exchg.150\)) PowerShell 主題。如果您是 PowerShell 的新功能，請參閱下列主題說明在使用 Powershell：

  - [使用遠端 PowerShell 連線到 Exchange Online](https://technet.microsoft.com/zh-tw/library/jj984289\(v=exchg.150\))

  - [使用遠端命令介面連接至 Exchange](https://technet.microsoft.com/zh-tw/library/dd335083\(v=exchg.150\))

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「傳輸規則」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 使用使用者介面來建立傳輸規則，以略過的雜亂資料夾

本範例可讓標題的所有郵件略過雜亂的 「 會議 」。

1.  在 Exchange 系統管理中心中，瀏覽至 \[**郵件流程**\>**規則**。按一下 \[ ![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") ，然後選擇 \[**建立新的規則...**。

2.  完成後在建立新的規則，按一下 \[**儲存**\] 以啟動規則。

![美工圖案範例：如果主旨包含會議，則略過待過濾郵件](images/Dn896639.75957aa4-4b2a-4142-92ff-07f8ccc64d82(EXCHG.150).png "美工圖案範例：如果主旨包含會議，則略過待過濾郵件")

## 使用命令介面來建立傳輸規則，以略過雜亂資料夾

本範例可讓標題的所有郵件略過雜亂的 「 會議 」。

    New-TransportRule -Name <name_of_the_rule> -SubjectContainsWords "Meeting" -SetHeaderName "X-MS-Exchange-Organization-BypassClutter" -SetHeaderValue "true"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在這個範例中，&quot;X-MS-Exchange-組織-BypassClutter&quot;和&quot;true&quot;是區分大小寫。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [New-TransportRule](https://technet.microsoft.com/zh-tw/library/bb125138\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

您可以檢查電子郵件訊息標頭以查看是否電子郵件因為雜亂傳輸規則收件匣中登陸略過。選擇電子郵件訊息的已略過套用傳輸規則雜亂貴組織中的信箱。查看上戳記在郵件標頭及您應該會看見**X-MS-Exchange 位組織-BypassClutter： true**標頭。這表示略過正常運作。 查看如何尋找標頭資訊資訊的[檢視的電子郵件的網際網路標頭資訊](https://go.microsoft.com/fwlink/p/?linkid=822530)主題。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>行事曆項目，例如會議接受、 傳送或拒絕不會在其上有這些標頭。我們使用推出擴充雜亂功能給這些行事曆項目。</td>
</tr>
</tbody>
</table>


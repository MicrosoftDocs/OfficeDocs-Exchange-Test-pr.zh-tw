---
title: '檢視群組成員的動態通訊群組: Exchange Online Help'
TOCTitle: 檢視群組成員的動態通訊群組
ms:assetid: 40b100c6-864e-4c82-9f98-08dd5c83e378
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232019(v=EXCHG.150)
ms:contentKeyID: 50472263
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視群組成員的動態通訊群組

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2018-03-02_

動態通訊群組的成員資格根據特定收件者篩選器而不是一組已定義的收件者的通訊群組。MicrosoftExchange提供預先定義篩選器以讓您輕鬆將建立動態通訊群組的收件者篩選器。*預先定義篩選器*是最常使用的篩選器，您可以使用以符合各種收件者篩選準則。您可以指定您想要包含在動態通訊群組中的收件者類型。此外，您也可以指定收件者必須符合的條件清單。您可以使用命令介面中預覽的收件者使用預先定義篩選器動態通訊群組清單。

## 開始之前有哪些須知？

  - 預估完成時間：2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「動態通訊群組」項目。

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

## 使用命令介面預覽動態通訊群組的成員清單

此範例會傳回名為全職員工的動態通訊群組的成員的清單。第一個命令會動態通訊群組物件儲存在變數`$FTE`。第二個命令會使用**Get-Recipient**指令程式列出符合準則動態通訊群組所定義的收件者。

    $FTE = Get-DynamicDistributionGroup "Full Time Employees"

    Get-Recipient -RecipientPreviewFilter $FTE.RecipientFilter -OrganizationalUnit $FTE.RecipientContainer

如需詳細的語法及參數資訊，請參閱 [Get-DynamicDistributionGroup](https://technet.microsoft.com/zh-tw/library/bb124762\(v=exchg.150\)) 與 [Get-Recipient](https://technet.microsoft.com/zh-tw/library/aa996921\(v=exchg.150\))。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 來檢視動態通訊群組的成員。</td>
</tr>
</tbody>
</table>


## 如何知道這是否正常運作？

若要確認您是否已成功檢視動態通訊群組的成員，執行下列動作：

  - 在命令介面中執行預覽動態通訊群組成員的清單上一個命令之後會傳回成員的清單。例如，如果您使用符合動態通訊群組的收件者篩選器的屬性建立新的使用者信箱，這個新的使用者應該顯示清單中的群組成員。


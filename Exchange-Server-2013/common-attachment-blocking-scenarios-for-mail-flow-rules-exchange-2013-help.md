---
title: '常見的附件封鎖案例: Exchange Online Help'
TOCTitle: 常見的附件封鎖案例
ms:assetid: 5c576439-d55b-4c7f-90ed-a7f72cbb16c2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn950026(v=EXCHG.150)
ms:contentKeyID: 65210907
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 常見的附件封鎖案例

 

_**適用版本：**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**上次修改主題的時間：**2017-02-23_

您的組織可能會需要特定類型的郵件會封鎖或已拒絕以符合法律或規範需求，或以實作特定業務需求。以下是一些常見的案例封鎖您可以設定在Exchange中使用的傳輸規則的所有附件的範例：

  -  
    範例 1： 封鎖郵件含有附件，並通知寄件者

  -  
    範例 2： 通知時封鎖內送的郵件預定的收件者

  -  
    範例 3： 修改通知的主旨列

  -  
    範例 4： 適用於時間限制的規則

如需其他範例顯示如何封鎖特定的附件，請參閱：

  - [使用傳輸規則檢查郵件附件](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013)

  - [使用檢查 Office 365 中的郵件附件的郵件流程規則](https://technet.microsoft.com/zh-tw/library/jj919236\(v=exchg.150\)) (Exchange Online, Exchange Online Protection)

惡意程式碼篩選器包括常見的附件類型篩選。在Exchange 系統管理中心 (EAC)，請移至 \[**保護**，然後按一下 \[**新增\]** (![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")) 新增篩選器。在Exchange Online入口網站中，瀏覽至 \[**保護**\]，然後選取**惡意軟體篩選器**。

若要開始實作任何這些案例封鎖特定訊息類型：

1.  登入Exchange 系統管理中心。

2.  移至 \[**郵件流程**\>**規則**。

3.  按一下 \[**新增\]** (![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示"))，然後選取 \[**建立新的規則**。

4.  在 \[**名稱**\] 方塊中指定規則的名稱\] 和 \[**更多選項\]**。

5.  選取條件和您想要的動作。

**請注意：** 在 EAC 中，您可以輸入最小附件大小為 1 kb，應該會偵測到大部分的附件。不過，如果您想要偵測之任何規模的每個可能的附件，您需要使用 PowerShell 1 個位元組附件大小調整為您在 EAC 中建立規則之後。若要了解如何在內部部署 Exchange 組織中開啟 Exchange 管理命令介面，請參閱[開啟命令介面。](https://technet.microsoft.com/zh-tw/library/dd638134\(v=exchg.150\))。若要了解如何使用 Windows PowerShell 連線到 Exchange Online，請參閱[連線到 Exchange Online Protection PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554)。若要了解如何使用 Windows PowerShell 連線到 Exchange Online Protection，請參閱[連線到 Exchange Online Protection PowerShell](https://go.microsoft.com/fwlink/p/?linkid=627290)。

將現有的規則名稱取代*\<Rule Name\>*並執行下列命令以將附件大小設為 1 個位元組：

    Set-TransportRule -Identity "<Rule Name>" -AttachmentSizeOver 1B

您將附件大小調整為 1 個位元組之後，會顯示在 EAC 中規則的值會是**0.00 KB**。

## 範例 1： 封鎖郵件含有附件，並通知寄件者

如果您不想人員在您的組織傳送或接收附件，您可以設定傳輸規則封鎖所有附件的郵件。

在這個範例中，會封鎖所有傳送至或來自組織之附件的郵件。

![封鎖所有附件的規則](images/Dn950026.38094183-166f-4ba5-a9cf-242e7d0f4e04(EXCHG.150).png "封鎖所有附件的規則")

如果所有您想要做為封鎖郵件，您可能會想要停止規則處理一旦符合此規則。捲動 \[規則\] 對話方塊中，然後選取 \[**停止處理其他規則**\] 核取方塊。

## 範例 2： 通知時封鎖內送的郵件預定的收件者

如果您想要拒絕郵件，但讓預定的收件者知道有何變化，您可以使用 \[**通知郵件的收件者**\] 動作。

您可以通知訊息中包含預留位置，使其包含原始郵件的相關資訊。版面配置區必須括住兩個百分比符號 （%） 及時傳送通知訊息，將預留位置取代從原始郵件的資訊。您也可以使用基本 HTML 例如 \< 巴西 \> \< b \> \< i \> 及 \< img \> 訊息中。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>資訊類型</strong></p></td>
<td><p><strong>版面配置區</strong></p></td>
</tr>
<tr class="even">
<td><p>寄件者的郵件。</p></td>
<td><p>%%從 %%</p></td>
</tr>
<tr class="odd">
<td><p>列出在&quot;To&quot;列上的收件者。</p></td>
<td><p>%%到 %%</p></td>
</tr>
<tr class="even">
<td><p>&quot;[&quot;副本] 行上所列的收件者。</p></td>
<td><p>%%Cc %%</p></td>
</tr>
<tr class="odd">
<td><p>原始郵件的主旨。</p></td>
<td><p>%%主旨 %%</p></td>
</tr>
<tr class="even">
<td><p>從原始郵件標頭。 這是類似的標頭中產生原始郵件的傳遞狀態通知 (DSN) 清單。</p></td>
<td><p>%%標頭 %%</p></td>
</tr>
<tr class="odd">
<td><p>傳送原始郵件的日期。</p></td>
<td><p>%%MessageDate%%</p></td>
</tr>
</tbody>
</table>


在此範例中所包含的附件而傳送給組織內的人的所有郵件已都封鎖，且收件者會收到通知。

![封鎖內送訊息時通知收件者的規則](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "封鎖內送訊息時通知收件者的規則")

## 範例 3： 修改通知的主旨列

時通知傳送給收件者、 主旨行是原始郵件的主旨。如果您想要修改之主旨，以便更清楚收件者，您必須使用這兩個傳輸規則：

  - 第一個規則新增至任何附件的郵件主旨開頭的 「 無法傳遞 」 這個字。

  - 第二個規則封鎖郵件並將通知訊息傳送給寄件者使用新的原始郵件的主旨。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這兩個規則必須具有相同的條件。規則處理順序，因此的第一個規則將新增 「 無法傳遞 」 的字和第二個規則封鎖郵件，並通知收件者。</td>
</tr>
</tbody>
</table>


以下是新的第一個規則看起來如果您想要新增 「 無法傳遞 」 主題：

![在含附件的訊息之前加上「無法傳遞」的規則](images/Dn950026.2552b0bd-c69d-48b4-9e69-267fcaf20e70(EXCHG.150).png "在含附件的訊息之前加上「無法傳遞」的規則")

與第二個規則的作用的封鎖與通知 （範例 2 中從相同的規則）：

![封鎖內送訊息時通知收件者的規則](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "封鎖內送訊息時通知收件者的規則")

## 範例 4： 適用於時間限制的規則

如果您有惡意程式碼散播，可能要套用時間限制的規則，讓您暫時封鎖的附件。例如，以下規則具有 start 和 stop 日和時間：

![顯示時間限制的規則](images/Dn950026.bdc8c4d8-72fa-4c5b-97f2-5fe76d50e643(EXCHG.150).png "顯示時間限制的規則")

## 請參閱


[Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\))  


[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)  
[Exchange Online Protection 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/dn271424\(v=exchg.150\))


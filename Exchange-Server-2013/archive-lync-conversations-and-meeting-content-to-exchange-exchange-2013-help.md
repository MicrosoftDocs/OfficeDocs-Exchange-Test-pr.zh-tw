---
title: 'Lync 交談和會議內容封存至 Exchange: Exchange Online Help'
TOCTitle: Lync 交談和會議內容封存至 Exchange
ms:assetid: 3cff970e-e5ed-4a54-88e6-3665d84b5ed7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn508399(v=EXCHG.150)
ms:contentKeyID: 59678418
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lync 交談和會議內容封存至 Exchange

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

您可以封存Lync Online內容，例如 IM 交談， Exchange Online中使用者的信箱。您可以在內部部署封存Lync 2013Exchange 2013信箱內容。 在兩者線上及內部部署環境中，您必須進行此使用者的信箱上放置訴訟暫止狀態或就地保留。當 Lync 內容會永久刪除的使用者信箱位於所保留、 封存的 Lync 內容保留在使用者的信箱中 \[可復原的項目\] 資料夾。不是可讓使用者看到，但它隨附於 eDiscovery 搜尋。

當您信箱置於訴訟暫止狀態時，會保留所有的內容類型，包括 Lync 項目。根據預設，這也是大小寫當您建立就地保留。不過，如果您想要使用就地保留功能來保留只有 Lync 項目，您可用於從**就地 eDiscovery 和保留**精靈的 \[**選取訊息類型**\] 選項選取**Lync 項目**，如下列螢幕擷取畫面所示。

![保留的位置 Lync 項目](images/Dn508399.691d2324-9fac-4689-8527-c78d387e0e3e(EXCHG.150).jpg "保留的位置 Lync 項目")

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以設定為 「 就地保留來排除 Lync 項目。例如，組織可能會希望比其他類型的內容更短的期間內保留立即訊息和語音信箱項目。若要實作此類型的保留原則，您可以建立的一段時間 （例如 7 年） 保留內容並排除此保留在 Lync 項目為 「 就地保留。然後您可以建立另一個 In-place Hold 保留只有 Lync 項目更短保留持續時間。您還可以指定應保留內容的時間。如需建立保留特定持續時間的詳細資訊，請參閱<a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">就地保留與訴訟暫止</a>。</td>
</tr>
</tbody>
</table>


請參閱下列主題的逐步指示將使用者放置在保留：

  - [建立或移除就地保留](create-or-remove-an-in-place-hold-exchange-2013-help.md)

  - [將信箱設為訴訟暫止](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

與封存相關的其他管理工作，請參閱：

  - [在 Exchange Online 中啟用或停用封存信箱](https://technet.microsoft.com/zh-tw/library/jj984357\(v=exchg.150\))

  - [管理 Exchange 2013 中的就地封存](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

## 其他資訊

  - 封存的 Lync 內容獨立的使用者是否已設定為[儲存在 \[交談記錄\] 資料夾中的 Lync IM 交談](https://go.microsoft.com/fwlink/p/?linkid=400589)的 Lync 用戶端之伺服器上發生。

  - 封存的 Lync 內容開始後使用者放置訴訟暫止或就地保留功能。若要確保使用者的 Lync 封存從建立其帳戶時的時間上的帳戶保留建立後立即進行通訊。

此外，在內部Exchange 2013和Lync 2013部署：

  - 您必須設定 Lync 2013 與 Exchange 2013 之間的 OAuth 驗證。如需詳細資訊，請參閱[與 SharePoint 和 Lync 整合](integration-with-sharepoint-and-lync-exchange-2013-help.md)。

  - 您也可以封存Lync 2013內容至Exchange 2013不論使用者是否處於保留狀態。做法是設定使用者的 Exchange 封存原則。將 Lync 使用者的*ExchangeArchivingPolicy*屬性設定為`ArchivingToExchange`Lync 2013伺服器上使用`Set-CsUser`指令程式。

  - 更多有關封存內部部署中的 Lync 內容的詳細資訊，請[規劃封存](https://go.microsoft.com/fwlink/p/?linkid=400590)Lync 2013文件中。


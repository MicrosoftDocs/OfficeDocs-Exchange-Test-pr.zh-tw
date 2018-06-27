---
title: '必須重新啟動電腦才能繼續執行安裝程式: Exchange 2013 Help'
TOCTitle: 必須重新啟動電腦才能繼續執行安裝程式
ms:assetid: d5c73280-4e54-473a-b328-9673af11e2c0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.rebootpending(v=EXCHG.150)
ms:contentKeyID: 50474343
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 必須重新啟動電腦才能繼續執行安裝程式

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange Server 2013安裝程式無法繼續因為它偵測到本機電腦必須重新啟動以完成其他程式安裝或 Windows 更新。

## 為什麼會發生這種情況？

程式和 Windows 更新在進行安裝時，會對電腦上儲存的檔案進行變更。在安裝期間，程式或 Windows 更新有時候必須變更使用中的檔案。發生這種情況時，您必須先重新啟動電腦，然後才能安裝其他任何程式，例如 Exchange 2013。Exchange 安裝程式需要等其他所有安裝完成後，才能確認其正常運作所需的所有必要條件皆已安裝好。

有時候，上一個程式或 Windows 更新的安裝可能未順利完成。發生這種情況時，它可能會留下變更而導致 Windows 和其他程式認為需要重新啟動。不幸的是，因為失敗的安裝永遠不會清除這些變更，因此會封鎖 Windows 更新和其他程式的安裝。如果發生這種情況，每次您執行 Exchange 安裝程式時，都會繼續看到此錯誤。

## 如何修正？

在大部分的情況下，您只需要重新啟動電腦就能跳過這個錯誤。但有時候即使您已重新啟動電腦，仍可能會收到這個錯誤。當程式或 Windows 更新的安裝需要進行其他變更，而且這些變更也需要重新啟動電腦時，就會發生這種情況。如果重新啟動電腦後仍看到這個錯誤，請嘗試再次重新啟動電腦。

如果您已重新啟動電腦兩次或三次以上，但仍看到這個錯誤，請嘗試將最近安裝的任何程式或 Windows 更新重新安裝。這可能會讓失敗的安裝順利完成。

如果之後重新啟動電腦及重新安裝任何最近程式或Windows更新，您*仍*收到此錯誤，建議您連絡 Microsoft 支援人員。它們可協助您尋找的原因為何Windows和其他程式認為電腦必須重新啟動。若要連絡 Microsoft 支援，請移至[Microsoft Exchange server 支援](https://go.microsoft.com/fwlink/p/?linkid=525940)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您很可能會想要手動刪除或變更 Windows 登錄中的機碼或值，但我們強烈建議您不要嘗試透過這種方式來解決這個問題。這種方式可能可以在當下修正這個問題，但卻可能在日後導致其他問題。如果失敗的安裝是 Windows 更新，這一點格外重要。</td>
</tr>
</tbody>
</table>


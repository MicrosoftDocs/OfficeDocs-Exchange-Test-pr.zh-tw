---
title: '找不到收件者更新 service_RUSMissing: Exchange 2013 Help'
TOCTitle: 找不到收件者更新 service_RUSMissing
ms:assetid: 920fbf51-d5e4-4ac6-869f-7f1c5d9a3024
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.rusmissing(v=EXCHG.150)
ms:contentKeyID: 50473742
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 找不到收件者更新 service\_RUSMissing

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-15_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 或 Exchange Server 2010 安裝程式無法繼續因為找不到收件者更新服務 （俄文） 負責在現有的 Exchange 組織的網域\]。

Microsoft Exchange 安裝程式會要求在現有的 Exchange 組織中每個網域的收件者更新服務執行個體。

如果收件者更新服務執行個體遺漏網域，在網域中建立新的使用者物件將不會收到發行給他們的電子郵件地址。

若要解決此問題，請確認收件者更新服務執行個體存在的每個網域並建立不具有一個，然後重新執行 Microsoft Exchange 安裝程式的網域之收件者更新服務執行個體。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>若要建立為網域的收件者更新服務執行個體</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>開啟 [Exchange 系統管理員。</p></li>
<li><p>依序展開 [<strong>收件者</strong>。</p></li>
<li><p>以滑鼠右鍵按一下 [<strong>收件者更新服務</strong>] 節點、 [<strong>新增</strong>] 和 [<strong>收件者更新服務</strong>。</p></li>
<li><p>在 [新物件] 視窗中，按一下 [<strong>瀏覽]</strong>找出的網域名稱。</p></li>
<li><p>選取的網域名稱及 [<strong>確定]</strong>。</p></li>
<li><p>在 [新物件] 視窗中，按一下 [<strong>下一步</strong>，然後<strong>完成</strong>。</p></li>
</ol></td>
</tr>
</tbody>
</table>


如需收件者更新服務的詳細資訊，請參閱下列 Microsoft 知識庫文章：

  - "How 收件者更新服務會套用收件者原則 」 ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=328738](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=328738))。

  - "How 收件者更新服務會填入通訊清單 」 ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253828](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=253828))。

  - 」 如何檢查進度的 Exchange 收件者更新服務 」 ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=246127](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=246127))。

  - "Exchange 收件者更新服務所執行的工作 」 ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253770](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=253770))。


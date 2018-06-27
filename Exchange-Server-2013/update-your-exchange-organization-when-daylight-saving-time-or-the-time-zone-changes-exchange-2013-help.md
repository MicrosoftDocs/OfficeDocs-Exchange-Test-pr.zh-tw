---
title: '更新 Exchange 組織日光節約時間或時區變更時: Exchange 2013 Help'
TOCTitle: 更新 Exchange 組織日光節約時間或時區變更時
ms:assetid: 5b12615c-24cf-4f46-bf3c-2334dc734ef8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh530051(v=EXCHG.150)
ms:contentKeyID: 70076142
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更新 Exchange 組織日光節約時間或時區變更時

 

_**適用版本：**Exchange Online, Exchange Server, Exchange Server 2010, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

如果您的組織或某些使用者所在的國家或地區變更了本身對日光節約時間 (DST) 的認知原則，或者透過世界協調時 (UTC) 變更本地時間差距，則您可能需要更新 Microsoft Windows、Microsoft Exchange、Microsoft Outlook 或其他程式以順應這些變更。

如需為全球各地的 DST 變更的詳細資訊，包括的連結，請參閱[Microsoft 日光節約時間說明及支援中心](https://go.microsoft.com/fwlink/p/?linkid=99640)。也請瀏覽網站所需要的任何其他更新其他軟體供應商的支援。

即使您的時區並未變更，如果您與世界各地的其他電腦或使用者進行互動，則您的電腦必須能夠顯示正確的日期及計算世界其他地區各種活動的時間。

盡快安裝時區更新可以在從舊時間和日期過渡到新時間和日期時，將預定召開的會議或排定的約會次數減至最少。

## 該怎麼做？

## 步驟 1： 所有用戶端與桌上型電腦上安裝 Windows DST 更新

因為當 DST 或時區變更時，Office 365 驗證系統也會進行更新，因此所有 Office 365 用戶端電腦都必須進行更新，否則可能會發生連線問題。

  - 請確定所有的用戶端和桌面電腦已安裝Windows DST 更新。如需詳細資訊，查看[如何設定日光節約時間的 Microsoft Windows 作業系統](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=914387)。

## 步驟 2︰ 的所有伺服器上安裝 Windows DST 更新

1.  使用 Windows DST 更新來更新所有內部部署伺服器。

2.  如果您正在執行 Office 365，更新任何伺服器互動的 Office 365 驗證系統，例如 DirSync 或 AD FS 伺服器。必須更新這些伺服器以確保上線時間百分比。

**附註**  如果您正在更新伺服器叢集，請確定您依照更新叢集的一般程序。您第一次更新被動 server、 容錯移轉至被動伺服器 （會變成使用中），然後再更新舊名為作用中 （現在被動） 伺服器。如需如何更新伺服器叢集與高可用性伺服器叢集的詳細資訊，請參閱[Update Exchange Server Clusters and High Availability Servers](https://technet.microsoft.com/zh-tw/library/hh530052\(v=exchg.150\))和[如何更新 Windows Server 容錯移轉叢集](https://support.microsoft.com/en-us/kb/174799)。

## 步驟 3： 更新 Exchange 和 Outlook 中，在必要時，用戶端和桌面的電腦上

1.  如果您的使用者使用 Outlook 2007 或舊版用戶端，決定何種 Exchange 或 Outlook 的時區工具來執行，請使用此程序的資料表。

2.  傳送郵件給您需要更新其電腦的使用者，並提供他們取得適當工具的連結。

下表顯示當使用者應該要執行[Exchange 行事曆更新工具](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=930879)或[Microsoft Office Outlook 時區資料更新工具](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667)。尋找您的組織伺服器正在執行，哪個版本和將您的使用者正在執行哪些用戶端程式。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>用戶端版本</strong></p></td>
<td> </td>
</tr>
<tr class="even">
<td><p><strong>組織版本</strong></p></td>
<td><p><strong>Outlook 2003 或 Outlook 2007</strong></p></td>
<td><p><strong>Outlook 2010</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Exchange 2003 內部部署</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=930879">Exchange 行事曆工具</a>或</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">時區資料更新 Microsoft Office Outlook 工具</a></p></td>
<td><p>不需要採取任何動作</p></td>
</tr>
<tr class="even">
<td><p><strong>Exchange 2007 內部部署</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=930879">Exchange 行事曆工具</a>或</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">時區資料更新 Microsoft Office Outlook 工具</a></p></td>
<td><p>不需要採取任何動作</p></td>
</tr>
<tr class="odd">
<td><p><strong>Exchange 2010 內部部署</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=930879">Exchange 行事曆工具</a>或</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">時區資料更新 Microsoft Office Outlook 工具</a></p></td>
<td><p>不需要採取任何動作</p></td>
</tr>
<tr class="even">
<td><p><strong>在內部部署 Exchange 2013</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">時區資料更新 Microsoft Office Outlook 工具</a></p></td>
<td><p>不需要採取任何動作</p></td>
</tr>
<tr class="odd">
<td><p><strong>BPOS-S (Exchange 2007)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">時區資料更新 Microsoft Office Outlook 工具</a></p></td>
<td><p>不需要採取任何動作</p></td>
</tr>
<tr class="even">
<td><p><strong>BPOS-S (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">時區資料更新 Microsoft Office Outlook 工具</a></p></td>
<td><p>不需要採取任何動作</p></td>
</tr>
<tr class="odd">
<td><p><strong>Office 365 (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">時區資料更新工具 Microsoft Office outlook</a>（不支援與 Outlook 2003）</p></td>
<td><p>不需要採取任何動作</p></td>
</tr>
<tr class="even">
<td><p><strong>Office 365 (Exchange 2013)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">時區資料更新 Microsoft Office Outlook 工具</a>（不支援與 Outlook 2003）</p></td>
<td><p>不需要採取任何動作</p></td>
</tr>
<tr class="odd">
<td> </td>
<td> </td>
<td> </td>
</tr>
</tbody>
</table>


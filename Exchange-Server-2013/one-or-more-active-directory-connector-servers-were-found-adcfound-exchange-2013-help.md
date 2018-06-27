---
title: '一或多個 Active Directory 連接器伺服器已 found_ADCFound: Exchange 2013 Help'
TOCTitle: 一或多個 Active Directory 連接器伺服器已 found_ADCFound
ms:assetid: a874f51f-09a2-4a76-9695-d61fb1ee6c1c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.adcfound(v=EXCHG.150)
ms:contentKeyID: 50473900
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 一或多個 Active Directory 連接器伺服器已 found\_ADCFound

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-15_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 與 Exchange Server 2010 安裝程式無法繼續因為一或多個 Active Directory 連接器 (ADC) 已位於目前的 Microsoft Exchange 環境。

ADC 物件從 Exchange Server 5.5 版將混合的模式在 Microsoft Exchange 環境中的 Active Directory 目錄服務，並不支援 Exchange 2007 或 Exchange 2010。

Exchange 2007 或 Exchange 2010 安裝程式需要會移除所有 ADC 元件。

若要解決這個問題，移除所有 ADC 元件，並重新執行 Exchange 2007 或 Exchange 2010 安裝程式。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>若要移除 Active Directory 連接器元件</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>若要停用 ADC 服務正在執行 ADC 服務的伺服器上，以滑鼠右鍵按一下在桌面上的<strong>「 我的電腦</strong>並再按一下 [<strong>管理</strong>。</p></li>
<li><p><strong>服務及應用程式</strong>] 節點，並再按一下 [<strong>服務</strong>] 節點。</p></li>
<li><p>在右窗格中以滑鼠右鍵按一下 [ <strong>Microsoft Active Directory 連接器</strong>，然後按一下 [<strong>內容</strong>。</p></li>
<li><p>將<strong>啟動類型</strong>變更為 [<strong>已停用</strong>。下次啟動電腦時，ADC 服務不會啟動。</p></li>
<li><p>按一下 [<strong>套用</strong>]，然後按一下 [<strong>確定</strong>]。</p></li>
<li><p>若要解除安裝 ADC 服務，使用 Active Directory 安裝精靈在 Microsoft Exchange 2000 Server 或 Microsoft Exchange Server 2003 CD 上。開啟 [\ADC\I386 資料夾並連按兩下 Setup.exe 程式。遵循提示來<strong>移除所有</strong>ADC 服務元件。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須完成步驟 6 和<strong>移除所有</strong>ADC 元件來解決這個問題。停用 ADC 服務不足。</td>
</tr>
</tbody>
</table>

</li>
</ol></td>
</tr>
</tbody>
</table>


如需 ADC 的詳細資訊，請參閱下列 Microsoft 知識庫文章：

  - 325300，"支援網路廣播： 簡介 Active Directory 連接器 」 ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325300](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=325300))。

  - 325221，"支援網路廣播： Microsoft 進階 Active Directory 連接器 」 ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325221](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=325221))。

  - 312632，"如何安裝及 Exchange 2000 Server 中設定 Active Directory 連接器 」 ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=312632](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=312632))。


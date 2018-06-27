---
title: 'Active Directory 網域被混合 mode_LocalDomainModeMixed: Exchange 2013 Help'
TOCTitle: Active Directory 網域被混合 mode_LocalDomainModeMixed
ms:assetid: a6affcfe-7264-455b-8e5c-683fa87383f1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.localdomainmodemixed(v=EXCHG.150)
ms:contentKeyID: 50473883
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory 網域被混合 mode\_LocalDomainModeMixed

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式無法繼續因為現有的 Active Directory 網域不設為 Microsoft Windows® ° 2000 Server 原生模式或搭配成效更佳。

Exchange 2007 的安裝程式會在 Windows 2000 Server 原生模式中，或更佳、 網域中建立可以只存在於的萬用安全性群組。

若要解決此問題，請遵循下列步驟來提高網域功能等級到至少 Windows 2000 Server 原生等級，並再重新執行 Exchange 2007 的安裝程式。

若要提高網域功能等級

1.  開啟 \[Active Directory 網域及信任\]。

2.  在主控台樹狀目錄中，以滑鼠右鍵按一下您要引發功能、 的網域及 \[**提高網域功能等級**。

3.  在**選取 \[可用的網域功能等級**，請使用下列程序之一：
    
      - 若要引發 Windows 2000 server 原生網域功能等級，請按一下**Windows 2000 原生**，然後按一下 \[**提高**。
    
      - 若要引發 Windows Server® 2003 網域功能等級，按一下 \[ **Windows Server 2003**，\] 和 \[**引發。**

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><br />
如果有或會有任何執行 Windows NT® 4.0 的網域控制站與舊版不會引發至 Windows 2000 Server 原生網域功能等級。網域功能等級設為 Windows 2000 Server 原生之後，則無法變更回至 Windows 2000 Server 混合。<br />
如果您有或會有任何執行 Windows NT 4.0 和舊版或 Windows 2000 Server 的網域控制站，不會引發 Windows Server 2003 網域功能等級。網域功能等級設為 Windows Server 2003 之後，它無法回到混合的 Windows 2000 Server 或 Windows 2000 Server 原生變更。</td>
</tr>
</tbody>
</table>


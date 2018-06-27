---
title: 'IIS 是在 32 位元的相容性 mode_IIS32BitMode: Exchange 2013 Help'
TOCTitle: IIS 是在 32 位元的相容性 mode_IIS32BitMode
ms:assetid: 742dfc32-353c-46a2-830e-68aed6a68ce0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.iis32bitmode(v=EXCHG.150)
ms:contentKeyID: 50473498
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS 是在 32 位元的相容性 mode\_IIS32BitMode

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式無法繼續因為 Microsoft 網際網路資訊服務 (IIS) 執行 32 位元模式中的此 64 位元電腦上。

Exchange 2007 需要 IIS 是完整的 64 位元模式中執行 64 位元電腦上時。

若要解決此問題、 IIS 切換成 64 位元模式，然後重新執行 Microsoft Exchange 安裝程式。

IIS 切換成 64 位元模式

1.  開啟命令提示字元。

2.  輸入下列命令：
    
    **cscript c:\\inetpub\\adminscripts\\adsutil.vbs SET /w3svc/AppPools/Enable32BitAppOnWin64 False**

3.  按 enter 鍵


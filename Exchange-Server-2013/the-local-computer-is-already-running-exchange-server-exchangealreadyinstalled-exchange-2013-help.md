---
title: '本機電腦已執行 Exchange Server_ExchangeAlreadyInstalled: Exchange 2013 Help'
TOCTitle: 本機電腦已執行 Exchange Server_ExchangeAlreadyInstalled
ms:assetid: 3f168b5d-9910-418f-86fb-e99d852dcb5e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.exchangealreadyinstalled(v=EXCHG.150)
ms:contentKeyID: 50473016
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 本機電腦已執行 Exchange Server\_ExchangeAlreadyInstalled

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式無法繼續因為本機電腦具有先前安裝的 Microsoft Exchange 元件。

Exchange 2007 的安裝程式會要求之本機電腦未安裝的現有 Microsoft Exchange 元件。

若要解決此問題，移除任何 Microsoft Exchange 2000 Server 或 Microsoft Exchange Server 2003 的元件\]，然後重新執行 Microsoft Exchange 安裝程式。

若要移除 Microsoft Exchange 元件

1.  按一下 \[**開始\]**、 指向 \[**設定**\] 和 \[**控制台\]**。

2.  按兩下 \[新增或移除程式\]。

3.  在**目前安裝的程式**\] 清單中，按一下 \[ **Microsoft Exchange**\] 和 \[**變更/移除**。

4.  在 Microsoft Exchange 安裝精靈\] 中，按一下 \[**下一步**\]。

5.  在 \[元件選擇\] 頁面上的 \[動作\] 清單中，按一下已安裝，每個元件旁的向下箭頭和 \[**移除**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>已安裝的元件有核取記號表示在 [動作] 清單中。當您按一下 [<strong>移除</strong>時] 核取記號表示會<strong>移除</strong>word 所取代。</td>
    </tr>
    </tbody>
    </table>


6.  按一下 \[**下一步**\] 兩次。

7.  按一下 \[完成\]。


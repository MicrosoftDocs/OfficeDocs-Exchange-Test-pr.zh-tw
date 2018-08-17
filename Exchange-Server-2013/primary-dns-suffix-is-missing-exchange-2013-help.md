﻿---
title: '主要 DNS 尾碼遺漏: Exchange 2013 Help'
TOCTitle: 主要 DNS 尾碼遺漏
ms:assetid: 310765bf-a650-4a3d-a5e4-6173b559d4f6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.fqdnmissing(v=EXCHG.150)
ms:contentKeyID: 61204225
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 主要 DNS 尾碼遺漏

 

_<strong>適用版本：</strong> Exchange Server_

_<strong>上次修改主題的時間：</strong> 2014-01-15_

因為您要在安裝 Exchange 的電腦的主要網域名稱系統 (DNS) 尾碼尚未設定的 Microsoft Exchange Server 2013安裝程式無法繼續執行。

若要解決此問題，請使用下列步驟，在電腦上新增主要 DNS 尾碼，然後重新執行安裝程式。


> [!IMPORTANT]  
> 不支援您安裝 Exchange 2013 後變更主要 DNS 尾碼的電腦名稱。




1.  以您要安裝 Edge Transport role 之電腦上本機系統管理員群組成員的使用者身分登入。

2.  開啟 <strong>\[控制台\]</strong>，然後連按兩下 <strong>\[系統\]</strong>。

3.  在 <strong>\[電腦名稱、網域及工作群組設定\]</strong> 區段中，按一下 <strong>\[變更設定\]</strong>。

4.  在 <strong>\[系統內容\]</strong> 視窗中，確定已選取 <strong>\[電腦名稱\]</strong> 索引標籤，然後按一下 <strong>\[變更...\]</strong>。

5.  在 <strong>\[電腦名稱/網域變更\]</strong> 頁面上，按一下 <strong>\[其他\]</strong>。

6.  在 <strong>\[這部電腦的主要 DNS 尾碼\]</strong> 中，輸入 Edge Transport Server 的 DNS 網域名稱。例如，contoso.com。

7.  按一下 <strong>\[確定\]</strong> 關閉每個視窗。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。


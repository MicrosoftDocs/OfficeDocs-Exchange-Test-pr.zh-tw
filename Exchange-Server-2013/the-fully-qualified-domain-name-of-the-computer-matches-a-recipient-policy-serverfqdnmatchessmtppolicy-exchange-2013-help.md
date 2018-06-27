---
title: '電腦的完整網域名稱比對收件者 policy_ServerFQDNMatchesSMTPPolicy: Exchange 2013 Help'
TOCTitle: 電腦的完整網域名稱比對收件者 policy_ServerFQDNMatchesSMTPPolicy
ms:assetid: f3ea61f8-1788-4cbf-814e-f7c088c1ac47
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.serverfqdnmatchessmtppolicy(v=EXCHG.150)
ms:contentKeyID: 50474583
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 電腦的完整網域名稱比對收件者 policy\_ServerFQDNMatchesSMTPPolicy

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式無法繼續因為完全完整網域名稱 (FQDN) 至本機電腦的比對收件者原則的簡易郵件傳送通訊協定 (SMTP) 位址。

Microsoft Exchange 安裝程式需要 Exchange 組織中的伺服器的 FQDN 不符合相同的 Exchange 組織中的收件者原則的所有 SMTP 地址。

如果電腦的 FQDN 相符的收件者原則的 SMTP 位址，此相符項目可能導致容錯移轉 SMTP 與停滯不前 MTA 佇列中的郵件。

若要解決此問題，重新命名之本機電腦或移除或重新命名的收件者原則並重新執行 Microsoft Exchange 安裝程式。

要重新命名之本機電腦

1.  開啟 \[**控制台**\] 中的 \[**系統**\]。

2.  在 \[電腦名稱\] 索引標籤上，按一下 \[變更\]。

3.  **電腦名稱**\] 底下輸入電腦的新名稱，然後按一下 \[**確定\]**。系統會提示您提供使用者名稱和重新命名網域中的電腦的使用者密碼。

4.  按一下**\[確定\]**以關閉 \[**系統內容**\] 對話方塊。系統會提示您重新啟動電腦以套用變更。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您想要重新命名之電腦的網域控制站，請參閱 「 重新命名的網域控制站&quot;(<a href="https://go.microsoft.com/fwlink/?linkid=66828">https://go.microsoft.com/fwlink/?LinkId=66828</a>)。</td>
</tr>
</tbody>
</table>


若要修改的收件者原則 SMTP 位址

1.  啟動 Exchange 系統管理員。

2.  按一下 \[**組織**\]、 \[**收件者**，和 \[**收件者原則**。

3.  按兩下您想變更的原則。

4.  按一下 \[**電子郵件地址**\] 索引標籤，並變更適當的 SMTP 位址

如需詳細 Recipient 原則命名問題，查看 Microsoft 知識庫文章 288175，"XCON： Recipient 原則不符合組織、 5.4.8 中任何伺服器的 FQDN Ndr"([http://go.microsoft.com/fwlink/?linkid=3052\&kbid=288175](http://go.microsoft.com/fwlink/?linkid=3052%26kbid=288175))。


---
title: '測試 Outlook 無所不在連線: Exchange 2013 Help'
TOCTitle: 測試 Outlook 無所不在連線
ms:assetid: 0dc5b68f-2316-446a-84c9-5f1c50dc3776
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee633453(v=EXCHG.150)
ms:contentKeyID: 50553935
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 測試 Outlook 無所不在連線

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

您可以測試的端對端用戶端Outlook無所不在連線使用介面或 Exchange Remote Connectivity Analyzer （exrca） 這是。這包括測試透過建立使用者設定檔及登入使用者的信箱的自動探索服務的連線。所有必要的值會從自動探索服務來擷取。

如需了解與 Outlook Anywhere 相關的其他管理工作，請參閱 [Outlook 無所不在](outlook-anywhere-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「Outlook Anywhere」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用命令介面測試 Outlook Anywhere 連線

若要使用命令介面測試 Outlook Anywhere 連線，請使用 **Test-OutlookConnectivity** Cmdlet。

執行下列命令。

    Test-OutlookConnectivity -ProbeIdentity 'OutlookMailboxDeepTestProbe' -MailboxId tony@contoso.com -Hostname contoso.com

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>OutlookMailboxDeepTestProbe</em>參數值會測試從信箱伺服器的連線。若要測試從用戶端存取伺服器的連線，請使用<em>OutlookMailboxCTPProbeProbeIdentity</em>參數值。</td>
</tr>
</tbody>
</table>


## 使用 Exchange Remote Connectivity Analyzer 測試 Outlook Anywhere 連線

Exchange Remote Connectivity Analyzer （exrca） 這是設計用於測試與 Exchange 通訊協定各種連線的 web 式工具。您可以存取 exrca 這是[此處](https://go.microsoft.com/fwlink/p/?linkid=167905)。

1.  在 ExRCA 網站上的 \[Microsoft Office Outlook 連線測試\] 下，選取 \[Outlook Anywhere\]，然後在頁面底部選取 \[下一步\]。

2.  在下一個畫面上輸入必要的資訊，包括電子郵件地址、網域、使用者名稱及密碼。

3.  選擇要使用自動探索偵測伺服器設定，或是手動指定伺服器設定。

4.  接受免責聲明，輸入驗證碼，然後選取 \[驗證\]。

5.  選取 \[執行測試\]。

## 如何才能了解這是否正常運作？

Exrca 這是測試完成時，其輸出將會顯示在網頁上。將會列於任何失敗。


---
title: '啟用信箱伺服器上的反垃圾郵件功能: Exchange 2013 Help'
TOCTitle: 啟用信箱伺服器上的反垃圾郵件功能
ms:assetid: 59d22c5e-64bc-4879-8ad1-364862b6ba11
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201691(v=EXCHG.150)
ms:contentKeyID: 50473259
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 啟用信箱伺服器上的反垃圾郵件功能

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-01-23_

在 Microsoft Exchange Server 2013中，信箱伺服器上的傳輸服務可使用下列反垃圾郵件代理程式，但其並非預設安裝：

  - 內容篩選器代理程式

  - 寄件者識別碼代理程式

  - 寄件者篩選器代理程式

  - 寄件者信譽的通訊協定分析代理程式

不過，您可使用 Exchange 管理命令介面中的指令碼安裝這些反垃圾郵件代理程式。一般來說，您只能在組織接受所有內送郵件時，且未經任何反垃圾郵件篩選，信箱伺服器才能安裝反垃圾郵件代理程式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然您可以在 Mailbox Server 上使用收件者篩選代理程式，但是不應該進行設定。Mailbox Server 上的收件者篩選在含有其他有效收件者的郵件中偵測到一個無效或已封鎖收件者時，即會拒絕郵件。雖然預設會啟用收件者篩選代理程式，但是不會將它設定為封鎖任何收件者。如需詳細資訊，請參閱<a href="manage-recipient-filtering-on-edge-transport-servers-exchange-2013-help.md">管理 Edge Transport server 上的收件者篩選</a>。</td>
</tr>
</tbody>
</table>


若您在郵件伺服器的傳輸服務中安裝可用的反垃圾郵件代理程式，但在送達信箱伺服器前，您的郵件也有其他的 Exchange 反垃圾郵件代理程式在作業，這會發生什麼狀況？例如，若您在周邊網路有 Edge Transport Server 會發生什麼狀況？信箱伺服器上的反垃圾郵件代理程式辨識到反垃圾郵件 X-header 值，並由其他反垃圾郵件代理程式新增至郵件，而這些包含 X-header 的郵件未重新掃描即可通過。不過，信箱伺服器會由件者篩選器代理程式再次執行收件者查詢。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：15 分鐘

  - [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「傳輸設定」項目。

  - 無法使用信箱伺服器上的連線篩選代理程式與附件篩選器代理程式。它們只能在 Edge Transport Server 上使用。不過，信箱伺服器已安裝惡意軟體代理程式且預設為啟用。如需相關資訊，請參閱[反惡意程式防護](anti-malware-protection-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 該怎麼做？

## 步驟 1：使用命令介面執行 Install-AntispamAgents.ps1 指令碼

執行下列命令：

    & $env:ExchangeInstallPath\Scripts\Install-AntiSpamAgents.ps1

## 如何才能了解此步驟是否正常運作？

若指令碼執行時未發生錯誤且要求重新啟動 Microsoft Exchange Transport 服務，代表此步驟正常運作。

## 步驟 2：使用命令介面重新開啟 Microsoft Exchange Transport 服務

執行下列命令：

    Restart-Service MSExchangeTransport

## 如何才能了解此步驟是否正常運作？

若 Microsoft Exchange Transport 服務重新開啟時未發生錯誤，代表此步驟正常運作。

## 步驟 3：使用命令介面指定組織的內部 SMTP 伺服器

需要任一內部 SMTP 伺服器的 IP 位址，讓寄件者 ID 代理程式忽略。事實上，您需要至少指定一個內部 SMTP 伺服器的 IP 位址。如果執行反垃圾郵件代理程式的信箱伺服器是組織中唯一的 SMTP 伺服器，請指定該電腦的 IP 位址。

若要在不影響任何現有值的情況下新增內部 SMTP 伺服器的位址，請執行下列命令：

    Set-TransportConfig -InternalSMTPServers @{Add="<ip address1>","<ip address2>"...}

此範例會將內部 SMTP 伺服器位址 10.0.1.10 和 10.0.1.11 新增至組織的傳輸組態。

    Set-TransportConfig -InternalSMTPServers @{Add="10.0.1.10","10.0.1.11"}

## 如何才能了解此步驟是否正常運作？

若要確認是否成功指定至少一個內部 SMTP 伺服器的 IP 位址，請執行下列操作：

1.  執行下列命令：
    
        Get-TransportConfig | Format-List InternalSMTPServers

2.  確認至少一個有效內部 SMTP 伺服器的 IP 位址隨即顯示。


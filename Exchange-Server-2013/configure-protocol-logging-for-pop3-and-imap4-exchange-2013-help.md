---
title: '設定 POP3 與 IMAP4 通訊協定記錄: Exchange 2013 Help'
TOCTitle: 設定 POP3 與 IMAP4 通訊協定記錄
ms:assetid: 451b337b-cb6b-4460-8687-be0b19c469bc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997690(v=EXCHG.150)
ms:contentKeyID: 50553976
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 POP3 與 IMAP4 通訊協定記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-27_

您可以使用命令介面來啟用、 停用或修改通訊協定記錄 POP3 和 IMAP4 設定。根據預設，並未啟用通訊協定記錄。

通訊協定記錄可讓您檢閱Exchange環境中的 POP3 和 IMAP4 連線。這可以是如果您正在進行疑難排解相關 POP3 或 IMAP4 的效能問題。如需詳細資訊，請參閱[POP3 與 IMAP4 通訊協定記錄](protocol-logging-for-pop3-and-imap4-exchange-2013-help.md)。POP3 與 IMAP4 的詳細資訊，請參閱[Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「POP3 設定」和「IMAP4 設定」項目。

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

## 使用命令介面來啟用 POP3 或 IMAP4 的通訊協定記錄

此範例會啟用 Client Access Server CAS01 上的 IMAP4 或 POP3 的通訊協定記錄。

    Set-ImapSettings -Server "CAS01" -ProtocolLogEnabled $true
    Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您是否已變更的 POP3 或 IMAP4 通訊協定記錄設定之後，您必須重新啟動無論您正在使用的服務： POP3 或 IMAP4。如需如何重新啟動 POP3 與 IMAP4 服務的資訊，請參閱<a href="start-and-stop-the-pop3-services-exchange-2013-help.md">啟動及停止 [POP3 服務</a>和<a href="start-and-stop-the-imap4-services-exchange-2013-help.md">啟動及停止 IMAP4 服務</a>。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [Set-ImapSettings](https://technet.microsoft.com/zh-tw/library/aa998252\(v=exchg.150\)) 與 [Set-PopSettings](https://technet.microsoft.com/zh-tw/library/aa997154\(v=exchg.150\))。

## 使用命令介面來停用 POP3 或 IMAP4 的通訊協定記錄

此範例會停用 Client Access Server CAS01 上的 IMAP4 或 POP3 的通訊協定記錄。

    Set-ImapSettings -Server "CAS01" -protocolLogEnabled $false
    Set-PopSettings -Server "CAS01" -protocolLogEnabled $false

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您是否已變更的 POP3 或 IMAP4 通訊協定記錄設定之後，您必須重新啟動無論您正在使用的服務： POP3 或 IMAP4。如需如何重新啟動 POP3 與 IMAP4 服務的資訊，請參閱<a href="start-and-stop-the-pop3-services-exchange-2013-help.md">啟動及停止 [POP3 服務</a>和<a href="start-and-stop-the-imap4-services-exchange-2013-help.md">啟動及停止 IMAP4 服務</a>。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [Set-ImapSettings](https://technet.microsoft.com/zh-tw/library/aa998252\(v=exchg.150\)) 與 [Set-PopSettings](https://technet.microsoft.com/zh-tw/library/aa997154\(v=exchg.150\))。

## 使用命令介面來修改 POP3 或 IMAP4 的通訊協定記錄

若要修改 POP3 或 IMAP4 記錄設定，請執行 **Set-ImapSettings** 或 **Set-PopSettings** Cmdlet 搭配一或多個下列參數。

  - *LogFileLocation*  此參數會指定 POP3 或 IMAP4 通訊協定記錄檔的位置。根據預設，POP3 通訊協定記錄檔位於 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Logging\\Pop3 目錄中。本範例會啟用 POP3 通訊協定記錄在 Client Access server CAS01 上。它也會變更記錄 C:\\Pop3Logging 目錄將 POP3 通訊協定。
    
        Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true -LogFileLocation "C:\Pop3Logging"

  - *LogFileRollOverSettings*  此參數會定義 POP3 或 IMAP4 通訊協定記錄建立新的記錄檔的頻率。根據預設，新的記錄檔會建立每一天。可能的值為：
    
    每小時
    
    每日
    
    每週
    
    每月
    
    此設定會套用只時*LogPerFileSizeQuota*參數的值設為零。此範例會變更登入的用戶端存取伺服器 CAS01 為每小時建立新的記錄檔將 POP3 通訊協定。
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 0 -LogFileRollOverSettings Hourly

  - *LogPerFileSizeQuota*  此參數會定義 POP3 或 IMAP4 通訊協定記錄檔的大小上限 （位元組）。根據預設，這個值設為零。當此值設為零時，會將新的通訊協定記錄檔建立好*LogFileRollOverSettings*參數所指定的頻率。
    
    此範例會將 Client Access Server CAS01 上的 POP3 通訊協定記錄變更為在記錄檔達到 2 MB 時建立新的記錄檔。
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 2000000
    
    此範例會將 Client Access Server CAS01 上的 POP3 通訊協定記錄變更為使用相同記錄檔，不論其建立日期與大小為何。
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota unlimited

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您是否已變更的 POP3 或 IMAP4 通訊協定記錄設定之後，您必須重新啟動無論您正在使用的服務： POP3 或 IMAP4。如需如何重新啟動 POP3 與 IMAP4 服務的資訊，請參閱<a href="start-and-stop-the-pop3-services-exchange-2013-help.md">啟動及停止 [POP3 服務</a>和<a href="start-and-stop-the-imap4-services-exchange-2013-help.md">啟動及停止 IMAP4 服務</a>。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [Set-ImapSettings](https://technet.microsoft.com/zh-tw/library/aa998252\(v=exchg.150\)) 與 [Set-PopSettings](https://technet.microsoft.com/zh-tw/library/aa997154\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認 POP3 通訊協定記錄設定的命令介面中執行下列命令。如果已啟用 POP3 通訊協定記錄、 *ProtocolLogEnabled*參數的值為`True`。若停用 POP3 通訊協定記錄時，此值為`False`。您可確定*LogFileLocation*、 *LogPerFileSizeQuota*、 值和*LogFileRollOverSettings*參數正確無誤。

    Get-PopSettings | format-list

若要確認 IMAP4 通訊協定記錄設定的命令介面中執行下列命令。如果已啟用 IMAP4 通訊協定記錄、 *ProtocolLogEnabled*參數的值為`True`。若停用 IMAP4 通訊協定記錄時，此值為`False`。您可確定*LogFileLocation*、 *LogPerFileSizeQuota*、 值和*LogFileRollOverSettings*參數正確無誤。

    Get-ImapSettings | format-list

## 相關資訊

在您設定 POP3 和 IMAP4 的通訊協定記錄之後，您還可以：

[啟動及停止 IMAP4 服務](start-and-stop-the-imap4-services-exchange-2013-help.md)

[啟動及停止 \[POP3 服務](start-and-stop-the-pop3-services-exchange-2013-help.md)


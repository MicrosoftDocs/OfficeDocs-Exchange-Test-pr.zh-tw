---
title: '允許使用者在 Outlook Web App 中檢視 POP3、IMAP4 及 SMTP 伺服器設定: Exchange 2013 Help'
TOCTitle: 允許使用者在 Outlook Web App 中檢視 POP3、IMAP4 及 SMTP 伺服器設定
ms:assetid: bd22bf7e-3bf7-45e6-8790-919b780166f6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg298947(v=EXCHG.150)
ms:contentKeyID: 50554089
ms.date: 01/12/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 允許使用者在 Outlook Web App 中檢視 POP3、IMAP4 及 SMTP 伺服器設定

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-28_

如果您有使用 POP3 或 IMAP4 連線至其 MicrosoftExchange Server 2013 信箱的使用者，他們必須知道正確的伺服器設定才能順利連線。完成預設的 Exchange 2013 安裝之後，您的使用者就無法查詢他們自己的傳入 POP3 或 IMAP4 伺服器設定或傳出 SMTP 伺服器設定。但是，您可以設定 Exchange，讓使用者能使用 MicrosoftOutlook Web App 查詢自己的設定。

執行這些程序後，您的使用者便可在 Outlook Web App 中查詢其伺服器設定，如下所示：

1.  在 Outlook Web App 中，按一下 \[設定\] \> \[選項\]。

2.  在 \[選項\] 中，按一下 \[帳戶\] \> \[我的帳戶\] \> \[POP 或 IMAP 存取的設定\]。

如需 POP3 與 IMAP4 的詳細資訊，請參閱 [Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

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

## 使用命令介面允許 POP3 和 IMAP4 使用者在 Outlook Web App 中檢視其傳入 POP3 和 IMAP4 設定

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md) 主題中的「POP3 設定」與「IMAP4 設定」項目。

此範例可允許使用者檢視外部 POP3 伺服器設定。

    Set-PopSettings -ExternalConnectionSettings {Dublin01.Contoso.com:995:SSL}

如需詳細的語法及參數資訊，請參閱 [Set-PopSettings](https://technet.microsoft.com/zh-tw/library/aa997154\(v=exchg.150\))。

此範例可允許使用者檢視外部 IMAP4 伺服器設定。

    Set-ImapSettings -ExternalConnectionSettings {Dublin01.Contoso.com:993:SSL}

如需詳細的語法及參數資訊，請參閱 [Set-ImapSettings](https://technet.microsoft.com/zh-tw/library/aa998252\(v=exchg.150\))。

若要套用這些變更，您必須重新啟動 IIS。您不需要重新啟動 POP3 服務。若要重新啟動 IIS，請在命令提示字元中輸入下列命令：

    iisreset

## 如何知道這是否正常運作？

若要驗證您是否已設定好 Exchange 以允許使用者檢視其 POP3 伺服器設定：

1.  在命令介面中執行下列命令。
    
        Get-PopSettings | format-list

2.  確認已設定了 *ExternalConnectionSettings* 內容。

若要驗證您是否已設定好 Exchange 以允許使用者檢視其 IMAP4 伺服器設定：

1.  在命令介面中執行下列命令。
    
        Get-ImapSettings | format-list

2.  確認已設定了 *ExternalConnectionSettings* 內容。

## 使用命令介面允許 POP3 和 IMAP4 使用者在 Outlook Web App 中檢視其傳出 SMTP 設定

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[郵件流程權限](mail-flow-permissions-exchange-2013-help.md) 主題中的「接收連接器」項目。

此範例可允許使用者利用 Outlook Web App 檢視內部和外部 SMTP 伺服器設定。

    Get-ReceiveConnector "*Client Frontend*" | Set-ReceiveConnector -Fqdn Server.Contoso.com -AdvertiseClientSettings $true 

如需詳細的語法及參數資訊，請參閱 [Set-ReceiveConnector](https://technet.microsoft.com/zh-tw/library/bb125140\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要驗證您是否已設定好 Exchange 以允許使用者檢視其 SMTP 伺服器設定：

1.  在命令介面中執行下列命令。
    
        Get-ReceiveConnector | format-list

2.  如果 *AdvertiseClientSettings* 內容設為 `true`，使用者就能檢視在 Outlook Web App 中檢視其 SMTP 伺服器設定。如果 *AdvertiseClientSettings* 設為 `false`，則使用者無法檢視在 Outlook Web App 中檢視其 SMTP 伺服器設定。

## 相關資訊

讓使用者可以檢視其 POP3、IMAP4 和 SMTP 設定之後，您還可以：

[啟用或停用使用者的 POP3 存取](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[啟用或停用使用者的 IMAP4 存取](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)


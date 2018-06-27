---
title: '設定 IP 位址和 POP3 和 IMAP4 存取的連接埠: Exchange 2013 Help'
TOCTitle: 設定 IP 位址和 POP3 和 IMAP4 存取的連接埠
ms:assetid: 8292747b-6626-4d7f-ba73-1e17f5d99fa4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123530(v=EXCHG.150)
ms:contentKeyID: 50554020
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 IP 位址和 POP3 和 IMAP4 存取的連接埠

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-28_

您可以使用 EAC 與命令介面來設定Microsoft Exchange POP3 和 IMAP4 服務使用的 IP 位址和與預設設定不同的連接埠。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>輸入 IP 位址和 IP 位址範圍中的網際網路通訊協定第 4 版 (IPv4) 格式、 網際網路通訊協定第 6 版 (IPv6) 格式或這兩種格式。Windows Server 2008的預設安裝可讓支援 IPv4 和 IPv6。</td>
</tr>
</tbody>
</table>


如需 POP3 與 IMAP4 的詳細資訊，請參閱 [Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

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

## 為 POP3 設定的 IP 位址和連接埠

## 使用 EAC 來設定的 IP 位址和連接埠進行 POP3

1.  在 EAC 中，瀏覽至 \[伺服器\]**\>** \[伺服器\]。

2.  在伺服器清單中選取 Client Access Server，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在伺服器內容頁面上，按一下 \[POP3\]。

4.  **TLS 或未加密的連線**，請按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

5.  在 \[**新增 IP 位址**\] 頁面上的 \[ **IP 位址**\] 中，選擇下列其中一項：
    
      - **所有可用的 IPv4 位址**  使用所有可用的 IPv4 IP 位址的伺服器。
    
      - **所有可用的 IPv6 位址**  使用所有可用的 IPv6 IP 位址的伺服器。
    
      - **指定 IP 位址**  使用特定的 IP 位址。

6.  **連接埠**下, 輸入連接埠號碼，或接受預設的連接埠。

7.  按一下 **\[儲存\]** 以儲存變更。

您已設定 POP3 的 IP 位址和連接埠設定之後，您必須重新啟動 POP3 服務的設定才會生效。如需如何重新啟動 POP3 服務的資訊，請參閱[啟動及停止 \[POP3 服務](start-and-stop-the-pop3-services-exchange-2013-help.md)。

## 使用命令介面設定 IP 位址和連接埠進行 POP3

本範例會設定的 IP 位址及連接埠進行通訊的Exchange使用 POP3 使用 Secure Sockets Layer (SSL)。

    Set-PopSettings -SSLBindings: IPaddress:Port

本範例會設定的 IP 位址及連接埠進行通訊的Exchange使用 POP3 未加密或傳輸層安全性 (TLS) 加密。

    Set-PopSettings -UnencryptedOrTLSBindings IPaddress:Port

您已設定 POP3 的 IP 位址和連接埠設定之後，您必須重新啟動 POP3 服務的設定才會生效。如需如何重新啟動 POP3 服務的資訊，請參閱[啟動及停止 \[POP3 服務](start-and-stop-the-pop3-services-exchange-2013-help.md)。

如需語法及參數的相關資訊，請參閱 [Set-PopSettings](https://technet.microsoft.com/zh-tw/library/aa997154\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

請執行下列 cmdlet 以確認您已變更的伺服器上的 POP3 IP 位址和連接埠設定。

1.  在命令介面中執行下列命令。
    
        Get-PopSettings | format-list

2.  確認*UnencryptedOrTLSBindings* \] 及 \[ *SSLBindings*設定正確。

## IMAP4 設定的 IP 位址和連接埠

## 使用 EAC 來設定 IMAP4 的 IP 位址和連接埠

1.  在 EAC 中，瀏覽至 \[伺服器\]**\>** \[伺服器\]。

2.  在伺服器清單中選取 Client Access Server，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在伺服器內容頁面上，按一下 \[IMAP4\]。

4.  如果您想要設定 TLS 或未加密的連線設定\] 的 \[ **TLS 或未加密的連線**，請按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。如果您想要變更 Secure Sockets Layer (SSL) 連線設定， **Secure Sockets Layer (SSL) 連線**\] 下按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

5.  在 \[**新增 IP 位址**\] 頁面上的 \[ **IP 位址**\] 中，選擇下列其中一項：
    
      - **所有可用的 IPv4 位址**  使用所有可用的 IPv4 IP 位址的伺服器。
    
      - **所有可用的 IPv6 位址**  使用所有可用的 IPv6 IP 位址的伺服器。
    
      - **指定 IP 位址**  使用特定的 IP 位址。

6.  **連接埠**下, 輸入連接埠號碼，或接受預設的連接埠。

7.  按一下 **\[儲存\]** 以儲存變更。

您已設定 IMAP4 的 IP 位址和連接埠設定之後，您必須重新啟動 IMAP4 服務的設定才會生效。如需如何重新啟動 IMAP4 服務的資訊，請參閱[啟動及停止 IMAP4 服務](start-and-stop-the-imap4-services-exchange-2013-help.md)。

## 使用命令介面來設定 IMAP4 的 IP 位址和連接埠

本範例會設定的 IP 位址及連接埠進行通訊的Exchange使用 IMAP4。

    Set-ImapSettings -SSLBindings: IPaddress:Port

本範例會設定的 IP 位址及連接埠進行通訊的Exchange使用 IMAP4 未加密或 TLS 加密。

    Set-ImapSettings -UnencryptedOrTLSBindings IPaddress:Port 

您已設定 IMAP4 的 IP 位址和連接埠設定之後，您必須重新啟動 IMAP4 服務的設定才會生效。如需如何重新啟動 IMAP4 服務的資訊，請參閱[啟動及停止 IMAP4 服務](start-and-stop-the-imap4-services-exchange-2013-help.md)。

如需語法及參數的相關資訊，請參閱 [Set-ImapSettings](https://technet.microsoft.com/zh-tw/library/aa998252\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

請執行下列 cmdlet 以確認您已變更的伺服器上的 IMAP4 IP 位址和連接埠設定。

1.  在命令介面中執行下列命令。
    
        Get-ImapSettings | format-list

2.  確認*UnencryptedOrTLSBindings* \] 及 \[ *SSLBindings*設定正確。

## 相關資訊

POP3 和 IMAP4 設定的 IP 位址和連接埠之後，您可能也想要：

[啟用 Exchange 2016 的 IMAP4](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[在 Exchange 2013 中啟用 POP3](enable-pop3-in-exchange-2013-exchange-2013-help.md)


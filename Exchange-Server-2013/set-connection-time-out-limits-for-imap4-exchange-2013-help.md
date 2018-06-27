---
title: '設定 IMAP4 的連線逾時限制: Exchange 2013 Help'
TOCTitle: 設定 IMAP4 的連線逾時限制
ms:assetid: 6b6a5bd1-a878-4a70-8e21-14d5042a58f1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998665(v=EXCHG.150)
ms:contentKeyID: 50554004
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 IMAP4 的連線逾時限制

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-28_

您可以使用 EAC 或命令介面為閒置中已驗證及未驗證的 IMAP4 連線設定連線逾時限制。

如需 IMAP4 的詳細資訊，請參閱 [Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「IMAP4 設定」項目。

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

## 使用 EAC 設定 IMAP4 的連線逾時限制

1.  在 EAC 中，瀏覽至 \[伺服器\]**\>** \[伺服器\]。

2.  在伺服器清單中選取 Client Access Server，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在伺服器內容頁面上，按一下 \[IMAP4\]。

4.  向下捲動並按一下 \[更多選項\]。

5.  在 \[逾時設定\] 下方，使用下列設定：
    
      - **驗證逾時 （秒）**   指定關閉閒置的已驗證的連線前所等待的時間。預設值為 1800。可能的值為介於 30 到 86,400。
    
      - **未經過驗證的逾時 （秒）**  指定關閉未驗證的閒置連線前所等待的時間。預設值為 60。可能的值是來自至 3600 30。

6.  按一下 \[套用\]，然後按一下 \[確定\] 以儲存變更。

您已設定連線逾時限制 IMAP4 之後，您必須重新啟動 IMAP4 服務的設定才會生效。如需如何重新啟動 IMAP4 服務的資訊，請參閱[啟動及停止 IMAP4 服務](start-and-stop-the-imap4-services-exchange-2013-help.md)。

## 使用命令介面設定 IMAP4 的連線逾時限制

此範例會為閒置中的已驗證連線設定連線逾時限制。

    Set -ImapSettings -Identity CAS01 -AuthenticatedConnectionTimeout TimeValue

此範例會為閒置中的未驗證連線設定連線逾時限制。

    Set -ImapSettings -Identity CAS01 -PreAuthenticatedConnectionTimeout TimeValue

您已設定連線逾時限制 IMAP4 之後，您必須重新啟動 IMAP4 服務的設定才會生效。如需如何重新啟動 IMAP4 服務的資訊，請參閱[啟動及停止 IMAP4 服務](start-and-stop-the-imap4-services-exchange-2013-help.md)。

如需語法及參數的詳細資訊，請參閱 [Set-ImapSettings](https://technet.microsoft.com/zh-tw/library/aa998252\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認是否已成功設定連線限制，請執行下列其中一項操作：

1.  在 EAC 中，瀏覽至 \[伺服器\]**\>** \[伺服器\]。

2.  在伺服器清單中選取 Client Access Server，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在伺服器內容頁面上，按一下 \[IMAP4\]。

4.  向下捲動並按一下 \[更多選項\]。

5.  在 \[逾時設定\] 下方，驗證連線設定是否正確。

或

1.  在命令介面中執行下列命令。
    
        Get-ImapSettings | format-list

2.  驗證連線設定是否正確。

## 相關資訊

在您爲 IMAP4 設定驗證逾時限制之後，您可能還想要：

[啟用 Exchange 2016 的 IMAP4](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[設定 IMAP4 的連線限制](set-connection-limits-for-imap4-exchange-2013-help.md)


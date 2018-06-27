---
title: '設定 POP3 和 IMAP4 訊息擷取格式選項: Exchange 2013 Help'
TOCTitle: 設定 POP3 和 IMAP4 訊息擷取格式選項
ms:assetid: 481096e0-4492-46c2-8ca8-bdf84a84531e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997869(v=EXCHG.150)
ms:contentKeyID: 50553979
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 POP3 和 IMAP4 訊息擷取格式選項

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

您可以設定連線至電子郵件使用 POP3 和 IMAP4 使用者的訊息擷取格式。郵件擷取選項可以使用 EAC 或命令介面中的伺服器層級設定以及可以在使用者層級使用命令介面設定。

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

## 在伺服器層級設定 POP3 郵件擷取格式

## 在伺服器層級使用 EAC 設定 POP3 郵件擷取格式

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  在伺服器清單中選取 Client Access Server，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在伺服器內容頁面上，按一下 \[POP3\]。

4.  在 \[郵件 MIME 格式\] 底下，從下列設定中選擇：
    
      - 文字
    
      - HTML
    
      - HTML 及替代文字
    
      - 豐富型文字
    
      - 豐富型文字及替代文字
    
      - 最佳內文格式
    
      - TNEF

5.  按一下 \[儲存\]。

您已設定郵件的 POP3 擷取格式設定後，您必須重新啟動 POP3 服務的設定才會生效。如需如何重新啟動 \[POP3 服務的資訊，請參閱[啟動及停止 \[POP3 服務](start-and-stop-the-pop3-services-exchange-2013-help.md)。

## 在伺服器層級使用命令介面設定 POP3 郵件擷取格式

此範例針對伺服器 CAS01 上的所有 POP3 使用者將郵件擷取格式選項設定為僅限文字。

    Set-PopSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly

您可以選擇下列設定值。您可以使用的數值或文字字串來指定*MessageRetrievalMimeFormat*參數的值。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>郵件格式</strong></p></td>
<td><p><strong>值</strong></p></td>
</tr>
<tr class="even">
<td><p>文字</p></td>
<td><p><code>0</code> 或 <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> 或 <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML 及替代文字</p></td>
<td><p><code>2</code> 或 <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>豐富型文字</p></td>
<td><p><code>3</code>或<code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>豐富型文字及替代文字</p></td>
<td><p><code>4</code> 或 <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>最佳內文格式</p></td>
<td><p><code>5</code> 或 <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> 或 <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


您已設定郵件的 POP3 擷取格式設定後，您必須重新啟動 POP3 服務的設定才會生效。如需如何重新啟動 \[POP3 服務的資訊，請參閱[啟動及停止 \[POP3 服務](start-and-stop-the-pop3-services-exchange-2013-help.md)。

如需語法及參數的相關資訊，請參閱 [Set-PopSettings](https://technet.microsoft.com/zh-tw/library/aa997154\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

執行下列動作以驗證您已成功在伺服器上設定 POP3 郵件擷取設定。

1.  在命令介面中執行下列命令。
    
        Get-PopSettings | format-list

2.  驗證 *MessageRetrievalMimeFormat* 設定是否正確。

## 在伺服器層級設定 IMAP4 郵件擷取格式

## 在伺服器層級使用 EAC 設定 IMAP4 郵件擷取格式

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  在伺服器清單中選取 Client Access Server，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在伺服器內容頁面上，按一下 \[IMAP4\]。

4.  在 \[郵件 MIME 格式\] 底下，從下列設定中選擇：
    
      - 文字
    
      - HTML
    
      - HTML 及替代文字
    
      - 豐富型文字
    
      - 豐富型文字及替代文字
    
      - 最佳內文格式
    
      - TNEF

5.  按一下 \[儲存\]。

您已設定的郵件擷取格式設定 IMAP4 的之後，您必須重新啟動 IMAP4 服務的設定才會生效。如需如何重新啟動 IMAP4 服務的資訊，請參閱[啟動及停止 IMAP4 服務](start-and-stop-the-imap4-services-exchange-2013-help.md)。

## 在伺服器層級使用命令介面設定 IMAP4 郵件擷取格式

此範例針對伺服器 CAS01 上的所有 IMAP4 使用者將郵件擷取格式選項設定為僅限文字。

    Set-ImapSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly

您可以選擇下列設定值。您可以使用的數值或文字字串來指定*MessageRetrievalMimeFormat*參數的值。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>郵件格式</strong></p></td>
<td><p><strong>值</strong></p></td>
</tr>
<tr class="even">
<td><p>文字</p></td>
<td><p><code>0</code> 或 <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> 或 <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML 及替代文字</p></td>
<td><p><code>2</code> 或 <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>豐富型文字</p></td>
<td><p><code>3</code>或<code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>豐富型文字及替代文字</p></td>
<td><p><code>4</code> 或 <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>最佳內文格式</p></td>
<td><p><code>5</code> 或 <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> 或 <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


您已設定的郵件擷取格式設定 IMAP4 的之後，您必須重新啟動 IMAP4 服務的設定才會生效。如需如何重新啟動 IMAP4 服務的資訊，請參閱[啟動及停止 IMAP4 服務](start-and-stop-the-imap4-services-exchange-2013-help.md)。

如需語法及參數的相關資訊，請參閱 [Set-ImapSettings](https://technet.microsoft.com/zh-tw/library/aa998252\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

執行下列動作以驗證您已成功在伺服器上設定 IMAP4 郵件擷取設定。

1.  在命令介面中執行下列命令。
    
        Get-ImapSettings | format-list

2.  驗證 *MessageRetrievalMimeFormat* 設定是否正確。

## 為使用者設定 POP3 郵件擷取格式

## 使用命令介面設定使用者的 POP3 郵件擷取格式

此範例會為 `USER01` 將 POP3 存取的郵件擷取格式設定為僅限文字。

    Set-CASMailbox -Identity USER01 -PopMessagesRetrievalMimeFormat TextOnly

您可以選擇下列設定值。您可以使用的數值或文字字串來指定*PopMessagesRetrievalMimeFormat*參數的值。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>郵件格式</strong></p></td>
<td><p><strong>值</strong></p></td>
</tr>
<tr class="even">
<td><p>文字</p></td>
<td><p><code>0</code> 或 <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> 或 <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML 及替代文字</p></td>
<td><p><code>2</code> 或 <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>豐富型文字</p></td>
<td><p><code>3</code>或<code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>豐富型文字及替代文字</p></td>
<td><p><code>4</code> 或 <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>最佳內文格式</p></td>
<td><p><code>5</code> 或 <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> 或 <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


您已設定郵件的 POP3 擷取格式設定後，您必須重新啟動 POP3 服務的設定才會生效。如需如何重新啟動 \[POP3 服務的資訊，請參閱[啟動及停止 \[POP3 服務](start-and-stop-the-pop3-services-exchange-2013-help.md)。

如需語法及參數的相關資訊，請參閱 [Set-CASMailbox](https://technet.microsoft.com/zh-tw/library/bb125264\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

執行下列動作以驗證您已成功為使用者設定 POP3 郵件擷取格式選項。

1.  在命令介面中執行下列命令。
    
        Get-CAS Mailbox <identity> | format-list

2.  驗證 *PopMessagesRetrievalMimeFormat* 的值是否正確。

## 為使用者設定 IMAP4 郵件擷取格式

## 使用命令介面設定使用者的 IMAP4 郵件擷取格式

此範例會為 `USER01` 將 IMAP4 存取的郵件擷取格式設定為僅限文字。

    Set-CASMailbox -Identity USER01 -ImapMessagesRetrievalMimeFormat TextOnly

您可以使用數值或文字字串，指定 *ImapMessagesRetrievalMimeFormat* 參數的值。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>郵件格式</strong></p></td>
<td><p><strong>值</strong></p></td>
</tr>
<tr class="even">
<td><p>文字</p></td>
<td><p><code>0</code> 或 <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> 或 <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML 及替代文字</p></td>
<td><p><code>2</code> 或 <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>豐富型文字</p></td>
<td><p><code>3</code>或<code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>豐富型文字及替代文字</p></td>
<td><p><code>4</code> 或 <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>最佳內文格式</p></td>
<td><p><code>5</code> 或 <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> 或 <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


您已設定的郵件擷取格式設定 IMAP4 的之後，您必須重新啟動 IMAP4 服務的設定才會生效。如需如何重新啟動 IMAP4 服務的資訊，請參閱[啟動及停止 IMAP4 服務](start-and-stop-the-imap4-services-exchange-2013-help.md)。

如需語法及參數的相關資訊，請參閱 [Set-CASMailbox](https://technet.microsoft.com/zh-tw/library/bb125264\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

執行下列動作以驗證您已成功為使用者設定 IMAP4 郵件擷取格式選項。

1.  在命令介面中執行下列命令。
    
        Get-CAS Mailbox <identity> | format-list

2.  驗證 *ImapMessagesRetrievalMimeFormat* 的值是否正確。

## 相關資訊

在您為 IMAP4 和 POP3 使用者設定訊息擷取格式之後，您可能還想要：

[啟用或停用使用者的 POP3 存取](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[啟用或停用使用者的 IMAP4 存取](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

[設定 IMAP4 的行事曆選項](configure-calendar-options-for-imap4-exchange-2013-help.md)

[設定 POP3 行事曆選項](configure-calendar-options-for-pop3-exchange-2013-help.md)


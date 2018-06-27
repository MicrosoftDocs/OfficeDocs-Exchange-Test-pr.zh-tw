---
title: '內容轉換追蹤: Exchange 2013 Help'
TOCTitle: 內容轉換追蹤
ms:assetid: eb9c7df2-9093-49f9-aa4f-044909bd2225
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb397226(v=EXCHG.150)
ms:contentKeyID: 50474523
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 內容轉換追蹤

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-09-25_

內容轉換追蹤會擷取 Microsoft Exchange Server 2013 信箱伺服器上，信箱傳輸服務對輸入與輸出郵件執行之 MAPI 內容轉換中的失敗。

在信箱伺服器上的信箱傳輸服務負責傳送到與信箱收件者的郵件內容轉換。尤其是信箱傳輸提交服務會從信箱使用者從 MAPI MIME 轉換外寄郵件。Mailbox Transport 傳遞服務會將信箱使用者的輸入的郵件從 MIME 轉換成 MAPI。內容轉換追蹤負責擷取這些 MAPI 轉換失敗率。

在信箱伺服器上的傳輸服務中分類程式負責傳送給外部收件者的所有訊息內容轉換。內容轉換追蹤不會擷取內容轉換失敗的傳輸服務中分類程式遇到當它會將郵件傳送給外部收件者的轉換。

**目錄**

Configure content conversion tracing

How content conversion tracing works

Considerations for content conversion tracing

## 設定內容轉換追蹤

內容轉換追蹤由 Exchange 管理命令介面的 **Set-TransportService** 和 **Set-MailboxTransportService** Cmdlet 中的下列參數所控制：

  - *ContentConversionTracingEnabled*  此參數會啟用或停用在 Mailbox server 上的傳輸服務或 Mailbox server 上的信箱傳輸服務中的內容轉換追蹤。此參數的有效值為`$true`和`$false`。預設值為`$false`。如果您的 Exchange 組織包含多個信箱伺服器，您必須啟用每個信箱伺服器上的內容轉換追蹤。

  - *PipelineTracingPath*  雖然此參數相關聯管線追蹤，也會指定內容轉換追蹤檔案的根目錄位置。傳輸服務中的預設位置是`%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`。信箱傳輸服務中的預設位置是`%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`。路徑必須是本機 Exchange 的電腦。

內容轉換會建立名為`ContentConversionTracing`*PipelineTracingPath*參數所指定的路徑中的資料夾。內容轉換`ContentConversionTracing` \] 資料夾中建立兩個子資料夾： `InboundFailures`和`OutboundFailures`。`InboundFailures`資料夾包含從內送的郵件內容轉換失敗的資訊。`OutboundFailures`資料夾包含外寄郵件內容轉換失敗的資訊。

`InboundFailures`或`OutboundFailures`資料夾中的所有檔案的大小上限為 128 mb (MB)。內容轉換追蹤不會使用循環記錄來移除舊的保留時間下限或的檔案大小為基礎的檔案。一旦達到資料夾的大小上限，內容轉換追蹤停駐點的資料夾的寫入資訊。如果您想要確保未超過最大資料夾大小限制，您可以建立排定的工作會定期將內容轉換追蹤檔案移至不同的位置。

內容轉換追蹤使用之資料夾與子資料夾所需的權限如下：

  - 系統管理員：完全控制

  - 網路服務：完全控制

  - 系統：完全控制

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>內容轉換追蹤複製完整的電子郵件的內容。若要避免不想要機密資訊的揭露，您需要設定適當的安全性權限的內容轉換位置追蹤檔案。</td>
</tr>
</tbody>
</table>


回到頁首

## 內容轉換追蹤的運作方式

當內送郵件內容轉換失敗時，請傳遞狀態通知 (DSN) 具有狀態碼 5.6.0 傳送給郵件寄件者。如果已啟用內容轉換追蹤、 失敗資訊會記錄在時間的 5.6.0 DSN 郵件摘要產生。每個內容轉換錯誤會產生兩個不同的檔案。

在輸入郵件從 MIME 轉換成 MAPI 時所發生的內容轉換錯誤，會在 InboundFailures 資料夾中產生下列兩個檔案：

  - **\<GUID\>.eml**   此檔案包含文字格式的失敗郵件。

  - **\<GUID\>.txt**   此檔案包含例外狀況描述、轉換結果、轉換選項，以及信箱傳輸服務對所有郵件施加的郵件大小限制。

在輸出郵件從 MAPI 轉換成 MIME 時所發生的內容轉換錯誤，會在 OutboundFailures 資料夾中產生下列兩個檔案：

  - **\<GUID\>.msg**   此檔案包含 Microsoft Outlook 郵件格式的失敗郵件。

  - **\<GUID\>.txt**   此檔案包含例外狀況描述、轉換結果，以及轉換選項與儲存區驅動程式對所有郵件施加的郵件大小限制。

版面配置區 \<*GUID*\> 相當於在這兩個檔案名稱。每個內容轉換錯誤會產生不同的 GUID 是使用中的對應的訊息和文字檔案的檔名。範例中的檔案名稱中使用的 GUID 是`038b930e-61fd-4bfd-b9b4-0374c18b73f7`。

回到頁首

## 內容轉換追蹤的考量事項

您可以將保留內容轉換追蹤啟用主動式監控。或者，您可以啟用內容轉換追蹤疑難排解特定的失敗事件。您通常可以重現輸入的內容轉換失敗率所提出的 5.6.0 收件者至 resend 原始郵件的 DSN 郵件。

最常見所輸入的內容轉換失敗率。一些輸入的內容轉換錯誤的原因包括下列：

  - **違規的郵件大小限制**  這些郵件大小限制的信箱傳輸服務以協助防止拒絕服務等攻擊 (DoS) 所加諸。這些郵件限制列示於 \<*GUID*\>.txt 檔案。這些郵件限制包括下列各項：
    
      - **MaxMimeTextHeaderLength**  此限制指定 MIME 標頭中可用的文字字元數目上限。此值為 2000年。
    
      - **MaxMimeSubjectLength**  此限制指定主旨行中可用的文字字元數目上限。此值為 255。
    
      - **MSize**  此限制指定的郵件大小上限。此值為 2147483647 個位元組。
    
      - **MaxMimeRecipients**  此限制指定的收件者\]、 \[副本\] 和 \[密件副本\] 欄位允許的收件者總數。此值為 12288。
    
      - **MaxRecipientPropertyLength**  此限制的收件者的描述中指定可用的文字字元數目上限。此值為 1000年。
    
      - **MaxBodyPartsTotal**  此限制 MIME multipart 郵件中指定可用的郵件部分的數目上限。此值為 250。
    
      - **MaxEmbeddedMessageDepth**  此限制指定在郵件中可以存在的轉寄的郵件數目上限。此值為 30。
    
    若想深入了解信箱伺服器或 Edge Transport Server 上的傳輸服務所使用的可設定郵件大小限制，請參閱[郵件大小限制](message-size-limits-exchange-2013-help.md)。

  - **轉換至會議邀請的內送的 iCalendar 訊息失敗**  RFC 2445 定義 iCalendar 行事曆資料交換的標準為。特定的轉換失敗的原因如下：
    
      - 傳送代理程式使用 iCalendar 的方式不正確。
    
      - Outlook 或 Exchange 行事曆架構不支援 iCalendar 的建構。
    
    寄件者收到 5.6.0 不造成轉換失敗率的 iCalendar DSN 郵件。而是將郵件傳遞搭配附加的.ics 檔案包含 iCalendar 郵件內文。

  - **失敗而造成格式的 MIME 郵件**  來路不明的商業電子郵件或垃圾郵件可能會有格式中的郵件標頭，例如 \[收件者的描述不相符的引號的錯誤。更加較少的格式的 MIME 郵件所造成的失敗視為 bug。

輸出內容轉換失敗率為較不常見比輸入失敗。當發生輸出失敗時，他們通常會造成 Exchange 程式碼錯誤或損毀的郵件內容。

回到頁首


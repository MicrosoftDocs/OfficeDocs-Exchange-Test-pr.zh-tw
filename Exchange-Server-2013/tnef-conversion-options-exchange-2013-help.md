---
title: 'TNEF 轉換選項: Exchange 2013 Help'
TOCTitle: TNEF 轉換選項
ms:assetid: 989a62fc-4bc1-448f-90c8-7c7b56fe1084
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb310786(v=EXCHG.150)
ms:contentKeyID: 52062377
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# TNEF 轉換選項

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

您可以指定 Transport Neutral Encapsulation Format (TNEF) 是否應該保留或移除保留Exchange組織的郵件。TNEF，也稱為Outlook Rtf 格式或Exchange Rtf 格式，是Microsoft-特定格式封裝 MAPI 編製郵件內容。所有版本的MicrosoftOutlook完全了都解 TNEF。Outlook Web App TNEF 轉譯 MAPI 並顯示格式化的郵件。不過，不了解 TNEF 通常會顯示 TNEF 其他電子郵件用戶端被設為 Winmail.dat 或 Win.dat 附件的純文字郵件的郵件。

**目錄**

TNEF conversion options for remote domains

TNEF conversion options for mail users and mail contacts

TNEF conversion options in Outlook

Order of precedence for TNEF conversion options

## 遠端網域的 TNEF 轉換選項

當您設定遠端網域的 TNEF 對話選項時，這些 TNEF 轉換選項套用至所有傳送至該網域的郵件。

  - 針對 Exchange Online 專用，您可以使用 Exchange 系統管理中心 (EAC) 在 \[**郵件流程**設定遠端網域的 TNEF 對話選項 \>**遠端網域**\>**編輯**(![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")) \>**使用 Exchange rtf 格式**。

  - Exchange Online和Exchange 2013，您使用*TnefEnabled*參數**Set-RemoteDomain**指令程式上設定遠端網域的 TNEF 對話選項。

對於組織中的遠端網域，您可以使用下列 TNEF 轉換的組態選項：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>在 EAC 中</th>
<th>在命令介面</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用 TNEF 傳送至遠端網域的所有郵件。</p></td>
<td><p><strong>Always</strong></p></td>
<td><p><code>$true</code></p></td>
</tr>
<tr class="even">
<td><p>永遠不使用 TNEF 任何郵件傳送給遠端網域。</p></td>
<td><p><strong>Never</strong></p></td>
<td><p><code>$false</code></p></td>
</tr>
<tr class="odd">
<td><p>TNEF 郵件未特別允許或避免遠端網域中的收件者。是否 TNEF 郵件傳送給遠端網域中的收件者取決於上的郵件連絡人或郵件使用者的特定設定或寄件者在 Outlook 中所指定的設定。此為預設值。</p></td>
<td><p><strong>請遵循使用者設定</strong></p></td>
<td><p><code>$null</code>（空白）</p></td>
</tr>
</tbody>
</table>


如需遠端網域的詳細資訊，請參閱[遠端網域](remote-domains-exchange-2013-help.md)或[Exchange Online 中的遠端網域](https://technet.microsoft.com/zh-tw/library/jj966211\(v=exchg.150\))。

回到頁首

## 郵件使用者和郵件連絡人的 TNEF 轉換選項

當您設定郵件連絡人或郵件使用者的 TNEF 轉換選項時，這些 TNEF 轉換選項會套用到傳送至該特定收件者的所有郵件。 您可以使用 **Set-MailUser** 和 **Set-MailContact**指令程式的 *UseMapiRichTextFormat* 參數，設定郵件連絡人和郵件使用者的 TNEF 轉換選項。

如果是組織中的郵件連絡人和郵件使用者，您有下列 TNEF 轉換的組態選項：

  - **永遠**   對傳送給收件者的所有郵件使用 TNEF。 *UseMapiRichTextFormat* 參數的對應值是 `Always`。

  - **永不**   對傳送給收件者的任何郵件，永不使用 TNEF。 *UseMapiRichTextFormat* 參數的對應值是 `Never`。

  - **使用預設設定**  TNEF 郵件未特別允許或不讓郵件使用者或郵件連絡人。是否 TNEF 郵件傳送給收件者取決於對應的遠端網域的特定設定或寄件者在 Outlook 中所指定的設定。對應*UseMapiRichTextFormat*參數的值是`UseDefaultSettings`。這是預設設定。

回到頁首

## Outlook 中的 TNEF 轉換選項

寄件者可以控制 TNEF 郵件傳送至 Exchange 組織之外的所有收件者的預設 TNEF 郵件對話選項。這些選項會呼叫*網際網路郵件格式*選項。用於遠端收件者，而不適用於 Exchange 組織中的收件者，僅適用於選項。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>下列選項定義將包含 Outlook RTF 的郵件傳送給外部收件者時，如何處理這些郵件。 如果使用的郵件格式為 HTML 或純文字，則這些設定不適用。</td>
</tr>
</tbody>
</table>


在 Outlook 中有下列 TNEF 轉換選項：

  - **轉換成 HTML 格式**   此為預設選項。 傳送給遠端收件者的任何 TNEF 郵件都會轉換成 HTML。 郵件的任何格式應該都會極為接近原始郵件。 許多 (並非全部) 電子郵件用戶端都支援 MIME 編碼的 HTML 郵件。

  - **轉換成純文字格式**   傳送給遠端收件者的任何 TNEF 郵件都會轉換成純文字。 將失去郵件中的任何格式。

  - **使用 Outlook RTF 格式傳送**   傳送給遠端收件者的任何 TNEF 郵件仍然為 TNEF 郵件。

您可在 Outlook 的下列位置設定這些選項：

  - **Outlook 2010 或 Outlook 2013**   **檔案** \> **選項** \> **郵件** \> **郵件格式**。

  - **Outlook 2007**   **工具** \> **選項** \> **郵件格式** \> **網際網路格式**。

寄件者也可以控制 TNEF 郵件傳送至 Exchange 組織外的特定收件者的預設 TNEF 郵件對話選項。這些選項會呼叫*網際網路收件者的郵件格式*選項。選項僅適用於遠端儲存在 \[連絡人\] 資料夾中的收件者與未提供給 Exchange 組織中的收件者。在 \[連絡人\] 資料夾中有遠端收件者的下列 TNEF 對話選項：

  - **讓 Outlook 決定最佳傳送格式**   此為預設設定。 此設定會強制 Outlook 使用預設網際網路格式所指定的 TNEF 轉換選項。 可能的值有 \[轉換成 HTML 格式\]、\[轉換成純文字格式\] 或 \[使用 Outlook RTF 格式傳送\]。 因此，TNEF 郵件可能維持為 TNEF、轉換成 HTML 或轉換成純文字。 如果要確保此收件者的 TNEF 郵件保持為 TNEF，應該將此設定從 **\[讓 Outlook 決定最佳傳送格式\]** 變更為 **\[使用 Outlook RTF 格式傳送\]**。

  - **僅傳送純文字**   傳送給收件者的任何 TNEF 郵件都會轉換成純文字。 將失去郵件中的任何格式。

  - **使用 Outlook RTF 格式傳送**   傳送給遠端收件者的任何 TNEF 郵件仍然為 TNEF 郵件。

您可在 Outlook 的下列位置設定連絡人的這些選項：

  - **Outlook 2010 或 Outlook 2013**   開啟連絡人卡片、按兩下電子郵件地址、按一下 **\[檢視更多與此人互動的選項\]** 圖示，然後選取 **\[Outlook 內容\]**。 在 **\[電子郵件內容\]** 對話方塊中，選取 **\[網際網路格式\]**。

  - **Outlook 2007**   開啟連絡人卡片、按兩下 **\[電子郵件\]** 欄位並選取 **\[網際網路格式\]**。

回到頁首

## TNEF 轉換選項的優先順序

Exchange 會使用下列清單所述的優先順序，決定傳送至 Exchange 組織外收件者之外寄郵件的 TNEF 轉換選項：

1.  遠端網域設定

2.  郵件使用者或郵件連絡人設定

3.  Outlook 設定

\[\] 清單中指定的優先順序，從最高到最低。遠端網域的 TNEF 設定會覆寫在信箱使用者、 郵件連絡人或在 Outlook 中的 TNEF 設定。例如，假設您傳送 Rtf 郵件在 Outlook 中，但是收件者是其中的遠端網域設定特別不允許 TNEF 格式郵件的網域。收件者所接收的訊息將會是純文字或 HTML、 但不是 TNEF。

另外，Exchange 絕不將摘要 Transport Neutral Encoding Format (STNEF) 郵件傳送至外部收件者。僅限 TNEF 郵件可以傳送至 Exchange 組織外部收件者。

回到頁首


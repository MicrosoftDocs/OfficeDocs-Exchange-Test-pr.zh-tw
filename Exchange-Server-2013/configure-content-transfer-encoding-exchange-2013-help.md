---
title: '設定內容傳輸編碼: Exchange 2013 Help'
TOCTitle: 設定內容傳輸編碼
ms:assetid: c4922362-18d4-42f7-9189-9076720eb1d8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg144562(v=EXCHG.150)
ms:contentKeyID: 50474156
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定內容傳輸編碼

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

*內容傳輸編碼*定義編碼方法將二進位電子郵件訊息資料轉換成 US-ASCII 純文字格式。這個轉換允許透過僅支援 US-ASCII 文字中的 \[郵件的舊 SMTP 郵件伺服器的一點傳輸訊息。內容傳輸編碼定義於 RFC 2045。傳輸編碼方法為儲存在郵件中**的內容傳輸編碼**標頭\] 欄位。在 Microsoft Exchange Server 2013、 內容傳輸編碼方法為可用的：

  - **7 位**   這個值表示郵件內文資料已是 US ASCII 純文字格式，不再需要對郵件進行編碼。

  - **Quoted-printable (QP)**  此編碼方法使用列印 US-ASCII 字元編碼郵件內文資料。如果原始郵件文字是多半 US-ASCII 文字，QP 編碼提供有點可讀取及精簡結果。根據預設， Exchange 2013使用 QP 編碼二進位郵件資料。

  - **Base64**  此編碼的方法主要根據隱私權增強郵件 (PEM) 標準 RFC 1421 中所定義。Base64 編碼使用方法與輸出邊框距離設 PEM 所定義的字元編碼 64 個字元英文字母編碼郵件內文資料。Base64 編碼郵件大小中建立可預測的增加也最佳的二進位資料和非 US-ASCII 文字。

設定傳輸編碼的**Set-organizationconfig**和**Set-RemoteDomain**指令程式使用*ByteEncoderTypeFor7BitCharsets*參數的方法。設有**Set-OrganizationConfig**內容傳輸編碼設定會套用至 Exchange 組織中的所有郵件。設有**Set-RemoteDomain**內容傳輸編碼設定僅適用於傳送至遠端網域中的外部收件者的郵件。

下表列出可用來設定傳輸編碼方法的值。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Set-OrganizationConfig</strong> 中的參數</th>
<th><strong>Set-RemoteDomain</strong> 中的參數</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p><code>Use7Bit</code></p></td>
<td><p>一律使用 7 位元編碼 HTML 和純文字。此為預設值。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p><code>UseQP</code></p></td>
<td><p>HTML 和純文字一律使用 QP 編碼。</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p><code>UseBase64</code></p></td>
<td><p>HTML 和純文字一律使用 Base64 編碼。</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p><code>UseQPHtmlDetectTextPlain</code></p></td>
<td><p>使用 QP 編碼 HTML 和純文字除非啟用列換行以純文字。如果啟用列換行，則使用 7 位元編碼純文字。</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p><code>UseBase64HtmlDetectTextPlain</code></p></td>
<td><p>使用 Base64 編碼 HTML 和純文字除非啟用列換行以純文字。如果啟用列換行純文字中，使用 Base64 編碼 HTML，並使用純文字編碼 7 位元。</p></td>
</tr>
<tr class="even">
<td><p>13</p></td>
<td><p><code>UseQPHtml7BitTextPlain</code></p></td>
<td><p>一律使用 QP 編碼 HTML。一律使用純文字編碼 7 位元。</p></td>
</tr>
<tr class="odd">
<td><p>14</p></td>
<td><p><code>UseBase64Html7BitTextPlain</code></p></td>
<td><p>一律使用 Base64 編碼 HTML。一律使用純文字編碼 7 位元。</p></td>
</tr>
</tbody>
</table>


如需有關 **Content-Transfer-Encoding** 標頭欄位的詳細資訊，請參閱[內容轉換](content-conversion-exchange-2013-help.md)中的「了解電子郵件的結構」一節。

有关远程域的详细信息，请参阅[遠端網域](remote-domains-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱主題中的「傳輸服務」[郵件流程權限](mail-flow-permissions-exchange-2013-help.md)項目。

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


## 您要執行的工作

## 使用命令介面為組織設定內容傳輸編碼方法

若要為組織設定內容傳輸編碼方法，請執行下列命令：

    Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets <Integer>

例如，若要將內容傳輸編碼方式設為 Base64，請執行下列命令：

    Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets 2

## 使用命令介面為遠端網域設定內容傳輸編碼方法

若要為遠端網域中的所有收件者設定內容傳輸編碼方法，請執行下列命令：

    Set-RemoteDomain -ByteEncoderTypeFor7BitCharsets <Value>

例如，若要將內容傳輸編碼方式設為 Base64，請執行下列命令：

    Set- RemoteDomain -ByteEncoderTypeFor7BitCharsets UseBase64

## 如何才能了解這是否正常運作？

若要驗證您已成功設定內容傳輸編碼方法，請執行下列動作：

1.  傳送測試郵件包含 US-ASCII 文字和二進制資料或非 US-ASCII 文字內部或外部測試帳戶的混合。測試遠端網域設定遠端網域中使用帳戶來測試組織設定內部和外部帳戶。

2.  在電子郵件用戶端，檢視郵件中的 **Content-Transfer-Encoding** 標頭欄位，驗證郵件中使用的內容傳輸編碼方法符合您設定的方法。


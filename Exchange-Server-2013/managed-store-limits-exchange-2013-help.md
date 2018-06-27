---
title: '受管理的儲存限制: Exchange 2013 Help'
TOCTitle: 受管理的儲存限制
ms:assetid: bea9ec15-bfb5-4716-b14e-010e389c9f9e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt741981(v=EXCHG.150)
ms:contentKeyID: 73226002
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 受管理的儲存限制

 

_**上次修改主題的時間：**2016-09-15_

**摘要：** 關於受管理的存放區的連線限制和設定方式。

在MicrosoftExchange Server 2013、 連線和流量限制已放置在Exchange受管理存放區，以防止單一應用程式或單一使用者使用受管理存放區的所有可用的連線。若要使用的所有連線允許單一使用者或應用程式，其他使用者或應用程式無法能夠存取受管理存放區，可能會導致停機時間。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>對於具有管理權限的帳戶所進行的任何連線，最大工作階段限制有增加到 64000。</td>
</tr>
</tbody>
</table>


## 術語

下列詞彙的知識可協助您了解本主題中所參照的連線類型。

  - 工作階段  
    工作階段代表服務和用戶端應用程式，例如 Microsoft Outlook，用來連線至受管理存放區的連線。服務和用戶端可以有多個工作階段在特定時間。可以交替使用的字詞*連線*和*工作階段*。

<!-- end list -->

  - 執行緒  
    執行緒代表受管理存放區同時執行的要求。例如，如果使用者開啟Outlook資料夾， Outlook執行即代表使用者要求之受管理存放區。執行要求的是單一往來書信時。
    
    在Exchange Server 2013、 有不再執行緒限制根據用戶端類型。相反地，適用於所有的用戶端執行緒**每個信箱資料庫**的數目上限為 50。例外是 16 的可用性服務，且每位使用者最大限制。

回到頁首

## 工作階段限制

下表列出受管理存放區並將這些連線為基礎的限制的用戶端連線的類型。如果您想要修改的工作階段限制，請參閱 「 設定工作階段限制 」 緊接在表格。

舊版 Exchange 設定限制的每部伺服器連線數目為基礎之受管理存放區的連線數目而定。在 Exchange 2013、 工作階段限制根據每個信箱資料庫的連線。

類型的連線限制在 Exchange 2013 如下：

  - **每個程序的最大工作階段**  會指定Exchange服務可以有一次開啟信箱資料庫上的工作階段數目上限。

  - **每個程序的最大使用者工作階段**  會指定單一使用者的特定通訊協定的工作階段數目上限。

下一節 「 設定工作階段限制 」 說明如何修改這些限制。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端類型</th>
<th> </th>
<th>最大工作階段每個信箱資料庫</th>
<th>使用者工作階段每個信箱資料庫的預設數目</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>管理員</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>可用性服務</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>內容索引</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td> </td>
<td><p>不適用</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Web 服務</p></td>
<td> </td>
<td><p>不適用</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>管理</p></td>
<td> </td>
<td><p>不適用</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>中間層 (MoMT) 上的 MAPI</p></td>
<td> </td>
<td><p>不適用</p></td>
<td><p>32</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants︰ 事件</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxAssistants： 逾時</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>MSExchange 遠端程序呼叫</p></td>
<td> </td>
<td><p>不適用</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Office Outlook Web App</p></td>
<td> </td>
<td><p>不適用</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>POP3 及 IMAP4</p></td>
<td> </td>
<td><p>不適用</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>傳輸</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>整合通訊</p></td>
<td> </td>
<td><p>不適用</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>其他人</p></td>
<td> </td>
<td><p>不適用</p></td>
<td><p>16</p></td>
</tr>
</tbody>
</table>


## 設定工作階段限制

您只能修改預設的工作階段限制。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您想要修改的工作階段限制，您必須加以修改任何資料庫可用性群組 (Dag) 內的所有信箱伺服器上。如果您未在所有伺服器上進行相同的變更，則結果將是不一致。若要增加用戶端存取伺服器上的工作階段限制， <code>RCAMaxConcurrency</code>值必須增加上的節流原則。如需詳細資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/dd298094(v=exchg.150)">Set-ThrottlingPolicy</a>。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不正確編輯登錄會造成嚴重問題，可能需要重新安裝作業系統。如因不正確編輯登錄造成任何問題，這些問題可能無法解決。編輯登錄前請先備份所有珍貴資料。</td>
</tr>
</tbody>
</table>


1.  啟動 \[登錄編輯程式\] (regedit)。

2.  瀏覽至下列登錄子機碼：
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**。

3.  以滑鼠右鍵按一下**ParametersSystem**、 指向 \[**新增**\] 和 \[ **DWORD （32 位元） 值。**
    
    在結果窗格中建立新數值。

4.  重新命名為下列值，其中的機碼，然後按 Enter：
    
      - **每位使用者的最大允許工作階段**  此限制指定每個使用者最大可允許的工作階段。
    
      - **每位使用者的最大允許的服務工作階段**  此限制指定每個使用者工作階段的最大允許的服務。
    
      - **每一個服務的最大允許的 Exchange 工作階段**  此限制指定允許每一個服務Exchange工作階段的最大。預設值為 10000。

5.  以滑鼠右鍵按一下新建立的機碼，並再按一下 \[**修改**\]。

6.  在**數值資料**\] 方塊中，輸入您要將此項目物件的數目，然後按一下 \[**確定\]**。使用上述表格檢視的預設設定。

回到頁首

## 開啟項目限制

開啟項目限制會放置在單一信箱可以開啟一個工作階段中的項目數的限制。不過，使用者可以同時開啟多個工作階段。例如，如果使用者已開啟兩個工作階段，使用者無法開啟 1000 個資料夾。

如果您想要修改這些限制，請參閱 「 設定開啟項目限制 」 緊接在表格。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>項目類型</th>
<th>登錄物件類型</th>
<th>最大開啟每個工作階段</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ACL 的檢視</p></td>
<td><p>objtACLView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>附件</p></td>
<td><p>objtAttachment</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>附件檢視</p></td>
<td><p>objtAttachmentView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>CStream</p></td>
<td><p>objtCStream</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>資料夾</p></td>
<td><p>objtFolder</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>資料夾檢視</p></td>
<td><p>objtFolderView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>FX 目的地資料流</p></td>
<td><p>objtFXDstStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>FX 來源資料流</p></td>
<td><p>objtFXSrcStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>郵件</p></td>
<td><p>objtMessage</p></td>
<td><p>250</p></td>
</tr>
<tr class="even">
<td><p>郵件檢視</p></td>
<td><p>objtMessageView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>通知</p></td>
<td><p>objtNotify</p></td>
<td><p>500,000</p></td>
</tr>
<tr class="even">
<td><p>規則檢視</p></td>
<td><p>objtRulesView</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>資料流</p></td>
<td><p>objtStream</p></td>
<td><p>250</p></td>
</tr>
</tbody>
</table>


## 設定開啟項目限制

您可以將限制可同時使用 MAPI 用戶端的資源數目上限。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您想要修改的開啟項目限制，您需要加以修改任何 Dag 和用戶端存取陣列內的所有信箱伺服器上。如果您未在所有伺服器上進行相同的變更，則結果將是不一致。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不正確編輯登錄會造成嚴重問題，可能需要重新安裝作業系統。如因不正確編輯登錄造成任何問題，這些問題可能無法解決。編輯登錄前請先備份所有珍貴資料。</td>
</tr>
</tbody>
</table>


1.  啟動 \[登錄編輯程式\] (regedit)。

2.  瀏覽至下列登錄子機碼：
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**

3.  在 \[ParametersSystem\] 上按一下滑鼠右鍵，指向 \[新增\]，然後按 \[機碼\]。
    
    在主控台樹狀目錄中建立新的金鑰。

4.  重新命名的索引鍵**MaxObjsPerMapiSession**，並按 Enter。

5.  **MaxObjsPerMapiSession**上按一下滑鼠右鍵，並指向 \[**新增**\]，然後按一下 \[ **DWORD （32 位元） 值**。
    
    在結果窗格中建立新的數值。

6.  重新金鑰命名為*\<Object\_type\>*，其中*\<Object\_type\>*是您要修改登錄物件類型的名稱。例如，若要修改可以開啟的訊息數目、 使用*objtMessage*。按 Enter 鍵。

7.  以滑鼠右鍵按一下新建立的機碼，並再按一下 \[**修改**\]。

8.  在 \[**數值資料**\] 方塊中輸入您想要限制，此項目物件的數目，然後按一下 \[**確定\]**。例如，輸入**350**增加物件的值。

9.  重新啟動 Microsoft Exchange Information Store 服務。

回到頁首

## 項目大小限制

項目大小限制會被放置在使用者的信箱內的項目上的限制。他們是可設定使用*MaxSendSize*及*MaxReceiveSize*參數[Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))指令程式上。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>項目類型</th>
<th>限制</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>訊息 （儲存）</p></td>
<td><p>SendLimit、 ReceiveLimit 的大小上限</p></td>
</tr>
<tr class="even">
<td><p>訊息 （傳送）</p></td>
<td><p>SendLimit 的大小上限</p></td>
</tr>
<tr class="odd">
<td> </td>
<td> </td>
</tr>
</tbody>
</table>


回到頁首


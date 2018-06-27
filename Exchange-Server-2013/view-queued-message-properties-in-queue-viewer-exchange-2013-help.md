---
title: '在佇列檢視器中檢視已排入佇列的郵件內容: Exchange 2013 Help'
TOCTitle: 在佇列檢視器中檢視已排入佇列的郵件內容
ms:assetid: 9d15d8b8-e061-4288-9354-df58e282fb6b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123934(v=EXCHG.150)
ms:contentKeyID: 50473813
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.Edge.SystemManager.MessagePropertyPage
ms.translationtype: MT
---

# 在佇列檢視器中檢視已排入佇列的郵件內容

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-01-17_

您可以使用 Exchange 工具箱中的佇列檢視器，檢視待傳遞之佇列郵件的內容。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「佇列」項目。

  - 您也可以使用 Exchange 管理命令介面中的 Get-message 指令程式來檢視佇列檢視器中看不到的其他訊息內容。如需詳細資訊，請參閱[訊息篩選器](message-filters-exchange-2013-help.md)和[使用 Exchange 管理命令介面管理佇列](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md)。

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

## 在 Exchange 工具箱中使用佇列檢視器檢視郵件內容

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange 2013\] \> \[Exchange 工具箱\]。

2.  在 \[郵件流程工具\] 區段下，按兩下 \[佇列檢視器\]，在新視窗中開啟工具。

3.  在佇列檢視器中，選取 \[郵件\] 索引標籤以參閱組織內目前在佇列中等待傳遞的郵件清單。

4.  在想要檢視內容的郵件上按一下滑鼠右鍵，然後選取 \[內容\]。

5.  
    
    \[一般\] 索引標籤顯示下列有關郵件的詳細資訊：
    
      - **身分識別**  此欄位顯示整數代表特定的郵件。郵件識別碼指派佇列資料庫時接收的郵件進行處理。您可以包含選用的伺服器與佇列 identity 以找出郵件的唯一執行個體。
    
      - **主旨**  此欄位會顯示郵件的主旨，以文字字串表示。此值是取自`Subject:`標頭\] 欄位。
    
      - **網際網路訊息識別碼**  此欄位顯示`MessageID:`標頭欄位的值。此屬性的值以表示後面接著傳送伺服器，如本範例所示的 SMTP 位址的 GUID: 67D754D6103DC4FB3BA6BC7205DACABA61231@exchange.contoso.com
    
      - **從地址**  此欄位顯示郵件的寄件者的 SMTP 位址。這個值取自 MAIL FROM： 郵件信封中。
    
      - **狀態**  此欄位會顯示目前的郵件狀態。訊息可以有一個下的 \[狀態\] 值：
        
          - **作用中**  如果郵件的傳遞佇列中，郵件被傳遞至的目的地。提交佇列中郵件時，正在分類程式處理郵件。
        
          - **擱置的移除**  郵件已遭刪除由系統管理員，但已經有相同的傳遞。如果傳遞結束於錯誤導致重新輸入佇列的訊息將會刪除郵件。否則請會繼續傳遞。
        
          - **擱置擱置**  郵件已由系統管理員擱置但已經在傳遞。如果傳遞結束於錯誤導致重新輸入佇列的訊息將擱置郵件。否則請會繼續傳遞。
        
          - **準備就緒**   郵件已在佇列中準備就緒可進行處理。
        
          - **重試**  此訊息所在的佇列的最後一個嘗試連線失敗。郵件等候下一個佇列重試。
        
          - **已擱置   **郵件已由系統管理員擱置。
    
      - **大小 (KB)** 這個欄位會以進位至最接近 KB 的值來顯示郵件大小。
    
      - **郵件來源名稱** 此欄位顯示將此郵件提交到佇列的元件名稱。
    
      - **\[來源 IP\]** 此欄位顯示將郵件提交到 Exchange 組織之外部伺服器的 IP 位址。
    
      - **SCL**  此欄位顯示垃圾郵件信賴等級 (scl) 的郵件。有效的 SCL 項目為整數 0 到 9 或-1。空的 SCL 項目會指出郵件尚未尚未處理的內容篩選器代理程式。
    
      - **收到日期** 此欄位顯示伺服器收到郵件時的日期與時間，而該伺服器就是擁有郵件所在佇列的伺服器。
    
      - **到期時間** 此欄位顯示郵件因無法傳遞而即將到期，並且將從佇列中刪除時的日期與時間。
    
      - **上個錯誤**   此欄位顯示上次記錄到的郵件錯誤。
    
      - **佇列識別碼**  此欄位顯示保留郵件佇列的識別。佇列識別碼將表示於表單*Server\\destination*，其中*目的地*是傳遞群組、 路由目的地、 持續佇列名稱或佇列資料庫識別碼。佇列資料庫識別碼以整數表示，並可由檢視郵件的內容。
    
      - **收件者** 此欄位顯示郵件寄送的收件者清單。
    
      - **重試計數** 此欄位顯示已嘗試將郵件傳遞至目的地的次數。

6.  
    
    **收件者資訊** 索引標籤顯示郵件收件者的下列相關資訊：
    
      - **地址**  此欄位顯示郵件的收件者的 SMTP 位址。這個值是取自`RCPT TO:`郵件信封中。
    
      - **狀態**  此欄位會顯示目前的郵件狀態。訊息可以有一個下的 \[狀態\] 值：
        
          - **作用中**  如果郵件的傳遞佇列中，郵件被傳遞至的目的地。提交佇列中郵件時，正在分類程式處理郵件。
        
          - **擱置的移除**  郵件已刪除由系統管理員，但已經有相同的傳遞。如果傳遞結束於錯誤導致重新輸入佇列的訊息將會刪除郵件。否則請會繼續傳遞。
        
          - **擱置擱置**  郵件已暫停由系統管理員，但已經有相同的傳遞。如果傳遞結束於錯誤導致重新輸入佇列的訊息將擱置郵件。否則請會繼續傳遞。
        
          - **準備就緒**   郵件已在佇列中準備就緒可進行處理。
        
          - **重試**  此訊息所在的佇列的最後一個嘗試連線失敗。郵件等候下一個佇列重試。
        
          - **已擱置** 郵件已由系統管理員擱置。
    
      - **上個錯誤**   此欄位顯示上次記錄到的郵件錯誤。

## 使用命令介面檢視訊息的內容

您可以使用**Get-Message**指令程式來檢視目前佇列進行傳遞郵件的屬性。下列範例會以表格形式列出寄件者地址、 收件者、 主旨與目前處於 retry 狀態的所有郵件的接收的日期資訊：

    Get-Message -IncludeRecipientInfo -Filter {Status -eq "Retry"} | Format-Table FromAddress,Recipients,Subject,DateReceived

如需詳細的語法及參數資訊，請參閱 [Get-Message](https://technet.microsoft.com/zh-tw/library/bb124738\(v=exchg.150\))。


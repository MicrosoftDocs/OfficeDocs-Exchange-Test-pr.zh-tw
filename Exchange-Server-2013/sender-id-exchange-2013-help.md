---
title: '寄件者識別碼: Exchange 2013 Help'
TOCTitle: 寄件者識別碼
ms:assetid: 0f628f83-df8c-43fb-bf49-7aaa9ec69ab1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996295(v=EXCHG.150)
ms:contentKeyID: 50472579
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 寄件者識別碼

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

寄件者識別碼代理程式是在 Microsoft Exchange Server 2013反垃圾郵件代理程式。寄件者識別碼代理程式依賴收到的 SMTP 標頭及傳送的系統 DNS 服務來決定何種巨集指令，內送郵件採取的任何查詢。

寄件者識別碼被為了抵禦模擬的寄件者和網域，經常呼叫*詐騙*的作法。*詐騙的郵件*是具有傳送位址的上次修改看起來像於非實際的郵件寄件者的寄件者的電子郵件訊息。

詐騙的郵件通常包含 From： 自稱要從特定組織的地址。過去是較容易詐騙 From： 地址，這兩個 SMTP 工作階段中，例如 MAIL FROM： 標頭及 RFC 2822 郵件資料，例如以從:"Masato Kawai"masato@contoso.com 因為未驗證標頭。

**目錄**

Using Sender ID to combat spoofing

Updating your organization's Internet-facing DNS to support Sender ID

Specifying recipients and sender domains to exclude from Sender ID filtering

## 使用者寄件者識別碼抵禦詐騙

寄件者識別碼詐騙比較難。當您啟用寄件者識別碼時，每則訊息包含寄件者識別碼狀態中的中繼資料的郵件。時接收電子郵件訊息、 Exchange server 查詢以確認從中收到郵件的 IP 位址有權傳送的郵件標頭中所指定之網域的郵件的寄件者的 DNS 伺服器。已授權的傳送端伺服器的 IP 位址被稱為一頭負責的地址 (PRA)。

網域系統管理員將發佈及其 DNS 伺服器上的寄件者原則架構 (SPF) 記錄。SPF 記錄來識別授權的外寄電子郵件伺服器。如果寄件者的 DNS 伺服器上設定 SPF 記錄，則 Exchange 伺服器會剖析 SPF 記錄，並判斷是否已授權可代表在郵件中所指定的網域傳送電子郵件的來源收到郵件的 IP 位址。如需 SPF 記錄所包含的功能以及如何建立 SPF 記錄的詳細資訊，請參閱[寄件者識別碼](https://go.microsoft.com/fwlink/p/?linkid=50977)。

Exchange server 更新 SPF 記錄為基礎的寄件者識別碼狀態訊息中繼資料。之後的 Exchange server 更新訊息中繼資料、 郵件傳遞繼續像平常一樣。

## 寄件者識別碼狀態值

寄件者識別碼評估程序會產生之郵件的寄件者識別碼狀態。寄件者識別碼狀態用來評估垃圾郵件信賴等級 (scl) 的郵件。此狀態可以將為下列值之一：

  - **Pass**   IP 位址及 Purported Responsible Address (PRA) 均通過寄件者識別碼驗證檢查。

  - **Neutral**   發佈的寄件者識別碼明確未下定論。

  - **Soft fail**   PRA 的 IP 位址可能位於不允許的集合內。

  - **Fail   **不允許 IP 位址；傳入的郵件中找不到 PRA，或者傳送網域不存在。

  - **None   **寄件者的 DNS 中沒有發行的 SPF 資料。

  - **TempError   **發生暫時的 DNS 失敗 (如 DNS 伺服器無法使用)。

  - **PermError   **DNS 記錄無效 (如記錄格式錯誤)。

寄件者識別碼狀態新增至訊息的中繼資料及更新版本轉換成的 MAPI 屬性。在 Microsoft Outlook 垃圾郵件篩選器會使用 MAPI 屬性期間產生的 SCL 值。

Outlook 會顯示寄件者識別碼狀態，皆一定為垃圾郵件的特定寄件者識別碼值的旗標一則訊息。Outlook 只在 SCL 值的計算期間所用的寄件者識別碼狀態值。

除了產生寄件者識別碼狀態的七個案例，寄件者識別碼評估程序可能會顯示執行個體其中 From: IP 位址會遺失。如果 \[自： IP 位址是遺失、 無法設定寄件者識別碼狀態。如果無法設定寄件者識別碼狀態，Exchange 會繼續進行重新處理郵件而不包括在郵件的寄件者識別碼狀態。未捨棄或已拒絕郵件。在此案例中，寄件者識別碼狀態未設定，並記錄應用程式事件。

如需寄件者識別碼狀態在郵件中顯示方式的相關資訊，請參閱[反垃圾郵件戳記](anti-spam-stamps-exchange-2013-help.md)。

## 用於處理詐騙郵件和無法連線之 DNS 伺服器的寄件者識別碼選項

您也可以定義的 Exchange server 如何處理會被識別為詐騙郵件的郵件和時的 DNS 伺服器無法連線至 Exchange server 如何處理郵件。Exchange 伺服器會處理詐騙的郵件並無法存取之 DNS 伺服器的選項包括下列動作：

  - **戳記狀態**  此選項會將預設動作。您組織的所有內送的郵件已包含在郵件的中繼資料的寄件者識別碼狀態。

  - **拒絕**  此選項會拒絕郵件並傳送至傳送伺服器 SMTP 錯誤回應。SMTP 錯誤回應是 5*xx*層級的通訊協定回應會對應至寄件者識別碼狀態的文字。

  - **刪除**  此選項會刪除郵件而未通知傳送端系統的刪除。事實上，Exchange server 傳送至傳送伺服器假確定 SMTP 命令，，然後刪除郵件。傳送伺服器假設傳送郵件，因為它不會重試中相同的工作階段傳送郵件。

如需如何設定寄件者識別碼代理程式的相關資訊，請參閱[管理寄件者識別碼](manage-sender-id-exchange-2013-help.md)。

回到頁首

## 更新組織面向網際網路的 DNS，以支援寄件者識別碼

寄件者識別碼的有效性取決於特定的 DNS 資料。使用 SPF 更新其網際網路對向的 DNS 伺服器的多組織記錄、 寄件者識別碼更有效率地識別詐騙的電子郵件訊息。

若要支援的寄件者識別碼基礎結構，您必須建立 SPF 記錄和主控您公用 DNS 伺服器上的 SPF 記錄更新網際網路對向的 DNS 資料。如需如何建立及部署 SPF 記錄的詳細資訊，請參閱[寄件者識別碼](https://go.microsoft.com/fwlink/p/?linkid=50977)。

回到頁首

## 指定要排除在寄件者識別碼篩選之外的收件者與寄件者網域

若要從 \[寄件者識別碼篩選排除特定收件者和寄件者的網域。為達成此目的，您可以指定的收件者和寄件者網域在 Exchange 管理命令介面中使用**Set-SenderIdConfig**指令程式。如需詳細資訊，請參閱[Set-SenderIdConfig](https://technet.microsoft.com/zh-tw/library/aa998859\(v=exchg.150\))。

回到頁首


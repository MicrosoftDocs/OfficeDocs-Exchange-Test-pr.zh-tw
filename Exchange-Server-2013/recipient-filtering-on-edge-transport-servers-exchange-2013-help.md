---
title: 'Edge Transport Server 上的收件者篩選: Exchange 2013 Help'
TOCTitle: Edge Transport Server 上的收件者篩選
ms:assetid: 994eefd9-3903-41e6-a882-1e333d6d2d18
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123891(v=EXCHG.150)
ms:contentKeyID: 50473791
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge Transport Server 上的收件者篩選

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-05-07_

收件者篩選器是 Microsoft Exchange Server 2013 中一個反垃圾郵件的功能，依賴 RCPT TO SMTP 標頭 (若有的話)，來決定要對輸入郵件採取的動作。收件者篩選器是由收件者篩選器代理程式執行。

收件者篩選器代理程式會根據組織中預定收件者的特性來封鎖訊息。收件者篩選器代理程式可以協助您防止在下列案例中接受訊息：

  - **不存在的收件者**   您可以防止傳遞至不在組織通訊錄內的收件者。例如，您可能想要停止傳遞至常被濫用的帳戶名稱，例如 administrator@contoso.com 或 support@contoso.com。

  - **限制的通訊群組清單**   您可以防止網際網路郵件傳遞至只應由內部使用者使用的通訊群組清單。

  - **絕對不應收到網際網路郵件的信箱**   您可以防止網際網路郵件傳遞至通常只在組織內部使用的特定信箱或別名，例如 Helpdesk。

收件者篩選器代理程式會對儲存在下列一或兩個資料來源中的收件者執行：

  - **收件者封鎖清單**   系統管理員定義的收件者清單，這些收件者一律不會收到網際網路所輸入的郵件。

  - **收件者查閱**   查詢 Active Directory 以確認組織中存在的收件者。在邊際傳輸伺服器上，收件者查閱需要存取 EdgeSync 所提供的 Active Directory 資訊與 Directory Active 輕量型目錄服務 (AD LDS) 的本機執行個體。

啟用收件者篩選器代理程式時，會根據收件者的特性，對輸入郵件採取下列其中一個動作。這些收件者由 RCPT TO 標頭指示。

  - 如果輸入郵件包含收件者封鎖清單中的收件者，則 Exchange 伺服器會傳送 `550 5.1.1 User unknown` SMTP 工作階段錯誤至傳送伺服器。

  - 如果輸入郵件包含收件者封鎖清單中沒有的收件者，則 Exchange 伺服器會傳送 `550 5.1.1 User unknown` SMTP 工作階段錯誤至傳送伺服器。

  - 如果收件者不在收件者封鎖清單中，但是有在收件者查閱中，則 Exchange 伺服器會傳送 `250 2.1.5 Recipient OK` SMTP 回應至傳送伺服器，鏈結中的下一個反垃圾郵件代理程式會處理郵件。

**目錄**

Configuring recipient lookup

Tarpitting functionality

Multiple namespaces

## 設定收件者查閱

若要減少垃圾郵件，最有效的方法之一，就是在接收網際網路的輸入郵件之前先驗證收件者。您可以啟用封鎖傳送郵件給 Exchange 組織中不存在之收件者，並使用 Exchange 管理命令介面中的 **Set-RecipientFilterConfig** Cmdlet 封鎖特定收件者。如需詳細資訊，請參閱 [管理 Edge Transport server 上的收件者篩選](manage-recipient-filtering-on-edge-transport-servers-exchange-2013-help.md)。

如果您的周邊網路中安裝了邊際傳輸伺服器，可以將邊際傳輸伺服器上所執行的 AD LDS 執行個體設定為與 Active Directory 同步。根據預設，AD LDS 是在 Edge Transport server 上進行安裝及設定。不過，您必須透過組織訂閱邊際傳輸伺服器，來設定 AD LDS 與連結網域的 Active Directory 全域目錄伺服器通訊。如需詳細資訊，請參閱 [使用 Exchange 2010 或 2007 Edge Transport server 在 Exchange 2013](use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md)。

回到頁首

## 垃圾郵件防堵 (Tarpitting) 功能

收件者查閱功能可讓傳送伺服器判定電子郵件地址是否有效。前面提過，輸入郵件的收件者若是已知的收件者，Exchange 伺服器就會傳回一個 `250 2.1.5 Recipient OK` SMTP 回應至傳送伺服器。此功能為目錄搜集攻擊提供了理想的環境。

*目錄搜集攻擊*會嘗試從特定組織收集有效的電子郵件地址，以便將電子郵件地址加入垃圾郵件資料庫中。因為所有傳入的垃圾郵件都必須經由人員開啟電子郵件才能作用，所以惡意使用者或*垃圾郵件傳送者*會出錢購買已知使用中的地址。由於 SMTP 通訊協定會提供已知寄件者和未知寄件者的回應，因此垃圾郵件傳送者可以編寫一個自動化程式，使用常見名稱或字典名詞，建構特定網域的電子郵件地址。此程式會收集所有傳回 `250 2.1.5 Recipient OK` SMTP 回應的電子郵件地址並放棄所有傳回 `550 5.1.1 User unknown` SMTP 工作階段錯誤的電子郵件地址。然後垃圾郵件傳送者可以販售有效的電子郵件地址，或是使用這些地址作為來路不明郵件的收件者。

為了對抗目錄搜集攻擊，Exchange 2013 包含了垃圾郵件防堵功能。*垃圾郵件防堵*是指針對指出大量垃圾郵件或其他煩人郵件的特定 SMTP 通訊模式，以人工方式延遲伺服器回應的作法。垃圾郵件防堵的目的是減慢這些電子郵件流量的通訊處理速度，使傳送垃圾郵件的人員或組織傳送垃圾郵件的成本增加。垃圾郵件防堵使目錄搜集攻擊需要極高的代價才能有效自動執行。

如果未設定垃圾郵件防堵，Exchange 伺服器會在收件者查閱中沒有收件者時，立即傳回 `550 5.1.1 User unknown` SMTP 工作階段錯誤給寄件者。如果設定了垃圾郵件防堵，則 SMTP 會在等候特定的秒數後，才傳回 `550 5.1.1 User unknown` 錯誤。此 SMTP 工作階段的暫停，會使目錄搜集攻擊更難自動執行，降低垃圾郵件傳送者的成本效益。根據預設，接收連接器上的垃圾郵件防堵會設定為 5 秒。

若要在 SMTP 傳回 `550 5.1.1 User unknown` 前設定延遲，您何以使用 **Set-ReceiveConnector** Cmdlet 上的 *TarpitInterval* 參數來設定垃圾郵件防堵間隔。語法為：

    Set-ReceiveConnector <Receive Connector> -TarpitInterval <00:00:00 to 00:10:00>

預設值是 `00:00:05` 或 5 秒。Edge Transport Server 上的預設接收連接器名稱是 `Default internal receive connector <server name>`。

如果您決定要變更垃圾郵件防堵間隔，請謹慎執行。間隔過長可能會使一般的郵件流量中斷，但間隔若過短，則可能無法有效防止目錄搜集攻擊。因此在變更垃圾郵件防堵間隔時，請採用微量增減的方式並驗證結果。例如，如果 5 秒沒有效果，請試著將間隔變更為 10 秒。

回到頁首

## 多重命名空間

收件者篩選器代理程式僅為授權網域執行收件者查閱。如果您的組織會代表設為內部延遲或外部延遲網域之其他網域接受並轉寄郵件，收件者篩選器代理程式就不會對這些網域中的收件者執行收件者查閱。不過，如果收件者封鎖清單有指定封鎖的收件者，該收件者將被收件者篩選器代理程式封鎖。

請注意，您也可以在邊際傳輸伺服器本機上設定接受的網域。如果網域被設為內部延遲或外部延遲網域，邊際傳輸伺服器上的收件者篩選器代理程式也不會對這些網域中的收件者執行收件者查閱。

回到頁首


---
title: 'Exchange Server 2013 中的 POP3 和 IMAP4: Exchange 2013 Help'
TOCTitle: POP3 及 IMAP4
ms:assetid: a7dc91ee-2919-4db3-ae9c-cd665d2e09ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657728(v=EXCHG.150)
ms:contentKeyID: 50473892
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 2013 中的 POP3 和 IMAP4

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-08-16_

深入了解 Exchange Server 2013 中 POP3 和 IMAP4 通訊協定的差異，以及如何設定選項以從各種電子郵件程式存取 Exchange 2013 信箱。

依預設，會在 Exchange Server 2013 中停用 POP3 與 IMAP4。為支援仍然依賴這些通訊協定的 POP3 用戶端，您需要啟動兩個 POP3 服務：Microsoft Exchange POP3 服務和 Microsoft Exchange POP3 後端服務。為支援仍然依賴這些通訊協定的 IMAP4 用戶端，您需要啟動兩個 IMAP4 服務：Microsoft Exchange IMAP4 服務和 Microsoft Exchange IMAP4 後端服務。

如需啟用 POP3 與 IMAP4 服務的詳細步驟，請參閱 [在 Exchange 2013 中啟用 POP3](enable-pop3-in-exchange-2013-exchange-2013-help.md) 和 [啟用 Exchange 2016 的 IMAP4](enable-imap4-in-exchange-2013-exchange-2013-help.md)。

根據預設，在執行 Exchange 2013 的電腦上具有信箱的使用者可以使用 Outlook 或 Outlook Web App、Exchange ActiveSync 或 Outlook 語音存取來存取其信箱。Outlook、Outlook Web App 和 Outlook 語音存取可讓您的電子郵件使用者使用一組完整功能，這組功能可供在 Exchange 2016 伺服器上具有信箱的使用者使用。

**目錄**

POP3 與 IMAP4 功能概觀

POP3 和 IMAP4 跨站台連線

使用非標準帳戶搭配 POP3 及 IMAP4

了解 POP3 和 IMAP4 之間的差異

POP3 與 IMAP4 電子郵件應用程式的傳送和接收選項

POP3 和 IMAP4 應用程式

設定 POP3 或 IMAP4 存取其 Exchange 2013 信箱的使用者設定

## POP3 與 IMAP4 功能概觀

本節說明 Exchange 2013 的 POP3 與 IMAP4 功能。

POP3 與 IMAP4 通訊協定有下列優點和限制：

  - **POP3** POP3 是針對支援離線郵件處理而設計的。使用 POP3 時，除非用戶端上已設為將郵件留在伺服器上，否則，會從伺服器中移除電子郵件，並儲存在本機 POP3 用戶端上。這會將資料管理與安全性責任交給使用者。POP3 並未提供進階的共同作業功能，例如規劃行事曆、連絡人和工作。

  - **IMAP4**   IMAP4 提供離線及線上存取，但和 POP3 一樣，IMAP4 並不提供進階共同作業功能，如規劃行事曆、連絡人與工作。

POP3 與 IMAP4 電子郵件應用程式不使用 POP3 與 IMAP4 將郵件傳送到電子郵件伺服器；它們依賴 SMTP 通訊協定傳送郵件。接收來自用戶端應用程式 (使用 POP3 或 IMAP4) 之電子郵件提交的連接器，會在安裝 Exchange 時自動建立。如需連接器的相關資訊，請參閱[接收連接器](receive-connectors-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每次使用者使用 POP 或 IMAP 電子郵件程式開啟 Office 365 電子郵件時，都會感覺到幾秒鐘的延遲。延遲是因為使用 Proxy 伺服器，而產生額外的驗證用躍點。Proxy 伺服器會先查看指派的 pod 伺服器 (用戶端存取伺服器)，然後對其進行驗證。</td>
</tr>
</tbody>
</table>


## POP3 和 IMAP4 跨站台連線

在舊版的 Exchange 中，如果組織的信箱位於其他站台，您必須執行手動設定步驟，讓 POP3 及 IMAP4 用戶端從組織的某個站台連線至郵件。依預設，Exchange 2013 會自動從某個站台的 Client Access Server 代理至正確的伺服器。

## 使用非標準帳戶搭配 POP3 及 IMAP4

您無法使用 \[匿名\] 帳戶或 \[來賓\] 帳戶，透過 POP3 或 IMAP4 來登入 Exchange 2016 信箱。因為使用非標準帳戶進行 POP3 和 IMAP4 存取時會產生安全性漏洞，所以會封鎖 \[匿名\] 帳戶。此外，您無法透過 POP3 或 IMAP4 連線至系統管理員信箱。Exchange 2013 已特地在內部設下此限制，以強化系統管理員信箱的安全性。若要存取系統管理員信箱，您必須使用 Outlook 或 Outlook Web App。

## 了解 POP3 和 IMAP4 之間的差異

**POP3** POP3 是常用的電子郵件網際網路通訊協定。當 POP3 電子郵件應用程式將電子郵件下載至用戶端電腦時，預設會從伺服器移除下載的郵件。當使用者的電子郵件副本未保留在電子郵件伺服器時，使用者就無法從多部電腦存取相同的電子郵件。不過，部分 POP3 電子郵件應用程式可以設定成將郵件的副本保留在伺服器上，這樣就可以從另一部電腦存取相同的電子郵件。POP3 用戶端應用程式只可以用來將郵件從電子郵件伺服器下載至用戶端電腦的單一資料夾 (通常是「收件匣」)。POP3 通訊協定無法將電子郵件伺服器上的多個資料夾與用戶端電腦的多個資料夾進行同步處理。

**IMAP4** 使用 IMAP4 的電子郵件用戶端應用程式較具彈性，而且提供的功能一般會多於使用 POP3 的電子郵件用戶端應用程式。當 IMAP4 電子郵件應用程式將電子郵件下載至用戶端電腦時，預設會在電子郵件伺服器上保留所下載郵件的副本。因為使用者的電子郵件副本會保留在電子郵件伺服器上，所以使用者可以從多部電腦存取相同的電子郵件。運用 IMAP4 電子郵件，使用者可以在電子郵件伺服器上存取並建立多個電子郵件資料夾。然後，使用者就可以從多個位置的電腦存取他們在伺服器上的所有郵件。例如，大部分 IMAP4 應用程式可以設定成在伺服器上保留使用者寄件備份的副本，讓使用者可以從其他任何電腦檢視他們的寄件備份。IMAP4 支援大部分 IMAP4 應用程式所支援的其他功能。例如，部分 IMAP4 應用程式包含的功能可以讓使用者只檢視他們在伺服器上的電子郵件標頭 (郵件寄件者及主旨)，然後只下載他們想要閱讀的郵件。IMAP4 也不支援公用資料夾存取。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>IMAP4 與 POP3 用戶端對 Exchange 行事曆資訊的存取是有限的。如需詳細資訊，請參閱<a href="configure-calendar-options-for-pop3-exchange-2013-help.md">設定 POP3 行事曆選項</a>及<a href="configure-calendar-options-for-imap4-exchange-2013-help.md">設定 IMAP4 的行事曆選項</a>。</td>
</tr>
</tbody>
</table>


## POP3 與 IMAP4 電子郵件應用程式的傳送和接收選項

POP3 和 IMAP4 電子郵件應用程式可讓使用者選擇想要連線至伺服器以傳送和接收電子郵件的時間。本節討論一些最常用的連線選項，也提供使用者在選取其 POP3 和 IMAP4 電子郵件應用程式的可用連線選項時應該考慮的一些因素。

## 一般組態設定

您可以在 POP3 或 IMAP4 用戶端應用程式上設定的三個最常用連線設定如下：

  - 在每次啟動電子郵件應用程式時傳送和接收郵件。使用此選項時，只會在使用者啟動電子郵件應用程式時傳送和接收郵件。

  - 手動傳送和接收郵件。使用此選項時，只會在使用者按一下用戶端使用者介面中的 \[傳送及接收\] 選項時才會傳送和接收郵件。

  - 在每隔設定的分鐘數之後傳送和接收郵件。使用者設定此選項時，用戶端應用程式會在每隔設定的分鐘數之後連線至伺服器，以傳送郵件和下載所有新的郵件。

如需如何設定所使用電子郵件應用程式之這些設定的相關資訊，請參閱各電子郵件應用程式提供的說明文件。

## 設定傳送/接收選項時的考量

如果執行 POP3 或 IMAP4 電子郵件應用程式的裝置或電腦一律會連線至網際網路，則使用者可能會想要設定電子郵件應用程式在每隔設定的分鐘數之後傳送和接收郵件。以頻繁間隔連線至伺服器可讓使用者的電子郵件應用程式具有伺服器上的最新資訊。不過，如果執行 POP3 或 IMAP4 電子郵件應用程式的裝置或電腦不一定會連線至網際網路，則使用者可能會想要設定電子郵件應用程式手動傳送和接收郵件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果使用者使用支援 IMAP4 IDLE 命令的 IMAP4 相容電子郵件應用程式，則使用者可能可以用接近即時的方式將電子郵件傳送至其 Exchange 信箱，以及接收來自該信箱的電子郵件。若要讓此連線方法運作，則電子郵件伺服器應用程式和用戶端應用程式必須支援 IMAP4 IDLE 命令。在大部分情況下，使用者不需要在其 IMAP4 應用程式中進行任何設定，就可以使用此連線方法。</td>
</tr>
</tbody>
</table>


## POP3 和 IMAP4 應用程式

因為 Exchange 2013 支援 POP3 和 IMAP4，使用者可以使用任何支援 POP3 和 IMAP4 用戶端應用程式的應用程式連線至 Exchange 2013。這些應用程式包含 Outlook、Outlook Web App、Windows Live Mail、Outlook Express、Entourage 和協力廠商應用程式 (如 Gmail、Mozilla Thunderbird 和 Eudora)。每個電子郵件用戶端應用程式所支援的功能會有所不同。如需特定 POP3 和 IMAP4 用戶端應用程式提供之特定功能的相關資訊，請參閱每個應用程式內含的文件。

## 設定 POP3 或 IMAP4 存取其 Exchange 2013 信箱的使用者設定

啟用 POP3 與 IMAP4 用戶端存取功能之後，必須提供使用者所需資訊，以便將其電子郵件程式連線至 Exchange 2016 信箱。

若要從公司網路內部連線，使用者將需要下列資訊：

  - 內部 POP3 或 IMAP4 伺服器名稱

  - 內部 POP3 或 IMAP4 通訊埠號碼

  - 內部 POP3 或 IMAP4 加密方法

  - 內部 SMTP (外寄伺服器) 名稱

  - 內部 SMTP (外寄伺服器) 通訊埠號碼

  - 內部 SMTP (外寄伺服器) 加密方法

若要從網際網路連線，他們將需要下列資訊：

  - 外部 POP3 或 IMAP4 伺服器名稱

  - 外部 POP3 或 IMAP4 通訊埠號碼

  - 外部 POP3 或 IMAP4 加密方法

  - 外部 SMTP (外寄伺服器) 名稱

  - 外部 SMTP (外寄伺服器) 通訊埠號碼

  - 外部 SMTP (外寄伺服器) 加密方法

您可以透過電子郵件或其他手動通訊方法讓使用者可使用這些設定。您也可以設定 Exchange，讓使用者能使用 Outlook Web App 查詢其自己的設定。

**設定 Exchange，讓使用者可查詢他們的 POP3、IMAP4 和 SMTP 伺服器設定**

根據預設，使用者無法透過 Outlook Web App 查看其 POP3、IMAP4 和 SMTP 伺服器設定。若要讓您的使用者這麼做，您必須使用 **Set-PopSettings** 和 **Set-ImapSettings** Cmdlet。若要允許您的使用者查閱其 SMTP (外寄) 伺服器設定，您必須使用 **Set-ReceiveConnector** Cmdlet。

請執行下列動作，以允許使用者查詢他們自己的 POP3、IMAP4 和 SMTP 設定：

  - **POP3 設定**   執行 **Set-POPSettings** Cmdlet 和 *ExternalConnectionSettings* 參數。請使用格式 `Set-POPSettings -ExternalConnectionSetting {<FQDN>:995:SSL}`。例如，如果您希望使用 FQDN Dublin01.Contoso.com 透過伺服器連線，以便能夠查詢自己的 POP 設定，請執行 `Set-PopSettings -ExternalConnectionSetting {Dublin01.Contoso.com:995:SSL}`。
    
    套用此設定後，需重新啟動 IIS。

  - **IMAP4 設定**   執行**Set-IMAPSettings** Cmdlet 和 *ExternalConnectionSettings* 參數。請使用格式 `Set-ImapSettings -ExternalConnectionSetting {<FQDN>:993:SSL}`。例如，如果您希望使用 FQDN Dublin01.Contoso.com 透過伺服器連線，以便能夠查詢自己的 IMAP 設定，請執行 `Set-IMAPSettings -ExternalConnectionSetting {Dublin01.Contoso.com:993:SSL}`。
    
    套用此設定後，需重新啟動 IIS。

  - **SMTP 設定**   執行 **Set-ReceiveConnector** Cmdlet 和 *AdvertiseClientSettings* 參數。請使用格式 `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN <FQDN>`。例如，如果您希望使用 FQDN Dublin01.Contoso.com 透過伺服器連線，以便能夠查詢自己的 SMTP 設定，請執行 `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN Dublin01.Contoso.com`。
    
    套用此設定後，需重新啟動 IIS。

透過執行 **Set-POPSettings**、**Set-IMAPSettings** 和 **Set-ReceiveConnector** 指令程式變更預設設定之後，使用者就可以在 Outlook Web App 中，按一下 \[設定\] \> \[選項\] \> \[帳戶\] \> \[我的帳戶\] \> \[POP 或 IMAP 存取的設定\]，來查詢他們的外部 POP、IMAP 與 SMTP 伺服器設定。

**在伺服器上保留郵件的副本**

某些電子郵件程式上的預設值，是設為當您擷取郵件之後，會從伺服器移除訊息。請記得要建議使用者，務必將電子郵件程式設為當用戶端從伺服器擷取郵件之後，保留一份副本在伺服器上。保留一份郵件副本在伺服器上，可讓您的使用者從其他電子郵件程式存取郵件。


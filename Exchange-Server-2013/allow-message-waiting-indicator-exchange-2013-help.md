---
title: '允許郵件等待指示器: Exchange 2013 Help'
TOCTitle: 允許郵件等待指示器
ms:assetid: 57fb439e-8208-499f-a20b-814677843a8c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298001(v=EXCHG.150)
ms:contentKeyID: 54652584
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允許郵件等待指示器

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-03-09_

訊息等待指示器 (MWI) 是在大部分的舊版的語音信箱系統中找到的功能。它可讓使用者知道有新的或技術面貌語音郵件訊息。在其最常見的表單中，這項功能 lights 燈表示新的或技術面貌語音訊息平台服務使用者的電話上。

**目錄**

概觀

The Mailbox server's role in MWI

MWI SIP NOTIFY messages

MWI resilience

MWI administration

Text message (SMS) notifications for voice mail messages and missed calls

## 概觀

MWI 通知可以包含任何其他機制，表示新的或技術面貌語音訊息存在。訊息可以在新的電子郵件訊息或已標記為未讀取的其中一個。MWI 通知可能會採取任何一種格式：

  - Microsoft Outlook 或 Outlook Web App 中的新語音訊息。

  - 傳送到已設定為接收文字訊息之行動電話的文字或短訊服務 (SMS) 訊息。

  - 從 Exchange 整合通訊 (UM) 撥出的電話。

  - 電話上的燈號。

  - 特殊撥號音。

  - 電話顯示螢幕上的圖示或按鈕。

  - 軟體應用程式內反白顯示的通知。

整合通訊中使用者的語音信箱會儲存在他們的信箱。從使用Outlook語音存取電話、 使用Outlook或Outlook Web App、 桌面或攜帶型電腦和行動電話用戶端可以存取它。當使用者會收到新的語音訊息時，會出現訊息其語音信箱搜尋資料夾中。如果語音訊息用於存取Outlook或Outlook Web App、 電子郵件訊息會包含語音訊息。

當舊版 UM 部署在組織中時，MWI 傳統的 VoIP 閘道環境或 IP PBX 環境中支援使用協力廠商的解決方案或應用程式，或已加入為 Exchange UM。在 Exchange 2010 或更新版本、 MWI 也時所支援的 UM 部署與 Microsoft Lync Server。Lync Server 所使用的 MWI 通知機制取決於 VoIP 電話的使用 Enterprise Voice 並已啟用 UM 的使用者，而且可以位於下列任何一種：

  - 電話

  - 電話顯示螢幕

  - 撥號鍵台按鈕

根據預設，MWI 會開啟之所有已啟用 UM 的使用者。它會透過建立及連結至 UM 撥號對應表的 UM IP 閘道或 UM 信箱原則上設定控制。MWI 也適用於受保護的語音訊息。

若要實作與 VoIP 閘道、 IP Pbx 或已啟用 SIP 的 Pbx 的傳統電話語音環境中執行 Microsoft Exchange 整合通訊服務傳送 MWI 工作階段初始通訊協定 (SIP) 通知訊息至*SIP 對等*，這是其中一個 IP PBX、 VoIP 閘道與舊版的 PBX 搭配使用的信箱伺服器已啟用 SIP 的 PBX，或如果您已部署 Lync Server、 Lync 伺服器會被視為 SIP 對等。IP PBX 或 PBX lights 燈上桌上電話通知新的或技術面貌語音訊息的使用者。

有兩種來電者可以留下語音訊息的方式： 使用自動答錄和Outlook語音存取。使用來電接聽、 信箱伺服器接聽來電，並讓來電者留下語音訊息給使用者。使用Outlook語音存取，當來電者撥打 Outlook 語音存取號碼，他們可以使用功能表系統留下語音訊息給已啟用 UM 的使用者。

回到頁首

## Mailbox Server 在 MWI 中的角色

當來電者撥話給已啟用 UM 的使用者與使用者不會接聽電話時，在信箱伺服器上的 Microsoft Exchange 整合通訊服務會接收 MWI 狀態變更資訊並變更的通知的要求傳送至 VoIP 閘道、 IP PBX 或已啟用 SIP 的 PBX 會使用 SIP 通知訊息。變更的通知包含下列資訊：

  - 啟用等待訊息指示器 (是或否)。

  - 新語音訊息或標示為未聽取之語音訊息的數目。

  - 舊語音訊息或標示為已聽取之語音訊息的數目。

  - 新緊急語音訊息或標示為未聽取之緊急語音訊息的數目。

  - 舊緊急語音訊息或標示為已聽取之緊急語音訊息的數目。

  - 主要 UM 撥號對應表上的主要分機號碼。

  - 要對 SIP NOTIFY 訊息使用之 SIP 對等的 IP 位址或完整網域名稱 (FQDN)。

  - 安全性類型的 um 撥號對應表 （「 不安全 」、 SIP 安全 」 或 「 安全 」）。此資訊會用來決定是否 VoIP 閘道或 IP PBX 連線必須是 SIP over TCP\] 或 \[SIP over TLS。MWI SIP 通知支援傳輸層安全性 (TLS)。

在信箱伺服器會使用 history-info 資訊來電頁首上判斷已啟用 UM 之使用者的電話號碼或分機號碼。當副檔名或電話號碼決定時，Mailbox server 會將要求傳送至 SIP 對等。SIP 對等再變更 MWI 狀態並開啟使用者的電話上的通知。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然 PBX 中斷應極少、 UM 自動重新整理每個信箱的 MWI 狀態至少一次每隔 12 小時。沒有強制 refresh 方法，但如果 PBX 或 IP PBX 電源關閉所有 MWI 燈都移，所有燈應為正確的狀態內都還原六個小時。</td>
</tr>
</tbody>
</table>


回到頁首

## MWI SIP NOTIFY 訊息

MWI 通知與 SIP 對等通訊使用 SIP 通知訊息。MWI 狀態變更資訊 SIP 通知訊息中包含並指出是否將 MWI 通知傳送給使用者。MWI 狀態變更時，信箱助理員將此資訊傳送至執行 Mailbox server 上的 Microsoft Exchange 整合通訊服務。整合通訊服務會收到此資訊之後，它會剖析來取得目標 SIP 對等和 MWI 狀態變更資訊訊息。然後郵件內文中的表單 SIP 通知訊息 MWI 狀態變更資訊並傳送到 SIP 對等此資訊。

MWI 根據 RFC 3842。RFC 3842 狀態的訊息等待通知必須使用 SIP 事件通知。MWI 為基礎的 SIP 模型，並驅動的整合的郵件傳送系統中找到之端點。SIP 端點，也稱為 \[SIP 對等的取得 MWI 資訊必須傳送 SIP 訂閱訊息至整合通訊服務。服務回覆與通知訊息，指出尚未接受訂閱。所有 MWI 狀態變更資訊將會從整合通訊系統都傳達給使用先前建立的訂閱中內嵌的通知郵件的 SIP 端點。SIP 通知訊息傳送給 SIP 對等的確切的語法。會根據 RFC 3842 所述的格式。

當信箱伺服器上的 Unified Messaging 服務傳送至 SIP 對等 MWI 通知訊息時、 事件標頭是設定為"訊息-summary"，這表示這是 MWI 相關通知訊息。標頭\] 欄位會指出必須提供 MWI 服務的 SIP 端點。訂閱狀態標頭必須設為 「 終止 」，而不是 「 使用時間 」。為了回應 SIP 通知訊息中發生下列動作：

1.  SIP 對等會使用電路交換通訊協定 (例如 SMDI)，將此資訊傳達給 PBX。

2.  PBX 會透過電路交換通訊協定傳送成功訊息。

3.  SIP 對等可以回應與下列訊息： 200 \[確定\] （成功） 或 480 （暫時無法使用）。在信箱伺服器可以處理這些回應及其他失敗回應。

## 傳統電話語音環境中的 MWI

在傳統的電話語音環境中，來電會接收到 PBX 並將再傳送至 VoIP 閘道或 IP PBX 或已啟用 SIP 的 PBX 會接收。Mailbox server 和信箱助理員可用來判斷已啟用 UM 之使用者的 MWI 狀態。它們負責回到 VoIP 閘道和舊版的 PBX、 IP PBX 或已啟用 SIP 的 PBX 遞送 SIP 通知。

在傳統電話語音環境中，呼叫流程和 MWI 通知如下：

1.  來電會接收到舊版的 PBX、 轉接 VoIP 閘道或 IP PBX 或已啟用 SIP 的 PBX、，然後轉寄給啟用 UM 之使用者的分機號碼。使用者不會接聽和來電者會被提示留下語音訊息。

2.  VoIP 閘道或 IP PBX 將來電提交到執行 Microsoft Exchange 整合通訊服務的 Mailbox Server。

3.  信箱伺服器執行 LDAP 查詢來尋找已啟用 UM 之使用者的資訊，例如使用者的分機號碼及個人問候語。已啟用 UM 之使用者的問候語時會播放。

4.  由整合通訊服務建立的語音訊息會提交到相同 Mailbox Server 上的 Microsoft Exchange Transport 服務。

5.  Mailbox server 上的傳輸服務會送出至包含使用者信箱的信箱伺服器的語音訊息。在信箱助理員收到新的語音訊息的 MAPI 事件。

6.  在信箱助理員讀取計劃和 UM 信箱原則決定是否要傳送 MWI 通知給已啟用 UM 之使用者的 UM 撥號對應表。所有的信箱伺服器相關聯 UM 的信箱助理員查詢撥號對應表的已啟用 UM 的使用者。在信箱助理員會嘗試將 RPC 事件傳送至第一個信箱伺服器所傳回。如果這個失敗，它會嘗試下一個。它會保留重試中執行 5 分鐘或之前已嘗試所有 Mailbox server。如果所有的 RPC 呼叫失敗，信箱助理員錯誤事件檢視器記錄檔。信箱伺服器的查詢所有 UM IP 閘道相關聯 UM 撥號對應表的已啟用 UM 之使用者的信箱。

7.  UM 將 SIP 通知訊息傳送至第一個 VoIP 閘道或 IP PBX 從查詢傳回。如果這個失敗，Mailbox server 會選擇 \[下一步 VoIP 閘道或 IP PBX。將保留的 Mailbox server 嘗試如 VoIP 閘道或 IP PBX 五分鐘。如果所有嘗試找出 VoIP 閘道或 IP PBX 都失敗，Mailbox server 將會記錄錯誤。如果 VoIP 閘道或 IP PBX 位於成功、 VoIP 閘道就會傳送通知給 PBX、 和 PBX 接著會傳送通知 MWI 事件的亮度電話燈到使用者的電話。如果將 IP PBX，MWI 通知處理的 IP PBX 及它再將淺使用者的電話燈。其他 MWI 通知機制會列在 \[概觀\] 區段中。通知類型取決於 PBX 或 IP PBX 硬體廠商，以及是否要使用 Lync Server。它也取決於的電話類型 — 類比、 數位或 VoIP — 所使用。

回到頁首

## Lync Server 環境中的 MWI

在包含 Lync Server 電話語音環境中，來電可以是從外部的電話傳送到中繼伺服器、 從 Lync 用戶端或傳送的整合的通訊 (UC) 或其他 VoIP 型電話。接到電話時後，其會傳送到 Lync Server 前端伺服器集區。Mailbox server 和信箱助理員可用來判斷已啟用 UM 之使用者的 MWI 狀態並傳遞此通知給 Lync 用戶端類比或數位或 UC 或 VoIP 型電話。

在包含 Lync Server 的電話語音環境中，呼叫流程和 MWI 通知如下：

1.  從下列其中一項傳送呼叫：
    
      - 組織外部的電話 (傳送至中繼伺服器)
    
      - Lync 式用戶端
    
      - UC 或其他 VoIP 式電話

2.  為 Lync Server 前端伺服器集區所接收到來電並將其傳送至電話或啟用 UM 之使用者的 SIP 端點。使用者不會接聽和來電者會被提示留下語音訊息。

3.  Lync Server 前端伺服器集區會將電話提交至內部部署網路內的 Mailbox Server，並找出使用者的信箱。

4.  信箱伺服器執行 LDAP 查詢來尋找已啟用 UM 之使用者的分機號碼等問候語的資訊。播放問候語，並將來電者會被提示留下語音訊息。

5.  由整合通訊服務建立的語音訊息會提交到相同站台內相同 Mailbox Server 上的傳輸服務。

6.  傳輸服務會送出至包含使用者信箱的信箱伺服器的語音訊息。在信箱助理員收到新的語音郵件 MAPI 事件。

7.  在信箱助理員讀取 UM 撥號對應表和 UM 信箱原則決定是否應 MWI 通知傳送給使用者。信箱助理員查詢的所有信箱伺服器相關聯 UM 撥號對應表的使用者。在信箱助理員會嘗試將 RPC 事件傳送至第一個信箱伺服器所傳回。如果此嘗試失敗，請在信箱助理員嘗試下一個。它會保留嘗試執行 5 分鐘或之前的所有伺服器已都嘗試尋找信箱伺服器。如果所有的 RPC 呼叫失敗，信箱助理員會錯誤記錄在事件檢視器。信箱伺服器會查詢 Active Directory 的所有與 UM 撥號對應表已啟用 UM 之使用者的相關聯的 UM IP 閘道。

8.  UM 將 SIP 通知訊息傳送至第一個 VoIP 閘道或 IP PBX 從查詢傳回。如果這個失敗，Mailbox server 會選擇 \[下一步 VoIP 閘道或 IP PBX。信箱伺服器將會保留嘗試尋找 VoIP 閘道或 IP PBX 五分鐘。如果連絡人的 VoIP 閘道或 IP PBX 的所有嘗試都失敗，Mailbox server 將會記錄錯誤。如果成功，VoIP 閘道或 IP PBX 會傳送通知給 Lync Server 前端伺服器集區，接著會傳送給使用者、 使用者的電話或 Lync 用戶端所使用的 SIP 端點的 MWI 事件通知。

回到頁首

## MWI 恢復

如果您正在部署信箱和用戶端存取伺服器、 UM 撥號對應表和 UM IP 閘道器\] 中，您已啟用 UM 之使用者的使用 MWI，最好部署多個信箱和用戶端存取伺服器，以及多個 VoIP 閘道器、 IP Pbx 建立容錯度與台回復性。這麼做也會建立 mwi 因為它可提供多種方式傳送 MWI 通知上一節所述。

若要為整合通訊中的 MWI 啟用容錯，必須建立及設定下列一或多項：

  - 與將接收 MWI 通知之啟用 UM 功能的使用者連結的 UM 撥號對應表。

  - 與將接收 MWI 通知之啟用 UM 功能的使用者連結的 UM 信箱原則。

  - 與 UM 撥號對應表連結的 UM IP 閘道，該 UM 撥號對應表與將接收 MWI 通知之啟用 UM 功能的使用者連結。

  - 如果使用 Lync Server，則所有 Client Access Server 和 Mailbox Server 必須新增至 UM SIP URI 撥號對應表，該撥號對應表與將接收 MWI 通知之啟用 UM 功能的使用者連結。

## MWI 管理

MWI 可以管理來設定兩個 UM 元件 ︰ UM 信箱原則與 UM IP 閘道。這兩個 UM 元件，您可以啟用或停用的 Exchange 管理命令介面中使用**Set-UMMailboxPolicy**指令程式或**Set-UMIPgateway**指令程式 MWI 通知。您也可以使用 Exchange 系統管理中心 (EAC) 設定的設定。 您可以在命令介面中使用**Get-UMMailboxPolicy** cmdlet 和**Get-UMIPgateway** cmdlet 或 EAC 中檢視設定來檢視 MWI 通知的狀態。

## UM 信箱原則和 MWI

您可以建立 UM 信箱原則套用至一組已啟用 UM 之信箱的一組通用的 UM 原則設定。例如，您可以使用 UM 信箱原則套用 PIN 原則設定、 撥號限制和 MWI 通知設定。如果您啟用或停用 UM 信箱原則上的 MWI，它會啟用或停用的所有已啟用 UM 之使用者的 UM 信箱原則與連結。MWI 設定也可以套用至連結與 UM 撥號對應表之使用者的子集。若要深入了解 UM 信箱原則，包括如何啟用或停用已啟用 UM 的使用者群組的 MWI 請參閱[UM 信箱原則程序](um-mailbox-policy-procedures-exchange-2013-help.md)。

您可以在命令介面中使用 EAC 或 **Set-UMMailboxPolicy** 指令程式來配置 MWI 設定，如下表所示。

### UM 信箱原則上的等待訊息指示器設定

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>命令介面參數</th>
<th>EAC 中有可用的設定嗎？</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowMessageWaitingIndicator</em></p></td>
<td><p>是</p></td>
<td><p><em>AllowMessageWaitingIndicator</em>參數會指定連結與 UM 信箱原則的使用者是否能在收到新的語音郵件時所收到的 MWI 通知。預設值為<code>$true</code>。</p>
<p>啟用此設定時，MWI 通知傳送給連結與 UM IP 閘道器所採取的來電單一 UM 信箱原則的使用者。此設定可讓接收及傳送 SIP 通知訊息給已啟用 UM 之使用者的電話或 SIP 端點之 UM IP 閘道。</p>
<p></p></td>
</tr>
</tbody>
</table>


如需如何管理 UM 信箱原則的 MWI 設定的詳細資訊，請參閱下列主題：

  - [管理 UM 信箱原則](manage-a-um-mailbox-policy-exchange-2013-help.md)

  - [為使用者啟用訊息等待指示器 (MWI)](enable-message-waiting-indicator-mwi-for-users-exchange-2013-help.md)

  - [停用使用者訊息等待指示器 (MWI)](disable-message-waiting-indicator-mwi-for-users-exchange-2013-help.md)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/zh-tw/library/bb124903\(v=exchg.150\))

## UM IP 閘道和 MWI

如果您停用 UM IP 閘道器上的 MWI，將會停用所有使用者連線到 VoIP 閘道或 IP PBX 的 UM IP 閘道所表示的 MWI 的通知。停用單一的 UM IP 閘道的已連結至 UM 撥號對應表上的 MWI 可以停用所有已啟用 UM 的使用者與單一或多個 UM 撥號對應表或單一或多個 UM 信箱原則關聯的 MWI 通知。若要深入了解 UM 信箱原則，包括如何啟用或停用已啟用 UM 的使用者群組的 MWI 請參閱[管理 UM 信箱原則](manage-a-um-mailbox-policy-exchange-2013-help.md)。

您可以在命令介面中使用 EAC 或 **Set-UMMailboxPolicy** 指令程式來配置 MWI 設定，如下表所示。

### UM IP 閘道上的等待訊息指示器設定

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>命令介面參數</th>
<th>EAC 中有可用的設定嗎？</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>MessageWaitingIndicatorAllowed</em></p></td>
<td><p>是</p></td>
<td><p><em>MessageWaitingIndicatorAllowed</em>參數會指定是否啟用 UM IP 閘道允許 SIP 通知訊息傳送給使用者相關聯 UM 撥號對應表。預設值為<code>$true</code>。</p>
<p>啟用此設定時，可以傳送語音信箱簡訊通知給使用者的 UM IP 閘道所接聽的來電。此設定可讓傳送訊息等待通知給已啟用 UM 之使用者的 UM IP 閘道。</p></td>
</tr>
</tbody>
</table>


如需如何管理 MWI 設定的詳細資訊，請參閱下列主題：

  - [管理 UM IP 閘道器](manage-a-um-ip-gateway-exchange-2013-help.md)

  - [允許郵件等待指示器 (MWI) 上的 UM IP 閘道](allow-message-waiting-indicator-mwi-on-a-um-ip-gateway-exchange-2013-help.md)

  - [防止訊息等待指示器 (MWI) 上的 UM IP 閘道](prevent-message-waiting-indicator-mwi-on-a-um-ip-gateway-exchange-2013-help.md)

  - [Set-UMIPGateway](https://technet.microsoft.com/zh-tw/library/aa996577\(v=exchg.150\))

回到頁首

## 語音信箱訊息和未接來電的簡訊 (SMS) 通知

如先前所述，MWI 通知是表示新的語音郵件訊息存在任何機制。除了已討論的機制，使用者可以具有語音訊息等待透過文字訊息，也稱為 SMS （短訊息服務） 訊息的通知。這是針對較傳統淺掃描或其他機制的新語音訊息 MWI 通知不同類型。

當來電者會保留新的語音訊息的文字訊息會傳送到使用者的行動電話。使用者也可以接收簡訊通知他們他們錯過撥打的電話及語音訊息不留時。未接的來電通知的文字訊息可以傳送給以及新的語音信箱通知使用者。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>傳送給使用者的簡訊包括語音信箱預覽。</td>
</tr>
</tbody>
</table>


文字訊息通知的 UM IP 閘道或 UM 信箱原則上使用比 MWI 設定不同的設定。UM 信箱原則與 UM 信箱上所設定的新語音信箱和未接的來電的文字訊息通知。您可以啟用或停用的命令介面中使用**Set-UMMailboxPolicy** cmdlet 和**Set-UMMailbox** cmdlet 文字訊息通知。您可以使用**Get-UMMailboxPolicy**指令程式和**Get-UMMailbox**指令程式來檢視的文字訊息通知的狀態。您不可以在 EAC 中設定文字訊息通知。

下表展示 UM 信箱上的參數，您必須設定這些參數，使用者才能收到語音郵件和未接來電通知簡訊：

### 使用者信箱上的簡訊通知設定

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><em>UMSMSNotificationOption</em></p></td>
<td><p>否</p></td>
<td><p><em>UMSMSNotificationOption</em>參數會指定是否已啟用 UM 的使用者可以接收僅、 語音信箱文字訊息通知的語音信箱和未接的來電或不允許收到通知。此參數的值是： <code>VoiceMail</code>、 <code>VoiceMailAndMissedCalls</code>，以及<code>None</code>。預設值為<code>None</code>。</p>
<p></p></td>
</tr>
</tbody>
</table>


如需如何管理使用者信箱上之簡訊通知設定的詳細資訊，請參閱下列主題：

  - [管理使用者的語音郵件設定](manage-voice-mail-settings-for-a-user-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/zh-tw/library/bb124893\(v=exchg.150\))

下表展示 UM 信箱原則上的參數，您必須設定這些參數，使用者才能收到語音郵件和未接來電通知簡訊：

### UM 信箱原則上的簡訊和未接來電通知設定

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>命令介面參數</th>
<th>EAC 中有可用的設定嗎？</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowSMSNotification</em></p></td>
<td><p>否</p></td>
<td><p><em>AllowSMSNotification</em>參數會指定是否已啟用 UM 之使用者的信箱關聯的 UM 信箱原則允許接收其行動電話上的文字訊息通知。如果此參數設為<code>$true</code>，也必須使用<strong>Set-UMMailbox</strong>指令程式並將<em>UMSMSNotificationOption</em>參數設為<code>voicemail</code>或<code>VoiceMailAndMissedCalls</code>已啟用 UM 的使用者。預設值為<code>$true</code>。</p>
<p></p></td>
</tr>
</tbody>
</table>


如需如何管理簡訊通知設定的詳細資訊，請參閱下列主題：

  - [管理 UM 信箱原則](manage-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/zh-tw/library/bb124903\(v=exchg.150\))

若要讓語音郵件和未接來電的簡訊通知正常運作，您必須執行以下工作：

1.  使用 EAC 或命令介面為使用者啟用 UM，並使其連結正確的 UM 信箱原則。

2.  連結至使用者的 UM 信箱原則\] 確認*AllowSMSNotification*參數會設為`$true`。若要將參數設定為`$true`，執行下列命令： `Set-UMMailboxPolicy -id MyUMMailboxPolicy - AllowSMSNotification $true`。

3.  在使用者的信箱上，將 *UMSMSNotificationOption* 參數設為 `VoiceMailAndMissedCalls` 或 `VoiceMail` 以啟用簡訊通知。

4.  預設值是`None`，因為您必須從命令介面中執行下列命令並將文字訊息通知選項設定為`VoiceMailAndMissedCalls`或`VoiceMail`。例如： `Set-UMMailbox- -id MyUMMailbox -UMSMSNotificationOption VoiceMailAndMissedCalls`。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您必須將 UM 信箱原則上的 <em>AllowSMSNotification</em> 參數和使用者信箱上的 <em>UMSMSNotificationOption</em> 參數設為 <code>$true</code>，SMS 通知才能運作。</td>
    </tr>
    </tbody>
    </table>


除了您設定 UM 信箱原則與使用者的信箱啟用新的語音信箱和未接的來電的文字訊息通知使用者必須啟用並設定文字訊息通知時登入 Outlook Web App。若要安裝及設定文字訊息通知，使用者必須：

1.  登入 Outlook Web App 並前往 **\[選項\]** \> **\[電話\]** \> **\[語音信箱\]**。

2.  在 **\[語音信箱\]** 頁面的 **\[通知\]** 下，按一下 **\[設定通知\]**。

3.  在 **\[簡訊\]** 頁面中按一下 **\[開啟通知\]** 按鈕。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請勿按下 <strong>[語音信箱通知]</strong>，否則您將會返回 <strong>[語音信箱]</strong> 頁面。</td>
    </tr>
    </tbody>
    </table>


4.  在 **\[簡訊\]** 頁面的 **\[地區設定\]** 下，使用下拉式清單來選取簡訊行動電信業者的地區設定或位置。

5.  在 **\[簡訊\]** 頁面的 **\[行動電信業者\]** 下，使用下拉式清單來選取簡訊行動電信業者，接著按 **\[下一步\]**。

6.  在**文字郵件**\] 頁面的 \[**輸入您的電話號碼，按一下 \[下一步\]**方塊中，輸入用於文字訊息通知的行動電話號碼然後再按 \[**下一步**。6 位數密碼會傳送至行動電話。如果您沒有收到密碼，請按一下 \[**我沒有收到密碼和需要傳送一次**。

7.  在 **\[密碼\]** 方塊中輸入密碼，然後按一下 **\[完成\]**。

8.  使用者可讓文字訊息通知之後，他們可以**設定語音信箱簡訊通知**頁面上按一下 \[**簡訊**。將會採取語音信箱\] 頁面上，他們可以在其中捲動至 \[**通知**\] 區段和未接的來電和語音信箱文字訊息通知選項設定的備份。

回到頁首


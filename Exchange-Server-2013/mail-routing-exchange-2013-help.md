---
title: '郵件路由: Exchange 2013 Help'
TOCTitle: 郵件路由
ms:assetid: 6fd39079-9655-4fd9-9269-c7462c76e0a7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998825(v=EXCHG.150)
ms:contentKeyID: 50473457
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 郵件路由

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

在您 Microsoft Exchange Server 2013 的組織中，所有信箱伺服器的傳輸服務之主要工作，是將接收自使用者和外部來源的郵件路由傳送至其最終目的地。路由決策是在郵件分類期間完成的。分類程式是信箱伺服器的傳輸服務的元件之一，會處理所有內送郵件，並根據目的地的相關資訊決定如何處理郵件。

現在，在 Exchange 2013 中路由傳送可完全知悉資料庫可用性群組 (DAG)，並將 DAG 成員資格作為路由界限。為什麼？在 Exchange 2013 中，所有的信箱伺服器均可提供傳輸服務。因此，當信箱伺服器隸屬於一個 DAG 時，路由傳送郵件的主要機制就會密切對應該 DAG。而且，當一個 DAG 的範圍跨越多個 Active Directory 站台時，將 Active Directory 站台作為主要的路由界限就顯得沒有效率。Exchange 2013 也將 Active Directory 站台的成員資格作為非隸屬於 DAG 之 Mailbox Server 的路由界限，以及與舊版 Exchange 的路由互通性。Exchange 2013 路由的其他重大變更包括：

  - 信箱伺服器上的傳輸服務絕不會直接與信箱資料庫進行通訊。相反地，傳輸服務會與信箱伺服器上的傳輸服務進行通訊。僅有信箱傳輸服務會與本機信箱伺服器上的信箱資料庫進行通訊。當信箱伺服器為 DAG 成員時，唯有擁有該信箱資料庫之主動副本的信箱伺服器之傳輸服務能接受該目的地收件者的郵件。

  - 唯有傳送郵件至本機信箱資料庫或從該處接收郵件時，信箱傳輸服務才會使用遠端程序呼叫 (RPC)。當信箱伺服器為 DAG 成員時，信箱傳輸服務僅會使用 RPC 與本機中的該信箱資料庫的主動副本進行通訊。換言之，RPC 絕不會用於跨伺服器通訊。相反地，信箱傳輸服務和不同信箱伺服器的傳輸服務一定會使用 SMTP 進行通訊。

  - 若為遠端目的地，Exchange 2013 會使用較精確的佇列作業。Exchange 2013 會針對 Active Directory 站台中特定的目的地 (例如個別傳送連接器) 將郵件加入佇列，而非針對遠端 Active Directory 站台中所有的目的地都使用同一個佇列。

  - 連結的連接器已過時。連結的連接器是連結到傳送連接器的接收連接器。所有由接收連接器接收的郵件已自動轉送至傳送連接器。

**目錄**

路由元件

  - 路由目的地

  - 傳遞群組

  - 佇列

路由傳送郵件

  - 在 Acitve Directory 站台之間路由傳送郵件

  - Client Access Server 的前端傳輸服務中的路由

  - Mailbox Server 的信箱傳輸服務中的路由

  - Edge Transport Server 的傳輸服務中的路由

## 路由元件

當 Exchange 2013 信箱伺服器上的傳輸服務收到郵件時，必須將該封郵件分類。郵件分類的第一個階段是解析收件者。完成解析收件者之後，便可以決定最終目的地。下一個階段為路由傳送，需決定到達目的地的最佳途徑。藉由引進路由目的地和傳遞群組的概念，Exchange 2013 中的路由功能已經通用化，以提供更佳的彈性和更低的複雜度。

## 路由目的地

在 Exchange 2013 中，郵件的最終目的地稱為*路由目的地*。以下為 Exchange 2013 中的路由目的地：

  - **信箱資料庫**   這是任何在 Exchange 組織的郵件伺服器中擁有信箱之收件者的路由目的地。在 Exchange 2013 中，公用資料夾是一種信箱類型，因此，將郵件路由傳送至公用資料夾收件者，等同將郵件路由傳送至信箱收件者。

  - **連接器**   將連接器作為路由路徑使用時，連接器即為 SMTP 郵件的傳送連接器。傳遞代理程式連接器或外部連接器是作為非 SMTP 郵件的路由路徑使用。

  - **通訊群組擴充伺服器**   此為將一個擴充伺服器指派給一個通訊群組，以擴充該群組成員資格清單時的路由路徑。通訊群組擴充伺服器必為一台集線傳輸伺服器或一台 Exchange 2013 信箱伺服器。

請注意，在舊版的 Exchange 中同樣找得到這些路由目的地。

回到頁首

## 傳遞群組

Exchange 2013 中的每一個路由目的地均有一個包含一台或多台傳輸伺服器的集合，負責將郵件傳遞至該路由目的地。我們稱此傳輸伺服器集合為*傳遞群組*。傳輸伺服器可以是 Exchange 2013 Mailbox Server，或是已安裝 Hub Transport server role 的 Exchange 2010 伺服器或 Exchange 2007 伺服器。當路由目的地為一個信箱資料庫時，傳遞群組中的傳輸伺服器使用與該信箱伺服器相同版本的 Exchange。當路由目的地為一個連接器或一個通訊群組擴充伺服器時，該傳遞群組可能同時包含 Exchange 2013 Mailbox Server 和 Exchange 2010 或 Exchange 2007 Hub Transport Server。郵件採何種方式路由傳送須視來源傳輸伺服器和目的地傳遞群組之間的關係而定：

  - 如果來源傳輸伺服器位於目的地傳遞群組之內，路由目的地本身即為郵件的下一個躍點。郵件會由來源傳輸伺服器傳遞至傳遞群組中的傳輸伺服上的信箱資料庫或連接器。請注意，當通訊群組擴充伺服器為路由目的地時，通訊群組在郵件進入通訊群組擴充伺服器上的分類路由階段之前就已完成擴充。因此，通訊群組擴充伺服器的路由目的地必為信箱資料庫或連接器。

  - 如果來源傳輸伺服器位於目的地傳遞群組之外，則將沿著最低成本路由路徑將郵件轉送至目的地傳遞群組。依據 Exchange 拓撲的規模和複雜性而定，郵件會沿著最低成本路由路徑轉送至其他傳輸伺服器，或直接將郵件轉送至該目的地傳遞群組內的傳輸伺服器。

以下為 Exchange 2013 中的傳遞群組：

  - **可路由 DAG**   此為隸屬於一個 DAG 的 Exchange 2013 信箱伺服器集合。DAG 內的信箱資料庫為此傳遞群組提供服務的路由目的地。當郵件送達隸屬於該 DAG 的信箱伺服器上的傳輸服務時，該傳輸服務會將郵件路由傳送至目前擁有該目的地信箱資料庫主動副本之 DAG 內的信箱伺服器之信箱傳輸服務。接著，目的地信箱伺服器上的信箱傳輸服務會將郵件傳遞至本機信箱資料庫。雖然 DAG 可能包含位於不同 Active Directory 站台的信箱伺服器，該 DAG 仍為傳遞群組界限。

  - **信箱傳遞群組**   這是位於相同 Active Directory 站台且擁有相同版本的 Exchange 伺服器集合。該 Active Directory 站台為傳遞群組界限。Active Directory 站台內主要發行版本的 Exchange 會將路由目的地和為其提供服務的傳遞群組分開。Active Directory 站台中的 Exchange 2010 集線傳輸伺服器會為位於 Exchange 2010 信箱伺服器上的信箱資料庫提供服務。Active Directory 站台中的 Exchange 2007 集線傳輸伺服器會為位於 Exchange 2007 信箱伺服器上的信箱資料庫提供服務。Active Directory 站台之 Exchange 2013 信箱伺服器上的傳輸服務會為位於非隸屬於 DAG 的 Active Directory 站台之 Exchange 2013 信箱伺服器上的信箱資料庫提供服務。郵件傳遞至信箱資料庫的方式需視 Exchange 的版本而定：
    
      - **Exchange 2013**   當郵件送達目的地 Active Direction 站台內的目的地信箱伺服器之後，傳輸服務會使用 SMTP 將該郵件傳輸至信箱傳輸服務。接著，信箱傳輸服務會使用 RPC 將該郵件傳遞至本機信箱資料庫。
    
      - **Exchange 2010 或 Exchange 2007**   當郵件送達目的地 Active Direction 站台內相同版本的一個隨機 Hub Transport Server 之後，Hub Transport Server 上的儲存區驅動程式會使用 RPC 將該郵件寫入信箱資料庫。

  - **連接器來源伺服器**   此為混合 Exchange 2010 或 Exchange 2007 Hub Transport Server 或 Exchange 2013 Mailbox Server 的集合，這些伺服器均已界定為傳送連接器、傳遞代理程式連接器或外部連接器的來源伺服器。該連接器為此路由群組提供服務的路由目的地。當連接器被界定至一個特定伺服器時，唯有該伺服器可以將郵件路由傳送至該連接器所定義的目的地。此傳遞群組可能包含位於不同 Active Directory 站台的 Exchange 2010 或 Exchange 2007 或 Hub Transport Servers，或 Exchange 2013 Mailbox Server。

  - **AD 站台**   在一些情況下，Active Directory 站台並非郵件的最終目的地，但是該郵件仍必須通過該 Active Directory 站台內的 Exchange 2010 或 Exchange 2007 Hub Transport Server 或 Exchange 2013 Mailbox Server。那些情況包括：
    
      - 當該 Active Directory 已設定為中樞站台時。每當供郵件傳遞使用的最低成本路由路徑沿途有中樞站台存在時，在將郵件轉送到其最終目的地之前，郵件會進入中樞站台內傳輸伺服器的佇列，並由該傳輸伺服器處理。
    
      - 將 Edge Transport Server 訂閱至 Active Directory 站台時。這些已訂閱的邊際傳輸伺服器不能直接由其他的 Active Directory 站台存取。請注意，Edge Transport Server 可以是 Exchange 2013、Exchange 2010 或 Exchange 2007。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>當傳遞群組為 Active Directory 站台時，僅會使用延遲展開傳送。當多個收件者共用最低成本路由路徑的任何部分時，延遲展開傳送會嘗試減少郵件傳輸數量。</td>
    </tr>
    </tbody>
    </table>


  - **伺服器清單**   此為一或多個已設定為通訊群組擴充伺服器的 Exchange 2010 或 Exchange 2007 Hub Transport Server 或 Exchange 2013 Mailbox Server 的集合。此通訊群組擴充伺服器為此傳遞群組提供服務的路由目的地。

傳遞群組成員資格不會相互排斥。例如，一個隸屬於 DAG 成員的 Exchange 2013 信箱伺服器也可以是一個受界定的傳送連接器之來源伺服器。此信箱伺服器可隸屬於 DAG 內信箱資料庫的可路由 DAG 傳遞群組，也可以是受界定的傳送連接器之連接器來源伺服器傳遞群組。

下表將路由目的地對應至基於有關 Exchange 版本的傳遞群組：


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Exchange 2013 Mailbox Server</th>
<th>Exchange 2010 或 Exchange 2007 Hub Transport Server</th>
<th>周邊網路中的 Edge Transport Server</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DAG 內的信箱資料庫</p></td>
<td><p>可路由的 DAG</p></td>
<td><p>信箱傳遞群組</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>不在 DAG 內的信箱資料庫</p></td>
<td><p>信箱傳遞群組</p></td>
<td><p>信箱傳遞群組</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>連接器</p></td>
<td><p>連接器來源伺服器</p></td>
<td><p>連接器來源伺服器</p></td>
<td><p>AD 站台</p></td>
</tr>
<tr class="even">
<td><p>通訊群組擴充伺服器</p></td>
<td><p>伺服器清單</p></td>
<td><p>伺服器清單</p></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


回到頁首

## 佇列

從傳送伺服器的觀點來看，每個傳遞佇列均代表特定郵件的目的地。當 Exchange 2013 信箱伺服器的傳輸服務選擇郵件的目的地之後，目的地就會以 **NextHopSolutionKey** 屬性的形式，在收件者上加上戳記。如果有一封郵件要傳送給多位收件者，那麼每一位收件者都會有 **NextHopSolutionKey** 屬性。接收伺服器也會執行郵件分類，並將郵件放入佇列以等候傳遞。郵件放入佇列之後，您可以檢查特定佇列的傳遞類型，以判斷郵件是否會在抵達下一個躍點目的地時再次進行轉送。**NextHopSolutionKey** 屬性的每個唯一值相當於一個個別的傳遞佇列。

如需詳細資訊，請參閱[佇列](queues-exchange-2013-help.md)主題的「NextHopSolutionKey」一節。

回到頁首

## 路由傳送郵件

當必須將一封郵件傳遞至遠端傳遞群組時，必須替該郵件決定一條路由路徑。Exchange 2013 使用以下邏輯選擇一封郵件的路由路徑。此還輯基本上和 Exchange 2010 沒有差異：

1.  加總必須周遊才能到達目的地之 IP 站台連結的成本，來計算最低成本路由路徑。如果目的地是連接器，指派給位址空間的成本也要加總至到達所選取連接器的成本中。如果可行的路由路徑有數條，則會使用彙總成本最低的路由路徑。

2.  如果有多條路由路徑的彙總成本相同，則會評估每個路徑中的躍點數量，然後使用躍點數量最少的路由路徑。

3.  如果仍有多條路由路徑可用，就會考量在目的地之前的 Active Directory 站台所獲指派的名稱。Active Directory 站台最接近目的地且英數字元順序最低的路由路徑會獲得採用。如果對於受評估的所有路由路徑而言，最接近目的地的站台是相同的，則會考慮使用字元順序較優先的站台名稱。

在 Exchange 2010 中，每個郵件收者僅可與一個 Active Directory 站台建立關聯，且從來源 Active Directory 站台至目的地 Active Directory 站台僅有一個最低成本路由路徑。在 Exchange 2013 中，傳遞群組的範圍可能跨越多個 Active Directory 站台，且可能會有多條最低成本路由路徑可通往那些 Active Directory 站台。Exchange 2013 會將該目的地傳遞群組內的單一 Active Directory 站台指定為*主要站台*。根據前述的路由邏輯，主要站台是最接近的 Active Directory 站台。為能成功地在傳遞群組之間路由傳送郵件，Exchange 2013 會考慮以下問題：

  - **最低成本路由路徑上有一個或多個中樞站台**   如果通往主要站台的最低成本路由路徑含有任何中樞站台，該郵件則必須經由該中樞站台路由傳送。已選擇最低成本路由路徑上最接近的中樞站台作為類型 **AD site** 的新傳遞群組，這包含該中樞站台內所有的傳輸伺服器。在郵件周遊中樞站台之後，會繼續沿著最低成本路由路徑路由傳送郵件。如果主要站台正好為中樞站台，基於以下原因仍會視該主要站台為中樞站台：
    
      - 如果目的地傳遞群組跨越多個 Active Directory 站台，則來源伺服器應該只會嘗試與該中樞站台內的伺服器建立連線。
    
      - 優先選擇該中樞站台內實際隸屬於該目標傳遞群組的伺服器。
    
    與舊版 Exchange 相同，任何不在通往主要站台的最低成本路由路徑上之中樞站台均會予以忽略。

  - **目的地路由群組中可選的目標 Exchange 伺服器**   當目的地傳遞群組跨越多個 Active Directory 站台時，通往該傳遞群組內特定伺服器的路由路徑可能會有不同的成本。根據最低成本路由路徑，位於最接近的 Active Directory 站台中的伺服器會被選為該傳遞群組的目標伺服器，而那些伺服器所在的 Active Directory 站台會被選為主要站台。

  - **當嘗試連線至目的地路由群組中所有伺服器失敗時的後援選項**   如果目的地傳遞群組跨越多個 Active Directory 站台，則第一個後援選項為其他 Active Directory 站台的目的地傳遞群組中未被選為目標伺服器的所有其他伺服器。伺服器是根據通往那些 Active Directory 站台的路由路徑之成本進行選擇的。如果目的地傳遞群組有任何一台伺服器位於本機 Active Directory 站台內，由於郵件已非常接近目標路由目的地，因此不會有其他的後援選項。如果目的地傳遞群組有伺服器位於遠端 Active Directory 站台內，選項則為嘗試與該主要站台內的所有其他伺服器建立連線。如果失敗，則會使用通往主要站台的最低成本路由路徑中的輪詢路徑。Exchange 2013 會在連線建立之前，嘗試透過輪詢，一個躍點接著一個躍點，順著最低成本的路由路徑，盡可能地將郵件傳送至最接近的目的地上。

回到頁首

## 在 Acitve Directory 站台之間路由傳送郵件

Exchange 2013 在 Active Directory 站台之間路由傳送郵件的方法幾乎與 Exchange 2010 相同。如需詳細資訊，請參閱[Active Directory 站台之間路由傳送郵件](route-mail-between-active-directory-sites-exchange-2013-help.md)。

回到頁首

## Client Access Server 的前端傳輸服務中的路由

這作為 Exchange 2013 組織之所有輸入與 (選擇性) 輸出外部 SMTP 流量的無狀態 Proxy。若為外寄郵件，傳輸服務會使用傳送連接器與用戶端存取伺服器上的前端傳輸服務進行通訊。尤其是，將可適用傳送連接器上的 *FrontEndProxyEnabled* 參數設定為 `$true` 時，或在 Exchange 系統管理中心 (EAC) 的 \[傳送連接器\] 內容中選取 **\[透過 Client Access Server 代理\]** 選項時，就會透過前端傳輸服務來代理外寄郵件。將會選取本機 Active Directory 站台中的任何 Client Access Server。請注意，前端傳輸服務沒有傳送連接器。

若為內送郵件，無論收件者的數量或類型為何，前端傳輸服務均必須在信箱伺服器上快速找到一個運作狀態良好的單一傳輸服務來接收郵件傳輸。若未能達成，將會讓外部寄件者認為無法使用電子郵件服務。如同傳輸服務，前端傳輸服務會根據來自 Active Directory 的資訊載入路由表，並使用傳遞群組來判定路由傳送郵件的方法。不過，前端傳輸服務所使用的路由表具有以下的獨特特性：

  - 即使同一台實體伺服器中已安裝信箱伺服器和用戶端存取伺服器，也不會視前端傳輸服務為傳遞群組的成員。這會迫使前端傳輸服務僅能與傳輸服務進行通訊。

  - 路由表不含任何傳送連接器路線。

  - 路由表包含一份本機 Active Directory 站台中信箱伺服器的特殊清單，其目的在於快速進行容錯轉移。

在前端傳輸服務中進行路由傳送能夠解析信箱資料庫的郵件收件者。前端傳輸服務所使用的信箱伺服器清單是根據郵件收件者的信箱資料庫而建立的。請注意，有可能會發生沒有任何收件者擁有信箱的情況，例如，如果收件者是通訊群組或郵件使用者。前端傳輸服務會針對每一個信箱資料庫查詢傳遞群組和相關路由資訊。前端傳輸服務所使用的傳遞群組為：

  - 可路由的 DAG

  - 信箱傳遞群組

  - AD 站台

根據收件者的數量和類型，前端傳輸服務會執行下列其中一個操作：

  - 針對寄給單一信箱收件者的郵件，請在目標傳遞群組中選取信箱伺服器，然後根據 Active Directory 站台的距離設定信箱伺服器的優先順序。將郵件路由至收件者可能會透過中樞站台路由郵件。

  - 針對寄給多個信箱收件者的郵件，請根據 Active Directory 站台的距離，使用前 20 個收件者來選取最近傳遞群組中的信箱伺服器。請注意，前端傳輸不會出現郵複本發送，因此，不論郵件中的收件者數量為何，最終也僅會選取一個信箱伺服器。

  - 如果該郵件未含信箱收件者，在本機 Active Directory 站台中任選一台信箱伺服器。

回到頁首

## Mailbox Server 的信箱傳輸服務中的路由

這包含兩個不同的服務：Mailbox Transport Submission 服務和 Mailbox Transport Delivery 服務。若為內送郵件，信箱傳輸傳遞服務會從傳輸服務接收 SMTP 郵件，並使用 RPC 與信箱資料庫建立連線來傳遞郵件。若為外寄郵件，信箱傳輸提交服務會使用 RPC 與本機信箱資料庫建立連線來擷取郵件，並透過 SMTP 將郵件提交至傳輸服務。信箱傳輸服務是無狀態的，且不會在本機上產生任何郵件佇列。

如同傳輸服務，信箱傳輸服務會根據來自 Active Directory 的資訊載入路由表，並使用傳遞群組來判定路由傳送郵件的方法。不過，信箱傳輸服務具有獨特的路由問題：

  - 由於傳輸服務和信箱傳輸服務存在於相同的 Exchange 2013 信箱伺服器上，因此，信箱傳輸服務必定和該信箱伺服器隸屬於相同的傳遞群組。此傳遞群組即指*本機傳遞群組*。

  - 信箱信箱傳輸提交服務不會自動將郵件傳送至所屬的本機傳遞群組中之本機信箱伺服器上或其他信箱伺服器上的傳輸服務。信箱傳輸提交服務和傳輸服務一樣有權存取相同的路由拓撲資訊，因此，信箱傳輸提交服務可將郵件傳送至傳遞群組外部信箱伺服器上的傳輸服務。本機傳遞群組中的信箱伺服器是作為後援選項及傳遞至非信箱收件者之用途。

  - 信箱傳輸服務僅會與 Exchange 2013 信箱伺服器上的傳輸服務進行通訊。

  - 信箱傳輸服務僅會與本機 Exchange 2013 信箱伺服器上的信箱資料庫進行通訊。信箱傳輸服務決不會與其他信箱伺服器上的信箱資料庫進行通訊。

當使用者從他們的信箱傳送郵件時，信箱傳輸提交服務會解析信箱資料庫的郵件收件者。信箱傳輸提交服務所使用的信箱伺服器清單是根據郵件收件者的信箱資料庫而建立的。請注意，有可能會發生沒有任何收件者擁有信箱的情況，例如，如果收件者是通訊群組或郵件使用者。信箱傳輸提交服務會針對每一個信箱資料庫查詢傳遞群組和相關路由資訊。信箱傳輸提交服務所使用的傳遞群組為：

  - 可路由的 DAG

  - 信箱傳遞群組

  - AD 站台

根據收件者的數量和類型，信箱傳輸提交服務會執行下列其中一個操作：

  - 針對寄給單一信箱收件者的郵件，請在目標傳遞群組中選取信箱伺服器，然後根據 Active Directory 站台的距離設定信箱伺服器的優先順序。將郵件路由至收件者可能會透過中樞站台路由郵件。

  - 針對寄給多個信箱收件者的郵件，請根據 Active Directory 站台的距離，使用前 20 個收件者來選取最近傳遞群組中的信箱伺服器。

  - 如果該郵件未含信箱收件者，在本機傳遞群組中選擇一台信箱伺服器。

當信箱傳輸傳遞服務從傳輸服務接收郵件時，它可以接受或拒絕將郵件傳送到本機信箱資料庫。如果收件者位於本機信箱資料庫主動副本中，則信箱傳輸傳遞服務可以傳遞該郵件。但是，如果收件者位於本機信箱資料庫的主動副本中，郵件傳輸傳遞服務就無法傳遞該郵件，且必須提供一個未傳遞回應至傳輸服務。舉例來說，如果該信箱資料庫的主動副本最近已移至另一台伺服器，則傳輸服務有可能會將郵件誤傳至一台目前保有該信箱資料庫之非作用副本的郵件伺服器。信箱傳輸傳遞服務回傳至傳輸服務的未傳遞回應包括：

  - 重試傳遞

  - 產生一個 NDR

  - 重新路由傳送此郵件

回到頁首

## Edge Transport Server 的傳輸服務中的路由

如果您已在周邊網路中安裝 Edge Transport Server，則 Edge Transport Server 上的傳輸服務會提供所有網際網路對向郵件流程的 SMTP 轉送及智慧主機服務。從網際網路傳送及接收的郵件會本機佇列在 Edge Transport Server 上。佇列會對應至外部網域或傳送連接器。如需詳細資訊，請參閱[佇列](queues-exchange-2013-help.md)主題的「NextHopSolutionKey」一節。

通常，當您在周邊網路中安裝 Edge Transport Server 時，即會將 Edge Transport Server 訂閱至 Active Directory 站台。Active Directory 站台包含將郵件轉送至 Edge Transport Server 以及從中轉送郵件的 Mailbox Server。Edge 訂閱程序會建立 Edge Transport Server 的 Active Directory 站台成員資格聯盟。站台聯盟可讓 Active Directory 站台中的 Mailbox Server 將郵件轉送至 Edge Transport Server，以傳遞到網際網路，而不需要設定明確的傳送連接器。

在多站台組態中，從內部收件者到外部收件者的輸出郵件會先路由傳送到訂閱的 Active Directory 站台。目標 Active Directory 站台為傳遞群組。路由目的地是傳輸服務中的組織內傳送連接器，而傳輸服務位於已記閱 Active Directory 站台的任何 Mailbox Server 上。*「組織內傳送連接器」*是存在於每部 Mailbox Server 之傳輸服務中的特殊傳送連接器。此傳送連接器是以隱含方式建立、不可見、不需要管理，以及用來在 Exchange 伺服器之間轉送郵件。

外部收件者的輸出郵件會從 Mailbox Server 路由傳送至 Edge Transport Server。將郵件路由傳送至已訂閱 Edge Transport Server 時，不包括 Client Access Server。郵件會從 Mailbox Server 之傳輸服務中的組織內傳送連接器傳輸至 Edge Transport Server 之傳輸服務中的接收連接器。在已訂閱 Edge Transport Server 上，預設接收連接器設定為接聽來自已訂閱 Active Directory 站台的內部 Mailbox Server 中的連線，以及來自網際網路的匿名連線。Edge Transport Server 上的傳輸服務將郵件分類之後，會在本機佇列服務，以便使用 Edge 訂閱期間所建立的專用傳送連接器來傳遞至網際網路。

來自外部收件者的輸入郵件是透過預設接收連接器到達 Edge Transport，並且會分類和佇列郵件以進行傳遞。郵件是透過 Edge 訂閱所建立的專用傳送連接器進行轉送，以將郵件傳送至 Exchange 組織。郵件的下一個目的地取決於內部 Exchange 伺服器的設定方式。

  - **在相同電腦上安裝 Mailbox Server 和 Client Access Server**   此組態會使用 Client Access Server 進行輸入郵件流程。郵件會從 Edge Transport Server 之傳輸服務中的傳送連接器流向 Client Access Server 之前端傳輸服務中的預設接收連接器，再流向 Mailbox Server 之傳輸服務中的預設接收連接器。

  - **在不同電腦上安裝 Mailbox Server 和 Client Access Server**   此組態會在輸入郵件流程中略過 Client Access Server。郵件會從 Edge Transport Server 之傳輸服務中的傳送連接器流向 Mailbox Server 之傳輸服務中的預設接收連接器。

如果您已在周邊網路中安裝 Exchange 2007 或 Exchange 2010 Edge Transport Server，則輸入及輸出郵件流程一律會直接在 Edge Transport Server 與 Mailbox Server 之間進行。不會使用 Client Access Server。

回到頁首


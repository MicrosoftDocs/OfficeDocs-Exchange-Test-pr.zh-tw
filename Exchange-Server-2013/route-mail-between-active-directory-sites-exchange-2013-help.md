---
title: 'Active Directory 站台之間路由傳送郵件: Exchange 2013 Help'
TOCTitle: Active Directory 站台之間路由傳送郵件
ms:assetid: 86b423e3-7bec-4430-9a5a-4f84ce9d82ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ916681(v=EXCHG.150)
ms:contentKeyID: 52062568
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory 站台之間路由傳送郵件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Active Directory 站台是以實體網路層面為基礎的邏輯組態元件。建立 Active Directory 站台的主要用途是定義網路中的哪些子網路，是以最佳化 Active Directory 複寫流量控制的方式連線。Microsoft Exchange Server 2013 可以辨識資料庫可用性群組 (DAG) 和 Active Directory 站台作為路由界限，而 Exchange 2013 伺服器會根據 Active Directory 站台拓撲進行路由決策。

根據預設，Active Directory 樹系只包含一個 Active Directory 站台。此 Active Directory 站台的預設名稱是 `Default-First-Site-Name`。如果沒有建立其他 Active Directory 站台，則樹系中的所有網域成員電腦都會是 `Default-First-Site-Name` 的成員。您不需要設定子網路到站台 (subnet-to-site) 的關聯。如果有建立其他的 Active Directory 站台，您就必須指定要指派給該 Active Directory 站台的子網路。

**目錄**

Determining site membership

IP site links

Controlling IP site link costs

Implementing hub sites

Topology discovery

## 決定站台成員資格

每個 Active Directory 站台可與一或多個 IP 子網路關聯。系統管理員可以針對設定為網域控制站及通用類別目錄伺服器的電腦，指派 Active Directory 站台成員資格。設定 Exchange 伺服器之類的網域成員電腦使用的 IP 位址位在與 Active Directory 站台關聯的 IP 子網路中時，就會自動將 Active Directory 站台成員資格指派給它們。擁有相同 Active Directory 站台成員資格的電腦，應該可有良好的網路連線性。伺服器則一律是單一 Active Directory 站台的成員。

若某個應用程式能夠判斷電腦所安裝位置的 Active Directory 站台成員資格，以及樹系內其他電腦的站台成員資格，然後使用這項資訊來控制通訊流程，這就是站台感知式應用程式。當站台感知式應用程式必須使用其他伺服器的服務時，例如網域控制站或通用類別目錄伺服器，會優先考慮與要求那些服務之電腦擁有相同 Active Directory 站台成員資格的伺服器。

Exchange 2013 是站台感知式應用程式，而且會使用 Active Directory 拓撲進行郵件路由，以及與在其他 Exchange 2013 電腦上執行的服務進行通訊。Active Directory 站台不只是路由界限，也是服務探索界限。

判斷網域成員電腦的站台成員資格，需根據一連串 DNS 查詢，來將本機 IP 位址和定義的子網路相比較，然後判定適當的站台成員資格關聯。為了降低與 DNS 查詢相關的額外負荷，新增的 Exchange 2013 Active Directory 架構包含 Exchange 伺服器物件的 **msExchServerSite** 屬性。此屬性值是 Exchange 伺服器的 Active Directory 站台辨別名稱。此屬性是每個 Exchange 伺服器物件的內容。將站台成員資格相似性儲存為伺服器物件屬性後，便可以直接從 Active Directory 讀取目前的拓撲而不用依賴 DNS 查詢，對於如已訂閱邊際傳輸伺服器等的非網域電腦，則會啟用站台成員資格關聯。

Microsoft Exchange Active Directory 拓撲服務會填入 **msExchServerSite** 屬性的值，並讓值保持在最新狀態。Windows 型的電腦啟動時，Net Logon 服務即會判斷該部電腦的站台成員資格。Net Logon 服務會使用那項資訊尋找和本機電腦位於相同 Active Directory 站台的網域控制站，然後將授權和驗證要求直接送往那些伺服器。Microsoft Exchange Active Directory 拓撲服務會使用 **DsGetSiteName** API 呼叫，從 Net Logon 服務擷取站台成員資格值，並將 Active Directory 站台的辨別名稱寫入 Active Directory 中 Exchange 伺服器物件的 **msExchServerSite** 屬性。

下表顯示組織可能會如何定義 Active Directory 站台。在此範例中，定義了三個 Active Directory 站台，而且每個 Active Directory 站台都與一個以上的 IP 子網路關聯。

**Active Directory 站台對子網路關聯的範例**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Active Directory 站台名稱</th>
<th>關聯的 IP 子網路</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>站台 A</p></td>
<td><p>192.168.1.0/24</p>
<p>192.168.2.0/24</p></td>
</tr>
<tr class="even">
<td><p>站台 B</p></td>
<td><p>192.168.3.0/24</p>
<p>192.168.4.0/24</p></td>
</tr>
<tr class="odd">
<td><p>站台 C</p></td>
<td><p>192.168.5.0/24</p>
<p>192.168.6.0/24</p></td>
</tr>
</tbody>
</table>


如果名為 Mailbox01 的伺服器具有 IP 位址 192.168.1.1，代表它是站台 A 的成員。透過變更伺服器的 IP 位址，即可變更該伺服器的站台成員資格。如果您將 Mailbox01 的 IP 位址變更為 192.168.2.1，這樣並不會變更該伺服器的 Active Directory 站台成員資格，因為該子網路還與站台 A 關聯。不過，如果您移動了伺服器，並將 IP 位址變更為 192.168.3.1，則該伺服器就會被視為站台 B 的成員。

如果您變更子網路對 Active Directory 站台的關聯，站台成員資格也會有所變更。例如，如果您移除子網路 192.168.3.0，使其不再與站台 B 關聯，然後建立該子網路與站台 A 的關聯，那麼，IP 位址為 192.168.3.1 的伺服器，其站台成員資格也會隨之變更成站台 A。每當站台成員資格有所變更時，Exchange 就必須更新其組態資料，如此當 Exchange 在進行路由決策時，才會將變更列入考量。從 Active Directory 站台成員資格發生變更，直到完全傳播拓撲變更，期間可能會有些微的時間延遲。

回到頁首

## IP 站台連結

站台連結是 Active Directory 站台間的邏輯路徑。站台連結物件代表以一致的成本相互通訊的一組站台。站台連結和在實體網路上傳送網路封包的實際路徑沒有對應關係。不過，系統管理員指派給站台連結的成本通常和基礎網路可靠性、速度以及可用頻寬有關。例如，跟速度為 10 Mbps 的網路連線相比，Active Directory 系統管理員對於速度每秒 100 MB (Mbps) 的網路連線會指派較低的成本。

所有站台連結預設均為可轉移。這表示如果站台 A 連結至站台 B，且站台 B 連結至站台 C，則站台 A 間接地連結至站台 C。站台 A 與站台 C 之間的間接連結稱為*站台連結橋接*。

Exchange 只會使用 IP 站台連結來判斷其 Active Directory 站台路由拓撲。計算路由表時，Exchange 的路由元件會考量指派給 IP 站台連結的成本。這些成本可用來計算將郵件送往最終目的地的最低成本路由路徑。

每個 Active Directory 站台必須與至少一個 IP 站台連結關聯。有一個預設 IP 站台連結，名稱為 `DEFAULTIPSITELINK`。當您建立一個 Active Directory 站台時，您必須將該站台與 IP 站台連結關聯。您可以建立額外的 IP 站台連結以實作所需的拓撲，也可以將每個 Active Directory 站台都與 `DEFAULTIPSITELINK` 建立關聯。屬於 IP 站台連結一部的每個 Active Directory 站台，都能以一致的成本與該連結中所有其他站台直接通訊。

在下圖中，樹系中已設定四個 Active Directory 站台。每個站台都已經與 `DEFAULTIPSITELINK` 建立關聯。因此，每個 Active Directory 均能使用相同的成本量值，與其他每個站台直接通訊。其中顯示了多條通訊路徑，但只定義了一個 IP 站台連結。

**包含單一 IP 站台連結的完整網狀拓撲**

![包含單一 IP 站台連結的完整網狀拓撲](images/JJ916681.af38d41d-e768-4221-ab4b-b782aa388b73(EXCHG.150).gif "包含單一 IP 站台連結的完整網狀拓撲")

在下圖中，樹系中已設定四個 Active Directory 站台。在此拓撲中，系統管理員利用已設定的 IP 站台連結來建立 Active Directory 站台的*中樞與支點拓撲*。每個支點站台均可與中心站台直接通訊，而且支點站台能使用可轉移 IP 站台連結來彼此通訊。

**Active Directory IP 站台連結的中樞與支點拓撲**

![IP 站台連結的中樞與支點拓撲](images/JJ916681.eca6cd51-8c2e-4996-81ea-070cd9766ef8(EXCHG.150).gif "IP 站台連結的中樞與支點拓撲")

請務必注意，Exchange 只有在決定最低成本路徑時才會使用站台連結，但一律會嘗試直接將郵件傳遞至目的 Exchange 伺服器。例如，如果上圖所示拓撲中站台 B 的使用者，將郵件傳送給站台 C 中的其他使用者，則站台 B 中的 Mailbox Server 會直接連接至站台 C 中的 Mailbox Server。若您希望強制郵件經過站台 A，則必須啟用該站台作為中樞站台。如需中樞站台的詳細資訊，請參閱本主題稍後的＜實作中樞站台＞。

Active Directory 系統管理員會實作最能呈現樹系的連線性與通訊需求的拓撲。因為 Exchange 會使用相同的拓撲，所以您必須確定目前的拓撲支援有效率的郵件通訊。

站台連結的預設成本是 100。有效的站台連結成本可以是 1 到 99,999 的任何數字。如果您指定多餘的連結，則一律會優先選擇具有最低成本指派的連結。Exchange 組織系統管理員可將 Exchange 特定成本指派給 IP 站台連結。如果將 Exchange 成本指派給 IP 站台連結，Exchange 就會使用該成本。否則，會使用 Active Directory 成本。如需如何針對 IP 站台連結設定 Exchange 成本的相關資訊，請參閱本主題稍後提供的「控制 IP 站台連結成本」。隸屬 Enterprise Administrators 群組成員的系統管理員才能建立額外的 IP 站台連結。

如需 Active Directory 站台組態的詳細資訊，請參閱[設計站台拓撲](https://go.microsoft.com/fwlink/p/?linkid=33551)。

回到頁首

## 控制 IP 站台連結成本

Active Directory IP 站台連結成本是依據與 WAN 中所有網路連線相較之下的相對網路速度而定，而且是為了產生可靠且有效的複寫拓撲所設計。因此，在多數情況下，現有 IP 站台連結成本應該適用於 Exchange 郵件路由。不過，若在記載現有 Active Directory 站台及 IP 站台連結拓撲之後，您確定 Active Directory IP 站台連結成本與流量模式並不是 Exchange 最理想的狀態，您可以調整 Exchange 所評估的成本。使用 Active Directory 工具變更指派給 IP 站台連結的成本，會影響整個環境。請改為在 Exchange 管理命令介面中使用 **Set-AdSiteLink** 指令程式，將 Exchange 特定成本指派給 IP 站台連結。例如，若要在名為 SITELINKAB 的 IP 站台連結上設定 Exchange 特定成本值 25，請在命令介面中執行下列命令：`Set-AdSiteLink SITELINKAB -ExchangeCost 25`.

將 Exchange 特定成本指派給 IP 站台連結後，Exchange 成本只會為了郵件路由目的覆寫 Active Directory 成本，而路由在評估最低成本的路由路徑時，只會將 Exchange 成本列入考量。

當郵件路由拓撲必須從 Active Directory 複寫拓撲岔開時，調整 IP 站台連結成本可能會很有用。Exchange 成本可用來強制所有郵件路由使用中樞站台。與 Active Directory 站台的通訊失敗時，Exchange 成本也可以用來控制郵件的佇列位置。下圖顯示具有四個站台的 Active Directory 拓撲。

**包含在 IP 站台連結上設定之 Exchange 成本的拓撲**

![包含在 IP 站台連結上之 Exchange 成本的拓撲](images/JJ916681.56ac2bab-99de-4ddf-b968-80cd34ab8c21(EXCHG.150).gif "包含在 IP 站台連結上之 Exchange 成本的拓撲")

在上圖中，站台 C 與站台 D 之間的網路連線是低頻寬連線，只能用於 Active Directory 複寫，不應用於郵件路由。不過，Active Directory IP 站台連結成本將該連結納入其他任何 Active Directory 站台至站台 D 的最低成本路由路徑中。因此，傳遞至站台 D 的郵件會佇列在站台 C。Exchange 系統管理員反而希望最低成本路由路徑包含站台 B，這樣一來，當站台 D 無法使用時，郵件將會佇列在站台 B。在站台 C 與站台 D 之間的 IP 站台連結上設定較高的 Exchange 成本，可防止該 IP 站台連結被納入站台 D 的最低成本路由路徑中。

Exchange 支援設定 Active Directory IP 站台連結的郵件大小上限。依預設，對於不同 Active Directory 站台內的 Exchange 伺服器之間轉送的郵件，Exchange 不會規定郵件大小上限。如果使用 **Set-AdSiteLink** 指令程式來設定 Active Directory IP 站台連結的郵件大小上限，當郵件大於在最低成本路由路徑中的任何 Active Directory 站台連結上設定的郵件大小上限時，路由會產生未傳遞回報 (NDR)。如果郵件傳送至必須在低頻寬連線上通訊的遠端 Active Directory 站台，則此組態適用於限制這類郵件的大小。如需詳細資訊，請參閱 [郵件大小限制](message-size-limits-exchange-2013-help.md)。

回到頁首

## 實作中樞站台

在 Exchange 組織中，您可能想要強制透過特定的 Active Directory 站台來傳遞所有的郵件。您可以使用命令介面將 Active Directory 站台指定為中樞站台。當您這麼做時，有可能因為涉入郵件傳遞的伺服器變多，而導致整體負荷加重。例如，假設郵件從站台 A 傳送至站台 E。如果最低成本路由路徑是「站台 A - 站台 B - 站台 C - 站台 D - 站台 E」，而且您指定站台 C 為中樞站台，則郵件會從站台 A 轉送至站台 C，再從站台 C 轉送至站台 E。

您要使用 **Set-AdSite** 指令程式來指定 Active Directory 站台作為中樞站台。每當供郵件傳遞使用的最低成本路由路徑沿途有中樞站台存在時，在將郵件轉送到其最終目的地之前，郵件會排入佇列並由中樞站台內 Mailbox Server 上的 Transport 服務處理。

選擇最低成本路由路徑後，路由會判斷該路由路徑沿途是否有中樞站台。若有設定中樞站台，則郵件會先停留在中樞站台的 Mailbox Server，再轉送到目的地。若最低成本路由路徑上有多個中樞站台，郵件就會停留在路由路徑沿途的每個中樞站台。

當中樞站台位於最低成本路由路徑時，此項直接轉送路由的變化形式才有作用。下圖顯示中樞站台的正確用法。在此圖表中，站台 B 被設定為中樞站台。從站台 A 轉送至站台 D 的郵件會先轉送至站台 B，然後再傳遞給站台 D。

**利用中樞站台的郵件傳遞**

![利用中樞站台的郵件傳遞](images/JJ916681.93238bcb-6bbc-4a48-aeb0-09342a421b5b(EXCHG.150).gif "利用中樞站台的郵件傳遞")

下圖顯示 IP 站台連結成本如何影響前往中樞站台的路由選擇。在此情況中，已將站台 B 指定為中樞站台。但是，站台 B 並不位於其他任何站台間的最低成本路由路徑。因此，從站台 A 轉送至站台 D 的郵件絕不會轉送至站台 B。Active Directory 站台並不在兩個其他站台間的最低成本路由路徑上，則該站台永不作為中樞站台使用。

**設定錯誤的中樞站台**

![設定錯誤的中樞站台](images/JJ916681.c010d4d8-5cd3-4b79-b7db-0367ba3cc287(EXCHG.150).gif "設定錯誤的中樞站台")

您可以將任何 Active Directory 站台設定為中樞站台。不過，在中樞站台內必須至少有一部 Mailbox Server，此組態才能正常運作。

回到頁首

## 拓撲探索

有了下列必要元素，Exchange 就能使用 Active Directory 拓撲：

  - Microsoft Exchange Active Directory 拓撲服務。

  - Microsoft Exchange Transport 服務內的拓撲探索模組。

Microsoft Exchange Active Directory 拓撲服務會在所有 Exchange 2013 Client Access Server 和 Mailbox Server 上執行。這些伺服器會使用 Microsoft Exchange Active Directory 拓撲服務來探索 Exchange 伺服器能使用的網域控制站與通用類別目錄伺服器，以便讀取與寫入 Active Directory 資料。每當 Exchange 必須讀取或寫入 Active Directory 時，Exchange 2013 就會繫結至已識別的目錄伺服器。

拓撲探索模組是 Microsoft Exchange Transport 服務的一部分，而且可提供有關 Exchange 伺服器的 Active Directory 拓撲資訊。此 API 會探索組織中的 Exchange 伺服器與角色，並判斷它們與 Active Directory 組態物件的關係。接著從 Active Directory 擷取組態資料後加以快取，如此便可供在該電腦上執行的 Exchange 服務存取。

拓撲探索模組會執行下列步驟以產生 Exchange 路由拓撲：

1.  會從 Active Directory 讀取資料。擷取下列所有物件：
    
      - Active Directory 站台。
    
      - IP 站台連結。
    
      - 所有 Exchange 伺服器。

2.  步驟 1 擷取的資料會用來建立初始拓撲，然後開始連結和對應相關的組態物件。

3.  透過從 Exchange 中儲存的 Exchange 伺服器物件擷取站台屬性值，將 Exchange 伺服器對應至 Active Directory 站台。

4.  以所擷取的資訊集合更新路由表。

此程序可使每部 Exchange 2013 伺服器注意到組織中的其他 Exchange 伺服器，以及 Exchange 伺服器彼此間關係的密切程度。

回到頁首


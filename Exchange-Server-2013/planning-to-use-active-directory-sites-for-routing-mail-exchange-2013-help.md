---
title: '規劃使用 Active Directory 站台的路由傳送郵件: Exchange 2013 Help'
TOCTitle: 規劃使用 Active Directory 站台的路由傳送郵件
ms:assetid: 0f697cee-bcaa-4c69-b80c-7a2afd1817d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996299(v=EXCHG.150)
ms:contentKeyID: 52062516
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 規劃使用 Active Directory 站台的路由傳送郵件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-05-21_

Microsoft Exchange Server 2013會將 Active Directory 站台及資料庫可用性群組 (DAGs) 辨識為路由界限。不過， Exchange 2013仍會使用 Active Directory 站台拓撲來決定如何將郵件傳輸不同 Dag 或組織內的網站中的 Exchange 伺服器之間。如需詳細資訊，請參閱[郵件路由](mail-routing-exchange-2013-help.md)。

在信箱伺服器上的傳輸服務提供內部部署 Exchange 組織的郵件傳輸。當您正在部署完全Exchange 2013的組織或簡介Exchange 2013到純粹Exchange Server 2010的組織，進行其他設定才能建立樹系中的路由。

**目錄**

How Exchange 2013 uses Active Directory site membership

Determine Active Directory site membership

Overview of IP site links

Exchange 2013 server placement in Active Directory sites

## Exchange 2013 如何使用 Active Directory 站台成員資格

Exchange 2013是網站感知應用程式。網站感知應用程式可以決定他們自己的 Active Directory 站台成員資格與網站成員資格的其他伺服器查詢 Active Directory。Exchange 2013使用網站成員資格來決定哪一個網域控制站與通用類別目錄伺服器，以用於處理 Active Directory 查詢。此外，當執行 Exchange server 已決定另一部 Exchange 伺服器的 Active Directory 站台成員資格，它可以查詢 Active Directory 擷取網站名稱。

在Exchange 2013、 Microsoft Exchange Active Directory 拓撲服務負責更新網站屬性的 Exchange 伺服器物件。Active Directory 站台成員資格是伺服器的物件屬性，因為 Exchange 沒有查詢 DNS 伺服器位址解析 Active Directory 站台相關聯的子網路。在 Exchange 伺服器物件上戳記 Active Directory 網站屬性也可讓指派給不是網域成員，例如訂閱的 Edge Transport server 的伺服器的 Active Directory 站台成員資格。

Exchange 2013 伺服器會如下所示使用 Active Directory 站台成員資格資訊：

  - **郵件提交**  Exchange 2013 Mailbox server 上的信箱傳輸提交服務會使用 Active Directory 站台成員資格資訊來判斷其他Exchange 2013信箱伺服器都位於相同的 Active Directory 站台。如果來源信箱伺服器不屬於 DAG 或 DAG 不會跨多個 Active Directory 站台、 來源信箱伺服器上的信箱傳輸提交服務會送出郵件的路由和傳輸到相同的 Active Directory 站台中Exchange 2013 Mailbox server 上的傳輸服務。

  - **郵件傳遞**  Exchange 2013 Mailbox server 上的傳輸服務執行收件者的解析度和查詢 Active Directory 來比對收件者帳戶的電子郵件地址。收件者帳戶的資訊包括使用者的信箱資料庫的完整的網域名稱 (FQDN)。傳輸服務會查詢 Active Directory 來判斷使用者的信箱資料庫的 Active Directory 站台。如果信箱資料庫不屬於 DAG，它會將郵件傳遞到該信箱伺服器。否則，它會轉送郵件傳遞的目標信箱伺服器相同的網站中的另一個信箱伺服器。

  - **郵件路由。**  Exchange 2013 Mailbox server 上的傳輸服務擷取資訊從 Active Directory 來判斷組織內部的路由郵件應方式。Exchange 2013來決定何處及如何使用的*傳遞群組*概念來路由傳送訊息。根據目的地無法路由傳送郵件的傳輸服務或信箱傳輸傳遞伺服器上的服務Exchange 2013信箱，或者集線傳輸伺服器執行舊版 Exchange。如需詳細資訊，請參閱[郵件路由](mail-routing-exchange-2013-help.md)。

  - **整合通訊郵件提交**  整合通訊服務Exchange 2013 Mailbox server 上的使用 Active Directory 站台成員資格資訊來尋找其他位於相同的 Active Directory 站台信箱伺服器。整合通訊服務提交給郵件路由傳送至相同的 Active Directory 站台內的信箱伺服器上的傳輸服務。傳輸服務伺服器執行收件者解析和查詢 Active Directory 以符合的電話號碼、 E.164 號碼或 SIP 位址給收件者的帳戶。收件者解析完成後，傳輸服務將郵件傳遞至目標信箱一般電子郵件訊息的形式相同的方式。

  - **用戶端存取伺服器的用戶端連線**  如果用戶端存取伺服器收到使用者連線要求，它會查詢 Active Directory 來決定哪一個信箱伺服器會主控使用者的信箱。Client Access server 然後擷取該信箱伺服器和 proxy 的 Active Directory 站台成員資格的信箱伺服器的連線。

## 判定 Active Directory 站台成員資格

Active Directory 用戶端會假設網站成員資格來比對其指派至 Active Directory 站台及服務中定義且與 Active Directory 站台相關聯的子網路的 IP 位址。用戶端然後會使用此資訊來判斷哪些網域控制站和通用類別目錄伺服器該站台存在於並且回饋與這些目錄的伺服器進行驗證和授權。Exchange 2013利用此關係由也偏好Exchange 2013伺服器相同的網站中的目錄伺服器從擷取的收件者的相關資訊。

屬於相同的 Active Directory 站台的所有電腦都視為良好的連線，以高速、 可靠的網路連線。根據預設，當先部署 Active Directory 樹系，沒有名為`Default-First-Site-Name`單一站台。如果由系統管理員手動不設定任何其他網站、 所有伺服器和樹系中的用戶端電腦都視為`Default-First-Site-Name`的成員。

定義多個站台時，Active Directory 系統管理員必須定義組織中出現的子網路，並建立那些子網路與 Active Directory 站台的關聯。

Microsoft Exchange Active Directory 拓撲服務在伺服器啟動時檢查 Exchange 伺服器物件上的網站成員資格屬性。如果網站屬性設為更新，Microsoft Exchange Active Directory 拓撲服務會使用新的值標屬性。Microsoft Exchange Active Directory 拓撲服務每隔 15 分鐘會驗證站台屬性值，並更新值如果網站成員資格有所變更。Microsoft Exchange Active Directory 拓撲服務使用的網路登入服務取得目前的網站成員資格。Net 登入服務更新網站成員資格每五分鐘。這表示最多達 20 分鐘延遲期間可能等待時間該站台成員資格變更和新的值為 site 屬性上加上戳記。

## IP 站台連結概觀

IP 站台連結所定義 Active Directory 站台之間的關係。IP 站台連結是由兩個或多個 Active Directory 站台所組成。在相同的成本通訊之連結的一部分的所有 Active Directory 站台。IP 站台連結內容\] 包括成本工作分派、 排程及間隔。排程\] 和 \[間隔屬性用於判斷 Active Directory 複寫頻率。Exchange 2013使用成本指派來決定最低成本路由的多個路徑存在至目的地時要遵循的流量。彙總的傳輸路徑中所有站台連結成本取決於該路由的成本。Active Directory 管理員會將成本指派給相對的網路速度為基礎的連結和可用頻寬相較於其他可用的連線。

根據預設，在信箱伺服器上的傳輸服務永遠嘗試直接連線至的傳輸服務或另一個 Active Directory 站台中的信箱伺服器上的信箱傳輸傳遞服務。傳輸規則中的郵件沒有轉送到站台連結路徑中的每個信箱伺服器上的傳輸服務。但中的路由路徑的中階 Active Directory 站台信箱伺服器可能會在下列情況中執行訊息轉送：

  - Mailbox server 之間的直接轉接將不會發生時的最低成本路由路徑的中樞站台已存在。您可以設定 Active Directory 站台作為中樞站台讓郵件都透過中樞站台之前將郵件轉送至目標伺服器。本主題稍後的討論中樞站台。

  - Exchange 2013使用目的地 Active Directory 站台的通訊失敗時的衍生 IP 站台連結資訊的路由路徑。如果沒有目的地 Active Directory 站台中的信箱伺服器的回應，傳遞郵件會的最低成本路由路徑直到中 Active Directory 站台中的路由路徑的信箱伺服器進行連線。將郵件佇列中的 Active Directory 站台及佇列將處於 retry 狀態。此行為會呼叫*失敗點的佇列*。

  - 在Exchange 2013組織中沒有 Dag、 信箱伺服器上的傳輸服務也可以使用 IP 站台連結資訊最佳化路由傳送給多個收件者的訊息。Mailbox server 延遲複本發送的郵件直到它達到分支中的收件者的路由路徑。代表在個別的路由路徑分支 Active Directory 站台中信箱伺服器會將緣故的郵件轉送至每個收件者的目的地。此功能稱為*延遲送出*。

## 指定中樞站台

您可以使用**Set-AdSite**指令程式 Active Directory 站台設定為中樞站台。當中樞站台存在沿著兩種傳輸伺服器之間的最低成本路由路徑時，郵件都被透過中樞站台的處理之前它們轉送至目的地伺服器。若要發生此路由行為，該中樞站台必須存在於沿著兩種傳輸伺服器之間的最低成本路由路徑。當它需要有網路拓撲，例如防火牆時存在於 Active Directory 站台之間及防止直接轉接的 SMTP 通訊只應使用此設定。如需詳細資訊，請參閱[在 Active Directory 中設定 Exchange 郵件路由設定](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md)。

## 在 IP 站台連結上設定 Exchange 特定成本

您可以使用 Exchange 管理命令介面中的**Set-AdSiteLink**指令程式來設定 Active Directory IP 站台連結的 Exchange 特定成本。Exchange 特定成本是用來取代 Active Directory 指派成本來決定 Exchange 路由路徑不同屬性。此設定在 Active Directory IP 站台連結成本不會導致最佳 Exchange 郵件路由拓撲時很有用。如需詳細資訊，請參閱[在 Active Directory 中設定 Exchange 郵件路由設定](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md)。

## 在 IP 站台連結上設定郵件大小限制

根據預設， Exchange 2013不時各有不同的 Active Directory 站台中的信箱伺服器之間轉送郵件的最大郵件大小限制。如果您使用**Set-AdSiteLink**指令程式 Active Directory IP 站台連結上設定的郵件大小上限時，郵件只要含有大於最低成本路由路徑中任何 Active Directory 站台連結上設定的最大郵件大小限制的路由產生未傳遞回報 (NDR)。此設定時十分有用限制傳送給遠端必須透過低頻寬連線通訊的 Active Directory 站台的郵件的大小。

## Exchange 2013 伺服器在 Active Directory 站台中的位置

郵件路由正確發生Exchange 2013伺服器之間、 樹系中部署的所有 Exchange 伺服器必須都屬於 Active Directory 站台。請確定您已指派的 IP 位址都是已正確地與 Active Directory 站台相關聯的子網路。

規劃 Active Directory 站台拓撲中的Exchange 2013伺服器的位置的第一個步驟是文件目前的拓撲。您的說明文件應如下：

  - Sites

  - 子網路及其站台關聯

  - IP 站台連結及其成員站台

  - IP 站台連結成本

  - 每一個站台中的目錄伺服器

  - 實體網路連線

  - 防火牆位置

您有 diagrammed 這些物件後，規劃部署 Exchange 伺服器的位置。決定放置伺服器時，請考慮下列資訊：

  - Mailbox Server 需要與通用類別目錄伺服器直接通訊，才能執行 Active Directory 查閱。

  - 我們建議您在每一個 Active Directory 站台部署多部 Mailbox Server 來提供負載平衡與容錯。

  - DAG 及站台恢復

  - Mailbox server 上的 Unified Messaging 服務送出至傳遞至信箱的信箱伺服器上傳輸服務的語音信箱訊息。執行 Unified Messaging Call Router 服務之 Client Access server 可能是位於中樞站台內或附近 IP 或 Voice over IP (VoIP) 閘道、 IP 專用交換機 (IP Pbx)、 已啟用 SIP 的 PBX 或工作階段邊界控制器 (SBC)。信箱伺服器具有相同的網站成員資格的用戶端存取伺服器上的傳輸服務接收傳輸的語音信箱郵件和郵件路由傳送至組織中其他信箱伺服器上的傳輸服務。

  - 用戶端存取伺服器提供連線點至 Exchange 組織的遠端存取 Exchange 使用者。用戶端存取伺服器必須部署在信箱伺服器會包含每個 Active Directory 站台。

規劃您Exchange 2013伺服器位置之後，您可能會識別您可以將會修改 Active Directory 站台拓撲以改善通訊流程的區域。若要調整 IP 站台連結和最佳化郵件傳遞的站台連結成本。有效的 Active Directory 拓撲不需要任何支援Exchange 2013的變更


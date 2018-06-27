---
title: '案例： 將 Exchange 設定為支援 WAN 的最佳化控制站: Exchange 2013 Help'
TOCTitle: 案例： 將 Exchange 設定為支援 WAN 的最佳化控制站
ms:assetid: 1f407698-0b71-45a3-867a-640ccf7351da
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee633456(v=EXCHG.150)
ms:contentKeyID: 52062523
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 案例： 將 Exchange 設定為支援 WAN 的最佳化控制站

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-09-28_

在 Microsoft Exchange Server 2013、 傳輸層安全性 (TLS) 加密是必要的 Mailbox server 之間的傳輸服務中的所有 SMTP 通訊。這會增加 Mailbox server 之間的傳輸服務通訊的整體的安全性。不過，在某些可用 WAN 最佳化控制器 (WOC) 裝置的拓撲中，可能會非預期 SMTP 流量 TLS 加密。您可以停用這些特定案例的 Mailbox server 之間的傳輸服務通訊 TLS。

請考慮下圖所示的拓撲。這四個站台拓撲的假設是兩個中央網站與分支 Office 2 皆連線良好而中央 Office 網站 1 和 Branch Office 1 之間的連線為透過 WAN 連結。公司已安裝 WOC 裝置在此連結可以壓縮及透過 WAN 最佳化流量。

**範例網路拓撲與 WOC 裝置**

![含有 WAN 最佳化程式的範例拓撲](images/Ee633456.52876869-52f1-4c0f-85b2-7a850643e8a1(EXCHG.150).gif "含有 WAN 最佳化程式的範例拓撲")

在此拓撲中，由於Exchange 2013使用 TLS 加密的 Mailbox server 之間的通訊無法壓縮移 WAN 連結上的 SMTP 流量。理想狀況下，應該會透過 WAN 連結的所有 SMTP 傳輸未加密 SMTP，同時保持 TLS 連線良好的網站中的安全性。Exchange 2013可讓您停用流量所設定的接收連接器的站台之間的 TLS 加密的選項。使用Exchange 2013這項功能，您可以設定 SMTP 和之間的流量中央 Office 網站 1 Branch Office 1、 例外，如下圖所示。

**慣用的邏輯訊息流程**

![慣用的邏輯訊息流程](images/Ee633456.e0fe62fa-1bad-4d43-9eaf-205a9b8d07e1(EXCHG.150).gif "慣用的邏輯訊息流程")

若要限制只透過 WAN 連結所傳遞的郵件的非加密 SMTP 流量是建議的組態。因此，站台內的所有站台信箱伺服器和不涉及 Branch Office 1 應可 TLS 加密的 Mailbox server 之間的跨網站傳輸服務通訊之間的傳輸服務通訊。

為了達到這項最終結果，您需要在包含 WOC 裝置的站台中每台 Mailbox Server 上 (Central Office Site 1 和 Branch Office 1 在相同拓撲中)，以指定的順序完成下列動作：

1.  啟用降級的 Exchange Server 驗證。

2.  建立專屬的接收連接器，以處理具有 WOC 裝置之連線上的流量。
    
    1.  將專屬接收連接器的遠端 IP 位址範圍內容，設定成遠端 Active Directory 站台中的 Mailbox Server IP 位址範圍。
    
    2.  在專屬接收連接器上停用 TLS。

此外，您需要完成下列動作，以確保 WAN 上的所有 SMTP 流量由您建立的專屬接收連接器來處理：

  - 設定將參與非 TLS 通訊中當作中樞站台的 Active Directory 站台，強制所有郵件流過專屬接收連接器 (Central Office Site 1 和 Branch Office Site 1 在相同拓撲中)。

  - 確認 Active Directory IP 站台連結成本已可確保您的遠端站台 (分公司範例拓撲中的 Office 1) 的最低成本路由路徑會通過具有 WOC 裝置的網路連結的方式。將 Exchange 特定成本指派給視 Active Directory 站台連結。

下列各節提供這些步驟的概觀。如需如何設定此案例的組織的逐步指示，請參閱[停用 Active Directory 站台之間的 TLS](disable-tls-between-active-directory-sites-exchange-2013-help.md)。

**目錄**

Downgrade authentication over TLS-disabled connections

Create and configure dedicated Receive connectors

Configure Hub sites

Configure Exchange-specific Active Directory site link costs

## 停用 TLS 之連線上的降級驗證

Kerberos 驗證可搭配 TLS 加密在 Exchange。當您停用傳輸服務之間的通訊 Mailbox server 上的 TLS 時，您需要執行另一份表單的驗證。當Exchange 2013會與其他執行 Exchange 的伺服器不支援**X-ANONYMOUSTLS**通訊時，它會回復成使用一般安全性服務應用程式發展介面 (GSSAPI) 驗證。Exchange 2013 Mailbox server 之間的所有傳輸服務通訊都使用**X-ANONYMOUSTLS**。當您使用降級 Exchange Server 驗證信箱伺服器上設定的傳輸服務時，您是在啟用 GSSAPI 驗證的其他Exchange 2013 Mailbox server 的傳輸服務通訊的影響。

回到頁首

## 建立及設定專屬接收連接器

您需要建立察覺將負責處理非 TLS 加密流量的接收連接器。針對此目的而使用不同的接收連接器可確保不會通過 WAN 連結的所有流量會都維持 TLS 加密來保護。

若要透過 WAN 的流量限制專用的接收連接器，您需要設定遠端的 IP 位址範圍屬性。Exchange 一定會使用最特定的遠端 IP 位址範圍的連接器。因此，這些新連接器會喜好設定來接收郵件從任何位置的預設接收連接器上。

回到範例拓撲，該範例假設類別 C 子網路 10.0.1.0/24 用於 Central Office Site 1 且 10.0.2.0/24 用於 Branch Office 1。若要準備在這兩個站台之間停用 TLS，您需要：

1.  在 Central Office Site 1 和 Branch Office 1 中每台 Mailbox Server 上建立名為 WAN 的接收連接器。

2.  在 Central Office Site 1 中每個專屬接收連接器上設定遠端 IP 位址範圍 10.0.2.0/24。

3.  在 Branch Office 1 中每個專屬接收連接器上設定遠端 IP 位址範圍 10.0.1.0/24。

4.  在所有專屬接收連接器上停用 TLS。

最終結果是由 （具有遠端 IP 位址範圍屬性名為 WAN 括號中顯示的接收連接器），如下圖所示。Branch Office 1 所示的單一 Mailbox server 和 Branch Office 2 省略清楚用途。

**接收連接器組態**

![接收連接器組態](images/Ee633456.1821b3db-1f7a-4ae7-afbc-5c99e117f976(EXCHG.150).gif "接收連接器組態")

回到頁首

## 設定中樞站台

根據預設， Exchange 2013信箱伺服器會嘗試直接連線至最接近最終目的地的特定郵件的信箱伺服器。在範例拓撲中，如果 Branch Office 2 中的使用者將郵件傳送至分支 Office 1 中的使用者、 Branch Office 2 中的信箱伺服器會連線至 Branch Office 1 直接傳遞該郵件的信箱伺服器。特定的拓撲中會加密與因此不理想的連線。若要有這類郵件通過信箱伺服器上集中 Office 網站 1，進而確認透過 WAN 連結，未加密的傳送過程中中央 Office 網站 1 和 Branch Office 1 需要設定為中樞站台。簡而言之，必須具有使用 TLS 的接收連接器的信箱伺服器的任何網站停用來設定為中樞站台，因此您可以透過該網站的路由流量強制伺服器中的其他網站的需求。如需詳細資訊，請參閱[在 Active Directory 中設定 Exchange 郵件路由設定](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md)。

回到頁首

## 設定 Exchange 特定的 Active Directory 站台連結成本

設定中樞站台來說不是不足以確保所有流量未加密透過 WAN 連結。這是因為 Exchange 會路由傳送的郵件透過中樞站台只有當該中樞站台之內的最低成本路由路徑。例如，假設我們的範例拓撲的 IP 站台連結成本設定 Active Directory 中 （中央 Office 網站 2 以利檢視省略），如下圖所示。

**範例拓樸的 IP 站台連結成本**

![範例拓撲的 IP 站台連結成本](images/Ee633456.099deb15-795a-417a-b6aa-925b3bedf8b4(EXCHG.150).gif "範例拓撲的 IP 站台連結成本")

在此情况下，通過中樞站台之 Branch Office 2 到 Branch Office 1 的路徑總成本為 12 (6+6)，而直接路徑的成本為 10。因此，沒有任何從 Branch Office 2 送到 Branch Office 1 的郵件會通過 Central Office Site 1，該流量也就仍然都會以 TLS 加密。

若要避免此問題，您需要指定是高於 IP 站台之間的連結 Branch Office 2 和 Branch Office 1，12，如下圖所示的 Exchange 特定成本。如此可確保所有訊息都移到未加密的通道中央 Office 網站 1 和 Branch Office 1 之間。

**設定 Exchange 特定 IP 站台連結成本的範例拓撲**

![含有 Exchange 成本的範例拓撲](images/Ee633456.cd036fe0-c37d-479e-a4c1-235e17e90ca7(EXCHG.150).gif "含有 Exchange 成本的範例拓撲")

如需詳細資訊，請參閱[在 Active Directory 中設定 Exchange 郵件路由設定](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md)。

回到頁首


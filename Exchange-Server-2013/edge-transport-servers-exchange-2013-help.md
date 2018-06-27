---
title: 'Edge Transport Server: Exchange 2013 Help'
TOCTitle: Edge Transport Server
ms:assetid: cfff9f59-afac-447c-8297-afcebe49a52d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124701(v=EXCHG.150)
ms:contentKeyID: 61180458
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge Transport Server

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-09-29_

Edge 傳輸伺服器所處理所有網際網路郵件流程，以提供 SMTP （簡易郵件傳送通訊協定） 轉送和智慧主機服務的組織Exchange減少攻擊層面。在 Edge Transport server 上執行的代理程式提供郵件保護和安全性的其他層的級。這些代理程式提供理想的垃圾郵件及套用傳輸規則來控制郵件流程。

因為 Edge Transport Server 已安裝在周邊網路中，所以絕對不會成為貴組織內部 Active Directory 樹系的成員且無法存取 Active Directory 資訊。不過，Edge Transport Server 需要位於 Active Directory 中的資料—例如，郵件流程的連接器資訊以及反垃圾郵件收件者查閱工作的收件者資訊。此資料是由 Microsoft Exchange EdgeSync 服務 (EdgeSync) 同步處理至 Edge Transport Server。EdgeSync 是在 Exchange 2013 Mailbox Server 上執行的程序集合，用以建立從 Active Directory 至 Edge Transport Server 上 Active Directory 輕量型目錄服務 (AD LDS) 執行個體的單向收件者和組態資訊複寫。EdgeSync 只會複製 Edge Transport Server 執行反垃圾郵件設定工作及啟用端對端郵件流程所需的資訊。EdgeSync 會執行排定的更新，讓 AD LDS 資訊保持最新。

您可以在周邊網路中安裝多部 Edge Transport Server。為您的輸入郵件流程部署一部以上的 Edge Transport Server，以提供重複和容錯移轉功能。您可以為郵件網域定義多個具有相同優先順序值的 MX 記錄，藉此將貴組織的 SMTP 流量負載均衡分散至每個 Edge Transport Server。您可以使用複製的組態指令碼，在多部 Edge Transport Server 之間達到組態的一致性。

Edge Transport server role 可讓您管理下列郵件處理案例。

## 網際網路郵件流程

Edge Transport Server 會接受從網際網路進入Exchange 組織的郵件。在 Edge Transport Server 處理郵件之後，郵件接著要路由傳送到的位置取決於內部 Exchange 伺服器的組態：

  - 如果 Client Access Server 和 Mailbox Server 安裝於不同的電腦上，則郵件會路由傳送至 Mailbox Server 上的傳輸服務。輸入 SMTP 郵件流程會略過 Client Access Server。

  - 如果 Client Access Server 和 Mailbox Server 安裝於相同的電腦上，則郵件會路由傳送至 Client Access Server 上的前端傳輸服務，然後再傳送至 Mailbox Server 上的傳輸服務。

從組織內傳送到網際網路的所有郵件經 Mailbox Server 上的傳輸服務處理後，會路由傳送到 Edge Transport Server。您可以設定 Edge Transport Server 使用 DNS 解析外部 SMTP 網域的 MX 資源記錄，也可以設定 Edge Transport Server 將郵件轉寄到智慧主機進行 DNS 解析。

## 反垃圾郵件保護

在 \[ Exchange 2013、 反垃圾郵件功能提供要封鎖周邊網路處之來路不明的商業電子郵件服務。

濫發垃圾郵件者會使用各種技術將垃圾郵件傳送至您的組織。Edge Transport Server 會利用一組互相合作的代理程式來提供不同層級的垃圾郵件篩選和保護，協助防止使用者收到垃圾郵件。在連接器上建立垃圾郵件防堵 (Tarpitting) 間隔會使電子郵件收集嘗試失效。

## Edge Transport 規則

Edge Transport 規則是用來控制在網際網路中傳送或接收郵件的流程。Edge Transport 規則設定於每部 Edge Transport Server 上，可將動作套用到符合指定條件的郵件，進而協助保護企業網路資源和資料。Edge Transport 規則條件是以資料為基礎，例如郵件主旨、本文、標頭或寄件者地址中的特定字或文字模式、垃圾郵件信賴等級 (SCL) 或附件類型。動作判定在指定條件成立時，郵件處理的方式。可能的動作包括隔離郵件、捨棄或拒絕郵件、附加其他收件者，或記錄事件。選用的例外狀況會將特定的郵件排除，不套用動作。

## 地址修正

地址修正功能會對外部收件者呈現一致的電子郵件地址外觀。您可在 Edge Transport Server 上設定地址修正功能，以修改輸入和輸出郵件上的 SMTP 位址。對於想要呈現一致電子郵件地址外觀的新合併組織，地址修正功能特別實用。

如需地址修正的相關資訊，請參閱[地址修正 Edge Transport server 上](address-rewriting-on-edge-transport-servers-exchange-2013-help.md)。


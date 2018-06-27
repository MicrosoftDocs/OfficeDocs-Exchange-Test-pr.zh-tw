---
title: '信箱伺服器: Exchange 2013 Help'
TOCTitle: 信箱伺服器
ms:assetid: 1aacc1c9-c81b-47d4-b222-ee73956cf968
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150491(v=EXCHG.150)
ms:contentKeyID: 50472727
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 信箱伺服器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-02-19_

在 Microsoft Exchange Server 2010 中，信箱伺服器角色主控信箱與共用資料夾資料庫，且提供電子郵件儲存。現在，在 Exchange Server 2013 中，信箱伺服器角色同時包含用戶端存取通訊協定、傳輸服務、信箱資料庫以及整合通訊元件。

在 Exchange 2013 中，信箱伺服器角色將透過下列程序直接與 Active Directory、用戶端存取伺服器、以及 Microsoft Outlook 客戶端互動：

  - 信箱伺服器會使用 LDAP 從 Active Directory 存取收件者、伺服器及組織組態資訊。

  - 用戶端存取伺服器會將用戶端的要求傳送到信箱伺服器，並將信箱伺服器中的資料傳回用戶端。信箱伺服器也會透過 NetBIOS 檔案共用，存取信箱伺服器上的線上通訊錄 (OAB) 檔案。用戶端存取伺服器傳送郵件、空閒／忙碌資料、客戶端設定檔設定、以及客戶端與信箱伺服器間的 OAB 資料。

  - 防火牆內部的 Outlook 用戶端存取 Client Access Server 以傳送和擷取郵件。防火牆外的 Outlook 用戶端能使用 Outlook 無所不在 (透過 HTTP Proxy 元件使用 RPC) 來存取用戶端存取伺服器。

  - 共用資料夾信箱可透過 RPC over HTTP 來存取，無論用戶端位於防火牆內或防火牆外。

  - 僅限系統管理員電腦會從 Microsoft Exchange Active Directory 拓撲服務擷取 Active Directory 拓撲資訊。它也會擷取電子郵件地址原則資訊及通訊清單資訊。

  - 用戶端存取伺服器使用 LDAP 或名稱服務提供者介面 (NSPI) 來聯絡 Active Directory 伺服器及擷取使用者的 Active Directory 資訊。

**信箱與客戶端存取伺服器互動與架構**

![Client Access Server 和信箱伺服器互動](images/JJ150491.d14577bf-14f9-40fa-bd49-a92932eb003a(EXCHG.150).gif "Client Access Server 和信箱伺服器互動")

若欲瞭解更多細節，請參閱 [Exchange 2013 的新功能](what-s-new-in-exchange-2013-exchange-2013-help.md) 中的「Exchange 2012 架構」章節。

## 新信箱功能

下列清單將簡述 Exchange 2013 信箱角色中的部分新加強功能：

  - Exchange 2010 資料庫可用性群組 (DAG) 演變：
    
      - 交易記錄碼以被動資料庫副本上的深入檢查點為更快的容錯移轉進行重構。
    
      - 為支援加強的站點備援，伺服器可能位於不同位置。

  - Exchange 2013 現在會主控部分用戶端存取元件、傳輸元件以及整合通訊元件。

  - Exchange Store 已透過 Managed 程式碼進行重新編寫，以加強額外 I/O 減少程度與可靠度的效能。

  - 每個 Exchange 2013 資料庫目前皆以其程序執行。

  - 智慧搜尋已取代 Exchange 2010 多信箱搜尋基礎結構。

## 保護 Mailbox Server 的安全

根據預設，信箱伺服器與其他 Exchange server role、網域控制站及通用類別目錄伺服器之間的 HTTP、Microsoft Exchange ActiveSync、POP3 及 IMAP4 通訊都會加密。此外，也請確定網際網路無法存取您的信箱伺服器。

## 相關資訊

[整合通訊](unified-messaging-exchange-2013-help.md)

[郵件流程](mail-flow-exchange-2013-help.md)

[高可用性和站台恢復](high-availability-and-site-resilience-exchange-2013-help.md)

[郵件原則及符合性](messaging-policy-and-compliance-exchange-2013-help.md)

[在 Exchange 2013 移動信箱](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

[管理 Exchange 2013 中的信箱資料庫](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)

[郵件原則及符合性](messaging-policy-and-compliance-exchange-2013-help.md)

[收件者](recipients-exchange-2013-help.md)

[共同作業](collaboration-exchange-2013-help.md)


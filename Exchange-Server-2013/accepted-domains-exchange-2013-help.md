---
title: '公認的網域: Exchange 2013 Help'
TOCTitle: 公認的網域
ms:assetid: c1839a5b-49f9-4c53-b247-f4e5d78efc45
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124423(v=EXCHG.150)
ms:contentKeyID: 50474118
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 公認的網域

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-06-16_

公認的網域是 Microsoft Exchange Server 2013 組織允許傳送或接收電子郵件的任何 SMTP 命名空間。公認的網域包含 Exchange 組織取得授權的那些網域。Exchange 組織在處理公認的網域中之收件者的郵件傳遞時，該組織即已取得授權。公認的網域中也有一些網域，Exchange 組織會接收這些網域的郵件，再轉送至組織外部的電子郵件伺服器以傳遞給收件者。

**目錄**

Configuring accepted domains

Authoritative domains

Relay domains

Internal relay domain

External relay domain

Accepted domains and email address policies

## 設定公認的網域

系統會將公認的網域設定為 Exchange 組織的全域設定。您必須設定 Exchange 組織用於轉送或傳遞郵件的每個網域，做為組織中公認的網域。

公認的網域共有三種類型：授權、內部轉送及外部轉送。這些公認的網域類型會在下列各節中說明。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您的周邊網路中有訂閱的 Edge Transport Server，則可在 Exchange 組織的 Mailbox Server 上設定公認網域。公認網域組態會在 EdgeSync 同步處理期間複寫至 Edge Transport Server。如需詳細資訊，請參閱<a href="edge-subscriptions-exchange-2013-help.md">Edge 訂閱</a>。</td>
</tr>
</tbody>
</table>


## 授權網域

組織可能會有多個 SMTP 網域。組織的這組電子郵件網域就是授權網域。在 Exchange 2013 中，如果 Exchange 組織主控此 SMTP 網域的收件者信箱，則公認的網域就是授權網域。

安裝第一個 Exchange 2013 信箱伺服器時，預設會將某個公認的網域設定為 Exchange 組織的授權網域。預設的公認網域就是樹系根網域的網域全名 (FQDN)。通常，內部網域名稱會與外部網域名稱不同。例如，您的內部網域名稱可能是 contoso.local，但是外部網域名稱是 contoso.com。組織的網域名稱系統 DNS 郵件交換程式 (MX) 記錄會參照 contoso.com。contoso.com 是您在建立電子郵件地址原則時，指派給使用者的 SMTP 命名空間。您必須建立公認的網域以符合外部網域名稱。

若要深入了解，請參閱：

  - [設定 Exchange 組織中公認的網域成為授權](configure-an-accepted-domain-within-your-exchange-organization-as-authoritative-exchange-2013-help.md)

  - [將 Exchange 設定為接受多個授權網域的郵件](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md)

## 轉送網域

系統通常會設定大部分面對網際網路的郵件伺服器，以拒絕其他網域透過它們轉送。不過，有時候您可能會想要讓合作夥伴或分公司透過 Exchange 伺服器轉送電子郵件。在 Exchange 2013 中，您可以將公認的網域設定為轉送網域。您的組織會接收電子郵件，再將郵件轉送給另一部電子郵件伺服器。

您可以將轉送網域設定為內部轉送網域或外部轉送網域。這兩種轉送網域類型會在下列各節中說明。

## 內部轉送網域

當您設定內部轉送網域時，此網域中的部分或全部收件者在此 Exchange 組織中沒有信箱。系統會透過這個 Exchange 組織中的傳輸伺服器，為此網域轉送來自網際網路的郵件。本節所說明的案例使用此組態。

在兩個以上不同的郵件系統之間，組織可能必須共用相同的 SMTP 位址空間。例如，在 Exchange 與協力廠商郵件系統之間，或在不同 Active Directory 樹系中設定的 Exchange 環境之間，您可能必須共用 SMTP 位址空間。在這些案例中，每一個電子郵件系統中的使用者在其電子郵件地址都有相同的網域尾碼。

若要支援這些案例，您必須建立一個設定為內部轉送網域的公認網域。您也必須新增由信箱伺服器提供且設為將電子郵件傳送至共用位址空間的傳送連接器。如果公認的網域已設定為授權網域，但在 Active Directory 中找不到收件者，則未傳遞回報 (NDR) 會傳回給寄件者。設定為內部轉送網域的公認網域會先嘗試傳遞至 Exchange 組織中的收件者。如果找不到收件者，郵件會路由至符合最近位址空間的傳送連接器。

如果組織包含多個樹系，而且已設定全域通訊清單 (GAL) 同步處理，則可能會將某個樹系的 SMTP 網域設定為第二個樹系中的內部轉送網域。從網際網路寄給內部轉送網域中的使用者的郵件會轉送到相同組織內的信箱伺服器。接著，接收信箱伺服器會將這些郵件路由傳送至收件者樹系中的信箱伺服器。將 SMTP 網域設定為內部轉送網域，確定 Exchange 組織接受指向該網域的電子郵件。組織的連接器組態會決定郵件的路由傳送方式。

若要深入了解，請參閱[利用 Exchange 組織外部的信箱為業務單位設定公認的網域](configure-an-accepted-domain-for-a-business-unit-with-mailboxes-outside-your-exchange-organization-exchange-2013-help.md)。

## 外部轉送網域

設定外部轉送網域時，會將郵件轉送至 Exchange 組織外部及組織周邊網路外部的電子郵件伺服器。

如需詳細資訊，請參閱[獨立業務單位設定公認的網域](configure-an-accepted-domain-for-an-independent-business-unit-exchange-2013-help.md)。

## 公認的網域和電子郵件地址原則

您需要設定公認的網域才能使用該 SMTP 位址空間中的電子郵件地址原則。當您建立公認的網域時，您可以使用的位址空間中萬用字元 （\*） 表示的所有子網域的 SMTP 位址空間也可接受Exchange組織。例如，若要為公認的網域設定 contoso.com 和其所有子網域，請輸入**\*。 contoso.com**作為 SMTP 位址空間。公認的網域項目都能使用的電子郵件地址原則自動使用。

如果刪除用於電子郵件地址原則的公認網域，則此原則不再有效，而且擁有該 SMTP 網域之電子郵件地址的收件者也無法傳送或接收電子郵件。


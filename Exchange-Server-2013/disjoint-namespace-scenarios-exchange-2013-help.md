---
title: '斷續的命名空間案例: Exchange 2013 Help'
TOCTitle: 斷續的命名空間案例
ms:assetid: 90101d49-6f45-44be-8a93-eeb2c8283e3b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb676377(v=EXCHG.150)
ms:contentKeyID: 50473732
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 斷續的命名空間案例

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

本主題提供有關脫離命名空間及支援案例之概念的相關資訊，用來在擁有脫離命名空間的網域中部署 Microsoft Exchange 2013。

**目錄**

DNS 和 NetBIOS 網域名稱

脫離的命名空間

Exchange 2013 和脫離的命名空間

允許 Exchange 2013 伺服器存取脫離的網域控制站

檢視執行 Windows Server 2008 之電腦的 DNS 和 NetBIOS 名稱相關資訊

## DNS 和 NetBIOS 網域名稱

首先要了解一些背景。網際網路上的每一部電腦都有網域名稱系統 (DNS) 名稱，也稱為*電腦名稱*或*主機名稱*。每一部執行 Windows 作業系統且具有網路功能的電腦也具有 NetBIOS 名稱。

在 Active Directory 網域中執行 Windows 的電腦會同時擁有 DNS 網域名稱和 NetBIOS 網域名稱，如下所示：

  - **DNS 網域名稱**   DNS 網域名稱是由一或多個子網域組成，並且以句點 (**.**) 分隔，終止於最上層網域名稱。例如，在 DNS 網域名稱 corp.contoso.com 中，子網域為 corp 和 contoso，而最上層網域名稱為 com。

  - **NetBIOS 網域名稱**   通常，NetBIOS 網域名稱是 DNS 網域名稱的子網域。例如，如果 DNS 網域名稱是 contoso.com，則 NetBIOS 網域名稱是 contoso。如果 DNS 網域名稱是 corp.contoso.com，則 NetBIOS 網域名稱是 corp。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需尋找執行 Windows Server 2008 電腦的 DNS 和 NetBIOS 資訊，請參閱檢視執行 Windows Server 2008 之電腦的 DNS 和 NetBIOS 名稱相關資訊。</td>
</tr>
</tbody>
</table>


在 Active Directory 網域中的電腦也具有主要 DNS 尾碼，而且可能還有其他 DNS 尾碼。根據預設，主要 DNS 尾碼與 DNS 網域名稱相同。如需如何變更主要 DNS 尾碼的詳細步驟，請參閱本主題稍後的程序。

當您設定網域中的第一個網域控制站時，可以定義 Active Directory 網域的 DNS 網域名稱和 NetBIOS 網域名稱。如需設定網域控制站的相關資訊，請參閱[網域控制站角色](https://go.microsoft.com/fwlink/p/?linkid=268367) 和 [Active Directory 網域服務概述](https://go.microsoft.com/fwlink/p/?linkid=268366)。

## 脫離的命名空間

在大多數網域拓撲中，網域中電腦的主要 DNS 尾碼與 DNS 網域名稱相同。

在某些情況下，您可能要讓這些命名空間不同。這稱為*脫離的命名空間*。例如，公司的合併和收購行為可能使您的拓撲中具有脫離的命名空間。此外，如果貴公司的 DNS 管理工作切割給管理 Active Directory 的系統管理員和管理網路的系統管理員，那麼您可能需要在拓撲中使用脫離的命名空間。

脫離的命名空間案例是指電腦的主要 DNS 尾碼不符合電腦所在 DNS 網域名稱。具有不符合之主要 DNS 尾碼的電腦即稱為*脫離的*電腦。另一個脫離的命名空間案例發生在網域控制站的 NetBIOS 網域名稱不符合 DNS 網域名稱的情況。

## Exchange 2013 和脫離的命名空間

Exchange 2013 支援以下三個案例在具有脫離命名空間的網域中部署 Exchange：

  - **主要 DNS 尾碼和 DNS 網域名稱不同**   網域控制站的主要 DNS 尾碼與 DNS 網域名稱不同。屬於網域成員的電腦可以是脫離的或不脫離的。

  - **成員電腦為脫離的狀態**   在 Active Directory 網域中的成員電腦是脫離的，即使網域控制站不是脫離的。

  - **網域控制站的 NetBIOS 名稱與其 DNS 網域名稱的子網域不同**   網域控制站的 NetBIOS 網域名稱與該網域控制站的 DNS 網域名稱的子網域不同。

這些案例將在以下幾節中詳述。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>目前支援在此主題中說明的任何脫離的命名空間案例中執行 Exchange 2013。不過，如果脫離的命名空間案例不屬於本主題中所說明的案例之一，請務必與 Microsoft 服務合作來部署 Exchange 2013。如需相關資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=94845">Microsoft 服務</a>。</td>
</tr>
</tbody>
</table>


## 案例：主要 DNS 尾碼和 DNS 網域名稱不同

在此案例中，網域控制站的主要 DNS 尾碼與 DNS 網域名稱不同。在此案例中，網域控制站是脫離的。屬於網域成員的電腦，包括 Exchange 伺服器與 Microsoft Outlook 用戶端電腦，其主要 DNS 尾碼可以符合網域控制站的主要 DNS 尾碼，或符合 DNS 網域名稱。

## 案例：成員電腦是脫離的

在此案例中，安裝 Exchange 2013 的成員電腦之主要 DNS 尾碼與 DNS 網域名稱不同，即使網域控制站的主要 DNS 尾碼與 DNS 網域名稱相同。在此案例中，您具有不脫離的網域控制站和脫離的成員電腦。執行 Outlook 的成員電腦，其主要 DNS 尾碼可以符合脫離的 Exchange 伺服器或符合 DNS 網域名稱。

## 案例：網域控制站的 NetBIOS 與其 DNS 網域名稱不同

在此案例中，網域控制站的 NetBIOS 網域名稱與相同網域控制站的 DNS 網域名稱不同。

**NetBIOS 網域名稱不符合 DNS 網域名稱**

![NetBIOS 網域名稱不符合 DNS 網域名稱](images/Bb676377.1ee18cb6-0296-4875-b572-0ddf33f65f7c(EXCHG.150).gif "NetBIOS 網域名稱不符合 DNS 網域名稱")

## 允許 Exchange 2013 伺服器存取脫離的網域控制站

若要讓 Exchange 2013 伺服器存取脫離的網域控制站，您必須修改網域物件容器上的 **msDS-AllowedDNSSuffixes**Active Directory 屬性。您必須將兩個 DNS 尾碼都新增至屬性中。如需修改屬性的詳細步驟，請參閱[電腦的主要 DNS 尾碼不符合電腦所在網域的 FQDN](https://go.microsoft.com/fwlink/p/?linkid=98848)。

此外，為了確保 DNS 尾碼搜尋清單包含組織內部署的所有 DNS 命名空間，您必須針對網域內每部脫離的電腦設定搜尋清單。命名空間清單不僅要包含網域控制站的主要 DNS 尾碼以及 DNS 網域名稱，也要包含其他可能與 Exchange 交互操作之伺服器 (例如監視伺服器或協力廠商應用程式的伺服器) 的任何額外命名空間。做法是設定網域的群組原則。如需群組原則的相關資訊，請參閱下列主題：

  - [群組原則常見問題集 (FAQ)](https://go.microsoft.com/fwlink/p/?linkid=100128)

  - [在 Windows Server 2003 中 DNS 的新群組原則](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=294785)

  - [群組原則](https://go.microsoft.com/fwlink/p/?linkid=268043)

如需如何設定 DNS 尾碼搜尋清單群組原則的詳細步驟，請參閱[設定脫離的命名空間的 DNS 尾碼搜尋清單](configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md)。

## 檢視執行 Windows Server 2008 之電腦的 DNS 和 NetBIOS 名稱相關資訊

1.  按一下 \[開始\]，在\[電腦\] 上按一下滑鼠右鍵，然後按一下 \[內容\]。

2.  在 **\[系統\]** 中，DNS 主機名稱和主要 DNS 尾碼會顯示於 **\[電腦名稱、網域及工作群組設定\]** 下，就在 **\[完整電腦名稱\]** 旁。DNS 網域名稱會顯示在 **\[網域\]** 旁。

3.  按一下 \[變更設定\]。

4.  在 \[系統內容\] 的 \[電腦名稱\] 索引標籤上，按一下 \[變更\]。

5.  在 **\[電腦名稱/網域變更\]** 頁面上，按一下 **\[其他\]**。主要 DNS 尾碼會顯示在 **\[這部電腦的主要 DNS 尾碼\]** 下。NetBIOS 電腦名稱會顯示在 **\[NetBIOS 電腦名稱\]** 下。
    
    若要變更主要 DNS 尾碼，請在 \[這部電腦的主要 DNS 尾碼\] 下輸入新的主要 DNS 尾碼，然後按一下 \[確定\]。

6.  在 \[命令提示字元\] 視窗中輸入 **set**。變數 USERDNSDOMAIN 會顯示 DNS 網域名稱。變數 USERDOMAIN 會顯示 NetBIOS 網域名稱。


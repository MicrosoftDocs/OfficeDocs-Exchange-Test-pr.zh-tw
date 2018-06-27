---
title: '通訊錄原則: Exchange Online Help'
TOCTitle: 通訊錄原則
ms:assetid: d0a916a1-e3ed-49ae-b116-a559be0dcce6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh529948(v=EXCHG.150)
ms:contentKeyID: 50474264
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 通訊錄原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

了解如何到特定群組 Outlook 和Outlook Web App中建立自訂的 Gal 區隔全域通訊清單。

全域通訊清單 (GAL) 區隔 (也稱為*GAL 區隔*) 是讓系統管理員可以區隔使用者到特定的母體提供其組織的 GAL 的自訂的檢視的程序。通訊錄原則 (Abp) 允許您線段使用者到特定群組提供貴組織的全域通訊清單 (GAL) 的自訂的檢視。建立 ABP，您可以對原則指派的 GAL、 離線通訊錄 (OAB)、 \[聊天室\] 清單中和一個以上的通訊清單。然後您可指派 ABP 提供其到 Outlook 與Outlook Web App中自訂 GAL 存取的信箱使用者。目標是提供簡易的機制來完成需要多個的 Gal 的內部部署組織的 GAL 區隔。.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Abp 都是要最佳化每個使用者群組的 GAL 和通訊清單、 不能不易為查看彼此或與其他組織中的使用者進行通訊。Abp 目錄觀點來看，不法律分離從建立虛擬區隔的使用者。</td>
</tr>
</tbody>
</table>


**目錄**

How ABPs work

ABP example

Entourage, Outlook for Mac, and ABPs

## ABP 運作方式

ABP 包含下列清單：

  - 一個 GAL

  - 一個 OAB

  - 一個會議室清單 (預約用)

  - 一或多個通訊清單

下圖，通訊錄原則的所組成的各種 （示底端一半的圖） 組織中存在的地址物件子集。所產生的 ABP 範圍等於的 GAL 中的原則，在此案例的 GAL1 包含。當 ABP，建立並指派給使用者時、 ABP 的地址物件會成為使用者能夠檢視物件的範圍。

![通訊錄原則的概觀](images/Hh529948.68084064-7319-431b-be3b-0cce761258b1(EXCHG.150).gif "通訊錄原則的概觀")

您可以使用下列方式指定 ABP 給個別信箱使用者：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>建立新信箱或使用現有的信箱？</th>
<th>命令介面</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>新增</p></td>
<td><p><a href="https://technet.microsoft.com/zh-tw/library/aa997663(v=exchg.150)">New-Mailbox</a> 指令程式，含 <em>AddressBookPolicy</em> 參數</p></td>
</tr>
<tr class="even">
<td><p>現有的</p></td>
<td><p><a href="https://technet.microsoft.com/zh-tw/library/bb123981(v=exchg.150)">Set-Mailbox</a> 指令程式，含 <em>AddressBookPolicy</em> 參數</p>
<p></p></td>
</tr>
</tbody>
</table>


當使用者的用戶端應用程式連接到 Client Access server 在 Exchange 2013 Abp 就會生效。如果您變更 ABP，更新的 ABP 才會生效直到使用者重新啟動或重新連接他們的用戶端或重新啟動Exchange 2013 Mailbox server 上的 RPC Client Access server。

## 通訊錄原則路由代理程式

在不使用 Abp Exchange 組織中發生下列事項 Outlook 或Outlook Web App中建立及傳送至 Exchange 組織中的另一個收件者電子郵件：

1.  電子郵件地址會解析。例如，如果您在**欄位中**輸入**kweku@contoso.com** ，SMTP 電子郵件地址會解析至使用者的顯示名稱**Kweku Ako Adjei**中。

2.  您可以檢視其他人的連絡人卡片。解析名稱之後，您可以連按兩下 \[使用者的名稱並檢視其連絡人資訊，例如 office 和電話號碼。

如果您使用 Abp，而且不想不同的虛擬組織中的使用者能夠檢視彼此的潛在私人資訊，您可以開啟的 Address Book Policy Routing 代理程式。ABP 路由代理程式會控制 \[收件者在組織中的解決方式傳輸代理程式。當安裝及設定 ABP 路由代理程式時，指派給不同的 Gal 的使用者顯示為外部收件者，因為他們無法檢視外部收件者的連絡人卡片。

如需如何開啟中Exchange OnlineABP 路由代理程式的詳細資訊，請參閱[開啟 \[通訊錄原則路由](https://technet.microsoft.com/zh-tw/library/jj891095\(v=exchg.150\))。

如需關於如何在 Exchange Server 中開啟 ABP 路由代理程式的詳細資訊，請參閱[安裝及設定 Address Book Policy Routing 代理程式](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md)。

## ABP 範例

下圖、 Fabrikam 及 Tailspin Toys 共用相同的 Exchange 組織與相同 CEO。執行長是唯一的員工通用這兩家公司。

![兩家公司一位執行長](images/Hh529948.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "兩家公司一位執行長")

此組態包含三個 ABP：

  - 一個包含 Fabrikam 員工和 CEO

  - 一個包含 Tailspin Toys 員工和 CEO

  - 一個僅包含 CEO

ABP 遵循下列規則：

  - Tailspin Toys 中的使用者瀏覽 GAL 時，只會看見 Tailspin Toys 員工和 CEO。

  - Fabrikam 中的使用者瀏覽 GAL 時，只會看見 Fabrikam 員工和 CEO。

  - CEO 瀏覽 GAL 時，可看見所有 Fabrikam 及 Tailspin Toys 員工。

  - 檢視執行長的群組成員資格的使用者可以看到屬於使用者的公司的群組。就不會看到其他公司中存在的群組。

## Entourage、Outlook for Mac 與 ABP

Abp 將不會為 Entourage 的使用者或 Outlook for Mac 使用者連接至其公司網路功能。在公司網路內 Entourage 和 Outlook for Mac 用戶端直接連接到的通用類別目錄伺服器和查詢 Active Directory 直接，而不是使用用戶端存取伺服器。不過，Outlook for Mac 2011 從網際網路連線的用戶端可以使用 OAB 或 Exchange Web 服務 (EWS)。因此，這些用戶端可搜尋的 GAL 指派 ABP.為基礎若要深入了解管理 Outlook for Mac 2011，請參閱Planning for Outlook for Mac 2011[](https://go.microsoft.com/fwlink/p/?linkid=231878)

## 相關資訊

[案例： 部署通訊錄原則](scenario-deploying-address-book-policies-exchange-2013-help.md)

Exchange Online 中的[處理 \[線上\] 通訊錄原則程序](https://technet.microsoft.com/zh-tw/library/jj891096\(v=exchg.150\))


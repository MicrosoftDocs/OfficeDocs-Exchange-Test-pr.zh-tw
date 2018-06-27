---
title: '離線通訊錄: Exchange 2013 Help'
TOCTitle: 離線通訊錄
ms:assetid: a6bcb072-4ab9-400e-a5d0-c05264629097
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232155(v=EXCHG.150)
ms:contentKeyID: 50473924
ms.date: 01/12/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 離線通訊錄

 

_**適用版本：**Exchange Server 2010, Exchange Server 2013_

_**上次修改主題的時間：**2014-11-16_

離線通訊錄 (OAB) 是已下載的通訊清單集合副本，可讓 Microsoft Outlook 使用者在與伺服器中斷連線時存取通訊錄資訊。Microsoft Exchange 會產生新的 OAB 檔案，壓縮檔案，然後將檔案放在本機共用上。您可以選擇離線工作的使用者可以用哪些通訊清單，也可以設定散佈通訊錄的方法。

若要深入了解通訊清單，請參閱[通訊清單](address-lists-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>OAB 資料是由 Microsoft Exchange OABGen 服務產生，該服務是一個信箱助理員。如果您使用安全性描述元來避免使用者檢視 Active Directory 中的特定收件者，則下載 OAB 的使用者將能夠檢視那些隱藏的收件者。因此，若要隱藏通訊清單中的收件者，請設定 <a href="https://technet.microsoft.com/zh-tw/library/aa998596(v=exchg.150)">Set-PublicFolder</a>、<a href="https://technet.microsoft.com/zh-tw/library/aa995950(v=exchg.150)">Set-MailContact</a>、<a href="https://technet.microsoft.com/zh-tw/library/aa995971(v=exchg.150)">Set-MailUser</a>、<a href="https://technet.microsoft.com/zh-tw/library/bb123796(v=exchg.150)">Set-DynamicDistributionGroup</a>、<a href="https://technet.microsoft.com/zh-tw/library/bb123981(v=exchg.150)">Set-Mailbox</a> 和 <a href="https://technet.microsoft.com/zh-tw/library/bb124955(v=exchg.150)">Set-DistributionGroup</a> Cmdlet 上的參數 <em>HiddenFromAddressListsEnabled</em>。或者也可以建立一個新的預設 OAB，其中不含隱藏的收件者。如需如何在 OAB 中新增或移除通訊清單的詳細資訊，請參閱<a href="add-an-address-list-to-or-remove-an-address-list-from-an-offline-address-book-exchange-2013-help.md">地址清單中新增或移除的通訊清單的離線通訊錄</a>。</td>
</tr>
</tbody>
</table>


要尋找與 OAB 相關的管理工作嗎？請參閱[離線通訊錄程序](offline-address-book-procedures-exchange-2013-help.md)。

**目錄**

在各種 Exchange 版本之間移動 OAB

OAB 版本 4 和 Outlook 用戶端

Web 式發佈

OAB 考量

## 在各種 Exchange 版本之間移動 OAB

在 Exchange 2007 和 Exchange 2010 中，您可以使用 **Move-OfflineAddressBook** Cmdlet 將 OAB 產生檔移動到另一個信箱伺服器中。Exchange 2013 僅支援 OAB (版本 4)。這與 Exchange 2010 中預設的 OAB 版本相同，您無法設定 Exchange 2013 產生其他 OAB 版本，OAB 產生是在與組織信箱所在的信箱伺服器上進行。因此，在 Exchange 2013 中，若要移動 OAB 產生檔，您必須移動組織信箱。您只能將 OAB 產生檔移動到另一個 Exchange 2013 信箱資料庫。您不能將 OAB 產生檔移動到舊版的 Exchange 中。若要尋找 Exchange 2013 OAB 組織信箱，請執行下列命令介面命令：

    Get-Mailbox -Arbitration | where {$_.PersistedCapabilities -like "*oab*"}

然後，您可以使用 **MoveRequest** Cmdlet 移動信箱。

## OAB 版本 4 和 Outlook 用戶端

Exchange 2013 僅支援 OAB版本 4，OAB 版本 4 已在 Exchange 2003 Service Pack 2 (SP2) 中引進且由 Outlook 2007、Outlook 2010 和 Outlook 2013 支援。此 Unicode OAB 允許用戶端電腦接收非完整 OAB 下載的更新，同時可降低檔案大小。

## 使用 OAB 版本 4 的 Outlook 用戶端

針對使用 OAB 版本 4 的 Outlook 2013、Outlook 2010、Outlook 2007 和用戶端，如果 changes.oab 檔案的大小是整個 OAB 檔案大小的一半 (或更多)，則 Outlook 會開始下載完整的 OAB。

## Web 式發佈

*Web 式發佈* 是離線工作之 Outlook 2013、Outlook 2010 或 Outlook 2007 用戶端存取 OAB 所用的發佈方式。

使用 Web 式發佈的優點有好幾項，包括：

  - 同時支援更多用戶端電腦。

  - 減少頻寬使用。

  - 更完善控制 OAB 發佈點。如果使用 Web 式發佈，則發佈點是 HTTPS 網址，用戶端電腦可以從該處下載 OAB。

為了發揮 Web 式發佈的最大功能，用戶端電腦必須執行 Outlook 2013、Outlook 2010 或 Outlook 2007。

若要正常運作，Web 式發佈取決於下列元件：

  - **OAB 產生程序**   這是 Exchange 用來建立及更新 OAB 的程序。為了建立和更新 OAB，OABGen 服務會在組織信箱所在的信箱伺服器上執行 OABGen 服務。若要支援 OAB 發佈，此伺服器必須為 Exchange 信箱伺服器。

  - **離線通訊錄 (OAB) 發佈**   如果用戶端初始化 OAB 發佈要求，該要求將被傳遞給用戶端存取伺服器。之後，用戶端存取伺服器可以將要求路由至裝載 OAB 檔案的信箱伺服器。OAB 檔隨即被直接從信箱伺服器發佈到用戶端。

  - **OAB 虛擬目錄**   OAB 虛擬目錄是 Web 式發佈方法所使用的發佈點。安裝 Exchange 時，預設會在網際網路資訊服務 (IIS) 的預設內部網站中建立名為 **OAB** 的新虛擬目錄。如果您有一些用戶端使用者是從組織的防火牆之外連接到 Outlook，則可以新增一個外部網站。或者，當您在命令介面中執行 **New-OABVirtualDirectory** Cmdlet 時，本機 Exchange 用戶端存取伺服器上的預設 IIS 網站中也會建立一個名為 OAB 的新虛擬目錄。如需詳細資訊，請參閱[建立離線通訊錄虛擬目錄](create-an-offline-address-book-virtual-directory-exchange-2013-help.md)。

  - **自動探索服務**   這是 Outlook 2013、Outlook 2010、Outlook 2007 以及部分可自動設定用戶端來存取 Exchange 之行動裝置中的功能。服務會在 Client Access Server 上執行，並傳回特定用戶端連線的正確 OAB URL。

## OAB 考量

最佳作法是，不論您使用單一 OAB 或多個 OAB，請在計劃及實作 OAB 策略時，考量下列因素：

  - 您組織中每個 OAB 的大小。如需詳細資訊，請參閱本主題稍後的 OAB 大小考量。

  - OAB 下載的數目。

  - 父系辦別具名變更的數目和頻率。

  - SMTP 地址不符。

  - 對目錄所做變更的總數。

## OAB 大小考量

有些組織的 OAB 是一些小型檔案，遠端使用者偶爾會下載這些檔案。這類組織的 OAB 下載通常不會有問題。但是，對於有些擁有大型目錄的大型組織，或者使用 Exchange 快取模式部署了 Outlook 2003 的組織，就會有很大的關係，尤其組織若是已將 Exchange 伺服器合併到地區性資料中心時更為明顯。

OAB 大小可能有幾 MB 到幾百 MB 的變化。下列因素可能影響 OAB 的大小：

  - 公司中憑證的使用量。公開金鑰基礎結構 (PKI) 憑證越多，OAB 越大。PKI 憑證的範圍從 1 KB 到 3 KB。這些都是 OAB 大小的單一最大構成因素。

  - Active Directory 中的郵件收件者數目。

  - Active Directory 中的通訊群組數目。

  - 公司針對每個擁有信箱功能或郵件功能之物件，加入 Active Directory 中的資訊。例如，有些組織會為每個使用者填入地址內容，有些則不會。


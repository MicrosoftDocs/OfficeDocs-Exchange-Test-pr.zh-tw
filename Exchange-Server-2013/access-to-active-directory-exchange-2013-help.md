---
title: 'Active Directory 權: Exchange 2013 Help'
TOCTitle: Active Directory 權
ms:assetid: 61080b45-8bce-4c23-b744-ed264d5f0b7d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998561(v=EXCHG.150)
ms:contentKeyID: 50473322
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory 權

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange Server 2013儲存Active Directory目錄服務資料庫中的所有組態和收件者資訊。當執行Exchange 2013的電腦需要收件者的資訊和Exchange組織的組態資訊時，則必須查詢Active Directory存取資訊。Active Directory伺服器必須是可供Exchange 2013以正常運作。

本主題說明如何Exchange 2013儲存及擷取資訊Active Directory ，規劃Active Directory存取。本主題也討論您應該注意如果您嘗試復原已刪除的Exchange 2013Active Directory物件的問題。

## 儲存在 Active Directory 中的 Exchange 資訊

Active Directory 資料庫以三種類型的邏輯磁碟分割來儲存資訊，如下列各節所述：

  - 架構分割

  - 設定分割

  - 網域分割

## 架構分割

架構磁碟分割會儲存以下兩種類型的資訊：

  - **架構類別**定義可在 Active Directory 中建立及儲存的所有物件類型。

  - **架構屬性**定義可用來描述 Active Directory 中所儲存之物件的所有內容。

當您在樹系中安裝第一個Exchange 2013伺服器角色或執行Active Directory準備程序時， Active Directory準備程序會新增多個類別及 \[ Active Directory結構描述屬性。新增至結構描述的類別用來建立Exchange-代理程式及連接器之類的特定物件。會新增至結構描述的屬性用於設定Exchange位特定的物件及擁有郵件功能的使用者和群組。這些屬性包含內容，例如MicrosoftOffice Outlook Web Access與MicrosoftExchange整合通訊 (UM) 設定。每個網域控制站和樹系的通用類別目錄伺服器包含結構描述分割區的完整複本。

如需 Exchange 2013 中的架構修改的詳細資訊，請參閱 [Exchange 2013 Active Directory 架構變更](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)。

## 設定分割

組態磁碟分割儲存整個樹系的組態資訊。此設定的資訊包括Active Directory網站、 Exchange通用設定、 傳輸設定與信箱原則的設定。每種類型的組態資訊都會儲存在組態分割區中的容器。Exchange組態資訊都會儲存在組態磁碟分割服務容器下的子資料夾。會儲存在此容器中的資訊包括下列：

  - 通訊清單

  - 通訊錄信箱原則

  - 系統管理群組

  - 用戶端存取設定

  - 連線

  - 行動信箱設定

  - 通用設定

  - 監視設定

  - 系統原則

  - 保留原則容器

  - 傳輸設定

樹系中的每一個網域控制站及通用類別目錄伺服器都包含組態磁碟分割的完整複本。

## 網域分割

網域磁碟分割儲存的資訊及Active Directory系統管理員所建立的組織單位中預設容器。這些容器保留特定網域的物件。此資料會包含在該網域Exchange system 物件和電腦、 使用者和群組的相關資訊。在安裝Exchange 2013時Exchange更新以支援Exchange功能此分割區中的物件。這項功能會影響方式收件者資訊儲存及存取。

每個網域控制站會包含它是授權網域的網域分割完整複本。每個樹系的通用類別目錄伺服器會包含在樹系中每個網域分割區中的資訊子集。

## Exchange 2013 如何存取 Active Directory 中的資訊

Exchange 2013使用Active Directory API 來存取儲存在Active Directory中的資訊。在所有Exchange 2013伺服器角色上執行 Microsoft ExchangeActive Directory拓撲服務。此服務會讀取Active Directory的所有分割區中的資訊。擷取的資料快取及Exchange 2013伺服器用來探索的組織中的所有Exchange服務Active Directory網站位置。

如需拓撲及服務探索的相關資訊，請參閱[規劃使用 Active Directory 站台的路由傳送郵件](planning-to-use-active-directory-sites-for-routing-mail-exchange-2013-help.md)。

Exchange 2013是偏好的目錄伺服器位於相同的網站以最佳化網路流量的Exchange伺服器通訊Active Directory網站感知應用程式。每個Exchange 2013組織的伺服器角色必須彼此Active Directory擷取收件者的相關資訊及其他Exchange 2013伺服器角色的相關資訊。下列各節說明每個伺服器角色會取得資料。

根據預設，每當Exchange 2013 server 開始，它繫結至隨機選取的網域控制站和自己站台中的通用類別目錄伺服器。您可以在 Exchange 管理命令介面中使用**Get-ExchangeServer**指令程式來檢視所選取的目錄伺服器。您也可以使用**Set-ExchangeServer**指令程式來設定靜態清單中的網域控制站的Exchange 2013伺服器應該繫結或排除的網域控制站清單。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Windows Server 2008網域控制站可以設定為唯讀目錄伺服器。當您想要部署網域控制站或通用類別目錄伺服器的遠端網站的驗證和授權的目的，但不想要允許管理員可以在該網站將變更寫入Active Directory，這個設定特別有用。不過，您不能Exchange 2013 server 部署中含有只有唯讀目錄伺服器的任何網站。</td>
</tr>
</tbody>
</table>


## Mailbox server role

Mailbox server role 儲存在信箱使用者的組態資訊，並將儲存Active Directory。此外，如Exchange 2013、 信箱伺服器包含在 Exchange 2010 中找到的所有傳統伺服器元件： 用戶端存取通訊協定、 傳輸服務、 信箱資料庫和整合通訊。信箱伺服器負責處理所有作用中的信箱在該伺服器上的活動。

## Client Access server role

在Exchange 2013、 用戶端存取伺服器提供驗證、 有限的重新導向及 proxy 服務。用戶端存取伺服器本身沒有任何資料轉譯。用戶端存取伺服器是細並無狀態的伺服器。沒有永不不要排入佇列或儲存在用戶端存取伺服器上。Client Access server 提供所有一般用戶端存取通訊協定： HTTP、 POP 與 IMAP 和 SMTP。

## 復原已刪除的 Exchange 物件

Active Directory 資源回收筒藉由提升對保留和復原意外刪除之 Active Directory 物件，而不是從備份還原 Active Directory 資料、重新啟動 Active Directory 網域服務 (AD DS)，或重新啟動網域控制站的能力，使目錄服務的停機時間降至最低。

若要了解有關復原最重要的是刪除Exchange-相關Active Directory物件是Exchange物件不存在的隔離。例如，當您啟用郵件功能的使用者、 數個不同的原則及連結計算您目前的Exchange設定為基礎的使用者。當您還原已刪除的Exchange設定\] 或 \[收件者物件時可能發生的兩個問題是：

  - **衝突**  跨樹系，部分Exchange屬性必須是唯一的。例如 proxy (email) 位址不必須相同的兩個不同的使用者。Active Directory不會使用 proxy 位址唯一性 —Exchange系統管理工具\] 核取獨特性要求。Exchange電子郵件地址原則也會自動解決可能發生的衝突的決定性規則為基礎的 proxy 位址指派。因此，則有可能還原Exchange使用者物件與因此，建立利用 proxy 位址衝突或應該是唯一的其他屬性。

  - **更正**   Exchange具有自動指派給不同的原則或設定的規則。如果您刪除收件者，然後變更的規則或原則還原Exchange使用者物件可能會導致使用者已指派了錯誤的原則 （或甚至是以不復存在的原則）。

當您復原已刪除的 Exchange 相關物件時，以下指導方針可協助您將問題減至最少：

  - 如果您刪除Exchange組態物件使用Exchange管理工具時，不要還原物件。相反地，建立一次使用Exchange管理工具 （Exchange系統管理中心或Exchange管理命令介面） 物件。

  - 如果您刪除Exchange組態物件而不需使用Exchange管理工具時，儘速復原物件。更多系統管理和設定所進行的變更已在系統中刪除，自多可能很還原物件會導致設定錯誤。

  - 如果您復原刪除Exchange recipients （連絡人、 使用者或通訊群組） 密切監視的衝突與復原物件與相關的錯誤。如果Exchange原則\] 或 \[收件者與相關的其他設定可能會有已修改之後刪除，重新將目前原則套用至以確保它們正確設定還原收件者。

## 相關資訊

[Active Directory 資源回收筒逐步說明指南](https://go.microsoft.com/fwlink/p/?linkid=178720)

[Active Directory 系統管理中心增強功能 (等級 100) 簡介](https://go.microsoft.com/fwlink/p/?linkid=267641)

[進階 AD DS 管理使用 Active Directory 系統管理中心 (等級 200)](https://go.microsoft.com/fwlink/p/?linkid=267642)


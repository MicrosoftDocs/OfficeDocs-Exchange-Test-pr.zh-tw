---
title: '收件者: Exchange 2013 Help'
TOCTitle: 收件者
ms:assetid: 40300ed4-85a5-463d-bb3a-cf787bd44e9d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201680(v=EXCHG.150)
ms:contentKeyID: 50473062
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 收件者

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

傳送和接收郵件的人員與資源是任何郵件和協同作業系統的核心。在 Exchange 組織中，這些人員和資源稱之為*收件者*。收件者是指在 Active Directory 中，Microsoft Exchange 可以傳遞或路由郵件到該位置之任何擁有郵件功能的物件。

## Exchange 收件者類型

Exchange 包括數種明確的收件者類型。Exchange Administration Center (EAC) 可識別各個收件者類型且在 Exchange 管理命令介面中的 *RecipientTypeDetails* 內容擁有獨特值。使用明確收件者類型有下列好處：

  - 您一眼就能區分各種收件者類型。

  - 您可以依照每位收件者類型來進行搜尋和排序。

  - 您可以更容易執行特定收件者類型的大量管理作業。

  - 您可以更容易檢視收件者內容，因為 EAC 使用收件者類型來呈現不同的內容頁面。例如，會顯示會議室信箱的資源容量，但不會顯示使用者信箱的資源容量。

下表列出可用的收件者類型。本主題稍後會更詳細討論這些收件者類型。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>收件者類型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>動態通訊群組</p></td>
<td><p>使用收件者篩選器和條件，在傳送郵件的同時取得成員資格的通訊群組。</p></td>
</tr>
<tr class="even">
<td><p>設備信箱</p></td>
<td><p>指派給像是可攜式電腦投影機、麥克風或公務車等非地點特有資源的資源信箱。設備信箱可以納入成為會議邀請中的資源，進而提供簡單而有效率的方式讓使用者善用資源。</p></td>
</tr>
<tr class="odd">
<td><p>連結的信箱</p></td>
<td><p>指派給個別信任樹系中某個使用者的信箱。</p></td>
</tr>
<tr class="even">
<td><p>郵件連絡人</p></td>
<td><p>擁有郵件功能的 Active Directory 連絡人，其中包含存在於 Exchange 組織外之人員或組織的相關資訊。每個郵件連絡人都有外部的電子郵件地址。傳送給郵件連絡人的所有郵件都會路由傳送至這個外部電子郵件地址。</p></td>
</tr>
<tr class="odd">
<td><p>郵件樹系連絡人</p></td>
<td><p>代表來自另一個樹系之收件者物件的郵件連絡人。郵件樹系連絡人通常是由 Microsoft Identity Integration Server (MIIS) 同步處理建立。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>郵件樹系連絡人是唯讀的收件者物件，只會透過 MIIS 或類似的自訂同步處理更新。您無法使用 EAC 或命令介面來移除或修改郵件樹系連絡人。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>郵件使用者</p></td>
<td><p>擁有郵件功能的 Active Directory 使用者，代表 Exchange 組織之外的使用者。每個郵件使用者都有外部的電子郵件地址。傳送給郵件使用者的所有郵件都會路由傳送至這個外部電子郵件地址。</p>
<p>郵件使用者與郵件連絡人類似，只不過郵件使用者具有 Active Directory 登入認證並可存取資源。</p></td>
</tr>
<tr class="odd">
<td><p>擁有郵件功能的非萬用群組</p></td>
<td><p>擁有郵件功能的 Active Directory 全域或本機群組物件。擁有郵件功能的非萬用群組在 Exchange Server 2007 中已終止，只有當它們從 Exchange 2003 或舊版的 Exchange 移轉後才會存在。您無法使用 Exchange Server 2013 建立非萬用通訊群組。</p></td>
</tr>
<tr class="even">
<td><p>擁有郵件功能的公用資料夾</p></td>
<td><p>設定來接收郵件的 Exchange 公用資料夾。</p></td>
</tr>
<tr class="odd">
<td><p>通訊群組</p></td>
<td><p>通訊群組是一個擁有郵件功能的 Active Directory 通訊群組物件，只能用來將郵件發佈給收件者群組。</p></td>
</tr>
<tr class="even">
<td><p>擁有郵件功能的安全性群組</p></td>
<td><p>通訊群組是一個擁有郵件功能的 Active Directory 安全性群組物件，可以用來將存取權限指派給 Active Directory 中的資源，也可以用於發佈郵件。</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 收件者</p></td>
<td><p>特殊收件者物件，提供一致且已知的郵件寄件者，可以區別系統產生的郵件和其他郵件。它會取代舊版 Exchange 中用於系統產生郵件的「系統管理員」寄件者。</p></td>
</tr>
<tr class="even">
<td><p>會議室信箱</p></td>
<td><p>指派給像是會議室、視聽室或訓練室等會議地點的資源信箱。會議室信箱可以納入成為會議邀請中的資源，進而提供簡單而有效率的方式來為使用者組織會議。</p></td>
</tr>
<tr class="odd">
<td><p>共用信箱</p></td>
<td><p>主要不是與單一使用者關聯，而且通常會設定為允許多個使用者存取的信箱。</p></td>
</tr>
<tr class="even">
<td><p>網站信箱</p></td>
<td><p>信箱是由儲存郵件的 Exchange 以及儲存文件的 SharePoint 站台組成。使用者可利用同一個用戶端介面存取電子郵件與文件。如需相關資訊，請參閱<a href="site-mailboxes-exchange-2013-help.md">網站信箱</a>。</p></td>
</tr>
<tr class="odd">
<td><p>使用者信箱</p></td>
<td><p>指派給 Exchange 組織中某個別使用者的信箱。該信箱通常包含郵件、行事曆項目、連絡人、工作、文件及其他重要商務資料。</p></td>
</tr>
<tr class="even">
<td><p>Office 365 信箱</p></td>
<td><p>在混合式部署中，郵件使用者的 Office 365 信箱將存在於 Active Directory 內部部署，而關聯的雲端信箱則存在於 Exchange Online 中。</p></td>
</tr>
<tr class="odd">
<td><p>連結的使用者</p></td>
<td><p>連結的使用者信箱位於不同樹系，而不是位於使用者所在樹系中。</p></td>
</tr>
</tbody>
</table>


## 信箱

信箱是 Exchange 組織中資訊工作者最常使用的收件者類型。每個信箱都與 Active Directory 使用者帳戶關聯。使用者可以使用信箱來傳送和接收郵件，以及儲存郵件、約會、工作、記事和文件。信箱是您 Exchange 組織中使用者主要的郵件處理和協同作業工具。

## 信箱元件

每個信箱是由 Active Directory 使用者以及儲存在 Exchange 信箱資料庫的信箱資料所組成 (如下圖所示)。信箱的所有組態資料會儲存在 Active Directory 使用者物件的 Exchange 屬性中。信箱資料庫包含位於與使用者帳戶關聯之信箱中的實際資料。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建立新使用者或現有使用者的信箱時，信箱所需的 Exchange 屬性會新增至 Active Directory 中的使用者物件。要等到信箱接收郵件或使用者登入信箱之後，才會建立關聯的信箱資料。</td>
</tr>
</tbody>
</table>


**信箱元件**

![組成信箱的組件](images/Bb201680.5fcb5e6d-656e-42ae-871f-0eef8aea456b(EXCHG.150).gif "組成信箱的組件")

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果移除信箱，則儲存在 Exchange 信箱資料庫中的信箱資料會標示為要刪除，並且也會從 Active Directory 刪除關聯的使用者帳戶。若要保留使用者帳戶而只刪除信箱資料，您必須停用信箱。</td>
</tr>
</tbody>
</table>


## 信箱類型

Exchange 支援下列信箱類型：

  - **使用者信箱**   使用者信箱會指派給 Exchange 組織中的個別使用者。使用者信箱提供使用者多功能的協同作業平台。使用者可以傳送和接收郵件、管理他們的連絡人、安排會議以及維護工作清單。也可以將語音信箱訊息傳遞至他們的信箱。使用者信箱是最常用的信箱類型，而且通常是指派給組織中使用者的信箱類型。

  - **連結的信箱**   連結的信箱是由個別信任樹系中的使用者存取的信箱。對於在資源樹系中部署 Exchange 的組織，可能需要連結的信箱。資源樹系案例讓組織能夠在單一樹系中集中管理 Exchange，同時又允許使用一或多個信任樹系中的使用者帳戶來存取 Exchange 組織。
    
    如前所述，每個信箱都必須有關聯的使用者帳戶。不過，存取連結信箱的使用者帳戶，並不存在於已部署 Exchange 的樹系中。因此，存在於與 Exchange 相同樹系中的已停用使用者帳戶，會與每個連結信箱關聯。下圖說明將用於存取連結信箱的連結使用者帳戶與 Exchange 資源樹系中與連結信箱關聯的已停用使用者帳戶之間的關係。
    
    **連結的信箱**
    
    ![具有資源樹系的複雜 Exchange 組織](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "具有資源樹系的複雜 Exchange 組織")  

  - **Office 365 信箱**當您建立混合部署的 Exchange Online Office 365 信箱，郵件使用者將會建立於 Active Directory 內部部署。目錄同步作業 (如果有設定) 會自動將這個新使用者物件同步處理到 Office 365，再將之轉換為 Exchange Online 雲端信箱。您可將 Office 365 信箱建立為一般使用者信箱、會議室與設備資源信箱以及共用信箱。

  - **共用信箱** 共用信箱主要不是與個別使用者關聯，而且通常設定為允許多個使用者存取。
    
    雖然有可能將任何信箱類型的登入權限指派給其他使用者，但是共用信箱專用於這個功能。與共用信箱關聯的 Active Directory 使用者必須是停用的帳戶。建立共用信箱之後，您必須將權限指派給需要存取共用信箱的使用者。

  - **資源信箱**   資源信箱是專門設計用於排程資源的特殊信箱。和所有信箱類型一樣，資源信箱也有關聯的 Active Directory 使用者帳戶，但必須是停用的帳戶。下列是資源信箱的類型：
    
      - **會議室信箱**　這些信箱指派至會議位置，例如會議室、禮堂和訓練實驗室。
    
      - **設備信箱**   這些信箱是指派給非地點特有資源 (例如可攜式電腦投影機、麥克風或公務車) 的資源信箱。
    
    您可以將這兩種資源信箱納入會議邀請中，為使用者提供一種簡單有效的方法來使用資源。您可以根據資源擁有者所定義的資源預約原則來設定資源信箱自動處理傳入的會議邀請。例如，您可以設定會議室自動接受除了週期性會議以外的傳入會議邀請，而資源擁有者可決定是否核准該邀請。

## 系統信箱

在安裝期間，Exchange 會於 Active Directory 樹系的根網域建立系統信箱。使用者或系統管理員無法登入這些信箱。系統信箱是為整合郵件 (UM)、遷移、郵件核准以及就地保留 eDiscovery 等特色所建立的。下表會列出 Active Directory 中顯示的系統信箱相關資訊。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>信箱</th>
<th>名稱</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織</p></td>
<td><p>SystemMailbox {bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
</tr>
<tr class="even">
<td><p>訊息核准</p></td>
<td><p>SystemMailbox {1f05a927-<em>xxxx</em>- <em>xxxx</em> - <em>xxxx</em> -<em>xxxxxxxxxxxx</em>}</p>
<p><em>x</em> 為隨機指派且每個 Exchange 樹系皆有獨特號碼</p></td>
</tr>
<tr class="odd">
<td><p>UM 資料存儲</p></td>
<td><p>SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}</p></td>
</tr>
<tr class="even">
<td><p>探索</p></td>
<td><p>DiscoverySearchMailbox {D919BA05-46A6-415f-80AD-7E09334BB852}</p></td>
</tr>
<tr class="odd">
<td><p>同盟電子郵件</p></td>
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
</tr>
<tr class="even">
<td><p>遷移</p></td>
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
</tr>
</tbody>
</table>


如果您要解除 Exchange 委任組織中最後一個 Mailbox Server，則應該使用 [Disable-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997210\(v=exchg.150\)) 指令程式，先停用這些系統信箱。解除委任包含這些系統信箱的信箱伺服器時，應該將這些信箱移到其他信箱伺服器，以確保您不會喪失任何功能。

## 規劃信箱

信箱是建立於已安裝 Mailbox server role 之 Exchange 伺服器上的信箱資料庫中。為了協助提供可靠有效的平台給信箱使用者，詳細規劃信箱伺服器和資料庫是必要的。如要深入了解信箱伺服器與資料庫規劃，請參閱[規劃及部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)。

## 通訊群組

通訊群組是擁有郵件功能的 Active Directory 群組物件，主要用於將郵件發佈給多位收件者。任何收件者類型都可以是通訊群組的成員。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>請注意 Active Directory 和 Exchange 之間的術語差異。在 Active Directory 中，通訊群組是指任何沒有安全性內容的群組 (無論是否擁有郵件功能)。在 Exchange 中，所有擁有郵件功能的群組指的是通訊群組 (不論是否具有安全性內容)。</td>
</tr>
</tbody>
</table>


Exchange 支援下列類型的通訊群組：

  - **通訊群組**   這些是擁有郵件功能的 Active Directory 萬用通訊群組物件。只能用來將郵件發佈給收件者群組。

  - **郵件安全性群組**   這些是擁有郵件功能的 Active Directory 萬用安全性群組物件。可以用來將存取權限指派給 Active Directory 中的資源，也可用於發佈郵件。

  - **擁有郵件功能的非萬用群組**   這些是擁有郵件功能的 Active Directory 全域或本機群組物件。可以只建立萬用通訊群組或啟用萬用通訊群組的郵件功能。您可能會有從舊版 Exchange 遷移之擁有郵件功能的群組，但這些群組不是萬用群組。使用 EAC 或命令介面仍然可以管理這些群組。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要將網域本機或全域群組轉換至萬用群組，您可以使用命令介面中的 <a href="https://technet.microsoft.com/zh-tw/library/bb123770(v=exchg.150)">Set-Group</a> 指令程式。</td>
    </tr>
    </tbody>
    </table>


## 動態通訊群組

動態通訊群組係依據特定收件者篩選器決定成員資格的通訊群組，而不是一組已定義的收件者。

和一般通訊群組不同，每次郵件傳送給動態通訊群組時，會根據您指定的篩選器和條件來計算該群組的成員清單。將郵件傳到動態通訊群組時，會將該郵件傳給與針對動態通訊群組所定義的準則相符之組織的所有收件者。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在傳送郵件時，動態通訊群組會納入 Active Directory 中有符合該群組篩選器之屬性的收件者。如果修改收件者的內容來符合此群組的篩選器，則該收件者會意外地成為群組成員並開始接收傳送至動態通訊群組的郵件。嚴謹、一致的帳戶供應程序可減少發生這種問題的機會。</td>
</tr>
</tbody>
</table>


為了協助您建立動態通訊群組的收件者篩選器，您可以使用預先定義的篩選器。*預先定義篩選器*是常用的篩選器，可用於比對各種收檢者篩選準則。您可以使用這些篩選器來指定要併入動態通訊群組中的收件者類型。此外，也可以指定收件者必須符合的條件清單。您可以根據下列內容來建立預先定義的條件：

  - 自訂屬性 1–15

  - State 或 province

  - Company

  - Department

  - 收件者容器

您也可以根據收件者內容而非先前所列的內容來指定條件。若要這樣做，您必須使用命令介面建立動態通訊群組的自訂查詢。請記得，具有自訂收件者篩選之動態通訊群組的篩選和條件設定，只能使用命令介面來管理。如需如何使用自訂查詢建立動態通訊群組的範例，請參閱[管理動態通訊群組](manage-dynamic-distribution-groups-exchange-2013-help.md)。

## 郵件連絡人

郵件連絡人通常包含存在於 Exchange 組織外的人員或組織相關資訊。郵件連絡人可以出現在組織共用通訊錄 (亦稱作全域通訊清單或 GAL) 和其他通訊清單中，也可以當作成員加入通訊群組中。每個連絡人都有外部電子郵件地址，而且傳送給連絡人的所有電子郵件都會自動轉寄至該地址。這種連絡人很適合代表 Exchange 組織外不需要存取內部資源的人員。郵件連絡人類型如下：

  - **郵件連絡人**   這些是擁有郵件功能的 Active Directory 連絡人，這些連絡人包含存在於 Exchange 組織之外的人員或組織相關資訊。

  - **郵件樹系連絡人**   這些代表來自另一個樹系的收件者物件。這些連絡人通常是由目錄同步作業建立。郵件樹系連絡人是唯讀收件者物件，只能利用同步處理更新或移除。您不能使用 Exchange 管理介面修改或移除郵件樹系連絡人。

## 郵件使用者

郵件使用者類似於郵件連絡人。這兩者都擁有外部電子郵件地址，也都包含 Exchange 組織外的人員相關資訊，而且兩者都可以顯示在共用通訊錄和其他通訊清單中。不過，和郵件連絡人不同的是，郵件使用者具有 Active Directory 登入認證，而且可以存取已指派權限的資源。

如果組織外的人員需要存取您網路上的資源，則您應該建立郵件使用者而非郵件連絡人。例如，您可以為需要存取您的伺服器基礎結構，但是會使用自己的外部地址的短期顧問建立郵件使用者。

另一個案例是在組織中為您不想維護其 Exchange 信箱的人員建立郵件使用者。例如，在併購之後，被併購的公司可以維持其不同的郵件基礎結構，但也可能需要存取您網路上的資源。對那些使用者而言，您可能需要建立郵件使用者而非信箱使用者。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 EAC 中，使用 [收件者組態] [連絡人] &gt; 頁面來建立並管理郵件使用者。郵件使用者沒有個別的頁面。</td>
</tr>
</tbody>
</table>


## 擁有郵件功能的公用資料夾

公用資料夾專門當做許多使用者共用之資訊的存放庫。啟用公用資料夾的郵件功能可提供其他等級的功能給使用者。除了能夠將郵件張貼到資料夾，使用者還可傳送電子郵件至公用資料夾，且有時候還可從公用資料夾接收電子郵件。每個擁有郵件功能的資料夾在 Active Directory 中都有一個物件，用來儲存其電子郵件地址、通訊錄名稱和其他郵件相關的屬性。

您可以使用 EAC 或命令介面管理公用資料夾。如需管理公用資料夾的相關資訊，請參閱[公用資料夾](public-folders-exchange-2013-help.md)。

## Microsoft Exchange 收件者

Microsoft Exchange 收件者是特殊收件者物件，可提供一致且已知的郵件寄件者，可以區別系統產生的郵件和其他郵件。它會取代舊版 Exchange 中用於系統產生郵件的「系統管理員」寄件者。

Microsoft Exchange 收件者不是一般的收件者物件 (例如信箱、郵件使用者或郵件連絡人)，而且不是使用一般收件者工具來管理。然而，您可以使用命令介面中的 [Set-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997443\(v=exchg.150\)) 指令程式來設定 Microsoft Exchange 收件者。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>系統產生的郵件傳送至外部寄件者時，不會使用 Microsoft Exchange 收件者作為郵件的寄件者，而是使用 <a href="https://technet.microsoft.com/zh-tw/library/bb124151(v=exchg.150)">Set-TransportConfig</a> 指令程式中的 <em>ExternalPostmasterAddress</em> 參數所指定的電子郵件地址。</td>
</tr>
</tbody>
</table>


## 收件者文件

下列表格包含可協助您了解並管理 Exchange 收件者的主題連結。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主題</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">建立使用者信箱</a></p></td>
<td><p>了解如何使用 Exchange 系統管理中心或 Exchange 管理命令介面建立使用者信箱。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-user-mailboxes-exchange-2013-help.md">管理使用者信箱</a></p></td>
<td><p>了解如何建立使用者信箱、變更信箱內容以及大量編輯多個信箱選取的內容。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-linked-mailboxes-exchange-2013-help.md">管理連結的信箱</a></p></td>
<td><p>了解連結信箱的要求、如何建立並將它們連結到主要帳戶，及變更連結信箱的內容。</p></td>
</tr>
<tr class="even">
<td><p><a href="create-and-manage-distribution-groups-exchange-2013-help.md">建立並管理通訊群組</a></p></td>
<td><p>了解如何建立並管理通訊群組，以及建利組織的群組命名原則。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mail-enabled-security-groups-exchange-2013-help.md">管理擁有郵件功能的安全性群組</a></p></td>
<td><p>了解如何建立並管理擁有郵件功能的安全性群組。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-dynamic-distribution-groups-exchange-2013-help.md">管理動態通訊群組</a></p></td>
<td><p>了解如何建立動態通訊群組並管理動態通訊群組內容，例如使用自訂屬性及其他判定成員資格的內容。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mail-contacts-exchange-2013-help.md">管理郵件連絡人</a></p></td>
<td><p>了解如何建立並管理郵件連絡人。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-mail-users-exchange-2013-help.md">管理郵件使用者</a></p></td>
<td><p>了解如何建立並管理郵件使用者。</p></td>
</tr>
<tr class="odd">
<td><p><a href="create-and-manage-room-mailboxes-exchange-2013-help.md">建立及管理會議室信箱</a></p></td>
<td><p>了解如何建立會議室信箱並管理會議室信箱內容，例如啟用週期性會議以及設定預約與排程選項。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-equipment-mailboxes-exchange-2013-help.md">管理設備信箱</a></p></td>
<td><p>了解如何建立設備信箱、設定預約與排程選項，以及管理其他信箱內容。</p></td>
</tr>
<tr class="odd">
<td><p><a href="disconnected-mailboxes-exchange-2013-help.md">中斷連線的信箱</a></p></td>
<td><p>了解兩種類型的中斷連線信箱和如何操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="custom-attributes-exchange-2013-help.md">自訂屬性</a></p></td>
<td><p>了解如何使用自訂屬性新增收件者的相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/bb124268(v=exchg.150)">在 [收件者的命令介面命令的篩選器</a></p></td>
<td><p>了解如何搭配使用預先定義或自訂的篩選和命令來篩選一組收件者。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-permissions-for-recipients-exchange-online-help.md">管理收件者的權限</a></p></td>
<td><p>了解如何使用 EAC 或命令介面將權限指派給使用者和群組。</p></td>
</tr>
<tr class="odd">
<td><p><a href="automatic-mailbox-distribution-exchange-2013-help.md">自動信箱發佈</a></p></td>
<td><p>了解自動信箱發佈如何運作，以及如何控制針對新信箱和移動後信箱選取的信箱資料庫。</p></td>
</tr>
</tbody>
</table>


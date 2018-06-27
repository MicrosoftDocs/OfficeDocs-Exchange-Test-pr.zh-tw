---
title: '如何及何時在混合式部署中解除委任您的內部部署 Exchange 伺服器: Exchange 2013 Help'
TOCTitle: 如何及何時在混合式部署中解除委任您的內部部署 Exchange 伺服器
ms:assetid: 4f884b7a-3b8a-4207-8843-65d3141731dc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn931280(v=EXCHG.150)
ms:contentKeyID: 65048793
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 如何及何時在混合式部署中解除委任您的內部部署 Exchange 伺服器

 


_**適用版本：** Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：** 2017-07-27_

如果您已經準備好從 Exchange 混合式部署移轉到完整雲端實作，請閱讀本文章。

其中一個易於Exchange Online存取公司的更多吸引人選項是使用[Exchange 混合式部署與移轉至 Office 365](https://msdn.microsoft.com/en-us/library/ff633682\(v=exchsrvcs.149\).aspx)所述的混合式部署方法。這是唯一的選擇，可讓您輕鬆主機板和關閉委員會 （所有原生的選項是主機板僅） 的信箱。除了能夠關閉委員會、 混合設定具有下列機碼選項。

本主題將協助您了解在解除委任 Exchange 混合式的選項和應該實作時每個這些選項。何時以及如何解除委任 Exchange 混合伺服器中有許多變異數。花費的時間來了解含意並適當地規劃 \[完整或部分解除委任內部部署伺服器的很重要。

  - **跨部署可用性**。這可讓您查看使用者的空閒/忙碌資訊並同時排程會議，而不需顧及其信箱部署。

  - **跨部署封存**。這可讓客戶只將一位使用者的封存信箱移至雲端。這通常是客戶嘗試 Office 365 的第一個步驟，並更具體而言，也就是嘗試 Exchange Online。

  - **跨部署探索搜尋**。這可讓客戶執行 e-探索搜尋，進而在兩個部署中耙梳信箱及封存 (您必須設定 OAuth 驗證)。

  - **Outlook Web App URL 重新導向**。這可將使用者重新導向至適當的部署以進行 Outlook Web App 存取。

  - **移動後沒有設定檔重新建立**。和其他移轉選項不同，信箱 GUID 不會變更。這表示您不需要重新建立您的設定檔或在信箱移動後重新下載 OST。

根據您的組織需求，混合式部署會是提供最順暢的使用者與共存體驗的最佳選項。

## 移轉至 Exchange Online 的其他方法

混合部署不是可供任何人;事實上還有通常較佳的選項。有許多租用戶的已選擇要部署的混合式設定是 \[了大約 50 個基座。時的混合部署優點的清單可能會發出嗶吸引人，它隨附針對複雜性所沈價格。較小的租用戶的一些需要功能的混合部署中，但對於大部分的承租人來說是說過使用任一轉換，更好的經驗分段，\] 或 \[IMAP 移轉選項。沒有呼叫的 FastTrack 您可以使用決定的移轉方法時所採取的程式。 在[Office 365 FastTrack 頁面](https://go.microsoft.com/fwlink/?linkid=846696)說明 FastTrack 資訊。

使用下表來決定的移轉類型適用於您的組織。（如需詳細資訊，請參閱[移轉至 Office 365 的多個電子郵件帳戶的方式](https://support.office.com/en-us/article/ways-to-migrate-multiple-email-accounts-to-office-365-0a4913fe-60fb-498f-9155-a86516418842?ui=en-us%26rs=en-sg%26ad=sg)、）


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>現有的組織</th>
<th>要移轉的信箱數目</th>
<th>是否要在內部部署組織中管理使用者帳戶？</th>
<th>移轉類型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013、Exchange 2010、Exchange 2007 或 Exchange 2003</p></td>
<td><p>少於 2,000 個信箱</p></td>
<td><p>否</p></td>
<td><p>完全 Exchange 移轉</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 或 Exchange 2003</p></td>
<td><p>少於 2,000 個信箱</p></td>
<td><p>否</p></td>
<td><p>分段 Exchange 移轉</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2007 或 Exchange 2003</p></td>
<td><p>超過 2000 個信箱*</p></td>
<td><p>是</p></td>
<td><p>Exchange 混合式部署中的分段 Exchange 移轉或遠端移動移轉</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 或 Exchange 2010</p></td>
<td><p>超過 2000 個信箱*</p></td>
<td><p>是</p></td>
<td><p>Exchange 混合式部署中的遠端移動移轉</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2000 Server 或更早版本</p></td>
<td><p>沒有上限</p></td>
<td><p>是</p></td>
<td><p>IMAP 移轉</p></td>
</tr>
<tr class="even">
<td><p>非 Exchange 內部部署郵件系統</p></td>
<td><p>沒有上限</p></td>
<td><p>是</p></td>
<td><p>IMAP 移轉</p></td>
</tr>
</tbody>
</table>


\*具有少於 2000 個信箱有些組織可能獲益特性與僅可用的混合部署的功能。請務必謹慎考慮使用介紹的複雜性混合式部署的優點。我們強烈建議使用少於 2000 個信箱的客戶考量轉換或分段移轉再繼續進行混合部署。

## 為什麼您可能不想從內部部署解除委任 Exchange 伺服器

擁有混合式組態的客戶通常會在一段時間之後發現他們所有的信箱已移至 Exchange Online。在這個時候，他們可能會決定從內部部署移除 Exchange 伺服器。然而，他們會發現他們不能再管理他們的雲端信箱。

為租用戶啟用目錄同步作業並從內部部署將使用者同步處理時，大部分的屬性都無法從 Exchange Online 管理，必須從內部部署管理。這不是因為混合式組態，而是因為目錄同步作業而發生。此外，即使您已具備目錄同步作業卻未執行混合式組態精靈，您仍然無法從雲端管理大部分的收件者工作。如需詳細資訊，請參閱 [TechNet 部落格](http://blogs.technet.com/b/exchange/archive/2012/12/05/decommissioning-your-exchange-2010-servers-in-a-hybrid-deployment.aspx)。

## 可以使用協力廠商管理工具嗎？

是否可以使用協力廠商管理工具或 ADSIEDIT 是常見的。答案是，您可以使用它們，但是它們不受支援。Exchange 管理主控台、Exchange 系統管理中心 (EAC) 和 Exchange 管理命令介面是唯一支援的工具，可用來管理 Exchange 收件者和物件。如果您決定要使用協力廠商管理工具，就要自行承擔風險。協力廠商管理工具通常會正常運作，但是 Microsoft 並不會驗證這些工具。

## 常見案例

要從混合式組態移至雲端並不簡單。進入混合式組態的程序是我們花費了很多時間才得以正確執行的程序。遇到問題時，我們覺得我們表現優異，使得邁向混合這個幾乎不可能的工作，成為相當容易的精靈式程序。

然而，我們唯一尚未做到的，就是讓您從混合組態移至雲端。根據您的即時目標，這個程序可透過一些指引變得相當簡單。以下是三個常見的混合案例，以及如何適當地達成客戶最終目標的建議。

由於混合客戶的基底是非常不同，要嘗試將全部的客戶套用「共同」的案例並不容易。我們嘗試提供以下的一些內部部署 Exchange Server 解除委任的高階案例，讓您徹底了解這些案例並形成解除委任的計劃，您必須決定最適合您需求的案例。

## 案例一

**問題：** 「 我的組織具有已執行混合組態中而且我有全部我Exchange Online中的信箱。我不需要從內部部署的管理我的使用者且不再需要目錄同步處理或密碼同步處理。

**解決方案：** 因為所有的使用者將在 Office 365 中受管理，且沒有額外的目錄同步作業需求，所以您可以安心地停用目錄同步作業並從內部部署環境移除 Exchange。

![從內部部署環境中移除 Exchange](images/Dn931280.f9c2a2cb-4c16-4ca3-8244-b89c1cdf0744(EXCHG.150).jpg "從內部部署環境中移除 Exchange") 停用目錄同步作業和解除安裝 Exchange 混合

1.  執行`Get-OrganizationConfig |fl PublicFoldersEnabled`並確定不設為 \[遠端。如果它設為遠端，並將公用資料夾是您想要繼續進行存取的某個項目，您必須將它們遷移到Exchange Online。如需詳細資訊，請參閱[使用批次移轉至 Office 365 和 Exchange Online 移轉舊版公用資料夾](https://technet.microsoft.com/zh-tw/library/dn874017\(v=exchg.150\))。

2.  假設您已經將所有信箱移至 Exchange Online，您可以將 MX 和自動探索 DNS 記錄指向 Exchange Online，而不是指向內部部署。如需詳細資訊，請參閱 [參照：Office 365 的外部網域名稱系統記錄](http://technet.microsoft.com/zh-tw/library/hh852557.aspx)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請務必更新內部和外部 DNS，否則您可能會有不一致的用戶端連線行為。</td>
    </tr>
    </tbody>
    </table>


3.  接下來，您應該移除 Exchange 伺服器上的服務連線點 (SCP) 值。這可確保不會傳回 SCP，且用戶端會改為使用自動探索的 DNS 方法。範例如下所示：
    
        Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您有環境中的 Exchange 2007 伺服器，您必須在 Exchange 2007 伺服器上執行類似的命令，以清除設定。</td>
    </tr>
    </tbody>
    </table>


4.  有必須刪除的輸入和輸出連接器，這些連接器是由混合式組態精靈所建立。使用下列步驟來執行這項操作：
    
    1.  登入 [Office 365 管理入口網站](http://portal.office.com) 並以租用戶系統管理員身分登入。
    
    2.  選取選項來管理 **Exchange**。
    
    3.  導覽至 **郵件流程** -\> **連線**。
    
    4.  您現在可以停用或刪除輸入和輸出連接器。HCW 會建立具有唯一命名空間 **輸入自 \<唯一識別項\>** 和**輸出自 \<唯一識別項\>** 的連接器，如下圖所示。
        
        ![混合式組態精靈會建立具有唯一命名空間的連接器](images/Dn931280.7b1b6f0b-43d6-4407-8cd7-7dd52e016697(EXCHG.150).jpg "混合式組態精靈會建立具有唯一命名空間的連接器")  

5.  移除混合式組態精靈所建立的組織關係。使用下列步驟來執行這項操作：
    
    1.  登入 [Office 365 管理入口網站](http://portal.office.com) 並以租用戶系統管理員身分登入。
    
    2.  選取選項來管理 Exchange。
    
    3.  導覽至 \[**組織**\]。
    
    4.  在**組織共用**下，移除名為 **O365 到內部部署 – \<唯一識別項\>** 的組織，如下圖所示。
        
        ![移除混合式組態精靈所建立的組織關係。](images/Dn931280.2f0c1077-8785-487a-87a5-a75f0a4f0fea(EXCHG.150).jpg "移除混合式組態精靈所建立的組織關係。")  

6.  如果已經為 Exchange 混合式部署設定了 OAuth，則您必須要從內部部署和 Office 365 兩方來停用此組態。在大部分的環境中，這些步驟都可以略過，因為我們的客戶中只有一小部分已設定 OAuth。
    
    停用內部部署組態：
    
    1.  從 Exchange 2013 伺服器，開啟 Exchange 管理命令介面。
    
    2.  執行下列命令：
        
            Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
    
    停用 Exchange Online 組態：
    
    1.  將 Windows PowerShell 連線到 Exchange Online。
    
    2.  執行下列命令：
        
            Run Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        
        *Identity* 參數會假設您使用混合式組態精靈設定 OAuth。如果不是這樣，您可能需要調整您為連線器的身分識別所指定的值。

7.  停用租用戶的目錄同步作業。完成此步驟時，所有的使用者管理工作都會從 Office 365 管理工具完成。這表示您將不再使用 Exchange 管理主控台或 Exchange 系統管理中心 (EAC)。如需有關如何停用目錄同步作業的詳細資訊，請參閱[停用目錄同步作業](https://technet.microsoft.com/zh-tw/library/dn144760.aspx)。

8.  您可以現在安全地從內部部署解除安裝 Exchange。

## 案例二

**問題：** 我的組織已經在混合式組態中執行了大約一年，而且終於將我最後的信箱移至雲端。我規劃要保留 Active Directory 同盟服務 (AD FS) 來進行 Exchange Online 信箱的使用者驗證。(這個案例可套用到任何規劃保留目錄同步作業的客戶)。

**解決方案：** 由於客戶規劃保留 AD FS，所以他們也必須保留目錄同步作業，因為它是必要條件。因此，他們無法從內部部署環境完全移除 Exchange 伺服器。不過，他們可以解除委任大部分的 Exchange 伺服器，但仍需保留數個伺服器進行使用者管理。請記住，保留執行的伺服器可以在虛擬機器上執行，因為工作負載已幾乎完全移至 Exchange Online。

下圖描述您想要的最終狀態：

![解除委任具有某些剩餘項的 Exchange Server](images/Dn931280.d7734579-6999-45b2-9a0f-a23f18353a49(EXCHG.150).jpg "解除委任具有某些剩餘項的 Exchange Server")

下圖描述實際的最終狀態：

![解除委任 Exchange Server 之前的狀態](images/Dn931280.c692f0af-6536-4bc9-950d-58a1e486525f(EXCHG.150).jpg "解除委任 Exchange Server 之前的狀態") 保留 AD FS 與目錄同步作業和解除委任大部分的 Exchange 伺服器

1.  執行 `Get-OrganizationConfig |fl PublicFoldersEnabled` 並確保未將其設為遠端。如果將其設為遠端，而您想要繼續存取公用資料夾，您就必須將公用資料夾移轉到 Exchange Online。有關如何執行這項操作，請參閱 [使用批次移轉至 Office 365 和 Exchange Online 移轉舊版公用資料夾](https://technet.microsoft.com/zh-tw/library/dn874017\(v=exchg.150\))。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果將公用資料夾移轉至 Exchange Online 不是選項之一，而且您的使用者仍然需要它們，您不應該繼續進行。</td>
    </tr>
    </tbody>
    </table>


2.  在您將所有信箱移至 Exchange Online 後，您為了解除委任大部分的 Exchange 伺服器而想要做的第一件事是將 MX 和自動探索 DNS 記錄指向 Exchange Online 而不是指向內部部署。如需詳細資訊，請參閱 [參照：Office 365 的外部網域名稱系統記錄](http://technet.microsoft.com/zh-tw/library/hh852557.aspx)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請務必更新內部和外部 DNS，否則您可能會有不一致的用戶端連線和郵件流程行為。</td>
    </tr>
    </tbody>
    </table>


3.  接下來，您應該移除 Exchange 伺服器上的服務連線點 (SCP) 值。這可確保不會傳回 SCP，且用戶端會改為使用自動探索的 DNS 方法。範例如下所示：
    
        Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您有環境中的 Exchange 2007 伺服器，您必須在 Exchange 2007 伺服器上執行類似的命令，以清除設定</td>
    </tr>
    </tbody>
    </table>


4.  若要避免以後重新建立混合式組態物件，您應該從 Active Directory 移除混合式組態物件。若要這麼做，請開啟 Exchange 管理命令介面並執行下列作業：
    
        Remove-HybridConfiguration

5.  移除所有 Exchange 伺服器，但保留您要用來管理和建立使用者的伺服器。雖然兩部伺服器應該已足夠供使用者管理工作使用，但您也可能只需要一部伺服器即可完成。此外，也不需要擁有資料庫可用性群組或任何其他高可用性選項。

6.  如果已經為 Exchange 混合式部署設定了 OAuth，則您必須要從內部部署和 Office 365 兩方來停用此組態。在大部分的環境中，這些步驟都可以略過，因為我們的客戶中只有一小部分已設定 OAuth。
    
    停用內部部署組態：
    
    1.  從 Exchange 2013 伺服器，開啟 Exchange 管理命令介面。
    
    2.  執行下列命令：
        
            Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
    
    停用 Exchange Online 組態：
    
    1.  將 Windows PowerShell 連線到 Exchange Online。
    
    2.  執行下列命令：
        
            Run Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        
        身分識別參數會假設您使用混合式組態精靈設定 OAuth。如果不是這樣，您可能需要調整您為連線器的身分識別所指定的值。

7.  有必須刪除的輸入和輸出連接器，這些連接器是由混合式組態精靈所建立。使用下列步驟來執行這項操作：
    
    1.  登入 [Office 365 管理入口網站](http://portal.office.com) 並以租用戶系統管理員身分登入。
    
    2.  選取選項管理 **Exchange**。
    
    3.  導覽至 **\[郵件流程\]** -\> **\[連接器\]**。
    
    4.  您現在可以停用或刪除輸入和輸出連接器。HCW 會建立具有唯一命名空間 **輸入自 \<唯一識別項\>** 和**輸出自 \<唯一識別項\>** 的連接器，如下圖所示。
        
        ![混合式組態精靈會建立具有唯一命名空間的連接器](images/Dn931280.7b1b6f0b-43d6-4407-8cd7-7dd52e016697(EXCHG.150).jpg "混合式組態精靈會建立具有唯一命名空間的連接器")  

8.  移除混合式組態精靈所建立的組織關係。使用下列步驟來執行這項操作：
    
    1.  登入 [Office 365 管理入口網站](http://portal.office.com) 並以租用戶系統管理員身分登入。
    
    2.  選取選項管理 **Exchange**。
    
    3.  導覽至 \[**組織**\]。
    
    4.  在**組織共用**下，移除名為 **O365 到內部部署 – \<唯一識別項\>** 的組織，如下圖所示。
        
        ![移除混合式組態精靈所建立的組織關係。](images/Dn931280.2f0c1077-8785-487a-87a5-a75f0a4f0fea(EXCHG.150).jpg "移除混合式組態精靈所建立的組織關係。")  

## 案例三

**問題：** 將所有信箱移至 Exchange Online 之後，我想要移除我的 Exchange 伺服器內部部署。然而，我們發現他們正在將 Exchange 用於其他用途，例如用於應用程式的簡易郵件傳送通訊協定 (SMTP) 轉送或用於公用資料夾存取。如果您需要使用內部部署的 Exchange 伺服器來滿足組織目前的需求，最好是不要移除這些內部部署伺服器。

**解決方案：** 建議您不要在此時移除 Exchange 和混合式組態。如果您甚至打算要將自動探索記錄指向 Exchange Online 以開始進行此程序，則您要立即中斷某些功能，例如混合式公用資料夾存取。您可以將 MX 記錄變更為指向 Exchange Online Protection (如果尚未進行這個動作)，甚至可以移除一些內部部署 Exchange 伺服器。然而，您必須保留足夠的伺服器來處理剩餘的混合功能。通常，只會剩下很少量的內部部署伺服器。


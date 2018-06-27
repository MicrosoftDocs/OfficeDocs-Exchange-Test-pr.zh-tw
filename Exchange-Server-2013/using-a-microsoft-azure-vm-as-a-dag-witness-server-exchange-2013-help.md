---
title: '使用 Microsoft Azure 虛擬機器為 DAG 見證伺服器: Exchange 2013 Help'
TOCTitle: 使用 Microsoft Azure 虛擬機器為 DAG 見證伺服器
ms:assetid: 03d1e215-518b-4b48-bfcd-8d187ff8f5ef
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn903504(v=EXCHG.150)
ms:contentKeyID: 63892218
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 Microsoft Azure 虛擬機器為 DAG 見證伺服器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Exchange Server 2013可讓您設定自動資料中心容錯移轉資料庫可用性群組 (DAG) 中的信箱資料庫。此設定需要三個不同的實體位置： 信箱伺服器與第三個放置在 dag 見證伺服器位置的兩個資料中心。現在只有兩個實體位置與組織也可以利用的自動的資料中心容錯移轉使用Microsoft Azure檔案伺服器虛擬機器來做為 DAG 見證伺服器。

本文著重在 DAG 見證 Microsoft Azure 上的位置，並假設您熟悉 site resilience 概念和已跨越之兩個資料中心之正常運作 DAG 基礎結構。如果您沒有已設定在 DAG 基礎結構，建議您先檢閱下列文章：

[高可用性和站台恢復](high-availability-and-site-resilience-exchange-2013-help.md)

[資料庫可用性群組 (DAGs)](database-availability-groups-dags-exchange-2013-help.md)

[規劃高可用性及站台恢復](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)

## Microsoft Azure 的變更

此設定需要多個網站 VPN。一直以來可能貴組織的網路連線到 Microsoft Azure 中使用的網站 VPN 連線。但是，在過去，Azure 支援單一網站 VPN。由於跨三個資料中心來設定 DAG 和其見證需要多個網站 Vpn DAG 見證在 Azure 虛擬機器上的位置） 最初可行。

在年 6 月 2014 Microsoft Azure 導入多個網站 VPN 支援啟用連線至相同的 Azure 虛擬網路的多個資料中心的組織。這項變更也使它具有兩個資料中心的組織可以運用 Microsoft Azure 做為第三個位置以放置其 DAG 見證伺服器。若要深入了解在 Azure 中的多個網站 VPN 功能，請參閱 ＜[設定多個網站 VPN](http://go.microsoft.com/fwlink/?linkid=522621)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此設定會 Azure 虛擬機器與多個網站 VPN 運用部署見證伺服器和不會使用 Azure 雲端見證。</td>
</tr>
</tbody>
</table>


## Microsoft Azure 檔案伺服器見證

下圖是使用 Microsoft Azure 檔案伺服器 VM 為 DAG 見證的概觀。您需要 Azure 虛擬網路，會在資料中心來連接至 Azure 虛擬網路和網域控制站部署在 Azure 虛擬機器上的檔案伺服器的多個網站 VPN。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>它是針對此目的而使用單一的 Azure 虛擬機器和網域控制站上放置檔案見證共用可行。 但是，這會導致不必要的權限提高權限。因此，它不是建議的組態。</td>
</tr>
</tbody>
</table>


**Microsoft Azure 上的 DAG 見證伺服器**

![Azure 上的 Exchange DAG 見證概觀](images/Dn903504.7cbda882-bbae-4be7-b0ea-60947b8aa4ef(EXCHG.150).png "Azure 上的 Exchange DAG 見證概觀")

您需要執行才可使用 Microsoft Azure 虛擬機器的 DAG 見證的第一個項重點是要取得訂閱。請參閱[如何購買 Azure](http://go.microsoft.com/fwlink/?linkid=398989)取得 Azure 訂閱的最佳方法。

在 Azure 訂閱之後，您需要執行順序下列動作：

1.  準備 Microsoft Azure 虛擬網路

2.  設定多個網站 VPN

3.  設定虛擬機器

4.  設定 DAG 見證

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本文中的指導重要部分涉及Microsoft Azure組態。因此，每當適用可以用 Azure 的文件連結。</td>
</tr>
</tbody>
</table>


## 必要條件

  - 雖能夠支援 Exchange 高可用性和站台回復性部署的兩個資料中心。請參閱[規劃高可用性及站台恢復](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)如需詳細資訊

  - 在每一個網站的 VPN 閘道 NAT 後方不是在公用 IP 位址

  - 每個網站，相容於 Microsoft Azure VPN 裝置。請參閱[關於 VPN 裝置的虛擬網路](http://go.microsoft.com/fwlink/?linkid=522619)相容裝置的詳細資訊

  - 非常熟悉 DAG 概念與管理

  - 非常熟悉 Windows PowerShell

## 階段 1： 準備 Microsoft Azure 虛擬網路

設定 Microsoft Azure 網路是之部署程序最重要的一部分。在此階段的結尾，您必須完全運作 Azure 虛擬網路連線至多個網站 VPN 透過在兩個資料中心。

## 註冊 DNS 伺服器

因為此設定需要在內部伺服器和 Azure Vm 之間的名稱解析，您將需要設定 Azure 来使用 DNS 伺服器。 [名稱解析 (DNS)](http://msdn.microsoft.com/en-us/library/azure/jj156088.aspx)主題提供名稱解析 Azure 中的概觀。

執行下列 cmdlet 以註冊您的 DNS 伺服器：

1.  在 Azure 入口網站中，移至**網路**，並再按一下 \[**新增\]**。

2.  按一下 \[**網路服務**\] \>**虛擬網路**\>**註冊 DNS 伺服器**。

3.  輸入的名稱和 IP 位址之 DNS 伺服器。此處指定的名稱為 management portal 中所使用的邏輯名稱且不會以符合您的 DNS 伺服器的實際名稱。

4.  針對想要新增任何其他 DNS 伺服器重複步驟 1 到 3。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>循環配置資源易中不使用您註冊的 DNS 伺服器。Azure 的 Vm 將會使用所列的第一個 DNS 伺服器並無法使用第一個時只會使用任何其他伺服器。</td>
    </tr>
    </tbody>
    </table>


5.  重複步驟 1 至 3 新增您要用於您將 Microsoft Azure 部署網域控制站的 IP 位址。

## 建立本機 （內部） 網路 Azure 中的物件

接下來，執行下列 cmdlet 以建立代表您 in Microsoft Azure 資料中心的邏輯網路物件：

1.  在 Azure 入口網站中，則請移至**網路**，然後按 \[**新增\]**。

2.  按一下 \[**網路服務**\>**虛擬網路**\>**新增本機網路**。

3.  在該網站上輸入您的第一個資料中心站台和 VPN 裝置的 IP 位址的名稱。此 IP 位址必須是靜態公用 IP 位址不背後的 nat。

4.  在下一步\] 畫面上，指定您的第一個網站的 IP 子網路。

5.  重複步驟 1 到 4 的第二個網站。

## 建立 Azure 虛擬網路

現在，執行下列 cmdlet 以建立會使用 Vm Azure 虛擬網路：

1.  在 Azure 的入口網站中移至**網路**，與 \[**新增**。

2.  按一下 \[**網路服務**\>**虛擬網路**\>**自訂的建立**。

3.  在 \[**虛擬網路詳細資料**\] 頁面上指定的虛擬網路的名稱並選取 \[網路的地理位置。

4.  在 \[ **DNS 伺服器和 VPN 連線**\] 頁面上，確認先前所登錄的 DNS 伺服器列為 DNS 伺服器。

5.  選取 \[**以網站連線設定網站 VPN**核取方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請勿選取<strong>使用 ExpressRoute</strong>因為如此可防止多個網站 VPN 設定所需的必要設定變更。</td>
    </tr>
    </tbody>
    </table>


6.  底下的 \[**區域網路**中，選取一個或兩個您所設定的內部網路。

7.  在 \[**虛擬網路位址空間**\] 頁面上，指定要用於 Azure 虛擬網路 IP 位址範圍。

## 檢查點： 檢閱網路設定

此時，當您前往**網路**時，您應該會看到 \[**虛擬網路**您本機**本機網路**與**DNS 伺服器**下的您註冊的 DNS 伺服器\] 下的網站設定虛擬網路。

## 階段 2： 設定多個網站 VPN

下一步是建立內部網站的 VPN 閘道。為達成此目的，您需要：

1.  使用 Azure 入口網站中建立一個網站的 VPN 閘道。

2.  將匯出虛擬網路組態設定。

3.  多個網站 VPN 修改設定檔。

4.  匯入更新 Azure 網路組態。

5.  記錄 Azure 閘道 IP 位址及預先共用的機碼。

6.  設定內部部署 VPN 裝置。

如需設定多個網站 VPN 的詳細資訊，請參閱 ＜[設定多個網站 VPN](http://go.microsoft.com/fwlink/?linkid=522621)。

## 建立您第一個網站的 VPN 閘道

建立虛擬閘道，記下您已經指定它將會連線至第一個內部部署網站。當您進入虛擬網路儀表板時，您會看到尚未建立閘道。

若要建立在 Azure 端 VPN 閘道，請遵循[設定虛擬網路閘道 Management Portal 中](http://msdn.microsoft.com/en-us/library/azure/jj156210.aspx)的 \[[啟動虛擬網路閘道](http://msdn.microsoft.com/en-us/library/azure/jj156210.aspx#bkmk_startgateway) \] 區段中的指示。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>僅執行步驟&quot;開始的虛擬網路閘道 」 章節中的文章和請勿繼續後續各節。</td>
</tr>
</tbody>
</table>


## 匯出虛擬網路組態設定

Azure 管理入口網站目前不允許您設定多個網站 VPN。此設定，您需要將虛擬網路組態設定匯出至 XML 檔案並修改該檔案。依照指示在[網路組態檔來匯出虛擬網路設定](http://msdn.microsoft.com/en-us/library/azure/dn133804.aspx)匯出您的設定。

## 修改多個網站 VPN 網路組態設定

在任何 XML 編輯器中開啟您匯出的檔案。閘道連線至內部網站列示於"ConnectionsToLocalNetwork 」 一節。找出 \[\] 區段中的 XML 檔中搜尋該字詞。本節中的設定檔看起來像下列 （假設您建立本機網站的 「 站台的 「 站台名稱）。

    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>

若要設定您的第二個網站，新增另一個"LocalNetworkSiteRef"區段的 \["ConnectionsToLocalNetwork 」 一節。 更新的設定檔中區段看起來像下列 （假設站台名稱的第二個本機網站是"網站 B"）。

    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
        <LocalNetworkSiteRef name="Site B">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>

將更新的組態設定檔案儲存。

## 匯入虛擬網路組態設定

已新增至設定檔的第二個站台參照會觸發 Microsoft Azure 來建立新的通道。匯入中[匯入網路組態檔](http://msdn.microsoft.com/en-us/library/azure/jj156213.aspx)使用指示的更新的檔案。完成匯入之後，虛擬網路儀表板會顯示兩個本機網站閘道連線。

## 記錄 Azure 閘道 IP 位址及預先共用的機碼

匯入新的網路組態設定之後，虛擬網路 dashboard 會顯示 Azure 閘道的 IP 位址。這是要連接兩個網站上的 VPN 裝置的 IP 位址。記錄參考 （英文） 此 IP 位址。

您也必須取得建立每個通道前共用的 IPsec/IKE 索引鍵。這些機碼以及 Azure 閘道 IP 位址會用於設定您的內部部署 VPN 裝置。

您需要使用 PowerShell 取得預先共用的機碼。如果您不熟悉使用 PowerShell 管理 Azure，請參閱[Azure PowerShell](http://msdn.microsoft.com/en-us/library/azure/jj156055.aspx)。

使用[Get AzureVNetGatewayKey](http://msdn.microsoft.com/en-us/library/azure/dn495198.aspx) cmdlet 可擷取前共用的機碼。執行此指令程式一次的每個通道。下列範例所示的命令會您需要執行以解壓縮虛擬網路"Azure Site"和"Site 的"和"網站 B 」 的網站之間的通道的機碼在這個範例中，輸出會儲存到不同的檔案。或者，您可以使用管線處理其他 PowerShell cmdlet 這些機碼或指令碼中使用。

    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site A" > C:\Keys\KeysForTunnelToSiteA.txt 
    
    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site B" > C:\Keys\KeysForTunnelToSiteB.txt

## 設定內部部署 VPN 裝置

Microsoft Azure 提供支援的 VPN 裝置 VPN 裝置組態指令碼。按一下適當的指令碼的 VPN 裝置的虛擬網路儀表板上**下載的 VPN 裝置指令碼**連結。

您下載指令碼會有時設定虛擬網路和可用時若要設定為該網站的 VPN 裝置所設定的第一個網站的組態設定。 例如，如果您建立虛擬網路站台 A 指定為**區域網路**，VPN 裝置指令碼可用於網站 a。但是您必須修改該設定的 VPN 裝置的網站 b。 特別是，您需要更新前共用的機碼以符合第二個站台的索引鍵。

例如，如果您要用於網站的路由和遠端存取服務 (RRAS) VPN 裝置，您必須：

1.  設定指令碼任何文字編輯器中開啟。

2.  尋找`#Add S2S VPN interface` \] 區段。

3.  本節中尋找**Add-VpnS2SInterface**命令。請確認*SharedSecret*參數的值符合您設定 VPN 裝置之網站的預先共用的金鑰。

其他裝置可能需要額外的驗證。例如，Cisco 裝置組態指令碼會將使用本機的 IP 位址範圍設定 ACL 規則。您需要檢閱才能使用該驗證本機站台設定指令碼中的所有參考。請參閱下列主題的詳細資訊：

[路由及遠端存取服務 (RRAS) 範本](http://msdn.microsoft.com/en-us/library/azure/dn133801.aspx)

[Cisco ASR 範本](http://msdn.microsoft.com/en-us/library/azure/dn133802.aspx)

[Cisco ISR 範本](http://msdn.microsoft.com/en-us/library/azure/dn133800.aspx)

[Juniper SRX 範本](http://msdn.microsoft.com/en-us/library/azure/dn133794.aspx)

[Juniper J 數列範本](http://msdn.microsoft.com/en-us/library/azure/dn133799.aspx)

[Juniper ISG 範本](http://msdn.microsoft.com/en-us/library/azure/dn133797.aspx)

[Juniper SSG 範本](http://msdn.microsoft.com/en-us/library/azure/dn133796.aspx)

## 檢查點： 檢閱 VPN 狀態

此時，兩個網站會連線到透過 VPN 閘道 Azure 虛擬網路。您可以 PowerShell 中執行下列命令來驗證多個網站 VPN 的狀態。

    Get-AzureVnetConnection -VNetName "Azure Site" | Format-Table LocalNetworkSiteName, ConnectivityState

如果這兩個通道會啟動並執行，此命令的輸出看起來像下列。

    LocalNetworkSiteName    ConnectivityState
    
    --------------------    -----------------
    
    Site A                  Connected
    
    Site B                  Connected

您也可以透過 Azure management portal 中檢視虛擬網路儀表板驗證連線。兩個網站的 \[**狀態**\] 欄位會顯示為**已連接**。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>它可能需要數分鐘後會出現在 Azure 管理入口網站中的狀態變更為已成功建立連線。</td>
</tr>
</tbody>
</table>


## 階段 3： 設定虛擬機器

您需要建立此部署 in Microsoft Azure 兩個虛擬機器的最小值： 在網域控制站與將會當做 DAG 見證的檔案伺服器。

1.  建立虛擬機器在網域控制站與您在[建立虛擬機器執行 Windows](http://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-tutorial/)中使用指示的檔案伺服器。請務必選取 \[指定設定的虛擬機器時的**地區/親和性群組/虛擬網路**建立虛擬網路。

2.  指定慣用的網域控制站和使用 Azure PowerShell 檔案伺服器的 IP 位址。當您指定的虛擬機器的慣用的 IP 位址時，則需要更新，這將會需要重新啟動虛擬機器。下列範例中的 IP 位址 Azure DC 與 Azure FSW 10.0.0.10 與 10.0.0.11 將分別設定為。
    
        Get-AzureVM Azure-DC | Set-AzureStaticVNetIP -IPAddress 10.0.0.10 | Update-AzureVM
        
        Get-AzureVM Azure-FSW | Set-AzureStaticVNetIP -IPAddress 10.0.0.11 | Update-AzureVM
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>慣用的 IP 位址的 VM 會嘗試使用該位址。不過，如果該位址已指派給不同的虛擬機器，也不會啟動喜好的 IP 位址設定虛擬機器。若要避免此情況下，請確定您使用 IP 位址不指派給其他虛擬機器。請參閱<a href="http://msdn.microsoft.com/library/azure/dn630228.aspx">Configure VM 靜態內部 IP 位址</a>的詳細資訊。</td>
    </tr>
    </tbody>
    </table>


3.  佈建網域控制站上使用標準貴組織所使用的 Azure 虛擬機器。

4.  準備讓檔案伺服器與 Exchange DAG 見證的必要條件：
    
    1.  新增使用 \[新增角色及功能精靈\] 或[Add-windowsfeature](http://technet.microsoft.com/en-us/library/ee662309.aspx)指令程式檔案伺服器角色\]。
    
    2.  將 Exchange 受信任子系統萬用安全性群組新增至本機系統管理員群組。

## 檢查點： 檢閱虛擬機器狀態

此時，讓虛擬機器應該啟動並執行並應該能夠與這兩個內部部署資料中心伺服器通訊：

  - 確認您在 Azure 中的網域控制站已複寫內部部署網域控制站。

  - 確認您可以連線到檔案伺服器 Azure 上的依名稱建立 SMB 連線從 Exchange 伺服器。

  - 確認依名稱從檔案伺服器在 Azure 上可以找到 \[Exchange 伺服器。

## 階段 4： 設定 DAG 見證

最後，您需要設定 DAG 以使用新的見證伺服器。根據預設，Exchange 會使用 C:\\DAGFileShareWitnesses 為檔案共用見證路徑見證伺服器上。如果您使用的自訂檔案路徑，您也應該更新特定共用的見證目錄。

1.  連線至Exchange 管理命令介面。

2.  執行下列命令以設定您的 Dag 的見證伺服器。
    
        Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessServer Azure-FSW

請參閱下列主題的詳細資訊：

[設定資料庫可用性群組內容](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-databaseavailabilitygroup](http://technet.microsoft.com/en-us/library/dd297934\(v=exchg.150\).aspx)

## 檢查點： 驗證 DAG 檔案共用見證

此時，您已設定在 Azure 上使用檔案伺服器做為 DAG 見證 DAG。執行下列 cmdlet 以驗證您的設定：

1.  執行下列命令來驗證 DAG 組態。
    
        Get-DatabaseAvailabilityGroup -Identity DAG1 -Status | Format-List Name, WitnessServer, WitnessDirectory, WitnessShareInUse
    
    *WitnessServer*參數設為在 Azure 上檔案伺服器、 *WitnessDirectory*參數設為正確的路徑及*WitnessShareInUse*參數會顯示**Primary**確認。

2.  如果 DAG 有偶數的節點，即會設定檔案共用見證。 驗證檔案共用見證叢集屬性設定來執行下列命令。*SharePath*參數值應指向 \[檔案伺服器並顯示正確路徑。
    
        Get-ClusterResource -Cluster MBX1 | Get-ClusterParameter | Format-List

3.  下一步\] 執行下列命令來確認 「 檔案共用見證 」 叢集資源的狀態。叢集資源*State*應該顯示**Online**。
    
        Get-ClusterResource -Cluster MBX1

4.  最後，驗證共用已成功建立檔案伺服器上透過檢閱在檔案總管\] 中的資料夾及共用在 \[伺服器管理員。

## 請參閱


[規劃高可用性及站台恢復](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
[轉換及容錯移轉](switchovers-and-failovers-exchange-2013-help.md)  
[管理資料庫可用性群組](managing-database-availability-groups-exchange-2013-help.md)


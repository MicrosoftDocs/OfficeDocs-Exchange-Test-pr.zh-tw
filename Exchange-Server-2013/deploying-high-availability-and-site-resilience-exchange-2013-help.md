---
title: '部署高可用性和站台恢復: Exchange 2013 Help'
TOCTitle: 部署高可用性和站台恢復
ms:assetid: 4c4e00a4-1f57-4fdb-b9b2-2779abf381a9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638129(v=EXCHG.150)
ms:contentKeyID: 50473193
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 部署高可用性和站台恢復

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

針對高可用性和站台恢復，Microsoft Exchange Server 2013 使用名為*「增量部署」*的概念。您只要將兩部以上的 Exchange 2013 信箱伺服器安裝為獨立伺服器，然後視需要累加地設定信箱伺服器和信箱資料庫，就能提供高可用性和站台恢復。

## 部署程序的概觀

雖然每個組織所使用的實際步驟有些許不同，但是以高可用或站台恢復組態來部署 Exchange 2013 的整體程序通常是相同的。在執行建立與部署資料庫可用性群組 (DAG) 及建立信箱資料庫副本的必要規劃與設計工作之後，您應該：

1.  建立 DAG。如需詳細步驟，請參閱[建立資料庫可用性群組](create-a-database-availability-group-exchange-2013-help.md)。

2.  如有需要，請預先接移叢集名稱物件 (CNO)。在部署信箱伺服器執行 Windows Server 2012 的 DAG 時，必須預先設置 CNO。如果您要以執行 Windows Server 2012 R2 的信箱伺服器部署不含管理存取點的 DAG，則無需預先配置 CNO。在電腦帳戶建立受限的環境、或電腦帳戶在預設電腦容器以外的容器建立時也需要預先接移。如需詳細步驟，請參閱[針對資料庫可用性群組預先接移叢集名稱物件](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)。

3.  將兩個或多個信箱伺服器新增到 DAG。如需詳細步驟，請參閱[管理資料庫可用性群組成員資格](manage-database-availability-group-membership-exchange-2013-help.md)。

4.  視需要設定 DAG 內容：
    
    1.  可以選擇性地設定 DAG 加密和壓縮、複寫連接埠、DAG IP 位址及其他 DAG 內容。如需詳細步驟，請參閱[設定資料庫可用性群組內容](configure-database-availability-group-properties-exchange-2013-help.md)。
    
    2.  為 DAG 啟用資料中心啟動協調 (DAC) 模式。這樣可保護 DAG 在執行資料中心轉換完成後切換回主要資料中心時，不會產生資料庫層級核心分裂狀況，同時也將啟用內建 DAG 復原 Cmdlet 的使用。如需詳細資訊，請參閱[資料中心啟動協調模式](datacenter-activation-coordination-mode-exchange-2013-help.md)。

5.  在 DAG 中，跨信箱伺服器新增信箱資料庫副本。如需詳細步驟，請參閱[新增信箱資料庫副本](add-a-mailbox-database-copy-exchange-2013-help.md)。

## 部署範例：在兩個資料中心中的四個成員 DAG

本範例詳細說明 Contoso, Ltd. 組織如何設定與部署四個成員的 DAG，且此 DAG 將會遍佈兩個實體位置：華盛頓雷德蒙以及奧勒岡波特蘭。

## 基本基礎結構

每個位置包含以 Exchange 2013 為基礎操作郵件傳送基礎結構的基礎結構元素，也就是下列項目：

  - 目錄服務 (Active Directory 或 Active Directory 網域服務 (AD DS))

  - 網域名稱系統 (DNS) 名稱解析

  - 多個 Exchange 2013 用戶端存取伺服器

  - 多個 Exchange 2013 信箱伺服器

下圖說明 Contoso 組態。

**遍佈兩個站台的資料庫可用性群組**

![延伸到兩個站台的資料庫可用性群組](images/Dd638129.1c326fd4-3c7b-4416-a63d-fbfdd0cc6b18(EXCHG.150).gif "延伸到兩個站台的資料庫可用性群組")

## 網路組態

如前圖所述，該方案包含多個子網路和多個網路的使用。DAG 中的每個信箱伺服器在個別子網路上都有兩個網路介面卡。在每個信箱伺服器中，其中一個網路介面卡將用於 MAPI 網路 (192.168.*x*.*x*)，而另一個網路介面卡將用於複寫網路 (10.0.*x*.*x*)。只有 MAPI 網路提供與 Active Directory、DNS 服務、其他 Exchange 伺服器及用戶端的連線。每個成員中的複寫網路所使用的介面卡僅提供與 DAG 其他成員中之複寫網路介面卡的連線。

下表詳細說明每個節點中每個網路介面卡的設定。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>IPv4 位址</th>
<th>子網路遮罩</th>
<th>預設閘道</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MBX1 (MAPI)</p></td>
<td><p>192.168.1.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>MBX2 (MAPI)</p></td>
<td><p>192.168.1.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX3 (MAPI)</p></td>
<td><p>192.168.2.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="even">
<td><p>MBX4 (MAPI)</p></td>
<td><p>192.168.2.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX1 (複寫)</p></td>
<td><p>10.0.1.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>無</p></td>
</tr>
<tr class="even">
<td><p>MBX2 (複寫)</p></td>
<td><p>10.0.1.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>無</p></td>
</tr>
<tr class="odd">
<td><p>MBX3 (複寫)</p></td>
<td><p>10.0.2.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>無</p></td>
</tr>
<tr class="even">
<td><p>MBX4 (複寫)</p></td>
<td><p>10.0.2.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>無</p></td>
</tr>
</tbody>
</table>


如上表所示，用於複寫網路的介面卡不使用預設閘道。為了在每個複寫網路介面卡之間提供網路連線，Contoso 使用持續性靜態路由，這些路由是使用 Netsh.exe 工具所設定。

為了設定 MBX1 和 MBX2 上之複寫網路介面卡的路由，每個伺服器上都執行了以下命令。

    netsh interface ipv4 add route 10.0.2.0/24 <NetworkName> 10.0.1.254

為了設定 MBX3 和 MBX4 上之複寫網路介面卡的路由，每個伺服器上都執行了以下命令。

    netsh interface ipv4 add route 10.0.1.0/24 <NetworkName> 10.0.2.254

下列額外的網路設定也已經設定：

  - 為每個 DAG 成員的 MAPI 網路介面卡選取 **\[在 DNS 中登錄這個連線網路的位址\]** 核取方塊，並為每個複寫網路介面卡清除該核取方塊。

  - 至少為每個 DAG 成員的 MAPI 網路介面卡設定一個 DNS 伺服器位址，且不為複寫網路介面卡設定任何 DNS 伺服器位址。為了做到備援，Contoso 為其 MAPI 網路介面卡使用了多個 DNS 伺服器地址。

  - Contoso 未使用 Windows 防火牆，而且已經在其伺服器上將它關閉。

在設定網路介面卡之後，Contoso 已準備好建立 DAG 及新增信箱伺服器到 DAG。

## 資料庫可用性群組建立與組態

系統管理員已決定建立執行數個工作的 Windows PowerShell 命令列介面指令碼：

  - 它會使用 [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd351107\(v=exchg.150\)) 指令程式來建立 DAG。因為考慮將 REDMOND 當作主要資料中心，Contoso 已選擇在同一個資料中心 (也就是 CAS1) 中使用見證伺服器。

  - 它使用 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd297934\(v=exchg.150\)) 指令程式來預先設定其他見證伺服器和備用見證目錄，以防隨時需要資料中心轉換。

  - 它使用 [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-tw/library/dd298049\(v=exchg.150\)) 指令程式將四個信箱伺服器的每一個新增到 DAG。

  - 它使用 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd297934\(v=exchg.150\)) 指令程式來設定 DAG 的 DAC 模式。如需 DAC 模式的詳細資訊，請參閱[資料中心啟動協調模式](datacenter-activation-coordination-mode-exchange-2013-help.md)。

指令碼中使用的命令如下：

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer CAS1 -WitnessDirectory C:\DAGWitness\DAG1.contoso.com -DatabaseAvailabilityGroupIPAddresses 192.168.1.8,192.168.2.8

上述命令會建立 DAG (DAG1)、設定 CAS1 做為見證伺服器、設定特定的見證目錄 (C:\\DAGWitness\\DAG1.contoso.com)，以及為 DAG 設定兩個 IP 地址 (MAPI 網路上的每個子網路各一個)。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGWitness\DAG1.contoso.com -AlternateWitnessServer CAS4

上述命令設定 DAG1 使用 CAS4 的備用見證伺服器及使用 CAS1 上設定之相同路徑的 CAS4 上的備用見證目錄。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用相同路徑並非必要；Contoso 選擇這樣做是為了標準化其組態。</td>
</tr>
</tbody>
</table>


    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX3
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX2
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX4

上述命令將每個信箱伺服器新增到 DAG 中，一次一個。該命令也會在每個信箱伺服器上安裝 Windows 容錯移轉叢集 (如果尚未安裝)、建立容錯移轉叢集，並將每個信箱伺服器加入新建立的叢集。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly

上述命令啟用了 DAG 的 DAC 模式。

## 信箱資料庫與信箱資料庫副本

在建立 DAG 和新增信箱伺服器到 DAG 之後，Contoso 準備要建立信箱資料庫和信箱資料庫副本。為了符合他們預防失敗的準則，Contoso 計畫為每個信箱資料庫設定三個非延遲資料庫副本，以及一個延遲資料庫副本。延遲副本的記錄檔重新顯示將會設定為三天的延遲。

此組態為每個資料庫提供總計四個副本 (一個在作用中、兩個非延遲被動，以及一個延遲被動)。Contoso 計劃每個伺服器有四個作用中的資料庫。由於每個伺服器有四個作用中的資料庫，而每個資料庫有三個被動副本，因此 Contoso 解決方案總計包含了 16 個資料庫副本。

如下圖所示，Contoso 為他們的資料庫配置採取了一種平衡方式。

**Contoso, Ltd 的資料庫副本配置**

![Contoso, Ltd 的資料庫副本佈局](images/Dd638129.41d0c78e-ccaf-4b67-8bab-6fb344668ead(EXCHG.150).gif "Contoso, Ltd 的資料庫副本佈局")

每個信箱伺服器都主控一個作用中的信箱資料庫副本、兩個非延遲被動資料庫副本，以及一個延遲被動資料庫副本。每個作用中信箱資料庫的延遲副本是由其他站台中的信箱伺服器所主控。

若要建立這種組態，系統管理員必須執行數個命令。

在 MBX1 上，執行下列命令。

    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -SuspendComment "Seed from MBX4" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB1\MBX3 -SourceServer MBX4
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -ActivationOnly

在 MBX2 上，執行下列命令。

    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -SuspendComment "Seed from MBX3" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB2\MBX4 -SourceServer MBX3
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -ActivationOnly

在 MBX3 上，執行下列命令。

    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -SuspendComment "Seed from MBX2" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB3\MBX1 -SourceServer MBX2
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -ActivationOnly

在 MBX4 上，執行下列命令。

    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX2 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -SuspendComment "Seed from MBX1" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB4\MBX2 -SourceServer MBX1
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -ActivationOnly

在上述 **Add-MailboxDatabaseCopy** 指令程式的範例中，並未指定 *ActivationPreference* 參數。該工作會隨著他們所新增的每個副本自動遞增啟動喜好設定編號。原始資料庫的喜好設定編號一定是 1。使用 **Add-MailboxDatabaseCopy** 指令程式新增的第一個副本的喜好設定編號會自動指派為 2。假設沒有任何副本移除，新增的下一個副本的喜好設定編號會自動指派為 3，依此類推。因此，在上述範例中，與作用中副本在同一個資料中心中的被動副本的啟動喜好設定編號為 2、遠端資料中心中的非延遲被動副本的啟動喜好設定編號為 3，而遠端資料中心中的延遲被動副本的啟動喜好設定編號則為 4。

雖然在 WAN 上的其他位置中，每個作用中的資料庫有兩個副本，但是透過 WAN 植入只會執行一次。這是因為 Contoso 利用 Exchange 2013 功能將資料庫的被動副本當作植入的來源。使用 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd298105\(v=exchg.150\)) 指令程式搭配 *SeedingPostponed* 參數，可防止該工作自動植入已建立的新資料庫副本。然後，系統管理員可以擱置未植入的副本，並且透過使用 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\)) 指令程式搭配 *SourceServer* 參數，將資料庫的本機副本指定為植入作業的來源。因此，新增至每個位置的第二個資料庫副本植入會在本機上進行，而不會透過 WAN 進行。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在上述範例中，非延遲資料庫副本是透過 WAN 植入，然後該副本會用來植入與非延遲副本在相同資料中心中的資料庫延遲副本。</td>
</tr>
</tbody>
</table>


Contoso 已經將每個信箱資料庫的其中一個被動副本設定為延遲資料庫副本，以提供保護，預防極少發生但卻極端嚴重的資料庫邏輯損毀。因此，系統管理員會使用 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd351074\(v=exchg.150\)) 指令程式搭配 *ActivationOnly* 參數，將延遲副本設定為阻止啟動。這可確保如果發生資料庫或伺服器容錯移轉，延遲資料庫副本將不會啟動。

## 驗證解決方案

在部署和設定解決方案之後，管理員在將工作信箱移至 DAG 的資料庫之前，執行數個工作以確認解決方案已準備就緒。應該使用數個方式 (包括失敗模擬) 來測試與檢查解決方案。為驗證解決方案，系統管理員會執行幾項工作。

為了驗證 DAG 的整體健康狀況，系統管理員會執行 [Test-ReplicationHealth](https://technet.microsoft.com/zh-tw/library/bb691314\(v=exchg.150\)) 指令程式。這個指令程式會檢查複寫與重新顯示狀態的數個層面，提供有關每個信箱伺服器與 DAG 中之資料庫副本的資訊。

為了驗證副本與重新顯示活動，系統管理員會執行 [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-tw/library/dd298044\(v=exchg.150\)) 指令程式。這個指令程式可提供特定信箱資料庫副本或特定伺服器上之所有信箱資料庫副本的即時狀態資訊。如需監視 DAG 中之複寫資料庫健康狀況與狀態的詳細資訊，請參閱[監視資料庫可用性群組](monitoring-database-availability-groups-exchange-2013-help.md)。

為了驗證轉換工作一如預期，系統管理員會使用 [Move-ActiveMailboxDatabase](https://technet.microsoft.com/zh-tw/library/dd298068\(v=exchg.150\)) Cmdlet 來執行一系列的資料庫轉換和伺服器轉換。當這些工作順利完成時，系統管理員會使用相同的指令程式將作用中的資料庫副本移回其原始位置。

為了驗證各種失敗案例中的預期行為，系統管理員會執行數個工作以模擬失敗或實際引起失敗發生。例如，系統管理員可能會：

  - 拔除 MBX1 的電源線，藉以觸發伺服器容錯移轉。然後，系統管理員會驗證 DB1 在另一個伺服器 (根據啟動喜好設定值，最好是 MBX2) 上成為作用中。

  - 拔除 MBX2 上 MAPI 網路介面卡的網路線，藉以觸發伺服器容錯移轉。然後，系統管理員會驗證 DB2 在另一個伺服器 (根據啟動喜好設定值，最好是 MBX1) 上成為作用中。

  - 將 DB3 的作用中副本所使用的磁碟離線，藉以觸發資料庫容錯移轉。然後，系統管理員會驗證 DB3 在另一個伺服器 (根據啟動喜好設定值，最好是 MBX4) 上成為作用中。

根據業務需要，組織可以測試其他失敗案例。在模擬單一失敗 (例如拔除電源插頭) 並驗證解決方案的復原行為之後，系統管理員可將解決方案還原至其原始組態。在某些情況下，可以針對多個同時發生的失敗，測試解決方案。最後，在完成每個失敗模擬之後，您的解決方案測試計畫會指示該解決方案是否要還原為其原始組態。

此外，系統管理員可能決定中斷兩個資料中心之間的網路連線，藉以模擬站台失敗。執行資料中心轉換是更複雜且更需要協調的程序；不過，如果希望所部署的解決方案能針對郵件服務與資料提供站台恢復，建議您進行此程序。

## 轉換至作業

在部署解決方案之後，可以使用增量部署將它進一步擴充。此時，解決方案的管理也會轉換為作業程序，下列工作將在其中執行：

  - 監視 DAG 與信箱資料庫副本的健康狀況與狀態。如需詳細資訊，請參閱[監視資料庫可用性群組](monitoring-database-availability-groups-exchange-2013-help.md)。

  - 視需要執行資料庫轉換。如需如何執行資料庫轉換的詳細步驟，請參閱[啟動信箱資料庫副本](activate-a-mailbox-database-copy-exchange-2013-help.md)。

如需管理解決方案的詳細資訊，請參閱[管理高可用性和站台恢復](managing-high-availability-and-site-resilience-exchange-2013-help.md)。


---
title: '建立資料庫可用性群組: Exchange 2013 Help'
TOCTitle: 建立資料庫可用性群組
ms:assetid: d6b98299-e203-488b-af73-50753fe152c8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351172(v=EXCHG.150)
ms:contentKeyID: 50474354
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立資料庫可用性群組

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

資料庫可用性群組 (DAG) 是一組 Microsoft Exchange Server 2013 信箱伺服器，數量最多可達 16 部，可提供從資料庫、伺服器或網路失敗中進行自動復原資料庫層級的功能。當您將 Mailbox Server 新增至 DAG 後，它即可與 DAG 中其他的伺服器搭配使用，以在資料庫、服務器和網路失敗時提供自動的資料庫層級復原功能。

要尋找與 DAG 相關的其他管理工作嗎？請參閱[管理資料庫可用性群組](managing-database-availability-groups-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：1 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md) 主題中的「資料庫可用性群組」項目。

  - 透過執行 Windows Server 2012 的信箱伺服器建立 DAG 時，必須預先設置叢集名稱物件 (CNO)，然後才可將成員新增至 DAG。如果建立的 DAG 沒有執行 Windows Server 2012 R2 之 Mailbox Server 的管理存取點，則不需要預先接移 DAG 的 CNO。如需詳細步驟，請參閱[針對資料庫可用性群組預先接移叢集名稱物件](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)。

  - 建立 DAG 時，您必須提供 DAG 的唯一名稱，名稱中最多可包含 15 個字元。除非建立的 Windows Server 2012 R2 DAG 沒有管理存取點，而且未將任何 IP 位址指派給 DAG，否則除了提供 DAG 的名稱外，您還必須為 DAG 指派一或多個 IP 位址 (使用 IPv4 或是同時使用 IPv4 與 IPv6)。否則，您指派的 IP 位址必須位於將用於 MAPI 網路的各個子網路上，而且必須可用。如果您指定一或多個 IPv4 位址，而且設定您的系統使用 IPv6，工作也將嘗試為 DAG 指定一或多個 IPv6 位址。

  - 建立 DAG 時，您可以選擇指定見證伺服器和見證目錄。如果指定見證伺服器，建立您使用未安裝信箱伺服器角色的用戶端存取伺服器。這可讓 Exchange 系統管理員注意到見證的可用性，並確保使用見證伺服器所需的所有必要安全性權限準備就緒。
    
    以下是可用的選項與行為組合：
    
      - 您可以只指定 DAG 的名稱，並讓 \[見證伺服器\] 與 \[見證目錄\] 欄位保留空白。在此情況下，工作會搜尋尚未安裝信箱伺服器角色的用戶端存取伺服器。這將在該用戶端存取伺服器自動建立預設見證目錄並共用，並且設定 DAG 使用該伺服器作為其見證伺服器。
    
      - 您可以指定 DAG 的名稱、您要使用的見證伺服器、以及您要在見證伺服器上建立並共用的目錄。
    
      - 您可以指定 DAG 的名稱和要使用的見證伺服器，然後將 \[見證目錄\] 欄位保留空白。在此情況下，工作將會在指定的見證伺服器上建立預設見證目錄。
    
      - 您可以指定 DAG 的名稱、將 \[見證伺服器\] 欄位保留空白，並指定您要在見證伺服器上建立及共用的目錄。在此情況下，此精靈將會搜尋未安裝信箱伺服器角色的用戶端存取伺服器，並且將自動在該伺服器上建立指定的見證目錄並加以共用，並設定 DAG 使用該用戶端存取伺服器作為見證伺服器。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您指定見證伺服器不是Exchange 2013或Exchange 2010伺服器，您必須以本機管理員群組的見證伺服器上新增Exchange受信任子系統萬用安全性群組。下列安全性權限所需確保該Exchange可以建立目錄並視需要見證伺服器上共用。如果未設定適當的權限，則會傳回下列錯誤：<br />
    <code>Error: An error occurred during discovery of the database availability group topology. Error: An error occurred while attempting a cluster operation. Error: Cluster API &quot;AddClusterNode() (MaxPercentage=12) failed with 0x80070005. Error: Access is denied.&quot;</code></td>
    </tr>
    </tbody>
    </table>


  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用 EAC 建立資料庫可用性群組

1.  在 EAC 中，移至 \[伺服器\] \> \[資料庫可用性群組\]。

2.  按一下 ![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 建立 DAG。

3.  
    
    在 \[新增資料庫可用性群組\] 頁面上，針對新的 DAG 提供下列資訊：
    
      - \[資料庫可用性群組名稱\]   使用此欄位可輸入最多 15 個字元的 DAG 唯一有效名稱。此名稱相當於電腦名稱，並會在 Active Directory 中使用該名稱建立對應的 CNO。此名稱將是 DAG 的名稱及基礎叢級的名稱。
    
      - \[驗證伺服器\]   使用此欄位可指定 DAG 的見證伺服器。如果您將此欄位保留空白，系統將嘗試自動選取本機 Active Directory 站台中的用戶端存取伺服器，這個本機 Active Directory 站台並非安裝在信箱伺服器作為見證伺服器的電腦上。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>若是您指定了見證伺服器，必須使用主機名稱或網域全名 (FQDN)。不支援使用 IP 位址或萬用字元名稱。此外，見證伺服器不得為 DAG 的成員。</td>
        </tr>
        </tbody>
        </table>
    
      - \[見證目錄\]   使用此欄位可輸入見證伺服器將用來儲存見證資料的目錄路徑。如果目錄不存在，系統會在見證伺服器上為您建立該目錄。如果將此欄位保留空白，將在見證伺服器建立預設目錄 (%SystemDrive%\\DAGFileShareWitnesses\\\<DAG FQDN\>)。
    
      - \[資料庫可用性群組 IP 位址\]   使用此欄位可將一或多個靜態 IPv4 位址指派給 DAG。輸入 IPv4 位址，並且按一下 ![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 新增該位址。如果要 DAG 使用動態主機設定通訊協定 (DHCP) 取得必要的 IPv4 位址，請將此欄位保留空白。您可以選擇輸入 255.255.255.255 建立沒有 IP 位址或叢集管理存取點的 DAG，這僅適用於包含執行 Windows Server 2012 R2 之 Mailbox Server 的 DAG。

4.  按一下 \[儲存\] 以建立 DAG。

## 使用命令介面建立資料庫可用性群組

此範例會建立名為 DAG1、依設定會使用見證伺服器 FILESRV1 以及本機目錄 C:\\DAG1 的 DAG。DAG1 依設定也會針對 DAG 的 IP 位址使用 DHCP。

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer FILESRV1 -WitnessDirectory C:\DAG1

此範例會建立 DAG DAG2。系統會自動在本機 Active Directory 站台中選取不含 Mailbox server role 的 Client Access Server，作為 DAG 的見證伺服器。DAG2 將被指派一個靜態 IP 位址，因為在此例中所有 DAG 成員都有 MAPI 網路在相同的子網路上。

    New-DatabaseAvailabilityGroup -Name DAG2 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

此範例會建立 DAG DAG3。DAG3 已設定為使用見證伺服器 MBX2，以及本機目錄 C:\\DAG3。DAG3 會被指派多個靜態 IP 位址，因為其 DAG 成員位於 MAPI 網路的不同子網路上。

    New-DatabaseAvailabilityGroup -Name DAG3 -WitnessServer MBX2 -WitnessDirectory C:\DAG3 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,192.168.0.8

此範例會建立名為 DAG4、依設定會使用 DHCP 的 DAG。此外，系統將會自動選取見證伺服器，並且會建立預設見證目錄。

    New-DatabaseAvailabilityGroup -Name DAG4

此範例會建立將不會有管理存取點的 DAG DAG5 (僅適用於 Windows Server 2012 R2 DAG)。此外，MBX4 將用作 DAG 的見證伺服器，並且會建立預設見證目錄。

    New-DatabaseAvailabilityGroup -Name DAG5 -DatabaseAvailabilityGroupIPAddresses ([System.Net.IPAddress]::None) -WitnessServer MBX4

## 如何知道這是否正常運作？

若要確認您是否成功建立 DAG，請執行下列其中一項：

  - 在 EAC 中，瀏覽至 \[伺服器\] \> \[資料庫可用性群組\]。新建立的 DAG 隨即顯示。

  - 在命令介面中執行下列命令，確認已建立 DAG，並顯示 DAG 屬性資訊。
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## 相關資訊

[資料庫可用性群組 (DAGs)](database-availability-groups-dags-exchange-2013-help.md)

[設定資料庫可用性群組內容](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd297934\(v=exchg.150\))

[New-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd351107\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-tw/library/dd335225\(v=exchg.150\))

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-tw/library/dd298049\(v=exchg.150\))


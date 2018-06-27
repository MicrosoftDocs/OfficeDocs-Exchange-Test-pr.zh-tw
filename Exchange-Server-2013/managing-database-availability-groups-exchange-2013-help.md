---
title: '管理資料庫可用性群組: Exchange 2013 Help'
TOCTitle: 管理資料庫可用性群組
ms:assetid: 74be3f97-ec0f-4d2a-b5d8-7770cc489919
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298065(v=EXCHG.150)
ms:contentKeyID: 50473504
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理資料庫可用性群組

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-10-04_

資料庫可用性群組 (DAG) 是最多有 16 個 Microsoft Exchange Server 2013 Mailbox 伺服器的組合，提供從資料庫、伺服器或是網路失敗時，自動的資料庫層級復原能力。DAG 使用連續複寫與 Windows 容錯移轉叢集技術子集，提供高可用性與站台回覆性。DAG 中的信箱伺服器可以監視彼此是否出現失敗情況。當您將 Mailbox Server 新增至 DAG 後，它即可與 DAG 中其他的伺服器搭配使用，以在資料庫失敗時提供自動的資料庫層級復原功能。

DAG 在建立時一開始是空的。當您新增第一個伺服器到 DAG 時，就會自動為 DAG 建立容錯移轉叢集。此外，還會初始化監視伺服器的網路或伺服器失敗的基礎結構。然後使用容錯移轉叢集活動訊號機制和叢集資料庫來追蹤和管理可能快速變更的 DAG 資訊，例如資料庫裝載狀態、複寫狀態和最後裝載位置。

**目錄**

Creating DAGs

DAG membership

Configuring DAG properties

DAG networks

Configuring DAG members

Performing maintenance on DAG members

Shutting down DAG members

Installing updates on DAG members

## 建立 DAG

您可以在 Exchange 系統管理中心 (EAC) 中使用 \[新增資料庫可用性群組\] 精靈，或是在 Exchange 管理命令介面中執行 **New-DatabaseAvailabilityGroup** 指令程式來建立 DAG。建立 DAG 時，您需要提供 DAG 的名稱，以及選用的見證伺服器和見證目錄設定。此外，還會使用靜態 IP 地址，或允許 DAG 使用動態主機設定通訊協定 (DHCP) 自動指派所需的 IP 位址 (DHCP)，將一或多個 IP 位址指派給 DAG。您可以使用 *DatabaseAvailabilityGroupIpAddresses* 參數，以手動方式為 DAG 指派 IP 位址。如果您省略此參數，則 DAG 會嘗試使用網路上的 DHCP 伺服器來取得 IP 地址。

如果建立的 DAG 將包含執行 Windows Server 2012 R2 的 Mailbox Server，則也可以選擇建立沒有叢集管理存取點的 DAG。在該情況下，叢集在 Active Directory 中不會有叢集名稱物件 (CNO)，而且叢集核心資源群組不會包含網路名稱資源或 IP 位址資源。

如需有關如何建立 DAG 的詳細步驟，請參閱[建立資料庫可用性群組](create-a-database-availability-group-exchange-2013-help.md)。

當您建立 DAG 時，會在 Active Directory 中建立一個表示 DAG 的空物件，其具有所指定的名稱和 **msExchMDBAvailabilityGroup** 的物件類別。

DAG使用 Windows 容錯移轉叢集技術子集，例如叢集律動、叢集網路以及層級資料庫 (可儲存變更或是快速變更的資料，例如資料庫狀態從主動變被動或是從被動變主動，或是從已裝載變為已卸載或是已卸載變為已裝載)。因為 DAG 倚賴 Windows 容錯移轉叢集，所以只能在執行 Windows Server 2008 R2 Enterprise or Datacenter 作業系統、Windows Server 2012 Standard 或 Datacenter 作業系統或 Windows Server 2012 R2 Standard 或 Datacenter 作業系統的 Exchange 2013 Mailbox Server 上建立。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由 DAG 建立及使用的容錯移轉叢集必須供 DAG 專用。該叢集不可供任何其他高可用性解決方案或任何其他目的使用。例如，容錯移轉叢集不可用來叢集其他應用程式或服務。不支援針對非 DAG 目的使用 DAG 的基礎容錯移轉叢集。</td>
</tr>
</tbody>
</table>


## DAG 見證伺服器與見證目錄

建立 DAG 時，您必須為 DAG 指定一個在 Active Directory 樹系中唯一且不超過 15 個字元的名稱。此外，每個 DAG 都會設定見證伺服器和見證目錄。見證伺服器及其目錄僅供在具有偶數個成員數之 DAG 仲裁使用。您不需要事先建立見證目錄。Exchange 會自動在見證伺服器上為您建立和保護目錄。除了 DAG 見證伺服器之外，目錄不應用於任何其他用途。

見證伺服器的需求如下：

  - 見證伺服器不得為 DAG 的成員。

  - 見證伺服器必須與 DAG 位於相同的 Active Directory 樹系中。

  - 見證伺服器必須執行支援的 Windows Server 版本。如需詳細資訊，請參閱[Exchange 2013 系統需求](exchange-2013-system-requirements-exchange-2013-help.md)。

  - 一個伺服器可以作為多個 DAG 的見證。不過，每個 DAG 需要它自己的見證目錄。

不論使用什麼伺服器作為見證伺服器，如果預訂的見證伺服器上已啟用 Windows 防火牆，則必須啟用檔案及印表機共用的 Windows 防火牆例外。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您指定見證伺服器不是Exchange 2013或Exchange 2010伺服器，您必須以之前建立 DAG 的見證伺服器上的本機管理員群組新增Exchange受信任子系統萬用安全性群組 (USG)。下列安全性權限所需確保該Exchange可以建立目錄並視需要見證伺服器上共用。<br />
見證伺服器使用 SMB 連接埠 445。</td>
</tr>
</tbody>
</table>


見證伺服器和見證目錄都不需要具備容錯能力，或使用任何形式的備援或具備高可用性。不需要為見證伺服器使用叢集檔案伺服器，或為見證伺服器使用任何其他形式的恢復功能。這樣做有幾個原因。在需要見證伺服器之前，必須使用幾個較大的 DAG (例如，六個或更多成員) 來處理失敗。因爲六個成員的 DAG 最多可以容忍兩個 Voter 失敗而不遺失仲裁，因此在需要使用見證伺服器來維護仲裁之前，它最多可處理三個 Voter 的失敗。而且，如果發生影響到目前見證伺服器的失敗 (例如，由於硬體失敗而遺失見證伺服器)，則可以使用 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd297934\(v=exchg.150\)) Cmdlet 來設定新的見證伺服器和見證目錄 (只要您有仲裁)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果見證伺服器遺失其儲存裝置，或者如果某人變更了見證目錄或共用權限，您還可以使用 <strong>Set-DatabaseAvailabilityGroup</strong> Cmdlet 在原始位置設定見證伺服器和見證目錄。</td>
</tr>
</tbody>
</table>


## 見證伺服器位置的考量

DAG 的見證伺服器位置取決於您的業務需求與您的組織使用的選項。Exchange 2013包含新的 DAG 設定選項不建議或可能無法在舊版的Exchange的支援。這些選項包括使用第三個位置，例如第三個資料中心、 分公司或Microsoft Azure虛擬網路。

下表列出對於不同部署案例的一般見證伺服器位置建議。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>部署案例</th>
<th>建議</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在單一資料中心內部署單一 DAG</p></td>
<td><p>將見證伺服器放在和 DAG 成員一樣的資料中心內</p></td>
</tr>
<tr class="even">
<td><p>跨兩個資料中心來部署單一 DAG；沒有其他可用位置</p></td>
<td><p>若要啟用自動資料中心容錯移轉Microsoft Azure虛擬網路上找出見證伺服器或</p>
<p>將見證伺服器放在主要資料中心內</p></td>
</tr>
<tr class="odd">
<td><p>在單一資料中心內部署多個 DAG</p></td>
<td><p>將見證伺服器放在和 DAG 成員一樣的資料中心內。其他選項包括：</p>
<ul>
<li><p>對多個 DAG 使用同一個見證伺服器</p></li>
<li><p>使用 DAG 成員作為其他 DAG 的見證伺服器</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>跨兩個資料中心來部署多個 DAG</p></td>
<td><p>若要啟用自動資料中心容錯移轉Microsoft Azure虛擬網路上找出見證伺服器或</p>
<p>將見證伺服器放在對每個 DAG 而言都是主要資料中心的資料中心內。其他選項包括：</p>
<ul>
<li><p>對多個 DAG 使用同一個見證伺服器</p></li>
<li><p>使用 DAG 成員作為其他 DAG 的見證伺服器</p>
<p></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>跨三個以上的資料中心部署單一或多個 DAG</p></td>
<td><p>在此組態中，見證伺服器應放在您要讓大多數仲裁投票存在於的資料中心內。</p></td>
</tr>
</tbody>
</table>


當 DAG 已部署跨兩個資料中心時， Exchange 2013中新的組態選項是主控見證伺服器使用第三個位置。如果您的組織有具有隔離影響在其中部署 DAG，兩個資料中心的網路失敗的網路基礎結構的第三個位置然後您可以部署中的第三個位置的 DAG 的見證伺服器進而設定您DAG 和能力自動容錯移轉資料庫至回應 datacenter 層級的失敗事件中的其他資料中心。如果您的組織只會有兩個實體位置，您可以使用第三個位置為 Microsoft Azure 虛擬網路放置在見證伺服器。

## 在 DAG 建立期間指定見證伺服器和見證目錄

建立 DAG 時，您必須提供 DAG 的名稱。您也可以選擇性地指定見證伺服器與見證目錄。

建立 DAG 時，可使用以下的選項與行為組合：

  - 您可以只指定 DAG 的名稱，並讓 **\[見證伺服器\]** 與 **\[見證目錄\]** 欄位保留空白。在此情況中，精靈會在本機 Active Directory 站台中搜尋未安裝 Mailbox 伺服器的 Client Access 伺服器，並且自動在該伺服器上建立預設目錄 (%SystemDrive%:\\DAGFileShareWitnesses\\\<*DAGFQDN*\>) 與預設共用 (\<*DAGFQDN*\>)，並使用該 Client Access 伺服器作為見證伺服器。例如，假設有個見證伺服器 CAS3，其作業系統是安裝在磁碟 C 上。contoso.com 網域中名為 DAG1 的 DAG 會使用預設見證目錄 C:\\DAGFileShareWitnesses\\DAG1.contoso.com，該目錄會分享為 \\\\CAS3\\DAG1.contoso.com。

  - 您可以指定 DAG 的名稱、您要使用的見證伺服器、以及您要在見證伺服器上建立並共用的目錄。

  - 您可以指定 DAG 的名稱和要使用的見證伺服器，然後將 **\[見證目錄\]** 欄位保留空白。在此情況下，此精靈會在指定的見證伺服器上建立預設目錄。

  - 您可以指定 DAG 的名稱、將 **\[見證伺服器\]** 欄位保留空白，並指定您要在見證伺服器上建立及共用的目錄。在此情況下，此精靈會搜尋未安裝信箱伺服器的用戶端存取伺服器，然後自動在該伺服器上建立指定的 DAG 並加以共用，並以該用戶端存取伺服器作為見證伺服器。

形成 DAG 時，其最初會使用「節點多數」仲裁模型。當新增第二個 Mailbox Server 到 DAG 時，仲裁會自動變更為「節點和檔案共用多數」仲裁模型。發生此變更時，DAG 的叢集會開始使用見證伺服器以維護仲裁。如果見證目錄不存在，Exchange 會自動建立及共用該目錄，並為 DAG 的 CNO 電腦帳戶佈建具有完整控制權限的共用。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不支援使用為分散式檔案系統 (DFS) 名稱空間一部分的檔案分享。</td>
</tr>
</tbody>
</table>


如果建立 DAG 之前已在見證伺服器上啟用 Windows 防火牆，可能會封鎖 DAG 的建立。Exchange 使用 Windows Management Instrumentation (WMI) 在見證伺服器上建立目錄及檔案共用。如果 Windows 防火牆已在見證伺服器上啟用，且沒有為 WMI 設定任何防火牆例外狀況，則 **New-DatabaseAvailabilityGroup** Cmdlet 會因錯誤而失敗。如果您指定見證伺服器，但未指定見證目錄，則會收到下列錯誤訊息。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>工作無法在伺服器 &lt;<em>Server Name</em>&gt; 上建立預設的見證目錄。請手動指定見證目錄。</p></td>
</tr>
</tbody>
</table>


如果您指定見證伺服器和見證目錄，則會收到下列警告訊息。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>無法存取見證伺服器 '<em>ServerName</em>' 上的檔案共用。在修正此問題之前，資料庫可用性群組可能會更容易失敗。請使用 Set-DatabaseAvailabilityGroup 指令程式來重試該作業。錯誤：找不到網路路徑。</p></td>
</tr>
</tbody>
</table>


如果是在建立 DAG 之後但在新增伺服器之前，於見證伺服器上啟用 Windows 防火牆，則可能會無法新增或移除 DAG 成員。如果 Windows 防火牆已在見證伺服器上啟用，且沒有為 WMI 設定任何防火牆例外狀況，則 **Add-DatabaseAvailabilityGroupServer** Cmdlet 會顯示下列警告訊息。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>無法在見證伺服器 <em>'ServerName'</em> 上建立檔案共用見證目錄 'C:\DAGFileShareWitnesses\DAG_FQDN'。在修正此問題之前，資料庫可用性群組可能會更容易失敗。請使用 Set-DatabaseAvailabilityGroup 指令程式來重試該作業。錯誤：伺服器 <em>'ServerName'</em> 發生 WMI 例外狀況：RPC 伺服器無法使用。(例外來自 HRESULT：0x800706BA)</p></td>
</tr>
</tbody>
</table>


若要解決先前的錯誤和警告，請執行下列其中一項動作：

  - 在見證伺服器上手動建立見證目錄與共用，並將目錄與共用的 DAG 完全控制指派給 CNO。

  - 在 Windows 防火牆中啟用 WMI 例外狀況。

  - 停用 Windows 防火牆。

回到頁首

## DAG 成員資格

建立 DAG 後，您可以使用 EAC 中的管理資料庫可用性群組精靈，或是在命令介面中使用 **Add-DatabaseAvailabilityGroupServer** 或 **Remove-DatabaseAvailabilityGroupServer** 命令程式在 DAG 上新增伺服器或從 DAG 移除伺服器。如需有關如何管理 DAG 成員資格的詳細步驟，請參閱[管理資料庫可用性群組成員資格](manage-database-availability-group-membership-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每個屬於 DAG 成員的 Mailbox Server 也都會是 DAG 所使用之基礎叢集中的節點。因此，在任何時間，Mailbox Server 只可以是一個 DAG 的成員。</td>
</tr>
</tbody>
</table>


如果新增到 DAG 的 Mailbox Server 未安裝容錯移轉叢集元件，則會使用新增伺服器 (例如，**Add-DatabaseAvailabilityGroupServer** 指令程式或「管理資料庫可用性群組」精靈) 的方法來安裝容錯移轉叢集功能。

當第一個 Mailbox Server 新增到 DAG 時，會發生下列情況：

  - 安裝 Windows 容錯移轉叢集元件 (如果尚未安裝)。

  - 使用 DAG 的名稱建立容錯移轉叢集。此容錯移轉叢集僅供 DAG 使用，而且該叢集必須供 DAG 專用。不支援使用該叢集供所有其他目的之用。

  - 在預設的電腦容器中建立 CNO。

  - DAG 名稱和 IP 位址在網域名稱系統 (DNS) 中登錄為主機 (A) 記錄。

  - 將伺服器新增到 Active Directory 中的 DAG 物件。

  - 以新增之伺服器上裝載的資料庫資訊更新叢集資料庫。

在大型或多網站環境中，特別是將 DAG 擴充到多個 Active Directory 站台的環境時，必須等待包含第一個 DAG 成員之 DAG 物件的 Active Directory 複寫完成。如果沒有在您的整個環境中複寫此 Active Directory 物件，則新增第二個伺服器可能會導致為 DAG 建立新的叢集 (和新的 CNO)。這是因為從正在新增之第二個成員的觀點，DAG 物件看起來是空的，因而導致 **Add-DatabaseAvailabilityGroupServer** Cmdlet 為 DAG 建立叢集和 CNO，即使這些物件已經存在也一樣。若要確認已複寫包含第一個 DAG 伺服器的 DAG 物件，請在正在新增的第二個伺服器上使用 **Get-DatabaseAvailabilityGroup** Cmdlet，確定您所新增的第一個伺服器已列為 DAG 的成員。

當第二個和後續伺服器新增到 DAG 時，會發生下列情況：

  - 將伺服器加入 DAG 的 Windows 容錯移轉叢集。

  - 自動調整仲裁模型：
    
      - 在含奇數成員的 DAG 中使用「節點多數」仲裁模型。
    
      - 在含偶數成員的 DAG 中使用「節點和檔案共用多數」仲裁模型。

  - 在需要時由 Exchange 自動建立見證目錄和共用。

  - 將伺服器新增到 Active Directory 中的 DAG 物件。

  - 使用裝載資料庫的相關資訊更新叢集資料庫。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>仲裁模型變更應該會自動發生。不過，如果仲裁模型未自動變更為正確模型，則可以執行只包含 <em>Identity</em> 參數的 <strong>Set-DatabaseAvailabilityGroup</strong> 指令程式來修正 DAG 的仲裁設定。</td>
</tr>
</tbody>
</table>


## 預先接移 DAG 的叢集名稱物件

CNO 是在 Active Directory 中建立，且與叢集之名稱資源關聯的電腦帳戶。叢集的名稱資源會繫結至 CNO，CNO 是已啟用 Kerberos 功能的物件，用來當作叢集的識別碼並提供叢集的安全性內容。當新增第一個成員至 DAG 時，會執行 DAG 之基礎叢集和該叢集之 CNO 的形成。第一個伺服器新增至 DAG 時，遠端 PowerShell 會在新增時聯絡 Mailbox 伺服器上的 Microsoft Exchange 複寫服務。Microsoft Exchange 複寫服務會安裝容錯移轉叢集功能 (如果尚未安裝)，並開始叢集建立程序。Microsoft Exchange 複寫服務會在 LOCAL SYSTEM 安全性內容下執行，且叢集建立就是在這個內容下執行。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您的 DAG 成員正執行 Windows Server 2012，您必須在新增第一個伺服器到 DAG 之前先預先接移 CNO。如果您的 DAG 成員執行的是 Windows Server 2012 R2，而且您建立沒有叢集管理存取點的 DAG，則不會建立 CNO，而且您不需要建立 DAG 的 CNO。</td>
</tr>
</tbody>
</table>


在電腦帳戶建立受到限制的環境中，或者電腦帳戶是在預設電腦容器以外的容器中建立時，您可以預先設置並佈建 CNO。您可以為 CNO 建立和停用電腦帳戶，然後執行下列其中一項動作：

  - 指派電腦帳戶的完全控制權給您新增至 DAG 的第一個信箱伺服器的電腦帳戶。

  - 將電腦帳戶的完全控制指派給 Exchange 受信任子系統 USG.

將電腦帳戶的完全控制指派給要新增至 DAG 之第一個信箱伺服器的電腦帳戶，可確保 LOCAL SYSTEM 安全性內容能夠管理預先設置的電腦帳戶。可以改用將電腦帳戶的完全控制指派給 Exchange 受信任子系統 USG，因為 Exchange 受信任子系統 USG 包含網域中所有 Exchange Server 的電腦帳戶。

如需如何為 DAG 預先設置及佈建 CNO 的詳細步驟，請參閱[針對資料庫可用性群組預先接移叢集名稱物件](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)。

## 從 DAG 移除伺服器

藉由使用 EAC 內的管理資料庫可用性群組精靈，或是在命令介面中使用 **Remove-DatabaseAvailabilityGroupServer**，就可從 DAG 移除 Mailbox 伺服器。在將 Mailbox Server 從 DAG 移除之前，必須先從伺服器移除所有複寫的信箱資料庫。如果您嘗試從 DAG 移除含有複寫信箱資料庫的郵件伺服器，該工作會失敗。

在某些情況下，您必須先從 DAG 移除郵件伺服器，才能執行某些作業。這些情況包括：

  - **執行伺服器復原作業**   如果遺失了 DAG 之成員的郵件伺服器，或者是失敗和無法恢復且需要更換，您可以使用 **Setup /m:RecoverServer** 參數執行伺服器復原作業。不過，您必須先使用含 *ConfigurationOnly* 參數的 [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-tw/library/dd297956\(v=exchg.150\)) Cmdlet 將伺服器從 DAG 移除，才能執行復原作業。

  - **移除資料庫可用性群組**   在某些情況下，您可能需要移除 DAG (例如，當停用協力廠商複寫模式時)。如果您需要移除 DAG，必須先從 DAG 移除所有伺服器。如果您嘗試移除包含任何成員的 DAG，工作會失敗。

回到頁首

## 設定 DAG 內容

在將伺服器新增到 DAG 之後，您可以使用 EAC 或命令介面來設定 DAG 的內容，包括由 DAG 使用的見證伺服器和見證目錄，以及指派給 DAG 的 IP 位址。

可設定的內容包括：

  - **見證伺服器**   您要裝載檔案共用見證之檔案共用的伺服器名稱。我們建議您指定 Client Access 伺服器作為見證伺服器。這可讓系統自動配置、保全以及使用分享 (如有需要) 並且讓訊息管理員知曉見證伺服器的可用性。

  - **見證目錄**   用於儲存檔案共用見證資料的目錄名稱。系統會自動在指定的見證伺服器上建立此目錄。

  - **資料庫可用性群組 IP 位址**   除非 DAG 成員執行的是 Windows Server 2012 R2，而且您是建立沒有 IP 位址的 DAG，否則必須將一或多個 IP 位址指派給 DAG。否則，可以使用手動指派的靜態 IP 位址來設定 DAG 的 IP 位址，或者使用組織中的 DHCP 伺服器自動指派給 DAG。

此命令介面讓您配置 EAC 中不可用的屬性 (例如 DAG IP 位址、網路加密與壓縮設定、網路探索、複寫使用的 TCP 連接埠以及替代見證伺服器與見證目錄設定) 以及啟用 \[資料中心啟動協調\] 模式。

如需如何設定 DAG 內容的詳細步驟，請參閱[設定資料庫可用性群組內容](configure-database-availability-group-properties-exchange-2013-help.md)。

## DAG 網路加密

Dag 支援加密的使用利用Windows Server作業系統的加密功能。Dag 使用Exchange伺服器之間的 Kerberos 驗證。Microsoft Kerberos 安全性支援提供者 (SSP) EncryptMessage 和 DecryptMessage Api 控點加密的 DAG 網路流量。Microsoft Kerberos SSP 支援多個加密演算法。（如完整清單，請參閱區段 3.1.5.2，"加密類型 」 的[Kerberos 通訊協定 Extensions](https://go.microsoft.com/fwlink/p/?linkid=179131)。）Kerberos 驗證信號交換會選取清單中支援的最強加密通訊協定： 通常進階加密標準 (AES) 256 位元，可能會與 SHA-1 雜湊式訊息驗證碼 (HMAC) 來維護的完整性資料。如需詳細資訊，請參閱[HMAC](https://en.wikipedia.org/wiki/hmac)。

網路加密是 DAG 的內容，而不是 DAG 網路。您可以在命令介面中使用 **Set-DatabaseAvailabilityGroup** Cmdlet 來設定 DAG 網路加密。以下表格中顯示 DAG 網路通訊可能的加密設定。

### DAG 網路通訊加密設定

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>已停用</p></td>
<td><p>不使用網路加密。</p></td>
</tr>
<tr class="even">
<td><p>已啟用</p></td>
<td><p>在所有 DAG 網路上使用網路加密進行複寫及植入。</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>在不同子網路間進行複寫時，在 DAG 網路上使用網路加密。這是預設設定。</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>僅植入時才在所有 DAG 網路上使用網路加密。</p></td>
</tr>
</tbody>
</table>


## DAG 網路壓縮

Dag 支援內建壓縮。啟用壓縮時，DAG 網路通訊使用 XPRESS，這是 Microsoft 實作的 LZ77 演算法。如需詳細資訊，請參閱[說明上平凹演算法](http://www.zlib.net/feldspar.html) and 3.1.4.11.1.2.1 ＞ 一節的[線路格式通訊協定規格](https://go.microsoft.com/fwlink/p/?linkid=179133)的"LZ77 壓縮演算法"。這是同一類型的壓縮特別是用於許多 Microsoft 通訊協定、 Microsoft Outlook和Exchange之間的 MAPI RPC 壓縮。

與網路加密一樣，網路壓縮也是 DAG 的內容，而不是 DAG 網路。您可以在命令介面中使用 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd297934\(v=exchg.150\)) 指令程式設定 DAG 網路壓縮。以下表格中顯示 DAG 網路通訊可能的壓縮設定。

### DAG 網路通訊的壓縮設定

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>已停用</p></td>
<td><p>不使用網路壓縮。</p></td>
</tr>
<tr class="even">
<td><p>已啟用</p></td>
<td><p>在所有 DAG 網路上使用網路壓縮進行複寫及植入。</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>在不同子網路間進行複寫時，在 DAG 網路上使用網路壓縮。這是預設設定。</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>僅植入時才在所有 DAG 網路上使用網路壓縮。</p></td>
</tr>
</tbody>
</table>


回到頁首

## DAG 網路

DAG 網路是用於複寫流量或 MAPI 流量的一或多個子網路的集合。每個 DAG 包含一個 MAPI 網路的最大值和零或多個複寫網路。

## 單一網路介面卡組態

在單一網路介面卡設定，位於相同網路用於 MAPI 及複寫流量。若要降低複雜度，單一網路介面卡是Exchange伺服器的建議的組態因此 MAPI 及複寫流量具有相同的網路上的 \[確定\]。

## 雙網路介面卡組態

一般而言，您只需要使用雙重網路介面卡增加的網路流量其中有可能會滲透單一網路介面卡。

在雙網路介面卡組態中，有一個網路通常為專用複寫流量和其他網路主要用於 MAPI 流量。您也可以新增至每個 DAG 成員的網路介面卡並將其他 DAG 網路設定為複寫網路。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用多個複寫網路時，無法指定網路使用的優先順序。Exchange 會從複寫網路的群組隨機選取複寫網路，以便用於記錄傳送。</td>
</tr>
</tbody>
</table>


在 Exchange 2010 中，有許多情況必須手動配置 DAG 網路。根據在 Exchange 2013 中的預設，系統會自動配置 DAG 網路。建立或修改 DAG 網路之前，您必須先執行下列指令啟用手動 DAG 網路控制：

    Set-DatabaseAvailabilityGroup <DAGName> -ManualDagNetworkConfiguration $true

啟用手動 DAG 網路配置之後，您可以在命令介面中使用 **New-DatabaseAvailabilityGroupNetwork** 命令程式以建立 DAG 網路。如需如何建立 DAG 網路的詳細步驟，請參閱[建立資料庫可用性群組網路](create-a-database-availability-group-network-exchange-2013-help.md)。

您可以在命令介面中使用 **Set-DatabaseAvailabilityGroupNetwork** 指令程式來設定 DAG 網路內容。如需如何設定 DAG 網路內容的詳細步驟，請參閱[設定資料庫可用性群組網路內容](configure-database-availability-group-network-properties-exchange-2013-help.md)。每個 DAG 網路需要的設定和選擇性的參數為：

  - **網路名稱**   DAG 網路的唯一名稱，最多 128 個字元。

  - **網路描述**   DAG 網路的選用描述，最多 256 個字元。

  - **網路子網路**   使用 *IP 位址/位元遮罩*格式 (例如，網際網路通訊協定第 4 版 (IPv4) 子網路為 192.168.1.0/24；網際網路通訊協定第 6 版 (IPv6) 子網路為 2001:DB8:0:C000::/64) 輸入的一或多個子網路。

  - **啟用複寫**   在 EAC 中，選取核取方塊以讓 DAG 網路專門負責複寫流量與阻擋 MAPI 流量。清除核取方塊避免使用 DAG 網路進行複寫並且允許 MAPI 流量。在命令介面中，使用 [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-tw/library/dd298008\(v=exchg.150\)) 指令程式中的 *ReplicationEnabled* 參數啟用和停用複寫。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>停用 MAPI 網路上的複寫不能保證系統不會使用該 MAPI 網路進行複寫。當所有設定的複寫網路為離線、失敗或無法使用，並且只剩下 MAPI 網路 (已設定為停用複寫) 時，系統會使用 MAPI 網路進行複寫。</td>
</tr>
</tbody>
</table>


系統所建立的初始 DAG 網路 (例如，MapiDagNetwork 和 ReplicationDagNetwork01) 是以由叢集服務列舉之子網路為基礎。每個 DAG 成員必須具備相同數目的網路介面卡，而且每個網路介面卡必須具備唯一子網路上的 IPv4 位址 (或者也可以選擇性地具備 IPv6 位址)。多個 DAG 成員可以具備相同子網路上的 IPv4 位址，但是特定 DAG 成員中的每個網路介面卡與 IP 網址配對必須是唯一的子網路。此外，只有 MAPI 網路使用的介面卡應該設定預設閘道。複寫網路不應該設定預設閘道。

例如，假設有一個 DAG1 是兩個成員的 DAG，其中，每個成員具有兩個網路介面卡 (一個為 MAPI 網路專用，另一個供複寫網路使用)。範例 IP 位址組態設定如下表所示。

### 範例網路介面卡設定

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器-網路介面卡</th>
<th>IP 位址/子網路遮罩</th>
<th>預設閘道</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1-MAPI</p></td>
<td><p>192.168.1.15/24</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX1-複寫</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>EX2-MAPI</p></td>
<td><p>192.168.1.16</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX2-複寫</p></td>
<td><p>10.0.0.16</p></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


在下列組態中，DAG 中設定了兩個子網路：192.168.1.0 和 10.0.0.0。當 EX1 和 EX2 新增至 DAG 時，將會列舉兩個子網路並建立兩個 DAG 網路：MapiDagNetwork (192.168.1.0) 與 ReplicationDagNetwork01 (10.0.0.0)。這些網路將如下表所示來設定。

### 單一子網路 DAG 的列舉 DAG 網路設定

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>子網路</th>
<th>介面</th>
<th>MAPI 存取已啟用</th>
<th>複寫已啟用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.1.0/24</p></td>
<td><p>EX1 (192.168.1.15)</p>
<p>EX2 (192.168.1.16)</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p></td>
<td><p>EX1 (10.0.0.15)</p>
<p>EX2 (10.0.0.16)</p></td>
<td><p>False</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


若要將 ReplicationDagNetwork01 設定為專用複寫網路，請執行下列命令停用 MapiDagNetwork 的複寫功能。

    Set-DatabaseAvailabilityGroupNetwork -Identity DAG1\MapiDagNetwork -ReplicationEnabled:$false

停用 MapiDagNetwork 的複寫之後，Microsoft Exchange 複寫服務會使用 ReplicationDagNetwork01 進行連續複寫。如果 ReplicationDagNetwork01 發生失敗，Microsoft Exchange 複寫服務會恢復使用 MapiDagNetwork 進行連續複寫。這是系統特別執行的工作，以維持高可用性。

## DAG 網路與多重子網路部署

在先前的範例中，雖然 DAG 使用兩個不同的子網路 (192.168.1.0 和 10.0.0.0)，但 DAG 是視為單一子網路的 DAG，因為每個成員都使用相同子網路以形成 MAPI 網路。當 DAG 成員使用不同子網路作為 MAPI 網路時，該 DAG 稱為*多重子網路 DAG*。在多子網路 DAG 中，正確的子網路會自動與每個 DAG 網路相關聯。

例如，假設有一個 DAG2 是兩個成員的 DAG，其中，每個成員具有兩個網路介面卡 (一個為 MAPI 網路專用，另一個供複寫網路使用)，而且每個 DAG 成員都位於個別 Active Directory 站台中，其 MAPI 網路在不同子網路上。範例 IP 位址組態設定如下表所示。

### 多重子網路 DAG 的範例網路介面卡設定

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器-網路介面卡</th>
<th>IP 位址/子網路遮罩</th>
<th>預設閘道</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1-MAPI</p></td>
<td><p>192.168.0.15/24</p></td>
<td><p>192.168.0.1</p></td>
</tr>
<tr class="even">
<td><p>EX1-複寫</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>EX2-MAPI</p></td>
<td><p>192.168.1.15</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX2-複寫</p></td>
<td><p>10.0.1.15</p></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


在下列組態中，DAG 中設定了四個子網路：192.168.0.0、192.168.1.0、10.0.0.0 和 10.0.1.0。當 EX1 和 EX2 新增至 DAG 時，將會列舉四個子網路，但僅建立兩個 DAG 網路：MapiDagNetwork (192.168.0.0, 192.168.1.0) 與 ReplicationDagNetwork01 (10.0.0.0, 10.0.1.0)。這些網路將如下表所示來設定。

### 多重子網路 DAG 的列舉 DAG 網路設定

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>子網路</th>
<th>介面</th>
<th>MAPI 存取已啟用</th>
<th>複寫已啟用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.0.0/24</p>
<p>192.168.1.0/24</p></td>
<td><p>EX1 (192.168.0.15)</p>
<p>EX2 (192.168.1.15)</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p>
<p>10.0.1.0/24</p></td>
<td><p>EX1 (10.0.0.15)</p>
<p>EX2 (10.0.1.15)</p></td>
<td><p>False</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


## DAG 網路和 iSCSI 網路

依預設，DAG 會對所有偵測到和已設定為由基礎叢集使用的網路執行探索。這包括由於為一或多個 DAG 成員使用 iSCSI 儲存而在使用中的任何 Internet SCSI (iSCSI) 網路。最佳作法是，iSCSI 儲存應該使用專用的網路和網路介面卡。這些網路不應由 DAG 或其叢集進行管理，或用作 DAG 網路 (MAPI 或複寫)。相反地，這些網路應該手動停用不讓 DAG 使用，這樣它們才能專用於 iSCSI 儲存流量。若要停用 iSCSI 網路以防止受偵測並作為 DAG 網路使用，請使用 [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-tw/library/dd298008\(v=exchg.150\)) 指令程式將 DAG 設定為忽略任何目前偵測到的 iSCSI 網路，如以下範例所示：

    Set-DatabaseAvailabilityGroupNetwork -Identity DAG2\DAGNetwork02 -ReplicationEnabled:$false -IgnoreNetwork:$true

此指令同時將停用叢集使用網路。雖然 iSCSI 網路將繼續顯示為 DAG 網路，執行上述指令後，不會為 MAPI 或複寫流量使用網路。

回到頁首

## 設定 DAG 成員

DAG 成員的信箱伺服器擁有某些專用於高可用性的內容，這些內容應該依下列各節所述來設定：

  - Automatic database mount dial

  - Database copy automatic activation policy

  - Maximum active databases

## 自動資料庫裝載撥號

*AutoDatabaseMountDial* 參數會指定資料庫容錯移轉之後的自動資料庫裝載行為。您可以使用 [Set-MailboxServer](https://technet.microsoft.com/zh-tw/library/aa998651\(v=exchg.150\)) Cmdlet 將 *AutoDatabaseMountDial* 參數設定為下列值其中之一：

  - `BestAvailability`   如果指定此值，複製佇列長度少於或等於 12 時，資料庫會在容錯移轉後立即自動裝載。複製佇列長度是需複寫的被動複本所辨識的記錄個數。如果複製佇列長度超過 12，資料庫將不會自動裝載。當複製佇列長度小於或等於 12 時，Exchange 會嘗試將剩餘的記錄複寫至被動複本，並裝載資料庫。

  - `GoodAvailability`   如果指定此值，資料庫將在複製佇列長度小於或等於 6 時，在容錯移轉之後立即自動裝載。複製佇列長度是需複寫的被動複本所辨識的記錄個數。如果複製佇列長度超過 6，資料庫將不會自動裝載。當複製佇列長度小於或等於 6 時，Exchange 會嘗試將剩餘的記錄複寫至被動複本，並裝載資料庫。

  - `Lossless`   如果指定此值，在將主動複本上產生的所有記錄複製到被動複本之前，資料庫將不會自動裝載。此設定也會使 Active Manager 最佳副本選擇演算法根據資料庫副本的啟動喜好設定值 (而非其副本佇列長度) 來排序啟動的可能候選項目。

預設值為 `GoodAvailability`。如果指定 `BestAvailability` 或 `GoodAvailability`，而且主動複本上的所有記錄無法複製到已啟動的被動複本，您可能會遺失部分信箱資料。但是，安全網功能 (已根據預設啟用) 會藉由重新提交位於安全網佇列中的訊息，有助防止資料遺失。

## 範例：設定自動資料庫裝載撥號

下列範例會以 `GoodAvailability` 的 *AutoDatabaseMountDial* 設定來設定信箱伺服器。

    Set-MailboxServer -Identity EX1 -AutoDatabaseMountDial GoodAvailability

## 資料庫副本自動啟動原則

*DatabaseCopyAutoActivationPolicy* 參數會指定所選取的信箱伺服器上信箱資料庫複本可用的自動啟用類型。您可以使用 [Set-MailboxServer](https://technet.microsoft.com/zh-tw/library/aa998651\(v=exchg.150\)) Cmdlet 將 *DatabaseCopyAutoActivationPolicy* 參數設定為下列值其中之一：

  - `Blocked`   如果指定此值，則無法在所選取的信箱伺服器上自動啟動資料庫。

  - `IntrasiteOnly`   如果指定此值，則可在同一個 Active Directory 站台的伺服器上啟動資料庫副本。這可防止跨站台的容錯移轉或啟用。此屬性用於內送郵件資料庫複本 (例如作為主動複本的被動複本)。無法在此信箱伺服器上啟動已在另一個 Active Directory 站台上啟動資料庫複本的資料庫。

  - `Unrestricted`   如果指定此值，對於在所選取的信箱伺服器上啟動信箱資料庫複本，並沒有任何特殊限制。

## 範例：設定資料庫副本自動啟動原則

下列範例會以 `Blocked` 的 *DatabaseCopyAutoActivationPolicy* 設定來設定信箱伺服器。

    Set-MailboxServer -Identity EX1 -DatabaseCopyAutoActivationPolicy Blocked

## 使用中資料庫上限

*MaximumActiveDatabases* 參數 (也搭配 [Set-MailboxServer](https://technet.microsoft.com/zh-tw/library/aa998651\(v=exchg.150\)) Cmdlet 使用) 會指定可裝載於信箱伺服器上的資料庫數量。透過確保個別信箱伺服器不會超載，您可以設定信箱伺服器以符合您的部署需求。

*MaximumActiveDatabases* 參數是以整數數值來設定。到達數目上限時，如果發生容錯移轉或轉換，將不會啟動伺服器上的資料庫複本。如果已在伺服器上使用複本，該伺服器將不允許裝載資料庫。

## 範例：設定使用中資料庫上限

下列範例會將信箱伺服器設定為支援上限 20 個使用中資料庫。

    Set-MailboxServer -Identity EX1 -MaximumActiveDatabases 20

回到頁首

## 在 DAG 成員上執行維護

在 DAG 成員上執行任何類型的軟體或硬體維護之前，應該先讓此 DAG 成員進入維護模式。這包括將所有使用中資料庫移出伺服器，並防止使用中資料庫移到此伺服器。這也包括確保此伺服器上所有可能的重要 DAG 支援功能 (例如，Primary Active Manager (PAM) 角色) 都移至其他伺服器，並防止它們移回此伺服器。具體而言，您應該執行下列工作：

1.  為了開始清空傳輸佇列的程序，請執行 `Set-ServerComponentState <ServerName> -Component HubTransport -State Draining -Requester Maintenance`

2.  若要啟動清空傳輸佇列，請執行 `Restart-Service MSExchangeTransport`

3.  為了開始清空所有整合通訊呼叫的程序，請執行 `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Draining -Requester Maintenance`

4.  為了將本機佇列中的待傳遞郵件重新導向至 Target 參數指定的 Mailbox 伺服器，請執行 `Redirect-Message -Server <ServerName> -Target <MailboxServerFQDN>`

5.  為了暫停叢集節點以防止該節點成為及變成 PAM，請執行 `Suspend-ClusterNode <ServerName>`

6.  為了將目前裝載於 DAG 成員上的所有使用中資料庫移至其他 DAG 成員，請執行 `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $True`

7.  為了防止伺服器裝載使用中資料庫副本，請執行 `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Blocked`

8.  為了使伺服器進入維護模式，請執行 `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Inactive -Requester Maintenance`

為了確認伺服器已準備好供人在其上進行維護，請執行下列工作：

1.  為了確認伺服器是否已進入維護模式，請執行 `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`

2.  為了確認伺服器是否未裝載任何使用中資料庫副本，請執行 `Get-MailboxServer <ServerName> | ft DatabaseCopy* -Autosize`

3.  為了確認節點是否已暫停，請執行 `Get-ClusterNode <ServerName> | fl`

4.  為了確認是否已清空所有傳輸佇列，請執行 `Get-Queue`

在維護完成且 DAG 成員已準備好恢復服務之後，您可以執行下列工作來將 DAG 成員移出維護模式，並使其回到生產模式：

  - 指定伺服器退出維護模式，請執行 `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Maintenance`

  - 為了允許伺服器接受整合通訊呼叫，請執行 `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Active -Requester Maintenance`

  - 為了在叢集中恢復節點，並啟用伺服器的完整叢集功能，請執行 `Resume-ClusterNode <ServerName>`

  - 為了允許資料庫在伺服器上變為使用中狀態，請執行 `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $False`

  - 為了移除自動啟動封鎖，請執行 `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Unrestricted`

  - 若要啟用傳輸佇列，並允許伺服器接受與處理郵件，請執行 `Set-ServerComponentState <ServerName> -Component HubTransport -State Active -Requester Maintenance`

  - 若要繼續傳輸活動，請執行 `Restart-Service MSExchangeTransport`

若要驗證伺服器已準備好用於實際執行，請執行下列工作：

1.  若要驗證伺服器不是處於維護模式，請執行 `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`

如果您是安裝 Exchange 更新，而更新程序失敗，則可以讓一些伺服器元件處於非使用中狀態，這類伺服器元件將會顯示於上面 Get-ServerComponentState 指令程式的輸出中。若要解決此問題，請執行下列命令：

  - `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component Monitoring -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component RecoveryActionsEnabled -State Active -Requester Functional`

回到頁首

## 關閉 DAG 成員

Exchange 2013 高可用性解決方案已整合 Windows 關機程序。如果系統管理員或應用程式在具有裝載資料庫 (已複寫到一或多個 DAG 成員) 的 DAG 中初始化 Windows 伺服器的關機程序，系統會先嘗試啟動裝載資料庫的另一個副本，然後再允許完成關機程序。

不過，這項新行為不保證在伺服器上關閉的所有資料庫都將啟動 `lossless`。因此，最佳作法是在關閉屬於 DAG 成員的伺服器之前，先執行伺服器轉換。

回到頁首

## 在 DAG 成員上安裝更新

在 DAG 的成員伺服器上安裝 Microsoft Exchange Server 2013 更新，這是一種比較直接的程序。當您在 DAG 的成員伺服器上安裝更新時，有幾個服務會在安裝期間停止，包括所有的 Exchange 服務和叢集服務。對 DAG 成員套用更新的一般程序如下：

1.  使用前文所述步驟，使 DAG 成員進入維護模式。

2.  安裝更新。

3.  使用前文所述步驟，將 DAG 成員移出維護模式，並使其回到生產模式。

4.  (選用) 使用 RedistributeActiveDatabases.ps1 指令碼以重新平衡整個 DAG 的使用中資料庫副本。

您可以從 [Microsoft 下載中心](http://www.microsoft.com/downloads)下載 Exchange 2013 的最新更新。

回到頁首


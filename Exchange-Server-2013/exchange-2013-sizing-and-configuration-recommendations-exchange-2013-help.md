---
title: 'Exchange 2013 大小和設定建議: Exchange 2013 Help'
TOCTitle: Exchange 2013 大小和設定建議
ms:assetid: 4c4ba2fc-014a-46fb-949a-2dabba92c4a5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn879075(v=EXCHG.150)
ms:contentKeyID: 63763696
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 大小和設定建議

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-03-27_

Exchange 2013 會比舊版的 Exchange 系統資源的多個要求。 透過正確大小調整您的 Exchange 2013 基礎結構，並再進行一些建議採用的設定 Exchange 相關元件的基礎結構內，您可以配置以最佳方式執行部署的基礎。

## Exchange 2013 調整大小

正確地調整大小 Exchange 2013 為其中一種最有效地不要讓效能問題。Exchange 2013 伺服器角色需求計算器是[可用的以下是](https://go.microsoft.com/fwlink/p/?linkid=523844)。最新版本 6.6，但建議您回來定期的更新。若要正確使用此 \[小算盤\]，您必須請洽詢[Exchange 2013 伺服器角色需求計算器](https://go.microsoft.com/fwlink/p/?linkid=386677)及[調整大小 Exchange 2013 部署](https://go.microsoft.com/fwlink/p/?linkid=301990)部落格文章中的指引。

請務必開頭前購買及部署您的硬體; calculator （英文）您應該先決定您根據 \[小算盤\] 結果的整體資源需求。 您可以使用 \[小算盤\] 將輸入組織的需求並使用結果如何擴充您的硬體上的指引。 \[小算盤\] 不會告訴您多少部伺服器使用，但它可讓您評估在指定的一組伺服器上的 Exchange 工作負載的影響。您應該實驗查看它如何影響效能，以符合硬體的不同設定與業務需求專屬於您的環境。

若要簡化部署並取得利用硬體，Exchange 產品群組建議多重角色伺服器。 如有多個用戶端存取伺服器可用來處理要求期間失敗案例使用多重角色伺服器提供您更好的用戶端存取伺服器 (CAS) 層級的可用性。 Exchange 2013 主要的設計考量是使用 「 小 」 商品類型伺服器 （而不向上擴充方式向外延展）。 設計與測試已完成包含最多個二十個處理器核心，具有最多可有 96 gb 的 RAM 的兩個通訊端電腦。若您的硬體大於此，則應考慮其他選項，例如使用其他需求的硬體和購買 Exchange 2013 環境的較小的伺服器或虛擬化。

最好是建立更多伺服器 （向外擴展） 比其會將資源新增至現有的且更大的伺服器 （擴充）。 向外擴展可讓您的環境以利用 Exchange 2013 中的內建的高可用性功能。了解這種設定建議為何，，請檢閱詳細[的慣用架構](https://go.microsoft.com/fwlink/p/?linkid=523782)及[可用性的站台恢復能力影響](https://go.microsoft.com/fwlink/p/?linkid=523845)的文章。

\[小算盤\] 不會將列入帳戶協力廠商產品執行於 Exchange 伺服器或與 Exchange （包括內部開發的應用程式），這表示您必須確定在您調整這些帳戶互動的產品。 Lync Server，例如與協力廠商 Exchange Web 服務 (EWS) 應用程式與 ActiveSync 裝置可以所有大幅增加每位使用者的 CPU 需求。 您可以參考如需如何它將會影響 Exchange 的協力廠商產品文件。 建議您將 for Exchange 建立效能比較基準實作協力廠商解決方案之前。

## 建議的效能設定

下列效能最佳化 Exchange 2013 環境的建議。

## 開啟/關閉

設定以允許作業系統 (OS) 來管理 power BIOS。

在作業系統中，開啟高效能電源計劃。

## 處理

關閉超執行緒實體的 Exchange 伺服器上。如果虛擬化、 啟用超執行緒可能是在實體伺服器上，但每個虛擬伺服器應該只可配置所需的數量的虛擬 Cpu （請勿超額配置虛擬 Cpu），而且只會使用調整大小計算的實體處理器核心數目。

在 Exchange Server 2013 Service Pack 1 或更新版本，您可以啟用 SSL 卸載若要協助減少用戶端存取伺服器 CPU 使用率但複雜的 SSL 卸載設定可能不是值得好處。

## .NET Framework


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
<th>Exchange 版本</th>
<th>.NET Framework 4.7.1</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU19</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU16 - CU18</p></td>
<td><p></p></td>
<td><p> X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


如果您無法安裝.net 4.5.2，請參閱 Microsoft 知識庫文章 2995145"[的效能問題或當您連線至 Exchange Server 2013 的 Windows Server 中執行的延遲](https://go.microsoft.com/fwlink/p/?linkid=524159)。 」 該文章中的修正的開發方法根據對存放區工作者處理序記憶體使用率內部發現項目。 套用這些修正程式，會降低整體記憶體使用率的所有受管理的程序 （包括存放區工作者處理序），並將會降低.NET 廢棄項目集合中所花費的整體 CPU 時間。

## Hotfix

Exchange 效能小組 」 所建議安裝所有的下列相關效能 hotfix。

  - [有可用的改善叢集中恢復在 Windows Server 2012 中的更新](https://go.microsoft.com/fwlink/p/?linkid=524088)

  - [建議使用 hotfix 和 Windows Server 2012 型容錯移轉叢集的更新](https://go.microsoft.com/fwlink/p/?linkid=524089)

  - [建議使用 hotfix 和 Windows Server 2012 R2 型容錯移轉叢集的更新](https://go.microsoft.com/fwlink/p/?linkid=524090)

  - [Windows 8 或 Windows Server 2012 電腦具有多核心處理器上不正確的 RSS 處理器工作分派](https://go.microsoft.com/fwlink/p/?linkid=324140)

  - [效能問題或當您連線至執行 Windows Server 中的 Exchange Server 2013 的延遲](https://go.microsoft.com/fwlink/p/?linkid=312962)

  - [Outlook 連線問題時 SSLOffloading"True"在 Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=524091)

  - [Exchange Server 2013 的資料庫容錯移轉後的 outlook 長伺服器連線](https://go.microsoft.com/fwlink/p/?linkid=524092)

  - [在 Outlook Web App 時 Lync 整合 Exchange Server 2013 的效能低落](https://go.microsoft.com/fwlink/p/?linkid=524093)

  - [EMS 採用長時間執行 Exchange Server 2013 累計更新 5 環境中的第一個命令](https://go.microsoft.com/fwlink/p/?linkid=524094)

  - [如果 Exchange Server 2013 中啟用 IPv6 的郵件路由的延遲](https://go.microsoft.com/fwlink/p/?linkid=524095)

  - [取決於 WIndows Server 2008 R2 SP1 中的 Microsoft LDAP 用戶端應用程式所造成高 CPU 使用量](https://go.microsoft.com/fwlink/p/?linkid=530287)

  - [CPU 使用率太高當您使用 RPC over HTTP 通訊協定 Windows 8.1 或 Windows Server 2012 R2 中](https://go.microsoft.com/fwlink/p/?linkid=619127)

## 網路功能

與 Exchange 2013 的單一網路介面卡，建議如下不再需要分割 MAPI 和複寫網路。 如需詳細資訊，請參閱[網路需求](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)。

使用預設值 SNP 卸載設定其中可用，並確定已啟用 \[RSS （設定 Windows Server 2012 和較新版本的預設值）。 RSS 有助於規模上的 CPU 使用率，特別是 10GbE。

確認 OS 未關閉儲存 power 之網路卡。

維持最新的 NIC 驅動程式。 請洽詢您的廠商相關的驅動程式更新的每月為基礎。

## Internet Information Services (IIS)

在安裝期間，Exchange 會針對 IIS 修改某些的連線限制。沒有進一步調整 IIS 的建議。

避免盡可能自訂項目。對 web.config 或登錄機碼的任何變更可以覆寫 Exchange 累計更新或 Windows 更新。

## 儲存裝置

Exchange 2013 儲存的準則都可以在[Exchange 2013 儲存裝置組態選項](exchange-2013-storage-configuration-options-exchange-2013-help.md)。

## 虛擬化

請檢閱[硬體虛擬的需求](exchange-2013-virtualization-exchange-2013-help.md)。另外，Exchange 不是非統一記憶體存取 (NUMA 注意) 附註。因此，建議使用的硬體製造商預設 NUMA 設定。

## Active Directory

監視目錄伺服器的效能，因為 Active Directory 查詢直接影響您的 Exchange 部署。

關鍵效能計數器來測量 Active Directory 狀況聲明的 LDAP 搜尋時間。 監視網域控制站上的 CPU。 網域控制站上的 CPU 問題會轉譯為瀏覽 Exchange 伺服器上的效能。

執行內建 「 Active Directory 診斷 」 位於下方"的資料收集器集合工具"為了隔離網域控制站的效能問題的原因的效能監視器\] 中的網域控制站上。

規劃足夠的 RAM，可讓快取的網域控制站上完整的 AD 資料庫檔案。

建議您部署的每一個用來處理作用中的負載 （依據在 64 位元通用類別目錄核心） 的 8 信箱核心 1 Active Directory 通用類別目錄核心。

## 負載平衡

所有用戶端存取伺服器應該會收到大約相同數目的傳入連線。

所有通訊協定、 Exchange 2013 不需要指定的 Client Access server 和負載平衡器之間的工作階段親和性。

硬體或軟體負載平衡器應該用來管理用戶端存取伺服器的所有內送的流量。使用"循環，"中的每個撥入的連線會前往下目標伺服器中循環\] 清單中，例如方法或"最少連線、"中的負載平衡器將每個新的連接傳送至該次具有最少的建立的連線的伺服器可以判斷選取範圍的目標伺服器。 會詳細說明這些方法進一步投入[負載平衡](load-balancing-exchange-2013-help.md)。您也應該考量下列：

  - 循環配置資源有存留期長 （例如 RPC/HTTP) 連線的速度過慢交集的問題。為新的電腦所上線，達到負載平衡的不同目標電腦所服務的連線所需的時間很長的時間才能收斂。

  - 含有"最低連線"方法、 留意很可能的用戶端存取伺服器會成為超載並沒有回應或修補維護期間用戶端存取伺服器中斷。 在 Exchange 效能的內容，驗證是昂貴的作業。

由於數目限制與 Windows 網路負載平衡 (NLB) 在 Exchange 2013 環境的詳細[負載平衡](load-balancing-exchange-2013-help.md)，我們不建議使用 Windows NLB。

## 使用者與資料庫通訊群組

維護每個資料庫和每部伺服器的使用中資料庫的使用者完善平衡通訊群組。 平均分散資料庫磁碟空間耗用量以及大量使用者平衡跨所有資料庫。

您必須設定您的使用者群檔以瞭解他們與 Exchange （裝置、 Outlook 和 OWA） 和這些互動會導致效能的觀點而言影響的互動。 請參閱計算器部落格的區段 2 的較佳的了解如何將每個使用者 Exchange 使用方式的設定檔。

設定資料庫副本啟動喜好設定和"MaximumPreferredActiveDatabases"（每個伺服器） 設定容錯移轉或轉換期間維持達到負載平衡。

RedistributeActiveDatabases.ps1 指令碼會重新使用中資料庫平衡整個 DAG 節點中。

請考慮強制執行嚴格的項目計數限制符合 Office 365。您可以使用 Set-mailbox 指令程式與[信箱資料夾限制](https://go.microsoft.com/fwlink/p/?linkid=398779)所提供的資訊來這麼做。

## 分頁檔

如果您使用多個 32 GB 的 RAM，設定之 32778 MB 的分頁檔大小上限。

分頁檔不應該主控於相同的磁碟機 Exchange 資料庫檔案或資料庫記錄檔。

請務必您使用固定的大小分頁檔並不允許 Windows 管理大小。增加分頁檔案可能會是非常效能大量工作和 Exchange 處於壓力下時可能造成問題。

如果您需要以取得完整的核心傾印，然後使用 Microsoft 知識庫文章 969028、[如何產生核心或 Windows Server 2008 和 Windows Server 2008 R2 中完成的記憶體傾印檔案](https://go.microsoft.com/fwlink/p/?linkid=524044)、 專用的傾印檔案。

## Outlook 模式

建議快取的模式。 若要了解使用快取的模式的優點，請參閱[選擇快取 Exchange 模式還是線上模式為 Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=524045)。

請務必注意 server 增益集和 Outlook 第三方增益集可能會影響效能。 當您使用線上模式、 用戶端可預期一些效能問題從協力廠商增益集、 高的項目計數、 受限制的檢視存取信箱，其他因素之間的使用者人數。 舊版用戶端可以體驗更多影響高的項目計數和效能比 Outlook 2013 將。

如果組織有 Outlook 在線上模式中設定的主要原因的安全性考量，請考慮改用 BitLocker。

Outlook 2013 提供新的 「 同步處理滑桿 」 功能減少下載時間和 OST 檔案的大小。 請參閱[Configure Cached Exchange Mode in Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=390456)如需詳細資訊。

檢查每月的 Outlook 用戶端更新您的環境中支援的。

## 第三方軟體

最佳作法是解除安裝或停用第三方軟體時疑難排解 Exchange 效能。 下列清單包含第三方軟體的 Microsoft 技術支援人員有最常呈現影響 Exchange 2013 效能的類型。

  - 防毒解決方案

  - 入侵防護軟體

  - 備份軟體

  - 稽核檔案和使用者的軟體

  - 封存的解決方案


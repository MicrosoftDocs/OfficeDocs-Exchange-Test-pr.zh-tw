---
title: 'Edge Transport Server 規劃: Exchange 2013 Help'
TOCTitle: Edge Transport Server 規劃
ms:assetid: 3d34de82-58a5-4b30-9978-7d330102eb92
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn641596(v=EXCHG.150)
ms:contentKeyID: 61543913
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge Transport Server 規劃

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

Exchange Service Pack 1 中重新引進了 Edge Transport server role。Edge Transport 可為 Exchange 組織提供更好的反垃圾郵件保護。Edge Transport Server 也會將原則套用在組織與組織間傳輸的郵件。此伺服器角色是部署在周邊網路中及 Active Directory 樹系之外。Edge Transport Server 無法像 Client Access 或 Mailbox Server 一樣直接存取 Active Directory 取得組態和收件者資訊。Edge Transport Server 是使用 Active Directory 輕量型目錄服務 (AD LDS) 在本機儲存組態和收件者資訊。

您可以將 Edge Transport Server 新增至現有 Exchange 2013 組織。安裝 Edge Transport Server 時，您不需要執行任何其他 Active Directory 準備步驟。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要新增邊際傳輸至現有Exchange 2010或Exchange 2007組織，您將需要特定彙總套件更新舊版伺服器上安裝之前先安裝Exchange 2013邊際傳輸。如需詳細資訊，請參閱<a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 系統需求</a>。</td>
</tr>
</tbody>
</table>


計劃部署 Edge Transport Server 之前，您應考量下列問題：

  - **伺服器容量** 規劃伺服器容量包括規劃執行 Edge Transport Server 的效能監視。效能監視可協助您了解伺服器的工作負荷量。此資訊可判斷目前硬體組態的容量。

  - **傳輸功能** Edge Transport Server 可在網路邊界上提供反垃圾郵件保護。在規劃過程中，您應該決定在 Edge Transport Server 上要啟用的反垃圾郵件功能及如何設定。

  - **安全性** Edge Transport server role 是為了將受攻擊面縮到最小而設計。因此，必須正確保護和管理伺服器的實體存取和網路存取。規劃安全性可協助您確定只允許授權的伺服器和授權的使用者建立 IP 連線。如需詳細資訊，請參閱[部署安全性檢查清單](deployment-security-checklist-exchange-2013-help.md)。
    
    建議的作法是將 Edge Transport Server 放置在周邊網路上。若要確定伺服器可以傳送及接收電子郵件，以及可以從 Microsoft Exchange EdgeSync 服務接收收件者和組態資料更新，您必須允許透過下表所列的通訊埠進行通訊。
    
    ### Edge Transport Server 的通訊埠設定
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>網路介面</th>
    <th>開啟通訊埠</th>
    <th>通訊協定</th>
    <th>附註</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>從網際網路輸入及輸出至網際網路</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>需要此通訊埠才能進行進出網際網路的郵件流程。</p></td>
    </tr>
    <tr class="even">
    <td><p>從內部網路輸入及輸出至內部網路</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>需要此通訊埠才能進行進出 Exchange 組織的郵件流程。</p></td>
    </tr>
    <tr class="odd">
    <td><p>僅限本機</p></td>
    <td><p>50389/TCP</p></td>
    <td><p>LDAP</p></td>
    <td><p>此通訊埠是用於與 AD LDS 進行本機連線。</p></td>
    </tr>
    <tr class="even">
    <td><p>從內部網路輸入</p></td>
    <td><p>50636/TCP</p></td>
    <td><p>安全 LDAP</p></td>
    <td><p>需要此通訊埠才能進行 EdgeSync 同步處理。</p></td>
    </tr>
    <tr class="odd">
    <td><p>從內部網路輸入</p></td>
    <td><p>3389/TCP</p></td>
    <td><p>RDP</p></td>
    <td><p>開啟此通訊埠是選擇性的。藉由讓您使用遠端桌面連線管理 Edge Transport Server，在從內部網路內管理 Edge Transport Server 方面提供更大的彈性。</p></td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Edge Transport server role 使用非標準的 LDAP 通訊埠。本主題中指定的通訊埠為安裝 Edge Transport server role 時設定的 LDAP 通訊埠。</td>
    </tr>
    </tbody>
    </table>


  - **EdgeSync**  建議的部署程序是建立 Edge 訂閱讓 Exchange 組織來訂閱 Edge Transport Server。建立 Edge 訂閱之後，收件者和組態資料會從 Active Directory 複寫到 AD LDS。您可以讓 Active Directory 站台訂閱 Edge Transport Server。之後，該站台上在 Mailbox Server 上執行的 MicrosoftExchange EdgeSync 服務會定期從 Active Directory 同步處理資料來更新 AD LDS。Edge 訂閱程序會自動提供讓郵件透過 Edge Transport Server 從 Exchange 組織傳送到網際網路所需的傳送連接器。如果您在 Edge Transport Server 上使用收件者查閱或安全清單彙總功能，則必須讓組織訂閱 Edge Transport Server。

## 設定 Edge Transport server role 的 DNS 設定

Edge Transport Server 是部署在 Exchange 組織外的周邊網路作為獨立伺服器，或作為周邊網路 Active Directory 網域的成員。您需要先針對 Edge Transport server role 手動設定正確的 DNS 尾碼，再安裝 Exchange 2013。若未設定 DNS 尾碼，則安裝會失敗。

因為 Edge Transport Server 部署在周邊網路上，所以其網路介面連線到多個網路區段。每個網路區段都具有唯一 IP 組態。連接至外部或公用網路區段的網路介面，應設定為使用公用 DNS 伺服器進行名稱解析。這可讓伺服器將 SMTP 網域名稱解析為 MX 資源記錄，並將郵件路由傳送至網際網路。

連線至內部或私人網路區段的網路介面應該設定為使用 DNS 伺服器以解析組織中 Mailbox Server 的名稱，或應該有可用的主機檔案。Edge Transport Server 與 Mailbox Server 必須能使用 DNS 主機解析以找出對方位置。

若要由 Edge Transport Server 啟用 Mailbox Server 名稱解析，請使用下列其中一種方法：

  - 在 Edge Transport Server 內部網路介面卡上設定之 DNS 伺服器的正向查閱區中，手動建立 Mailbox Server 的資源記錄。

  - 編輯 Edge Transport Server 上的主機檔案，以納入 Mailbox Server 的主機記錄。主機檔案為本機文字檔案，其格式與 4.3 Berkeley Software Distribution (BSD) UNIX /etc/hosts 檔案相同。此檔案會對應主機名稱至 IP 位址，而該檔案儲存在 \\%Systemroot%\\System32\\Drivers\\Etc 資料夾中。

若要由 Mailbox Server 啟用 Edge Transport Server 名稱解析，請使用下列其中一種方法：

  - 在 Mailbox Server 上設定之 DNS 伺服器的正向查閱區中，手動建立 Edge Transport Server 的資源記錄。

  - 若要納入 Edge Transport Server 的主機記錄，請編輯位於所訂閱 Active Directory 站台中之 Mailbox Server 上的主機檔案。

請遵循下列步驟，以設定 Edge Transport Server 的 DNS 設定：

1.  驗證每個網路介面卡的 DNS 伺服器設定的網路區段是否正確。

2.  使用下列步驟設定 Edge Transport Server 名稱的 DNS 尾碼：
    
    1.  開啟 \[控制台\]，然後選擇 \[系統內容\]。
    
    2.  選擇 \[電腦名稱\] 索引標籤。
    
    3.  選擇 \[變更\]。
    
    4.  在 \[電腦名稱變更\] 頁面上，按一下 \[其他\]。
    
    5.  在 \[這部電腦的主要 DNS 尾碼\] 欄位中，輸入 Edge Transport Server 的 DNS 網域名稱和尾碼。
    
    安裝 Edge Transport server role 後，便無法變更此名稱。

## 覆寫 DNS 設定

您可能需要覆寫 Exchange 伺服器上的預設 DNS 設定，才能正確地路由傳送和傳遞郵件。若要這樣做，請修改 Transport Server 內容的 \[內部 DNS 查閱\] 和 \[外部 DNS 查閱\] 設定。這些設定會覆寫網路面介卡的設定以路由電子郵件訊息。


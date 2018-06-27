---
title: '啟用遠端移動 MRS Proxy 端點: Exchange 2013 Help'
TOCTitle: 啟用遠端移動 MRS Proxy 端點
ms:assetid: 9840f712-127e-4c2d-bfe5-1b35cdb2a31b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn155787(v=EXCHG.150)
ms:contentKeyID: 54652596
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用遠端移動 MRS Proxy 端點

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-07-02_

信箱複寫服務 Proxy (MRS Proxy) 有助於跨樹系信箱移動及遠端移動遷移內部Exchange組織與Exchange Online之間。在Exchange 2013、 MRS Proxy 隨附於信箱伺服器角色 （也稱為*信箱伺服器*）。在跨樹系及遠端移動遷移期間用戶端存取伺服器會做為傳入的移動要求之信箱伺服器的 proxy。預設為停用用戶端存取伺服器接受這些要求的能力。若要允許用戶端存取伺服器接受傳入的移動要求，您必須啟用 MRS Proxy 端點。

啟用哪部 Client Access Server 上的 MRS Proxy 端點，視信箱移動的類型和方向而定。

  - **跨樹系企業移動**  針對跨樹系移動起始從目標環境 （稱為*提取*移動類型），您必須啟用 MRS Proxy 端點來源環境中的用戶端存取伺服器上。針對跨樹系移動起始從來源環境 （稱為*推入*移動類型），您必須啟用 MRS Proxy 端點目標環境中的用戶端存取伺服器上。

  - **內部部署 Exchange 組織和 Exchange Online 之間的遠端移動遷移**   針對 Onboarding 和 Offboarding 遠端移動遷移，您都需啟用內部部署組織中 Client Access Server 上的 MRS Proxy 端點。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用 EAC 來移動信箱、 跨樹系移動及 onboarding 遠端移動遷移會提取移動類型由於要求是從目標環境。Offboarding 遠端移動遷移的推入移動類型由於要求是從來源環境。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘每部伺服器。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「Exchange Web 服務權限」一節。

  - 如果您已部署 Exchange 組織中部署多個用戶端存取伺服器，您應該啟用 MRS Proxy 端點上每個。如果您新增額外的用戶端存取伺服器，請務必讓新的伺服器上的 MRS Proxy 端點。跨樹系移動及遠端移動遷移如果所有的用戶端存取伺服器上未啟用 MRS Proxy 端點可能會失敗。

  - 如果您不執行跨樹系移動或遠端移動遷移，請將 MRS Proxy 端點維持停用，以減少組織的攻擊面。

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

## 使用 EAC 啟用 MRS Proxy 端點

1.  在 EAC 中，瀏覽至 **\[收件者\]** \> **\[伺服器\]** \> **\[虛擬目錄\]**。

2.  在 \[**選取伺服器**\] 下拉式清單中，選取您要啟用 MRS Proxy 端點的用戶端存取伺服器的名稱。或選取組織中的所有用戶端存取伺服器上顯示的虛擬目錄的**所有伺服器**。

3.  在 **\[選取類型\]** 下拉式清單中，選取 **\[EWS\]** 以顯示選定伺服器的 Exchange Web 服務 (EWS) 虛擬目錄。

4.  在虛擬目錄清單中，按一下您要設定之 Client Access Server 的 **\[EWS (預設網站)\]**，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

5.  在 \[ **EWS （預設網站）**內容\] 頁面上選取 \[**啟用 MRS Proxy 端點**\] 核取方塊，和 \[**儲存**。

## 使用命令介面啟用 MRS Proxy 端點

下列命令可啟用名為 EXCH-SRV-01 之 Client Access Server 上的 MRS Proxy 端點。

    Set-WebServicesVirtualDirectory -Identity "EXCH-SRV-01\EWS (Default Web Site)" -MRSProxyEnabled $true

下列命令可啟用您 Exchange 組織中所有 Client Access Server 上的 MRS Proxy 端點。

    Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -MRSProxyEnabled $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>先前所述，應在組織中每個用戶端存取伺服器上啟用 MRS Proxy 端點。執行上述命令之後將新的用戶端存取伺服器新增至您的組織。</td>
</tr>
</tbody>
</table>


## 如何才能了解這是否正常運作？

若要確認您是否已成功啟用 MRS Proxy 端點，請執行下列其中一項操作：

1.  在 EAC 中，瀏覽至 **\[收件者\]** \> **\[伺服器\]** \> **\[虛擬目錄\]**。

2.  在虛擬目錄清單中，按一下 **\[EWS (預設網站)\]** 並在詳細資料窗格中確認已啟用 MRS Proxy 端點。
    
    或者，您可以按一下 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")檢視**EWS （預設網站）**的 \[內容\] 頁面並確認已選取 \[**啟用 MRS Proxy 端點**\] 核取方塊。

或

在命令介面中執行下列命令：

    Get-WebServicesVirtualDirectory | FL Identity,MRSProxyEnabled

確認 *MRSProxyEnabled* 參數已設為 `True`。

若要確認已啟用 MRS Proxy 端點的另一種方式是使用**Test-MigrationServerAvailability**指令程式來測試通訊是 offboarding Exchange Online信箱移轉至內部部署組織、 內部部署組織中的伺服器或是與遠端伺服器主控您要移動的信箱的能力。如需詳細資訊，請參閱[Test-MigrationServerAvailability](https://technet.microsoft.com/zh-tw/library/jj219169\(v=exchg.150\))。

下列範例測試能否連線至 corp.contoso.com 樹系中的伺服器。

    $Credentials = Get-Credential

    Test-MigrationServerAvailability -ExchangeRemoteMove -Autodiscover -EmailAddress administrator@corp.contoso.com -Credentials $Credentials

若想成功執行此命令，必須啟用 MRS Proxy 端點。


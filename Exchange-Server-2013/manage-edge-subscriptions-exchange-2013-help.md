---
title: '管理 Edge 訂閱: Exchange 2013 Help'
TOCTitle: 管理 Edge 訂閱
ms:assetid: 27de4104-fb8e-4eab-9ad2-a64f81a4fb69
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996865(v=EXCHG.150)
ms:contentKeyID: 61180449
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理 Edge 訂閱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2018-04-16_

本主題提供各種 Edge 訂閱管理工作的詳細資訊。

**目錄**

Subscribe an Edge Transport server

Remove an Edge subscription

Resubscribe an Edge Transport Server

Add or remove a Mailbox Server

Run EdgeSync manually

Verify EdgeSync results

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「EdgeSync」項目和「Edge Transport Server」一節。

  - 您必須將 Edge 伺服器訂閱至面向網際網路的 Active Directory 站台。如需詳細資訊，請參閱[透過訂閱的 Edge Transport Server 設定網際網路郵件流程](configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 訂閱 Edge Transport Server

您可以將一或多部 Edge Transport Server 訂閱至單一 Active Directory 站台。如果您在周邊網路中部署其他 Edge Transport Server，並讓已有 Edge 訂閱存在的相同 Active Directory 站台訂閱這些伺服器，則會執行下列動作：

  - 在 Active Directory 中建立新的 Edge 訂閱物件。

  - 為 Active Directory 站台中的每部信箱伺服器建立不同的 ESRA 帳戶。這些帳戶會複寫至 Active Directory 輕量型目錄服務 (AD LDS)，並在與新伺服器的同步處理期間，由 EdgeSync 同步處理程序使用。

  - 連至網際網路的自動傳送連接器來源伺服器清單會加入新的 Edge 訂閱。訂閱的 Edge Transport Server 之間會對提交至連接器進行處理的郵件進行載入平衡。

  - 自動建立從 Edge Transport Server 到 Exchange 組織的輸入傳送連接器。

  - 啟動對 Edge Transport Server 的 EdgeSync 同步處理。

## 移除 Edge 訂閱

在某些情況下，您可能會想從 Exchange 組織中移除 Edge 訂閱，或同時從 Exchange 組織和 Edge Transport Server 中移除。如果您後續還要將 Edge Transport Server 重新訂閱至 Exchange 組織，請不要從 Edge Transport Server 中移除 Edge 訂閱。當您從 Edge Transport Server 移除 Edge 訂閱時，會從 AD LDS 刪除所有複寫的資料。如果您有大量收件者資料，這可能需要很長的時間。

若要完全移除 Edge 訂閱，您必須在要移除的 Edge Transport Server 上執行此程序，並在訂閱此 Edge Transport Server 之 Active Directory 站台中的 Exchange 2013 信箱伺服器上執行此程序。

移除 Edge 訂閱之後，就會停止從 AD LDS 進行資訊同步處理。所有儲存在 AD LDS 中的帳戶都會被移除，並且會從所有傳送連接器的來源伺服器清單中移除 Edge Transport Server。您無法再使用依賴 Active Directory 資料的 Edge Transport Server 功能。

1.  若要從 Edge Transport Server 中移除 Edge 訂閱，請使用下列語法。
    
        Remove-EdgeSubscription <EdgeTransportServerIdentity>
    
    例如，若要在名為 Edge01 的 Edge Transport Server 上移除 Edge 訂閱，請執行下列命令。
    
        Remove-EdgeSubscription Edge01

2.  若要從信箱伺服器中移除 Edge 訂閱，請使用下列語法。
    
        Remove-EdgeSubscription <MailboxServerIdentity>
    
    例如，若要在名為 Mailbox01 的信箱伺服器上移除 Edge 訂閱，執行下列命令。
    
        Remove-EdgeSubscription Mailbox01

在下列情況下，您將必須移除 Edge 訂閱：

  - 您不想再讓 Edge Transport Server 加入 EdgeSync 同步處理中。您必須同時從 Edge Transport Server 和 Exchange 組織中移除 Edge 訂閱。

  - 解除委任 Edge Transport Server。在此情況下，您只需從 Exchange 組織中移除 Edge 訂閱。如果您解除安裝電腦上的 Edge Transport server role，則 AD LDS 執行個體與儲存在 AD LDS 中的所有 Active Directory 資料也會一併移除。

  - 您想要變更 Edge 訂閱的 Active Directory 站台關聯。您只需從 Exchange 組織中移除 Edge 訂閱。從 Exchange 組織中移除 Edge 訂閱後，您可以將 Edge Transport Server 重新訂閱至不同的 Active Directory 站台。

從 Exchange 組織中移除 Edge 訂閱時：

  - 會停止 Active Directory 與 AD LDS 的資訊同步處理。

  - 會同時從 Active Directory 與 AD LDS 中移除 ESRA 帳戶。

  - 會從任何傳送連接器的 *SourceTransportServers* 內容中移除 Edge Transport Server。

  - 會從 AD LDS 中移除從 Edge Transport Server 至 Exchange 組織的自動輸入傳送連接器。

從 Edge Transport Server 中移除 Edge 訂閱時：

  - 您無法再使用依賴 Active Directory 資料的 Edge Transport Server 功能。

  - 從 AD LDS 移除複寫的資料。

  - 在建立 Edge 訂閱時停用的工作會重新啟用，以供本機組態使用。

## 重新訂閱 Edge Transport Server

有時候，您必須將 Edge Transport Server 重新訂閱至 Active Directory 站台。重新建立 Edge 訂閱時會產生新的認證，且您必須遵循完整的 Edge 訂閱程序。在下列情況下，您將必須重新訂閱 Edge Transport Server：

  - 您在已訂閱的 Active Directory 站台中新增了信箱伺服器，且您想讓新的信箱伺服器加入 EdgeSync 同步處理中。

  - 您在建立 Edge 訂閱之後套用了 Edge Transport Server 的授權金鑰。建立 Edge 訂閱時，會擷取 Edge Transport Server 的授權資訊。必須先在 Edge Transport Server 上套用授權金鑰，然後再將其訂閱至 Exchange 組織，已訂閱的 Edge Transport Server 才會呈現為已授權的狀態。若在執行 Edge 訂閱程序後才在 Edge Transport Server 上套用授權金鑰，則不會在 Exchange 組織中更新授權資訊，而且您必須重新訂閱 Edge Transport Server。

  - ESRA 認證遭到洩漏。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要重新訂閱 Edge Transport Server，請在 Edge Transport Server 上匯出新的 Edge 訂閱檔案，然後在信箱伺服器上匯入 XML 檔案。您必須將 Edge Transport Server 重新訂閱至原本訂閱的同一個 Active Directory 站台。您不需要先移除原始 Edge 訂閱；重新訂閱程序會覆寫現有的 Edge 訂閱。</td>
    </tr>
    </tbody>
    </table>


## 新增或移除信箱伺服器

如果您將信箱伺服器新增至已訂閱 Edge Transport Server 的 Active Directory 站台，新的信箱伺服器並不會自動加入 EdgeSync 同步處理中。若要讓新部署的信箱伺服器加入 EdgeSync 同步處理中，您必須將每部 Edge Transport Server 重新訂閱至 Active Directory 站台。

從訂閱 Edge Transport Server 的 Active Directory 站台中移除信箱伺服器，並不會對 EdgeSync 同步處理造成影響，除非這部信箱伺服器是該站台中唯一的信箱伺服器。如果您從訂閱 Edge Transport Server 的 Active Directory 站台中移除所有信箱伺服器，則會孤立該站台訂閱的 Edge Transport Server。

## 手動執行 EdgeSync

如果您對 Active Directory 中的組態或收件者做了重大變更，並且想立即同步處理這些變更，您可以手動執行 EdgeSync。您可以執行完整同步處理，或僅同步處理上次複寫後所做的變更。

手動 EdgeSync 會重設 EdgeSync 同步處理排程。您執行手動同步處理的時間，將決定何時執行下一次的自動同步處理。

若要以手動方式執行 EdgeSync，請使用下列語法。

    Start-EdgeSynchronization [-Server <MailboxServerIdentity>] [-TargetServer <EdgeTransportServerIdentity> [-ForceFullSync]

下列範例將使用以下選項啟動 EdgeSync：

  - 從名為 Mailbox01 的 Exchange 2013 信箱伺服器起始同步處理。

  - 同步處理所有邊際傳輸伺服器。

  - 僅同步處理自上次複寫後的變更。

<!-- end list -->

    Start-EdgeSynchronization -Server Mailbox01

此範例會使用下列選項啟動 EdgeSync：

  - 從本機信箱伺服器起始同步處理。

  - 僅同步處理名為 Edge03 的 Edge Transport Server。

  - 完整同步處理所有收件者及組態資料。

<!-- end list -->

    Start-EdgeSynchronization -TargetServer Edge03 -ForceFullSync

## 驗證 EdgeSync 結果

您可以使用 **Test-EdgeSynchronization** 指令程式確認 Edge 同步處理是否正常運作。此指令程式會報告已訂閱的 Edge Transport Server 進行同步處理的狀態。

此指令程式的輸出可讓您檢視哪些物件尚未同步處理至 Edge Transport Server。這項工作會將儲存於 Active Directory 中的資料與儲存於 AD LDS 中的資料相比較，並報告資料是否不一致。

您可以在 **Test-EdgeSynchronization** 指令程式上使用 *ExcludeRecipientTest* 參數，以排除收件者資料同步處理的驗證。如果驗證收件者資料是否已同步處理，將會比只驗證組態資料要花費更長的時間。相較於僅驗證組態資料，驗證收件者資料需要更長的處理時間。

## 驗證單一收件者的 EdgeSync 結果

若要驗證單一收件者的 EdgeSync 結果，請在已訂閱的 Active Directory 站台中的信箱伺服器上使用下列語法。

    Test-EdgeSynchronization -VerifyRecipient <emailaddress>

此範例會驗證使用者 kate@contoso.com 的 EdgeSync 結果。

    Test-EdgeSynchronization -VerifyRecipient kate@contoso.com

回到頁首


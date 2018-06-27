---
title: '將 Exchange 2010 系統信箱移至 Exchange 2013: Exchange 2013 Help'
TOCTitle: 將 Exchange 2010 系統信箱移至 Exchange 2013
ms:assetid: a3b03c4e-0bc7-41a2-885c-e9cac37566c8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn249849(v=EXCHG.150)
ms:contentKeyID: 54914981
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將 Exchange 2010 系統信箱移至 Exchange 2013

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

Exchange 2010、 Microsoft Exchange 系統信箱是用來儲存整個組織資料例如系統管理員稽核記錄檔、 中繼資料的 eDiscovery 搜尋和整合通訊的資料，例如功能表仲裁信箱的撥號對應表計劃及自訂問候語。Microsoft Exchange 系統信箱名為**SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}**;顯示名稱是**Microsoft Exchange**。

升級時您現有的Exchange 2010組織至Exchange 2013，您必須Exchange 2013信箱伺服器上將 Microsoft Exchange 系統信箱移至的信箱資料庫。您應將此信箱移動後您已安裝，並確認Exchange 2013。如果您不要將此系統信箱移至Exchange 2013，當Exchange 2010和Exchange 2013共存 Exchange 組織中將會發生下列問題：

  - Exchange 2013 工作未儲存到系統管理員稽核記錄中。執行 **Search-AdminAuditLog** Cmdlet，或嘗試在 EAC 中匯出系統管理員稽核記錄時，您會收到一則錯誤訊息，說明因為系統信箱 SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9} 位於未執行 Exchange 2013 的伺服器上，所以您無法建立系統管理員稽核記錄搜尋。每次執行命令時，事件識別碼為 5000 的 Microsoft Exchange 錯誤也會記錄在 Windows 應用程式記錄中。

  - 您無法執行 eDiscovery 搜尋中Exchange 2013使用 EAC 或命令介面。信箱搜尋可建立及排入佇列，但無法啟動。事件識別碼為 6 的錯誤會記錄在 MsExchange 管理記錄檔，表示**Start-MailboxSearch**指令程式失敗。不過，您可以搜尋使用命令介面與 Exchange 控制台 (ECP) Exchange 2010中的信箱。

您也必須將 Microsoft Exchange 系統信箱移至Exchange 2013一部分升級Exchange 2010Exchange 2013整合通訊。

如需升級至 Exchange 2013 的詳細資訊，請參閱下列主題：

  - [從 Exchange 2010 升級至 Exchange 2013](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)

  - [將 Exchange 2010 UM 升級至 Exchange 2013 UM](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間：20 分鐘。實際的時間可能會因系統信箱的大小而有所不同。

  - [收件者權限](recipients-permissions-exchange-2013-help.md)中的 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「信箱移動與移轉權限」項目。

  - 在 Exchange 2013 中執行下列命令，以取得 Exchange 伺服器和包含組織中系統信箱之信箱資料庫的身分識別和版本。
    
        Get-Mailbox -Arbitration | FL Name,DisplayName,ServerName,Database,AdminDisplayVersion
    
    **AdminDisplayVersion** 內容會指出伺服器執行的 Exchange 的版本。`Version 14.x` 值表示 Exchange 2010；`Version 15.x` 值表示 Exchange 2013。

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

## 使用 EAC 來移動系統信箱

1.  在 EAC 中，移至 **\[收件者\]** \> **\[遷移\]**。

2.  按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，然後按一下 **\[移至不同資料庫\]**。

3.  在 **\[新本機信箱移動\]** 頁面上，按一下 **\[選取您要移動的使用者\]**，然後按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在 **\[選取信箱\]** 頁面上，新增具備下列內容的信箱：
    
      - 顯示名稱為 **\[Microsoft Exchange\]**。
    
      - 信箱的電子郵件地址別名為 **\[SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}\]**。

5.  按一下 \[**確定**\]，然後再按一下 \[**下一步**\]。

6.  在 **\[移動組態\]** 頁面上，輸入遷移批次的名稱，然後按一下 **\[目標資料庫\]** 方塊旁邊的 **\[瀏覽\]**。

7.  在 **\[選取信箱資料庫\]** 頁面上，新增要將系統信箱移到的信箱資料庫。確認您選取的信箱資料庫版本是 \[版本15.x\]，這表示該資料庫位於 Exchange 2013 伺服器上。

8.  按一下 \[**確定**\]，然後再按一下 \[**下一步**\]。

9.  在 **\[啟動批次\]** 頁面上，選取自動啟動並完成遷移要求的選項，然後按一下 **\[新增\]**。

## 使用命令介面來移動系統信箱

首先，在 Exchange 2013 中執行下列命令，以取得組織中所有信箱資料庫的名稱和版本。

    Get-MailboxDatabase -IncludePreExchange2013 | FL Name,Server,AdminDisplayVersion

在識別組織中的信箱資料庫名稱之後，請在 Exchange 2013 中執行下列命令，將 Microsoft Exchange 系統信箱移至位於 Exchange 2013 伺服器上的信箱資料庫。

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | New-MoveRequest -TargetDatabase <name of Exchange 2013 database>

## 如何知道這是否正常運作？

若要確認您已成功將 Microsoft Exchange 系統信箱移至位於 Exchange 2013 伺服器上的信箱資料庫，請在命令介面中執行下列命令。

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | FL Database,ServerName,AdminDisplayVersion

如果 **AdminDisplayVersion** 內容的值為 **\[版本 15.x (組建 xxx.x)\]**，就表示系統信箱確實位於 Exchange 2013 伺服器上的信箱資料庫。

將 Microsoft Exchange 系統信箱移至 Exchange 2013 之後，您將還能夠成功執行下列系統管理工作：

  - 執行 **Search-AdminAuditLog** Cmdlet。

  - 在 EAC 中匯出系統管理員稽核記錄。

  - 使用 Exchange 2013 中的 EAC 或命令介面成功建立並啟動 eDiscovery 搜尋。


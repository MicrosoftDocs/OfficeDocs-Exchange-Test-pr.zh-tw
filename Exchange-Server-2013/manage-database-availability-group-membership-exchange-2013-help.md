---
title: '管理資料庫可用性群組成員資格: Exchange 2013 Help'
TOCTitle: 管理資料庫可用性群組成員資格
ms:assetid: fb2ea15e-96d5-4045-b75b-b0aa5fc60479
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351278(v=EXCHG.150)
ms:contentKeyID: 50474657
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理資料庫可用性群組成員資格

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-08-13_

當您將伺服器新增到資料庫可用性群組 (DAG)，它即可與 DAG 中其他的伺服器搭配使用，以在資料庫、服務器和網路失敗時提供自動的資料庫層級復原功能。當您從 DAG 中移除伺服器後，該伺服器便不再自動受到失敗預防保護。

要尋找與 DAG 相關的其他管理工作嗎？請參閱[管理資料庫可用性群組](managing-database-availability-groups-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：每個伺服器 5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md) 主題中的「資料庫可用性群組」項目。

  - DAG 使用 Windows 容錯移轉叢集 (WFC) 技術。每個屬於 DAG 成員的 Mailbox Server 也都會是 DAG 所使用之基礎叢集中的節點。因此，不論何時，一個信箱伺服器都只能是一個 DAG 的成員。因為 DAG 採用 WFC 技術，因此所有新增至 DAG 的伺服器都必須執行相同的作業系統：Windows Server 2008 R2 Enterprise 或 Datacenter Edition，或者 Windows Server 2012 或 Windows Server 2012 R2 的 Standard 或 Datacenter Edition。

  - 如果您新增的是執行 Windows Server 2012 的信箱伺服器，您必須為 DAG 預先設置叢集名稱物件 (CNO)。如果您新增的是執行 Windows Server 2012 R2 的 Mailbox Server，而且 DAG 沒有管理存取點，則不需要預先接移 CNO，因為沒有管理存取點的 DAG 不會有 CNO。如需詳細步驟，請參閱[針對資料庫可用性群組預先接移叢集名稱物件](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)。

  - 您必須先建立 DAG，之後才能新增成員至 DAG。如需詳細步驟，請參閱[建立資料庫可用性群組](create-a-database-availability-group-exchange-2013-help.md)。

  - 您必須先移除從伺服器複製的所有複製資料庫，才能將資料庫從 DAG 中移除。

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

## 使用 EAC 管理資料庫可用性群組成員資格

1.  在 EAC 中，移至 \[伺服器\] \> \[資料庫可用性群組\]。

2.  選取要設定的 DAG，然後按一下 ![管理 DAG 成員](images/Dd351278.d567ae56-d6cd-4edb-ab67-ad8f7c58f337(EXCHG.150).gif "管理 DAG 成員")。
    
      - 若要新增一或多個信箱伺服器至 DAG，請按一下 ![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，從清單中選取伺服器，依序按一下 \[新增\]、\[確定\]。
    
      - 若要從 DAG 中移除一或多個信箱伺服器，請選取伺服器，然後按一下減號 (-) 圖示。

3.  按一下 \[儲存\] 以儲存變更。

4.  當工作成功完成時，按一下 \[關閉\]。

## 使用命令介面管理資料庫可用性群組成員資格

此範例會新增 DAG DAG1 中的信箱伺服器 MBX1。

    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

此範例會自 DAG DAG1 中移除信箱伺服器 MBX1。執行此命令之前，請確定信箱伺服器上沒有重複的資料庫。

    Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

本範例從 DAG DAG2 移除 MBX4 的 Mailbox Server 之組態設定。MBX4 預計會離線一段時間，以便在離線期間從 DAG 移除其組態，同時與其他仍在線上的 DAG 成員建立仲裁。

    Remove-DatabaseAvailabilityGroupServer -Identity DAG2 -MailboxServer MBX4 -ConfigurationOnly

## 如何知道這是否正常運作？

若要驗證您是否已成功管理 DAG 成員資格，請執行下列其中一項操作：

  - 在 EAC 中，瀏覽至 \[伺服器\] \> \[資料庫可用性群組\]。目前的 DAG 成員資格會顯示在 \[成員伺服器\] 欄中。

  - 在命令介面中，執行下列命令以顯示 DAG 成員資格資訊。
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List Servers

## 相關資訊

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-tw/library/dd298049\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-tw/library/dd297956\(v=exchg.150\))


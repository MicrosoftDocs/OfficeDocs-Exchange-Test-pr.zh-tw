---
title: '將 Exchange 2013 升級至最新的累計或服務套件: Exchange 2013 Help'
TOCTitle: 將 Exchange 2013 升級至最新的累計或服務套件
ms:assetid: 928a4a0b-0082-4d50-a696-bfaf2782f42d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ983803(v=EXCHG.150)
ms:contentKeyID: 52062574
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將 Exchange 2013 升級至最新的累計或服務套件

 

_**適用版本：**Exchange Online, Exchange Server, Exchange Server 2013_

_**上次修改主題的時間：**2015-09-04_

如果您已安裝 Microsoft Exchange Server 2013，則可以將它升級至最新的 Exchange 2013 累計更新或 Service Pack。您可以使用 Exchange 2013 安裝精靈升級您目前的 Exchange 2013 版本。如需最新 Exchange 2013 累計更新或 Service Pack 的詳細資訊，請參閱 [更新 Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md)。若要深入了解 Exchange 2013，請參閱 [Exchange 2013 的新功能](what-s-new-in-exchange-2013-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在您將 Exchange 2013 升級至較新的累計更新或 Service Pack 之後，就無法解除安裝新版本以還原為舊版本。如果您解除安裝新版本，就會從伺服器移除 Exchange。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：60 分鐘

  - 請務必先閱讀版本資訊，然後再安裝 Exchange 2013。如需詳細資訊，請參閱 [Exchange 2013 版本資訊](release-notes-for-exchange-2013-exchange-2013-help.md)。

  - 確定您打算安裝累計更新或 Service Pack 的伺服器都符合系統需求與必要條件。如需詳細資訊，請參閱[Exchange 2013 系統需求](exchange-2013-system-requirements-exchange-2013-help.md)及[Exchange 2013 必要條件](exchange-2013-prerequisites-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在您安裝 Exchange 累計更新 (CU) 後，將會覆寫您在 Exchange XML 應用程式組態檔 (例如 Client Access Server 上的 web.config 檔案，或 Mailbox Server 上的 EdgeTransport.exe.config 檔案) 中任何自訂的個別伺服器設定。請務必儲存此資訊，以便安裝後能輕易地重新設定伺服器。在安裝 Exchange CU 後，您必須重新配置這些設定。</td>
    </tr>
    </tbody>
    </table>


  - 安裝累計更新或 Service Pack 之後，您必須重新啟動電腦，才能對登錄和作業系統進行變更。

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


## 安裝 Exchange 2013 累計更新或 Service Pack

您可使用安裝精靈或透過自動模式安裝 Exchange 2013 的累計更新或 Service Pack。如需特定指示，請參閱下列主題：

  - [使用安裝精靈安裝 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

  - [使用自動模式安裝 Exchange 2013](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)

如果您已在安裝 service pack 或累計更新的電腦為資料庫可用性群組 (DAG) 的成員，請遵循[管理資料庫可用性群組](managing-database-availability-groups-exchange-2013-help.md)主題的[DAG 成員上的執行維護](managing-database-availability-groups-exchange-2013-help.md)\] 區段中的步驟。


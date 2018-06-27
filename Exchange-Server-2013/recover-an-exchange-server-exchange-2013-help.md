---
title: '復原 Exchange Server: Exchange 2013 Help'
TOCTitle: 復原 Exchange Server
ms:assetid: 46e9a1cf-b64c-43c3-a898-6171176da761
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876880(v=EXCHG.150)
ms:contentKeyID: 50473047
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 復原 Exchange Server

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

您可以在 Microsoft Exchange Server 2013 中使用 **Setup /m:RecoverServer** 參數復原遺失的伺服器。執行 Exchange 2013 之電腦的大部分設定都儲存在 Active Directory。*/m:RecoverServer* 參數會使用儲存在 Exchange 中的設定和其他資訊，以相同名稱重建 Active Directory 伺服器。

復原遺失的 Exchange 伺服器通常是藉由使用新的硬體達成。但是，您也可以使用現有的伺服器。

本主題將示範如何復原不是資料庫可用性群組 (DAG) 成員的遺失 Exchange 2013 伺服器。如需復原 DAG 成員伺服器的詳細步驟，請參閱[復原資料庫可用性群組成員伺服器](recover-a-database-availability-group-member-server-exchange-2013-help.md)。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若是 Exchange 並非安裝在預設位置，您必須使用 <em>/TargetDir</em> 參數來指定 Exchange 二進位檔案的位置。若是您不使用 <em>/TargetDir</em> 參數，Exchange 檔案將會安裝至預設的位置 (%programfiles%\Microsoft\Exchange Server\V15)。<br />
若要決定安裝位置，請遵循下列步驟：
<ol>
<li><p>開啟 ADSIEDIT.MSC 或 LDP.EXE。</p></li>
<li><p>瀏覽至下列位置： <strong>CN=ExServerName、CN=Servers、CN=First Administrative Group、CN=Administrative Groups、CN=ExOrg Name、CN=Microsoft Exchange、CN=Services、CN=Configuration、DC=DomainName、CN=Com</strong></p></li>
<li><p>在 Exchange 伺服器物件上按一下滑鼠右鍵，然後按一下 [內容]。</p></li>
<li><p>尋找 <strong>msExchInstallPath</strong> 屬性。此屬性儲存了當前的安裝路徑。</p></li>
</ol></td>
</tr>
</tbody>
</table>


要尋找與備份和還原資料相關的其他管理工作嗎？請參閱[備份、還原和嚴重損壞修復](backup-restore-and-disaster-recovery-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：20 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) 主題中的「Exchange 基礎結構權限」一節。

  - 正在進行復原的伺服器必須與遺失的伺服器執行相同的作業系統。例如，您無法在執行 Windows Server 2012 的伺服器上復原執行 Exchange 2013 和 Windows Server 2008 R2 的伺服器，反之亦然。同樣地，您無法在執行 Windows Server 2012 R2 的伺服器上復原執行 Exchange 2013 和 Windows Server 2012 的伺服器，反之亦然。

  - 裝載資料庫的故障伺服器上的相同磁碟機代號需存在於執行還原的伺服器中。

  - 正在執行復原的伺服器與遺失的伺服器應有相同的效能特徵和硬體組態。

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


## 復原遺失的 Exchange 伺服器

1.  重設遺失的伺服器的電腦帳戶。如需詳細步驟，請參閱[重設電腦帳戶](https://go.microsoft.com/fwlink/p/?linkid=165388)。

2.  安裝正確的作業系統，並且使用遺失伺服器的名稱命名新伺服器。如果正在執行復原的伺服器與遺失的伺服器未使用相同的名稱，復原將不會成功。

3.  將伺服器加入與遺失的伺服器相同的網域。

4.  安裝必要條件和作業系統元件。如需詳細資訊，請參閱 [Exchange 2013 系統需求](exchange-2013-system-requirements-exchange-2013-help.md)與 [Exchange 2013 必要條件](exchange-2013-prerequisites-exchange-2013-help.md)。

5.  登入復原的伺服器，並開啟命令提示字元。

6.  瀏覽至 Exchange 2013 安裝檔案，並執行下列命令。
    
        Setup /m:RecoverServer /IAcceptExchangeServerLicenseTerms

7.  在安裝程式完成之後，以及將復原伺服器放入實際執行環境之前，重新設定先前儲存在伺服器上的任何自訂設定，然後重新啟動伺服器。

## 如何知道這是否正常運作？

成功完成安裝程式會是復原成功的主要指標。若要進一步確認是否已成功復原損毀的伺服器，請執行下列其中一項操作：

  - 開啟 Windows 服務工具 (services.msc)，確認是否已安裝並正在執行 Microsoft Exchange 服務。


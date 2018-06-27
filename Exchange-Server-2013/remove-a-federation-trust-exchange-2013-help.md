---
title: '移除同盟信任: Exchange 2013 Help'
TOCTitle: 移除同盟信任
ms:assetid: dc4d126d-b567-470d-a5d0-e1402bf8f369
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657500(v=EXCHG.150)
ms:contentKeyID: 50474391
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除同盟信任

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-01-04_

同盟信任會建立 Microsoft Exchange 2013組織和Azure Active Directory驗證系統之間的信任關係，並且支援與其他同盟 Exchange 組織共用。移除同盟信任從內部部署 Exchange 組織會停用同盟共用與其他同盟 Exchange 組織與 Office 365 組織連線到組織的混合部署的一部分。您應該謹慎考量組織之前先移除同盟信任的整體的影響。

若欲瞭解更多與同盟信任相關的管理工作，請參閱[同盟程序](federation-procedures-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此 Exchange Server 2013 功能與中國的 21Vianet 所運作的 Office 365 不完全相容，部分功能可能受限。如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解 21Vianet 運作的 Office 365</a>。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的「同盟與憑證」權限項目。

  - 移除同盟信任後，即可從各個同盟網域的公用 DNS 伺服器移除 TXT 記錄。請檢閱從裝載公用 DNS 記錄的組織移除 TXT 記錄的需求。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 使用 EAC 移除同盟信任

1.  在內部部署組織中的 Exchange 2013 伺服器上，瀏覽至 \[組織\] \> \[共用\]。

2.  在 \[同盟信任\] 區段中，按一下 \[刪除\]。

3.  在警告中，按一下 \[是\] 確認您要移除同盟信任。

4.  移除同盟信任後，按一下 \[關閉\]。

## 使用命令介面來移除同盟信任

本範例會移除同盟信任。

    Remove-FederationTrust

如需詳細的語法及參數資訊，請參閱 [Remove-FederationTrust](https://technet.microsoft.com/zh-tw/library/dd351153\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否成功移除同盟信任，請執行下列其中一項：

  - 在 EAC 中，瀏覽至 \[組織\] \> \[共用\]。如果您成功移除同盟信任，則 \[同盟信任\] 下只會出現 \[啟用\] 按鈕。

  - 在命令介面中執行下列命令，確認未傳回您 Exchange 組織的同盟信任資訊。
    
        Get-FederationTrust
    
    如需詳細的語法及參數資訊，請參閱 [Get-FederationTrust](https://technet.microsoft.com/zh-tw/library/dd351262\(v=exchg.150\))。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。


---
title: '設定群組計量: Exchange 2013 Help'
TOCTitle: 設定群組計量
ms:assetid: 76ccd6a7-e2ec-42f4-9ab3-e8cc257ac896
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ649327(v=EXCHG.150)
ms:contentKeyID: 50473521
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定群組計量

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

提供資訊的通訊群組和動態通訊群組大小的郵件提示會依賴群組計量資料。在指定的信箱伺服器上產生群組計量資料。如需群組計量的詳細資訊，請參閱[群組計量 」 和 「 郵件提示](group-metrics-and-mailtips-exchange-2013-help.md)。

您可以在 Mailbox Server 上啟用或停用群組計量的產生作業。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「群組計量」項目。

  - 群組計量資料僅用於郵件提示。請確定郵件提示會啟用該群組計量組織中。如需詳細步驟，請參閱[管理郵件提示的組織關係](manage-mailtips-for-organization-relationships-exchange-2013-help.md)。

  - 您只能使用命令介面來執行此程序。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

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


## 使用命令介面啟用或停用產生群組計量

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，負責產生離線通訊錄 (OAB) 的任何伺服器上產生群組計量資料。這些範例只都未使用 Oab 的組織。</td>
</tr>
</tbody>
</table>


若要啟用或停用信箱伺服器上的群組計量產生作業，請執行以下命令：

    Set-MailboxServer <ServerIdentity> -ForceGroupMetricsGeneration <$true | $false>

此範例會啟用名為 MBX1 的信箱伺服器上的群組計量產生作業。

    Set-MailboxServer MBX1 -ForceGroupMetricsGeneration $true

## 如何才能了解這是否正常運作？

若要驗證您已成功啟用或停用在不使用 OAB 的組織中的群組計量產生功能，請執行以下操作：

1.  執行下列命令：
    
        Get-MailboxServer <ServerIdentity> | Format-List ForceGroupMetricsGeneration

2.  驗證顯示的設定是您配置的設定。


---
title: '檢視使用者的行動裝置資訊: Exchange 2013 Help'
TOCTitle: 檢視使用者的行動裝置資訊
ms:assetid: 4fd263c0-ad61-416c-bd68-339bf66605cf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997974(v=EXCHG.150)
ms:contentKeyID: 50473100
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視使用者的行動裝置資訊

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-29_

使用者可以設定多個進行同步處理的行動裝置MicrosoftExchange Server 2013。您可以使用 EAC 或命令介面來檢視相關聯之特定使用者的行動裝置的清單。

若欲瞭解更多與行動裝置相關的管理工作，請參閱 [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱主題中的「行動裝置信箱原則」[用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)項目。

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

## 使用 EAC 來檢視使用者的行動裝置資訊

EAC 中會顯示目前使用者的信箱與同步處理的行動裝置的清單。您可以檢視行動裝置系列、 模型、 電話號碼或狀態。

1.  在 EAC 中，按一下 \[收件者\] \> \[信箱\] 並選擇信箱。

2.  在 \[詳細資料\] 窗格中，拉動捲軸至 \[電話與語音功能\] 然後按一下 \[檢視詳細資料\] 來顯示 \[行動裝置詳細資料\] 畫面。

## 使用命令介面來檢視使用者的行動裝置資訊

您可以利用 **Get-MobileDevice** 指令程式檢視特定使用者的行動裝置清單。

1.  執行下列命令。
    
        Get-MobileDevice -Mailbox useralias


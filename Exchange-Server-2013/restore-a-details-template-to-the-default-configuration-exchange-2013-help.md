---
title: '還原設為預設組態的詳細資料範本: Exchange 2013 Help'
TOCTitle: 還原設為預設組態的詳細資料範本
ms:assetid: 84c5f49b-614d-4f0e-8701-0979a2eb90bf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232102(v=EXCHG.150)
ms:contentKeyID: 50473616
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 還原設為預設組態的詳細資料範本

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-12_

詳細資料範本編輯器不包含 \[**復原**\] 按鈕，也可以使用鍵盤快速鍵復原動作。若要復原對範本加入，您必須使用 DELETE 鍵。若要復原刪除，您必須重新套用設定。您也可以藉由離開而不儲存變更的詳細資料範本編輯器還原為原始設定。如果您想要復原變更已儲存之後，您可以還原範本。當您還原範本時，所有自訂項都目遺失、 和範本還原為其原始設定。

本主題說明如何使用 \[Exchange 2013 工具箱\] 或 Exchange 管理命令介面，將詳細資料範本還原成其預設組態。

若要深入瞭解詳細資料範本，請參閱[詳細資料範本](details-templates-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md)主題中的您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「詳細資料範本」項目。

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


## 使用 \[Exchange 工具箱\] 將詳細資料範本還原成預設組態

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange Server 2013\] \> \[Exchange 工具箱\]。

2.  在 \[Exchange 工具箱\] 中，按一下 \[詳細資料範本編輯器\]，然後再按一下執行窗格中的 \[開啟工具\]。

3.  在 \[詳細資料範本編輯器\] 的 \[詳細資料\] 窗格中，選取要還原的範本，然後按一下執行窗格中的 \[還原\]。

4.  按一下**\[是\]**確認您想要的範本還原成原始狀態。所有自訂將都會遺失。

## 使用命令介面將詳細資料範本還原成預設組態

此範例會還原美式英文的連絡人詳細資料範本。

    Restore-DetailsTemplate -Identity "en-US\Contact"

如需語法與參數的詳細資訊，請參閱 [Restore-DetailsTemplate](https://technet.microsoft.com/zh-tw/library/bb125188\(v=exchg.150\))。


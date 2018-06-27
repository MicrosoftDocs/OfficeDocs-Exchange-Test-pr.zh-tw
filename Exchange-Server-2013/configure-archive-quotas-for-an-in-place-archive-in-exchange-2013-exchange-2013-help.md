---
title: '設定封存配額為 「 就地封存在 Exchange 2013: Exchange 2013 Help'
TOCTitle: 設定封存配額為 「 就地封存在 Exchange 2013
ms:assetid: f10e77c7-e1d4-415a-bef9-cb3f00e74c34
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee633489(v=EXCHG.150)
ms:contentKeyID: 50554080
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定封存配額為 「 就地封存在 Exchange 2013

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-12-04_

在內部部署中就地封存預設會建立具有不受限制的儲存配額。因此，您需要編輯若要設定封存的儲存配額的信箱內容。您可以將封存的下列配額：

  - **封存警告配額**  就地封存超過指定的封存警告配額時, Exchange管理員記錄事件和警告訊息傳送給信箱使用者。

  - **封存配額**  就地封存超過指定的封存配額時, 的郵件不會再移至封存和警告訊息傳送給信箱使用者。

若要深入了解就地封存，請參閱[就地封存 in Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 在 Exchange 系統管理中心 (EAC)，您可以使用下拉式清單以固定值來設定封存配額及封存警告配額。如果您想要在 EAC 中未列出的值來設定任一配額，使用命令介面。

  - 設定封存警告配額比封存配額為較低值。根據使用者的封存成長率、 封存警告配額和封存配額之間的差異應該允許使用者採取適當的項目，例如封存的刪除項目或請求的足夠次系統管理員或 IT 服務台引發封存配額。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md) 主題中的「收件者佈建權限」一節。

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


## 您要執行的工作

## 使用 EAC 來設定封存配額和封存信箱的警告配額

1.  瀏覽至 \[**收件者**\>**信箱**

2.  在清單檢視中，選取 \[信箱

3.  在 \[詳細資料\] 窗格中 \[**就地封存**、 按一下 \[**檢視詳細資料**。

4.  **封存信箱**中使用**配額值 (GB)**和**發出警告 (GB)**清單中選取所需的值。

5.  按一下 **\[確定\]**。

## 使用命令介面來設定封存配額和封存信箱的警告配額

本範例會設定 Chris Ashton 信箱封存配額至 10 gb (GB) 的使用者會收到警告訊息為 「 就地封存已滿的時間與他將不再能夠將項目移至封存。這個範例也會將封存警告配額至 9.5 GB，使用者會收到此時就地封存是幾乎滿溢的警告訊息。

    Set-Mailbox -Identity "Chris Ashton" -ArchiveQuota 10GB -ArchiveWarningQuota 9.5GB

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要驗證是否成功為現有使用者信箱啟用內部部署封存，請執行以下其中一個操作：

  - 在 EAC 中，瀏覽至 \[**收件者**\>**信箱**和信箱選取您想。在 \[**就地封存**、 詳細資料窗格中按一下 \[**檢視詳細資料**並確認封存的配額設定。

  - 在命令介面中執行下列命令以顯示封存相關的配額資訊。
    
        Get-Mailbox <Name> | FL Name,Archive*Quota


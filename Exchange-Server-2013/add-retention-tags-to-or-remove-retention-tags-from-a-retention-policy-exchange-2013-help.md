---
title: '若要保留標記中新增或移除保留標記的保留原則: Exchange Online Help'
TOCTitle: 若要保留標記中新增或移除保留標記的保留原則
ms:assetid: 3a5196ce-2764-453d-9bc1-5ec22d06b40d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd362328(v=EXCHG.150)
ms:contentKeyID: 50472987
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 若要保留標記中新增或移除保留標記的保留原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-02_

您可以新增至保留原則原則會在建立時的保留標記或任何時候之後。如需如何建立保留原則的詳細資訊，包括如何同時新增保留標記，請參閱[建立保留原則](create-a-retention-policy-exchange-2013-help.md)。

保留原則可以包含下列保留標記：

  - 一個或多個受支援預設資料夾的保留原則標記 (RPT)

  - 一個預設原則標記 (DPT)，搭配 \[移到封存\] 動作

  - 一個含 **\[刪除並允許復原\]** 或 **\[永久刪除\]** 動作的 DPT

  - 一個語音郵件 DPT

  - 任意數目的個人標記

如需保留標記的詳細資訊，請參閱[保留標記和保留原則](retention-tags-and-retention-policies-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「通訊記錄管理」項目。

  - 除非它們連結至保留原則和受管理的資料夾助理員處理的信箱保留標記不會套用至信箱。若要啟動受管理的資料夾助理員，它會處理信箱，請參閱[設定受管理的資料夾助理員](configure-the-managed-folder-assistant-exchange-2013-help.md)。

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

## 使用 EAC 來新增或移除保留標記

1.  移至 \[**相符性管理**\>**保留原則**。

2.  在清單檢視中，選取您要新增保留標記的保留原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[保留原則\] 中，使用下列設定：
    
      - \[新增\]  ![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 按一下這個按鈕新增保留標記到原則。
    
      - \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")   從清單中選取一個標記，然後按一下這個按鈕從原則移除標記。

## 使用命令介面來新增或移除保留標記

此範例會將保留標記 VPs-Default、VPs-Inbox 及 VPs-DeletedItems，新增至尚未與保留標記連結的保留原則 RetPolicy-VPs。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果該原則具有與其連結的保留標記，此命令將會取代現有標記。</td>
</tr>
</tbody>
</table>


    Set-RetentionPolicy -Identity "RetPolicy-VPs" -RetentionPolicyTagLinks "VPs-Default","VPs-Inbox","VPs-DeletedItems"

此範例會將保留標記 VPs-DeletedItems 新增到保留原則 RetPolicy-VPs，此原則已有連結的其他保留標記。

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Add((Get-RetentionPolicyTag 'VPs-DeletedItems').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

此範例會從保留原則 RetPolicy-VPs 移除保留標記 VPs-Inbox。

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Remove((Get-RetentionPolicyTag 'VPs-Inbox').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

如需詳細的語法及參數資訊，請參閱 [Set-RetentionPolicy](https://technet.microsoft.com/zh-tw/library/dd335196\(v=exchg.150\)) 與 [Get-RetentionPolicy](https://technet.microsoft.com/zh-tw/library/dd298086\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證您是否成功自保留原則新增或移除保留標記，請使用 [Get-RetentionPolicy](https://technet.microsoft.com/zh-tw/library/dd298086\(v=exchg.150\)) 指令程式來驗證 *RetentionPolicyTagLinks* 屬性。

此範例使用 **Get-RetentionPolicy** 指令程式來擷取新增至預設 MRM 原則的保留標記，並將他們以管線傳輸至 **Format-Table** 指令程式，以輸出每個標記的名稱屬性。

    (Get-RetentionPolicy "Default MRM Policy").RetentionPolicyTagLinks | Format-Table name


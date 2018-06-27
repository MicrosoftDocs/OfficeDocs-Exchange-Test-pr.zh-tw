---
title: '套用或移除信箱上的 Outlook Web App 信箱原則: Exchange Online Help'
TOCTitle: 套用或移除信箱上的 Outlook Web App 信箱原則
ms:assetid: 51d8e269-b0d5-4bc7-9b3d-0460871e54fa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876884(v=EXCHG.150)
ms:contentKeyID: 50473107
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 套用或移除信箱上的 Outlook Web App 信箱原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-10-12_

您可以使用 EAC 或命令介面，套用 Outlook Web App 信箱原則到一個或多個信箱，或移除信箱原則。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「Outlook Web App 信箱原則」項目。

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

## 套用 Outlook Web App 信箱原則

## 使用 EAC 套用 Outlook Web App 信箱原則

1.  在 EAC 中，按一下 \[收件者\] \> \[信箱\]。

2.  在 \[工作\] 窗格中，按一下以選取您想要套用至Outlook Web App信箱原則的信箱。您也可以選取多個信箱。

3.  **如果您選擇了一個信箱：**
    
    1.  在 \[詳細資料\] 窗格中向下拉動捲軸至 \[電子郵件連線\] 然後按一下 \[檢視詳細資料\]。
    
    2.  按一下 \[瀏覽\] 檢視和選取可用的信箱原則。
    
    3.  按一下 \[儲存\] 以指派選擇的原則至選定的信箱。
    
    **如果您選擇了一個以上信箱：**
    
    1.  在 \[詳細資料\] 窗格中向下拉動捲軸至 \[Outlook Web App\] 然後按一下 \[指派原則\]。
    
    2.  按一下 \[瀏覽\] 檢視和選取可用的信箱原則。
    
    3.  按一下 \[儲存\] 以指派選擇的原則至選定的信箱。

## 使用命令介面可將 Outlook Web App 信箱原則套用到現有的信箱

此範例會將名爲「行事曆」的 Outlook Web App 信箱原則套用到使用者 tony@contoso.com 的信箱。

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:Calendar

如需語法及參數的詳細資訊，請參閱 [Set-CASMailbox](https://technet.microsoft.com/zh-tw/library/bb125264\(v=exchg.150\))。

## 移除 Outlook Web App 信箱原則

## 使用 EAC 移除 Outlook Web App 信箱原則

1.  在 EAC 中，按一下 \[收件者\] \> \[信箱\]。

2.  在工作窗格中，按一下以選取您要自 Outlook Web App 信箱原則移除的信箱。

3.  在 \[詳細資料\] 窗格中向下拉動捲軸至 \[電子郵件連線\] 然後按一下 \[檢視詳細資料\]。
    
    若已指定信箱原則，按一下 \[清除\] 將其自信箱中移除。

4.  按一下 **\[儲存\]** 以儲存變更。

## 使用命令介面可從現有信箱移除 Outlook Web App 信箱原則。

此範例會從使用者 tony@contoso.com 的信箱移除 Outlook Web App 信箱原則。

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:$null

如需語法及參數的相關資訊，請參閱 [Set-CASMailbox](https://technet.microsoft.com/zh-tw/library/bb125264\(v=exchg.150\))。


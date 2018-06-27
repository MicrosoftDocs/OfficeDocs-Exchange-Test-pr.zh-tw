---
title: '變更使用者節流設定在組織中的所有使用者: Exchange 2013 Help'
TOCTitle: 變更使用者節流設定在組織中的所有使用者
ms:assetid: c45cacfc-768d-4605-9bb0-53e30273fe4d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ863578(v=EXCHG.150)
ms:contentKeyID: 50554059
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 變更使用者節流設定在組織中的所有使用者

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-08-05_

您可以控制消耗的資源由 Exchange 組織中的個別使用者透過變更預設的節流設定。

控制個別使用者耗用資源的方式已經可能在Exchange Server 2010，並已展開這項功能的Exchange Server 2013。名為 GlobalThrottlingPolicy 原則定義預設的節流設定為在組織中每個新的和現有使用者除非您已自訂的節流原則。一般 Exchange 部署在許多案例中，名為 GlobalThrottlingPolicy 此原則會以管理使用者。

若要自訂套用至組織中的所有使用者的節流設定，建立新的節流原則的範圍指派的組織。您只可以變更預設的節流設定使用命令介面。

## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [伺服器健康狀況與效能的權限](server-health-and-performance-permissions-exchange-2013-help.md)主題中 「 使用者節流 」 的項目。

  - 在新組織範圍原則，您應設定只能在名為 GlobalThrottlingPolicy 和任何其他組織原則原則不同的節流設定。如此一來，從名為 GlobalThrottlingPolicy 原則的原則設定的其餘部分將會是繼承而來，如將任何節流原則會新增在未來更新 Exchange 的更新。建議您檢閱 「 管理節流原則使用範圍"\] 區段中的主題[Exchange 工作負載管理](exchange-workload-management-exchange-2013-help.md)然後再執行此程序。

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


## 使用命令介面來變更方式的資源可供整個組織中的所有使用者

此範例會建立套用至組織中的所有使用者節流原則。您省略任何參數會繼承預設的節流原則 GlobalThrottlingPolicy 中的值。

    New-ThrottlingPolicy -Name AllUsersEWSPolicy EwsMaxConcurrency 4 -ThrottlingPolicyScope Organization

如需詳細的語法及參數的詳細資訊，請參閱[New-ThrottlingPolicy](https://technet.microsoft.com/zh-tw/library/dd351045\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否已成功建立組織節流原則，請執行下列動作：

1.  執行下列命令。
    
        Get-ThrottlingPolicy | Format-List

2.  確認組織節流您剛才建立的原則會列在欄中顯示 GlobalThrottlingPolicy 物件。

3.  執行下列命令。
    
        Get-ThrottlingPolicy | Format-List

4.  確認新的組織原則的內容符合您所設定的值。


---
title: '修改、 停用或移除共用原則: Exchange 2013 Help'
TOCTitle: 修改、 停用或移除共用原則
ms:assetid: 714af42d-ca29-4bb4-ac48-f0b3d4fd1c15
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657460(v=EXCHG.150)
ms:contentKeyID: 50473427
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 修改、 停用或移除共用原則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-02-15_

共用原則可讓 Exchange 組織內的個別使用者與其他同盟 Exchang 組織、非同盟 Exchang 組織和個別網際網路使用者共用行事曆的空閒/忙碌資訊。在進行一般操作期間，您可能想變更一些共用原則內容，例如修改共用規則、變更空閒/忙碌存取等級、暫時停用共用原則或完全移除共用原則。

若要深入了解同盟共用，請參閱[共用](sharing-exchange-2013-help.md)

如需如何建立共用原則的詳細資訊，請參閱[建立共用原則](create-a-sharing-policy-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「行事曆與共用權限」項目。

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

## 使用 EAC 來修改共用原則

1.  瀏覽至 **\[組織\]** \> **\[共用\]**。

2.  在 \[單獨共享\]下選擇共享原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[共用原則\]** 中，按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  在 **\[共用規則\]** 中，據以修改共用規則。您可以變更設定 (例如想要與其共用資訊的網域，以及行事曆約會的共用層級)。完成時，按一下 **\[儲存\]** 關閉 **\[共用規則\]** 對話方塊。

5.  在 **\[共用原則\]** 中，按一下 **\[儲存\]** 更新共用原則。

## 使用 EAC 將一項共用原則設為預設的共用原則

1.  瀏覽至 **\[組織\]** \> **\[共用\]**。

2.  在 \[單獨共享\]下選擇共享原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[共用原則\]** 中，選取 **\[將此原則設為預設共用原則\]** 核取方塊。

4.  按一下 **\[儲存\]** 以更新共用原則。

## 使用 EAC 來停用共用原則

1.  瀏覽至 \[組織\] \> \[共享\]。

2.  在 \[單獨共享\] 下，選取一個共用原則。

3.  在 \[已啟用\] 欄位中，取消選取想要停用之共用原則的核取方塊。

## 使用 EAC 來移除共用原則

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在移除共用原則之前，必須先移除所有使用者信箱中的共用原則。</td>
</tr>
</tbody>
</table>


1.  瀏覽至 **\[組織\]** \> **\[共用\]**。

2.  在 \[單獨共享\] 下，選取一個共享原則，然後按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

3.  在警告中，按一下 **\[是\]** 來刪除共用原則。

## 使用命令介面修改、停用或移除共用原則

  - 本範例針對 contoso.com 這個您組織的外部網域修改共用原則 Contoso。此原則可讓 Contoso 網域的使用者看見簡單的空閒/忙碌資訊。
    
        Set-SharingPolicy -Identity Contoso -Domains 'sales.contoso.com: CalendarSharingFreeBusySimple'

  - 本範例將第二個網域新增至共用原則 Contoso。當您要將某網域新增至現有的原則時，必須包括先前所有已包含的網域。
    
        Set-SharingPolicy -Identity Contoso -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'atlanta.contoso.com: CalendarSharingFreeBusyReviewer', 'beijing.contoso.com: CalendarSharingFreeBusyReviewer'

  - 此範例會將共用原則 Contoso 設定為預設的共用原則。
    
        Set-SharingPolicy -Identity Contoso -Default $True

  - 此範例會停用共用原則 Contoso。
    
        Set-SharingPolicy -Identity "Contoso" -Enabled $False

  - 第一個範例會移除共用原則 Contoso。第二個範例會移除共用原則 Contoso，並抑制您想移除原則的確認。
    
        Remove-SharingPolicy -Identity Contoso
    
        Remove-SharingPolicy -Identity Contoso -Confirm

如需詳細的語法及參數資訊，請參閱 [Set-SharingPolicy](https://technet.microsoft.com/zh-tw/library/dd297931\(v=exchg.150\)) 與 [Remove-SharingPolicy](https://technet.microsoft.com/zh-tw/library/dd351071\(v=exchg.150\))。


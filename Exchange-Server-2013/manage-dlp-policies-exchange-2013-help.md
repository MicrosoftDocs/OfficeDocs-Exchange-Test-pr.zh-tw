---
title: '管理 DLP 原則: Exchange Online Help'
TOCTitle: 管理 DLP 原則
ms:assetid: ba81fabd-7f7f-4ef7-968f-ce851ada9d70
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673559(v=EXCHG.150)
ms:contentKeyID: 50474109
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理 DLP 原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-01-14_

您可以檢視、 變更或移除現有資料外洩防護 (DLP) 原則中 Microsoft Exchange，使用 Exchange 系統管理中心 (EAC) 或 Exchange 管理命令介面。

DLP 相關的其他管理工作，請參閱[DLP 程序](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013) 或[\[Exchange Online\] 的 DLP 程序](https://technet.microsoft.com/zh-tw/library/jj938003\(v=exchg.150\)) (Exchange Online)。

如需 Exchange 管理命令介面的詳細資訊，請參閱[使用 PowerShell 與 Exchange 2013 (Exchange 管理命令介面)](https://technet.microsoft.com/zh-tw/library/bb123778\(v=exchg.150\))。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間： 15-60 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「資料外洩防護 (DLP) 」項目。

  - 對於任何 DLP 原則，您可以選取下列其中一種模式：
    
      -  
        **強制**   系統會針對所有郵件和支援的檔案類型評估原則內的規則。 如果偵測到符合原則條件的資料，郵件流程可能會中斷。 原則內所述的所有動作都會執行。
    
      -  
        **測試 DLP 原則並顯示原則提示**   系統會針對所有郵件和支援的檔案類型評估原則內的規則。 如果偵測到符合原則條件的資料，郵件流程將不會中斷。 也就是說，郵件不會遭到攔截。 如果設有原則提示，使用者就會看到提示。
    
      -  
        **不搭配原則提示的測試 DLP 原則**  原則內的規則所評估的所有郵件及支援檔案類型。如果資料會偵測符合原則的條件，不會中斷郵件流程。也就是未封鎖的郵件。如果設定原則提示，他們是不會顯示給使用者。

  - DLP 原則內的個別規則可以擁有其所屬的模式設定。 如果原則模式與該原則內的規則模式不同，則規則設定的優先順序較高且將根據其模式進行評估。

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

## 檢視現有 DLP 原則的詳細資料

您可能需要檢視已為組織建立的現有 DLP 原則的規則和動作。 這在您經歷非預期的郵件流程問題，或您的組織變更需要受到監視之敏感資訊的方式時，可能會很實用。

## 使用 EAC 檢視現有 DLP 原則內的詳細資料

1.  在 EAC 中，瀏覽至 \[規範管理\] \> \[資料外洩防護\]。

2.  按兩下顯示在原則清單的其中一個原則，或反白顯示一個項目後，再按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[編輯 DLP 原則\] 頁面按一下 \[規則\]。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以建立 DLP 原則，並讓它保持非啟動或停用模式。 在此模式中，不會強制執行原則，而且您可以在測試或開始強制執行之前，變更與其規則相關的任何述詞、動作或值。</td>
</tr>
</tbody>
</table>


## 使用命令介面檢視現有 DLP 原則內的詳細資料

此範例會傳回與名為 Employee Numbers 的虛擬 DLP 原則有關的資訊。 此命令會透過管道傳送至 **Format-List** 指令程式，以顯示所指定 DLP 原則的詳細組態。

    Get-DlpPolicy "Employee Numbers" | Format-List

如需語法及參數資訊，請參閱 [Get-DlpPolicy](https://technet.microsoft.com/zh-tw/library/jj215752\(v=exchg.150\))。

## 變更 DLP 原則

您可以藉由修改原則的名稱或管理原則之影響的規則，來變更現有的 DLP 原則。 範例規則變更可能包括針對特定網域內傳送且偵測到擁有敏感資訊的郵件，將自訂免責聲明文字新增至郵件內文以及 RMS 保護。 如果您要使用 DLP 原則範本，務必記得這些只是 Exchange 2013 中可協助您為郵件環境設計和套用堅固原則和規範系統的眾多功能之一。

## 使用 EAC 變更現有的 DLP 原則

1.  在 EAC 中，瀏覽至 \[規範管理\] \> \[資料外洩防護\]。

2.  按兩下顯示在原則清單的其中一個範本原則，或反白顯示一個項目後，再按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[編輯 DLP 原則\] 頁面按一下 \[規則\]。

4.  若要變更現有的規則，請反白顯示該規則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

5.  若要新增您可以完全自訂的空白規則，請按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

6.  若要新增有關寄件者通知、封鎖郵件或允許覆寫的規則，請按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 圖示旁的箭頭。

7.  若要移除規則，請將該規則反白後再按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

8.  按一下 \[儲存\] 以完成這項政策的修改並儲存變更。

## 使用命令介面變更現有的 DLP 原則

您可以使用 Exchange 管理命令介面指定原則的動作和通知層級。 此範例會設定名為 Employee Numbers 的虛擬 DLP 原則的模式，如此便不會強制執行動作且不會顯示通知郵件。

    Set-DlpPolicy "Employee Numbers" -Mode Audit

如需語法及參數資訊，請參閱 [Set-DlpPolicy](https://technet.microsoft.com/zh-tw/library/jj215778\(v=exchg.150\))。

## 刪除 DLP 原則

您可以使用 EAC 永久移除 DLP 原則。 一旦刪除某個原則之後，就不會再強制執行該原則，而且不會儲存任何規則和動作。

或者，您可以將原則的操作狀態或模式設定為 \[沒有原則提示的情況下測試 DLP 原則\]。 這樣可停止在郵件環境中強制執行原則，但是保留原則本身的詳細組態設定。 如果您未來可能需要再次強制執行該原則，這樣可能會很有用。

## 使用 EAC 刪除現有的 DLP 原則

1.  在 EAC 中，瀏覽至 \[規範管理\] \> \[資料外洩防護\]。

2.  選取原則清單中您要移除的原則，然後按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

## 使用命令介面刪除現有的 DLP 原則

此範例會移除名為 Employee Numbers 的虛擬 DLP 原則。

    Remove-DlpPolicy "Employee Numbers"

如需語法及參數資訊，請參閱 [Remove-DlpPolicy](https://technet.microsoft.com/zh-tw/library/jj215677\(v=exchg.150\))。

## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[原則提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)


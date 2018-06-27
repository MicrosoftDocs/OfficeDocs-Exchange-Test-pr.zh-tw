---
title: '修改就地 eDiscovery 搜尋: Exchange Online Help'
TOCTitle: 修改就地 eDiscovery 搜尋
ms:assetid: 3162743c-cc12-4997-91e0-bcbfea8bcb17
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335182(v=EXCHG.150)
ms:contentKeyID: 50472923
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 修改就地 eDiscovery 搜尋

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-08-27_

建立就地 eDiscovery 搜尋之後，您可以修改其變更搜尋參數。例如，您可以變更要搜尋的信箱、 日期範圍、 關鍵字、 記錄選項，或您可以指定不同的探索信箱儲存搜尋結果。當您重新啟動搜尋會使用您對搜尋屬性進行任何變更。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果執行就地 eDiscovery 搜尋，必須先將它停止之前先對其進行修改。當您重新啟動搜尋結果的搜尋上次執行的時間會移除探索信箱。不過，從上一個搜尋記錄檔會儲存。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間： 2-5 分鐘。

  - 就地 eDiscovery 搜尋已建立且未執行。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「就地 eDiscovery」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 使用 EAC 來修改就地 eDiscovery 搜尋

1.  瀏覽至 \[規範管理\] \> \[就地 eDiscovery 和保留\]。

2.  在清單檢視中，選取您要修改就地 eDiscovery 搜尋和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在**就地 eDiscovery 和保留**、 您可以修改下列設定：
    
      - 在 \[**名稱**\] 索引標籤上修改搜尋及選擇性描述名稱。
    
      - 在 \[**信箱**\] 頁面中修改的信箱搜尋。您可以搜尋所有信箱或選取要都搜尋的特定錯誤。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>您無法使用<strong>搜尋所有信箱</strong>] 選項將所有信箱設為保留Exchange 2013 Mailbox server 上。若要建立就地保留，您必須選取<strong>指定信箱搜尋</strong>。如需詳細資訊，請參閱<a href="create-or-remove-an-in-place-hold-exchange-2013-help.md">建立或移除就地保留</a>。</td>
        </tr>
        </tbody>
        </table>
    
      - 在 \[**搜尋查詢**\] 頁面中修改下列欄位：
        
          - **包含所有使用者信箱內容**  選取此選項可將所有內容都放入保留所選的信箱。
        
          - \[篩選依據準則\]   選擇這個選項以指定搜尋準則，包含關鍵字、開始與結束日期、寄件人與收件人地址以及訊息類型。
    
      - 在**就地保留功能**\] 頁面上選取**符合搜尋查詢中所選取的信箱上進行內容保留**\] 核取方塊，，然後選取一個項目放入 In-place Hold 下列選項：
        
          - \[無限期保留\]   選擇這個選項以將傳回項目設為無限期保留。除非您從搜尋中移除信箱或移除搜尋，否則保留的項目會一直保存下來。
        
          - \[指定與項目收到日期相關的保留天數\] 使用這個選項將項目保留一段特定期間。例如，若您的組織要求所有郵件都必須至少保存七年時，即可使用此選項。您可使用「以時間為基礎」的就地保留和保留原則，以確保項目會在七年後受到刪除。
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>當為法律目的進行信箱或項目的 In-Place Hold 保留時，一般建議無限期保留項目並於案件或調查完成時移除保留。</td>
            </tr>
            </tbody>
            </table>


4.  按一下 **\[儲存\]**。

## 使用命令介面來修改就地 eDiscovery 搜尋

此範例會修改就地 eDiscovery 搜尋來搜尋信箱 DG ProjectManagers 通訊群組的成員屬於搜尋 Project Contoso。

    Set-MailboxSearch -Identity "Search-Project Contoso" -SourceMailboxes "DG-ProjectManagers"

## 如何知道這是否正常運作？

若要確認您已成功修改就地 eDiscovery 搜尋，請執行下列其中一項：

  - 使用 EAC 來檢查搜尋的內容。

  - 使用命令介面從**Get-MailboxSearch**指令程式檢查搜尋的屬性。如需如何檢查信箱搜尋的屬性的範例，請參閱[Get-MailboxSearch](https://technet.microsoft.com/zh-tw/library/dd351021\(v=exchg.150\))的 「 範例 」 一節。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用<strong>Get-MailboxSearch</strong>Exchange Online中擷取的 eDiscovery 搜尋的相關資訊，您必須指定搜尋以返回搜尋屬性 ； 的完整清單的名稱例如， <code>Get-MailboxSearch &quot;Contoso Legal Case&quot;</code>。如果您執行<strong>Get-MailboxSearch</strong>指令程式不使用任何參數時，不傳回下列屬性：
<ul>
<li><p>SourceMailboxes</p></li>
<li><p>Sources</p></li>
<li><p>SearchQuery</p></li>
<li><p>ResultsLink</p></li>
<li><p>PreviewResultsLink</p></li>
<li><p>Errors</p></li>
</ul>
原因是它需要大量的資源以傳回組織中所有的 eDiscovery 搜尋這些屬性。</td>
</tr>
</tbody>
</table>


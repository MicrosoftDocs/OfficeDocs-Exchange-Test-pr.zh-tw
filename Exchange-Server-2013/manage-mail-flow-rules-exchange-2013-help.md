---
title: '管理郵件流程規則: Exchange Online Help'
TOCTitle: 管理郵件流程規則
ms:assetid: e7a81372-b6d7-4d1f-bc9e-a845a7facac2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657505(v=EXCHG.150)
ms:contentKeyID: 50474492
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理郵件流程規則

 

_**適用版本：**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

郵件流程規則，也稱為傳輸規則可用來尋找特定條件郵件通過組織並採取動作。本主題說明如何建立、複製、調整順序、啟用或停用、刪除或匯入或匯出規則以及如何監視規則使用。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要確定您規則運作您預期的方式，請務必徹底測試每個規則和規則之間的互動。</td>
</tr>
</tbody>
</table>


對於使用這些程序的案例感興趣嗎？請參閱下列主題：

  - [整個組織的免責聲明、簽章、頁尾或標頭](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [使用傳輸規則檢查郵件附件](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [常見的附件封鎖案例](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)

  - [使用清單中的文字、 片語或模式為基礎的路由電子郵件的郵件流程規則](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md)

  - [常見的郵件核准案例](common-message-approval-scenarios-exchange-2013-help.md)

  - [使用郵件流程規則讓郵件可以略過雜亂](use-mail-flow-rules-so-messages-can-bypass-clutter-exchange-2013-help.md)

  - [設定郵件流程規則的最佳作法](best-practices-for-configuring-mail-flow-rules-exchange-2013-help.md)

  - [使用檢查 Office 365 中的郵件附件的郵件流程規則](https://technet.microsoft.com/zh-tw/library/jj919236\(v=exchg.150\))

  - [使用傳輸規則來設定大量電子郵件篩選](https://technet.microsoft.com/zh-tw/library/dn720438\(v=exchg.150\))

  - [定義加密或解密訊息的規則](https://go.microsoft.com/fwlink/p/?linkid=402846)。

  - [在 Office 365 中建立全組織的安全寄件者或封鎖的寄件者清單](https://technet.microsoft.com/zh-tw/library/dn198251\(v=exchg.150\))

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱＜[郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)＞(Exchange Server) 或＜[Exchange Online 中的功能權限](https://technet.microsoft.com/zh-tw/library/jj200673\(v=exchg.150\))＞中的「傳輸規則」項目。

  - 當規則已列為**版本 14**時，這表示規則根據Exchange Server 2010郵件流程規則格式。可以使用這些規則的所有選項。

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

## 建立郵件流程規則

您可以建立的郵件流程規則設定資料遺失防護 (DLP) 原則\]，建立新規則，或複製的規則。您可以使用Exchange 系統管理中心 (EAC) 或Exchange 管理命令介面。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建立或修改的郵件流程規則之後，則可能需要 30 分鐘的時間全新或更新規則套用至電子郵件。</td>
</tr>
</tbody>
</table>


## 使用 DLP 原則來建立郵件流程規則

每個 DLP 原則是郵件流程規則的集合。建立 DLP 原則之後，您可以使用下列程序的規則此細部調整。

1.  建立 DLP 原則。如需詳細指示，請參閱：
    
      - [Exchange Server 2013 DLP 程序](dlp-procedures-exchange-2013-help.md)
    
      - [Exchange Online DLP 程序](dlp-procedures-exchange-2013-help.md)

2.  修改建立的 DLP 原則的郵件流程規則。請參閱檢視或修改傳輸規則。

## 使用 EAC 來建立郵件流程規則

EAC 可讓您使用範本、 複製現有的規則或從頭建立郵件流程規則。

1.  移至 **\[郵件流程\]** \> **\[規則\]**。

2.  使用下列其中一個選項來建立規則：
    
      - 若要從範本建立規則，請按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，然後選取範本。
    
      - 若要複製規則，請選取規則，然後選取 **\[複製\]**![複製圖示](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "複製圖示")。
    
      - 若要從頭開始建立新規則，請按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，然後選取 **\[建立新規則\]**。

3.  在 **\[新增規則\]** 對話方塊中，將規則命名，然後為此規則選取條件和動作：
    
    1.  在 **\[套用此規則...\]** 中，從可用的條件清單中選取您想要的條件。
        
          - 一些情況都需要您指定的值。例如，如果您選取 \[**寄件者是...**條件，您必須指定寄件者地址。如果您要新增的單字或片語，請注意不允許行尾的空格。
        
          - 如果並未列出您想要的條件，或如果您需要新增例外狀況，請選取 **\[更多選項\]**。將會列出其他條件及例外狀況。
        
          - 如果您不想指定條件，而是想要此規則套用至組織中的所有郵件，請選取 \[套用到所有郵件\] 條件。
    
    2.  在 **\[執行下列動作...\]** 中，從可用的動作清單中，選取希望規則在郵件符合準則時所採取的動作。
        
          - 一些動作需要您指定值。例如，如果您選取 **\[將需要核准的郵件轉寄到\]** 條件，則需要選取組織中的收件者。
        
          - 如果您想要的條件並未列出，請選取 **\[更多選項\]**。將會列出其他條件。
    
    3.  指定此規則的規則比對資料[的資料遺失防護 (DLP) 報告](https://go.microsoft.com/fwlink/p/?linkid=402768)和[傳輸規則報告](https://go.microsoft.com/fwlink/p/?linkid=402769)中的顯示方式。
        
          - 下**稽核嚴重性層級與此規則**，選取 \[以指定此規則的嚴重性層級的層級。Office 365 活動報告的郵件流程規則群組規則比對依嚴重性層級。 嚴重層級是只以方便使用報告篩選器。嚴重層級上處理規則的優先順序有任何影響。
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>如果清除<strong>這個規則使用嚴重性層級的稽核</strong>] 核取方塊，規則比對未出現在規則報告。</td>
            </tr>
            </tbody>
            </table>
    
    4.  設定規則的模式。您可以使用的兩個測試模式來測試規則而不會影響郵件流程。在這兩個測試模式下時符合條件、 項目新增至郵件追蹤。
        
          - **強制執行**   這會開啟規則，並會立即開始處理郵件。將執行規則上的所有動作。
        
          - **搭配原則提示來測試**   這會開啟規則，且會傳送任何原則提示動作 (**\[以原則提示通知寄件者\]**)，但不會執行與郵件傳送相關的動作。需要資料外洩防護 (DLP) 才能使用此模式。若要深入了解，請參閱＜[原則提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)＞。
        
          - **不搭配原則提示就測試**   只會強制執行「產生事件報告」動作。不會執行與郵件傳送相關的動作。

4.  如果您滿意此規則，請移至步驟 5。如果您想要新增更多條件或動作，或者您想要指定例外狀況或設定其他屬性，請按一下 **\[更多選項\]**。按一下 \[更多選項\] 后，請完成下列欄位，建立規則：
    
    1.  若要新增更多條件，請按一下 \[新增條件\]\]。如果您有多個條件，您可以按一下任一條件旁邊的 \[移除 X\]，將其移除。請注意，在按一下 \[更多選項\] 之後，會有更多條件。
    
    2.  若要新增更多動作，請按一下 **\[新增動作\]**。如果您有多個動作，您可以按一下任一動作旁邊的 \[移除 X\]，將其移除。請注意，在按一下 \[更多選項\] 之後，會有更多動作。
    
    3.  若要指定例外狀況，請按一下 **\[新增例外狀況\]**，然後使用 **\[除非\]** 下拉式清單選取例外狀況。您可以按一下任意例外狀況旁邊的 \[移除 X\]，將其從規則移除。
    
    4.  如果您想要此規則在特定日期之後聲效，請按一下 \[在下列日期啟動此規則:\]且指定日期。請注意，規則仍會在此日期之前啟用，但不會進行處理。
        
        同樣，您也可以在特定日期使規則停止處理。為此，請按一下 \[於下列日期停用此規則:\]且指定日期。請注意，此規則將保持啟用狀態，但它不會進行處理。
    
    5.  您可以選擇使用此規則處理郵件后不套用其他規則。為此，請按一下 \[停止處理其他規則\]。如果您選取此選項，並且郵件已由此規則處理，則不再會有其他規則處理該郵件。
    
    6.  您可以指定如果無法完成規則處理時，應該如何處理郵件。預設會忽略此規則，並且定期處理郵件，但您可以選擇重新提交郵件進行處理。若要這麼做，請勾選 **\[如果無法完成規則處理時便順延郵件\]** 核取方塊。
    
    7.  如果您的規則會分析寄件者地址，預設它只會檢查郵件標頭。不過，您可以將您的規則設成也檢查 SMTP 郵件信封。若要指定檢查的項目，請為 **\[比對郵件中的寄件者地址\]** 按下列其中一個值：
        
          - **標頭**   只檢查郵件標頭。
        
          - **信封**   只檢查 SMTP 郵件信封。
        
          - **標頭或信封**   同時檢查郵件標頭和 SMTP 郵件信封。
    
    8.  您可以在 **\[註解\]** 方塊中新增此規則的註解。

5.  按一下 **\[儲存\]**，完成建立規則。

## 若要建立的郵件流程規則使用Exchange 管理命令介面

本範例會使用[New-TransportRule](https://technet.microsoft.com/zh-tw/library/bb125138\(v=exchg.150\))指令程式來建立新的郵件流程規則的前面加上"`External message to Sales DG:`"從組織外部寄至銷售部門通訊群組。

    New-TransportRule -Name "Mark messages from the Internet to Sales DG" -FromScope NotInOrganization -SentTo "Sales Department" -PrependSubject "External message to Sales DG:"

規則參數和上述程序中所使用的動作是針對僅。請檢閱所有可用的郵件流程規則條件和動作來決定哪些符合您的需求。

## 如何知道這是否正常運作？

若要確認您成功建立新的郵件流程規則，請執行下列動作：

  - 從 EAC 中，確認您建立的新郵件流程規則會列在 \[**規則**\] 清單中。

  - Exchange 管理命令介面，驗證您建立新的郵件流程規則成功執行下列命令 （下面的範例驗證上述Exchange 管理命令介面範例中建立的規則）：
    
        Get-TransportRule "Mark messages from the Internet to Sales DG"

## 檢視或修改的郵件流程規則

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建立或修改的郵件流程規則後，它可能需要 30 分鐘的時間全新或更新規則套用至電子郵件。</td>
</tr>
</tbody>
</table>


## 使用 EAC 來檢視或修改的郵件流程規則

1.  從 EAC 中，移至 **\[郵件流程\]** \> **\[規則\]**。

2.  當您在清單中選取規則后，該規則的條件、動作、例外狀況和選取內容會顯示在詳細資料窗格中。若要檢視特定規則的所有內容，請將它按兩下。這會開啟規則編輯器視窗，讓您變更規則。如需規則屬性的詳細資訊，請參閱本主題之前的＜Use the EAC to create a new Transport rule＞一節。

## 若要檢視或修改的郵件流程規則使用Exchange 管理命令介面

下列範例列出了組織中設定的所有規則清單：

    Get-TransportRule

若要檢視特定的郵件流程規則的屬性，您必須提供該規則或其 GUID 的名稱。是要將輸出傳送至**Format-List**指令程式來格式化屬性通常是很有幫助。下列範例會傳回名為 \[**寄件者是行銷部門成員**的郵件流程規則的所有屬性：

    Get-TransportRule "Sender is a member of marketing" | Format-List

若要修改現有規則的屬性，請使用 [Set-TransportRule](https://technet.microsoft.com/zh-tw/library/bb123534\(v=exchg.150\)) 指令程式。此指令程式允許您變更與規則相關的任何內容、條件、動作或例外狀況。下列範例新增例外狀況至「寄件者是行銷部門成員」規則，以便它不會套用到使用者 Kelly Rollin 傳送的郵件：

    Set-TransportRule "Sender is a member of marketing" -ExceptIfFrom "Kelly Rollin"

## 如何知道這是否正常運作？

若要確認您已成功修改的郵件流程規則，請執行下列動作：

  - 從 EAC 的規則清單中，在 **\[規則\]** 清單中按一下您修改的規則，然後檢視詳細資料窗格。

  - 從Exchange 管理命令介面中，確認您修改的郵件流程規則成功執行下列命令以列出您修改的規則 （下面的範例驗證上述Exchange 管理命令介面範例中修改的規則） 的名稱以及內容：
    
        Get-TransportRule "Sender is a member of marketing" | Format-List Name,ExceptIfFrom

## 郵件流程規則屬性

您還可以使用 Set-transportrule 指令程式來修改您組織中的現有傳輸規則。下面是無法使用在 EAC 中，您可以變更屬性的清單。如需使用 Set-transportrule 指令程式來進行查看[Set-TransportRule](https://technet.microsoft.com/zh-tw/library/bb123534\(v=exchg.150\))這些變更的詳細資訊


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>在 EAC 中的條件名稱</th>
<th>Exchange 管理命令介面中的條件名稱</th>
<th>屬性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>停止處理規則</strong></p></td>
<td><p><code>StopRuleProcessing </code></p></td>
<td><p><code> Not applicable</code></p></td>
<td><p>可讓您停止處理其他規則</p></td>
</tr>
<tr class="even">
<td><p><strong>頁首/信封比對</strong></p></td>
<td><p><code>SenderAddressLocation </code></p></td>
<td><p>不適用</p></td>
<td><p>可讓您檢查 SMTP 郵件信封確保標頭及包圍相符項目</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><strong>稽核嚴重性</strong></p></td>
<td><p><code>SetAuditSeverity </code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>可讓您選取的稽核嚴重性層級</p></td>
</tr>
<tr class="even">
<td><p><strong>規則模式</strong></p></td>
<td><p><code>Mode</code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>可讓您設定規則模式</p></td>
</tr>
</tbody>
</table>


## 設定郵件流程規則的優先順序

在清單頂端規則最先處理。此規則的 **\[優先順序\]** 為 0。

## 使用 EAC 來設定規則的優先順序

1.  從 EAC 中，移至 **\[郵件流程\]** \> **\[規則\]**。這會依處理順序來顯示規則。

2.  選取規則，然後使用箭號，在清單中將規則上移或下移。

## 使用Exchange 管理命令介面來設定規則的優先順序

下列範例將「寄件者是行銷部門的成員」的優先順序設為 2：

    Set-TransportRule "Sender is a member of marketing" priority "2"

## 如何知道這是否正常運作？

若要確認您已成功修改的郵件流程規則，請執行下列動作：

  - 從 EAC 的規則清單中，查看規則的順序。

  - Exchange 管理命令介面，驗證規則的優先順序 （下面的範例驗證上述Exchange 管理命令介面範例中修改的規則）：
    
        Get-TransportRule * | Format-List Name,Priority

## 啟用或停用郵件流程規則

您在建立時啟用規則。您可以停用郵件流程規則。

## 使用 EAC 來啟用或停用郵件流程規則

1.  從 EAC 中，移至 **\[郵件流程\]** \> **\[規則\]**。

2.  若要停用規則，請清除其名稱旁邊的核取方塊。

3.  若要啟用已停用的規則，請選取其名稱旁邊的核取方塊。

## 若要啟用或停用郵件流程規則使用Exchange 管理命令介面

下列範例會停用郵件流程規則 「 寄件者是行銷部門成員 」：

    Disable-TransportRule "Sender is a member of marketing"

下列範例中啟用郵件流程規則 「 寄件者是行銷部門成員 」：

    Enable-TransportRule "Sender is a member of marketing"

## 如何知道這是否正常運作？

確認您已順利啟用或停用郵件流程規則，請執行下列動作：

  - 在 EAC 中檢視 **\[規則\]** 清單中的規則清單，並檢查 **\[開啟\]** 欄位中核取方塊的狀態。

  - 從Exchange 管理命令介面中，執行下列命令，將傳回的所有規則清單及其狀態您組織中：
    
        Get-TransportRule | Format-Table Name,State

## 移除郵件流程規則

## 使用 EAC 來移除郵件流程規則

1.  從 EAC 中，移至 **\[郵件流程\]** \> **\[規則\]**。

2.  選取您要移除的規則，然後按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

## 使用Exchange 管理命令介面來移除郵件流程規則

下列範例會移除郵件流程規則 「 寄件者是行銷部門成員 」：

    Remove-TransportRule "Sender is a member of marketing"

## 如何知道這是否正常運作？

若要確認您已成功移除郵件流程規則，請執行下列動作：

  - 在 EAC 中檢視 **\[規則\]** 清單中的規則，並驗證您移除的規則不再顯示。

  - 從Exchange 管理命令介面中，執行下列命令並確認您移除的規則不再列出：
    
        Get-TransportRule

## 監視規則使用

如果是使用 Exchange Online 或 Exchange Online Protection，您可以使用規則報告來檢查每一個規則的符合次數。必須選取規則的 **\[此規則使用的稽核嚴重性層級\]** 核取方塊，此規則才會納入報告中。您可以在線上查看報告，或下載所有郵件保護報告的 Excel 版本。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>報告中的大部分資料都在 24 小時內，但有些資料可能需要 5 天才會出現。</td>
</tr>
</tbody>
</table>


## 使用 Office 365 系統管理中心來產生規則報告

1.  在 Office 365 系統管理中心，選取 **\[報告\]**。

2.  在 **\[規則\]** 區段中，選取 **\[郵件排名最前面的規則相符\]** 或 **\[郵件的規則相符\]**。

若要深入了解，請參閱 ＜[檢視郵件保護報告](https://go.microsoft.com/fwlink/p/?linkid=402958)。

## 下載報告的 Excel 版本

1.  在 Office 365 系統管理中心的 \[報告\] 頁面中，選取 **\[郵件保護報告 (Excel)\]**。

2.  如果這是您第一次使用 Excel 郵件保護報告，索引標籤會開啟下載頁面。
    
    1.  選取 **\[下載\]** 來下載 Exchange Online 報告的 Microsoft Office 365 Excel 外掛程式。
    
    2.  開啟下載。
    
    3.  在 **\[Office 365 的郵件保護報告安裝程式\]** 對話方塊中，選取 **\[下一步\]**，接受授權合約的條款，然後選取 **\[下一步\]**。
    
    4.  選取您使用的服務，然後選取 **\[下一步\]**。
    
    5.  確認必要條件，然後選取 **\[下一步\]**。
    
    6.  選取 **\[安裝\]**。桌面上會建立報告的捷徑。

3.  在桌面上，選取 **\[Office 365 郵件保護報告\]**。

4.  在報告中，選取 **\[規則\]** 索引標籤。

## 匯入或匯出的郵件流程規則集合

您必須使用Exchange 管理命令介面匯入或匯出郵件流程規則集合。如需如何從 XML 檔案匯入的郵件流程規則集合，請參閱 ＜ [Import-TransportRuleCollection](https://technet.microsoft.com/zh-tw/library/bb123582\(v=exchg.150\))。如需如何將郵件流程規則集合匯出至 XML 檔案，請參閱 ＜ [Export-TransportRuleCollection](https://technet.microsoft.com/zh-tw/library/bb124410\(v=exchg.150\))。

## 需要其他協助嗎？

Exchange Online的資源：

[Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\))

[Exchange Online 中的郵件流程規則條件和例外狀況 (predicates)](https://technet.microsoft.com/zh-tw/library/jj919235\(v=exchg.150\))

[郵件流程規則動作在 Exchange Online](https://technet.microsoft.com/zh-tw/library/jj919237\(v=exchg.150\))

[傳輸和收件匣規則限制](https://go.microsoft.com/fwlink/p/?linkid=324584)

Exchange Online Protection的資源：

[Exchange Online Protection 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/dn271424\(v=exchg.150\))

[郵件流程規則條件和例外狀況 （述詞） 在 \[Exchange Online Protection](https://technet.microsoft.com/zh-tw/library/jj919234\(v=exchg.150\))

[郵件流程規則動作在 Exchange Online Protection](https://technet.microsoft.com/zh-tw/library/jj920117\(v=exchg.150\))

[傳輸和收件匣規則限制](https://go.microsoft.com/fwlink/p/?linkid=324584)

Exchange Server 2013 的資源：

[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[傳輸規則條件 （述詞）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[傳輸規則動作](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)


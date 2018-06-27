---
title: '管理原則提示: Exchange Online Help'
TOCTitle: 管理原則提示
ms:assetid: cec50a35-1d00-47b3-b72f-ac1bb0fd630e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619307(v=EXCHG.150)
ms:contentKeyID: 50472379
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理原則提示

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

原則祕訣對他們正在撰寫郵件時的電子郵件的寄件者顯示的資訊性通知。原則提示的用途是對他們可能違反商務作法或所建立的資料遺失防護 (DLP) 原則使用的強制執行原則的使用者教育訓練。下列程序可協助您開始使用原則提示。觀賞此影片以深入了解。

> [!VIDEO https://www.microsoft.com/zh-tw/videoplayer/embed/dd629bb7-063d-49f3-b7e1-8f2e0aa4de13]

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：30 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「資料外洩防護 (DLP) 」項目。

  - 原則提示將向符合下列條件的電子郵件寄件者顯示：
    
    1.  寄件者的郵件用戶端程式是 Microsoft Outlook 2013。如果貴組織已部署 Exchange 2013 SP1 或正在使用 Exchange Online，則原則提示也會顯示在 Outlook Web App 和 裝置的 OWA 中。
    
    2.  存在叫用原則提示通知的傳輸規則。您可以設定包含 \[以原則提示通知寄件者\] 動作的 DLP 原則，以建立這類傳輸規則。
    
    3.  傳輸代理程式所掃描的郵件標頭內容、郵件內文或郵件附件，符合以 DLP 原則或也包含原則提示通知規則的規則所設定的條件。換句話說，原則提示只會向造成相關規則採取行動的使用者顯示。

  - 如果不使用原則提示設定功能來自訂原則提示文字，將顯示系統內建的預設原則提示通知文字。若要深入了解預設文字，請參閱[原則提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)。

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

## 建立或修改僅通知的原則提示

此程序導致通知性質的原則提示在符合特定規則的情況下向電子郵件寄件者顯示。在 Microsoft Outlook 中，寄件者可使用 \[原則提示選項\] 對話方塊避免顯示此提示。若要設定自訂原則提示文字，請參閱 Create custom Policy Tip notification text。

## 使用 EAC 設定僅通知原則提示

1.  在 EAC 中，移至 **\[規範管理\]** \> **\[資料外洩防護\]**。

2.  按兩下顯示在原則清單的其中一個原則或反白顯示一個項目，然後選取 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[編輯 DLP 原則\]** 頁面上，選取 **\[規則\]**。

4.  若要將原則提示新增至現有規則，請反白顯示規則，然後選取 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。
    
    若要新增一個可完全自訂的空白規則，請依序選取 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 和選取 **\[建立新的規則\]**。

5.  在 **\[套用此規則情況\]** 中，選取 **\[郵件包含敏感資訊\]**。這是必要條件。

6.  依序選取 ![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")、敏感資訊類型、**\[新增\]** 和 **\[確定\]**，然後選取 **\[確定\]**。

7.  在 **\[執行下列動作\]** 方塊中，選取 **\[以原則提示通知寄件者\]**，然後在 **\[選擇封鎖還是可以傳送郵件\]** 下拉式清單中選取選項，然後選取 **\[確定\]**。

8.  如果您想要新增其他條件或動作，請在視窗底端選取 **\[其他選項\]**。
    
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
    <td>只能使用下列條件：
    <ul>
    <li><p><strong>SentTo （收件者是）</strong></p></li>
    <li><p><strong>SentToScope （收件者位於）</strong></p></li>
    <li><p><strong>從 （寄件者是）</strong></p></li>
    <li><p><strong>Frommemberof （寄件者是成員） 以下</strong></p></li>
    <li><p><strong>FromScope （寄件者位於）</strong></p></li>
    </ul>
    下列是不能使用的動作：
    <ul>
    <li><p><strong>RejectMessageReasonText （拒絕此郵件並包含說明）</strong></p></li>
    <li><p><strong>RejectMessageEnhancedStatusCode （拒絕接收郵件以增強型的狀態碼）</strong></p></li>
    <li><p><strong>DeletedMessage （刪除郵件而不通知任何人）</strong></p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>


9.  在 **\[選擇此規則的模式\]** 清單中，選取是否要強制執行規則。建議您先測試規則。

10. 選取 **\[儲存\]** 以完成規則的修改並儲存變更。

## 如何知道這是否正常運作？

若要確認您是否成功建立僅通知寄件者的原則提示，請進行下列步驟：

1.  在 EAC 中，移至 **\[規範管理\]** \> **\[資料外洩防護\]**。

2.  選取預期包含通知郵件的原則。

3.  選取 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")，然後選取 **\[規則\]**。

4.  選取預期包含通知郵件的特定規則。

5.  確認 \[通知寄件者\] 動作出現在規則摘要的下半部。

## 建立或修改封鎖郵件原則提示

此程序導致原則提示向電子郵件寄件者顯示，表示郵件遭拒，在問題狀況解除之前將不予寄送。寄件者可以使用一個選項，表示本身的電子郵件並不包含問題狀況。這也稱為誤判覆寫。如果寄件者如此表示，則郵件可從寄件匣寄出，使用者的報告也會受到稽核。不過，Exchange 將封鎖正在發送的郵件。若要設定自訂原則提示文字，請參閱 Create custom Policy Tip notification text。

## 使用 EAC 設定封鎖郵件原則提示

1.  在 EAC 中，移至 **\[規範管理\]** \> **\[資料外洩防護\]**。

2.  按兩下顯示在原則清單的其中一個原則或反白顯示一個項目，然後選取 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[編輯 DLP 原則\]** 頁面上，選取 **\[規則\]**。

4.  若要將原則提示新增至現有規則，請反白顯示規則，然後選取 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

5.  若要新增一個可完全自訂的空白規則，請選取 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

6.  若要新增將顯示原則提示的動作，請選取 **\[其他選項\]**，然後選取 **\[新增動作\]** 按鈕。

7.  從下拉式清單中，選取 \[以原則提示通知寄件者\]，然後選取 \[封鎖郵件\]。

8.  選取 **\[確定\]**，然後選取 **\[儲存\]** 以完成這項規則的修改並儲存變更。

## 如何知道這是否正常運作？

若要確認您是否成功建立拒絕郵件原則提示，請進行下列步驟：

1.  在 EAC 中，移至 **\[規範管理\]** \> **\[資料外洩防護\]**。

2.  選取一次以將您要包含的通知郵件反白顯示。

3.  選取 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")，然後選取 **\[規則\]**。

4.  選取一次以將您要包含的通知郵件之具體規則反白顯示。

5.  確認您的 \[通知寄件者無法傳送郵件\] 動作出現在規則摘要的下半部。

## 建立或修改不覆寫即封鎖原則提示

原則提示有四個選項可拒絕郵件，或避免郵件從寄件者的寄件匣寄出。若要深入了解這些選項，請參閱[原則提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)。

## 使用 EAC 設定不覆寫即封鎖原則提示

1.  在 EAC 中，移至 **\[規範管理\]** \> **\[資料外洩防護\]**。

2.  選取兩次顯示在原則清單的其中一個原則或反白顯示一個項目，然後選取 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[編輯 DLP 原則\]** 頁面上，選取 **\[規則\]**。

4.  若要將原則提示新增至現有規則，請反白顯示規則，然後選取 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。
    
    若要新增一個可完全自訂的空白規則，請選取 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，然後選取 **\[其他選項\]**。

5.  若要新增將顯示原則提示的動作，請選取 **\[新增動作\]** 按鈕。

6.  從下拉式清單中，選取 \[以原則提示通知寄件者\]，然後選取 \[封鎖郵件，但允許寄件者覆寫及傳送\]。

7.  選取 **\[確定\]**，然後選取 **\[儲存\]** 以完成這項規則的修改並儲存變更。

## 如何知道這是否正常運作？

若要確認您是否成功建立不覆寫即拒絕郵件原則提示，請進行下列步驟：

1.  在 EAC 中，移至 **\[規範管理\]** \> **\[資料外洩防護\]**。

2.  選取一次以將您要包含的通知郵件反白顯示。

3.  選取 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")，然後選取 **\[規則\]**。

4.  選取一次以將您要包含的通知郵件之具體規則反白顯示。

5.  確定您的 \[封鎖郵件，但允許寄件者覆寫及傳送\] 動作出現在規則摘要的下半部。

## 建立自訂原則提示通知文字

此選用程序將協助您自訂電子郵件寄件者在電子郵件程式中看見的原則提示通知文字。如果您這麼做，除非您也設定有動作會造成通知出現的 DLP 原則規則，否則自訂原則提示通知文字將不會顯示。請注意，如果不自訂原則提示通知文字，則會顯示預設系統原則提示通知。若要深入了解預設文字，請參閱[原則提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)。

## 使用 EAC 建立和管理自訂原則提示通知文字

1.  在 EAC 中，移至 **\[規範管理\]** \> **\[資料外洩防護\]**。

2.  選取 **\[原則提示設定\]**![原則提示設定](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "原則提示設定")。

3.  若要以您自己的自訂郵件新增原則提示，請選取 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。如需可用動作選擇的詳細資訊，請參閱[原則提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)。
    
    若要修改現有原則提示，請反白顯示該提示，然後選取 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。
    
    若要刪除現有原則提示，請反白顯示該提示，並選取 **\[刪除\]**![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")，然後確認您的動作。

4.  選取 **\[儲存\]** 以完成原則提示的修改並儲存變更。

5.  選取 **\[關閉\]** 以完成原則提示的管理並儲存變更。

## 使用命令介面建立自訂原則提示通知文字

下列範例建立將封鎖郵件寄送的新英文原則提示。自訂原則提示的文字變更為下列值：「此郵件似乎包含受限制的內容，將不予寄送。」

    New-PolicyTipConfig -Name en\Reject -Value "This message appears to contain restricted content and will not be delivered."

如需 DLP 指令程式的詳細資訊，請參閱[原則及符合性命令指令程式](https://technet.microsoft.com/zh-tw/library/dd298082\(v=exchg.150\))。

## 使用命令介面修改自訂原則提示通知文字

下列範例修改現有英文僅通知原則提示。此自訂原則提示的文字將變更為「不建議以電子郵件傳送銀行帳號」。

    Set-PolicyTipConfig en\NotifyOnly "Sending bank account numbers in email is not recommended."

如需 DLP 指令程式的詳細資訊，請參閱[原則及符合性命令指令程式](https://technet.microsoft.com/zh-tw/library/dd298082\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否成功建立自訂原則提示文字，請進行下列步驟：

1.  在 EAC 中，移至 **\[規範管理\]** \> **\[資料外洩防護\]**。

2.  選取 **\[原則提示設定\]**![原則提示設定](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "原則提示設定")。

3.  選取 **\[重新整理\]**![重新整理圖示](images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "重新整理圖示")。

4.  確認您的動作、地區設定及該地區設定出現在清單中的文字。

## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[原則提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)

[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange 2013

[Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\)) Exchange Online

[Exchange 2010 郵件提示](https://go.microsoft.com/fwlink/?linkid=265179)


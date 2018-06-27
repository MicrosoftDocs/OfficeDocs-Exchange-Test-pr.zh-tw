---
title: '管理郵件核准: Exchange Online Help'
TOCTitle: 管理郵件核准
ms:assetid: 43a89f71-8002-4cb0-b3c8-1c2b2597f227
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd297936(v=EXCHG.150)
ms:contentKeyID: 50473144
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理郵件核准

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-05-04_

在傳送郵件之前，由另一個人監督郵件有時很合理。您可以 Exchange 系統管理員的身分進行此設定。此程序稱為「仲裁」，而核准者稱為「仲裁者」。視哪些郵件需要核准而言，您可以使用以下兩種方法之一：

  - 變更通訊群組屬性

  - 建立郵件流程規則

本文將說明：

  - 如何決定要使用哪一個核准方法

  - 核准程序的運作方式

若要了解如何實作常見案例，請參閱[常見的郵件核准案例](common-message-approval-scenarios-exchange-2013-help.md)。

## 如何決定要使用哪一個核准方法

以下是兩種郵件核准方法的比較。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>您要執行的工作</th>
<th>方法</th>
<th>第一個步驟</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>建立仲裁通訊群組，群組的所有郵件必須在此核准。</p></td>
<td><p>設定通訊群組的郵件核准。</p></td>
<td><p>移至 Exchange 系統管理中心 (EAC) &gt; [收件者] &gt; [群組]，編輯通訊群組，然後選取 [郵件核准]。</p></td>
</tr>
<tr class="even">
<td><p>需要核准符合特定條件或傳送給特定人員的郵件。</p></td>
<td><p>使用 [轉寄要核准的郵件] 動作建立傳輸規則。</p>
<p>您可以指定郵件條件，包括文字模式、寄件者和收件者。您的準則也可以包含例外狀況。</p></td>
<td><p>移至 EAC &gt; [郵件流程] &gt; [規則]。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 核准程序的運作方式

當某人傳送郵件給需要核准的人員或群組時，如果他們使用 Outlook Web Access，他們會接獲通知，表示其郵件可能延遲。

![顯示訊息核准通知的訊息](images/Dd297936.80e2e5f1-0a1e-4c37-9076-794581155405(EXCHG.150).png "顯示訊息核准通知的訊息")

仲裁者會收到一封電子郵件，要求核准或拒絕郵件。郵件的內文包含用以核准或拒絕郵件的按鈕，而附件包含要檢閱的原始郵件。

![核准要求訊息，包括附件](images/Dd297936.bf517f5a-b10e-40df-a48a-403b395b5962(EXCHG.150).png "核准要求訊息，包括附件")

仲裁者可以採取三個動作之一：

![顯示核准訊息之選項的工作流程](images/Dd297936.dc7a6ca9-c67d-487a-8713-4d628e07f4b3(EXCHG.150).png "顯示核准訊息之選項的工作流程")

1.  一旦核准，郵件就會送給預定的原始收件者。原始寄件者不會收到通知。

2.  如果遭到拒絕，就會傳送拒絕郵件給寄件者。仲裁者可以新增說明：
    
    ![拒絕通知，附有仲裁者的註解](images/Dd297936.a663d36a-c67d-4155-b8f6-4b5dc8e105d9(EXCHG.150).png "拒絕通知，附有仲裁者的註解")  

3.  如果核准者刪除或略過核准郵件，就會將過期郵件傳送給寄件者。這在 Exchange Online 中發生於兩天後，而在 Exchange Server 2013 中發生於五天後。(在 Exchange Server 2013 中，您可以變更此時間週期)。

等待核准的郵件會暫時儲存在稱為「仲裁信箱」的系統信箱中。在仲裁者決定要核准或拒絕此郵件、刪除核准郵件，或讓核准郵件到期之前，原始郵件都會保留在仲裁信箱中。

回到頁首

## 問題和解答

**通訊群組的核准者與擁有者之間的差異為何？**

通訊群組的擁有者負責管理通訊群組成員資格，但是無法仲裁傳送給通訊群組的郵件。例如，IT 人員可能是「所有員工」通訊群組的擁有者，但只能將人力資源主管設定為仲裁者。

**仲裁者或核准者將郵件傳送給通訊群組時，會發生什麼情況？**

郵件會略過核准程序，直接傳送到群組。

**只有部分的收件者需要核准時，會發生什麼情況？**

只有部分的收件者需要核准時，您可以將郵件傳送給一組收件者。假設要將郵件傳送給 12 位收件者，其中一個是仲裁通訊群組。郵件就會自動分成兩份。其中一個郵件會立即傳遞給不需要核准的 11 位收件者，而第二個郵件會提交到仲裁通訊群組的核准程序。 如果要將郵件傳送給多個仲裁收件者，則會針對每個仲裁收件者自動建立個別的郵件副本，而每個副本都會經歷適當的核准程序。

**如果我的通訊群組包含需要核准的仲裁收件者，要怎麼做？**

通訊群組可以包含也需要核准的仲裁收件者。在此情況下，核准傳送到通訊群組的郵件後，便會針對屬於通訊群組成員的各個仲裁收件者分別進行核准。然而，核准傳送到仲裁通訊群組的郵件後，您也可以啟用通訊群組成員的自動核准。若要這麼做，請使用 [Set-DistributionGroup](https://technet.microsoft.com/zh-tw/library/bb124955\(v=exchg.150\)) Cmdlet 上的 *BypassNestedModerationEnabled* 參數。

**如果我們有自己的 Exchange Server，此程序是否有所不同？**

根據預設，每個 Exchange 組織使用一個仲裁信箱。如果您有自己的 Exchange Server 且需要更多仲裁信箱進行負載平衡，請依照[管理及疑難排解郵件核准](manage-and-troubleshoot-message-approval-exchange-2013-help.md)中的指示新增仲裁信箱。仲裁信箱是系統信箱，不需要 Exchange 授權。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>如果您有Exchange 2007：</strong>Microsoft Exchange Server 2007 不支援仲裁收件者。如果傳送給仲裁通訊群組的郵件在 Exchange 2007 集線傳輸伺服器上展開，則郵件會略過仲裁並傳遞給通訊群組的所有成員。如果您的 Exchange 組織中有 Exchange 2007 集線傳輸伺服器，請務必將一個 Exchange Server 2013 信箱伺服器委派為仲裁通訊群組的擴充伺服器。這樣可確保所有傳送給通訊群組的郵件都經過仲裁。</td>
</tr>
</tbody>
</table>


回到頁首

## 需要其他資訊？

[管理郵件流程規則](manage-mail-flow-rules-exchange-2013-help.md)

[Exchange 2013 的 Exchange 管理命令介面快速參考](exchange-management-shell-quick-reference-for-exchange-2013-exchange-2013-help.md)

[Exchange Online PowerShell](https://technet.microsoft.com/zh-tw/library/jj200677\(v=exchg.150\))


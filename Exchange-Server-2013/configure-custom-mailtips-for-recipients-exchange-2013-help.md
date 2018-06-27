---
title: '設定收件者的自訂郵件提示: Exchange Online Help'
TOCTitle: 設定收件者的自訂郵件提示
ms:assetid: df8ee7ae-2486-4890-b057-cda87b4cb1ec
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638199(v=EXCHG.150)
ms:contentKeyID: 52062420
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定收件者的自訂郵件提示

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-06-01_

「郵件提示」是指使用者在編寫電子郵件的過程中執行下列任何動作時，在 Outlook Web App 和 Microsoft Outlook 2010 或更新版本的資訊列中對使用者顯示的參考訊息：

  - 新增收件者

  - 新增附件

  - 回覆或全部回覆

  - 從 \[草稿\] 資料夾開啟已經傳送給收件者的郵件

除了可用的內建郵件提示之外，您也可以為所有類型的收件者建立自訂的郵件提示。如需內建郵件提示的詳細資訊，請參閱[MailTips](mailtips-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「郵件提示」項目。

  - 您可以在 Exchange 系統管理中心 (EAC) 或命令介面中設定主要郵件提示。不過，您只能在命令介面中設定額外的郵件提示翻譯。

  - 當您對收件者新增郵件提示時，會發生兩個情形：
    
      - 自動在文字中加入 HTML 標記。例如，如果您輸入文字：`This mailbox is not monitored`，郵件提示會自動變成：`<html><body>This mailbox is not monitored</body></html>`。不支援郵件提示中的其他 HTML 標記。
    
      - 此文字會自動新增至收件者的 *MailTipTranslations* 內容做為預設值。如果您修改郵件提示文字，*MailTipTranslations* 內容中的預設值會自動更新。

  - 郵件提示的長度不能超過 175 個顯示的字元。

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

## 設定收件者的郵件提示

## 使用 EAC 來設定收件者的郵件提示

1.  在 EAC 中，瀏覽至 \[收件者\]。

2.  根據收件者類型來選取下列任一個收件者索引標籤：
    
      - **信箱**
    
      - **群組**
    
      - **資源**
    
      - **連絡人**
    
      - **Shared**

3.  在收件者索引標籤上選取您要修改的收件者，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  在出現的收件者內容頁面上，按一下 **\[郵件提示\]**。

5.  輸入郵件提示的文字。完成後，按一下 **\[儲存\]**。

## 使用命令介面來設定收件者的郵件提示

若要設定收件者的郵件提示，請使用下列語法。

    Set-<RecipientType> <RecipientIdentity> -MailTip "<MailTip text>"

*\<RecipientType\>* 可以是任何類型的收件者。例如，`Mailbox`、`MailUser`、`MailContact`、`DistributionGroup` 或 `DynamicDistributionGroup`。

例如，假設您有一個名為「服務台」的信箱供使用者提交支援要求，而且保證的回應時間為兩小時。若要設定說明此信箱的自訂郵件提示，請執行下列命令：

    Set-Mailbox "Help Desk" -MailTip "A Help Desk representative will contact you within 2 hours."

## 使用命令介面來設定其他使用不同語言的郵件提示

若要設定其他郵件提示翻譯，但不影響現有的郵件提示文字或其他現有的郵件提示翻譯，請使用以下語法：

    Set-<RecipientType> -MailTipTranslations @{Add="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...; Remove="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...}

*\<culture\>* 是與該語言相關聯的有效 ISO 639 雙字母式文化特性代碼。

例如，假設名為「通知」的信箱目前擁有郵件提示：「這個信箱並未受監視」。若要加入西班牙文翻譯，請執行下列命令：

    Set-Mailbox -MailTipTranslations @{Add="ES:Esta caja no se supervisa."}

## 如何知道這是否正常運作？

若要確認您已成功為收件者設定郵件提示，請執行下列動作：

1.  在 Outlook Web App 或 Outlook 2010 或更新版本中，撰寫已指定該收信者為收信人的電子郵件，但不要傳送。

2.  確認郵件提示出現在資訊列中。

3.  如果您已設定其他郵件提示翻譯，請在語言設定與郵件提示翻譯語言相符的 Outlook Web App 中撰寫郵件，以確認結果。


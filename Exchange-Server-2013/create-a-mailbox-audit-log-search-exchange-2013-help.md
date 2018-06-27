---
title: '建立信箱稽核記錄搜尋: Exchange 2013 Help'
TOCTitle: 建立信箱稽核記錄搜尋
ms:assetid: 48ba22cf-b1f2-4dbc-98fc-fed22d97db14
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff461929(v=EXCHG.150)
ms:contentKeyID: 50473169
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立信箱稽核記錄搜尋

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-11_

您可以建立信箱稽核記錄搜尋，以非同步方式搜尋一個或多個信箱，並透過電子郵件將搜尋結果作為 XML 檔案傳送給指定的位址。

若要在信箱稽核記錄中搜尋單一信箱，並在命令介面中顯示結果，請參閱[搜尋信箱的信箱稽核記錄](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md)。

如需與信箱稽核記錄相關的其他管理工作，請參閱[信箱稽核記錄程序](mailbox-audit-logging-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「信箱稽核記錄」項目。

  - 根據預設，信箱稽核記錄已停用所有的信箱。您想要稽核的信箱，您必須啟用稽核記錄功能並指定您想要稽核的信箱擁有者、 委派、 或系統管理員動作。如需詳細資訊，請參閱[啟用或停用信箱稽核記錄功能信箱](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)。

  - 您無法使用 EAC 來搜尋信箱稽核記錄擁有者存取的。在 EAC 中的 \[稽核\] 區段中包含的非擁有者信箱存取報告和也可讓您搜尋並匯出非擁有者存取事件。

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

## 使用 EAC 建立信箱稽核記錄搜尋

1.  瀏覽至 \[規範管理\] \> \[稽核\]。

2.  在清單檢視中，選擇 \[匯出信箱稽核記錄\]。

3.  在 \[匯出信箱稽核記錄\] 中，完成下列欄位然後按一下 \[匯出\]：
    
      - **開始日期**
    
      - **結束日期**
    
      - **搜尋這些信箱或留空白以尋找所有由非擁有者存取的信箱**
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>根據您的組織中的信箱數量以及每個信箱中的信箱稽核記錄資料總數而定，搜尋所有信箱可能需要一段時間。</td>
        </tr>
        </tbody>
        </table>
    
      - **搜尋存取方法**
        
        從下列存取類型中選擇您想要搜尋的事件：
        
          - **所有非擁有者**
        
          - **外部使用者**
        
          - **管理員與委派的使用者**
        
          - **管理員**
    
      - **傳送稽核報告至**

## 使用命令介面建立信箱稽核記錄搜尋

若需使用命令介面來建立信箱稽核記錄搜尋的方法範例，請參閱 **New-MailboxAuditLogSearch** 中的 [Example 1](https://technet.microsoft.com/zh-tw/95365cab-bbb2-4a64-8e8f-1c89fa9e0352\(exchg.150\)#example1)。


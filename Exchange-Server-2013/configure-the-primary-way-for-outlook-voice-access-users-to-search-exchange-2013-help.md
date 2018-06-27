---
title: '設定 Outlook 語音存取使用者要搜尋的主要方法: Exchange Online Help'
TOCTitle: 設定 Outlook 語音存取使用者要搜尋的主要方法
ms:assetid: 3d93a037-5820-41d3-9206-69f534414daf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997563(v=EXCHG.150)
ms:contentKeyID: 50472933
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Outlook 語音存取使用者要搜尋的主要方法

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-21_

當您建立整合通訊 (UM) 撥號時，您可以設定的主要和次要方式來電者可搜尋的名稱來尋找使用者撥打電話Outlook語音存取號碼\] 或 \[與撥號對應表關聯的 UM 自動語音應答時。來電者可以使用按鍵式輸入來尋找已啟用 UM 的使用者。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>None</strong>不是來電者可搜尋的名稱的主要方法可用的選項。<strong>無</strong>選取時可以尋求名稱的次要方法，主要的方式會提供給來電者。如果您設定這兩個主要和次要方式來電者可搜尋的名稱，他們會出現提示的這兩種方法。</td>
</tr>
</tbody>
</table>


如需與 UM 撥號對應表相關的其他管理工作，請參閱 [UM 撥號對應表規劃程序](um-dial-plan-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。 如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

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

## 使用 EAC 變更依主要名稱撥號方法

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面上，按一下 \[設定\]。

4.  在 \[設定\] 中，\[搜尋名稱的主要方法\] 下，使用下拉式清單選擇您想要的選項：
    
      - \[姓氏 名字\] (預設)
    
      - **名字 姓氏**
    
      - **SMTP 位址**

5.  按一下 \[儲存\]。

## 使用命令介面變更依主要名稱撥號方法

此範例會設定主要的撥號對應表名稱`FirstLast`方法。這可讓來電者Outlook語音存取號碼\] 或 \[UM 自動語音應答的電話相關聯的撥號對應表及其在前由已啟用 UM 的使用者搜尋並再姓氏。

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary FirstLast

此範例會設定主要的撥號對應表名稱`LastFirst`方法。這可讓來電者與搜尋的啟用 UM 之使用者依其上次然後名字撥號Outlook語音存取號碼\] 或 \[UM 自動語音應答的電話相關聯。

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary LastFirst 

此範例會設定主要的撥號對應表名稱`SMTP address`方法。這可讓來電者撥打Outlook語音存取號碼或 UM 自動語音應答相關聯的撥號對應表來搜尋已啟用 UM 之使用者及其 SMTP 地址。

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary SMTPAddress


---
title: '設定信箱的郵件轉寄: Exchange Online Help'
TOCTitle: 設定信箱的郵件轉寄
ms:assetid: c7a7afaf-577e-49d6-8cee-bb4c4a5d570b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351134(v=EXCHG.150)
ms:contentKeyID: 50554094
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 設定信箱的郵件轉寄

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

郵件轉寄可讓您設定將傳送至某個信箱的電子郵件轉寄至另一個使用者的信箱 (組織內或組織外)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用商務用 Office 365，您的電子郵件轉寄功能應透過 <a href="https://go.microsoft.com/fwlink/p/?linkid=834774">Office 365 系統管理中心：在 Office 365 中設定電子郵件轉寄功能</a>進行設定</td>
</tr>
</tbody>
</table>


如果您的組織使用內部部署 Exchange 或混合式 Exchange 環境，您應使用內部部署 Exchange 系統管理中心 (EAC) 來建立及管理共用信箱。

## 使用 Exchange 系統管理中心 來設定郵件轉寄

您可以使用 Exchange 系統管理中心 (EAC) 將電子郵件轉寄功能設定為單一內部收件者、單一外部收件者 (使用郵件連絡人)，或多位收件者 (使用通訊群組)。

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[收件者權限](recipients-permissions-exchange-2013-help.md) 主題中的「收件者佈建權限」項目。

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下或點選您想設定郵件轉寄的信箱，然後按一下或點選 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱的內容頁上，按一下 \[信箱功能\]。

4.  在 **\[郵件流程\]** 下，選取 **\[檢視詳細資料\]** 以檢視或變更電子郵件轉寄的設定。
    
    在此頁面上，您可以設定可供使用者傳送郵件的收件者人數上限。若是內部部署的 Exchange 組織，收件者限制則無上限。若是 Exchange Online 的組織，上限為 500 位收件者。

5.  勾選 \[啟用轉寄\] 核取方塊，然後點選或按一下 \[瀏覽\]。

6.  在 \[選取收件者\] 頁面上，選取您要轉寄傳送所有電子郵件的目標使用者。如果希望收件者和轉寄電子郵件地址都收到所傳送之電子郵件的副本，請選取 \[將郵件傳遞到轉寄地址和信箱\] 核取方塊。然後按一下或點選 \[確認\] 與 \[儲存\]。

如果要將郵件轉寄給組織外部的地址呢？或是將郵件轉寄給多位收件者呢？當然沒問題！

  - **外部地址**建立郵件連絡人，然後在上述步驟中的 \[選取收件者\] 頁面上選取郵件連絡人。需要了解如何建立郵件連絡人嗎？請參閱＜[管理郵件連絡人](manage-mail-contacts-exchange-2013-help.md)＞。

  - **多位收件者**建立通訊群組，並將收件者加入其中，然後在上述步驟中的 \[選取收件者\] 頁面上選取該郵件連絡人。需要了解如何建立郵件連絡人嗎？請參閱＜[建立並管理通訊群組](create-and-manage-distribution-groups-exchange-2013-help.md)＞。

## 如何才能了解這是否正常運作？

若要確定您已成功設定郵件轉寄，請執行下列其中一個動作：

1.  在 EAC 中，前往 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下或點選您已設定電子郵件轉寄的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱內容頁面上，按一下或點選 \[信箱功能\]。

4.  在 \[郵件流程\] 下，按一下或點選 \[檢視詳細資料\] 以檢視郵件轉寄設定。

## 其他資訊

這個主題適用於系統管理員。如果您想要將您自己的電子郵件轉寄給其他收件者，請參閱下列主題：

  - [將電子郵件轉寄給其他電子郵件帳戶](https://go.microsoft.com/fwlink/p/?linkid=510866)

  - [使用規則管理電子郵件](https://go.microsoft.com/fwlink/p/?linkid=510869)

如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。


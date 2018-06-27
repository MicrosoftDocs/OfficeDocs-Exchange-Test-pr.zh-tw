---
title: '群組計量 」 和 「 郵件提示: Exchange 2013 Help'
TOCTitle: 群組計量 」 和 「 郵件提示
ms:assetid: 74a55072-4ba9-45bb-a18f-41afbf3de30b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ674302(v=EXCHG.150)
ms:contentKeyID: 50473505
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 群組計量 」 和 「 郵件提示

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-16_

群組計量為集合中的通訊群組和動態通訊群組在組織中的關於下列資料：

  - 成員的數目

  - 您組織外部的成員的數目

群組計量資料用來在 Microsoft Exchange Server 2013支援郵件提示。寄件提醒 」 是指他們正在撰寫郵件時顯示寄件者。如需郵件提示，包括寄件提醒Exchange 2013，提供的完整清單的詳細資訊請參閱[MailTips](mailtips-exchange-2013-help.md)。

群組計量資料會使用下列的郵件提示：

  - **大型對象**  寄件者新增其成員資格計數被視為大型對象為您組織中設定的通訊群組時顯示此郵件提示。根據預設，任何 25 個以上的收件者的郵件會被視為大型對象。

  - **外部收件者**  寄件者新增具有外部組織成員的通訊群組時顯示此郵件提示。

每次寄件者新增至郵件的收件者的郵件提示進行評估。若要提供此資訊， Exchange計算群組計量資料為可以排程為定期貴組織的營業時間以外執行背景處理程序。評估收件者的寄件提醒、 時Exchange讀取群組計量資料。

## 群組計量產生

在Exchange 2013、 群組計量資料會儲存在 Active Directory 群組物件上的**msExchGroupMemberCount**和**msExchGroupExternalMemberCount**屬性。下列檔案在 %exchangeinstallpath%GroupMetrics 資料夾中的也是群組計量相關聯：

  - **Cookie\_*\<nnnnnnnn\>*.dsc**  此文字檔案包含設定為可產生群組計量資料，以及上次成功的群組計量產生的信箱伺服器的相關資訊。這可讓群組計量產生的最後一個群組計量產生後已變更的群組資料。

  - **ChangedGroups.txt**這個檔案包含已更新群組計量資料產生的最後一個時間的群組清單。

群組計量產生的處理方式的仲裁信箱，也稱為組織信箱。仲裁信箱上的*GMGen*參數設為`$true`、 時的仲裁信箱負責產生群組計量資料。

信箱伺服器所產生的完整群組計量資料的所有通訊群組和動態通訊群組第一次群組計量的信箱助理員執行及累加更新已修改自上次完整產生的任何群組。根據預設，每天一次隨機 Exchange 伺服器的工作負載時淺色產生群組計量資料。如果工作負載正比高，可能會被略過群組計量產生。

若要設定群組計量產生，請參閱[設定群組計量](configure-group-metrics-exchange-2013-help.md)。


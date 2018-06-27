---
title: '共用信箱: Exchange 2013 Help'
TOCTitle: 共用信箱
ms:assetid: 1d71c01b-e261-408e-a633-1d1c9d00032a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150498(v=EXCHG.150)
ms:contentKeyID: 50472771
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 共用信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-06-04_

了解 Exchange 共用信箱的 Microsoft Exchange Server 2013\]、 使用方式、 原因及如何轉換到 Exchange 委派的信箱共用信箱。

「共用信箱」是指可讓多位使用者用來讀取及傳送電子郵件的信箱。共用信箱也可以用來提供一般行事曆，讓多位使用者可以排程及檢視假期時間或排班表。

共用信箱在行動裝置上不支援。

**為什麼要設定共用信箱？**

  - 提供一般電子郵件地址 (例如 info@contoso.com 或 sales@contoso.com)，客戶可以使用這個電子郵件地址來查詢公司的相關資訊。

  - 允許為員工提供集中式服務的部門 (例如服務台、人力資源或列印服務) 回應員工的問題。

  - 允許多位使用者監視並回覆傳送到某個電子郵件地址 (例如，服務台專門使用的地址) 的電子郵件。

## 什麼是共用信箱？

共用的信箱是一種都不會有自己的使用者名稱和密碼的使用者信箱。因此，使用者無法登入其它們直接。若要存取共用的信箱，使用者必須先取得信箱傳送\] 或 \[完整存取權限。一旦完成，使用者登入他們自己的信箱並再將它新增至其 Outlook 設定檔存取共用的信箱。在 Exchange 2003 及舊版共用的信箱已只是一般信箱的系統管理員可以授與委派存取。共用的信箱從 Exchange 2007 開始，變成他們自己的收件者類型：

  - **RecipientType:** UserMailbox

  - **RecipientTypeDetails:** SharedMailbox

在舊版 Exchange 中，建立共用的信箱已多步驟的程序之前，才可完成之工作的一些使用 Exchange 管理命令介面。在 Exchange 2013，您可以使用 Exchange 系統管理中心 (EAC) 一步驟中建立共用的信箱。如需詳細資訊，請參閱[建立共用的信箱](create-a-shared-mailbox-exchange-2013-help.md)。事實上，EAC 具有完全專設共用信箱的功能區。剛瀏覽至 \[**收件者**\>**共用信箱**移轉至檢視的所有管理工作共用信箱。

以下是可與共用信箱搭配使用的權限。

  - **完整存取權**   「完整存取權」權限可讓使用者開啟共用信箱，做為該信箱的擁有者。在存取登入共用信箱後，使用者可以建立行事曆項目；讀取、檢視、刪除和變更電子郵件；建立工作和行事曆連絡人。不過，除非具有「完整存取權」權限的使用者也有「傳送為」或「代理傳送者」權限，否則無法從共用信箱傳送電子郵件。

  - **傳送為**   「傳送為」權限可讓使用者在傳送郵件時模擬共用信箱。例如，如果 Kweku 登入共用信箱 Marketing Department 並傳送一封電子郵件，看起來就像是 Marketing Department 傳送該電子郵件。

  - **代理傳送者**   「代理傳送者」權限可讓使用者代表共用信箱傳送電子郵件。例如，如果 John 登入共用信箱 Reception Building 32 並傳送一封電子郵件，看起來該電子郵件就像由「John 代表 Reception Building 32」傳送。您無法使用 EAC 授與「代理傳送者」權限，您必須使用 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\)) Cmdlet 搭配 *GrantSendonBehalf* 參數。

## 轉換共用信箱

在舊版的 Exchange 中，您可以使用一般的信箱為委派信箱。如果您有委派信箱，您可以使用命令介面將轉換那些委派信箱移轉至共用信箱。如需詳細資訊，請參閱[轉換信箱](convert-a-mailbox-exchange-2013-help.md)。


---
title: '部署公用資料夾時的考量: Exchange 2013 Help'
TOCTitle: 部署公用資料夾時的考量
ms:assetid: 2e416eed-b88f-45db-a482-1232fd2610fa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn957481(v=EXCHG.150)
ms:contentKeyID: 65012395
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 部署公用資料夾時的考量

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-07-12_

雖然使用 Exchange 2013 公用資料夾的許多好處，但有幾點考量您的組織中實作它們之前。

## 公用資料夾的部署考量

本文包含考慮在組織中部署公用資料夾之前特別是如果您要在有大量的公用資料夾的因素。Exchange 2013 現在可支援最多一個萬個公用資料夾。

  - 公用資料夾中的活動直接影響所在資料夾所在的公用資料夾信箱的負載。若要避免用戶端連線問題，例如高延遲或無法存取公用資料夾，建議下列程序：
    
      - 不讓超過 50%的信箱大小限制的公用資料夾信箱。如果發生這種情況請考慮將一些公用資料夾移至新的公用資料夾信箱使用`Split-PublicFolderMailbox.ps1`指令碼位於 Exchange 2013 伺服器上的 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts 資料夾中。
    
      - 請考慮將大量使用的公用資料夾移到專用的公用資料夾信箱。
    
      - 從提供公用資料夾階層中排除頻繁公用資料夾。您可以藉由使用**Set-Mailbox**指令程式的公用資料夾信箱上設定*IsExcludedFromServingHierarchy*屬性來這麼做。
    
      - 大型組織中具有許多公用資料夾，請考慮新增額外的公用資料夾信箱來分散的服務公用資料夾階層要求的負載。

  - 若要改善可用性信箱的 DAG 中的主要公用資料夾信箱的位置。主要公用資料夾信箱為公用資料夾階層的代表性複本。

  - 將 DAG 中的次要公用資料夾信箱或經常備份的信箱。

  - 將公用資料夾信箱為最接近的使用者會存取在公用資料夾內容的地理位置中。

  - 在使用者的信箱使用 DefaultPublicFolderMailbox 屬性來指定公用資料夾信箱接近其改善公用資料夾階層存取時間。這會防止這些使用者從其他地理位置中的公用資料夾信箱擷取公用資料夾階層。

  - 在部署中具有超過 50 個次要公用資料夾信箱，我們建議您不要將儲存在公用資料夾內容中的主要公用資料夾信箱。這是要使用的次要公用資料夾信箱同步處理階層 dedicates 主要公用資料夾信箱。

  - Exchange 2013 不再支援公用資料夾資料庫。因此，具有 Exchange 2013 信箱的 Outlook Web App 使用者將無法存取 Exchange 2010 或 Exchange 2007 公用資料夾。Exchange 2013 使用者可以存取 Exchange 2010 或 Exchange 2007 公用資料夾與 Outlook 或 Outlook for mac。

  - Outlook Web App 支援，但有限制。您可以新增和移除我的最愛公用資料夾並執行項目層級作業，例如建立、 編輯、 刪除文章及回覆的文章。不過，您無法建立或刪除公用資料夾從 Outlook Web App。此外，唯一的電子郵件、 文章、 行事曆及連絡人公用資料夾可新增至 Outlook Web App 中的 \[我的最愛\] 清單。

  - 您可以對公用資料夾內容執行全文搜尋，但無法在多個公用資料夾之間搜尋公用資料夾內容，Exchange 搜尋也未對內容編制索引。

  - 您必須使用 Outlook 2007 或更新版本才能存取 Exchange 2013 伺服器上的公用資料夾。

  - 公用資料夾信箱不支援保留原則。


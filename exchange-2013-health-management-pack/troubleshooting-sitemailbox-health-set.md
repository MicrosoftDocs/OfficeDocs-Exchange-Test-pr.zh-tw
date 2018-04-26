---
title: 疑難排解 SiteMailbox 健康情況設定
TOCTitle: 疑難排解 SiteMailbox 健康情況設定
ms:assetid: ac00985c-c9a5-44bf-b152-4b99d8ae24ed
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.sitemailbox(v=EXCHG.150)
ms:contentKeyID: 53276411
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 SiteMailbox 健康情況設定

 

_**適用版本：**Exchange Server 2013, Project Server 2013_

_**上次修改主題的時間：**2013-02-11_

SiteMailbox 健全設定會監控您組織中站台信箱的整體健康狀況和可存取性。

如果您收到警示指出 SiteMailbox 狀況不良，這表示使用者信箱的內容不在同步狀態。

## 說明

SiteMailbox 監控系統接收被動同步處理結果從背景同步處理服務。這個系統不使用任何探查。被動同步處理結果會寫入到 SiteMailbox 每個同步處理嘗試後監視系統。下列事件發生時，也會觸發同步處理：

  - 使用者利用 Outlook 或 Outlook Web App 存取其站台信箱

  - 您執行 **Update-SiteMailbox** 命令

  - 您開啟 \[Outlook Web App 選項\] 視窗，接著按一下所選站台信箱 **\[同步狀態\]** 頁面上的 **\[啟動同步\]** 按鈕

如需更新 SiteMailbox 指令程式的詳細資訊，請參閱： [Update-SiteMailbox](https://technet.microsoft.com/zh-tw/library/jj218690\(v=exchg.150\))

如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 常見問題

整個網站擴張同步處理問題發生時同步處理監視服務通常會觸發提醒。不會在單一站台信箱同步處理失敗時傳送通知。若要決定單一站台信箱的上方臨界值提醒的原因，建議您檢閱網站信箱同步處理記錄檔。

## 使用者動作

服務可能在發出警示之後已復原。因此，當您收到警示指出健全設定狀況不良時，請先確認問題仍然存在。如果問題確實存在，請執行以下幾節所列出的適當復原動作。

## 確認問題仍然存在

1.  識別警示中的健全設定名稱和伺服器名稱。

2.  訊息詳細資料會提供造成警示確切原因的相關資訊。在大部分情況下，訊息詳細資料會提供足夠的疑難排解資訊來找出根本原因。如果訊息詳細資料不清楚，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要擷取有關 server1.contoso.com 的 SiteMailbox 健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "SiteMailbox"}
    
    2.  檢閱命令輸出，以判斷是哪個監視器回報錯誤。發出警示之監視器的 **AlertValue** 值會是 `Unhealthy`。

## 疑難排解步驟

當您從健全設定收到警示時，電子郵件包含下列資訊：

  - 傳送警示的伺服器名稱

  - 警示的發生日期和時間

  - 所使用的驗證機制及認證資訊

  - 上一個錯誤的完整例外狀況追蹤，包括診斷資料與特定的 HTTP 標頭資訊  
    
    **附註**  您可以使用完整的例外狀況追蹤中的資訊，以協助疑難排解問題。探查所產生的例外狀況包含描述探查失敗的原因失敗原因。

**背景同步處理錯誤**

當背景同步處理失敗時，您會收到與下列類似的警示：

站台信箱背景同步處理失敗，至少有 25%: 41 移出 87 嘗試失敗。範例同步處理結果：

\[郵件： 遠端伺服器傳回錯誤： (401) 未經授權。\]\[\] Type:System.Net.WebException

此警示就會觸發時失敗擁有舊的四個小時期間發生的同步處理的普遍高百分比。若要避免 false 負片，期間舊的四個小時 15 分鐘視窗內符合下列條件時才傳送通知：

  - 在 15 分鐘期間至少發生 20 次失敗。

  - 相較於總嘗試次數，在 15 分鐘期間的失敗比例超過 25%。

Exchange中的每個站台信箱會連結到SharePoint網站。對於每個站台伺服器上的信箱指定的Exchange主控信箱角色的伺服器同步處理SharePoint從站台信箱相關資訊。

兩種類型的同步處理進行此程序期間： 成員資格同步處理及文件同步處理。這些同步處理程序的中繼資料來自不同的 web 服務。此外，指定的Exchange伺服器可能包含連結至數個SharePoint伺服器或伺服器陣列的站台信箱。因此，警示可能來自多個信箱伺服器，根據下列條件：

1.  組織中積極使用之站台信箱的分散方法

2.  積極使用之站台信箱所連結的 SharePoint 伺服器

3.  Mailbox Server 是否有符合警示閾值的充足同步磁碟區

若要協助解決此問題，範例同步處理結果警示中的可能會協助您判斷失敗的原因。成功或失敗的每個同步處理嘗試的詳細資訊記錄在*\<exExchangeSvrNoVersion installation directory\>*Logging\\TeamMailbox 資料夾中。檢閱最新 Microsoft.Exchange.ServiceHost\_TeamMailboxSyncLog\* 檔失敗搜尋上**失敗**的字詞。您也可以使用**Test-OAuthConnectivity**、 **Test-SiteMailbox**、 和**Get-SiteMailboxDiagnostics**指令程式來疑難排解進一步。

**MSExchangeServiceHost 服務未執行**

如果 MSExchangeServiceHost 服務未執行，您會收到與下列類似的警示：

'MSExchangeServiceHost' 服務未執行之後嘗試復原。服務可能會停用或在當機迴圈。

若要解決此問題，請確認 MSExchangeServiceHost 服務已傳送提醒的伺服器上執行。如果服務在執行，請檢閱Windows事件記錄檔的指示為何服務可能不具有已執行的稍早，例如手動服務控制或服務的重複當機次數。

**MSExchangeServiceHost 服務已當機**

如果 MSExchangeServiceHost 服務當機，您會收到與下列類似的警示：

MSExchangeServiceHost 處理程序在過去 60 分鐘內已當機至少 3 次。  
Watson 訊息:

\<*郵件*\>

若要解決此問題，請檢閱Windows應用程式事件記錄檔傳送有關 MSExchangeServiceHost 服務**4999**事件通知的伺服器上。詳細文字可以提供資訊問題的原因。

## 相關資訊

[Exchange 2013 的新功能](https://technet.microsoft.com/zh-tw/library/jj150540\(v=exchg.150\))

[Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\))


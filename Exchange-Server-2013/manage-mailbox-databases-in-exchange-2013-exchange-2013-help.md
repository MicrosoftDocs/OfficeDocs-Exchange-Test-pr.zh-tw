---
title: '管理 Exchange 2013 中的信箱資料庫: Exchange 2013 Help'
TOCTitle: 管理 Exchange 2013 中的信箱資料庫
ms:assetid: ead4a96b-1717-435b-bcfc-9901ac4e3b58
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150580(v=EXCHG.150)
ms:contentKeyID: 50474517
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理 Exchange 2013 中的信箱資料庫

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-04-29_

信箱資料庫是建立和儲存信箱的精細度單位。信箱資料庫將會儲存為 Exchange 資料庫 (.edb) 檔案。在 Microsoft Exchange Server 2013 中，每個信箱資料庫都有它自己內容可讓您設定。

本主題顯示如何在 Microsoft Exchange Server 2013 中執行與管理信箱資料庫相關的組態工作。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「信箱資料庫」項目。

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

## 建立信箱資料庫

## 使用 EAC 來建立信箱資料庫

1.  從 Exchange 系統管理中心瀏覽至 \[伺服器\]。

2.  選取 \[資料庫\]，然後按一下 **+** 符號，建立資料庫。

3.  使用新增資料庫精靈來建立資料庫。

## 使用命令介面來建立信箱資料庫

關於如何建立信箱資料庫的範例，請參閱 [New-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/aa997976\(v=exchg.150\)) 的範例 1。

## 如何才能了解這是否正常運作？

若要確認您是否已成功建立資料庫，請執行下列動作：

  - 在 EAC 中，確認您建立的信箱資料庫列在 \[資料庫\] 頁面中。

  - 在命令介面中，執行下列命令，確認資料庫建立在伺服器 Mailbox01 上。
    
        Get-MailboxDatabase -Server "Mailbox01"

## 取得信箱資料庫內容

如需詳細的語法及參數資訊，請參閱 [Get-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb124924\(v=exchg.150\))。

## 使用命令介面來取得信箱資料庫內容

關於如何取得信箱資料庫內容的範例，請參閱 [New-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/aa997976\(v=exchg.150\)) 的範例 2。

## 如何才能了解這是否正常運作？

若要確認您是否已成功擷取信箱資料庫資訊，請執行下列動作：

在命令介面中，確認您的所有信箱資料庫資訊都正確顯示。

## 設定信箱資料庫內容

## 使用 EAC 設定信箱資料庫內容

1.  在 EAC 中，瀏覽至 \[伺服器\]。

2.  選取 \[資料庫\]，然後按一下您要設定的信箱資料庫將其選取。

3.  按一下 \[編輯\] ![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")，以設定信箱資料庫的屬性。

4.  
    
    使用 \[一般\] 索引標籤，檢視信箱資料庫的狀態，包括信箱資料庫路徑、上一次備份，以及信箱資料庫狀態：
    
      - **資料庫路徑**   這個唯讀欄位會顯示所選取信箱資料庫的 Exchange 2013 資料庫 (.edb) 檔案完整路徑。若要檢視完整路徑，您可能必須按一下路徑，然後使用向右鍵來進行。您無法使用此欄位來變更該路徑。若要變更資料庫檔案的位置，請使用 [Move-DatabasePath](https://technet.microsoft.com/zh-tw/library/bb124742\(v=exchg.150\)) Cmdlet。
    
      - **上次完整備份**   這個唯讀欄位會顯示上次完整備份信箱資料庫的日期和時間。
    
      - **上次增量備份**   這個唯讀欄位會顯示上次增量備份信箱資料庫的日期和時間。
    
      - **狀態**   這個唯讀欄位會顯示信箱資料庫是處於裝載或卸載狀態。
    
      - **裝載在伺服器上**   這個唯讀欄位會顯示資料庫已裝載在哪個伺服器上。
    
      - **主要**   個唯讀欄位會顯示信箱資料庫的主要伺服器。主控資料庫作用中副本的信箱伺服器稱為信箱資料庫主機。
    
      - **主要類型**   這個唯讀欄位會顯示信箱資料庫主機的類型。
    
      - **修改時間**   這個唯讀欄位會顯示上次修改資料庫的日期和時間。
    
      - **裝載此資料庫副本的伺服器**   這個唯讀欄位會顯示具有此資料庫副本的其他伺服器。

5.  使用 \[維護\] 索引標籤可以設定信箱資料庫設定，包括指定日誌收件者、設定維護排程，以及在啟動時裝載資料庫：
    
      - **日誌收件者**   按一下 \[瀏覽\] 指定收件者，可啟用此信箱資料庫的日誌功能。移除列出的收件者則停用日誌功能。
    
      - **維護排程**   使用此清單選取其中一項預設的維護排程。您也可以設定自訂排程。若要設定自訂排程，請按一下 \[自訂\]。
    
      - **啟用背景資料庫維護 (24x7 全天候 ESE 掃描)**   選取這個核取方塊，以啟用會持續在背景執行的線上資料庫掃描。線上資料庫掃描會執行資料庫的總和檢查碼計算，並執行一些作業，可讓 Exchange 掃描資料庫上遺失的空間並進行復原。如果選取這個核取方塊，Exchange 每天會掃描資料庫一次，而且如果在七天內無法完成資料庫掃描，便會發出警告事件。
    
      - **不要在啟動時裝載此資料庫**   選取此核取方塊以避免 Exchange 在啟動時裝載此信箱資料庫。
    
      - **還原可覆寫此資料庫**   選取此核取方塊以允許在還原程序進行期間覆寫信箱資料庫。
    
      - **啟用循環記錄**   選取此核取方塊以啟用循環記錄。

6.  使用 \[限制\] 索引標籤，可指定信箱資料庫的儲存限制、警告訊息間隔及刪除設定。
    
      - **超過下列大小就發出警告 (GB)**   選取此核取方塊會自動警告信箱使用者其信箱接近儲存限制。若要指定儲存限制，請選取核取方塊，然後指定要傳送警告電子郵件給信箱使用者前，信箱能儲存內容的大小 (GB)。您可以輸入介於 0 到 2,097,151 (MB) (2.0 TB) 之間的值。
    
      - **超過下列大小就禁止傳送 (GB)**   選取此核取方塊可防止使用者在其信箱達到指定的限制大小之後傳送新的電子郵件。若要指定此限制，請選取核取方塊，然後輸入您要禁止傳送新電子郵件並通知使用者的信箱大小 (以 GB 為單位)。您可以輸入介於 0 到 2,097,151 MB (2.0 TB) 之間的值。
    
      - **超過下列大小就禁止收發 (GB)**   選取此核取方塊可防止使用者在其信箱達到指定的限制大小之後傳送及接收電子郵件。若要指定此限制，請選取核取方塊，然後輸入您要禁止傳送和接收電子郵件並通知使用者的信箱大小 (以 GB 為單位)。您可以輸入介於 0 到 2,097,151 MB (2.0 TB) 之間的值。
    
      - **保留已刪除郵件的天數**   選取此核取方塊，以設定已刪除的郵件保留在信箱中的天數。您可以輸入 0 到 24,855 天的值。
    
      - **保留已刪除信箱的天數**   選取此核取方塊，以設定保留已刪除信箱的天數。您可以輸入 0 到 24,855 天的值。
    
      - **不要在備份資料庫前永久刪除項目**   選取此核取方塊以便在備份信箱資料庫之後才永久刪除信箱和電子郵件。

7.  使用 \[用戶端設定\] 索引標籤可以設定信箱的離線通訊錄 (OAB)：
    
      - **離線通訊錄**   若要選取離線通訊錄，請按一下 \[瀏覽\]，然後選取離線通訊錄。

## 使用命令介面來設定信箱資料庫內容

關於如何設定信箱資料庫內容的範例，請參閱 [Set-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb123971\(v=exchg.150\))中的範例 1。

## 如何才能了解這是否正常運作？

若要確認您是否已成功設定屬性，請執行下列動作：

  - 確認您的變更已儲存至 EAC 中。

  - 從命令介面執行下列命令，以擷取信箱資料庫內容。
    
        Get-MailboxDatabase -Identity MailboxDatabase01 -Status | Format-List

## 移動信箱資料庫路徑

如需詳細的語法及參數資訊，請參閱 [Move-DatabasePath](https://technet.microsoft.com/zh-tw/library/bb124742\(v=exchg.150\))。

## 使用命令介面移動信箱資料庫路徑

關於如何設定信箱資料庫內容的範例，請參閱 [Move-DatabasePath](https://technet.microsoft.com/zh-tw/library/bb124742\(v=exchg.150\))中的範例 1。

## 如何才能了解這是否正常運作？

若要確認您是否已成功移動資料庫路徑，請執行下列動作：

1.  從 EAC 選擇 \[伺服器\] \> \[資料庫\]，然後按一下以選擇適合的信箱。

2.  按一下畫筆符號，確認資料庫路徑是否正確。

## 裝載信箱資料庫

如需詳細的語法及參數資訊，請參閱 [Mount-Database](https://technet.microsoft.com/zh-tw/library/aa998871\(v=exchg.150\))。

## 使用命令介面裝載信箱資料庫

關於如何裝載信箱資料庫的範例，請參閱 [Mount-Database](https://technet.microsoft.com/zh-tw/library/aa998871\(v=exchg.150\)) 的範例 1。

## 如何才能了解這是否正常運作？

若要確認您是否已成功裝載信箱資料庫，請執行下列動作。

  - 從命令介面執行下列命令，以針對所有信箱資料庫擷取信箱資料庫內容。
    
        Get-MailboxDatabase -IncludePreExchange2013

## 卸載信箱資料庫

如需詳細的語法及參數資訊，請參閱 [Dismount-Database](https://technet.microsoft.com/zh-tw/library/bb124936\(v=exchg.150\))。

## 使用命令介面卸載信箱資料庫

關於如何卸載信箱資料庫的範例，請參閱 [Dismount-Database](https://technet.microsoft.com/zh-tw/library/bb124936\(v=exchg.150\)) 的範例 1。

## 如何才能了解這是否正常運作？

若要確認您是否已成功卸載資料庫，請執行下列動作：

1.  從 EAC 選擇 \[伺服器\] \> \[資料庫\]，然後按一下以選擇適合的信箱。

2.  按一下畫筆符號，確認資料庫狀態為 \[卸載\]。

## 移除信箱資料庫

## 使用 EAC 移除信箱資料庫

1.  從 EAC 選擇 \[伺服器\] \> \[資料庫\]，然後按一下以選擇適合的信箱。

2.  按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")，移除信箱資料庫。

## 使用命令介面移除信箱資料庫

如需詳細的語法及參數資訊，請參閱 [Remove-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/aa997931\(v=exchg.150\))。

1.  執行以下命令，移除信箱資料庫 MyDatabase。
    
        Remove-MailboxDatabase -Identity "MyDatabase"

2.  提示您是否確定要執行動作時，請輸入 **Y**。

3.  出現說明已順利移除資料庫的對話方塊時，請記下 Exchange 2013 資料庫 (.edb) 檔案的位置。如果想要從硬碟中移除此檔案，則必須手動移除此檔案。

## 如何才能了解這是否正常運作？

若要確認您是否已成功移除信箱資料庫，請執行下列動作：

  - 在 EAC 中，選取 \[伺服器\] \> \[資料庫\]。

  - 確認信箱資料庫已被移除。


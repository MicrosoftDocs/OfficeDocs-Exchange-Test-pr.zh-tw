---
title: 疑難排解 OWA 健全設定
TOCTitle: 疑難排解 OWA 健全設定
ms:assetid: eae9dbd7-2ce6-43ce-b9a1-b114fd0c3ab4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.owa(v=EXCHG.150)
ms:contentKeyID: 53276420
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 OWA 健全設定

 

_**適用版本：** Exchange Server 2013_

_**上次修改主題的時間：** 2015-03-09_

Outlook Web App (OWA) 健全設定會監視 Outlook Web App 服務的整體健康狀況。

如果您收到警示，指出 Outlook Web App 的狀況不良，表示可能有問題令使用者無法使用 Outlook Web App 來存取信箱。

## 說明

Outlook Web App 服務是透過下列探查與監視器受到監視。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Probe</th>
<th>健全設定</th>
<th>相依性</th>
<th>關聯的監視器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OwaCtpProbe</p></td>
<td><p>Outlook Web App</p></td>
<td><p>Active Directory</p>
<p>資訊儲存庫</p></td>
<td><p>OwaCtpMonitor</p></td>
</tr>
</tbody>
</table>


如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 常見問題

數個原因可能導致此探查失敗。以下是一些更為常見原因：

  - 受監視 Client Access Server (CAS) 上裝載的 Outlook Web App 應用程式集區沒有回應，或 Mailbox Server 上裝載的應用程式集區沒有回應。

  - CAS 發生網路問題，無法連線到 Mailbox Server 或網域控制站。

  - 監視帳戶認證不正確。

  - 未裝載使用者的資料庫，或該信箱無法存取資訊儲存庫。

  - 資訊儲存庫沒有回應。

  - 網域控制站無回應。

## 使用者動作

服務可能在發出警示之後已復原。因此，當您收到警示指出健全設定狀況不良時，請先確認問題仍然存在。如果問題確實存在，請執行以下幾節所列出的適當復原動作。

## 確認問題仍然存在

1.  識別警示中的健全設定名稱和伺服器名稱。

2.  訊息詳細資料會提供造成警示確切原因的相關資訊。在大部分情況下，訊息詳細資料會提供足夠的疑難排解資訊來找出根本原因。如果訊息詳細資料不清楚，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取使警示產生之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        如需 server1.contoso.com 的 Outlook Web App 健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA"}
    
    2.  檢閱命令的輸出傳送至決定顯示器回報的錯誤。發出警示監視器**AlertValue**值為`Unhealthy`。
    
    3.  請為不健康狀態監視重新執行相關聯的探查。請參閱尋找相關聯的探查 \[說明\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，若要在 *server1.contoso.com* 上建立 Exchange ActiveSync 監視探查，請執行下列命令：
        
            Invoke-MonitoringProbe -Identity ActiveSync.Protocol\ActiveSyncSelfTestProbe -Server server1.contoso.com
    
    4.  在命令輸出中，檢閱探查的 **\[結果\]** 值。如果值為 **\[成功\]**，表示問題是暫時性錯誤，且已不存在。否則，請參閱以下幾節所列的復原步驟。

## OwaCtpMonitor 復原動作

來自健全設定的電子郵件警示包含下列資訊：

  - 傳送警示的伺服器名稱

  - 上個錯誤的完整例外狀況追蹤，包括診斷資料與特定的 HTTP 標頭資訊  
    
    **附註**  您可以使用完整例外狀況追蹤資訊可協助疑難排解問題。由探查所產生的例外狀況包含說明為何無法探查失敗原因。例如，例外包含下列項目：
    
      - **MissingKeyword**  伺服器回應中找不到預期的關鍵字。在此例中例外包含預期的關鍵字。
    
      - **NameResolution**   DNS 解析無法解析指定的伺服器名稱。
    
      - **NetworkConnection**   探查在嘗試連線到 CAFE 上的 OWA 應用程式集區時，收到網路連線失敗。
    
      - **UnexpectedHttpResponseCode**  回應有未預期的 HTTP 程式碼。例如，伺服器會傳回**503** HTTP 程式碼。
    
      - **RequestTimeout**   伺服器花太久時間來回應用戶端要求。
    
      - **ScenarioTimeout**  探查已成功完成，但花一分鐘以上為達成此目的。這通常表示正在超載的系統。
    
      - **OwaErrorPage**   Outlook Web App傳回錯誤頁面。通常是使用中的例外狀況訊息錯誤導致失敗的名稱。
    
      - **OwaMailboxErrorPage**   Outlook Web App傳回錯誤頁面包含一個信箱儲存區相關的錯誤。這通常表示信箱存放區已關閉或信箱會被卸載。
    
    例外狀況追蹤包含名為**FailingComponent**重要\] 欄位。探查嘗試判斷失敗，例如在下列範例：
    
      - **信箱**  探查可以達到Outlook Web App，但無法連線至信箱儲存區。在此例中探查失敗，或者信箱存取延遲造成失敗並產生**ScenarioTimeout**錯誤探查。當發生這些失敗類型時，就應該檢查信箱伺服器的狀況。
    
      - **Active Directory**   探查可以達到Outlook Web App，但無法連線至Active Directory。在此例中探查失敗或Active Directory通話延遲造成探查逾時。當發生這些失敗類型時，您應該檢查網域控制站的狀況及也會檢查 CA 與 Mailbox 伺服器與網域控制站之間的網路連線。
    
      - **Owa**  這通常表示Outlook Web App層內發生錯誤。當發生這些失敗類型時，您必須確認 CA 與 Mailbox 伺服器上， Outlook Web App程序的健康情況並且也會檢查網路連線。
    
    例外也包含收到探查失敗之前的最新 HTTP 要求和回應資訊。呈報本文包含探查記錄檔的路徑。您可以使用這項資訊來判斷完整 HTTP web 要求和回應探查失敗時傳送的。這個檔案包含失敗探查的資料因為會記錄失敗的嘗試。您可以使用這項資訊以取得更完整的測試為何無法檢視。

  - 可用性度量下降幅度 (x%)。

  - 包含探查的完整 HTTP 要求追蹤資料夾的完整路徑。根據預設，此資訊位於*\<ExchangeServer\>*\\Logging\\Monitoring\\OWA\\ClientAccessProbe 資料夾。

  - 警示的發生日期和時間。

若要疑難排解此問題，請遵循下列步驟：

1.  建立測試使用者帳戶，然後再登入 CA 所使用的測試使用者帳戶。例如，使用 https:// *\<servername\>*/owa 登入。
    
    如果失敗，請使用不同的 CA 伺服器來測試，以確認問題發生在特定的 CAS，而不是 Mailbox Server。

2.  確認 CA 與 Mailbox server 之間的網路連線。若要確認每部伺服器在回應使用 ping.exe。

3.  檢查在 OWA 的警示。可能表示問題影響特定的 Mailbox server 的通訊協定健全設定。如需詳細資訊，請參閱[疑難排解 OWA。通訊協定健全設定](troubleshooting-owa-protocol-health-set.md)。

4.  啟動 \[IIS 管理員\]，然後連線到回報問題的伺服器，以確認 CAS 上正在執行 MSExchangeOwaAppPool 應用程式集區。

5.  在 \[IIS 管理員\] 中，確認預設網站正在執行。

6.  找出失敗的探查的信箱資料庫並確認信箱資料庫是信箱伺服器上作用中儲存的信箱正常。若要找出失敗的資料庫 GUID 資訊、 開啟的完整例外狀況追蹤資訊。每個失敗應該包含類似下列範例中的項目：
    
    Owa 探查開頭目標 ︰ https://localhost/owa/、 使用者名稱： *HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com*

7.  複製 HealthMailbox GUID，然後在命令介面中執行下列命令：
    
        Get-Mailbox -Monitoring -Identity <username>
    
    例如，執行下列命令：
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    在傳回的物件中，您可以找到使用者的資料庫名稱，也可以判斷目前的使用中資料庫所在的位置。

8.  如果您已設定重新導向網站之間，您可能會看到探查失敗並產生 MissingKeyword 錯誤。這是因為依預設，在任何位置的帳戶執行 CA 探查和也因為探查不會嘗試將測試 CAS 不同網站上的使用重新導向時。若要解決此問題，請確定 MonitoringGroups 中所包含的每個網站的伺服器。指定監視群組中的 CA 伺服器測試僅搭配相同的群組中的信箱伺服器。
    
    若要判斷伺服器的監視群組，請執行下列命令：
    
        Get-ExchangeServer | ft MonitoringGroup
    
    若要修改的伺服器上的 \[監視\] 群組，使用*MonitoringGroup*參數搭配**Set-ExchangeServer**指令程式。例如，使用下列方法：
    
        Set-ExchangeServer -Identity "ServerName" -MonitoringGroup "Primary"

9.  在 \[IIS 管理員\] 中，按一下 **\[應用程式集區\]**，然後從 Exchange 管理命令介面 執行下列命令，以回收 **MSExchangeOWAAppPool** 應用程式集區：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

10. 依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

11. 如果問題仍然存在，請使用 IISReset 公用程式或執行下列命令來回收 IIS 服務。
    
        Iisreset /noforce

12. 依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

13. 如果問題仍然存在，請重新啟動伺服器。

14. 伺服器重新啟動後，請依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

15. 如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[Exchange 2013 的新功能](https://technet.microsoft.com/zh-tw/library/jj150540\(v=exchg.150\))

[Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\))


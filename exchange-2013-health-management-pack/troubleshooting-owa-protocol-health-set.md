---
title: 疑難排解 OWA。通訊協定健全設定
TOCTitle: 疑難排解 OWA。通訊協定健全設定
ms:assetid: fe172da8-65d3-43e0-ba62-d36a1b05fc11
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.owa.protocol(v=EXCHG.150)
ms:contentKeyID: 53276423
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 OWA。通訊協定健全設定

 

_**適用版本：** Exchange Server 2013_

_**上次修改主題的時間：** 2015-03-09_

OWA.Protocol 健全設定會監視 Mailbox Server 上的 Outlook Web App 通訊協定。

如果您收到警示，指出 OWA.Protocol 的狀況不良，表示可能有問題令使用者無法使用 Outlook Web App 來存取信箱。

## 說明

OWA 服務是透過下列探查與監視器受到監視。


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
<td><p>OwaSelfTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>無</p></td>
<td><p>OwaSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>OwaDeepTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>Active Directory</p>
<p>資訊儲存庫</p></td>
<td><p>OwaDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


**OwaSelfTestProbe**探查將單一 HTTP 要求傳送至下列地址： https://localhost:444/owa/exhealth.check。探查確認應用程式集區藉由傳回回應**200 確定**狀態碼。此探查上任何其他Exchange元件有任何相依性。

**OwaDeepTestProbe**探查是針對每一個信箱資料庫執行使用目前的伺服器上的複本。探查決定可以針對該伺服器進行完整的登入。若要這樣做，它會針對該特定伺服器模擬用戶端存取伺服器 (CAS) 所產生的流量的類型。探查取決於Active Directory網域服務 (AD DS) 進行驗證，以及存取信箱的信箱存放區上。如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 常見問題

下列任一常見原因都可能導致此探查失敗：

  - 受監視 CAS 上裝載的 OWA 應用程式集區沒有回應，或 Mailbox Server 上裝載的應用程式集區沒有回應。

  - CA 或 Mailbox Server 發生網路問題，無法連線到其他伺服器或網域控制站。

  - 監視帳戶認證不正確。

  - 未裝載使用者的資料庫，或該信箱無法存取資訊儲存庫。

  - 資訊儲存庫沒有回應。

  - 網域控制站無回應。

## 使用者動作

服務可能在發出警示之後已復原。因此，當您收到警示指出健全設定狀況不良時，請先確認問題仍然存在。如果問題確實存在，請執行以下幾節所列出的適當復原動作。

## 確認問題仍然存在

1.  識別警示中的健全設定名稱和伺服器名稱。

2.  訊息詳細資料會提供造成警示確切原因的相關資訊。在大部分情況下，訊息詳細資料會提供足夠的疑難排解資訊來找出根本原因。如果訊息詳細資料不清楚，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要擷取 server1.contoso.com 的 OWA.Protocol 健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Protocol"}
    
    2.  檢閱命令的輸出傳送至決定顯示器回報的錯誤。發出警示監視器**AlertValue**會`Unhealthy`。
    
    3.  請為不健康狀態監視重新執行相關聯的探查。請參閱尋找相關聯的探查 \[說明\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假設失敗監視已**OwaSelfTestMonitor**。相關聯的監視探查是**OwaSelfTestProbe**。若要執行的探查 server1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe OWA.Protocol\OwaSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  在命令輸出中，檢閱探查的 **\[結果\]** 值。如果值為 **\[成功\]**，表示問題是暫時性錯誤，且已不存在。否則，請參閱以下幾節所列的復原步驟。

當您收到來自健全設定的警示時，電子郵件會包含下列資訊：

  - 傳送警示的伺服器名稱

  - 失敗的探查類型 (SelfTest 或 DeepTest)

  - 警示的發生日期和時間

  - 資料夾的路徑，該資料夾包含探查的完整 HTTP 要求追蹤。
    
      
    根據預設，追蹤檔案位於下列資料夾中：
    
      - SelfTestProbe: \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\ProtocolProbe
    
      - DeepTestProbe: \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\MailboxProbe

  - 上個錯誤的完整例外狀況追蹤，包括診斷資料與特定的 HTTP 標頭資訊  
    
    **附註**  您可以使用完整的例外狀況追蹤中的資訊，以協助疑難排解問題。由探查所產生的例外狀況包含說明為何無法探查失敗原因。失敗原因可能是下列其中一項：
    
      - **MissingKeyword**  伺服器回應中找不到預期的關鍵字。在此例中例外包含預期的關鍵字。
    
      - **NameResolution**   DNS 解析無法解析指定的伺服器名稱。
    
      - **NetworkConnection**   探查在嘗試連線到 CAFE 上的 OWA 應用程式集區時，收到網路連線失敗。
    
      - **UnexpectedHttpResponseCode**  回應包含未預期的 HTTP 程式碼。例如，伺服器會傳回**503** HTTP 程式碼。
    
      - **RequestTimeout**   伺服器花太久時間來回應用戶端要求。
    
      - **UnexpectedHttpResponseCode**  回應傳回未預期的 HTTP 程式碼。例如，伺服器會傳回**503** HTTP 程式碼。
    
      - **ScenarioTimeout**  探查已成功完成，但萬一一分鐘以上來達成。這通常表示正在超載的系統。
    
      - **OwaErrorPage**  OWA 傳回錯誤頁面。通常位於例外狀況訊息錯誤導致失敗的名稱。
    
      - **OwaMailboxErrorPage**  OWA 傳回錯誤頁面包含一個信箱儲存區相關的錯誤。這通常是表示為信箱儲存區正在關閉或所要卸載的信箱等問題。
    
    例外狀況追蹤包含名為**FailingComponent**，在其中探查會嘗試判斷及分類 （英文） 的失敗工作的重要欄位。例如，探查可能會傳回下列任一值：
    
      - **信箱**  探查可以達到 OWA 中，但無法連線至信箱儲存區。在此例中探查失敗或信箱存取延遲造成失敗並產生**ScenarioTimeout**錯誤探查。當發生這些失敗類型時，就應該檢查信箱伺服器的狀況。
    
      - **Active Directory**  探查可以達到 OWA 中，但無法連線到 AD DS。在此例中探查失敗、 或 AD DS 通話延遲時間可能會導致逾時探查。當發生這些失敗類型時，您應該檢查網域控制站的狀況及也會檢查之間的 CA 和信箱伺服器和網域控制站的網路連線。
    
      - **OWA**  這通常表示 OWA 層內發生錯誤。當發生這些失敗類型時，您必須確認 CA 與 Mailbox server，在 OWA 程序的健康情況並且也會檢查網路連線。
    
    例外也包含收到探查失敗之前的最新 HTTP 要求和回應資訊。  
      
    呈報本文包含可用來確認完整 HTTP web 要求和回應探查失敗時傳送的探查記錄檔的路徑。這個檔案包含失敗探查的資料因為會記錄失敗的嘗試。您可以使用這項資訊以取得更完整的測試為何無法檢視。

## OwaSelfTestProbe 復原動作

因為此探查的依存性很低，失敗通常是在 OWA 應用程式集區處理程序沒有回應時發生。

若要疑難排解此問題，請遵循下列步驟：

1.  檢查警示電子郵件內文中的探查追蹤記錄 URL，以確認有新的失敗發生。

2.  建立測試使用者帳戶上裝載之信箱的同一部伺服器。嘗試登入以決定是否可重現問題。

3.  檢查可能表示問題影響特定的 Mailbox server OWA 健全設定上有警示。如需詳細資訊，請參閱[疑難排解 OWA 健全設定](troubleshooting-owa-health-set.md)。

4.  啟動 \[IIS 管理員\]，然後連線到回報問題的伺服器，以判斷 CAS 上是否正在執行 **MSExchangeOwaAppPool** 應用程式集區。

5.  在 \[IIS 管理員\] 中，確認預設網站正在執行。

6.  在 \[IIS 管理員\] 中，按一下 **\[應用程式集區\]**，然後從 Exchange 管理命令介面 執行下列命令，以回收 **MSExchangeOWAAppPool** 應用程式集區：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

7.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

8.  如果問題仍然存在，請使用 IISReset 公用程式或執行下列命令來回收 IIS 服務。
    
        Iisreset /noforce

9.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

10. 如果問題仍然存在，請重新啟動伺服器。

11. 伺服器重新啟動後，請依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

12. 如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## OwaDeepTestProbe 復原動作

1.  若要判斷問題是否仍存在，請建立測試使用者帳戶的同一部伺服器上已裝載信箱，並再嘗試登入 OWA。例如，嘗試使用登入： https:// *\<servername\>*/owa。

2.  檢查可能表示問題影響特定的 Mailbox server OWA 健全設定上有警示。如需詳細資訊，請參閱[疑難排解 OWA 健全設定](troubleshooting-owa-health-set.md)。

3.  啟動 \[IIS 管理員\]，然後連線到回報問題的伺服器，以判斷 CAS 上是否正在執行 **MSExchangeOwaAppPool** 應用程式集區。

4.  在 \[IIS 管理員\] 中，確認預設網站正在執行。

5.  找出失敗的探查的信箱資料庫並確認 \[信箱資料庫正確 Mailbox server 上作用中儲存的信箱正常。若要找出失敗的資料庫 GUID 資訊、 開啟的完整例外狀況追蹤資訊。每個失敗應該包含與下面類似的項目：
    
    `Starting Owa probe with Target: https://localhost/owa/, Username:  HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com`

6.  複製 HealthMailbox GUID，然後在命令介面中執行下列命令：
    
        Get-Mailbox -Monitoring -Identity <username>
    
    例如，執行下列命令：
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    在傳回的物件中，您可以找到使用者的資料庫名稱，也可以判斷目前的使用中資料庫所在的位置。

7.  在 \[IIS 管理員\] 中，按一下 **\[應用程式集區\]**，然後從命令介面執行下列命令，以回收 **MSExchangeOWAAppPool** 應用程式集區：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

8.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

9.  如果問題仍然存在，請使用 IISReset 公用程式或執行下列命令來回收 IIS 服務。
    
        Iisreset /noforce

10. 依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

11. 如果問題仍然存在，請重新啟動伺服器。

12. 伺服器重新啟動後，請依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

13. 如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[Exchange 2013 的新功能](https://technet.microsoft.com/zh-tw/library/jj150540\(v=exchg.150\))

[Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\))


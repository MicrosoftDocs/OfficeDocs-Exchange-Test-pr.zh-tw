---
title: '管理傳輸代理程式: Exchange 2013 Help'
TOCTitle: 管理傳輸代理程式
ms:assetid: f15ab7e4-015d-45b1-9c10-f733d7cd2a36
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125175(v=EXCHG.150)
ms:contentKeyID: 50474566
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理傳輸代理程式

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

傳輸代理程式郵件移動到傳輸管線操作郵件上使用 SMTP 事件。大部分的 Microsoft Exchange Server 2013隨附的內建傳輸代理程式且不可見無法管理。不過，您可以安裝並在組織中設定 Exchange 伺服器上的第三方傳輸代理程式。如需傳輸代理程式的詳細資訊，請參閱[傳輸代理程式](transport-agents-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸代理程式」項目。

  - 您只能使用命令介面來執行此程序。

  - 支援的舊版傳輸代理程式未啟用根據預設，但是您可以啟用它。指示，請參閱[啟用支援的舊版傳輸代理程式](enable-support-for-legacy-transport-agents-exchange-2013-help.md)。

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

## 關於用戶端存取伺服器上，前端傳輸服務的傳輸代理程式程序

您無法使用 Exchange 管理命令介面來管理 Client Access server 上 Front End Transport 服務中的傳輸代理程式。而您需要在用戶端存取伺服器上，開啟 Windows PowerShell，然後再匯入 Windows PowerShell 工作階段的 \[Exchange cmdlet。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不支援 Windows PowerShell 中執行 Exchange cmdlet 的非管理傳輸代理程式的前端傳輸服務中的工作。在 Windows PowerShell 中執行 Exchange cmdlet 有嚴重導致若您略過的 Exchange 管理命令介面和角色型存取控制 (RBAC) 的後果。您一律應在 Exchange 管理命令介面中執行 Exchange 指令程式。如需詳細資訊，請參閱<a href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange 2013 版本資訊</a>。</td>
</tr>
</tbody>
</table>


若要在前端傳輸服務中執行本主題所述的任一傳輸代理程式程序，您必須執行下列額外步驟：

1.  在用戶端存取伺服器上，開啟 Windows PowerShell 並執行下列命令：
    
        Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn

2.  執行命令所述，但命令中加入下列值： `-TransportService FrontEnd`。
    
    例如，若要檢視用戶端存取伺服器上前端傳輸服務中的傳輸代理程式，請執行下列命令：
    
        Get-TransportAgent -TransportService FrontEnd

## 使用命令介面安裝傳輸代理程式

當您安裝傳輸代理程式時，Exchange 只會註冊傳輸代理程式相關聯的 Dll。您需要確定已正確安裝並設定所有檔案、 登錄機碼及傳輸代理程式取決於其他物件。Exchange 會載入 Dll 後，它會繼續命令完成後參照 Dll。

傳輸代理程式具有完整存取權時所發生的所有電子郵件訊息。Exchange 會將任何限制放在傳輸代理程式的行為。傳輸代理程式不穩定或包含安全性瑕疵可能會影響的穩定性及 Exchange 安全性。因此，您應該只安裝傳輸代理程式的完全信任和，已在測試環境中完整測試。

傳輸代理程式會安裝以確定郵件流程不會受到尚未已設定的傳輸代理程式的已停用狀態。因此，已正確設定傳輸代理程式之後，您需要啟用傳輸代理程式。

請使用下列語法來安裝傳輸代理程式。

    Install-TransportAgent -Name <TransportAgentIdentity> -TransportAgentFactory <"TransportAgentFactory"> -AssemblyPath <"FilePath">

此範例會在信箱伺服器的傳輸服務中，安裝名為 Contoso Transport Agent 的虛擬傳輸代理程式。

    Install-TransportAgent -Name "Contoso Transport Agent" -TransportAgentFactory "vendor.exchange.ContosoTransportAgentfactory" -AssemblyPath "C:\Program Files\Vendor\TransportAgent\ContosoTransportAgentFactory.dll"

## 如何才能了解這是否正常運作？

若要確認您已成功安裝傳輸代理程式，請執行命令 `Get-TransportAgent` 並確認有列出傳輸代理程式。

## 使用命令介面啟用傳輸代理程式

請使用下列語法來啟用傳輸代理程式。

    Enable-TransportAgent <TransportAgentIdentity>

此範例會在信箱伺服器的傳輸服務中，啟用名為 Contoso Transport Agent 的傳輸代理程式。

    Enable-TransportAgent "Contoso Transport Agent"

## 如何才能了解這是否正常運作？

若要確認您已成功啟用傳輸代理程式，請執行命令 `Get-TransportAgent | Format-List Name,Enabled` 並確認傳輸代理程式已經啟用。

## 使用命令介面停用傳輸代理程式

請使用下列語法來停用傳輸代理程式：

    Disable-TransportAgent <TransportAgentIdentity>

此範例會在信箱伺服器的傳輸服務中，停用名為 Fabirkam Transport Agent 的傳輸代理程式。

    Disable-TransportAgent "Fabrikam Transport Agent"

## 如何才能了解這是否正常運作？

若要確認您已成功停用傳輸代理程式，請執行命令 `Get-TransportAgent | Format-List Name,Enabled` 並確認傳輸代理程式已經停用。

## 使用命令介面檢視傳輸代理程式

若要檢視傳輸代理程式的摘要清單，請執行下列命令：

    Get-TransportAgent

若要檢視特定傳輸代理程式的詳細組態，請執行下列命令：

    Get-TransportAgent <TransportAgentIdentity> | Format-List

此範例會提供名為 Transport Rule Agent 之傳輸代理程式的詳細組態。

    Get-TransportAgent "Transport Rule Agent" | Format-List

## 使用命令介面設定傳輸代理程式的優先順序

第一次傳輸優先順序 0 的程序電子郵件至最接近的代理程式。不過，在其中註冊傳輸代理程式傳輸管線中的 SMTP 事件可能會造成處理訊息之前較高的優先順序代理程式的較低優先順序代理程式。

若要修改現有傳輸代理程式的優先順序，請執行下列命令：

    Set-TransportAgent <TransportAgentIdentity> -Priority <Integer>

此範例會在信箱伺服器的傳輸服務中，將名為 Contoso Transport Agent 之現有傳輸代理程式的優先順序代理程式值設為 3。

    Set-TransportAgent "Contoso Transport Agent" -Priority 3

## 如何才能了解這是否正常運作？

若要確認您已成功設定傳輸代理程式的優先順序，請執行命令 `Get-TransportAgent | Format-List Name,Priority` 並確認傳輸代理程式的優先順序值。

## 使用命令介面解除安裝傳輸代理程式

當傳輸代理程式會在解除安裝時，Exchange 會取消登錄代理程式搭配使用 DLL 檔案。Exchange 不會移除任何檔案、 登錄機碼或新增傳輸代理程式安裝的其他物件。

若要解除安裝傳輸代理程式，請執行下列命令：

    Uninstall-TransportAgent <TransportAgentIdentity>

此範例會在信箱伺服器的傳輸服務中，解除安裝名為 Fabrikam Transport Agent 的傳輸代理程式。

    Uninstall-TransportAgent "Fabrikam Transport Agent"

## 如何才能了解這是否正常運作？

若要確認您已成功解除安裝傳輸代理程式，請執行命令 `Get-TransportAgent` 並確認未列出傳輸代理程式。


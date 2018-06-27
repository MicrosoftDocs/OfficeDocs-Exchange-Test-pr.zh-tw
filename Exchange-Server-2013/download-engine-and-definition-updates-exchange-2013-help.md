---
title: '下載引擎和定義更新: Exchange 2013 Help'
TOCTitle: 下載引擎和定義更新
ms:assetid: 8f2ca383-e463-4df0-aa5d-29afe2f81aaf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657471(v=EXCHG.150)
ms:contentKeyID: 50473719
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 下載引擎和定義更新

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

Microsoft Exchange Server 2013系統管理員可以手動下載反惡意程式碼引擎和定義 （簽章） 更新。我們強烈建議您下載引擎和定義更新之前先將它放在生產環境中Exchange伺服器上。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘

  - 您只能使用命令介面來執行此程序。 若要了解如何在內部部署 Exchange 組織中開啟 Exchange 管理命令介面，請參閱[開啟命令介面。](https://technet.microsoft.com/zh-tw/library/dd638134\(v=exchg.150\))。

  - 若要下載更新，您的電腦必須能夠存取網際網路且可以建立 TCP 連接埠 80 (HTTP) 連線。如果您的組織使用 proxy 伺服器的網際網路存取，請參閱本主題中的 \[使用命令介面來設定反惡意軟體更新的 proxy 伺服器設定\] 區段。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「 反惡意程式碼？[反垃圾郵件和反惡意程式的權限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主題中的項目。

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


## 使用命令介面手動下載引擎和定義更新

若要下載引擎和定義更新，請執行以下命令：

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity <FQDN of server>

本範例會手動下載引擎和定義更新名為 mailbox01.contoso.com Exchange伺服器上：

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com

（選用） 您可以使用*EngineUpdatePath*參數從兩者`http://forefrontdl.microsoft.com/server/scanengineupdate`的預設位置以外下載更新。您可以使用此參數可指定替代的 HTTP 位址或 UNC 路徑。如果您指定的 UNC 路徑，網路服務必須可以存取路徑。

本範例會手動下載引擎和定義更新名為 mailbox01.contoso.com 從 UNC 路徑`\\FileServer01\Data\MalwareUpdates`Exchange伺服器上：

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com -EngineUpdatePath \\FileServer01\Data\MalwareUpdates

## 如何知道這是否正常運作？

若要驗證是否成功下載更新，您必須存取 \[事件檢視器\] 並檢視事件記錄。我們建議您只篩選 FIPFS 事作，程序如下所述。

1.  從 \[開始\] 功能表按一下 \[所有程式\] \> \[系統管理工具\] \> \[事件檢視器\]。

2.  在 \[事件檢視器\] 中展開 \[Windows 記錄檔\]，然後按一下 \[應用程式\]。

3.  在 \[動作\] 功能表中，按一下 \[篩選目前的記錄\]。

4.  在 \[篩選目前的記錄\] 對話方塊中，從 \[事件來源\] 下拉式清單中選取 \[FIPFS\] 核取方塊，然後按一下 \[確定\]。

如果成功下載引擎更新，就會看到類似下列的事件識別碼 6033 出現：

`MS Filtering Engine Update process performed a successful scan engine update.`

`Scan Engine: Microsoft`

`Update Path: http://forefrontdl.microsoft.com/server/scanengineupdate`

`Last Update time: ‎2012‎-‎08‎-‎16T13:22:17.000Z`

`Engine Version: 1.1.8601.0`

`Signature Version: 1.131.2169.0`

## 使用命令介面來設定反惡意軟體更新的 proxy 伺服器設定

如果貴組織使用 proxy 伺服器來控制存取網際網路，您需要讓反惡意程式碼引擎和定義更新可以成功下載識別 proxy 伺服器。可使用**Netsh.exe**工具、 Internet Explorer連線設定及*InternetWebProxy*參數**Set-ExchangeServer**指令程式上的 proxy 伺服器設定不會影響反惡意程式碼更新下載的方式。

若要設定反惡意軟體更新的 proxy 伺服器設定，請執行下列步驟。

1.  執行下列命令：
    
        Add-PsSnapin Microsoft.Forefront.Filtering.Management.Powershell

2.  使用**Get-ProxySettings**和**Set-ProxySettings** cmdlet 來檢視和設定可用來下載反惡意程式碼更新之 proxy 伺服器設定。**Set-ProxySettings**指令程式會使用下列語法：
    
        Set-ProxySettings -Enabled <$true | $false> -Server <Name or IP address of proxy server> -Port <TCP port of proxy server>
    
    例如，若要設定要使用的 proxy 伺服器位址 172.17.17.10 TCP 連接埠 80 的反惡意程式碼更新，請執行下列命令。
    
        Set-ProxySettings -Enabled $true -Server 172.17.17.10 -Port 80
    
    若要確認 proxy 伺服器設定，請執行**Get-ProxySettings**指令程式。

## 相關資訊

[設定反惡意程式碼原則](configure-anti-malware-policies-exchange-2013-help.md)


---
title: '使用複製的組態設定 Edge Transport server: Exchange 2013 Help'
TOCTitle: 使用複製的組態設定 Edge Transport server
ms:assetid: 0bbc83e3-e5e8-4480-a8a6-15f035360856
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996008(v=EXCHG.150)
ms:contentKeyID: 61180447
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用複製的組態設定 Edge Transport server

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-13_

您可以使用隨附的 Exchange 管理命令介面指令碼 (位於 %ExchangeInstallPath%Scripts 中) 來複製 Edge Transport Server 的設定。此處理程序稱為*「複製組態」*。*「複製組態」*是根據先前設定之來源伺服器的組態資訊來部署新 Edge Transport Server 的作法。先前設定的來源伺服器之組態資訊會複製及匯出至 XML 檔，然後該檔案會匯入至目標伺服器。如需此程序的概觀，請參閱[Edge Transport server 複製的組態](edge-transport-server-cloned-configuration-exchange-2013-help.md)。

Edge Transport Server 組態資訊會儲存在 Active Directory 輕量型目錄服務 (AD LDS) 中，而不會在多部 Edge Transport Server 之間複寫。使用複製組態，可確保您的周邊網路中所部署的每部 Edge Transport Server 都使用相同的組態。

有兩個命令介面指令碼可用來執行複製組態工作：

  - **ExportEdgeConfig.ps1**   從 Edge Transport Server 匯出所有使用者設定的設定及資料，並將該資料儲存在 .XML 檔案中。

  - **ImportEdgeConfig.ps1**   在驗證組態步驟期間，ImportEdgeConfig.ps1 指令碼會檢查匯出的 XML 檔案，了解伺服器特定的匯出設定對目標伺服器是否有效。如果必須修改設定，此指令碼會將無效的設定寫入至可由您修改以指定目標伺服器資訊的回應檔案，供後續執行匯入組態步驟時使用。在匯入組態步驟期間，此指令碼會匯入儲存在中繼 XML 檔案 (由 ExportEdgeConfig.ps1 指令碼所建立) 中的所有使用者設定的設定和資料。

這兩個指令碼都位於 %ExchangeInstallPath%Scripts 資料夾中。

## 開始之前

  - 完成此工作的預估時間：30 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「Edge Transport Server」項目。

  - 複製組態不會複製伺服器的 \[Edge 訂閱\] 設定。並不會複製 EdgeSync 憑證。您必須個別執行每部 Edge Transport Server 的 EdgeSync 處理程序。EdgeSync 會覆寫「複製組態」資訊和 EdgeSync 複寫資訊中所含的任何設定。

  - 如果已將任何傳送連接器設定為使用認證，則會將密碼當做加密的字串寫入中繼 XML 檔案。您可以使用 *-key* 參數搭配 ImportEdgeConfig.ps1 及 ExportEdgeConfig.ps1 指令碼，以指定用於密碼加密及解密的 32 位元組字串。如果未使用 *-key* 參數，則會使用預設加密金鑰。

  - 您只能使用命令介面來執行此程序。 若要了解如何在內部部署 Exchange 組織中開啟 Exchange 管理命令介面，請參閱[開啟命令介面。](https://technet.microsoft.com/zh-tw/library/dd638134\(v=exchg.150\))。

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


## 該怎麼做？

## 步驟 1：將來源伺服器組態資料匯出至來源伺服器上的檔案

1.  將 ExportEdgeConfig.ps1 指令碼複製到來源伺服器上您的使用者設定檔之根資料夾。

2.  若要將來源伺服器組態資料匯出至來源伺服器上的檔案，請使用下列語法。
    
        ./ExportEdgeConfig.ps1 -CloneConfigData:"<configuration file>"
    
    例如，若要將來源伺服器組態資料匯出至檔案 C:\\CloneConfigData.xml，請執行下列命令。
    
        ./ExportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml"

## 如何才能了解此步驟是否正常運作？

出現下列確認訊息時，即表示您已順利將來源組態資料匯出至檔案：「Edge 組態資料已順利匯出至：\<輸出檔路徑\>」。

## 步驟 2：驗證組態檔，並在目標伺服器上建立回應檔案

1.  將您在上一個步驟中匯出的來源伺服器組態檔，複製到目標 Edge Transport Server。

2.  將 ImportEdgeConfig.ps1 指令碼複製到目標伺服器上您的使用者設定檔之根資料夾。

3.  若要驗證組態檔，並使用結果在目標伺服器上建立回應檔案，請使用下列語法。
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"<configuration file>" -IsImport $false -CloneConfigAnswer:"<answer file>"
    
    例如，若要驗證組態檔 C:\\CloneConfigData.xml，並建立回應檔案 C:\\CloneConfigAnswer.xml，請執行下列命令。
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $false -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

4.  開啟回應檔案並修改任何對目標伺服器無效的設定。如果不需要修改，回應檔案將不含任何項目。儲存變更。

## 如何才能了解此步驟是否正常運作？

出現確認訊息「已順利建立回應檔案」時，即表示您已順利驗證組態檔並建立回應檔案。

## 步驟 3：在目標伺服器上匯入組態檔

若要在目標伺服器上匯入組態檔，請使用下列語法。

    ./ImportEdgeConfig.ps1 -CloneConfigData:"<Configuration file>" -IsImport $true -CloneConfigAnswer:"<answer file>"

例如，若要使用回應檔案 C:\\CloneConfigAnswer.xml 匯入組態檔 C:\\CloneConfigData.xml，請執行下列命令。

    ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $true -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

## 如何才能了解此步驟是否正常運作？

出現確認訊息「Edge 組態資訊匯入成功」時，即表示您已順利在目標伺服器上匯入組態檔。


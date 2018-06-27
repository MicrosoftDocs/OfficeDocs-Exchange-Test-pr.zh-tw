---
title: '建立外部連接器將郵件傳送至非 SMTP 傳真閘道: Exchange 2013 Help'
TOCTitle: 建立外部連接器將郵件傳送至非 SMTP 傳真閘道
ms:assetid: 589db487-3c4c-409a-92e3-c78dd8f639b6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ710163(v=EXCHG.150)
ms:contentKeyID: 50473250
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立外部連接器將郵件傳送至非 SMTP 傳真閘道

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-17_

您可能會有您要傳送郵件給及從傳真閘道伺服器做為其主要傳輸機制不使用 SMTP 接收訊息的案例。遵循此程序可建立外部連接器傳送郵件給並接收來自外部系統的訊息中所述的步驟。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須將外寄郵件傳遞給非 SMTP 系統大多數的情況下，我們建議傳遞代理程式連接器，因為他們允許之訊息的佇列管理、 訊息沒有寫入檔案系統與其他優點。<a href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">傳遞代理程式及傳遞代理程式連接器</a>主題提供更多詳細資料。</td>
</tr>
</tbody>
</table>


對於案例感興趣一角與使用此程序？請參閱下列主題：

  - [規劃及部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)

## 開始之前有哪些須知？

  - 完成此工作的預估時間：30 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「外部連接器」項目。

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

## 步驟 1： 使用命令介面建立將郵件傳送至非 SMTP 閘道伺服器的外部連接器

1.  執行下列命令來建立外部連接器：
    
        New-ForeignConnector -Name "Contoso Foreign Connector" -AddressSpaces "X400:c=US;a=Fabrikam;P=Contoso;5" -SourceTransportServers Hub01,Hub02
    
    在本例中為 Hub01 和 Hub02 是您要指定將郵件傳送至外部系統貴組織中的來源伺服器。使用多個來源伺服器提供容錯。

一旦您建立外部連接器，則可設定放置收取以及重新顯示目錄，視組織的要求而定。

## 如何才能了解此步驟是否正常運作？

若要確認成功建立外部連接器，請執行下列命令：

    Get-ForeignConnector | Format-List Name

確認您建立的外部連接器名稱已顯示。

## 步驟 2： 使用命令介面來設定信箱伺服器執行的傳輸服務放置目錄

執行傳輸服務的信箱伺服器之放置目錄是用來傳送從外部連接器輸出的郵件。

您建立要當成本機檔案系統上放置目錄的目錄。您也可以使用網路檔案共用上的目錄。

1.  執行下列指令碼來指定外部連接器的放置目錄（將 *DropDirectory* 參數值變更為適合您環境的路徑）：
    
        Set-ForeignConnector "Contoso Foreign Connector" -DropDirectory "C:\Drop Directory"

## 如何才能了解此步驟是否正常運作？

若要確認您正確設定放置目錄，可執行下列指令程式指令碼，並確認 *DropDirectory* 參數值：

    Get-ForeignConnector "Contoso Foreign Connector" | Format-List

一旦您已建立外部連接器且指定您的放置目錄，則可使用建立外部連接器的信箱伺服器來傳送郵件，並確認檔案傳遞至放置目錄。

## 步驟 3： 使用命令介面來設定信箱伺服器上的傳輸服務的 \[收取\] 目錄

在信箱伺服器上的傳輸服務的 \[收取\] 目錄用來收集非 SMTP 系統所產生的訊息。在您要收集產生的非 SMTP 系統，例如傳真閘道伺服器，藉由檔案傳輸的新郵件的情況下使用此程序。

若欲瞭解設定 \[收取\] 目錄的詳細說明，請參閱 [設定 \[收取\] 目錄和重新顯示目錄](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md)。

## 如何才能了解此步驟是否正常運作？

若要確認您正確設定收取目錄，可執行下列指令程式，並確認 *PickupDirectoryPath* 參數值：

    Get-TransportService | Format-List PickupDirectoryPath

## 步驟 4： 使用命令介面來設定信箱伺服器上的傳輸服務的重新顯示\] 目錄

在信箱伺服器上的傳輸服務的重新顯示目錄用來收集非 SMTP 系統所產生的訊息。使用此程序可在您要重新提交電子郵件訊息，通常是從非 SMTP 外部閘道伺服器所產生的Exchange環境及匯出從 Exchange 傳輸的情況下設定重新顯示目錄。

若欲瞭解設定 \[收取\] 目錄的詳細說明，請參閱 [設定 \[收取\] 目錄和重新顯示目錄](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md)。

## 如何才能了解此步驟是否正常運作？

若要確認您正確設定重新顯示目錄，可執行下列指令程式，並確認 *ReplayDirectoryPath* 參數值：

    Get-TransportService | Format-List ReplayDirectoryPath

## 相關資訊

[外部連接器](foreign-connectors-exchange-2013-help.md)

[傳遞代理程式及傳遞代理程式連接器](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)


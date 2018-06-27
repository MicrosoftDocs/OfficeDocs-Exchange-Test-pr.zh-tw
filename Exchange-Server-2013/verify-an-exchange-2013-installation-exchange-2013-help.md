---
title: '確認 Exchange 2013 安裝: Exchange 2013 Help'
TOCTitle: 確認 Exchange 2013 安裝
ms:assetid: fdd20a2a-c8c1-4d17-b813-3c05d88a4411
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125254(v=EXCHG.150)
ms:contentKeyID: 50474683
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 確認 Exchange 2013 安裝

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

在您安裝 Microsoft Exchange Server 2013之後，建議您確認安裝執行**Get-ExchangeServer**指令程式並透過檢閱安裝記錄檔。如果安裝程序失敗或在安裝期間發生錯誤，您可以使用安裝程式記錄檔來追蹤問題的來源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。

## 執行 Get-ExchangeServer

若要確認是否已成功安裝 Exchange 2013，請在 Exchange 管理命令介面中執行 **Get-ExchangeServer** Cmdlet。當此指令程式執行時，會顯示一個清單，列出已在指定的伺服器上安裝的所有 Exchange 2013 伺服器角色。

如需詳細語法及參數的資訊，請參閱 [Get-ExchangeServer](https://technet.microsoft.com/zh-tw/library/bb123873\(v=exchg.150\))。

## 檢閱安裝記錄檔

透過檢閱安裝程序間建立的安裝記錄檔，也可以深入了解 Exchange 2013 的安裝和組態。

在安裝期間，Exchange 安裝程式會在執行 Windows Server 2008 R2 Service Pack 1 (SP1) 以及 Windows Server 2012 的電腦上之 **\[事件檢視器\]** 的 **\[應用程式\]** 記錄檔中記錄事件。請檢閱 **\[應用程式\]** 記錄檔，確認沒有 Exchange 安裝的相關警告或錯誤訊息。這些記錄檔包含 Exchange 2013 安裝期間系統採取之每個動作的歷程記錄，以及任何發生的錯誤。依預設，記錄方法設為`Verbose`。每個安裝的伺服器角色都有相關的資訊。

您可在 *\<system drive\>*\\ExchangeSetupLogs\\ExchangeSetup.log 找到安裝記錄檔。*\<system drive\>* 變數代表安裝作業系統之磁碟的根目錄。

安裝記錄檔會追蹤 Exchange 2013 安裝及組態期間所執行之每一項工作的進度。這個檔案包含安裝啟動前所執行之必要條件及系統就緒檢查的狀態、應用程式安裝進度，以及對系統所做組態變更的相關資訊。檢查此記錄檔，以驗證是否已經如預期般安裝伺服器角色。

建議您開始檢閱安裝記錄檔的第一步，是搜尋是否有任何錯誤。如果您發現表示發生錯誤的項目，請閱讀相關的文字以判斷錯誤的原因。


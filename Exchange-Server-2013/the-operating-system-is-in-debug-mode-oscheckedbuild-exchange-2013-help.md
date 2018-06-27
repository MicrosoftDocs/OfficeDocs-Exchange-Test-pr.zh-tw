---
title: '作業系統是在偵錯 mode_OSCheckedBuild: Exchange 2013 Help'
TOCTitle: 作業系統是在偵錯 mode_OSCheckedBuild
ms:assetid: 93a1380f-1388-494d-8f78-92dfefd069bd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.oscheckedbuild(v=EXCHG.150)
ms:contentKeyID: 50473794
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 作業系統是在偵錯 mode\_OSCheckedBuild

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-15_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server Analyzer 工具查詢**Win32\_OperatingSystem** Microsoft Windows® Management Instrumentation (WMI) 類別來決定是否**偵錯**屬性設定值。如果 Exchange Server 電腦上的此機碼的值設為**True**，會顯示錯誤。

Windows 偵錯模式已切換 Boot.ini 檔案中**新增/debug**參數。Windows Server 電腦 Boot.ini 檔案中指定**偵錯 /**時, 核心偵錯工具會在啟動時載入並一直保持在記憶體中。這可讓支援專業人員的撥號對應表中的系統正在偵錯及自動換行以偵錯工具，即使在核心停止\] 畫面上未暫停系統。不同**/crashdebug交換器/debug**參數是否在偵錯或不使用 COM 連接埠。偵錯會定期重現問題時使用此參數。很**可能/偵錯**參數設為以疑難排解問題、 方法及小心地保留設定。

因所執行的其他程序，效能會大幅受損。因此，不建議在偵錯模式中執行 Windows 的電腦上執行 Exchange Server。

若要去除這項錯誤，編輯 Boot.ini 檔案並**移除/偵錯**參數。

## 若要更正此錯誤

1.  在 \[Windows 檔案總管瀏覽至系統磁碟分割。這是包含如 Boot.ini 及 NTLDR 硬體特定檔案的磁碟分割。

2.  如果您不能看到 Boot.ini 檔案，它可能是因為**資料夾選項**\] 設定為 \[**隱藏保護作業系統檔案**。如果是這樣，在 \[Windows 檔案總管\] 視窗中，按一下 \[**工具\]**、 \[**資料夾選項**\]，和 \[**檢視**。清除 \[**隱藏保護作業系統檔案 （建議使用）** \] 核取方塊。出現提示時，按一下 \[**是**\]。

3.  在 Windows 檔案總管中顯示 Boot.ini 檔案時，請以滑鼠右鍵按一下檔案、 按一下**開啟與**，然後選取**\[記事本\] 中**開啟檔案。

4.  在**\[作業系統\]**區段中，會**移除/偵錯**參數。

5.  儲存並關閉檔案，然後再重新啟動 Exchange Server 電腦讓變更生效。

更多可用 Boot.ini 檔案中的參數的詳細資訊，請參閱 Microsoft 知識庫文章 833721、 「 Windows XP 及 Windows Server 2003 Boot.ini 檔可用的切換參數選項 」 ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=833721](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=833721))。


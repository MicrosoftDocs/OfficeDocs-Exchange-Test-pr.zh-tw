---
title: 'IIS 記錄檔和記錄剖析器 Studio 報告: Exchange 2013 Help'
TOCTitle: IIS 記錄檔和記錄剖析器 Studio 報告
ms:assetid: 01fa67d4-dc02-4c5f-93af-6da7b97d282f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn904092(v=EXCHG.150)
ms:contentKeyID: 63910974
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS 記錄檔和記錄剖析器 Studio 報告

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

## 分析記錄剖析器 Studio 報告

Log Parser Studio 是可讓您透過搜尋並建立報告數種類型的記錄檔，包括網際網路資訊服務 (IIS) 公用程式。 它組建記錄剖析器 2.2 上方，且輕鬆建立及管理相關的 SQL 查詢的完整使用者介面。

[下載 Log Parser Studio](https://go.microsoft.com/fwlink/p/?linkid=524244)與然後檢閱部落格文章[Log Parser Studio 入門](https://go.microsoft.com/fwlink/p/?linkid=524243)。

請記得在 Exchange 2013，所有流量移到 IIS。 這表示分析 IIS 記錄檔是最適合以取得完整的方式來點擊 server、 連線的特定通訊協定的資訊和大部分的使用者會影響效能的連線數目的圖片。 超過二十個新報告已針對 Log Parser Studio，開發基於疑難排解 Exchange 2013 的效能問題。

## Log Parser Studio 報告的 Exchange 2013 的效能問題

若要取得在 Exchange 2013 環境中的整體負載完整了解，使用下列報告功能和比較針對每部伺服器的數字。

包含的列在這裡、 Log Parser Studio 報告和其他疑難排解與相關的報告的.zip 檔案可以[從這裡下載](https://go.microsoft.com/fwlink/p/?linkid=524245)。

  - **IIS︰ 每小時的要求**。摘要中 IIS 記錄檔從 \[Default Web Site (W3SVC1 directory) 或後端網站 (W3SVC2 directory)、 但不可同時在同一時間。

  - **ACTIVESYNC\_WP： %的用戶端**。計算所有 ActiveSync 要求細分的使用者代理程式以及每個用戶端百分比的要求總數。

  - **ACTIVESYNC\_WP： 要求每小時 (CSV)**。列出每小時 ActiveSync 要求並將結果傳送至 CSV 檔案。

  - **ACTIVESYNC\_WP： 要求每位使用者 (CSV)**。列出每個使用者的 ActiveSync 要求並將結果傳送至 CSV 檔案。

  - **ACTIVESYNC\_WP： 要求每位使用者 （頂端 10k）**。列出 ActiveSync 要求每位使用者的上方 10000 位使用者。

  - **ACTIVESYNC\_WP︰ 最常用的說話者包括代表 (CSV)**。列出上方 ActiveSync 用戶端從最高至最低要求的計數，並將結果傳送至 CSV 檔案。

  - **EWS\_WP： %的用戶端**。計算所有 EWS 要求細分的使用者代理程式以及每個用戶端百分比的要求總數。

  - **EWS\_WP： 要求每小時 (CSV)**。列出每小時的 EWS 要求的總數。

  - **EWS\_WP： 每位使用者 (CSV) 要求**。列出每個使用者的 EWS 要求並將結果傳送至 CSV 檔案。

  - **EWS\_WP： 要求每位使用者 （頂層 10k）**。列出每位使用者的上方 10000 位使用者的 EWS 要求。

  - **EWS\_WP︰ 最常用的說話者包括代表 (CSV)**。列出上的 EWS 用戶端從最高最低要求計數。

  - **OLA\_WP： 錯誤，每位使用者，每小時、 每天**。Outlook 無所不在的使用者使用的要求數目。

  - **OLA\_WP： 每小時的要求**。列出 「 Outlook 無所不在 」 要求每小時。

  - **OLA\_WP： 每小時、 每位使用者要求**。列出 「 Outlook 無所不在 」 要求每小時、 每位使用者。

  - **OLA\_WP： 要求每位使用者 (CSV)**。列出 「 Outlook 無所不在 」 要求每位使用者。

  - **OLA\_WP： 要求每位使用者 （頂層 10k）**。列出 「 Outlook 無所不在 」 要求每位使用者的頂端 10000 個使用者。

  - **OLA\_WP︰ 最常用的說話者包括代表**。列出上的 Outlook 無所不在用戶端從最高最低要求計數。

  - **OWA\_WP: %的用戶端**。計算所有 OWA 要求細分的使用者代理程式以及每個用戶端百分比來要求總數。

  - **OWA\_WP： 要求每小時 (CSV)**。列出每小時 OWA 要求並將結果傳送至 CSV 檔案。

  - **OWA\_WP： 要求每位使用者 (CSV)**。列出每個使用者的 OWA 要求並將結果傳送至 CSV 檔案。

  - **OWA\_WP： 要求每位使用者 （頂端 10k）**。列出 OWA 要求每位使用者的上方 10000 位使用者。

  - **OWA\_WP︰ 最常用的說話者包括代表 (CSV)**。列出上方 OWA 的用戶端最高至最低要求的計數，並將結果傳送至 CSV 檔案。


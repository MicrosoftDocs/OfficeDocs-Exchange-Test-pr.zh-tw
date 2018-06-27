---
title: '檢視效能計數器的通訊記錄管理: Exchange 2013 Help'
TOCTitle: 檢視效能計數器的通訊記錄管理
ms:assetid: ec374d31-2797-4f8b-8c96-3839d01a662c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb397227(v=EXCHG.150)
ms:contentKeyID: 51409255
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視效能計數器的通訊記錄管理

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2009-12-09_

您可以使用Windows可靠性和效能監視器 (Perfmon.exe) 選取 \[及檢視通訊記錄管理 (MRM) 的效能計數器。藉由使用效能計數器，您可以監視受管理的資料夾助理員時執行大量消耗資源的 MRM 處理程序。

如需 MRM 的效能計數器清單，請參閱[通訊記錄管理的效能計數器](performance-counters-for-messaging-records-management-exchange-2013-help.md)。

要尋找其他工作相關監控 MRM 嗎？取出[監視通訊記錄管理](monitoring-messaging-records-management-exchange-2013-help.md)。

## 使用 Windows 可靠性和效能監視器檢視 MRM 效能計數器

若要執行此程序，必須對您使用的帳戶委派本機 Administrators 群組的成員資格。

1.  若要啟用「Windows 可靠性和效能監視器」，請依序按一下 **\[開始\]**、**\[執行\]**，然後輸入 **perfmon**。

2.  在主控台樹狀目錄中，瀏覽至 **\[監視工具\]** \> **\[效能監視器\]**。

3.  按一下工具列上的加號 （+） 按鈕。**新增計數器**\] 對話方塊隨即出現。

4.  在 **\[從下列電腦選取計數器\]** 清單中，選取下列其中一個選項：
    
      - 如果您本機電腦上執行此程序，請選取 \[ **\< 本機電腦 \>**。此為預設選取項目。
    
      - 如果您是在遠端執行此程序，請選取要監視的伺服器。

5.  在效能計數器清單中，展開 **\[MSExchange Assistants - Per Database\]** 或 **\[MSExchange Managed Folder Assistant\]**。

6.  選取您想要監視的效能計數器。

7.  \[ **MSExchange 助理-每個資料庫**的效能計數器若要檢視所有的信箱資料庫的計數器中**所選取物件的執行個體**，請按一下 \[**所有執行個體**。或者，若要指定一或多個信箱資料庫，請從清單中選取執行個體。

8.  若要新增選取的計數器，以讓其顯示於「Windows 可靠性和效能監視器」並開始收集效能資料，請按一下 **\[新增\]**。


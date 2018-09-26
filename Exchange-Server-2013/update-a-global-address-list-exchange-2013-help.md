﻿---
title: '更新全域通訊清單: Exchange 2013 Help'
TOCTitle: 更新全域通訊清單
ms:assetid: 236e8530-62dd-4c43-8a5d-8465623252e6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb266966(v=EXCHG.150)
ms:contentKeyID: 50472826
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更新全域通訊清單

 

_**適用版本：** Exchange Server 2013_

_**上次修改主題的時間：** 2014-12-16_

您可以使用命令介面來更新全域通訊清單 (GAL)。GAL 是一個目錄，內含組織執行 MicrosoftExchange 時所使用的每個群組、使用者與連絡人的項目。

如需與通訊清單相關的其他管理工作，請參閱[地址清單程序](address-list-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md)主題中的「通訊清單」項目。

  - 根據 Exchange Online 的預設，「通訊清單」角色並未指派給任何角色群組。若要使用任何需要「通訊清單」角色的指令程式，您需將此角色新增至角色群組。如需詳細資訊，請參閱＜[管理角色群組](manage-role-groups-exchange-2013-help.md)＞主題的＜將角色新增至角色群組＞一節。

  - 您無法使用 Exchange 系統管理中心 (EAC) 執行此程序。您必須使用命令介面。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。


> [!TIP]  
> 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。




## 使用命令介面來更新 GAL

此範例會更新 Fourth Coffee 公司的 GAL。


> [!NOTE]  
> 執行這個命令只會啟動更新程序。更新 GAL 可能需要數個小時。




```powershell
Update-GlobalAddressList -Identity "Fourth Coffee"
```

如需詳細的語法及參數資訊，請參閱 [Update-GlobalAddressList](https://technet.microsoft.com/zh-tw/library/aa998806\(v=exchg.150\))。


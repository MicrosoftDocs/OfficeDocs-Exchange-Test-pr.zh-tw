---
title: 與部署相關的程序
TOCTitle: 與部署相關的程序
ms:assetid: 6b7682bd-fe3d-43b9-a7db-66c0ac17656f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn195909(v=EXCHG.150)
ms:contentKeyID: 53276427
ms.date: 08/29/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 與部署相關的程序

 

_**上次修改主題的時間：** 2013-04-17_

本節包含使用 Exchange Server 2013 管理組件時可參考的程序。如需部署後作業的相關程序，請參閱[Procedures related to post-deployment operation](procedures-related-to-post-deployment-operation.md)。

## 驗證代理程式部署狀態

在匯入 Exchange Server 2013 管理組件之前，請確認 Exchange 伺服器上的 SCOM 代理程式正常運作，而且已經在 SCOM 中正確地報告作業系統健全狀態。

您的使用者帳戶必須是 Operations Manager Administrators 角色的成員，才能執行此程序。

1.  登入 SCOM 伺服器並開啟 SCOM 主控台。

2.  按一下 **\[監視\]**，然後再按 **\[Windows 電腦\]**。

3.  確定所有 Exchange 伺服器都顯示 **\[正常\]**。

![SCOM 主控台中的狀況良好代理程式](images/Dn195909.7d1ff0bb-419e-40dc-babf-5fa2fb7229a8(EXCHG.150).png "SCOM 主控台中的狀況良好代理程式")

## 驗證代理程式 Proxy 組態

在匯入 Exchange Server 2013 管理組件之前，請在 SCOM 中確認代理程式 Proxy 已啟用探索。否則，Exchange 伺服器的代理程式不會報告 Exchange 健全狀態。您需要針對所有 Exchange Server 驗證此組態。

您的使用者帳戶必須是 Operations Manager Administrators 角色的成員，才能執行此程序。

1.  登入 SCOM 伺服器並開啟 SCOM 主控台。

2.  在 \[作業\] 主控台中，按一下 **\[管理\]**。

3.  按一下 **\[代理程式管理\]**。在 Exchange 伺服器上按一下滑鼠右鍵，然後按一下 **\[內容\]**。

4.  在 **\[安全性\]** 索引標籤上，確認已選取 **\[允許此代理程式作為 Proxy 並探索其他電腦中的受管理物件\]** 核取方塊。

5.  按一下 **\[確定\]**。

## 驗證代理程式安全性組態

由於測試 Exchange 2013 時所用的安全性模型，不支援在 Exchange 伺服器上以 **LocalSystem** 以外的任何帳戶執行 SCOM 代理程式。如果以 LocalSystem 以外的任何帳戶執行代理程式，綜合交易會無法執行。您可能還會遇到其他問題。

您的使用者帳戶必須是 Server Management 角色群組的成員，才能執行此程序。

1.  登入 Exchange 伺服器。

2.  按一下 **\[開始\]** \> **\[系統管理工具\]** \> **\[服務\]**。

3.  將服務清單向下捲動，找到 **\[System Center Management\]** 服務。

4.  確認 **\[登入身分\]** 欄位顯示 **\[Local System\]**。

5.  如果 **\[登入身分\]** 欄位顯示其他值，請將服務登入變更為 Local System。
    
    1.  在 **\[System Center Management\]** 服務上按一下滑鼠右鍵，選取 **\[內容\]**。
    
    2.  按一下 **\[登入\]** 索引標籤。
    
    3.  按一下 **\[本機系統帳戶\]** 選項。
    
    4.  按一下 **\[確定\]**。


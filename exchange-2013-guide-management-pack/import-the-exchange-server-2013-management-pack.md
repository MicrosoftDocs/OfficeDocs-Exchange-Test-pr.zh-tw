---
title: 匯入 Exchange Server 2013 管理組件
TOCTitle: 匯入 Exchange Server 2013 管理組件
ms:assetid: dc929928-61b8-448b-9ae5-d3fa73a18ee9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn195914(v=EXCHG.150)
ms:contentKeyID: 53276432
ms.date: 08/29/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 匯入 Exchange Server 2013 管理組件

 

_**上次修改主題的時間：**  2013-03-30_

讓我們從匯入管理組件到您的 SCOM 部署中開始。

## 必要條件

在匯入管理組件之前，請先確認已符合下列條件：

  - 您的組織中已部署下列其中一個版本的 System Center Operations Manager：
    
      - System Center Operations Manager 2012 RTM 或更新版本
    
      - System Center Operations Manager 2007 R2 或更新版本

  - 您已將 SCOM 代理程式部署至您的 Exchange Server。[驗證代理程式部署狀態](procedures-related-to-deployment.md).

  - Exchange Server 上的 SCOM 代理程式正以本機系統帳戶來執行。[驗證代理程式安全性組態](procedures-related-to-deployment.md).

  - Exchange Server 上的 SCOM 代理程式已設定作為 Proxy，並且探索其他電腦上的受管理物件。[驗證代理程式 Proxy 組態](procedures-related-to-deployment.md).

  - 您的使用者帳戶是 Operations Manager 系統管理員角色的成員。

## 匯入 Exchange Server 2013 管理組件

使用下列步驟來匯入 Exchange Server 2013 管理組件。此程序假設您已將管理組件內容解壓縮至 System Center Operations Manager (SCOM) 伺服器上的本機磁碟。您可以從下列位置來下載 Exchange Server 2013 管理組件。

1.  登入您的 SCOM 伺服器，並從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/p/?linkid=268587)下載 Exchange Server 2013 管理組件。

2.  執行 `ExchangeServerManagementPack.msi` 檔，將管理組件內容解壓縮至您系統上的資料夾。

3.  啟動 SCOM 主控台。在 SCOM 主控台中，按一下 **\[管理\]**。

4.  在 **\[管理組件\]** 上按一下滑鼠右鍵，然後按一下 **\[匯入管理組件\]**。

5.  \[匯入管理組件\] 精靈便會開啟。按一下 **\[新增\]**，然後按一下 **\[從磁碟新增\]**。

6.  **\[選取要匯入的管理組件\]** 對話方塊隨即出現。瀏覽至您將管理組件解壓縮到的目錄。按一下 `Microsoft.Exchange.15.mp` 檔，然後按一下 **\[開啟\]**。

7.  在 **\[選取管理組件\]** 頁面上會列出 Exchange Server 2013 管理組件。按一下 **\[安裝\]**。

8.  **\[匯入管理組件\]** 頁面隨即出現並顯示進度。如果在匯入程序期間出現任何問題，選取清單中的管理組件以檢視狀態詳細資料。

9.  當匯入完成時，請按一下 \[關閉\]。

10. 依序按一下 **\[檢視\]** 和 **\[重新整理\]**，或按 F5 鍵，即可在 \[管理組件\] 清單中看到 Microsoft Exchange Server 2013 管理組件。

現在您已匯入管理組件，請參閱 [Exchange Server 2013 管理組件快速入門](getting-started-with-exchange-server-2013-management-pack.md)來深入了解新的儀表板。


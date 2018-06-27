---
title: '設定信箱資料庫的循環記錄: Exchange 2013 Help'
TOCTitle: 設定信箱資料庫的循環記錄
ms:assetid: 29cbd7cd-382b-4e0d-8368-2e49e75df2fc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn756374(v=EXCHG.150)
ms:contentKeyID: 62524850
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定信箱資料庫的循環記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-06-24_

對信箱資料庫啟用循環記錄時，您得到的循環記錄類型取決於您是否使用連續複寫來複寫信箱資料庫：

  - 如果不複寫信箱資料庫，則會使用 JET 循環記錄。在此情況下，啟用或停用 JET 循環記錄需要卸載和裝載資料庫。

  - 如果複寫信箱資料庫，則會使用連續複寫循環記錄 (CRCL)。在此情況下，啟用或停用 CRCL 會動態生效，並不需要卸載和重新裝載資料庫。

如需循環記錄和 CRCL 的詳細資訊，請參閱＜[Exchange Native Data Protection](backup-restore-and-disaster-recovery-exchange-2013-help.md)＞。

## 開始之前有哪些須知？

  - 預估完成時間：1 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱＜[收件者權限](recipients-permissions-exchange-2013-help.md)＞主題中的「信箱資料庫權限」項目。

## 使用 EAC 來設定資料庫的循環記錄

1.  在 EAC 中，移至 **\[伺服器\]** \> **\[資料庫\]**。

2.  選取要設定的信箱資料庫，然後按一下 ![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  選取或取消選取 **\[啟用循環記錄\]** 核取方塊，然後按一下 **\[儲存\]**。

4.  如果需要卸載和裝載作業，則會出現警告訊息。按一下 **\[確定\]** 關閉警告訊息。
    
    1.  若要卸載資料庫，請按一下 **\[其他\]**![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示")，然後按 **\[卸載\]**。出現警告訊息時，按一下 **\[是\]**。
    
    2.  若要裝載資料庫，請按一下 **\[其他\]**![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示")，然後按 **\[裝載\]**。出現警告訊息時，按一下 **\[是\]**。

## 使用命令介面來設定資料庫的循環記錄

本範例啟用資料庫 DB1 的循環記錄。

    Set-MailboxDatabase DB1 -CircularLoggingEnabled $True

本範例停用資料庫 DB1 的循環記錄。

    Set-MailboxDatabase DB1 -CircularLoggingEnabled $False

關於您可以設定的其他信箱資料庫參數，請參閱 [Set-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb123971\(v=exchg.150\))。


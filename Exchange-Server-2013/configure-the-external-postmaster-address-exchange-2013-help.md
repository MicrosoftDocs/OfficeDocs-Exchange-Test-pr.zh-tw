---
title: '設定外部郵件管理員地址: Exchange 2013 Help'
TOCTitle: 設定外部郵件管理員地址
ms:assetid: 6b0c8675-3238-462d-8973-b52305fb90d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb430765(v=EXCHG.150)
ms:contentKeyID: 52062548
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定外部郵件管理員地址

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

外部該地址會當做寄件者的系統產生的郵件及存在於 Microsoft Exchange Server 2013組織外的郵件寄件者的通知。外部寄件為具有電子郵件的地址不設定為在組織中公認的網域的網域中任何寄件。

根據預設，外部郵件管理員位址設定的值是空白的。此預設值會導致 Exchange 組織中的下列行為：

  - 所有 Mailbox Server 和訂閱的 Edge Transport Server 的外部郵件管理員地址是 postmaster@\<*預設接受的網域*\>。

  - 所有未訂閱的 Edge Transport Server 的外部郵件管理員地址是 postmaster@\<*Edge Transport server FQDN*\>。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸組態」項目。

  - 設定自訂的外部郵件管理員地址，值會套用到所有Exchange 2013信箱伺服器和 Exchange 組織中的部署Exchange 2010 Hub Transport server 時。不過，該值未複寫至 Edge Transport server。如果您指定自訂值作為外部該地址時，您需要手動設定任何 Edge Transport server 上的 \[外部郵件管理員的 \[位址\] 值。

  - 如果您在組織中有任何Exchange 2007 Hub Transport server 或 Edge Transport server，您需要在每個使用**Set-TransportServer**指令程式這些伺服器上設定自訂的外部該地址。如需詳細資訊，請參閱 ＜[管理外部該地址](https://go.microsoft.com/fwlink/?linkid=279922)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 使用 EAC 設定外部郵件管理員地址

1.  在 EAC 中，瀏覽至 **\[郵件流程\]** \> **\[接收連接器\]** \> **\[其他選項\]**![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示") \> **\[組織傳輸設定\]** \> **\[傳遞\]** 索引標籤。

2.  在 \[**外部郵件管理員地址**\] 欄位中輸入 SMTP 電子郵件地址，例如`postmaster@contoso.com`。如果您想要傳回外部該地址為預設值，所以欄位是空白刪除任何現有的值。

3.  完成作業後，按一下 **\[儲存\]**。

## 使用命令介面設定外部郵件管理員地址

若要設定外部郵件管理員地址，請使用下列語法。

    Set-TransportConfig -ExternalPostmasterAddress <postmaster address>

例如，若要將外部郵件管理員地址設為 `postmaster@contoso.com`，請執行下列命令

    Set-TransportConfig -ExternalPostmasterAddress postmaster@contoso.com

若要將外部郵件管理員地址回復為預設值，請執行下列命令：

    Set-TransportConfig -ExternalPostmasterAddress $null

## 如何才能了解這是否正常運作？

若要驗證您是否已成功設定外部郵件管理員地址，請執行下列動作：

1.  在 Mailbox Server 上執行下列命令來確認外部郵件管理員地址值：
    
        Get-TransportConfig | Format-List ExternalPostmasterAddress

2.  從外部電子郵件帳號傳送一則訊息將會產生傳遞狀態通知 (DSN) 您 Exchange 組織。例如，您可以設定傳輸規則來傳送未傳遞回報 (NDR) 中包含特定關鍵字的寄件者的郵件。請確認 DSN 中的寄件者的電子郵件地址符合您指定的值。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。


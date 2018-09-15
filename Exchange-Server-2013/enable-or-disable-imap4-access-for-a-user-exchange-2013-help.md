﻿---
title: '啟用或停用使用者的 IMAP4 存取: Exchange 2013 Help'
TOCTitle: 啟用或停用使用者的 IMAP4 存取
ms:assetid: a685fae4-b6f1-42fe-8bdc-5f99f9617799
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb676481(v=EXCHG.150)
ms:contentKeyID: 50473881
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用使用者的 IMAP4 存取

 

_**適用版本：** Exchange Server 2013_

_**上次修改主題的時間：** 2013-01-18_

您可以對使用者啟用或停用 IMAP4。


> [!NOTE]  
> 您已啟用或停用使用者的 IMAP4 之後，您必須重新啟動 Microsoft Exchange IMAP4 服務和 Microsoft Exchange IMAP4 後端服務。如需如何重新啟動 IMAP4 服務的詳細資訊，請參閱<a href="start-and-stop-the-imap4-services-exchange-2013-help.md">啟動及停止 IMAP4 服務</a>。




如需管理使用者信箱的相關資訊，請參閱[管理使用者信箱](https://docs.microsoft.com/zh-tw/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes)。

如需 POP3 與 IMAP4 的詳細資訊，請參閱 [Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「收件者佈建權限」一節。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。


> [!TIP]  
> 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.




## 您要執行的工作

## 使用 EAC 來啟用或停用使用者的 IMAP4

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在結果窗格中，選取要啟用或停用 IMAP4 的使用者，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[使用者信箱\] 對話方塊中，按一下控制台樹狀結構中的 \[信箱功能\]。
    
    在結果窗格的 \[電子郵件連線\] 下，進行下列其中一項動作：
    
      - 若要停用使用者的 IMAP4，請在 \[IMAP4:已啟用\]，按一下 \[停用\]。
    
      - 若要啟用使用者的 IMAP4，請在 \[IMAP4:已停用\]，按一下 \[啟用\]。

4.  按一下 **\[儲存\]**。

## 使用命令介面來啟用或停用使用者的 IMAP4

本範例會對使用者 John Smith 啟用 IMAP4。

    Set-CASMailbox -Identity "John Smith" -IMAPEnabled $true

此範例會對使用者 John Smith 停用 IMAP4。

    Set-CASMailbox -Identity "John Smith" -IMAPEnabled $false

## 如何才能了解這是否正常運作？

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在結果窗格中，選取要啟用或停用 IMAP4 的使用者，然後按一下 \[編輯\]。

3.  在 \[使用者信箱\] 對話方塊中，按一下控制台樹狀結構中的 \[信箱功能\]。
    
    在結果窗格中，查看 \[電子郵件連線\]。
    
      - 如果使用者的 IMAP4 已啟用，則您將看到 \[IMAP4:已啟用\]。
    
      - 若未啟用使用者的 IMAP4，您會看到**IMAP4 ︰ 已停用**。

4.  按一下 **\[儲存\]**。


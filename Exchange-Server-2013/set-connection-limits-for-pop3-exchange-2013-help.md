---
title: '設定的 POP3 連線限制: Exchange 2013 Help'
TOCTitle: 設定的 POP3 連線限制
ms:assetid: 512d61c2-2a34-4813-92a9-875339d3388b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997988(v=EXCHG.150)
ms:contentKeyID: 50553982
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定的 POP3 連線限制

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-28_

您可以使用 EAC 或命令介面管理組織的 POP3 連線限制。

指定 POP3 的連線限制時，您可以選取伺服器、IP 位址或特定使用者的連線限制。

如需 POP3 的詳細資訊，請參閱 [Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「POP3 設定」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用 EMC 設定伺服器、IP 位址或使用者的 POP3 連線限制

1.  在 EAC 中，瀏覽至 \[伺服器\]**\>** \[伺服器\]。

2.  在伺服器清單中選取 Client Access Server，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在伺服器內容頁面上，按一下 \[POP3\]。

4.  向下捲動並按一下 \[更多選項\]。

5.  在 \[連線限制\] 下方，使用下列設定：
    
      - **連線數目上限**  會指定將用來接受指定的伺服器的連線總數。這包括已驗證或未經過驗證的連線。預設值為 2147483647 個位元組。可能的值是介於 1 到 2147483647。
    
      - **從單一 IP 位址的連線數目上限**  會指定伺服器會接受來自單一 IP 位址的連線數目。預設值為 2147483647 個位元組。可能的值是介於 1 到 2147483647。
    
      - **從單一使用者連線數目上限**  指定伺服器會接受來自特定使用者的連線的數目上限。預設值為 16。可能的值是介於 1 到 2147483647。
    
      - **命令大小上限 （位元組）**會指定在單一命令的大小上限。預設大小為 512。可能的值是從 1024 到 40。

6.  按一下 \[套用\]，然後按一下 \[確定\] 以儲存變更。

設定連線限制之後，您必須重新啟動 \[POP3 服務。如需如何重新啟動 \[POP3 服務的資訊，請參閱[啟動及停止 \[POP3 服務](start-and-stop-the-pop3-services-exchange-2013-help.md)。

## 使用命令介面設定伺服器、IP 位址或使用者的 POP3 連線限制

此範例會設定伺服器的連線限制。

    Set-PopSettings -Identity CAS01 -MaxConnections Value

此範例會設定 IP 位址的連線限制。

    Set-PopSettings -Identity CAS01 -MaxConnectionsFromSingleIP Value

此範例會設定使用者的連線限制。

    Set-PopSettings -MaxConnectionsPerUser Value 

此範例會設定命令大小上限。

    Set-PopSettings -MaxCommandSize Value

設定連線限制之後，您必須重新啟動 \[POP3 服務。如需如何重新啟動 \[POP3 服務的資訊，請參閱[啟動及停止 \[POP3 服務](start-and-stop-the-pop3-services-exchange-2013-help.md)。

如需語法及參數的詳細資訊，請參閱 [Set-PopSettings](https://technet.microsoft.com/zh-tw/library/aa997154\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認是否已成功設定連線限制，請執行下列其中一項操作：

1.  在 EAC 中，瀏覽至 \[伺服器\]**\>** \[伺服器\]。

2.  在伺服器清單中選取 Client Access Server，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在伺服器內容頁面上，按一下 \[POP3\]。

4.  向下捲動並按一下 \[更多選項\]。

5.  在 \[連線限制\] 下方，驗證連線設定是否正確。

或

1.  在命令介面中執行下列命令。
    
        Get-PopSettings | format-list

2.  驗證連線設定是否正確。

## 相關資訊

設定伺服器、IP 位址或使用者的 POP3 連線限制之後，您可能還想要：

[在 Exchange 2013 中啟用 POP3](enable-pop3-in-exchange-2013-exchange-2013-help.md)

[設定的 POP3 連線逾時限制](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)


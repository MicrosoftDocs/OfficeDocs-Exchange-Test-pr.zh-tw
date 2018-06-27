---
title: '修改接收連接器上的 SMTP 橫幅: Exchange 2013 Help'
TOCTitle: 修改接收連接器上的 SMTP 橫幅
ms:assetid: d667704e-fd69-4aca-9c35-eef7006944b2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124740(v=EXCHG.150)
ms:contentKeyID: 52062592
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 修改接收連接器上的 SMTP 橫幅

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

「SMTP 橫幅」是遠端 SMTP 郵件伺服器在連線至 Microsoft Exchange Server 2013 電腦上所設定的接收連接器之後，所收到的 SMTP 連線回應。

這是遠端 SMTP 郵件伺服器在連線至接收連接器之後，所收到的預設回應。

    220 <Servername> Microsoft ESMTP MAIL service ready at <RegionalDay-Date-24HourTimeFormat> <RegionalTimeZoneOffset>

當您在接收連接器上指定自訂值作為 SMTP 橫幅時，連線至該 SMTP 接收連接器的遠端 SMTP 郵件伺服器會收到下列回應。

    220 <Banner Text>

您可能想要修改網際網路對向的 SMTP 接收連接器所用的 SMTP 橫幅，以免 SMTP 橫幅透露伺服器名稱及郵件伺服器軟體。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「接收連接器」項目。

  - 您只能使用命令介面來執行此程序。

  - 替代的 SMTP 橫幅字串必須一律以 `220` 開頭。如同 RFC 2821 中所定義，預設的服務就緒 SMTP 回應碼為 220。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用命令介面來修改接收連接器上的 SMTP 橫幅

執行下列命令：

    Set-ReceiveConnector <ConnectorIdentity> -Banner "220 <Banner Text>"

此範例會在名為 From the Internet 的現有接收連接器上修改 SMTP 橫幅，讓 SMTP 橫幅顯示 `220 Contoso Corporation`。

    Set-ReceiveConnector "From the Internet" -Banner "220 Contoso Corporation"

此範例會在名為 From the Internet 的現有接收連接器上移除自訂 SMTP 橫幅，讓 SMTP 橫幅回復成預設值。

    Set-ReceiveConnector "From the Internet" -Banner $null

## 如何知道這是否正常運作？

若要確認您已成功修改接收連接器上的 SMTP 橫幅，請執行下列動作：

1.  在可以存取該接收連接器的電腦上開啟 telnet 用戶端，並執行下列命令：
    
        open <Connector FQDN or IP address> <Port>

2.  確認接收連接器傳來的回應中包含您所設定的 SMTP 橫幅。

請注意，這項程序只適用於允許匿名或基本驗證的接收連接器。如需詳細資訊，請參閱 [使用 Telnet 測試 SMTP 通訊](use-telnet-to-test-smtp-communication-exchange-2013-help.md)。


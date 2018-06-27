---
title: '版本隔離的垃圾郵件隔離信箱的郵件: Exchange 2013 Help'
TOCTitle: 版本隔離的垃圾郵件隔離信箱的郵件
ms:assetid: 7a86bfde-f868-4689-bdec-5f01e52b510d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998920(v=EXCHG.150)
ms:contentKeyID: 50473567
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 版本隔離的垃圾郵件隔離信箱的郵件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

您可以使用 Microsoft Outlook 從垃圾郵件隔離信箱復原隔離郵件。

垃圾郵件隔離區是可以降低風險遺失合法的郵件內容篩選器代理程式的功能。當郵件符合垃圾郵件隔離區臨界值時，它有換行的未傳遞回報 (NDR) 中並傳遞至垃圾郵件隔離信箱。如需垃圾郵件隔離功能的詳細資訊，請參閱[垃圾郵件隔離](spam-quarantine-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「信箱存取」項目。

  - 此程序會要求您先設定反垃圾郵件隔離信箱。如需詳細資訊，請參閱[設定垃圾郵件隔離信箱](configure-a-spam-quarantine-mailbox-exchange-2013-help.md)。

  - 若要存取隔離信箱，您需要設定該信箱的 Outlook 設定檔及再開啟 \[使用 Outlook 信箱。如需設定和使用多個 Outlook 設定檔的詳細資訊，請參閱[概觀 （英文) 的 Outlook 電子郵件設定檔](https://go.microsoft.com/fwlink/p/?linkid=178975)。

  - 如果要讓更容易找到您想要復原的郵件，您可以建立自訂 Outlook 表單和修改公開的郵件清單中的原始寄件者地址的預設檢視。如需詳細步驟，請參閱[將 Outlook 設定為顯示隔離信箱中的原始寄件者](configure-outlook-to-show-the-original-sender-in-the-quarantine-mailbox-exchange-2013-help.md)。

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


## 您要執行的工作

## 使用 Outlook 2010 或 Outlook 2013 從垃圾郵件隔離信箱中釋放郵件

1.  在用戶端電腦上使用 Outlook 2010 或 Outlook 2013 來開啟隔離信箱。

2.  在 \[郵件\] 檢視中，在 \[收件匣\] 中找出您想要復原的郵件，接著在該郵件上按兩下將其開啟。

3.  在功能區的 \[移動\] 區段中，按一下 \[行動\] \> \[重新寄出此郵件\]。

4.  郵件開啟時，按一下 \[傳送\]，將郵件重新傳送給目標收件者。

## 使用 Outlook 2007 釋放垃圾郵件隔離信箱的郵件

1.  在用戶端電腦上使用 Outlook 2007 來開啟隔離信箱。

2.  在 \[郵件資料夾\] 檢視中，在 \[收件匣\] 中找出您想要復原的郵件，接著在該郵件上按兩下將其開啟。

3.  在 \[報告\] 索引標籤的 \[回應\] 群組中，按一下 \[再寄一次\]。

4.  郵件開啟時，按一下 \[傳送\]，將郵件重新傳送給目標收件者。

## 如何才能了解這是否正常運作？

若要驗證您已成功從垃圾郵件隔離信箱中釋放出郵件，請聯絡收件者並確認他們是否收到郵件。


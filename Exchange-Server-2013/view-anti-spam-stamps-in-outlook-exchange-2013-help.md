---
title: '在 Outlook 中檢視反垃圾郵件戳記: Exchange 2013 Help'
TOCTitle: 在 Outlook 中檢視反垃圾郵件戳記
ms:assetid: cddb5dbf-ad1e-471c-9fc8-28ddcf7ec1d0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124595(v=EXCHG.150)
ms:contentKeyID: 50474244
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Outlook 中檢視反垃圾郵件戳記

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

您可以使用 Microsoft Outlook 檢視 Microsoft Exchange 套用至電子郵件訊息的反垃圾郵件戳記。反垃圾郵件戳記協助您套用診斷的中繼資料、 或戳記，例如特定寄件者的資訊、 拼圖驗證結果，以及內容篩選結果的郵件通過訊息的反垃圾郵件代理程式診斷垃圾郵件相關的問題可篩選來自網際網路的內送的郵件。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「信箱存取」項目。

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

## 使用 Outlook 2010 或 Outlook 2013 檢視反垃圾郵件戳記

1.  在用戶端電腦上的 Outlook 2010 或 Outlook 2013 中，在 \[郵件\] 檢視下，連按兩下郵件以開啟郵件。

2.  在功能區的 \[標籤\] 區段中，按一下 \[選項\] 圖示，顯示郵件 \[內容\] 對話方塊。

3.  在 \[內容\] 對話方塊的 \[網際網路標頭\] 區段中，使用捲軸檢視如下例所示的反垃圾郵件戳記。
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures

## 使用 Outlook 2007 檢視反垃圾郵件戳記

1.  在用戶端電腦上的 Outlook 2007 中，在 \[郵件\] 檢視下，連按兩下郵件以開啟郵件。

2.  在 \[郵件\] 索引標籤上，按一下 \[選項\] 群組中的 \[郵件選項\]。

3.  在 \[郵件選項\] 對話方塊的 \[網際網路標頭\] 區段中，使用捲軸檢視如下例所示的反垃圾郵件戳記。
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures


---
title: '設定 Exchange 組織中公認的網域成為授權: Exchange 2013 Help'
TOCTitle: 設定 Exchange 組織中公認的網域成為授權
ms:assetid: e182d54f-e58a-47ba-a5c1-28c0dfa86eed
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657734(v=EXCHG.150)
ms:contentKeyID: 50474458
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Exchange 組織中公認的網域成為授權

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-02-17_

如果屬於您組織的網率主控 SMTP 命名空間所有收件者的信箱，該網域便屬於授權網域。根據預設，一個公認的網域將被設定為 Exchange 組織的授權網域。如果您的組織有多個 SMTP 命名空間，可以設定多個公認的網域成為授權網域。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱主題中的「公認的網域」[郵件流程權限](mail-flow-permissions-exchange-2013-help.md)項目。

  - 如果您的周邊網路中有訂閱的 Edge Transport Server，則可在 Exchange 組織的 Mailbox Server 上設定公認網域。公認網域組態會在 EdgeSync 同步處理期間複寫至 Edge Transport Server。如需詳細資訊，請參閱[Edge 訂閱](edge-subscriptions-exchange-2013-help.md)。

  - 您無法建立與已設定的遠端網域具有相同名稱的公認的網域。例如，若您將 fabrikam.com 設定為遠端伺服器，就無法為 fabrikam.com 建立公認的網域。

  - 設定公認的網域之後，必須驗證該 SMTP 命名空間有公用網域名稱系統 (DNS) MX 資源記錄存在，且 MX 資源記錄參照與 Exchange 組織關聯的伺服器名稱及 IP 位址。

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


## 使用 EAC 設定公認的網域成為授權網域

如果您 Exchange 組織公認的網域主控該網域 SMTP 命名空間內的收件者所有的信箱，您可能會想要將它設定為授權網域。

1.  在 EAC 中，瀏覽至 \[郵件流程\] \> \[公認的網域\]，並且按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[姓名\] 欄位中輸入公認的網域之顯示名稱。您組織的各個公認網域必須有唯一的顯示名稱。此名稱可能與公認網域不同。例如，網域 contoso.com 的顯示名稱可以是 Contoso Local Accepted Domain。

3.  在 \[公認的網域\] 欄位中，輸入公認的網域。指定您的組織接受電子郵件的 SMTP 命名空間。(例如，Contoso.com)。

4.  選取 \[授權網域\]。這個選項用於轉送到公認的網域中 Exchange 組織伺服器的電子郵件，這個公認的網域主控 SMTP 命名空間內所有收件者的信箱。

5.  按一下 \[儲存\]。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要設定已經建立的公認網域，請從公認的網域清單中選取網域，並且按一下 [編輯]<img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編輯圖示" alt="編輯圖示" />。您可以設定多個網域成為授權網域。</td>
</tr>
</tbody>
</table>


## 如何知道這是否正常運作？

您新的公認網域將出現在 EAC 中公認的網域清單。若要確認您是否成功設定公認的網域成為授權網域，請將郵件傳送到該網域，並確認收到該郵件。


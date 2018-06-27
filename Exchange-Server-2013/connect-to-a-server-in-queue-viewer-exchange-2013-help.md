---
title: '佇列檢視器中的伺服器連線: Exchange 2013 Help'
TOCTitle: 佇列檢視器中的伺服器連線
ms:assetid: 6c1ad574-9ab5-4dcc-9398-ec10eca4fd11
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998669(v=EXCHG.150)
ms:contentKeyID: 50473404
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 佇列檢視器中的伺服器連線

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

當您使用佇列檢視器位於內部部署 Exchange 組織的 Microsoft Exchange Server 2013伺服器上的 \[Exchange 工具箱\] 中時，您可以連線至其他 Mailbox server。根據預設，當您開啟 Mailbox server 上的佇列檢視佇列檢視器連接至本機伺服器上的佇列資料庫。 不過，您可以啟動一個以上的執行個體的佇列檢視器，讓每個執行個體著重在不同的伺服器。讓您輕鬆可以監視多個信箱伺服器每次您也可以並排顯示佇列檢視器視窗。

您也可以指定之伺服器的遠端 PowerShell 使用佇列檢視器中執行指定的工作。此伺服器不需要以符合您正在管理佇列檢視器中的遠端伺服器。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「佇列」項目。

  - 本主題中的程序不套用至 Edge Transport server。當您在 Edge Transport server 上使用佇列檢視器時，就無法變更此工具的駐點。

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

## 使用 Exchange 工具箱指定想在佇列檢視器中管理的伺服器

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange Server 2013\] \> \[Exchange 工具箱\]。

2.  在 \[郵件流程工具\] 區段中，按兩下 \[佇列檢視器\]。

3.  在執行窗格中，按一下 \[連接到伺服器\]。

4.  在 \[連接至伺服器\] 視窗中按一下 \[瀏覽\]，檢視可用的信箱伺服器清單。

5.  在 \[**選取 Exchange Server** \] 視窗中，選取信箱伺服器。若要搜尋的信箱伺服器，使用下列程序之一：
    
      - 在 \[**搜尋**\] 欄位中輸入伺服器名稱的第幾個字母或實際的伺服器名稱\] 和 \[便會**立即尋找\]**。從 \[結果\] 窗格中選取的伺服器。
    
      - 選取 \[**檢視**\] 功能表，然後按一下 \[**顯示篩選**。在 \[**名稱**\] 欄中或 \[**版本**\] 欄中，按一下 \[篩選器\] 圖示，然後選取的篩選器運算子。在**這裡輸入文字**\] 欄位中輸入篩選準則。按 ENTER 鍵。從 \[結果\] 窗格中選取的伺服器。

6.  按一下 \[確定\] 關閉 \[選取 Exchange Server\] 視窗。

7.  在選取伺服器之後，如果您希望每當開啟佇列檢視器時，佇列檢視器會先將焦點放在此伺服器，則請在 \[連接到伺服器\] 視窗中選取 \[設定為預設伺服器\] 核取方塊。

8.  在 \[連接到伺服器\] 視窗中按一下 \[連線\]。

## 使用 Exchange 工具箱指定佇列檢視器在執行遠端 PowerShell 時要使用伺服器

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange Server 2013\] \> \[Exchange 工具箱\]。

2.  在 \[郵件流程工具\] 區段中，按兩下 \[佇列檢視器\]。

3.  在執行窗格中，按一下 \[內容\]。

4.  在 \[佇列檢視器 - \<伺服器名稱\> 內容\] 對話方塊中，選取下列其中一個選項：
    
      - **連線到自動選取的伺服器**   選取此選項可以自動連接到您管理佇列用於執行遠端 PowerShell 的伺服器。
    
      - **指定連線至伺服器**  選取此選項可指定執行遠端 PowerShell 伺服器。如果您選取此選項時，按一下 \[**瀏覽\]**以開啟 \[**選取 Exchange Server** \] 對話方塊。選取您要執行遠端 PowerShell 中的伺服器並再按一下 \[**確定\]**。

## 如何才能了解這是否正常運作？

您應該能夠管理所指定信箱伺服器上的佇列。


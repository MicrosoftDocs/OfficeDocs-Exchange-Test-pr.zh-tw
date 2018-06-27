---
title: '針對資料庫可用性群組預先接移叢集名稱物件: Exchange 2013 Help'
TOCTitle: 針對資料庫可用性群組預先接移叢集名稱物件
ms:assetid: 51ebf2f6-8a02-44ef-a489-ca361cb0f63a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff367878(v=EXCHG.150)
ms:contentKeyID: 50473216
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 針對資料庫可用性群組預先接移叢集名稱物件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-08-14_

在環境中所在的電腦帳戶建立僅限於或非預設的電腦容器、 容器中建立電腦帳戶的其中您可以預先接叢集名稱物件 (CNO)，然後佈建 CNO 的權限指派給它。預先接移 CNO 也是必要的 Windows Server 2012 及 Windows Server 2012 R2 DAG 成員因為 Windows 的電腦物件的權限變更。部署時使用執行 Windows Server 2012 的信箱伺服器或 Windows Server 2012 R2 資料庫可用性群組 (DAG)，您必須預先設置及佈建 CNO，除非您要部署沒有叢集管理存取點之 DAG。沒有叢集管理存取點的 Dag 不使用 CNOs;因此預先接移不需要的那些 Dag。

您可以為 CNO 建立和停用電腦帳戶，然後執行下列其中一項動作：

  - 指派電腦帳戶的完全控制權給您新增至 DAG 的第一個信箱伺服器的電腦帳戶。

  - 指派電腦帳戶的完全控制權給 Exchange 受信任子系統萬用安全性群組 (USG)。

## 開始之前有哪些須知？

  - 預估完成時間：1 分鐘

  - 您必須使用擁有於 Active Directory 中建立電腦物件權限的帳號。

  - 完成下列步驟之後，允許進行 Active Directory 複寫。複寫物件之後，可以將第一個成員新增至 DAG。

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

## 預先接移 CNO

1.  開啟 \[Active Directory 使用者和電腦\]。

2.  展開樹系節點。

3.  在您要建立新帳戶的組織單位 (OU) 上按一下滑鼠右鍵，選取 \[新增\]，然後選取 \[電腦\]。

4.  在 \[新物件 - 電腦\] 中，於 \[電腦名稱\] 方塊內輸入 CNO 的電腦帳戶名稱。此名稱將用於 DAG。按一下 \[確定\] 以建立帳戶。

5.  在新電腦帳戶上按一下滑鼠右鍵，然後按一下 \[停用帳戶\]。按一下 \[是\] 以確認停用動作，然後按一下 \[確定\]。

## 指派權限給 CNO

1.  開啟 \[Active Directory 使用者和電腦\]。

2.  如果未啟用 \[進階功能\]，可按一下 \[檢視\]，然後按一下 \[進階功能\] 將其開啟。

3.  在新電腦帳戶上按一下滑鼠右鍵，然後按一下 \[內容\]。

4.  在 \[\<電腦名稱\> 內容\] 的 \[安全性\] 索引標籤上按一下 \[新增\]，新增要新增至 DAG 的第一個節點的電腦帳戶，或者新增 Exchange 受信任子系統 USG：
    
      - 若要新增 Exchange 受信任子系統，請在 \[輸入物件名稱來選取\] 欄位中輸入 **Exchange Trusted Subsystem**。按一下 \[確定\] 以新增 USG。選取 \[Exchange 受信任子系統 USG\]，並在 \[Exchange 受信任子系統的權限\] 欄位中，在 \[允許\] 欄選取 \[完全控制\]。按一下 \[確定\] 以儲存權限設定。
    
      - 若要新增要新增至 DAG 之第一個節點的電腦帳戶，請按一下 \[物件類型\]。清除 \[物件類型\] 對話方塊中的 \[內建安全性原則\]、\[群組\] 和 \[使用者\] 核取方塊。選取 \[電腦\] 核取方塊，然後按一下 \[確定\]。在 \[輸入物件名稱來選取\] 欄位中，輸入要新增至 DAG 的第一個信箱伺服器名稱，然後按一下 \[確定\]。選取第一個節點的電腦帳戶，並在 \[\<節點名稱\> 的權限\] 欄位中，在 \[允許\] 欄選取 \[完全控制\]。按一下 \[確定\] 以儲存權限設定。

## 如何才能了解這是否正常運作？

若要驗證您是否已成功建立 CNO，執行下列操作：

1.  開啟 \[Active Directory 使用者和電腦\]。

2.  展開樹系節點。

3.  開啟在其中建立帳號的 OU，然後驗證該帳戶是否列出。


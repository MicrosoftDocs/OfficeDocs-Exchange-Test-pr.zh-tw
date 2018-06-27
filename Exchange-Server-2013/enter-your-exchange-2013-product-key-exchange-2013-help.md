---
title: '輸入您的 Exchange 2013 產品金鑰: Exchange 2013 Help'
TOCTitle: 輸入您的 Exchange 2013 產品金鑰
ms:assetid: ccb14685-4bdc-42a4-a985-35cd2a1a415c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124582(v=EXCHG.150)
ms:contentKeyID: 51409244
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.EnterProductKeyWizardForm.EnterProductKeyWizardPage
ms.translationtype: MT
---

# 輸入您的 Exchange 2013 產品金鑰

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

產品金鑰會告知Exchange Server 2013您已購買 Standard 或 Enterprise Edition 授權。如果您所購買的產品金鑰未 Enterprise Edition 授權，它可讓您針對每部伺服器以及每個項目所適用的標準版授權的五個以上資料庫裝載。如果您想要閱讀更多 Exchange 授權，請參閱[Exchange 2013：版本](exchange-2013-editions-and-versions-exchange-2013-help.md)。

如果您沒有輸入產品金鑰，您的伺服器的自動授權為試用版。試用版的功能只 like Exchange Standard Edition server，如果您要購買之前, 試用Exchange還是執行測試實驗室中有所幫助。唯一的不同是您可以僅使用 180 天的授權為試用版Exchange伺服器。如果您想要繼續使用超過 180 天的伺服器，您需要輸入產品金鑰或 Exchange 系統管理中心 (EAC) 會在啟動顯示您需要輸入產品金鑰來授權伺服器的提醒。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我們發現此頁面的一些訪客都在尋找如何安裝或啟動 Office 的相關資訊。如果您也是，請查看這些頁面：
<ul>
<li><p><a href="http://go.microsoft.com/fwlink/p/?linkid=403360">安裝 Office</a></p></li>
<li><p><a href="http://go.microsoft.com/fwlink/p/?linkid=403361">需要 Office 產品金鑰方面的協助嗎？</a></p></li>
</ul>
如果您要在 Exchange 2010 伺服器上輸入產品金鑰，請移至＜<a href="http://go.microsoft.com/fwlink/p/?linkid=403370">輸入 Exchange 2010 產品金鑰</a>＞。<br />
如果您要在 Exchange 2013 伺服器上輸入產品金鑰，這裡就是正確的地方！請繼續閱讀。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 此程序預估完成時間：少於 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的「產品金鑰」 項目。

  - 如果是對執行 Mailbox server role 的 Exchange 伺服器進行授權，則在輸入產品金鑰之後，必須在伺服器上重新啟動 Microsoft Exchange Information Store 服務。

  - 如果要將 Exchange 伺服器從 Standard Edition 授權升級到 Enterprise Edition 授權，請遵循本主題的步驟。

  - 如果要將 Exchange 伺服器從 Enterprise Edition 授權降級到 Standard Edition 授權，您需要重新安裝 Exchange。

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

## 使用 EAC 輸入產品金鑰

1.  瀏覽到 https://\<*Client Access server 名稱*\>/ecp 來開啟 EAC。

2.  在 **\[網域\\使用者名稱\]** 和 **\[密碼\]** 中輸入您的使用者名稱和密碼，然後按一下 **\[登入\]**。

3.  前往 **\[伺服器\]** \> **\[伺服器\]**。選取要授權的伺服器，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  (選用) 如果您要將伺服器從 Standard Edition 授權升級為 Enterprise Edition 授權，請在 **\[一般\]** 頁面上選取 **\[變更產品金鑰\]**。只有當伺服器已授權之後，才會出現此選項。

5.  在 **\[一般\]** 頁面的 **\[輸入有效的產品金鑰\]** 文字方塊中，輸入您的產品金鑰。

6.  按一下 **\[儲存\]**。

7.  如果您授權的 Exchange 伺服器是執行 Mailbox server role，請執行下列動作來重新啟動 Microsoft Exchange Information Store 服務：
    
    1.  開啟 **\[控制台\]**，移至 **\[系統管理工具\]**，然後開啟 **\[服務\]**。
    
    2.  在 **Microsoft Exchange Information Store** 上按一下滑鼠右鍵，然後按一下 **\[重新啟動\]**。

## 使用命令介面輸入產品金鑰

此範例使用 **set-ExchangeServer** 指令程式來輸入產品金鑰。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以在相同的伺服器上再執行一次此命令，以將該伺服器從 Standard Edition 授權升級至 Enterprise Edition 授權。</td>
</tr>
</tbody>
</table>


    Set-ExchangeServer ExServer01 -ProductKey aaaaa-aaaaa-aaaaa-aaaaa-aaaaa

如需詳細的語法及參數資訊，請參閱 [Set-ExchangeServer](https://technet.microsoft.com/zh-tw/library/bb123716\(v=exchg.150\))。

如果您授權的 Exchange 伺服器是執行 Mailbox server role，請執行下列動作來重新啟動 Microsoft Exchange Information Store 服務：

1.  開啟 **\[控制台\]**，移至 **\[系統管理工具\]**，然後開啟 **\[服務\]**。

2.  **Microsoft Exchange Information Store**上按一下滑鼠右鍵並按一下 \[**重新啟動**。

## 如何才能了解這是否正常運作？

若要使用 EAC 確認您已成功將伺服器授權為 Standard Edition 或 Enterprise Edition，請執行下列作業：

1.  在 **\[網域\\使用者名稱\]** 和 **\[密碼\]** 中輸入您的使用者名稱和密碼，然後按一下 **\[登入\]**。

2.  前往 **\[伺服器\]** \> **\[伺服器\]**。

3.  選取您要檢視的伺服器，然後查詢伺服器詳細資料窗格。如果產品金鑰已被接受，**\[已授權\]** 會出現在 Exchange 2013 版本旁。

若要使用命令介面確認您已成功將伺服器授權為 Standard Edition 或 Enterprise Edition，請執行下列作業：

1.  開啟命令介面。

2.  執行下列命令，以檢視特定 Exchange 伺服器的授權狀態。
    
        Get-ExchangeServer ExServer01 | Format-Table Edition,*Trial*

3.  (選用) 執行下列命令，以檢視您組織中所有 Exchange 伺服器的授權狀態。
    
        Get-ExchangeServer | Format-Table Name, Edition, *Trial* -Auto


---
title: '設定脫離的命名空間的 DNS 尾碼搜尋清單: Exchange 2013 Help'
TOCTitle: 設定脫離的命名空間的 DNS 尾碼搜尋清單
ms:assetid: cfa715ac-7b69-47c3-b206-933ec2cf677b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb847901(v=EXCHG.150)
ms:contentKeyID: 50474249
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定脫離的命名空間的 DNS 尾碼搜尋清單

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

本主題說明如何使用群組原則管理主控台 (GPMC) 來設定網域名稱系統 (DNS) 尾碼搜尋清單。在某些 Microsoft Exchange 2013情況下，如果您具有脫離的命名空間，您必須設定 DNS 尾碼搜尋清單包含多個 DNS 尾碼。

## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘

  - 若要執行此程序，必須對您使用的帳戶委派 Domain Admins 群組的成員資格。

  - 確認您已經在將安裝 GPMC 的電腦上安裝 .NET Framework 3.0。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以從 Microsoft 下載中心下載 GPMC 的目前版本都會Windows Server 2003和Windows XP作業系統的 32 位元版本並可以從遠端管理 32 位元和 64 位元的網域控制站上的群組原則物件。GPMC 此版不包含在 64 位元版本，與 32 位元版本不能在 64 位元平台上執行。Windows Server 2008的 32 位元版本與 32 位元版本的Windows Vista這兩個包含 「 GPMC 的 32 位元版本。Windows Server 2008 64 位元版本與 64 位元版本的Windows Vista這兩個包含 「 GPMC 64 位元版本。</td>
    </tr>
    </tbody>
    </table>


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


## 使用 GPMC 設定 DNS 尾碼搜尋清單

1.  您網域中 32 位元電腦上安裝 GPMC 含 Service Pack 1 (SP1)。如下載資訊，請參閱 ＜[群組原則管理主控台 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=100126)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您的網域中有電腦執行 Windows Server 2008 或 Windows Vista，則可以略過此步驟。</td>
    </tr>
    </tbody>
    </table>


2.  按一下 \[開始\] \> \[程式集\] \> \[系統管理工具\] \> \[群組原則管理\]。

3.  在 \[群組原則管理\] 中，展開要在其中套用群組原則的樹系及網域。在 \[群組原則物件\] 上按一下滑鼠右鍵，然後按一下 \[新增\]。

4.  在 \[新增 GPO\] 中輸入原則的名稱，然後按一下 \[確定\]。

5.  在您於步驟 4 建立的新原則上按一下滑鼠右鍵，然後按一下 \[編輯\]。

6.  在 \[群組原則管理編輯器\] 中，依序展開 \[電腦組態\]、**\[原則\]、**\[系統管理範本\] 及 \[網路\]，然後按一下 \[DNS 用戶端\]。

7.  在 \[DNS 尾碼搜尋清單\] 上按一下滑鼠右鍵，然後依序按一下 \[全部工作\]、**\[編輯\]**。

8.  在 \[DNS 尾碼搜尋清單內容\] 頁面上，選取 \[啟用\]。在 \[DNS 尾碼\] 方塊中輸入脫離電腦的主要 DNS 尾碼、DNS 網域名稱，以及其他可以與 Exchange 交互操作之伺服器的任何額外命名空間 (如監視伺服器或協力廠商應用程式的伺服器)。按一下 \[確定\]。

9.  在 \[群組原則管理\] 中，展開 \[群組原則物件\]，然後選取您在步驟 4 建立的原則。在 \[範圍\] 索引標籤上，設定原則範圍，讓它只套用至脫離的電腦。

## 如何才能了解這是否正常運作？

若要驗證您是否已成功完成遷移，執行下列操作：

  - 安裝 Exchange 2013 之後，確認您可以將電子郵件傳送到組織內外。

## 相關資訊

[Windows Server 群組原則](https://go.microsoft.com/fwlink/p/?linkid=100128)

[群組原則](https://go.microsoft.com/fwlink/?linkid=268043)

[斷續的命名空間案例](disjoint-namespace-scenarios-exchange-2013-help.md)


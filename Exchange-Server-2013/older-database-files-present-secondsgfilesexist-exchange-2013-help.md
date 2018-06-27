---
title: '較舊的資料庫檔案 present_SecondSGFilesExist: Exchange 2013 Help'
TOCTitle: 較舊的資料庫檔案 present_SecondSGFilesExist
ms:assetid: fe2908e7-df8b-4f35-946a-cfbf8521e93a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.secondsgfilesexist(v=EXCHG.150)
ms:contentKeyID: 50474685
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 較舊的資料庫檔案 present\_SecondSGFilesExist

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式無法繼續因為它的目標安裝路徑中偵測到現有的 Microsoft Exchange 資料庫檔案。

Exchange 2007 的安裝程式需要目標安裝路徑是空的 Microsoft Exchange 資料庫檔案。

若要解決此問題，移除所有現有的檔案從目標的安裝路徑，然後重新執行安裝程式。

若要刪除現有的 Exchange Server 資料庫檔案從目標的安裝路徑

1.  在 「 我的電腦或 Windows 檔案總管中，找出目標的安裝路徑。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>根據預設，資料庫檔案位於：<br />
    &lt; 系統磁碟 &gt;: \Program Files\Microsoft\Exchange Server\Mailbox\First 儲存群組。</td>
    </tr>
    </tbody>
    </table>


2.  以滑鼠右鍵按一下要移除的檔案，然後選取 \[**刪除**。

3.  在 \[**確認刪除檔案**\] 對話方塊中，按一下 \[**是**\]。

4.  在目標安裝路徑中的所有檔案重複步驟 2 和 3。


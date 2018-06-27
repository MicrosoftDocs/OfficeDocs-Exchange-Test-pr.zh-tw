---
title: '協助識別 「 我的自動檢查-目錄同步作業問題: Exchange 2013 Help'
TOCTitle: 協助識別 「 我的自動檢查-目錄同步作業問題
ms:assetid: e6ea900a-c382-444c-a8ce-54d392bfeca3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn793977(v=EXCHG.150)
ms:contentKeyID: 62633022
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 協助識別 「 我的自動檢查-目錄同步作業問題

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

您可以使用以下的自動檢查來驗證您的設定和更新您的環境的說明。

如果您已經有 Office 365 使用者帳戶，請選取 \[登入\]。您不需要 Azure ID 帳戶。您可能會要求使用者帳戶一次執行檢查。若是如此，您的使用者帳戶是在 username@youroffice365login.domain 和您的密碼的格式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您在 Office 365 入口網站中的同步作業伺服器事件記錄檔] 或 [不健康的目錄同步作業電子郵件通知從 Microsoft Online Services 錯誤收到 sync 警告訊息，您可能需要某種類型的目錄同步作業問題。<a href="https://aka.ms/dsup">目錄同步處理的疑難排解員</a>是 Web 式診斷工具的設計用來協助識別的同步處理失敗的一般類型及擬定目標的解決方案移轉至任何發現的問題。目錄同步處理的疑難排解員必須 DirSync 伺服器上執行。</td>
</tr>
</tbody>
</table>


## 必要條件

我們將檢查看看是否有Azure Active Directory 登入小幫手和Windows PowerShell 的 Azure Active Directory 模組安裝。

Azure Active Directory 登入小幫手有兩種版本： [32 位元](https://go.microsoft.com/fwlink/?linkid=286261)與[64 位元](https://go.microsoft.com/fwlink/?linkid=286262)。

Windows PowerShell 的 Azure Active Directory 模組有兩種版本： [32 位元](https://go.microsoft.com/fwlink/?linkid=286258)與[64 位元](https://go.microsoft.com/fwlink/?linkid=286259)。

## 目錄同步作業檢查


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>應用程式</p></td>
<td><p>問題</p></td>
<td><p>勾選</p></td>
</tr>
<tr class="even">
<td><p>目錄同步處理</p></td>
<td><p>我已經不確定 「 我的 Active Directory 使用者帳戶的所有符合目錄同步處理的需求。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834884">執行這項檢查</a></p></td>
</tr>
<tr class="odd">
<td><p>目錄同步處理</p></td>
<td><p>我已經不確定 「 我的 Active Directory 網域功能等級正確設定 Windows Server 2003 或上方。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">執行這項檢查</a></p></td>
</tr>
<tr class="even">
<td><p>目錄同步處理</p></td>
<td><p>我已經不確定目錄同步作業中前三個小時發生。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">執行這項檢查</a></p></td>
</tr>
<tr class="odd">
<td><p>目錄同步處理</p></td>
<td><p>我已經不確定 「 我的 Active Directory 發生即會封鎖目錄同步處理任何重複的使用者屬性。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834883">執行這項檢查</a></p></td>
</tr>
<tr class="even">
<td><p>目錄同步處理</p></td>
<td><p>我已經不確定 Office 365 中啟用目錄同步作業。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">執行這項檢查</a></p></td>
</tr>
<tr class="odd">
<td><p>目錄同步處理</p></td>
<td><p>我已經不確定如果我可以在部署 Office 365 報價限制。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834920">執行這項檢查</a></p></td>
</tr>
<tr class="even">
<td><p>目錄同步處理</p></td>
<td><p>我已經不確定我可以部署 Office 365，並使用預設目錄同步處理設定。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">執行這項檢查</a></p></td>
</tr>
<tr class="odd">
<td><p>目錄同步處理</p></td>
<td><p>我已經不確定如果我使用 Active Directory 並可支援目錄同步處理。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834886">執行這項檢查</a></p></td>
</tr>
<tr class="even">
<td><p>目錄同步處理</p></td>
<td><p>我已經不確定 「 我的 Active Directory 群組的所有符合目錄同步處理的需求。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834913">執行這項檢查</a></p></td>
</tr>
</tbody>
</table>


---
title: 'Azure： 協助識別 「 我的問題與自動檢查層 DNS 記錄: Exchange 2013 Help'
TOCTitle: Azure： 協助識別 「 我的問題與自動檢查層 DNS 記錄
ms:assetid: 1ef42cde-4df4-401a-b8f2-494630996ca8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn793619(v=EXCHG.150)
ms:contentKeyID: 62629981
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Azure： 協助識別 「 我的問題與自動檢查層 DNS 記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

其中一個最常見的組態設定問題不正確地設定 DNS 記錄。您可以使用來驗證您的設定和說明更新您的環境下面所列的自動檢查。

如果您已經有 Office 365 使用者帳戶，請選取 \[登入\]。您不需要 Azure ID 帳戶。您可能會要求使用者帳戶一次執行檢查。若是如此，您的使用者帳戶是在 username@youroffice365login.domain 和您的密碼的格式。

## 必要條件

我們將檢查看看是否有Azure Active Directory 登入小幫手和Windows PowerShell 的 Azure Active Directory 模組安裝。

Azure Active Directory 登入小幫手有兩種版本： [32 位元](https://go.microsoft.com/fwlink/?linkid=286261)和[64 位元](https://go.microsoft.com/fwlink/?linkid=286262)。

Windows PowerShell 的 Azure Active Directory 模組有兩種版本： [32 位元](https://go.microsoft.com/fwlink/?linkid=286258)與[64 位元](https://go.microsoft.com/fwlink/?linkid=286259)。

## DNS 記錄檢查


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
<td><p>網域</p></td>
<td><p>我自訂的網域 (例如 contoso.com) 看似未設定 Office 365 的</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">執行這項檢查</a></p></td>
</tr>
<tr class="odd">
<td><p>網域</p></td>
<td><p>我自訂的網域 (例如 contoso.com) 看似未設定與 Office 365 （我使用 CNAME 記錄）</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">執行這項檢查</a></p></td>
</tr>
<tr class="even">
<td><p>網域</p></td>
<td><p>我自訂的網域 (例如 contoso.com) 看似未設定與 Office 365 （I 使用 TXT 記錄）</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">執行這項檢查</a></p></td>
</tr>
<tr class="odd">
<td><p>立即訊息</p></td>
<td><p>我的使用者時發生問題嗎運作其 Lync 用戶端</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834901">執行這項檢查</a></p></td>
</tr>
<tr class="even">
<td><p>立即訊息</p></td>
<td><p>我的使用者時發生問題嗎他們能夠與其他組織的 Lync 用戶端</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834902">執行這項檢查</a></p></td>
</tr>
<tr class="odd">
<td><p>郵件</p></td>
<td><p>無法取得 Outlook 自動設定 Office 365 的</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834897">執行這項檢查</a></p></td>
</tr>
<tr class="even">
<td><p>郵件</p></td>
<td><p>我的電子郵件看似要路由傳送至 Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834898">執行這項檢查</a></p></td>
</tr>
<tr class="odd">
<td><p>郵件</p></td>
<td><p>我的組織會取得許多垃圾郵件</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834903">執行這項檢查</a></p></td>
</tr>
<tr class="even">
<td><p>郵件</p></td>
<td><p>我似乎無法取得 Exchange 混合式工作</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834904">執行這項檢查</a></p></td>
</tr>
</tbody>
</table>


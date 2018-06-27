---
title: '語音郵件使用者鎖定之前設定登入失敗的次數: Exchange Online Help'
TOCTitle: 語音郵件使用者鎖定之前設定登入失敗的次數
ms:assetid: 855e1980-2868-4983-b097-0b5f63f202b8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123544(v=EXCHG.150)
ms:contentKeyID: 50554022
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 語音郵件使用者鎖定之前設定登入失敗的次數

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以設定允許Outlook語音存取使用者就會鎖定不在其信箱的登入失敗的次數。語音郵件使用者鎖定之前允許的登入失敗的次數設定整合通訊 (UM) 信箱原則\]，並套用至所有已啟用 UM 之使用者的 UM 信箱原則相關聯。根據預設它是設為 15。

若要增加安全性，減少失敗的次數上限。但是請記住是否您減少更加低於預設值為數，使用者可能會鎖定整天。整合的通訊會產生警告事件您可以檢視已啟用 UM 之使用者的 PIN 驗證失敗時或失敗時的使用者會嘗試登入系統時使用事件檢視器。此設定必須大於登入失敗的次數的設定才會重設 PIN。

如需了解與 Outlook 語音存取 PIN 碼安全性相關的其他工作，請參閱 [PIN 安全性程序](pin-security-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

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

## 使用 EAC 配置鎖定語音郵件使用者之前的登入失敗數

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面中的 \[UM 信箱原則\] 之下，選取您要變更的 UM 信箱原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  按一下 \[PIN 規則\]，然後在 \[鎖定前的登入失敗數\] 旁邊，輸入 1 至 999 之間的數值。

5.  按一下 \[儲存\]。

## 使用命令介面配置鎖定語音郵件使用者之前的登入失敗數

此範例為與 UM 信箱規則 `MyUMMailboxPolicy` 相關的啟用 UM 使用者設定登入嘗試最大數為 10。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MaxLogonAttempts 10

此範例將重設 Outlook 語音存取使用者 PIN 之前的登入失敗數為 3，登入嘗試最大數為 5，與 UM 信箱規則 `MyUMMailboxPolicy` 相關的啟用 UM 使用者的最少 PIN 長度為 9。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9


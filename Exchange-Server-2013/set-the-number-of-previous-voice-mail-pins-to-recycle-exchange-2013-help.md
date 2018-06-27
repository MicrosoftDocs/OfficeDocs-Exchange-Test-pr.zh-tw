---
title: '設定舊版的語音信箱 Pin 回收的數目: Exchange Online Help'
TOCTitle: 設定舊版的語音信箱 Pin 回收的數目
ms:assetid: b094e68e-c493-4576-a6b1-4c780e635405
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124254(v=EXCHG.150)
ms:contentKeyID: 50554082
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定舊版的語音信箱 Pin 回收的數目

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

當Outlook語音存取使用者撥入 Outlook 語音存取號碼時，系統會提示他們輸入其 PIN 以便語音郵件系統可以進行驗證。他們通過驗證之後，他們可以從任何電話存取語音信箱、 電子郵件、 行事曆，並在他們的信箱中的個人連絡人資訊。

可以整合通訊 (UM) 信箱原則上設定 pin 碼相關的數個設定。**PIN 回收計數**\] 設定會指定唯一的 Pin 使用者數目必須使用之前他們可以重複使用舊的 PIN。您可以設定此設定介於 1 到 20 之間的值。對於大多數的組織而言，此值應設到 5 的 Pin，這是預設值。將此值過高可以讓使用者不耐煩因為可能很難建立並記許多 Pin 的使用者。設定得太低可能會造成您網路的安全性威脅。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>無法停用 PIN 碼回收計數。</td>
</tr>
</tbody>
</table>


如需與 Outlook 語音存取 PIN 碼相關的其他工作，請參閱 [PIN 安全性程序](pin-security-procedures-exchange-2013-help.md)。

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

## 使用 EAC 變更 PIN 碼回收計數

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要變更的撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面中的 \[UM 信箱原則\] 之下，選取您要變更的 UM 信箱原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  按一下 \[PIN 碼原則\]，在 \[PIN 碼回收計數\] 旁輸入 1 到 20 之間的值。

5.  按一下 \[儲存\]。

## 使用命令介面變更 PIN 碼回收計數

此範例會將 UM 信箱原則 `MyUMMailboxPolicy` 中的 PIN 碼回收計數設為 10。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINHistoryCount 10


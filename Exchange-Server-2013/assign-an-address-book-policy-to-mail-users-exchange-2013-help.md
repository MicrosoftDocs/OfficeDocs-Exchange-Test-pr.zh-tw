---
title: '通訊錄原則指派給郵件使用者: Exchange Online Help'
TOCTitle: 通訊錄原則指派給郵件使用者
ms:assetid: bdfe6575-24c0-47d0-9cfb-ece910db248b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh529942(v=EXCHG.150)
ms:contentKeyID: 50474075
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 通訊錄原則指派給郵件使用者

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-10-11_

建立通訊錄原則 (ABP) 之後，您必須將其指派給信箱使用者。未指派給使用者的預設 ABP 建立其使用者帳戶時。如果您未將 ABP 指派給使用者，則會以透過 Outlook 和 Outlook Web App 使用者可以存取整個組織的全域通訊清單 (GAL)。若要深入了解，請參閱[通訊錄原則](address-book-policies-exchange-2013-help.md)。

如需其他 ABP 相關的管理工作資訊，請參閱 [Address book 原則程序](address-book-policy-procedures-exchange-2013-help.md)。

並使用此程序的案例的相關資料嗎？請參閱[案例： 部署通訊錄原則](scenario-deploying-address-book-policies-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - Estmated 完成時間： 少於 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md) 主題中的「通訊錄原則」項目。

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

## 使用 EAC 指派 ABP 給信箱使用者

1.  瀏覽至 \[收件者\] \> \[信箱\]。

2.  在清單檢視中，選取您要為其指派原則的使用者，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  按一下 \[信箱功能\]。

4.  在 \[通訊錄原則\] 清單中，選取您要套用到此使用者的 ABP。

5.  按一下 \[儲存\]。

## 使用 EAC 指派 ABP 給多個信箱使用者

1.  瀏覽至 \[收件者\] \> \[信箱\]。

2.  在清單檢視中，使用 Ctrl 鍵選取多個使用者。

3.  在詳細資料窗格中，按一下 \[其他選項\]。

4.  在 \[通訊錄原則\] 底下，按一下 \[更新\]。

5.  在 \[選取通訊錄原則\] 清單中，選取您要套用到這些使用者的 ABP。

6.  按一下 \[儲存\]。

## 使用命令介面指派 ABP 給信箱使用者

此範例會將 ABP All Fabrikam 指派給現有的信箱使用者 joe@fabrikam.com。

    Set-Mailbox -Identity joe@fabrikam.com -AddressBookPolicy "All Fabrikam"

此範例會將 ABP ABP\_EngineeringDepartment 指派給其 `CustomAttribute11` 值包含 "Engineering Department" 的所有信箱使用者。

    Get-Mailbox -Filter {(CustomAttribute11 -like "Engineering Department")} | Set-Mailbox -AddressBookPolicy ABP_EngineeringDepartment

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\)) 與 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))。


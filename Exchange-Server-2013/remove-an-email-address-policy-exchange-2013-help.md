---
title: '移除電子郵件地址原則: Exchange 2013 Help'
TOCTitle: 移除電子郵件地址原則
ms:assetid: f1d05223-7d41-406d-8fae-f4227be1c1c2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125181(v=EXCHG.150)
ms:contentKeyID: 50474571
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除電子郵件地址原則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-13_

根據預設， Exchange會包含指定收件者的別名為電子郵件地址的本機一部分並使用預設的公認網域的電子郵件地址原則。電子郵件地址的本機部分是出現"at"符號之前的名稱 (@)。此電子郵件地址原則套用至組織中的所有使用者。您無法移除此電子郵件地址原則。

如需瞭解與電子郵件地址原則相關的其他管理工作，請參閱[電子郵件地址原則程序](email-address-policy-procedures-exchange-2013-help.md)。

## 開始前需要瞭解什麼？

  - 預估完成時間：5 分鐘。

  - 如果您移除收件者做為主要原則的電子郵件地址原則，又沒為收件者設定其他原則，則會使用預設原則。

  - 您無法刪除預設原則。如果您想要刪除預設原則，您必須先指派不同的原則為預設值。

  - 如果您要刪除的電子郵件地址原則包含超過 3,000 位收件者，請使用命令介面執行此程序。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子郵件地址和通訊錄](email-addresses-and-address-books-exchange-2013-help.md) 項目中的「電子郵件地址原則」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用 EAC 移除電子郵件地址原則

1.  瀏覽至 \[郵件流程\]\> \[電子郵件地址原則\]。

2.  在清單檢視中，選取您要刪除的電子郵件地址原則，然後按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

3.  在警告中，按一下 \[是\]，移除原則。

## 使用命令介面移除電子郵件地址原則

本範例將會移除電子郵件地址原則 South East Offices。

    Remove-EmailAddressPolicy -Identity "South East Offices"

輸入 **Y** 確認您要移除原則，然後按 ENTER。

如需詳細語法及參數的資訊，請參閱 [Remove-EmailAddressPolicy](https://technet.microsoft.com/zh-tw/library/bb124504\(v=exchg.150\))。


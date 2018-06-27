---
title: '設定 Outlook 語音存取 PIN 安全性: Exchange Online Help'
TOCTitle: 設定 Outlook 語音存取 PIN 安全性
ms:assetid: ef6d9151-d333-4f52-9338-273f7a291e54
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125162(v=EXCHG.150)
ms:contentKeyID: 50554079
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Outlook 語音存取 PIN 安全性

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-16_

當電話連線到語音郵件系統整合通訊 (UM) 的使用者時，他們會使用Outlook語音存取瀏覽功能表系統。使用者可存取語音信箱系統之前，系統會提示他們進入他們的 pin 碼。以管理員身分，您可設定 pin 碼設定和需求及執行 PIN 管理工作。使用者已啟用語音信箱和未產生 PIN 之後，使用者的 pin 碼會儲存在使用者的信箱中加密。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outlook 語音存取使用者必須使用按鍵式 （也稱為複頻式訊號 (DTMF)） 輸入輸入存取已啟用 UM 信箱 pin 碼。語音辨識不適用於 PIN 項目。</td>
</tr>
</tbody>
</table>


**目錄**

PIN overview

PIN requirements

Managing Outlook Voice Access PINs

## PIN 碼概觀

PIN 是，讓使用者可以進行驗證，而獲得存取系統用於特定系統的數字字串。Pin 最常用於自動櫃員機 (Atm)。它們也用而不是英數字元密碼的語音信箱系統。PIN 強度取決於其長度、 如何妥善受到保護，很如何難以猜測。

整合通訊、Outlook 語音存取使用者在類比電話、數位電話或行動電話上輸入其 PIN 碼，使其可以在其 Exchange Server 信箱中存取電子郵件、語音郵件、聯絡人以及行事曆資訊。

在 UM 中，PIN 原則會定義和設定 UM 信箱原則。您可以建立多個 UM 信箱原則需求而定。當您啟用使用者的語音信箱時，您會將使用者連結至現有的 UM 信箱原則。UM 信箱原則設定 UM PIN 原則應該根據組織的安全性需求。

## PIN 碼要求

下列為數種可在 UM 信箱原則中設定的 PIN 碼組態設定。

## 最小 PIN 碼長度

**最小 PIN 長度**設定指定信箱 pin 碼必須包含的數字數目最小值。該範圍是 4 到 24，並預設為 6。如果您輸入 0 時，使用者不需要輸入 PIN。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此設定零不是建議的作法。如果要設定為零的設定，您大幅降低安全性層級為您的網路。</td>
</tr>
</tbody>
</table>


如果將最小 PIN 碼長度的值變更為較高的值，則會先提示 Outlook 語音存取使用者建立一個含有最小位數的新 PIN 碼，才能繼續執行。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>增加此數字會建立更安全的 UM 環境。不過，設得太高可能會導致使用者忘記他們的 pin 碼。</td>
</tr>
</tbody>
</table>


## 強制執行 PIN 碼存留時間

**強制執行 PIN 存留期**設定控制項的時間間隔，天日期 Outlook 語音存取使用者上次變更其 PIN 為他們將強制能夠再次變更他們的 pin 碼的日期。範圍是從 0 到 999 及預設值為 60 天。如果輸入 0，將不會過期的 pin 碼。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>整合通訊不會通知使用者他們的 PIN 碼即將到期。</td>
</tr>
</tbody>
</table>


## 重設 PIN 碼前允許的登入失敗次數

**登入失敗次數之前 pin 碼重設**設定指定循序成功登入嘗試的次數前自動重設 PIN 的信箱。若要停用此功能，設定此設定為 unlimited。否則它必須設定為數小於**鎖定前的登入失敗的次數**\] 設定。該範圍是 1 到 998，及預設值為 5。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要提高具備 UM 功能之使用者的安全性，請輸入一個比 5 還小的數字。</td>
</tr>
</tbody>
</table>


## 鎖定前允許的登入失敗次數

Outlook 語音存取使用者可以在之前進行他們正在鎖定不在其信箱的後續通話中**的鎖定前的登入失敗次數**\] 設定會指定在多少 PIN 項目錯誤。根據預設，會進行 5 次之後，PIN 會自動重設。該範圍是 1 到 999 及預設值為 15。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要增加安全性，減少失敗的嘗試允許的數目。但是請記住降低更加低於預設值為號碼可能會導致必要遭到鎖定的使用者。整合的通訊會產生警告事件如果已啟用 UM 之使用者的 PIN 驗證失敗或使用者是在嘗試登入系統失敗時使用事件檢視器可檢視。</td>
</tr>
</tbody>
</table>


## 允許共同 PIN 碼模式

**允許常見 PIN 模式**設定用來啟用或停用使用一般的數字模式時建立的 pin 碼。根據預設，此設定會停用而不允許輸入下列號碼模式的 Outlook 語音存取使用者：

  - **循序號碼**  完全組成連續的數字的 PIN 值。循序 PIN 號碼的範例會為 1234年與 65432。

  - **重複的數字**  重複的數字組成的 PIN 值。重複的數字的範例是 11111 和 22222。

  - **後置詞信箱分機號碼**  包含使用者的信箱分機號碼的後置詞的 PIN 值。如果信箱副檔名為 36697、 PIN 不能 6697。

## PIN 碼回收計數

**PIN 回收計數**\] 設定會設定不同的 pin 碼使用者必須使用之前可重複使用任何先前所使用的 Pin 號碼。該範圍是 1 到 20，並預設為 5。

## 管理 Outlook 語音存取 PIN 碼

規劃時 Outlook 語音存取 Pin，您必須選擇適當的安全性層級的組織。您必須謹慎考慮 Outlook 語音存取 PIN 需求和 PIN 安全性設定符合或超過貴組織的安全性原則的方式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>它是安全性的最佳作法來實作強式 Outlook 語音存取使用者的 PIN 需求。這可以強制執行藉由建立 UM 信箱原則 PIN 原則需要六個或多個字的 Pin，其會增加為您的網路安全性層級。</td>
</tr>
</tbody>
</table>


設定 Outlook 語音存取 PIN 需求之後，您必須建立並設定 UM 信箱原則來強制執行組織的 pin 碼需求。如需如何建立 UM 信箱原則的詳細資訊，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。如需有關如何管理 UM 信箱原則的詳細資訊，請參閱[管理 UM 信箱原則](manage-a-um-mailbox-policy-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建立 UM 信箱原則之後，您必須連結的啟用 UM 之使用者或使用者與適當的 UM 信箱原則。使用<strong>Enable-UMMailbox</strong>指令程式在Exchange管理命令介面或使用 Exchange 系統管理中心 (EAC) 您可以這麼做。如需Exchange管理命令介面 cmdlet 的詳細資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/aa998033(v=exchg.150)">Enable-UMMailbox</a>。</td>
</tr>
</tbody>
</table>


偶爾 Outlook 語音存取使用者忘記其 PIN 或移出信箱的語音信箱存取鎖定。不論執行哪項中可能需要重設已啟用 UM 之使用者的 PIN。如需詳細資訊，請參閱[重設語音信箱 pin 碼](reset-a-voice-mail-pin-exchange-2013-help.md)。

您可以擷取啟用整合通訊之使用者的 PIN 資訊。傳回給您的資訊是使用加密儲存在使用者信箱的 PIN 資料來計算。這可讓您檢視使用者的 PIN 資訊，而且還會指出使用者是否已鎖定不在他們的信箱。如需詳細資訊，請參閱[擷取語音信箱的 PIN 資訊](retrieve-voice-mail-pin-information-exchange-2013-help.md)。


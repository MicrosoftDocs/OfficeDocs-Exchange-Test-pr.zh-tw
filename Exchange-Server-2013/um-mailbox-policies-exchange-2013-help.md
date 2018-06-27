---
title: 'UM 信箱原則: Exchange Online Help'
TOCTitle: UM 信箱原則
ms:assetid: dfae629e-ee89-4494-a3ed-9655b67eb87e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124909(v=EXCHG.150)
ms:contentKeyID: 50554102
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 信箱原則

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-15_

當您啟用使用者的整合通訊整合通訊 (UM) 信箱原則是必要的。您建立 UM 信箱原則套用至一組語音郵件使用者的信箱的一組通用原則\] 或 \[安全性設定。UM 信箱原則用來指定 UM 設定如下所示：

  - PIN 碼原則

  - 撥號限制

  - 其他一般 UM 信箱原則屬性

例如，您可以建立 UM 信箱原則的 PIN 安全性層級增加降低登入失敗一組特定的已啟用 UM 的使用者，例如高階主管的數目上限。

## UM 信箱原則

至少一個 UM 信箱原則在才能啟用整合通訊的使用者必須已建立。您可以建立其他套用一組通用設定的使用者群組的 UM 信箱原則。

您可以使用 Exchange 管理命令介面或 Exchange 系統管理中心 (EAC) 建立 UM 信箱原則。根據預設，每次您建立 UM 撥號對應表建立單一的 UM 信箱原則。新的 UM 信箱原則會自動產生關聯 UM 撥號對應表，以及部分撥號計劃名稱包含在 UM 信箱原則的顯示名稱。您可以編輯此預設的 UM 信箱原則。

多個已啟用 UM 的使用者可以連結到單一的 UM 信箱原則。不過，每個已啟用 UM 之使用者信箱必須連結至單一的 UM 信箱原則。這可讓您控制 PIN 安全性設定，例如 PIN 的數字數目最小值或登入嘗試次數之相關聯的 UM 信箱原則已啟用 UM 之使用者的數目上限。您也可以控制訊息的文字設定\] 或 \[撥號限制為相同的已啟用 UM 的信箱。


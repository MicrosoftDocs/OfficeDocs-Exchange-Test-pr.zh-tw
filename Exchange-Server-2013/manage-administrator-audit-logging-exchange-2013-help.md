---
title: '管理系統管理員稽核記錄: Exchange 2013 Help'
TOCTitle: 管理系統管理員稽核記錄
ms:assetid: 15c284c0-b8e6-42ca-9913-7c59fdb6885d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335109(v=EXCHG.150)
ms:contentKeyID: 50553940
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理系統管理員稽核記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-05-17_

系統管理員稽核記錄中 Microsoft Exchange Server 2013可讓您建立每次執行指定的指令程式會在記錄項目。記錄項目提供給您何種 cmdlet 所執行、 已使用哪些參數、 誰執行此指令程式，及受哪些物件相關資訊。如需關於系統管理員稽核記錄，請參閱[系統管理員稽核記錄](administrator-audit-logging-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：不到 5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的「系統管理員稽核記錄」項目。

  - 系統管理員稽核記錄依賴Active Directory複寫來複寫到網域控制站您組織中您指定的組態設定。根據您的複寫設定所做的變更可能不會立即套用到貴組織中的所有Exchange 2013伺服器。

  - 稽核記錄檔設定的變更會重新整理已進行組態變更次開啟命令介面的電腦上每隔 60 分鐘。如果您想要套用所做的變更立即、 關閉，然後開啟 \[命令介面中的每部電腦上一次。

  - 命令可能會需要最多 15 分鐘後會出現在稽核記錄搜尋結果中執行。這是因為之前可搜尋稽核記錄項目必須編製索引。如果命令不會出現在系統管理員稽核記錄，請稍候幾分鐘然後重新執行搜尋。

  - 您必須使用命令介面來執行這些程序。

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

## 指定要稽核的指令程式

根據預設，稽核記錄會建立的日誌項目執行的每個指令程式。如果您正在啟用稽核記錄的第一次並想要的行為表現方式，您不需要變更指令程式的 \[稽核\] 清單。如果您先前指定稽核及現在要稽核所有 cmdlet 的指令程式，您可以都稽核所有 cmdlet 搭配**Set-AdminAuditLogConfig**指令程式上*AdminAuditLogCmdlets*參數指定星號 （\*） 萬用字元下列命令所示。

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets *

您可以指定哪些 cmdlet 以稽核在所提供的使用*AdminAuditLogCmdlets*參數的 cmdlet 清單。當您提供的稽核的 cmdlet 清單時，您可以提供單一的 cmdlet，使用星號 （\*） 萬用字元或兩者的混合 cmdlet。在清單中的每個項目是以逗號分隔。下列的值為所有有效項目：

  - `New-Mailbox`

  - `*TransportRule`

  - `*Management*`

  - `Set-Transport*`

本範例將稽核上述清單中所指定的指令程式。

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets New-Mailbox, *TransportRule, *Management*, Set-Transport*

如需詳細的語法及參數資訊，請參閱 [Set-AdminAuditLogConfig](https://technet.microsoft.com/zh-tw/library/dd298169\(v=exchg.150\))。

## 指定要稽核的參數

根據預設，稽核記錄會建立的日誌項目執行時，不論參數指定每個指令程式。如果您正在啟用稽核記錄的第一次並想要的行為表現方式，您不需要變更參數稽核清單。如果您先前指定稽核及現在要稽核的所有參數的參數，您可以這麼**Set-AdminAuditLogConfig**指令程式上*AdminAuditLogParameters*參數指定星號 （\*） 萬用字元以下列命令所示。

    Set-AdminAuditLogConfig -AdminAuditLogParameters *

您可以指定您想要使用*AdminAuditLogParameters*參數稽核哪些的參數。當您提供以稽核在參數清單時，您可以提供單一參數，星號 （\*） 萬用字元或兩者的混合的參數。在清單中的每個項目是以逗號分隔。下列的值為所有有效項目：

  - `Database`

  - `*Address*`

  - `Custom*`

  - `*Region`

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>針對命令執行時要建立的稽核記錄項目，命令必須包含存在於以 <em>AdminAuditLogCmdlets</em> 參數指定的至少一個或多個指令程式上的至少一個或多個參數。</td>
</tr>
</tbody>
</table>


本範例將稽核上述清單中所指定的參數。

    Set-AdminAuditLogConfig -AdminAuditLogParameters Database, *Address*, Custom*, *Region

如需詳細的語法及參數資訊，請參閱 [Set-AdminAuditLogConfig](https://technet.microsoft.com/zh-tw/library/dd298169\(v=exchg.150\))。

## 指定稽核記錄保留限制

稽核記錄保留限制會決定稽核記錄項目保留的期限。當記錄項目超過存留期限制時，因此遭到刪除。預設值為 90 天。

您可以指定天數、 小時、 分鐘和稽核的記錄項目應保留的秒的數。若要指定一個值，請使用格式 dd.hh.mm:ss 出下列適用於：

  - **dd** 保留稽核記錄項目的天數

  - **hh** 保留稽核記錄項目的小時數

  - **mm** 保留稽核記錄項目的分鐘數

  - **ss** 保留稽核記錄項目的秒數

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以將稽核記錄保留限制設為小於比目前保留天數的值。如果您這樣做，則會刪除其存留期超過新保留天數任何稽核記錄項目。<br />
如果您將保留限制設為 0，則 Exchange 會刪除稽核記錄中的所有項目。<br />
建議您僅將設定稽核記錄保留限制的權限授予您非常信任的使用者。</td>
</tr>
</tbody>
</table>


此範例指定保留限制為兩年六個月。

    Set-AdminAuditLogConfig -AdminAuditLogAgeLimit 913.00:00:00

如需詳細的語法及參數資訊，請參閱 [Set-AdminAuditLogConfig](https://technet.microsoft.com/zh-tw/library/dd298169\(v=exchg.150\))。

## 啟用或停用 Test 指令程式的記錄

開始使用動詞**Test** Cmdlet 不預設記錄。這是因為**Test**指令程式可以在短時間產生大量的資料。只啟用短期時間**Test**指令程式記錄功能。

此命令可啟用 **Test**指令程式的記錄。

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $True

此命令可停用 **Test**指令程式的記錄。

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $False

如需詳細的語法及參數資訊，請參閱 [Set-AdminAuditLogConfig](https://technet.microsoft.com/zh-tw/library/dd298169\(v=exchg.150\))。

## 停用系統管理員稽核記錄

若要停用系統管理員稽核記錄，請使用下列命令。

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $False

## 啟用系統管理員稽核記錄

若要啟用系統管理員稽核記錄，請使用下列命令。

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $True

## 檢視系統管理員稽核記錄設定

如果要檢視您為組織設定的系統管理員稽核記錄設定，請使用下列命令。

    Get-AdminAuditLogConfig


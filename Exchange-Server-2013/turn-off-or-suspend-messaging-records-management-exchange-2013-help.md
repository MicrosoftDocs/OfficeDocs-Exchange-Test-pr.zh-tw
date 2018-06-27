---
title: '關閉或擱置郵件記錄管理: Exchange 2013 Help'
TOCTitle: 關閉或擱置郵件記錄管理
ms:assetid: 631191aa-3bba-4ebf-a727-c48ed2ebe176
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998580(v=EXCHG.150)
ms:contentKeyID: 52062546
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 關閉或擱置郵件記錄管理

 

_**適用版本：**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**上次修改主題的時間：**2013-02-14_

若要符合個別、 IT、 或業務需求，您可能需要關閉或暫時擱置郵件記錄管理 (MRM) 或個別使用者的信箱伺服器。您可能需要關閉或暫停 MRM 的原因包括：

  - 如果信箱使用者離開辦公室或否則無法存取電子郵件，您可以暫時停用 MRM 信箱置於保留。當信箱處於 \[保留\] 時它無法再已處理的受管理的資料夾助理員。信箱使用者會傳回或時能夠再次存取信箱，您可以從信箱移除保留功能。

  - 如果您需要測試或解決效能問題，可藉由清除受管理的資料夾助理員的排程，暫時關閉該伺服器上的 MRM。

  - 如果您需要移除信箱的保留標記 (具有套用該標記的保留原則)，可從原則移除標記。

  - 如果您不想再將保留原則或受管理的資料夾信箱原則套用至信箱，可從信箱移除原則。

  - 如果貴組織決定不使用 MRM 功能，您可以關閉 MRM 永久整個組織。如果您稍後決定要部署 MRM，您必須能夠執行這項操作。

## 開始之前有哪些須知？

  - 預估完成時間：1 分鐘

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 您要執行的工作

## 設定信箱的保留功能

您可以將信箱就地保留保留關閉 MRM 暫時 （例如當使用者在休假時）。這會擱置信箱的保留原則處理直到保留功能已停用。這是與就地保留或訴訟保留上放置信箱不同。

如需如何為信箱設定保留功能的詳細資訊，請參閱[就地保留信箱保留 」 狀態](place-a-mailbox-on-retention-hold-exchange-2013-help.md)。

若要深入了解就地保留和訴訟資料暫留，請參閱[就地保留與訴訟暫止](in-place-hold-and-litigation-hold-exchange-2013-help.md)。

## 從信箱移除保留標記

若要從信箱移除保留標記，您取消連結從保留原則標記。取消預設資料夾的保留原則標記 （印） 的連結後，預設信箱標籤套用至該資料夾中的所有項目。取消個人標記的連結後，它不再提供給使用者。標籤套用至現有的郵件會繼續處理除非從 Exchange 組織中移除標籤。

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「郵件記錄管理」項目。

此命令介面範例會從保留原則 \[公司使用者\] 取消連結保留標記 \[3 天刪除\]。

    $tags = (Get-RetentionPolicy "Corp-Users").RetentionPolicyTagLinks
    $tags -= "Deleted Items - 3 Days"
    Set-RetentionPolicy "Corp-Users" -RetentionPolicyTagLinks $tags

如需詳細的語法及參數資訊，請參閱 [Get-RetentionPolicy](https://technet.microsoft.com/zh-tw/library/dd298086\(v=exchg.150\)) 與 [Set-RetentionPolicy](https://technet.microsoft.com/zh-tw/library/dd335196\(v=exchg.150\))。

## 從信箱移除保留原則

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「套用保留原則」項目。

您可以藉由從信箱使用者的內容移除原則，停止將保留原則套用至信箱。

此命令介面範例會從信箱 jpeoples 移除保留原則。

    Set-Mailbox jpeoples -RetentionPolicy $null.

此命令介面範例會從 Exchange 組織中的所有信箱移除保留原則。

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -ne $null} | Set-Mailbox -RetentionPolicy $null

此命令介面範例會從已套用原則之所有信箱使用者移除保留原則 \[公司財務\]。

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -eq "Corp-Finance"} | Set-Mailbox -RetentionPolicy $null

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\)) 與 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))。

## 為整個組織永久關閉 MRM

若要關閉 MRM 的組織\] 刪除所有的保留標記和保留原則除外 Exchange 安裝程式所建立的 ArbitrationMailbox 原則\]。這是完成之後，保留原則不會強制執行。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>保留原則也包含移至封存標記，將郵件移至使用者的封存信箱。如果您移除已移至封存標記的保留原則，已套用之原則的使用者將不再有移至封存中的受管理的資料夾助理員的郵件。<br />
若要避免此問題，從您的組織移除只刪除並允許復原和永久刪除標記及保留已移至封存標籤套用的原則。或者，有使用者並啟用封存無法手動使用Outlook或Outlook Web App封存信箱移動項目。<br />
然後再移除保留標記與保留原則，我們建議您檢查要移除的標記的設定。不要刪除具有移至封存保留動作標籤。</td>
</tr>
</tbody>
</table>


您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「郵件記錄管理」項目。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在下列命令中加入 <em>WhatIf</em> 參數，以模擬命令所採取的動作。</td>
</tr>
</tbody>
</table>


此範例會從 Exchange 組織中移除所有刪除標記，但 \[永不刪除\] 標記除外，它用於 Exchange 安裝程式所建立的 ArbitrationMailbox 原則中。

    Get-RetentionPolicyTag | ? {$_.RetentionAction -ne "MoveToArchive" -and $_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

此範例會移除 \[永不刪除\] 標記除外的其他所有保留標記。

    Get-RetentionPolicyTag | ? {$_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

此命令會從 Exchange 組織中移除 Corp-Users 保留原則。

    Remove-RetentionPolicy Corp-Users

如需詳細的語法及參數資訊，請參閱下列主題：

  - [Get-RetentionPolicyTag](https://technet.microsoft.com/zh-tw/library/dd298009\(v=exchg.150\))

  - [Remove-RetentionPolicyTag](https://technet.microsoft.com/zh-tw/library/dd335092\(v=exchg.150\))

  - [Remove-RetentionPolicy](https://technet.microsoft.com/zh-tw/library/dd297962\(v=exchg.150\))


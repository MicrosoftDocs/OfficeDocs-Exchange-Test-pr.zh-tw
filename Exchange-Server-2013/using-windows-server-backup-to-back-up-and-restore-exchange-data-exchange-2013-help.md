---
title: '使用 Windows Server Backup 備份及還原 Exchange 資料: Exchange 2013 Help'
TOCTitle: 使用 Windows Server Backup 備份及還原 Exchange 資料
ms:assetid: 0fac891a-5713-42b6-afd5-c91b2b88f966
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876851(v=EXCHG.150)
ms:contentKeyID: 50472581
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 Windows Server Backup 備份及還原 Exchange 資料

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Microsoft 的[慣用的架構](https://blogs.technet.com/b/exchange/archive/2014/04/21/the-preferred-architecture.aspx)的Exchange Server 2013如何運用稱為Exchange原生資料保護概念。Exchange原生資料保護依賴原生Exchange功能來保護您的信箱資料、 不使用傳統的備份。但如果您想要建立備份， Exchange包含Windows Server備份 (WSB) 可讓您建立 Exchange 感知的磁碟區陰影複製服務 VSS 型Exchange資料備份外掛程式。若要使 Exchange 感知的備份，您必須安裝 WSB 功能。

外掛程式 WSBExchange.exe 以服務方式執行，稱為 Microsoft Exchange Server Extension for Windows Server Backup (此服務的簡稱為 WSBExchange)。這項服務會自動安裝在所有信箱伺服器上並設定為手動啟動。此外掛程式可讓 WSB 建立 Exchange 感知的 VSS 備份。

使用 WSB 來備份 Exchange 資料之前，建議您先熟悉外掛程式的下列功能與選項：

  - 使用 WSB 來備份是在磁碟區層級上進行，執行應用程式層級備份或還原的唯一方法是選取整個磁碟區。若要備份資料庫及其記錄資料流，您必須備份包含資料庫與記錄檔在內的整個磁碟區，而不只是個別的資料夾。您無法僅備份某些資料，而不備份該資料所在的整個磁碟區。

  - 備份必須在要執行備份的伺服器上以本機方式執行，而且無法使用外掛程式製作遠端 VSS 備份。WEB 或外掛程式不支援遠端管理。不過，您可以使用遠端桌面服務或終端機服務從遠端管理備份。

  - 備份可建立在本機磁碟機或遠端網路共用位置上。

  - 只應該進行完整備份。只有在包含 Exchange 資料庫的磁碟區或資料夾順利完成 VSS 完整備份後，才會進行記錄檔截斷。

  - 還原資料時，可以只還原 Exchange 資料。這項資料可還原至其原始位置或替代位置。若將資料還原至其原始位置，WSB 與外掛程式會自動處理復原程序，包括卸載任何現有的資料庫，以及將記錄檔重新顯示在還原的資料庫中。

  - 還原程序不支援 Exchange 復原資料庫 (RDB)。如果您要使用 RDB，則必須將資料還原至替代位置，然後手動從該位置將還原的資料複製或移動到 RDB 資料夾結構中。

  - 還原 Exchange 資料時，所有備份的資料庫都必須同時還原。您無法還原單一資料庫。

  - 使用 WSB 時支援裸機還原；不過，Exchange 伺服器的建議復原方法是先復原 Exchange 伺服器，再還原資料。如果您使用協力廠商備份應用程式 (例如，非 Microsoft)，備份應用程式廠商可能會提供 Exchange 裸機還原的支援。

下表描述 Exchange 2013 搭配 WSB 所支援的備份及復原選項。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果您...</th>
<th>進行的動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>備份完整的伺服器...</p></td>
<td><p>將執行 VSS 複製備份，且不會截斷伺服器上資料庫的交易記錄。</p></td>
</tr>
<tr class="even">
<td><p>執行自訂的備份，然後選取要備份的一或多個磁碟區...</p></td>
<td><p>可選取 VSS 完整備份，允許順利完成備份時在所選取磁碟區上截斷資料庫的交易記錄。</p></td>
</tr>
<tr class="odd">
<td><p>執行自訂的備份，然後選取要備份的一或多個資料夾...</p></td>
<td><p>可選取 VSS 完整備份，且會截斷記錄檔；不過，備份的還原只限於檔案還原，因為不支援應用程式層級還原。</p></td>
</tr>
</tbody>
</table>


如需有關使用 WSB 來備份 Exchange 的詳細步驟，請參閱＜[使用 Windows Server Backup 來備份 Exchange](use-windows-server-backup-to-back-up-exchange-exchange-2013-help.md)＞。

如需有關從 WSB 製作的備份中還原資料的詳細步驟，請參閱＜[使用 Windows Server Backup 還原 Exchange 的備份](use-windows-server-backup-to-restore-a-backup-of-exchange-exchange-2013-help.md)＞。


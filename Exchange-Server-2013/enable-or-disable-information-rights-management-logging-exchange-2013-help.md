---
title: '啟用或停用資訊版權管理記錄: Exchange 2013 Help'
TOCTitle: 啟用或停用資訊版權管理記錄
ms:assetid: 6933bc65-4d98-4878-9167-0e9eaac68b6b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff686962(v=EXCHG.150)
ms:contentKeyID: 50473389
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用資訊版權管理記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-12_

在Exchange Server 2013，您可以使用資訊版權管理 (IRM) 記錄檔來監視及疑難排解 IRM 作業。預設會啟用 IRM 記錄。

IRM 記錄使用下列一組通用的參數：

  - *IrmLogEnabled*  啟用或停用 IRM 記錄。預設值： `$true`。

  - *IrmLogMaxAge*  會指定 IRM 記錄檔的保留天數上限。會刪除早於指定的存留期的檔案。預設值： 30 天。

  - *IrmLogMaxDirectorySize*  指定包含 IRM 記錄檔的目錄的大小上限。時目錄達到其最大檔案大小，伺服器會先刪除最舊的記錄檔。預設值： 250 MB。

  - *IrmLogMaxFileSize*  會指定每個 IRM 記錄檔的大小上限。當記錄檔達到指定的大小時，會建立新的記錄檔。預設值： 10 MB。

  - *IrmLogPath*  會指定 IRM 記錄檔目錄的位置。預設值： `%ExchangeInstallPath%Logging\IRMLogs`。

若欲瞭解更多與 IRM 相關的管理工作，請參閱 [資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成每項程序預估時間： 2-5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 主題中的「設定 IRM 記錄」項目　。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來啟用或停用 IRM 登入伺服器。您必須使用命令介面

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


## 使用命令介面啟用伺服器上的 IRM 記錄

此範例會在信箱伺服器上啟用 IRM 記錄。

    Set-TransportService -Identity EXCH01 -IRMLogEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-TransportService](https://technet.microsoft.com/zh-tw/library/jj215682\(v=exchg.150\))。

## 使用命令介面停用伺服器上的 IRM 記錄

此範例會在信箱伺服器上停用 IRM 記錄。

    Set-TransportService -Identity EXCH01 -IRMLogEnabled $false

如需詳細的語法及參數資訊，請參閱 [Set-TransportService](https://technet.microsoft.com/zh-tw/library/jj215682\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證您已成功地在伺服器上啟用或停用 IRM 記錄，請執行 [Get-TransportService](https://technet.microsoft.com/zh-tw/library/jj215746\(v=exchg.150\)) 指令程式來擷取 IRM 設定。

此範例會擷取伺服器 EXCH01 上的所有 IRM 記錄內容。

    Get-TransportService -Identity EXCH01 | Format-List IRMLog*


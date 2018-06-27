---
title: '從佇列匯出訊息: Exchange 2013 Help'
TOCTitle: 從佇列匯出訊息
ms:assetid: 688b342c-f380-4fe0-afce-7e38cf490627
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998625(v=EXCHG.150)
ms:contentKeyID: 51409187
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 從佇列匯出訊息

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-05-05_

當您從佇列將郵件匯出到檔案時，並不會從佇列中移除郵件。而會在指定的位置中以純文字檔形式建立郵件的複本。您可以在文字編輯器之類的應用程式或是電子郵件用戶端應用程式中檢視結果檔案，或是使用 Exchange 組織內外的任何其他 Mailbox Server 或 Edge Transport Server 上的重新顯示目錄來重新提交郵件檔案。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「佇列」項目。

  - 郵件必須處於「已擱置」狀態，匯出程序才能成功。您可以從傳遞佇列、無法存取的佇列或毒藥郵件佇列中匯出郵件。毒藥郵件佇列中的郵件已處於「已擱置」狀態。您無法擱置或匯出位於提交佇列中的郵件。

  - 您無法使用 Exchange 工具箱的佇列檢視器來匯出郵件。不過，在使用命令介面來匯出郵件之前，您可以使用佇列檢視器來尋找、識別及擱置郵件。

  - 確認郵件檔案之目標目錄位置的下列資訊：
    
      - 必須有目標目錄，您才能匯出郵件。系統不會為您建立目錄。若未指定絕對路徑，則會使用目前的 Exchange 管理命令介面工作目錄。
    
      - 該路徑可以在 Exchange 伺服器上，或是遠端伺服器上共用資料夾的通用命名慣例 (UNC) 路徑。
    
      - 您的帳戶必須要有該目標目錄的**寫入**權限。
    
      - 指定匯出之郵件的檔名時，請確定有加上 .eml 副檔名，使電子郵件用戶端應用程式可以輕易開啟該檔案，或讓重新顯示目錄正確處理該檔案。

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

## 使用命令介面從特定的佇列匯出特定的郵件

若要從特定佇列中匯出特定郵件，請執行下列命令：

    Export-Message -Identity <MessageIdentity> | AssembleMessage -Path <FilePath>\<FileName>.eml

此範例會將伺服器 Exchange01 的 contoso.com 傳遞佇列中具有 **InternalMessageID** 值 1234 的郵件副本，匯出至路徑 D:\\Contoso Export 中名為 export.eml 的檔案。

    Export-Message -Identity Exchange01\Contoso.com\1234 | AssembleMessage -Path "D:\Contoso Export\export.eml"

## 使用命令介面從特定的佇列匯出所有的郵件

若要從特定佇列中匯出所有郵件，並使用每個郵件的 **InternetMessageID** 值作為檔名，請使用下列語法。

    Get-Message -Queue <QueueIdentity> | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

請注意，**InternetMessageID** 值包含角括弧 (\> 和 \<)，但檔名中不允許此值，所以必須予以移除。

此範例會從伺服器 Mailbox01 上的 contoso.com 傳遞佇列中，將所有郵件的副本匯出至名為 D:\\Contoso Export 的本機目錄。

    Get-Message -Queue Mailbox01\Contoso.com | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

## 使用命令介面從伺服器上的所有佇列匯出特定的郵件

若要從伺服器的所有佇列中匯出特定郵件，並使用每個郵件的 **InternetMessageID** 值作為檔名，請使用下列語法。

    Get-Message -Filter {<MessageFilter>} [-Server <ServerIdentity>] | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

請注意，**InternetMessageID** 值包含角括弧 (\> 和 \<)，但檔名中不允許此值，所以必須予以移除。

此範例會從伺服器 Mailbox01 上所有佇列中，將 contoso.com 網域的寄件者寄來的所有郵件的副本，匯出至名為 D:\\Contoso Export 的本機目錄。

    Get-Message -Filter {FromAddress -like "*@contoso.com"} -Server Mailbox01 | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果省略 <em>Server</em> 參數，則命令會在本機伺服器上執行。</td>
</tr>
</tbody>
</table>


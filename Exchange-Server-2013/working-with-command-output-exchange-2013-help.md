---
title: '使用命令輸出: Exchange 2013 Help'
TOCTitle: 使用命令輸出
ms:assetid: 8320e1a5-d3f5-4615-878d-b23e2aaa6b1e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123533(v=EXCHG.150)
ms:contentKeyID: 50473617
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用命令輸出

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

Exchange 管理命令介面提供數個方法，供您用來格式化命令輸出。本主題討論下列主題：

  - 如何格式化資料   使用 **Format-List**、**Format-Table** 及 **Format-Wide** Cmdlet，控制如何將所見到之資料格式化。

  - 如何輸出資料   使用 **Out-Host** 和 **Out-File** Cmdlet，決定資料是要輸出至命令介面主控台視窗或檔案。本主題中包括的範例指令碼，會將資料輸出至 MicrosoftInternet Explorer。

  - 如何篩選資料   使用下列任一篩選方法來篩選資料：
    
      - 特定 Cmdlet 上可用的伺服器端篩選。
    
      - 所有 Cmdlet 上均可使用的用戶端篩選，會將命令的結果以管線傳輸至 **Where-Object** Cmdlet。

若要使用本主題中所描述的功能，您必須先熟悉下列概念：

  - [管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))

  - [殼層變數](https://technet.microsoft.com/zh-tw/library/bb124036\(v=exchg.150\))

  - [比較運算子](https://technet.microsoft.com/zh-tw/library/bb125229\(v=exchg.150\))

## 如何格式化資料

如果在管線尾端呼叫格式化 Cmdlet，便可覆寫預設的格式化，控制要顯示哪種資料及如何呈現該資料。格式化 Cmdlet 分別是 **Format-List**、**Format-Table** 和 **Format-Wide**。每一個 Cmdlet 都有不同於其他格式化 Cmdlet 的專屬輸出樣式。

## Format-List

**Format-List** Cmdlet 可從管線取得輸入，然後輸出每一個物件之所有指定內容的垂直欄清單。您可以使用 *Property* 參數指定要顯示的內容。如果呼叫 **Format-List** Cmdlet 時未指定任何參數，則會輸出所有內容。**Format-List** Cmdlet 會將文字換行而不會截斷它們。**Format-List** Cmdlet 的最佳用途之一是覆寫 Cmdlet 的預設輸出，使您可以擷取其他或更重要的資訊。

例如，呼叫 **Get-Mailbox** Cmdlet 時，只會看到以表格格式呈現的少量資訊。如果以管線將 **Get-Mailbox** Cmdlet 的輸出傳輸至 **Format-List** Cmdlet，並新增要檢視之其他或更重要資訊的參數，則您可以擷取想要的輸出。

您也可以指定萬用字元 "\*"，以代表部分的內容名稱。如果包括萬用字元，則可比對多個內容，而不需個別輸入每一個內容名稱。例如，`Get-Mailbox | Format-List -Property Email* ` 會傳回以 `Email` 開始的所有內容。

下列範例會顯示可供您檢視 **Get-Mailbox** Cmdlet 所傳回之相同資料的不同方式。

    Get-Mailbox TestUser1
    
    Name                      Alias                ServerName       ProhibitSendQuo
                                                                    ta
    ----                      -----                ----------       ---------------
    TestUser1                 TestUser1            mbx              unlimited

在第一個範例中，會呼叫不含特定格式的 **Get-Mailbox** Cmdlet，使預設輸出的格式為表格格式，並包含預定的內容集。

    Get-Mailbox TestUser1 | Format-List -Property Name,Alias,EmailAddresses
    
    Name           : TestUser1
    Alias          : TestUser1
    EmailAddresses : {SMTP:TestUser1@contoso.com}

在第二個範例中，**Get-Mailbox** Cmdlet 的輸出連同特定內容，會以管線傳輸至 **Format-List** Cmdlet。誠如所見，此輸出的格式和內容大不相同。

    Get-Mailbox TestUser1 | Format-List -Property Name, Alias, Email*
    Name                      : Test User
    Alias                     : TestUser1
    EmailAddresses            : {SMTP:TestUser1@contoso.com}
    EmailAddressPolicyEnabled : True

在最後一個範例中，**Get-Mailbox** Cmdlet 的輸出會以管線傳輸至 **Format-List** Cmdlet，如第二個範例所示。不過，在最後一個範例中，會使用萬用字元來比對以 `Email` 開頭的所有內容。

如果有多個物件傳遞至 **Format-List** Cmdlet，則物件的所有指定內容會按物件顯示並加以群組。顯示順序視 Cmdlet 的預設參數而定。最常見的預設參數是 *Name* 參數或 *Identity* 參數。例如，呼叫 **Get-Childitem** Cmdlet 時，預設顯示順序是按英文字母順序排列的檔案名稱。若要變更此行為，您必須呼叫 **Format-List** Cmdlet，連同 *GroupBy* 參數，以及您要用來將輸出加以群組的內容值名稱。例如，下列命令會列出目錄中的所有檔案，然後按副檔名將這些檔案加以群組。

    Get-Childitem | Format-List Name,Length -GroupBy Extension
    
        Extension: .xml
    
    Name   : Config_01.xml
    Length : 5627
    
    Name   : Config_02.xml
    Length : 3901
    
    
        Extension: .bmp
    
    Name   : Image_01.bmp
    Length : 746550
    
    Name   : Image_02.bmp
    Length : 746550
    
    
        Extension: .txt
    
    Name   : Text_01.txt
    Length : 16822
    
    Name   : Text_02.txt
    Length : 9835

在這個範例中，**Format-List** Cmdlet 會按 *GroupBy* 參數指定的 *Extension* 內容，將項目加以群組。您可以在管線資料流中，使用含有物件之任何有效內容的 *GroupBy* 參數。

## Format-Table

**Format-Table** Cmdlet 可讓您以含有標籤標題及內容資料欄的表格格式來顯示項目。根據預設，許多 Cmdlet (如 **Get-Process** 和 **Get-Service** Cmdlet) 都會針對輸出使用表格格式。**Format-Table** Cmdlet 的參數包括 *Properties* 和 *GroupBy* 參數。這些參數的作用與 **Format-List** Cmdlet 的作用一模一樣。

**Format-Table** Cmdlet 也會使用 *Wrap* 參數。此參數可讓冗長的內容資訊行全部顯示出來，而不會在行尾遭到截斷。若要了解如何使用 *Wrap* 參數來顯示傳回的資訊，請比較下列兩個範例中之 **Get-Command** 命令的輸出。

在第一個範例中，使用 **Get-Command** Cmdlet 來顯示 **Get-Process** Cmdlet 的相關命令資訊時，*Definition* 內容的資訊會遭到截斷。

    Get-Command Get-Process | Format-Table Name,Definition
    
    Name                                    Definition
    ----                                    ----------
    get-process                             get-process [[-ProcessName] String[]...

在第二個範例中，*Wrap* 參數會新增至命令中，以強迫顯示 *Definition* 內容的完整內容。

    Get-Command Get-Process | Format-Table Name,Definition -Wrap
    
    Get-Process                             Get-Process [[-Name] <String[]>] [-Comp
                                            uterName <String[]>] [-Module] [-FileVe
                                            rsionInfo] [-Verbose] [-Debug] [-ErrorA
                                            ction <ActionPreference>] [-WarningActi
                                            on <ActionPreference>] [-ErrorVariable
                                            <String>] [-WarningVariable <String>] [
                                            -OutVariable <String>] [-OutBuffer <Int
                                            32>]
                                            Get-Process -Id <Int32[]> [-ComputerNam
                                            e <String[]>] [-Module] [-FileVersionIn
                                            fo] [-Verbose] [-Debug] [-ErrorAction <
                                            ActionPreference>] [-WarningAction <Act
                                            ionPreference>] [-ErrorVariable <String
                                            >] [-WarningVariable <String>] [-OutVar
                                            iable <String>] [-OutBuffer <Int32>]
                                            Get-Process [-ComputerName <String[]>]
                                            [-Module] [-FileVersionInfo] -InputObje
                                            ct <Process[]> [-Verbose] [-Debug] [-Er
                                            rorAction <ActionPreference>] [-Warning
                                            Action <ActionPreference>] [-ErrorVaria
                                            ble <String>] [-WarningVariable <String
                                            >] [-OutVariable <String>] [-OutBuffer
                                            <Int32>]

如同 **Format-List** Cmdlet，您也可以指定萬用字元 "`*`"，來代表部分的內容名稱。藉由包括萬用字元，您就可以比對多個內容，而不必個別輸入每一個內容名稱。

## Format-Wide

**Format-Wide** Cmdlet 會提供比其他格式 Cmdlet 更簡易的輸出控制。根據預設，**Format-Wide** Cmdlet 會嘗試盡可能地在一行輸出中顯示更多欄的內容值。您可以藉由新增參數，來控制欄數及輸出空間的使用方式。

在最基本的用法中，呼叫不含任何參數的 **Format-Wide** Cmdlet，會儘量以頁面可容納的最多欄數來排列輸出。例如，如果執行 **Get-Childitem** Cmdlet，並以管線將其輸出傳輸至 **Format-Wide** Cmdlet，您會看到下列的顯示資訊：

    Get-ChildItem | Format-Wide
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml                           Config_02.xml
    Config_03.xml                           Config_04.xml
    Config_05.xml                           Config_06.xml
    Config_07.xml                           Config_08.xml
    Config_09.xml                           Image_01.bmp
    Image_02.bmp                            Image_03.bmp
    Image_04.bmp                            Image_05.bmp
    Image_06.bmp                            Text_01.txt
    Text_02.txt                             Text_03.txt
    Text_04.txt                             Text_05.txt
    Text_06.txt                             Text_07.txt
    Text_08.txt                             Text_09.txt
    Text_10.txt                             Text_11.txt
    Text_12.txt

一般而言，呼叫不含任何參數的 **Get-Childitem** Cmdlet，會顯示內容表格中之目錄內所有檔案的名稱。在這個範例中，以管線將 **Get-Childitem** Cmdlet 的輸出傳輸至 **Format-Wide** Cmdlet 之後，該輸出會以兩欄名稱顯示。請注意，一次只能顯示一個內容類型，這是由 **Format-Wide** Cmdlet 後面的內容名稱所指定。如果新增 *Autosize* 參數，該輸出將從兩欄變更為螢幕寬度可容納的欄數。

    Get-ChildItem | Format-Wide -AutoSize
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml   Config_02.xml   Config_03.xml   Config_04.xml   Config_05.xml
    Config_06.xml   Config_07.xml   Config_08.xml   Config_09.xml   Image_01.bmp
    Image_02.bmp    Image_03.bmp    Image_04.bmp    Image_05.bmp    Image_06.bmp
    Text_01.txt     Text_02.txt     Text_03.txt     Text_04.txt     Text_05.txt
    Text_06.txt     Text_07.txt     Text_08.txt     Text_09.txt     Text_10.txt
    Text_11.txt     Text_12.txt

在這個範例中，表格會排列成五欄，而非兩欄。*Column* 參數提供更大的控制，可讓您指定要顯示資訊的最大欄數，如下所示：

    Get-ChildItem | Format-Wide -Column 4
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml       Config_02.xml       Config_03.xml       Config_04.xml
    Config_05.xml       Config_06.xml       Config_07.xml       Config_08.xml
    Config_09.xml       Image_01.bmp        Image_02.bmp        Image_03.bmp
    Image_04.bmp        Image_05.bmp        Image_06.bmp        Text_01.txt
    Text_02.txt         Text_03.txt         Text_04.txt         Text_05.txt
    Text_06.txt         Text_07.txt         Text_08.txt         Text_09.txt
    Text_10.txt         Text_11.txt         Text_12.txt

在這個範例中，可使用 *Column* 參數，強迫欄數變成四個。

## 如何輸出資料

## Out-Host 和 Out-File Cmdlet

**Out-Host** Cmdlet 是位於管線尾端、不會顯示的預設 Cmdlet。在套用所有格式化之後，**Out-Host** Cmdlet 會將最後輸出傳送至主控台視窗，以進行顯示。您不必明確地呼叫 **Out-Host** Cmdlet，因為它是預設輸出。您可以呼叫 **Out-File** Cmdlet 做為命令的最後一個 Cmdlet，來置換將輸出傳送至主控台視窗的行為。**Out-File** Cmdlet 則會接著將輸出寫至您在命令中指定的檔案，如下列範例所示：

    Get-ChildItem | Format-Wide -Column 4 | Out-File c:\OutputFile.txt

在這個範例中，**Out-File** Cmdlet 會將 **Get-ChildItem | Format-Wide -Column 4** 命令所顯示的資訊寫至名為 `OutputFile.txt` 的檔案中。您也可以使用重新導向運算子，即右角括弧 (`>`)，將管線輸出重新導向至檔案。若要將命令的管線輸出附加至現有檔案而不取代原始檔案，請使用雙右角括弧 (`>>`)，如下列範例所示：

    Get-ChildItem | Format-Wide -Column 4 >> C:\OutputFile.txt

在這個範例中，**Get-Childitem** Cmdlet 的輸出會以管線傳輸至 **Format-Wide** Cmdlet 進行格式化，然後寫至 `OutputFile.txt` 檔案的結尾。請注意，如果 `OutputFile.txt` 檔案不存在，則使用雙右角括弧 (`>>`) 將會建立該檔案。

如需管線的詳細資訊，請參閱[管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))。

如需上述範例所用之語法的詳細資訊，請參閱[語法](https://technet.microsoft.com/zh-tw/library/bb123552\(v=exchg.150\))。

## 在 Internet Explorer 檢視資料

因為在 Exchange 管理命令介面中編寫指令碼容易又有彈性，您可以取得命令傳回的資料，並以數不盡的各種方式將其格式化及輸出。

下列範例會顯示如何使用簡易指令碼來輸出命令所傳回的資料，並將它顯示在 Internet Explorer 中。這個指令碼會取得透過管線傳遞的物件、開啟 Internet Explorer 視窗，然後在 Internet Explorer 中顯示資料：

    $Ie = New-Object -Com InternetExplorer.Application
    $Ie.Navigate("about:blank")
    While ($Ie.Busy) { Sleep 1 }
    $Ie.Visible = $True
    $Ie.Document.Write("$Input")
    # If the previous line doesn't work on your system, uncomment the line below.
    # $Ie.Document.IHtmlDocument2_Write(\"$Input\")
    $Ie

若要使用此指令碼，請將它儲存到要執行此指令碼之電腦上的 `C:\Program Files\Microsoft\Exchange Server\V15\Scripts` 目錄中。將該檔案命名為 `Out-Ie.ps1`。儲存該檔案之後，您就可以使用該指令碼做為一般 Cmdlet。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要在 Exchange 2013 中執行指令碼，必須新增指令碼至未限定範圍的管理角色，且您必須直接獲派管理角色，或透過管理角色群組獲派管理角色。如需詳細資訊，請參閱<a href="understanding-management-roles-exchange-2013-help.md">了解管理角色</a>。</td>
</tr>
</tbody>
</table>


`Out-Ie` 指令碼會假設它接收的資料是有效的 HTML。若要將您想檢視的資料轉換成 HTML，必須以管線將命令的結果傳輸至 **ConvertTo-Html** Cmdlet。然後，以管線將該命令的結果傳輸至 `Out-Ie` 指令碼。下列範例會顯示如何在 Internet Explorer 視窗中檢視目錄清單：

    Get-ChildItem | Select Name,Length | ConvertTo-Html | Out-Ie

## 如何篩選資料

命令介面可讓您存取關於組織內的伺服器、信箱、Active Directory 及其他物件的大量資訊。雖然存取此資訊有助於您進一步了解環境，但大量的資訊也很可能令您無法招架。命令介面可讓您控制此資訊，並使用篩選來傳回您想看到的資料。有下列幾種篩選類型可用：

  - **伺服器端篩選**   伺服器端篩選會使用您在命令列上指定的篩選，並將它提交給您查詢的 Exchange 伺服器。該伺服器會處理查詢，並只傳回符合您指定之篩選的資料。
    
    伺服器端篩選只能針對可傳回幾萬或幾十萬個結果的物件執行。因此，只有收件者管理 Cmdlet (如 **Get-Mailbox** Cmdlet) 和佇列管理 Cmdlet (如 **Get-Queue** Cmdlet) 才支援伺服器端篩選。這些 Cmdlet 支援 *Filter* 參數。此參數會使用您指定的篩選運算式，並將它提交給伺服器處理。

  - **用戶端篩選**   用戶端篩選是在您目前使用之本機主控台視窗中的物件上執行。當您使用用戶端篩選時，Cmdlet 會擷取符合您在本機主控台視窗上執行之工作的所有物件。然後，命令介面會取得所有傳回的結果、對那些結果套用用戶端篩選，並只傳回符合篩選的結果。所有的 Cmdlet 都支援用戶端篩選。這是以管線將命令的結果傳輸至 **Where-Object** Cmdlet 來呼叫。

## 伺服器端篩選

伺服器端篩選的實作是支援它之 Cmdlet 所特有的。伺服器端篩選只可在傳回之物件的特定內容上加以啟用。如需詳細資訊，請參閱下列 Cmdlet 的 \[說明\]：


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-ActiveSyncDevice</p></td>
<td><p>Get-ActiveSyncDeviceClass</p></td>
<td><p>Get-CASMailbox</p></td>
<td><p>Get-Contact</p></td>
<td><p>Get-DistributionGroup</p></td>
</tr>
<tr class="even">
<td><p>Get-DynamicDistributionGroup</p></td>
<td><p>Get-Group</p></td>
<td><p>Get-Mailbox</p></td>
<td><p>Get-MailboxStatistics</p></td>
<td><p>Get-MailContact</p></td>
</tr>
<tr class="odd">
<td><p>Get-MailPublicFolder</p></td>
<td><p>Get-MailUser</p></td>
<td><p>Get-Message</p></td>
<td><p>Get-MobileDevice</p></td>
<td><p>Get-Queue</p></td>
</tr>
<tr class="even">
<td><p>Get-QueueDigest</p></td>
<td><p>Get-Recipient</p></td>
<td><p>Get-RemoteMailbox</p></td>
<td><p>Get-RoleGroup</p></td>
<td><p>Get-SecurityPrincipal</p></td>
</tr>
<tr class="odd">
<td><p>Get-StoreUsageStatistics</p></td>
<td><p>Get-UMMailbox</p></td>
<td><p>Get-User</p></td>
<td><p>Get-UserPhoto</p></td>
<td><p>Remove-Message</p></td>
</tr>
<tr class="even">
<td><p>Resume-Message</p></td>
<td><p>Resume-Queue</p></td>
<td><p>Retry-Queue</p></td>
<td><p>Suspend-Message</p></td>
<td><p>Suspend-Queue</p></td>
</tr>
</tbody>
</table>


## 用戶端篩選

用戶端篩選可與任何 Cmdlet 一起使用。這項功能包括同時支援伺服器端篩選的那些 Cmdlet。如本主題稍早所述，用戶端篩選會接收管線中前一個命令傳回的所有資料，然後只傳回符合您指定之篩選器的結果。**Where-Object** Cmdlet 會執行此篩選。它可簡化為 **Where**。

當資料透過管線傳遞時，**Where** Cmdlet 會從先前的物件接收資料，接著篩選資料，之後才會將它傳遞至下一個物件。篩選是以 **Where** 命令所定義的指令碼區塊為基礎。指令碼區塊會根據物件的內容和值來篩選資料。

**Clear-Host** Cmdlet 是用來清除主控台視窗。在這個範例中，如果您執行下列命令，即可找到 **Clear-Host** Cmdlet 的所有已定義別名：

    Get-Alias | Where {$_.Definition -eq "Clear-Host"}
    
    CommandType     Name                            Definition
    -----------     ----                            ----------
    Alias           clear                           clear-host
    Alias           cls                             clear-host

**Get-Alias** Cmdlet 會與 **Where** 命令一起運作，以傳回已對 **Clear-Host** Cmdlet 而非其他 Cmdlet 定義的別名清單。下表概述此範例所使用之 **Where** 命令的每一個元素。

### Where 命令的元素

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>{ }</code></p></td>
<td><p>以大括弧括住定義篩選器的指令碼區塊。</p></td>
</tr>
<tr class="even">
<td><p><code>$_</code></p></td>
<td><p>此特殊變數會自動起始及繫結到管線中的物件。</p></td>
</tr>
<tr class="odd">
<td><p><code>Definition</code></p></td>
<td><p><code>Definition</code> 內容是儲存別名定義名稱之目前管線物件的內容。當 <code>Definition</code> 與 <code>$_</code> 變數一起使用時，內容名稱前面會有一個句點。</p></td>
</tr>
<tr class="even">
<td><p><code>-eq</code></p></td>
<td><p>這個「等於」比較運算子是用來指定其結果必須完全符合運算式中所提供的內容值。</p></td>
</tr>
<tr class="odd">
<td><p>&quot;<strong>Clear-Host</strong>&quot;</p></td>
<td><p>在這個範例中，&quot;<strong>Clear-Host</strong>&quot; 是命令剖析的值。</p></td>
</tr>
</tbody>
</table>


在這個範例中，**Get-Alias** Cmdlet 傳回的物件代表系統上所有已定義的別名。即使您沒有在命令列上看到它們，也可收集別名，並透過管線傳遞至 **Where** Cmdlet。**Where** Cmdlet 會使用指令碼區塊中的資訊，將篩選器套用至別名物件。

特殊變數 `$`\_ 代表要傳遞的物件。`$_` 變數是由命令介面自動初始化，並繫結至目前的管線物件。如需此特殊變數的詳細資訊，請參閱[殼層變數](https://technet.microsoft.com/zh-tw/library/bb124036\(v=exchg.150\))。

使用標準的「點」表示法 (object.property)，會新增 `Definition` 內容，來定義要評估之物件的確實內容。然後，`-eq` 比較運算子會將此內容的值與 `"Clear-Host"` 相比較。唯有含符合此準則的 `Definition` 內容的物件，才會傳遞至主控台視窗上，以進行輸出。如需比較運算子的詳細資訊，請參閱[比較運算子](https://technet.microsoft.com/zh-tw/library/bb125229\(v=exchg.150\))。

在 **Where** 命令已篩選由 **Get-Alias** Cmdlet 傳回的物件之後，您可以將篩選物件以管線傳遞到另一個命令。下一個命令僅處理由 Where 命令傳回的篩選物件。


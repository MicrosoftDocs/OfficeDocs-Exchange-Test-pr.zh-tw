---
title: 'Cmdlet 延伸代理程式: Exchange 2013 Help'
TOCTitle: Cmdlet 延伸代理程式
ms:assetid: 0257790d-3988-46c3-8882-25ca11559e84
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335054(v=EXCHG.150)
ms:contentKeyID: 50553926
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cmdlet 延伸代理程式

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

Cmdlet 延伸代理程式是在 Cmdlet 執行時，由 Exchange Server 2013 Cmdlet 叫用的 Microsoft Exchange 2013 中的元件。顧名思義，Cmdlet 延伸代理程式會透過協助處理資料或根據 Cmdlet 的需求執行其他動作，來延伸叫用它們之 Cmdlet 的功能。Cmdlet 延伸代理程式適用於任何伺服器角色。

代理程式可以修改、取代或擴充 Exchange 管理命令介面 Cmdlet 的功能。代理程式可以提供命令沒有提供之必要參數的值、覆寫使用者提供的值、在 Cmdlet 執行時於 Cmdlet 工作流程外執行其他動作等等。

例如，**New-Mailbox** Cmdlet 會接受指定信箱資料庫建立新信箱的 *Database* 參數。在 Microsoft Exchange Server 2007 中，當您執行 **New-Mailbox** Cmdlet 時，如果沒有指定 *Database* 參數，命令就會失敗。但是在 Exchange 2013 中，當 Cmdlet 執行時，**New-Mailbox** Cmdlet 會叫用 `Mailbox Resources Management` 代理程式。如果未指定 *Database* 參數，`Mailbox Resources Management` 代理程式會自動決定適合建立新信箱的信箱資料庫，並將該值插入 *Database* 參數中。

Cmdlet 延伸代理程式只能由 Exchange 2013 與 Microsoft Exchange Server 2010 Cmdlet 叫用。Exchange 2007 Cmdlet 以及其他 Microsoft 與協力廠商所提供的 Cmdlet 則無法叫用 Cmdlet 延伸代理程式。指令碼也無法直接叫用 Cmdlet 延伸代理程式。不過，如果指令碼包含 Exchange 2013 Cmdlet，則這些 Cmdlet 可繼續呼叫 Cmdlet 延伸代理程式。

要尋找與 Cmdlet 延伸代理程式相關的管理工作嗎？請參閱[管理指令程式延伸代理程式](manage-cmdlet-extension-agents-exchange-2013-help.md)。

## 代理程式優先順序

代理程式的優先順序會決定 Cmdlet 執行時叫用代理程序的順序。優先順序較高 (較接近零) 的代理程式會先被叫用。當兩個或多個代理程式嘗試設定相同內容的值時，代理程式的優先順序就變得很重要。嘗試設定內容值時優先順序最高的代理程式會成功，優先順序較低的代理程式對設定相同內容的所有後續嘗試會被忽略。例如，如果優先順序為 3 的代理程式修改了物件的 **Name** 內容，而另一個優先順序為 6 的代理程式修改相同物件，則優先順序為 6 的代理程式所做的修改會被忽略。

如果想要使用 `Scripting agent` 設定可能由其他優先順序較高之代理程式設定的內容值，您可以選擇下列方法：

  - 停用目前設定該內容的代理程式。

  - 將 `Scripting agent` 的優先順序設定為高於要取代的現有代理程式。

  - 讓代理程式的優先順序保持不變，並確定 `Scripting agent` 下執行的指令碼採用其他代理程式提供的值。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>變更內建代理程式的優先順序或取代其功能是進階作業。請確定您完全了解所要進行的變更。</td>
</tr>
</tbody>
</table>


如需變更代理程式優先順序的詳細資訊，請參閱[管理指令程式延伸代理程式](manage-cmdlet-extension-agents-exchange-2013-help.md)。

## 內建的代理程式

Exchange 2013 包括可在 Cmdlet 執行時叫用的數個代理程式。下表列出代理程式、其順序以及代理程式預設是否啟用。您無法向執行 Exchange 2013 的伺服器新增或移除代理程式。但是您可使用 `Scripting agent` 來執行 Windows PowerShell 指令碼，以延伸使用此代理程式之 Cmdlet 的功能。如需`Scripting agent`的詳細資訊，請參閱本主題稍後的＜指令碼處理代理程式＞一節。

如果您想使用以`Scripting agent`呼叫之自訂指令碼中所提供的功能來取代特定代理程式的功能，您可以啟用或停用大部分的代理程式，或是變更代理程式的優先順序。但是，某些代理程式無法停用。無法停用的代理程式稱為*系統代理程式*，其 *IsSystem* 內容設為 `$True`。下表提供關於 Exchange 2013 Cmdlet 延伸代理程式的資訊，包括系統代理程式在內。

代理程式的設定會儲存在組織層級。啟用或停用代理程式或設定其優先順序時，您可以跨組織中的每個伺服器來設定該代理程式的設定。將指令碼新增至 `Scripting agent` 則是例外狀況。您必須個別更新每個伺服器上的指令碼。如需設定指令碼以使用`Scripting agent`的詳細資訊，請參閱本主題稍後的＜指令碼處理代理程式＞一節。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您沒有完全了解每個代理程式的功能以及它們與 Exchange Cmdlet 互動的方式，變更代理程式的優先順序，或者啟用或停用代理程式可能會造成無法預期的結果。在您變更任何代理程式的設定之前，請確定您完全了解您想要的變更與結果，並確認您的自訂指令碼會如預期般運作。</td>
</tr>
</tbody>
</table>


### Exchange 2013 Cmdlet 延伸代理程式

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>代理程式名稱</th>
<th>優先順序</th>
<th>預設啟用</th>
<th>系統代理程式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Admin Audit Log agent</code></p></td>
<td><p>255</p></td>
<td><p>True</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><code>Scripting agent</code></p></td>
<td><p>6</p></td>
<td><p>False</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Resources Management agent</code></p></td>
<td><p>5</p></td>
<td><p>True</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><code>OAB Resources Management agent</code></p></td>
<td><p>4</p></td>
<td><p>True</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p><code>Query Base DN agent</code></p></td>
<td><p>3</p></td>
<td><p>True</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><code>Provisioning Policy agent</code></p></td>
<td><p>2</p></td>
<td><p>True</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p><code>Rus agent</code></p></td>
<td><p>1</p></td>
<td><p>True</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Creation Time agent</code></p></td>
<td><p>0</p></td>
<td><p>True</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


## 指令碼處理代理程式

您可以使用 Exchange 2013 中的 `Scripting agent` Cmdlet 延伸代理程式將您自己的指令碼處理邏輯插入 Exchange Cmdlet 的執行中。使用 `Scripting agent`，您可以新增條件、覆寫值，以及設定報告。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您啟用 <code>Scripting agent</code> Cmdlet 延伸代理程式時，每當在執行 Exchange 2013 的伺服器上執行 Cmdlet 時，就會叫用該代理程式。這不只包含您在 Exchange 管理命令介面中直接執行的 Cmdlet，也包含由 Exchange 服務和 Exchange 系統管理中心 (EAC) 執行的 Cmdlet。我們強烈建議您在將更新的組態檔複製到 Exchange 2013 Server 並啟用 <code>Scripting agent</code> Cmdlet 延伸代理程式之前，先測試您的指令碼及您對組態檔所做的任何變更，</td>
</tr>
</tbody>
</table>


每次當 Exchange Cmdlet 執行時，該 Cmdlet 都會叫用 `Scripting agent` Cmdlet 延伸代理程式。當叫用此代理程式時，該 Cmdlet 會檢查 Cmdlet 是否設定叫用任何指令碼。如果應該針對 Cmdlet 執行指令碼，該 Cmdlet 會嘗試叫用指令碼中定義的任何 API。下列 API 可以使用，而且是以下列順序叫用：

1.  **ProvisionDefaultProperties**   此 API 可用來在物件建立時，設定物件上的內容值。當您設定值時，該值會傳回給 Cmdlet，而且該 Cmdlet 會在內容上設定該值。如果使用者未指定值，您可以在內容上填入值，或者也可以覆寫由使用者指定的值。此 API 會採用較高優先順序代理程式所設定的值。`Scripting agent` Cmdlet 延伸代理程式不會覆寫由較高優先順序代理程式設定的值。

2.  **UpdateAffectedIConfigurable**   當所有其他處理皆已完成，但尚未叫用 `Validate` API 時，此 API 可用來傳送物件上的內容值。此 API 會採用較高優先順序代理程式所設定的值。`Scripting agent` Cmdlet 延伸代理程式不會覆寫由較高優先順序代理程式設定的值。

3.  **Validate**   此 API 可用來驗證物件內容上要由 Cmdlet 設定的值。在 Cmdlet 寫入任何資料之前，即呼叫此 API。您可以設定允許 Cmdlet 成功或失敗的驗證檢查。如果 Cmdlet 通過此 API 中的驗證檢查，該 Cmdlet 即可寫入資料。如果 Cmdlet 的驗證檢查失敗，它會傳回此 API 中定義的任何錯誤。

4.  **OnComplete**   當所有 Cmdlet 處理皆完成時，會使用此 API。它可以用來執行處理後的工作，例如將資料寫入外部資料庫。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當具有 <code>Get</code> 動詞的 Cmdlet 執行時，則不會呼叫 <code>Scripting agent</code> 延伸代理程式。</td>
</tr>
</tbody>
</table>


## 指令碼處理代理程式組態檔

`Scripting agent` 組態檔中包含您想要 `Scripting agent` 執行的所有指令碼。組態檔中的指令碼是包含在 XML 標記內；XML 標記用來定義指令碼的開始與結束，以及傳遞資料至指令碼所需的各種輸入參數。指令碼是以 Windows PowerShell 語法撰寫。組態檔是一個 XML 檔，使用下表中的元素或屬性。

### 指令碼處理代理程式組態檔的屬性

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>屬性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Configuration</code></p></td>
<td><p>不適用</p></td>
<td><p>此元素包含 <code>Scripting agent</code> Cmdlet 延伸代理程式可以執行的所有指令碼。<code>Feature</code> 標記是此標記的子系。</p>
<p>組態檔中只有一個 <code>Configuration</code> 標記。</p></td>
</tr>
<tr class="even">
<td><p><code>Feature</code></p></td>
<td><p>不適用</p></td>
<td><p>此元素包含與功能相關的一組指令碼。每個指令碼 (於 <code>ApiCall</code> 子系標記中定義) 都延伸 Cmdlet 執行管線的一個特定部分。此標記包含 <code>Name</code> 和 <code>Cmdlets</code> 屬性。</p>
<p>在 <code>Feature</code> 標記之下可以有多個 <code>Configuration</code> 標記。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>此屬性包含功能的名稱。使用此屬性可協助識別哪一個功能是由標記中所含之指令碼所延伸的。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Cmdlets</code></p></td>
<td><p>此屬性包含 Exchange Cmdlet 的清單 (此功能延伸中的一組指令碼會使用這些 Cmdlet)。您可以使用分號分隔每個 Cmdlet 來指定多個 Cmdlet。</p></td>
</tr>
<tr class="odd">
<td><p><code>ApiCall</code></p></td>
<td><p>不適用</p></td>
<td><p>此元素包含可延伸 Cmdlet 一部分執行管線的指令碼。每個指令碼是由其所延伸之 Cmdlet 執行管線中的 API 呼叫名稱所定義。下列為可延伸的 API 名稱：</p>
<ul>
<li><p><code>ProvisionDefaultProperties</code></p></li>
<li><p><code>UpdateAffectedIConfigurable</code></p></li>
<li><p><code>Validate</code></p></li>
<li><p><code>OnComplete</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>此屬性包含延伸 Cmdlet 執行管線之 API 呼叫的名稱。</p></td>
</tr>
<tr class="odd">
<td><p><code>Common</code></p></td>
<td><p>不適用</p></td>
<td><p>此元素包含組態檔中之任何指令碼可使用的功能。</p></td>
</tr>
</tbody>
</table>


每個 Exchange 2013 Server 都在 \<*installation path*\>\\V15\\Bin\\CmdletExtensionAgents 資料夾中包含 ScriptingAgentConfig.xml.sample 檔案。如果您啟用 Scripting Agent Cmdlet 延伸代理程式，則每個 Exchange 2013 Server 上的這個檔案都必須重新命名為 ScriptingAgentConfig.xml。範例組態檔包含可用來協助了解如何新增指令碼至組態檔的範例指令碼。

當您新增指令碼至組態檔後，或者對組態檔做了變更，必須更新組織中每個 Exchange 2013 Server 上的的檔案。此工作必須執行，以確保每個伺服器皆包含 `Scripting Agent` Cmdlet 延伸代理程式執行的最新版本指令碼。

通常在指令碼中使用的某些字元，在 XML 中也具有特殊意義。若要在指令碼中使用那些字元，請使用逸出序列。例如，下列字元使用逸出序列：

  - 請使用 `>` 來代替大於符號 ( `>` )。

  - 請使用 `$lt;` 來代替小於符號 ( `<` )。

  - 請使用 `&` 來代替 & 符號 ( `&` )。

## 啟用指令碼處理代理程式

`Scripting agent` Cmdlet 延伸代理程式預設是停用的。當您啟用 `Scripting agent` 時，整個 Exchange 2013組織都會啟用此代理程式。在啟用 `Scripting agent` 之前，請確認 `Scripting agent` 組態檔已正確重新命名並與您在每部 Exchange 2013 Server 上的指令碼一起更新。如果您未正確重新命名組態檔或從另一部 Exchange 2013 Server 將組態檔複製到此電腦上，則每當執行 Cmdlet 時，您都會收到一則錯誤訊息。

若要啟用 `Scripting agent`，您必須執行下列操作：

1.  在組織中的每個 Exchange 2013 Server 上，將 **\<安裝路徑\>\\V15\\Bin\\CmdletExtensionAgents** 中的ScriptingAgentConfig.xml.sample 檔案重新命名為 ScriptingAgentConfig.xml。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以將組態檔從一個 Exchange 2013 Server 複製到其他 Exchange 2013Server。複製之前，請確定更新要複製的組態檔。</td>
    </tr>
    </tbody>
    </table>


2.  將您的指令碼新增至組織中每個 Exchange 2013 Server 上已重新命名的組態檔。

3.  啟用 `Scripting agent` 延伸代理程式。如需啟用 Cmdlet 延伸代理程式的詳細資訊，請參閱[管理指令程式延伸代理程式](manage-cmdlet-extension-agents-exchange-2013-help.md)。

## 指令碼處理代理程式的優先順序

根據預設，`Scripting agent` Cmdlet 延伸代理程式會在其他每個代理程式之後執行，但 `Scripting agent` 代理程式除外。如果要以您建立的指令碼取代現有代理程式，必須停用其他代理程式或變更每個代理程式的優先順序，以便讓 `Scripting agent` Cmdlet 延伸代理程式先執行。如需關於如何停用或變更代理程式優先順序的詳細資訊，請參閱[管理指令程式延伸代理程式](manage-cmdlet-extension-agents-exchange-2013-help.md)。


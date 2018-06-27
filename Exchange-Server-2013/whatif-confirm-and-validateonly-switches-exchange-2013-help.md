---
title: 'WhatIf、Confirm 及 ValidateOnly 參數: Exchange 2013 Help'
TOCTitle: WhatIf、Confirm 及 ValidateOnly 參數
ms:assetid: a850eea7-431e-49c5-b877-1ebde2a2b48f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124088(v=EXCHG.150)
ms:contentKeyID: 50473932
ms.date: 03/28/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# WhatIf、Confirm 及 ValidateOnly 參數

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-04_

Both experienced administrators and script writers, and administrators who are new to Exchange and scripting, can benefit from using the *WhatIf*, *Confirm*, and *ValidateOnly* switches. These switches let you control how your commands run and indicate exactly what a command will do before it affects data. This functionality is quite valuable as you transition from your test environment into your production environment and as you roll out new scripts or commands.

The *WhatIf*, *Confirm*, and *ValidateOnly* switches are especially useful when you use them with commands that modify objects that are returned by using a filter or by using a **Get** command in a pipeline. This topic describes each switch and also provides an example command for each switch.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>If you want to use the <em>WhatIf</em>, <em>Confirm</em>, and <em>ValidateOnly</em> switches with commands in a script, you must add the appropriate switch to each command in the script, and not on the command line that calls the script.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>WhatIf</em>, <em>Confirm</em>, and <em>ValidateOnly</em> are called switch parameters. For more information about switch parameters, see <a href="https://technet.microsoft.com/zh-tw/library/bb124388(v=exchg.150)">參數</a>.</td>
</tr>
</tbody>
</table>


## WhatIf switch

The *WhatIf* switch instructs the command to which it is applied to run but only to display the objects that would be affected by running the command and what changes would be made to those objects. The switch does not actually change any of those objects. When you use the *WhatIf* switch, you can see whether the changes that would be made to those objects match your expectations, without the worry of modifying those objects.

When you run a command together with the *WhatIf* switch, you put the *WhatIf* switch at the end of the command, as in the following example:

    New-AcceptedDomain -Name "Contoso Domain" -DomainName "contoso.com" -WhatIf 

When you run this example command, the following text is returned by the Shell:

    What if: Creating Accepted Domain "Contoso Domain" with domain name "contoso.com".

## Confirm switch

The *Confirm* switch instructs the command to which it is applied to stop processing before any changes are made. The command then prompts you to acknowledge each action before it continues. When you use the *Confirm* switch, you can step through changes to objects to make sure that changes are made only to the specific objects that you want to change. This functionality is useful when you apply changes to many objects and want precise control over the operation of the Shell. A confirmation prompt is displayed for each object before the Shell modifies the object.

By default, the Shell automatically applies the *Confirm* switch to cmdlets that have the following verbs:

  - **Clear**

  - **Disable**

  - **Dismount**

  - **Move**

  - **Remove**

  - **Stop**

  - **Suspend**

  - **Uninstall**

When a cmdlet runs that has any of these verbs, the Shell automatically stops the command and waits for your acknowledgement before it continues to process.

If you want to manually apply the *Confirm* switch to a command, include the *Confirm* switch at the end of the command, as in the following example:

    Get-JournalRule | Enable-JournalRule -Confirm

When you run this example command, the following confirmation prompt is returned by the Shell:

    Confirm
    Are you sure you want to perform this action?
    Enabling journal rule "Litigation Journal Rule".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
    (default is "Y"):

The confirmation prompt gives you the following choices:

  - **\[Y\] Yes**   Type **Y** to instruct the command to continue the operation. The next operation will present another confirmation prompt. `[Y] Yes` is the default choice.

  - **\[A\] Yes to All**   Type **A** to instruct the command to continue the operation and all subsequent operations. You will not receive additional confirmation prompts for the duration of this command.

  - **\[N\] No**   Type **N** to instruct the command to skip this operation and continue with the next operation. The next operation will present another confirmation prompt.

  - **\[L\] No to All**   Type **L** to instruct the command to skip this operation and all subsequent operations.

  - **\[S\] Suspend**   Type **S** to pause the current pipeline and return to the command line. Type **Exit** to resume the pipeline.

  - **\[?\] Help**   Type **?** to display confirmation prompt Help on the command line.

If you want to override the default behavior of the Shell and suppress the confirmation prompt for cmdlets on which it is automatically applied, you can include the *Confirm* switch with a value of `$False`, as in the following example:

    Get-JournalRule | Disable-JournalRule -Confirm:$False

In this case, no confirmation prompt is displayed.

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>The default value of the <em>Confirm</em> switch is <code>$True</code>. The default behavior of the Shell is to automatically display a confirmation prompt. If you suppress this default behavior, you instruct the command to suppress all confirmation prompts for the duration of that command. The command will process all objects that meet the criteria for the command without confirmation.</td>
</tr>
</tbody>
</table>


## ValidateOnly switch

The *ValidateOnly* switch instructs the command to which it is applied to evaluate all the conditions and requirements that are needed to perform the operation before you apply any changes. The *ValidateOnly* switch is available on cmdlets that may take a long time to run, have several dependencies on multiple systems, or affect critical data, such as mailboxes.

When you apply the *ValidateOnly* switch to a command, the command runs through the whole process. The command performs each action as it would without the *ValidateOnly* switch. But the command doesn't change any objects. When the command completes its process, it displays a summary with the results of the validation. If the validation indicates that the command was successful, you can run the command again without the *ValidateOnly* switch.

When you run a command together with the *ValidateOnly* switch, you put the *ValidateOnly* switch at the end of the command.


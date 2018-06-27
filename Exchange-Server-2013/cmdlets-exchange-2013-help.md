---
title: '指令程式: Exchange 2013 Help'
TOCTitle: 指令程式
ms:assetid: 1d741dea-1eb8-4909-850f-63d4efaa1a32
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996589(v=EXCHG.150)
ms:contentKeyID: 50472772
ms.date: 03/28/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 指令程式

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

A *cmdlet*, pronounced "command-let", is the smallest unit of functionality in the Exchange Management Shell. Cmdlets resemble built-in commands in other shells, for example, the `dir` command found in `cmd.exe`. Like these familiar commands, cmdlets can be called directly from the command line in the Shell and run under the context of the Shell, not as a separate process.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Since Microsoft Exchange Server 2007, there have been changes to how Exchange 2013 uses cmdlets internally due to the use of Windows PowerShell remoting functionality. These changes have little to no impact on how you need to use cmdlets, but they may offer additional flexibility in how you manage your Exchange servers.</td>
</tr>
</tbody>
</table>


Cmdlets are usually designed around repetitive administrative tasks, and, in the Shell, several hundred cmdlets are provided for Exchange-specific management tasks. These cmdlets are available in addition to the non-Exchange system cmdlets included in the basic Windows PowerShell shell design. For information about how to open the Exchange Management Shell, see [開啟命令介面。](https://technet.microsoft.com/zh-tw/library/dd638134\(v=exchg.150\)).

All cmdlets in the Shell are presented in verb-noun pairs. The verb-noun pair is always separated by a hyphen (-) without spaces, and the cmdlet nouns are always singular. Verbs refer to the action that the cmdlet takes. Nouns refer to the object on which the cmdlet takes action. For example, in the **Get-SystemMessage** cmdlet, the verb is **Get**, and the noun is **SystemMessage**. All Shell cmdlets that manage a specific feature share the same noun. The following table provides examples of some verbs available in the Shell.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>By default, if the verb is omitted, the Shell assumes the <strong>Get</strong> verb. For example, when you call <strong>Mailbox</strong>, you retrieve the same results as when you call <strong>Get-Mailbox</strong>.</td>
</tr>
</tbody>
</table>


### Examples of verbs in the Exchange Management Shell

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Verb</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Disable</strong></p></td>
<td><p><strong>Disable</strong> cmdlets set the <code>Enabled</code> status of the specified Exchange object to <code>$False</code>. This prevents the object from processing data even though the object exists.</p></td>
</tr>
<tr class="even">
<td><p><strong>Enable</strong></p></td>
<td><p><strong>Enable</strong> cmdlets set the Enabled status of the specified Exchange object to <code>$True</code>. This enables the object to process data.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get</strong></p></td>
<td><p><strong>Get</strong> cmdlets retrieve information about a specific Exchange object.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Most <strong>Get</strong> cmdlets only return summary information when you run them. To tell the <strong>Get</strong> cmdlet to return verbose information when you run a command, pipe the command to the <strong>Format-List</strong> cmdlet. For more information about the <strong>Format-List</strong> command, see <a href="working-with-command-output-exchange-2013-help.md">使用命令輸出</a>. For more information about pipelining, see <a href="https://technet.microsoft.com/zh-tw/library/aa998260(v=exchg.150)">管線</a>.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><strong>Install</strong></p></td>
<td><p><strong>Install</strong> cmdlets install a new object or feature on an Exchange server.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Move</strong></p></td>
<td><p><strong>Move</strong> cmdlets relocate the specified Exchange object from one container or server to another.</p></td>
</tr>
<tr class="even">
<td><p><strong>New</strong></p></td>
<td><p><strong>New</strong> cmdlets create new Exchange object.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Remove</strong></p></td>
<td><p><strong>Remove</strong> cmdlets delete the specified Exchange object.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set</strong></p></td>
<td><p><strong>Set</strong> cmdlets modify the properties of an existing Exchange object.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Test</strong></p></td>
<td><p><strong>Test</strong> cmdlets test specific Exchange components and provide log files that you can examine.</p></td>
</tr>
<tr class="even">
<td><p><strong>Uninstall</strong></p></td>
<td><p><strong>Uninstall</strong> cmdlets remove an object or feature from an Exchange server.</p></td>
</tr>
</tbody>
</table>


The following list of cmdlets is an example of a complete cmdlet set. This cmdlet set is used to manage the delivery status notification (DSN) message and mailbox quota message features of Exchange 2013:

  - **Get-SystemMessage**

  - **New-SystemMessage**

  - **Remove-SystemMessage**

  - **Set-SystemMessage**


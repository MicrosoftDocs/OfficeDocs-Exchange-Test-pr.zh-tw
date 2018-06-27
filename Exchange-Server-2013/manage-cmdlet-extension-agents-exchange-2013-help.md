---
title: '管理指令程式延伸代理程式: Exchange 2013 Help'
TOCTitle: 管理指令程式延伸代理程式
ms:assetid: 9141b3cb-ad13-4415-be2f-aa89f91445f5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298143(v=EXCHG.150)
ms:contentKeyID: 50554031
ms.date: 03/28/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理指令程式延伸代理程式

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-19_

This topic shows you how to enable, disable, view, and change the priority of cmdlet extension agents in Microsoft Exchange Server 2013. For more information about cmdlet extension agents in Exchange 2013, see [Cmdlet 延伸代理程式](cmdlet-extension-agents-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: less than 5 minutes

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 "Cmdlet extension agents" entry in the [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) topic.

  - Before you enable the `Scripting Agent`, you must verify that it's configured correctly. For more information about the `Scripting Agent`, see [Cmdlet 延伸代理程式](cmdlet-extension-agents-exchange-2013-help.md).

  - You must use the Shell to perform these procedures.

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


## What do you want to do?

## Enable a cmdlet extension agent

When you enable a cmdlet extension agent in Exchange 2013, the agent is run on every server running Exchange 2013 in the organization. When an agent is enabled, it's made available to cmdlets, which can then use the agent to perform additional operations.

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Before you enable an agent, be sure that you're aware of how the agent works and what impact the agent will have on your organization.</td>
</tr>
</tbody>
</table>


This example enables a cmdlet extension agent by using the **Enable-CmdletExtensionAgent** cmdlet. You must specify the name of the agent you want to enable when you run the cmdlet. Before you enable the `Scripting Agent`, you need to make sure that you've deployed the `ScriptingAgentConfig.xml` configuration file to all the servers in your organization. If you don't deploy the configuration file first and you enable the `Scripting ``Agent`, all non-**Get** cmdlets fail when they're run. This example enables the `Scripting Agent`.

    Enable-CmdletExtensionAgent "Scripting Agent"

For detailed syntax and parameter information, see [Enable-CmdletExtensionAgent](https://technet.microsoft.com/zh-tw/library/dd335192\(v=exchg.150\)).

## Disable a cmdlet extension agent

When you disable a cmdlet extension agent in Exchange 2013, the agent is disabled on every server running Exchange 2013 in the organization. When an agent is disabled, it's not made available to cmdlets. Cmdlets can no longer use the agent to perform additional operations.

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Before you disable an agent, be sure that you're aware of how the agent works and what impact disabling the agent will have on your organization.</td>
</tr>
</tbody>
</table>


To disable a cmdlet extension agent, use the **Disable-CmdletExtensionAgent** cmdlet. Specify the name of the agent you want to disable when you run the cmdlet. This example disables the `Scripting Agent`.

    Disable-CmdletExtensionAgent "Scripting Agent"

For detailed syntax and parameter information, see [Disable-CmdletExtensionAgent](https://technet.microsoft.com/zh-tw/library/dd298132\(v=exchg.150\)).

## View existing cmdlet extension agents

Viewing cmdlet extension agents enables you to see which agents are run first and which agents are enabled in an Exchange 2013 organization. For more information about pipelining and the **Format-Table** cmdlet, see the following topics:

  - [管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))

  - [使用命令輸出](working-with-command-output-exchange-2013-help.md)

This example gets the details of a specific cmdlet extension agent by using the **Get-CmdletExtensionAgent** cmdlet. In this example, the details of the `Mailbox Permissions Agent` are returned.

    Get-CmdletExtensionAgent "Mailbox Permissions Agent"

This example gets multiple cmdlet extension agents by using the **Get-CmdletExtensionAgent** cmdlet, and then pipes the output to the **Format-Table** cmdlet. This example displays a list of all of the cmdlet extension agents in the organization, and by using the **Format-Table** cmdlet, the **Name**, **Enabled**, and **Priority** properties of each agent are displayed in a table.

    Get-CmdletExtensionAgent | Format-Table Name, Enabled, Priority

For detailed syntax and parameter information, see [Get-CmdletExtensionAgent](https://technet.microsoft.com/zh-tw/library/dd297946\(v=exchg.150\)).

## Change the priority of a cmdlet extension agent

The ability to change the priority of a cmdlet extension agent in Exchange 2013 is useful when you want a certain agent to be called by a cmdlet before another agent. This is especially useful if you create a custom script that's run in the `Scripting Agent`, and you want that script to take precedence over a built-in agent. For more information about the `Scripting Agent`, see [Cmdlet 延伸代理程式](cmdlet-extension-agents-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Changing the priority or replacing the functionality of a built-in agent is an advanced operation. Be sure that you completely understand the changes you're making.</td>
</tr>
</tbody>
</table>


Agents are ordered from zero to the maximum number of agents. The closer to zero the agent is, the higher the priority of the agent. Agents with a higher priority are called first. For more information about agent priorities, see [Cmdlet 延伸代理程式](cmdlet-extension-agents-exchange-2013-help.md).

This example changes the priority of a cmdlet extension agent by using the **Set-CmdletExtensionAgent** cmdlet. In this example, the priority of the `Scripting Agent` is changed to 3.

    Set-CmdletExtensionAgent "Scripting Agent" -Priority 3

For detailed syntax and parameter information, see [Set-CmdletExtensionAgent](https://technet.microsoft.com/zh-tw/library/dd335175\(v=exchg.150\)).


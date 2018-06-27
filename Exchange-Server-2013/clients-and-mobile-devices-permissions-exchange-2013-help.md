---
title: '用戶端和行動裝置權限: Exchange 2013 Help'
TOCTitle: 用戶端和行動裝置權限
ms:assetid: 57eca42a-5a7f-4c65-89f0-7a84f2dbea19
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638131(v=EXCHG.150)
ms:contentKeyID: 50473245
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 用戶端和行動裝置權限

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-11-10_

執行用戶端與行動裝置工作所需的權限，因所執行的程序或您要執行的指令程式而異。如需用戶端和行動裝置功能的詳細資訊，請參閱[用戶端和行動裝置](clients-and-mobile-exchange-2013-help.md)。

若要瞭解執行程序或執行 Cmdlet 所需的權限，請執行以下操作：

1.  在下表中，尋找與您想要執行的程序或 Cmdlet 最為相關的功能。

2.  接著查看功能所需的權限。您必須獲指派其中一個角色群組、相等的自訂角色群組，或相等的管理角色。您也可以按一下角色群組，查看其管理角色。如果功能列出多個角色群組，您只需要獲指派其中一個角色群組，就能使用功能。如需角色群組和管理角色的詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

3.  現在，執行 **Get-ManagementRoleAssignment** Cmdlet，查看指派給您的角色群組或管理角色，以瞭解您是否有管理該功能所需的權限。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您必須獲指派「角色管理」管理角色，才能執行 <strong>Get-ManagementRoleAssignment</strong> Cmdlet。如果您沒有執行 <strong>Get-ManagementRoleAssignment</strong> Cmdlet 的權限，請詢問您的 Exchange 系統管理員，以取得角色群組或是獲指派管理角色。</td>
    </tr>
    </tbody>
    </table>


如果您要將管理功能的能力委派給另一個使用者，請參閱[委派角色指派](delegate-role-assignments-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>某些功能可能會要求您在要管理的伺服器上具備本機系統管理員權限。若要管理這些功能，您必須是該伺服器上本機系統管理員群組的成員。</td>
</tr>
</tbody>
</table>


## Client Access Server 權限

您可以為用戶端存取伺服器設定下列任何一個功能。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中功能的組態。如需詳細資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>必要的權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client Access Server 陣列設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>Client Access Server 設定</p></td>
<td><p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>用戶端存取服務電子郵件通道設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>用戶端存取使用者設定</p></td>
<td><p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>用戶端存取虛擬目錄設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>RPC 用戶端存取設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>通播通知 Proxy 設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>OAuth 驗證重新導向設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
</tbody>
</table>


## Exchange ActiveSync 權限

您可以為 Exchange ActiveSync 設定下列任何一項。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中功能的組態。如需詳細資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>必要的權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange ActiveSync 自動封鎖設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync 信箱原則設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync 伺服器設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync 設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync 使用者設定</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync 虛擬目錄設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>行動裝置信箱原則設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>行動裝置使用者設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
</tbody>
</table>


## 自動探索權限

您可以為自動探索服務設定下列項目。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中功能的組態。如需詳細資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>必要的權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>自動探索服務組態設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">委派安裝</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">檢疫管理</a></p></td>
</tr>
<tr class="even">
<td><p>自動探索虛擬目錄設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
</tbody>
</table>


## 可用性服務權限

您可以為可用性服務設定下列項目。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中功能的組態。如需詳細資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>必要的權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>可用性服務位址空間設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>可用性服務組態設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p></td>
</tr>
</tbody>
</table>


## 用戶端節流權限

您可以為用戶端節流設定下列項目。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中功能的組態。如需詳細資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>必要的權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>用戶端節流設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p></td>
</tr>
</tbody>
</table>


## Exchange Web 服務權限

您可以為 Web 服務虛擬目錄設定下列項目。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中功能的組態。如需詳細資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>必要的權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Web 服務虛擬目錄設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>測試 Exchange Web 服務</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>測試 Outlook Web 服務</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
</tbody>
</table>


## Outlook 無所不在權限

您可以為 Outlook 無所不在設定及管理下列設定。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中功能的組態。如需詳細資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>必要的權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 無所不在組態 (啟用、停用、變更、檢視)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">委派安裝</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">檢疫管理</a></p></td>
</tr>
<tr class="even">
<td><p>RPC over HTTP Proxy 元件</p></td>
<td><p>本機伺服器系統管理員</p></td>
</tr>
<tr class="odd">
<td><p>測試 Outlook 無所不在連線</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
</tbody>
</table>


## Outlook Web App 權限

您可以使用下列功能來檢視 Outlook Web App 設定、控制 Outlook Web App 安全性及使用者存取權，以及測試 Outlook Web App 連線。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中功能的組態。如需詳細資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>必要的權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>圖形編輯器</p></td>
<td><p>本機伺服器系統管理員</p></td>
</tr>
<tr class="even">
<td><p>IIS 管理員</p></td>
<td><p>本機伺服器系統管理員</p></td>
</tr>
<tr class="odd">
<td><p>ISA Server 2006</p></td>
<td><p>ISA Server 企業系統管理員</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App 信箱原則</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Outlook Web App 虛擬目錄</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>登錄編輯程式</p></td>
<td><p>本機伺服器系統管理員</p></td>
</tr>
<tr class="odd">
<td><p>S/MIME 組態</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>文字編輯器</p></td>
<td><p>本機伺服器系統管理員</p></td>
</tr>
<tr class="odd">
<td><p>檢視 Outlook Web App 信箱原則</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">委派安裝</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">檢疫管理</a></p></td>
</tr>
</tbody>
</table>


## POP3 及 IMAP4 權限

您可以為 POP3 及 IMAP4 設定下列項目。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中功能的組態。如需詳細資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>必要的權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IMAP4 設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>POP3 設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>測試 IMAP4 設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>測試 POP3 設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p></td>
</tr>
</tbody>
</table>


## Windows PowerShell 虛擬目錄權限

您可以為 Windows PowerShell 設定下列項目。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中功能的組態。如需詳細資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>必要的權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>測試 Windows PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>Windows PowerShell 設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
</tbody>
</table>


## 簡訊權限

您可以為簡訊設定下列項目。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中功能的組態。如需詳細資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>必要的權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>簡訊通知設定</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>簡訊設定</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>簡訊使用者設定</p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">MyTextMessaging 角色</a></p>
<p>使用者可以在自己的信箱上設定簡訊設定。系統管理員無法設定郵件另一位使用者的信箱上設定的文字。</p></td>
</tr>
</tbody>
</table>


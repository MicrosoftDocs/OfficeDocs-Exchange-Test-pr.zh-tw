---
title: '設定 Exchange 混合部署中支援委派的信箱權限: Exchange 2013 Help'
TOCTitle: 設定 Exchange 混合部署中支援委派的信箱權限
ms:assetid: a2a10cb3-4557-4ff5-8191-c653522f4512
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt784505(v=EXCHG.150)
ms:contentKeyID: 74447337
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Exchange 混合部署中支援委派的信箱權限

 

_<strong>上次修改主題的時間：</strong>2018-01-30_

委派的信箱權限可以讓其他人以管理其他使用者信箱的某些部分。常見的範例為行政助理需要管理 executive 信箱和行事曆。在內部部署 Exchange 組織與 Office 365 支援**完整存取權**與**代理傳送者**之間的混合式部署委派信箱權限。不過，視您已安裝在內部部署組織中的 Exchange 版本，可能需要先執行其他設定即可使用混合部署中使用委派的信箱權限。以下列出支援委派在混合部署中的信箱權限與該版本是否需要其他設定 Exchange 版本。

  - **Exchange 2016**需要進行其他設定。

  - **Exchange 2013**A 支援 Exchange 2013 累計更新 (CU) 及其他設定都是必要。

  - **Exchange 2010**支援的 Exchange 2010 的更新彙 (RU) 及其他設定都是必要。

如需以支援混合式部署中的委派的信箱權限的特定需求的詳細資訊，請[Exchange 混合式部署中的權限](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md)查看。

下列各節可讓您逐步設定 Exchange 2013 和 Exchange 2010 內部部署啟用支援的委派的信箱權限。請遵循下列步驟之前，您必須確定您是在最新的 Exchange 2013 CU 或 Exchange SP3 RU。如需詳細資訊，請參閱[混合部署必要條件](hybrid-deployment-prerequisites-exchange-2013-help.md)。

## Exchange 2013

您需要執行啟用支援的委派的信箱權限是根據幾個因素而定。如果信箱移至 Office 365 與該次：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>已安裝下列...]</th>
<th>與組織在 ACLable 物件同步處理已...]</th>
<th>然後您需要...]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU9 或更早版本</p></td>
<td><p>此功能並未提供 Exchange 2013 CU9 與舊版。</p></td>
<td><p>手動設定來支援 Acl 每個信箱</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU10 或更新版本</p></td>
<td><p>已停用</p></td>
<td><ol>
<li><p>讓組織層級的 ACLable 物件同步處理</p></li>
<li><p>手動啟用每個信箱移至 Office 365 之前 ACLable 物件同步處理已啟用組織層級上的 Acl。</p></li>
</ol>
<p>信箱移至 Office 365 組織層級啟用 ACLable 物件同步處理之後需要進行其他設定。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2013 CU10 或更新版本</p></td>
<td><p>已啟用</p></td>
<td><p>需要進行其他設定</p></td>
</tr>
</tbody>
</table>


## 啟用 ACLable 物件同步處理

若要啟用組織層級的 ACLable 物件同步處理，請執行下列動作。

1.  在所有的 AAD 連線伺服器上安裝最新版的 Azure Active Directory 連線 （AAD 連線）。這會需要以允許 AAD 連線同步處理支援混合式的權限所需的屬性。您可以從[Microsoft Azure Active Directory 連線](http://go.microsoft.com/fwlink/p/?linkid=510956)中下載 AAD 連線。

2.  開啟 Exchange 管理命令介面執行最新可用 Exchange 2013 CU 或前 CU 的伺服器上。

3.  執行下列命令。
    
        Set-OrganizationConfig -ACLableSyncedObjectEnabled $True

執行這項作業之後，請移至 Office 365 任何信箱會適當地設定為支援委派的信箱權限。如果信箱已移至 Office 365 在您完成這些步驟之前，必須以手動啟用 \[使用遠端信箱上的 \[啟用 Acl中的步驟這些信箱上的 Acl。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Acl 不在 Office 365 中建立的遠端信箱上啟用。如果您在 Office 365 中建立的遠端信箱，您需要在遠端信箱] 區段中啟用該遠端信箱上的 Acl 遵循啟用 Acl 中的步驟。若要避免此額外的步驟，我們建議您在內部部署 Exchange 伺服器上建立信箱並再將信箱移至 Office 365。</td>
</tr>
</tbody>
</table>


## 啟用遠端信箱上的 Acl

若要啟用信箱移至 Office 365 之前 ACLable 物件同步處理已啟用組織層級上的 Acl，執行下列動作。

1.  開啟 Exchange 管理命令介面執行最新可用 Exchange 2013 CU 或前 CU 的伺服器上。

2.  若要啟用單一信箱上的 Acl，請執行下列命令。
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  若要啟用所有的信箱移至 Office 365 上的 Acl，請執行下列命令。
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  若要確認信箱已成功更新，請執行下列命令。
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

## Exchange 2010

Exchange 2010 SP3 伺服器支援遠端信箱上的 Acl 的設定，不過，此設定需要手動設定每個信箱。與 Exchange 版本還要新，不同 Exchange 2010 不提供組織層級設定這項功能的能力。您必須遵循下列步驟及任何將會從 Exchange 2010 SP3 伺服器移至 Office 365 未來的信箱上任何您先前已移至 Office 365 的信箱。

## 啟用遠端信箱上的 Acl

若要啟用信箱移至 Office 365 上的 Acl，執行下列動作。

1.  開啟 Exchange 管理命令介面執行最新可用 Exchange 2010 SP3 RU 或前 RU 的伺服器上。

2.  若要啟用單一信箱上的 Acl，請執行下列命令。
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  若要啟用所有的信箱移至 Office 365 上的 Acl，請執行下列命令。
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  若要確認信箱已成功更新，請執行下列命令。
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}


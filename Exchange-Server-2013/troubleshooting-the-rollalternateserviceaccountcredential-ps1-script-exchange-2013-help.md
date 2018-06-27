---
title: '疑難排解 RollAlternateServiceAccountCredential.ps1 指令碼: Exchange 2013 Help'
TOCTitle: 疑難排解 RollAlternateServiceAccountCredential.ps1 指令碼
ms:assetid: 2bbf36d3-eb89-4f92-a8de-259a7cb64d62
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff808310(v=EXCHG.150)
ms:contentKeyID: 63913429
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 RollAlternateServiceAccountCredential.ps1 指令碼

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-01-14_

本主題提供解決方案和使用 RollAlternateServiceAccountPassword.ps1 指令碼時可能發生的常見錯誤的相關資訊。

## 一或多個用戶端存取伺服器無法更新的密碼

## 問題

當您使用參數*ToEntireForest*或*ToArrayMembers*指令碼，在某些情況下，一或多個用戶端存取伺服器可能不會更新。

## 解決方法

確認伺服器指令碼將所有需要的伺服器藉由使用目標**Get-ClientAccessArray**指令程式，如下列範例所示。

    Get-ClientAccessArray | fl members

如果更新失敗的伺服器的用戶端存取陣列成員與仍不會正確更新，請重新執行Exchange安裝程式並再次增加伺服器的用戶端存取伺服器角色。您也可以指定將目標放在使用參數*ToSpecificServers*的個別伺服器。

## 有些伺服器沒有回應的指令碼

## 問題

在某些情況下，伺服器可能無法更新因發生暫時性錯誤等不正確的網路連線。

## 解決方法

確認有問題的伺服器都具備網路和Active Directory連線，再試一次指令碼。

## 某些陣列成員會停止服務的一段時間

## 問題

如果伺服器超出較長的一段時間的旋轉角度但還是陣列成員由**Get-ClientAccessArray cmdlet**決定、 指令碼功能可能受損時使用的參數*ToArrayMembers*和*ToEntireForest*。如果伺服器有鎖永久失敗但尚未從您的部署完全移除就會發生同樣的問題。

## 解決方法

若要解決此問題，請使用Exchange安裝程式部署移除伺服器，或在手動模式中執行指令碼，直到可移除伺服器。

如果伺服器只會向下短時間，而且不想要永久移除Exchange，您可以調整對使用參數*ToSpecificServers*如此針對使用中的伺服器的特定伺服器執行的指令碼。或者，您可以移除 RPC Client Access 服務的非回應伺服器Active Directory物件使用**Remove-ClientAccessArray**指令程式，如下列範例所示。

    Remove-RPCClientAccess -Server Server.Contoso.com

已移除 RPC Client Access 服務之後，伺服器不會傳回陣列成員身分的[Get-ClientAccessArray](https://technet.microsoft.com/zh-tw/library/dd297976\(v=exchg.150\))並將指令碼將不會目標它。一旦伺服器是一次正常運作，您可以重新使用**New-RpcClientAccess**指令程式來新增 RPC Client Access 服務。當重新加入 RPC Client Access 服務時，請務必重新啟動受影響的伺服器上的 Microsoft Exchange 通訊錄服務。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>從伺服器移除 RPC Client Access 服務之前，請參閱主題<a href="https://technet.microsoft.com/zh-tw/library/dd298151(v=exchg.150)">Remove-RPCClientAccess</a>。</td>
</tr>
</tbody>
</table>


## 相關資訊

如需如何使用 Kerberos 驗證與 Client Access server 陣列或負載平衡解決方案的詳細資訊，請參閱下列主題：

  - [設定負載平衡的 Client Access server 的 Kerberos 驗證](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)

  - [在命令介面中使用 RollAlternateserviceAccountCredential.ps1 指令碼](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md)


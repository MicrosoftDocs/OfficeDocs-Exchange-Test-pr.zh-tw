---
title: '同盟信任之信任的根憑證授權: Exchange 2013 Help'
TOCTitle: 同盟信任之信任的根憑證授權
ms:assetid: d4224bf5-69b3-484c-8a70-4f230d3dbdd9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee332350(v=EXCHG.150)
ms:contentKeyID: 50474326
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 同盟信任之信任的根憑證授權

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-07-26_

若要建立同盟信任 Microsoft Exchange Server 2013組織和[Azure Active Directory 驗證系統](https://go.microsoft.com/fwlink/p/?linkid=135986)之間，您需要用來建立信任Exchange伺服器上安裝數位憑證。我們強烈建議使用自我簽署的憑證。建立及使用Exchange 系統管理中心 (EAC) 中的 \[**啟用同盟信任**\] 精靈時自動安裝的自我簽署的憑證。

如果您不想要使用建議的自我簽署的憑證，您應該要求並安裝 Microsoft 所信任的憑證授權單位 (CA) 的 X.509 Secure Sockets Layer (SSL) 憑證。其他 Ca 所發出的憑證也可以用來建立與Azure AD驗證系統的同盟信任，雖然它們不由 Microsoft 認證日期。

下表列出 Microsoft 目前信任的 CA。這些 CA 已通過測試可與 Exchange 2013 搭配使用。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>CA 易記名稱</th>
<th>發行者</th>
<th>使用目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="even">
<td><p>Comodo</p></td>
<td><p>Comodo Certification Authority</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="odd">
<td><p>CyberTrust</p></td>
<td><p>巴爾的摩 CyberTrust 根憑證授權單位</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="even">
<td><p>Digicert</p></td>
<td><p>Digicert Global Root Certification Authority</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="odd">
<td><p>Digicert High Assurance EV</p></td>
<td><p>Digicert Global Root Certification Authority</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="even">
<td><p>Entrust</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="odd">
<td><p>Entrust (2048)</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="even">
<td><p>Equifax</p></td>
<td><p>Equifax Secure Certification Authority</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="odd">
<td><p>GlobalSign</p></td>
<td><p>GlobalSign 憑證授權單位</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="even">
<td><p>Go Daddy</p></td>
<td><p>Go Daddy Class 2 Certification Authority</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="odd">
<td><p>Network Solutions</p></td>
<td><p>Network Solutions Certification Authority</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="even">
<td><p>PositiveSSL</p></td>
<td><p>Comodo Certification Authority</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="odd">
<td><p>SECOM</p></td>
<td><p>SECOM 信任系統憑證授權單位</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="even">
<td><p>UTN-UserFirst-Hardware</p></td>
<td><p>Comodo Certification Authority</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="odd">
<td><p>VeriSign</p></td>
<td><p>Class 3 Public Primary Certification Authority</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
<tr class="even">
<td><p>VeriSign</p></td>
<td><p>VeriSign Trust Network</p></td>
<td><p>伺服器驗證、用戶端驗證</p></td>
</tr>
</tbody>
</table>


如需「同盟」的憑證需求的相關資訊，請參閱[同盟](federation-exchange-2013-help.md)。


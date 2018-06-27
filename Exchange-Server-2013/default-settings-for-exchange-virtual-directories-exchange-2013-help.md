---
title: 'Exchange 虛擬目錄的預設設定: Exchange 2013 Help'
TOCTitle: Exchange 虛擬目錄的預設設定
ms:assetid: d2d89ce6-4721-4737-a325-fba5ad9422e0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg247612(v=EXCHG.150)
ms:contentKeyID: 52062598
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 虛擬目錄的預設設定

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

Exchange Server 2013自動會在安裝期間設定多個網際網路資訊服務 (IIS) 虛擬目錄。本主題包含預設 IIS 驗證設定與預設的用戶端存取和信箱伺服器的 Secure Sockets Layer (SSL) 設定的相關資訊。

## Client Access server

下表列出在獨立Exchange 2013用戶端存取伺服器上的預設設定。

### 預設 Client Access Server IIS 驗證和 SSL 設定

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>虛擬目錄</th>
<th>驗證方法</th>
<th>SSL 設定</th>
<th>管理方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>預設網站</p></td>
<td><ul>
<li><p>Anonymous</p></li>
</ul></td>
<td><ul>
<li><p>必要</p></li>
</ul></td>
<td><p>IIS 管理主控台</p></td>
</tr>
<tr class="even">
<td><p>aspnet_client</p></td>
<td><ul>
<li><p>匿名驗證</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>需要 128 位元加密</p></li>
</ul></td>
<td><p>IIS 管理主控台</p></td>
</tr>
<tr class="odd">
<td><p>自動探索</p></td>
<td><ul>
<li><p>匿名驗證</p></li>
<li><p>基本驗證</p></li>
<li><p>Windows 驗證</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>需要 128 位元加密</p></li>
</ul></td>
<td><p>Exchange 管理命令介面 (命令介面)</p></td>
</tr>
<tr class="even">
<td><p>ecp</p></td>
<td><ul>
<li><p>匿名驗證</p></li>
<li><p>基本驗證</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>需要 128 位元加密</p></li>
</ul></td>
<td><p>Exchange 系統管理中心 (EAC) 或命令介面</p></td>
</tr>
<tr class="odd">
<td><p>EWS</p></td>
<td><ul>
<li><p>匿名驗證</p></li>
<li><p>Windows 驗證</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>需要 128 位元加密</p></li>
</ul></td>
<td><p>命令介面</p></td>
</tr>
<tr class="even">
<td><p>Microsoft-Server-ActiveSync</p></td>
<td><ul>
<li><p>基本驗證</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>需要 128 位元加密</p></li>
</ul></td>
<td><p>EAC 或命令介面</p></td>
</tr>
<tr class="odd">
<td><p>OAB</p></td>
<td><ul>
<li><p>Windows 驗證</p></li>
</ul></td>
<td><ul>
<li><p>不需要</p></li>
</ul></td>
<td><p>EAC 或命令介面</p></td>
</tr>
<tr class="even">
<td><p>owa</p></td>
<td><ul>
<li><p>基本驗證</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>需要 128 位元加密</p></li>
</ul></td>
<td><p>EAC 或命令介面</p></td>
</tr>
<tr class="odd">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>匿名驗證</p></li>
</ul></td>
<td><ul>
<li><p>不需要</p></li>
</ul></td>
<td><p>命令介面</p></td>
</tr>
<tr class="even">
<td><p>Rpc</p></td>
<td><ul>
<li><p>基本驗證</p></li>
<li><p>Windows 驗證</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>需要 128 位元加密</p></li>
</ul></td>
<td><p>命令介面</p></td>
</tr>
<tr class="odd">
<td><p>RpcWithCert</p></td>
<td><p>所有驗證方法都預設為停用。</p></td>
<td><ul>
<li><p>必要</p></li>
</ul></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 信箱伺服器

下表列出在獨立Exchange 2013信箱伺服器上的預設設定。

### 預設信箱伺服器 IIS 驗證和 SSL 設定

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>虛擬目錄</th>
<th>驗證方法</th>
<th>SSL 設定</th>
<th>管理方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>預設網站</p></td>
<td><ul>
<li><p>匿名驗證</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>需要 128 位元加密</p></li>
</ul></td>
<td><p>此虛擬目錄無法由使用者設定。</p></td>
</tr>
<tr class="even">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>匿名驗證</p></li>
</ul></td>
<td><ul>
<li><p>不需要</p></li>
</ul></td>
<td><p>命令介面</p></td>
</tr>
</tbody>
</table>


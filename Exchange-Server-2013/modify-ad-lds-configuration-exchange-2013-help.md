---
title: '修改 AD LDS 組態: Exchange 2013 Help'
TOCTitle: 修改 AD LDS 組態
ms:assetid: 381f582c-15ec-43bc-b674-5399fad72c97
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997269(v=EXCHG.150)
ms:contentKeyID: 61180450
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 修改 AD LDS 組態

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

在您將 Edge Transport Server 訂閱至 Exchange 組織之前，您可以使用 **ConfigureAdam.ps1** 指令碼 (位於 $env:ExchangeInstallPath\\Scripts 中)，修改 Edge Transport Server 的預設 Active Directory 輕量型目錄服務 (AD LDS) 組態。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>ConfigureAdam.ps1</strong> 指令碼會呼叫 <strong>dsdbutil</strong> 命令，以變更 AD LDS 的登錄設定。<strong>dsdbutil</strong> 命令是專門提供給經驗豐富之系統管理員使用的 AD LDS 管理工具；若要變更 AD LDS 組態，建議您使用 <strong>ConfigureAdam.ps1</strong>。</td>
</tr>
</tbody>
</table>


下表列出可用於 **ConfigureAdam.ps1** 指令碼的參數。您可以使用其中一個參數、所有參數或其任意組合來修改 AD LDS。

### ConfigureAdam.ps1 指令碼的可用參數

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Ldapport</em></p></td>
<td><p>修改 LDAP 通訊所使用的連接埠。依預設，Edge Transport Server 會使用非標準的通訊埠 50389。</p></td>
</tr>
<tr class="even">
<td><p><em>Sslport</em></p></td>
<td><p>修改安全 LDAP 通訊所使用的連接埠。依預設，Edge Transport Server 會使用非標準的通訊埠 50636。</p></td>
</tr>
<tr class="odd">
<td><p><em>LogPath</em></p></td>
<td><p>修改記錄檔的位置。根據預設，Edge Transport Server 會在 %ExchangeInstallPath%Transport Roles\Data\adam 路徑中建立記錄檔</p></td>
</tr>
<tr class="even">
<td><p><em>DataPath</em></p></td>
<td><p>修改目錄資料庫檔案的位置。根據預設，Edge Transport Server 會將目錄資料庫儲存在 %ExchangeInstallPath%Transport Roles\Data\adam 路徑中</p></td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：五分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)中的「Edge Transport Server」一節。

  - 如果您需要對 Edge Transport Server 的 AD LDS 組態進行任何修改，請在 Edge Transport Server 訂閱至您的 Exchange 組織之前修改。如果您對已訂閱的 Edge Transport Server 修改了 AD LDS 組態，您就必須將 Edge Transport Server 重新訂閱至 Exchange 組織。

  - 請一律使用指令碼來修改登錄設定。以手動方式變更 AD LDS 組態的登錄設定，可能導致 AD LDS 執行個體無法使用。

  - 如果您必須修改 AD LDS 所使用的 LDAP 連接埠或 SSL 連接埠，請先確認沒有其他應用程式正在使用選取的連接埠。您可以使用 **netstat** 命令檢視 Edge Transport Server 正在使用的連接埠。

  - 您只能使用命令介面來執行此程序。

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


## 修改 Edge Transport Server 的 AD LDS 組態

此範例會將 AD LDS 所使用的 LDAP 連接埠變更為 5000。& 符號是命令語法的一部分。

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000

此範例會對 AD LDS 組態進行下列變更。& 符號是命令語法的一部分。請注意每個參數及其值之間所使用的冒號 (:)：

  - 將 LDAP 通訊埠變更為 5000

  - 將 SSL 連接埠變更為 500

  - 將記錄檔路徑變更為 D:\\Exchange Server\\Data\\ADLDS

  - 將資料路徑變更為 D:\\Exchange Server\\Data\\ADLDS

<!-- end list -->

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000 -SslPort:5001 -LogPath:"D:\Exchange Server\Data\ADLDS" -DataPath:"D:\Exchange Server\Data\ADLDS"


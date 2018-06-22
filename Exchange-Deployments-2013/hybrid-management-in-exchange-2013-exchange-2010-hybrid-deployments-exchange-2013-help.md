---
title: 'Exchange 2013/Exchange 2010 混合式部署中的混合式管理: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2010 混合式部署中的混合式管理
ms:assetid: 613ad2c2-bb7a-4810-b572-71945bd103f1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn393961(v=EXCHG.150)
ms:contentKeyID: 59634076
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2010 混合式部署中的混合式管理

本主題正在編輯中。  

_<strong>適用版本：</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>上次修改主題的時間：</strong>2016-12-09_

在 Exchange 2010 內部部署組織中安裝執行 Microsoft Exchange Server 2013 的伺服器時，系統會自動將 Exchange 2013 管理工具安裝在伺服器上。您將使用下列工具來設定與管理內部部署 Exchange 與 Exchange Online 組織的混合功能：

  - **Exchange 系統管理中心**   EAC 是 Exchange 2013 隨附的 Web 管理主控台，不僅易於使用，而且可針對內部部署、線上或混合 Exchange 部署最佳化。EAC 補強了 Exchange 管理主控台 (EMC) 和 Exchange 控制台 (ECP) 等 Exchange Server 2010 管理介面。

  - **Exchange 管理命令介面**Exchange 管理命令介面 是 Windows PowerShell 式的命令列介面。

## Exchange 系統管理中心

EAC 可讓您在內部部署 Exchange 伺服器與 Exchange Online 組織中，執行許多部署工作及最常見的日常系統管理工作。預設會在每一部 Exchange 2013 伺服器上安裝。此外，由於這是一個 Web 管理主控台，因此您還可以使用網路中其他電腦上的 Web 瀏覽器或透過網際網路使用 ECP 虛擬目錄 URL 來存取它。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果想要使用信箱位於 Exchange 2010 信箱伺服器上的帳戶 (如網域系統管理員帳戶) 來存取 EAC，則必須在瀏覽器中使用下列網址來存取 EAC：<br />
https://<em>&lt;FQDN of Exchange 2013 Client Access server&gt;</em>/ECP? ExchClientVer=15</td>
</tr>
</tbody>
</table>


您可以藉由選取 Office 365 \[跨單位導覽\] 索引標籤存取 EAC 中的 Exchange Online 組織。跨單位導覽可讓您在 Exchange Online 與內部部署 Exchange 組織之間輕鬆切換。如果您已設定混合式部署，則選取 \[Office 365\] 索引標籤可讓您管理 Exchange Online 組織和收件者物件。如果您沒有 Exchange Online 組織，則選取 Office 365 連結會將您導向 Office 365 註冊頁面。

如需 EAC 的相關資訊，請參閱 [Exchange 2013 中的 Exchange 系統管理中心](https://technet.microsoft.com/zh-tw/library/jj150562\(v=exchg.150\))。

## Exchange 管理命令介面

Exchange 管理命令介面 可讓您執行 EAC 可執行的任何工作，以及只能在 Exchange 管理命令介面中執行的其他一些工作。Exchange 管理命令介面 是安裝 Exchange 2013 管理工具時安裝在電腦上的 Windows PowerShell 指令碼和指令程式的集合。只有在您使用 Exchange 管理命令介面 圖示開啟 Exchange 管理命令介面 時，才會載入這些指令碼和指令程式。如果您直接開啟 Windows PowerShell，則不會載入 Exchange 指令碼和指令程式，您也無法管理內部部署組織。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以對本機內部部署組織建立手動的 Windows PowerShell 連線，這類似手動連線到以下的 Exchange Online 組織。不過，強烈建議您使用 Exchange 管理命令介面 圖示來開啟 Exchange 管理命令介面，以管理內部部署 Exchange 伺服器。</td>
</tr>
</tbody>
</table>


當您在已安裝管理工具的電腦上使用 Exchange 管理命令介面 圖示開啟 Exchange 管理命令介面 時，您可以管理內部部署組織。不過，當您使用此圖示開啟 Exchange 管理命令介面 時，無法管理 Exchange Online 組織。這是因為使用 Exchange 管理命令介面 圖示開啟 Exchange 管理命令介面 時，將自動連線至本機 Exchange 伺服器。

如果要使用 Windows PowerShell 來管理 Exchange Online 組織，您必須直接開啟 Windows PowerShell，而不是透過 Exchange 管理命令介面 圖示開啟。當您開啟 Windows PowerShell 時，可以手動指定想要連線的目標。建立手動連線時，您會在 Office 365 租用戶組織中指定管理員帳戶，然後執行命令來建立連線。建立連線後，就可以使用您有權限執行的 Exchange 指令程式。若要深入了解，請參閱[使用 Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=209660)。

如果您才剛接觸 Exchange 管理命令介面，而且想要瞭解 Exchange 管理命令介面 的運作方式、命令語法等基礎概念，請參閱 [使用 PowerShell 與 Exchange 2013 (Exchange 管理命令介面)](https://technet.microsoft.com/zh-tw/library/bb123778\(v=exchg.150\))。


---
title: '尋找內部和外部 Url 的 Exchange 系統管理中心: Exchange 2013 Help'
TOCTitle: 尋找內部和外部 Url 的 Exchange 系統管理中心
ms:assetid: 3ddb30ff-a405-4b9d-8d77-2d7a3a5ab8fa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ680108(v=EXCHG.150)
ms:contentKeyID: 50472934
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 尋找內部和外部 Url 的 Exchange 系統管理中心

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-02-04_

Exchange 系統管理中心 (EAC) 是在 Exchange Server 2013 中的 web 式管理主控台，因為您存取其網頁瀏覽器使用的 ECP 虛擬目錄的 URL。本主題顯示如何尋找 ECP 虛擬目錄的 URL。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ECP 是專為Exchange Server 2010開發的 web 型使用者介面。仍然在名稱中使用&quot;ECP&quot;的虛擬目錄的 EAC cmdlet 與這些指令程式可用來管理Exchange 2010和Exchange 2013 ECP 虛擬目錄。</td>
</tr>
</tbody>
</table>


若要深入了解 EAC，請參閱[Exchange 2013 中的 Exchange 系統管理中心](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您無法使用 EAC 來執行此程序。您必須使用命令介面。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的「Exchange 系統管理中心連線」項目。

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


## 使用命令介面來尋找 ECP 虛擬目錄的內部與外部 URL

此範例將以格式化清單來傳回 ECP 虛擬目錄名稱、內部 URL 以及外部 URL。

    Get-ECPVirtualDirectory | Format-List Name,InternalURL,ExternalURL

當命令完成時，使用網頁瀏覽器中的 *InternalURL* 或 *ExternalURL* 值來啟動 EAC。

如需詳細的語法及參數資訊，請參閱 [Get-EcpVirtualDirectory](https://technet.microsoft.com/zh-tw/library/dd351058\(v=exchg.150\))。


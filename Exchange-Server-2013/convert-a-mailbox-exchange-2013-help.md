---
title: '轉換信箱: Exchange Online Help'
TOCTitle: 轉換信箱
ms:assetid: dfed045e-a740-4a90-aff9-c58d53592f79
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ710164(v=EXCHG.150)
ms:contentKeyID: 50474404
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 轉換信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2017-04-26_

將信箱轉換成不同類型是信箱的非常類似經驗在 Exchange 2010。您仍必須在命令介面中使用 Set-mailbox 指令程式來執行轉換作業。

您可以將下列信箱從一種類型轉換成另一個：

  - 資源 （會議室或設備） 信箱的使用者信箱

  - 使用者信箱的共用的信箱

  - 資源信箱的共用的信箱

  - 使用者信箱的資源信箱

  - 共用信箱的資源信箱

請注意是否貴組織使用混合式 Exchange 環境，您需要使用內部部署 Exchange 管理工具來管理您的部署信箱。若要轉換的信箱中的混合式環境，您可能需要將信箱移回內部部署 Exchange、 將信箱類型、 轉換和然後將它移回至 Office 365。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您將使用者信箱轉換成共用信箱，您也應該從之前轉換信箱中移除任何行動裝置或您應該轉換後要封鎖行動裝置信箱的存取權。這是因為一旦信箱會轉換為共用信箱、 行動功能將無法正常運作。如需有關封鎖存取的詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=847873">移除先前的員工從 Office 365</a>。</td>
</tr>
</tbody>
</table>


## 使用命令介面來轉換信箱

預估完成時間：5 分鐘。

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md) 主題中的「收件者佈建權限」一節。

此範例會將轉換共用的信箱 MarketingDept1 對使用者信箱。

    Set-Mailbox MarketingDept1 -Type Regular

您可以使用下列值*Type*參數：

  - Regular

  - 主會議室

  - Equipment

  - 共用

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否成功轉換信箱，請執行下列命令介面命令：

    Get-Mailbox -Identity MarketingDept1 | Format-List RecipientTypeDetails

*RecipientTypeDetails*的值應該是*UserMailbox*。

如需詳細的語法及參數資訊，請參閱 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))。

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


---
title: 'Recreating arbitration mailboxes: Exchange 2013 Help'
TOCTitle: Recreating arbitration mailboxes
ms:assetid: bb6b8524-aaee-4be8-a04e-e61cd2ab3465
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt829264(v=EXCHG.150)
ms:contentKeyID: 74518108
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recreating arbitration mailboxes

 

_**上次修改主題的時間：**2018-01-17_

**摘要：** 關於Exchange 2013以及如何重新建立這些中仲裁信箱。

Exchange 2013隨附稱為 「*仲裁信箱*的五個系統信箱。仲裁信箱可用儲存不同類型的系統資料及管理訊息的核准工作流程。圖表下方列出每種類型的仲裁信箱和其職責。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>仲裁信箱名稱</th>
<th>顯示名稱</th>
<th>持續性的功能</th>
<th>函數</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
<td><p>Microsoft Exchange 同盟信箱</p></td>
<td><p>{}</p></td>
<td><p>這個信箱儲存資料的方式來維護不同的 Exchange 組織之間的同盟。這包括 Rights Management Services、 跨單位郵件流程監視探查和通知的回覆 線上封存、 郵件記錄管理及跨部署的空閒/忙碌資訊。</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{1f05a927-9350-4efe-a823-5529c2d64109}</p></td>
<td><p>Microsoft Exchange 核准助理</p></td>
<td><p>{}</p></td>
<td><p>這個信箱已佈建使用 Exchange 核准 framework 收件者的仲裁] 及 [自動群組核准要求。</p></td>
</tr>
<tr class="odd">
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
<td><p>Microsoft Exchange 遷移</p></td>
<td><p>{OrganizationCapabilityManagement}</p></td>
<td><p>儲存時移動信箱的批次所使用的 Exchange 移轉服務資料。</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMDataStorage}</p></td>
<td><p>探索系統信箱。</p>
<p>佈建用於電子探索功能是由法務人員用來找出符合指定之選取範圍準則的郵件。 這個信箱也用於由整合通訊儲存 UM 主控台參加檔案及其他資訊。</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMGrammarReady, OrganizationCapabilityPstProvider, OrganizationCapabilityMessageTracking, OrganizationCapabilityMailRouting, OrganizationCapabilityClientExtensions, OrganizationCapabilityGMGen, OrganizationCapabilityOABGen, OrganizationCapabilityUMGrammar}</p></td>
<td><p>這是稱為組織信箱。它用來建立離線通訊錄 (Oab)。至整個組織，包括跨地理位置不同網站的負載平衡 OAB 產生您可以建立其他組織的信箱。</p></td>
</tr>
</tbody>
</table>


如果您需要重新建立一或多個這些仲裁信箱，請參閱遵循指示。

## 您應知道您開始之前

  - 預估完成時間： 10 分鐘每個程序。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「收件者佈建權限」一節。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 使用Exchange 管理命令介面重新建立仲裁信箱

使用下列指示以重新建立特定類型的仲裁信箱。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>下列各節中的所有步驟必須從都執行相同的目錄擷取 Exchange 安裝媒體中的位置。</td>
</tr>
</tbody>
</table>


## 重新建立 Microsoft Exchange 同盟信箱

若要重新建立的仲裁信箱 FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042：

1.  如果缺少任何仲裁信箱，請執行下列命令：
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  在Exchange 管理命令介面，執行下列命令：
    
        Enable-Mailbox -Arbitration -Identity "FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042"

## 重新建立 Microsoft Exchange 核准小幫手的信箱

若要重新建立 SystemMailbox {1f05a927-9350-4efe-a823-5529c2d64109} 的仲裁信箱：

1.  如果缺少任何仲裁信箱，請執行下列命令：
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  在Exchange 管理命令介面，執行下列命令：
    
        Get-User | Where-Object {$_.Name -like "SystemMailbox{1f05a927-7709-4e35-9dbe-d0f608fb781a}"} | Enable-Mailbox -Arbitration

## 重新建立 Microsoft Exchange 遷移信箱

若要重新建立的仲裁信箱 Migration.8f3e7716-2011年-43e4-96b1-aba62d229136：

1.  如果缺少任何仲裁信箱，請執行下列命令：
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  在Exchange 管理命令介面，執行下列命令：
    
        Enable-Mailbox -Arbitration -Identity "Migration.8f3e7716-2011-43e4-96b1-aba62d229136"

3.  在Exchange 管理命令介面、 設定保存功能 (msExchCapabilityIdentifiers) 中執行下列命令：
    
        Set-Mailbox "Migration.8f3e7716-2011-43e4-96b1-aba62d229136" -Arbitration -Management:$True -Force

## 重新建立 Microsoft Exchange 探索系統信箱

若要重新建立 SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9} 的仲裁信箱：

1.  執行下列命令：
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

## 重新建立 Oab Microsoft Exchange 組織信箱

若要重新建立 SystemMailbox {bb558c35-97f1-4cb9-8ff7-d53741dc928c} 的仲裁信箱：

1.  如果缺少任何仲裁信箱，請執行下列命令：
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  在Exchange 管理命令介面，執行下列命令：
    
        Enable-Mailbox -Arbitration -Identity "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}"

3.  在Exchange 管理命令介面、 設定保存功能 (msExchCapabilityIdentifiers) 中執行下列命令：
    
        Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration | Set-Mailbox -Arbitration -UMGrammar:$True -OABGen:$True -GMGen:$True -ClientExtensions:$True -MessageTracking:$True -PstProvider:$True -MaxSendSize 1GB -Force

完成時，如果您執行命令`$OABMBX = Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration (Get-ADUser $OABMBX.SamAccountName -Properties *).msExchCapabilityIdentifiers`您會看到 46、 47，以及 51 會遺失。執行下列命令以新增所有後的功能：

    Set-ADUser $OABMBX.SamAccountName -Add @{"msExchCapabilityIdentifiers"="40","42","43","44","47","51","52","46"}

## 如何知道這是否正常運作？

若要確認您已順利重新建立的仲裁信箱，請使用具有*Arbitration*參數**Get-Mailbox**指令程式來擷取系統信箱。

    Get-Mailbox -Arbitration | Format-Table Name, DisplayName

檢視命令來確認已重新建立該適當的系統信箱，其中會根據名稱或從上方\] 表格中的顯示名稱的結果。

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


---
title: '管理 outlook 的應用程式的使用者存取: Exchange Online Help'
TOCTitle: 管理 outlook 的應用程式的使用者存取
ms:assetid: e5833dec-a23a-439e-ac03-92671817bff8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ943757(v=EXCHG.150)
ms:contentKeyID: 52062606
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理 outlook 的應用程式的使用者存取

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2018-04-17_

您可以使用 EAC 或 Exchange Online PowerShell 來管理增益集的使用者存取 outlook。

  - 使用 Exchange 系統管理中心 (EAC)，您可以針對您的使用者組織層級管理基本的增益集存取設定。例如，您可以設定增益集已啟用或停用的您的使用者。您也可以指定增益集是否必要或選用的使用者。

  - 您可以使用 Exchange Online PowerShell 中管理您可以使用 EAC 中的所有設定，以及其他設定。例如，您可以限制只有特定使用者能在組織中。

其他管理工作，請參閱[適用於 Outlook 的應用程式](add-ins-for-outlook-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 若要了解如何使用 Windows PowerShell 連線到 Exchange Online，請參閱[連線到 Exchange Online Protection PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554)。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的 「 增益集 outlook 」 項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 指定是否增益集為可用、 已啟用或停用

## 使用 EAC 來指定是否增益集為可用、 已啟用或停用

1.  在 EAC 中，瀏覽至 \[**組織**\>**增益集**。

2.  在清單檢視中，選取您想要變更設定、 增益集\] 和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  如果您不想讓使用者使用增益集，清除 \[**讓此增益集提供給您組織中的使用者**\] 核取方塊，然後再按一下 \[**儲存**。

4.  如果您想要讓使用者能夠使用增益集，請選取 \[**讓此增益集提供給您組織中的使用者**，然後選取您要的選項。
    
      - **選用，預設會啟用**  使用此設定可如果您想要允許使用者關閉 \[增益集。
    
      - **選用，預設停用**  使用此設定可如果您想要允許使用者開啟的增益集。
    
      - **強制、 永遠啟用。使用者無法停用此增益集**使用此設定可如果您不想讓使用者關閉 \[增益集。

5.  按一下 **\[儲存\]**。

## 使用 Exchange Online PowerShell 指定增益集為可用、 已啟用或停用

您可以使用 Exchange Online PowerShell 來指定增益集為可用、 已啟用或停用。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>執行下列命令以安裝您的組織的 outlook 查閱的顯示名稱和增益集的所有增益集的識別碼。</td>
</tr>
</tbody>
</table>


    Get-app -Organizationadd-in | Format-List DisplayName,add-inID

若要停用並對所有使用者都隱藏增益集，請執行下列命令。

    Set-app <add-in ID> -Organizationadd-in -Enabled $false

如果您想要讓增益集來啟用根據預設，但您希望使用者能夠將它關閉，執行下列命令。

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser Enabled

如果您想要根據預設，停用增益集，但您希望使用者能夠將它開啟，請執行下列命令。

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser Disabled

若要為您的使用者需要增益集，請執行下列命令。

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser AlwaysEnabled

如需詳細的語法和參數資訊，請參閱[Set-App](https://technet.microsoft.com/zh-tw/library/jj218630\(v=exchg.150\))。

## 如何知道這是否正常運作？

1.  在 EAC 中，瀏覽至 \[**組織**\>**增益集**。

2.  檢閱在 **\[使用者預設值\]** 和 **\[已提供\]** 欄中的值。

或

1.  從 Exchange Online PowerShell 中執行`Get-app -Organizationadd-in | Format-List DisplayName,add-inId,Enabled,Default*`。

2.  檢閱 **DefaultStateForUser** 和 **Enabled** 的值。

## 限制只有特定使用者能使用

## 使用 Exchange Online PowerShell 來限制只有特定使用者能使用

若要只能夠使用 LinkedIn 增益集讓行銷團隊通訊群組的成員，請執行下列命令。

    $a = Get-DistributionGroupMember Marketing

    Set-app <add-in ID for the LinkedIn add-in> -Organizationadd-in -ProvidedTo SpecificUsers -UserList $a.Identity -DefaultStateForUser Enabled}

如需詳細的語法和參數資訊，請參閱[Set-App](https://technet.microsoft.com/zh-tw/library/jj218630\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認是否已順利限制特定使用者的存取，請執行下列動作：

1.  從 Exchange Online PowerShell 中執行`Get-app -Organizationadd-in | Format-List DisplayName,add-inId,Enabled,Default*,ProvidedTo,UserList`。

2.  檢閱 **ProvidedTo** 的值。


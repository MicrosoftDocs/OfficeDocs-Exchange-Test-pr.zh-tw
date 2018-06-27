---
title: '在 [撥號對應表授權之使用者的通話: Exchange Online Help'
TOCTitle: 在 [撥號對應表授權之使用者的通話
ms:assetid: 7c7fd0c4-4001-408e-b352-c49bac9f78cc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb691175(v=EXCHG.150)
ms:contentKeyID: 51409220
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 \[撥號對應表授權之使用者的通話

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-21_

您可以啟用整合通訊 (UM) 撥號對應表上的撥號授權。在 \[撥號對應表的撥號授權可用來禁止未經過驗證的 Outlook 語音存取使用者撥打國家/地區或國際電話通話或*撥出*。撥出時執行的動作他們已呼叫 UM 撥號對應表設定 Outlook 語音存取電話號碼之後整合通訊 places 撥出電話的使用者。當您設定設定在 UM 撥號對應表計劃，以設定會套用到所有未驗證的使用者撥打 Outlook 語音存取號碼。

如需與撥出相關的其他管理工作，請參閱[讓使用者能夠進行的通話程序](allowing-users-to-make-calls-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。 如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行此程序之前，請確認國家/地區及國際撥號規則的已建立 UM 撥號對應表上。如需詳細步驟，請參閱[建立使用者的撥號規則](create-dialing-rules-for-users-exchange-2013-help.md)。

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

## 使用 EAC 在國內/地區撥號規則群組的 UM 撥號對應表上啟用撥號授權

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\] 頁面上，按一下 \[設定\]。

3.  在 **\[UM 撥號對應表\]** 頁面 \> **\[撥號授權\]** 上，按一下 **\[已授權的國內/區域撥號規則群組\]** 之下的 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在 **\[選取要允許的撥號規則群組\]** 頁面上，選取撥號規則群組，按一下 **\[確定\]**，然後按**\[儲存\]**。

## 使用 EAC 在國際撥號規則群組的 UM 撥號對應表上啟用撥號授權

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\] 頁面上，按一下 \[設定\]。

3.  在 **\[UM 撥號對應表\]** 頁面 \> **\[撥號授權\]** 上，按一下 **\[已授權的國際撥號規則群組\]** 之下的 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在 **\[選取要允許的撥號規則群組\]** 頁面上，選取撥號規則群組，按一下 **\[確定\]**，然後按**\[儲存\]**。

## 使用命令介面在 UM 撥號對應表上啟用國內/地區及國際撥號授權

此範例會在名爲 `MyUMDialPlan` 的 UM 撥號對應表上啟用 InCountry/RegionGroup1、InCountry/RegionGroup2、InternationalGroup1 和 InternationalGroup2 撥號授權。

    Set-UMDialPlan -Identity MyUMDialPlan -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2


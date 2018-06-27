---
title: '安裝或移除 Outlook for 貴組織的應用程式: Exchange Online Help'
TOCTitle: 安裝或移除 Outlook for 貴組織的應用程式
ms:assetid: 112f3ef7-9943-4a1e-8a42-e08e8e9f67f4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ943752(v=EXCHG.150)
ms:contentKeyID: 52062517
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安裝或移除 Outlook for 貴組織的應用程式

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2017-02-03_

您可以安裝或移除增益集的您的組織的 Outlook 使用 EAC 或命令介面。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，針對您的組織安裝增益集之後的增益集是可供您組織中的所有使用者。安裝之後，您可以使用 EAC 或命令介面可讓增益集選用或需要您的使用者，並指定您是否要啟用或停用增益集。如需如何變更增益集的預設設定，請參閱<a href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">管理 outlook 的應用程式的使用者存取</a>。若要限制的增益集至組織中的特定使用者的可用性，您必須使用命令介面。如需詳細資訊，請參閱<a href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">管理 outlook 的應用程式的使用者存取</a>。</td>
</tr>
</tbody>
</table>


其他管理工作，請參閱[適用於 Outlook 的應用程式](add-ins-for-outlook-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的 「 Outlook 應用程式 」 項目。

  - 您可以安裝及管理組織的增益集的權限指派給系統管理員。您也可以指派使用者權限安裝及管理自己使用的增益集。如需詳細資訊，請參閱[指定系統管理員和使用者可安裝和管理適用於 Outlook 增益集](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md)。

  - 存取 Office 存放區不支援信箱或組織中特定區域 （英文）。如果您沒有看到**新增來自 Office 市集**在**Exchange 系統管理中心**\[**組織**\] 選項 \>**增益集**\> ![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，您可以從 URL 或檔案的位置的 outlook 安裝增益集。如需詳細資訊，請連絡您的服務提供者。

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

## 安裝 Outlook 增益集

## 使用 EAC 來將增益集

1.  在 EAC 中，瀏覽至 \[**組織**\>**增益集**。

2.  按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，，然後選擇 \[您想要安裝的增益集的位置。
    
      - **新增來自 Office 市集**。在 Office 市集、 選取您想要安裝的應用程式，然後按一下 \[**新增\]**。與Outlook Web App搭配使用的應用程式會列在**Office 與 SharePoint 的增益集**底下 \> **Outlook**。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>存取 Office 存放區不支援信箱或組織中特定區域 （英文）。如果您沒有看到<strong>來自 Office 市集新增</strong>在<strong>Exchange 系統管理中心</strong>[<strong>組織</strong>] 選項 &gt;<strong>增益集</strong>&gt; <img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="加入圖示" alt="加入圖示" />，您可以從 URL 或檔案的位置的 outlook 安裝增益集。如需詳細資訊，請連絡您的服務提供者。</td>
        </tr>
        </tbody>
        </table>
    
      - **新增與 URL**。在**URL**\] 中輸入的增益集資訊清單檔案您想要安裝完整的 URL。
    
      - **從檔案新增\]**。選取 \[**瀏覽\]**，然後瀏覽至 \[增益集資訊清單檔案您想要安裝的位置。

3.  按一下 **\[儲存\]**。

## 使用命令介面將增益集

本範例會示範如何將增益集從 URL。

    New-App -OrganizationApp -Url <URL location for add-in manifest file>

本範例會示範如何從檔案新增增益集。

    New-App -OrganizationApp -FileData <File location for add-in manifest file>

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您使用命令介面您的組織安裝增益集時，您可以安裝增益集和同時設定為其設定。</td>
</tr>
</tbody>
</table>


如需語法及參數，請參閱 [New-App](https://technet.microsoft.com/zh-tw/library/jj218722\(v=exchg.150\))。

## Outlook 增益集移除

## 使用 EAC 來移除增益集

1.  在 EAC 中，瀏覽至 \[**組織**\>**增益集**。

2.  在清單檢視中，選取要移除的應用程式，然後按一下 **\[刪除\]**![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

## 使用命令介面來移除增益集

您可以使用命令介面從您的組織移除增益集。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>執行下列命令以安裝您的組織的 outlook 查閱的顯示名稱和所有增益集的應用程式識別碼。</td>
</tr>
</tbody>
</table>


    Get-App -OrganizationApp |FL DisplayName,AppID

執行下列命令以從組織中移除自訂增益集 Finance Test 增益集。

    Remove-App -OrganizationApp -Identity <GUID for Finance Test Add-in>

如需語法及參數，請參閱 [Remove-App](https://technet.microsoft.com/zh-tw/library/jj218709\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要檢視您組織中安裝增益集，請執行下列其中一個動作：

  - 在 EAC 中，瀏覽至 \[**組織**\>**增益集**，然後檢閱已安裝的增益集的清單。

  - 在命令介面中執行`Get-App`，並再檢閱已安裝的增益集的清單。


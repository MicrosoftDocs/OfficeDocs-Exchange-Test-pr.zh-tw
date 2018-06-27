---
title: '從檔案匯入自訂的 DLP 原則範本: Exchange Online Help'
TOCTitle: 從檔案匯入自訂的 DLP 原則範本
ms:assetid: 83f49dbd-f9b1-498e-b548-1529c5e1ccdb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150531(v=EXCHG.150)
ms:contentKeyID: 50472341
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 從檔案匯入自訂的 DLP 原則範本

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-08-09_

您可以管理透過 DLP 原則的機密資訊匯入包含原則資訊設定檔案。DLP 原則範本可以被開發獨立的 Exchange 化為 XML 檔案。不過，使用者必須符合特定格式需求才能正常運作。或者，匯出從舊版 Exchange 的原則可以匯入 Microsoft Exchange Server 2013。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在生產環境中執行 DLP 原則之前，您應先在測試模式中啟用這些原則。在這類測試期間，建議您設定範例使用者信箱，然後傳送叫用測試原則的測試郵件，以便確認結果。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「資料外洩防護 (DLP) 」項目。

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


## 您要執行的工作

## 使用 EAC 來從檔案匯入自訂的 DLP 原則範本

使用下列程序從檔案匯入自訂的 DLP 原則範本。若要避免混淆，提供每個組件的原則或規則的唯一名稱時可選擇提供您自己的名稱。

1.  在 EAC 中，瀏覽至 \[規範管理\] \> \[資料外洩防護\]。

2.  按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 圖示旁邊的箭頭，接著按一下 \[匯入原則\]。

3.  在 \[匯入原則\] 頁面上，完成下列欄位：
    
    1.  \[選取要匯入的檔案\]   新增您所要安裝的原則檔案名稱。
    
    2.  **\[名稱\]** 新增可區分此原則與其他原則的名稱。
    
    3.  \[說明\]   新增能摘要說明此原則的說明 (選用)。
    
    4.  **更多選項**  選取模式或此原則的狀態。新原則完全未啟用直到您指定應該是。原則預設模式是測試不通知。
    
    5.  按一下 \[下一步\] 來驗證與匯入原則。

## 使用命令介面從檔案匯入自訂的 DLP 原則範本

本範例會匯入的自訂 DLP 原則範本檔案在檔案 C:\\My Documents\\DLP Backup.xml。從 XML 檔案匯入的 DLP 原則集合中移除或組織內定義的所有原先既 DLP 原則會覆寫。請確定符合您目前的 DLP 原則集合的備份再匯入並覆寫目前的 DLP 原則。

    Import-DlpPolicyCollection -FileData ([Byte[]]$(Get-Content -Path " C:\My Documents\DLP Backup.xml " -Encoding Byte -ReadCount 0))

## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)


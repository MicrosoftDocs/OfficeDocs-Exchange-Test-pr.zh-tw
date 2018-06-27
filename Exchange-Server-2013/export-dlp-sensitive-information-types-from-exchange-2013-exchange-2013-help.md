---
title: '從 Exchange 2013 中匯出 DLP 敏感資訊類型: Exchange Online Help'
TOCTitle: 從 Exchange 匯出 DLP 敏感資訊類型
ms:assetid: 8f02fbc2-dd1c-4276-be1a-517a43fe39b2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn479225(v=EXCHG.150)
ms:contentKeyID: 59637258
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 從 Exchange 2013 中匯出 DLP 敏感資訊類型

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-05-04_

您可以檢視或變更內 DLP 原則的詳細資料而不需使用Exchange 系統管理中心 (EAC) 或Exchange 管理命令介面指令程式來匯出原則、 儲存為 XML 檔案，並修改該 XML 檔案。通常您再將 XML 檔案匯回Exchange。如此一來，原則可以編輯缺少Exchange。不過，他們必須符合特定格式需求，也稱為 \[XML 結構描述才能正常運作。

DLP 相關的其他管理工作，請參閱[管理 DLP 原則](manage-dlp-policies-exchange-2013-help.md)。

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

EAC 中不提供 DLP 原則或範本匯出至外部檔案的方式。使用Exchange 管理命令介面來執行此工作。

## 使用Exchange 管理命令介面匯出 DLP 敏感資訊類型

本範例會匯出至 XML 檔案 C:\\My Documents\\exportedInformationTypes.xml 路徑中所有的 DLP 敏感資訊類型以及其屬性。建議您目前的 DLP 敏感資訊類型集合的備份複本。若要完成此工作的其中一個方法是以匯出然後立即複製並重新命名相同的 XML 檔案。

1.  開啟Exchange 管理命令介面。

2.  類型**Get-classificationrulecollection**，與您組織的敏感資訊類型應顯示在螢幕上。如果尚未建立您自己的任何敏感資訊類型，您僅會看見預設、 內建的敏感資訊類型集合，標示為 「"Microsoft 規則套件。

3.  儲存在變數中的敏感資訊類型輸入**$ruleCollections = Get-classificationrulecollection**。

4.  現在請格式化的 XML 檔案與所有的該資料輸入**Set-content-路徑"C:\\My Documents\\exportedRules.xml"-Encoding Byte-值 $ruleCollections.SerializedClassificationRuleCollection**.

您現在可以編輯要視需要調整原則之 XML 檔案。若要了解如何自訂內建的敏感資訊類型，請參閱[自訂內建的 DLP 敏感資訊類型](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md)。如需回復將 Exchange 匯入原則的詳細資訊，請參閱[從檔案匯入自訂的 DLP 原則範本](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)。

## 相關資訊

[在 Exchange 中的敏感資訊類型外觀](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[自訂內建的 DLP 敏感資訊類型](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md)

[從檔案匯入自訂的 DLP 原則範本](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)


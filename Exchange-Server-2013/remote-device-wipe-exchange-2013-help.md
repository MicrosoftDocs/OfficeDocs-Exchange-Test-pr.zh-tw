---
title: '遠端裝置資料抹除: Exchange 2013 Help'
TOCTitle: 遠端裝置資料抹除
ms:assetid: cd615210-cd8a-48de-b3e3-8f9ec39ca380
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124591(v=EXCHG.150)
ms:contentKeyID: 50474275
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 遠端裝置資料抹除

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-09-19_

行動電話、 平板電腦與其他裝置可以儲存機密的公司資料，並提供許多公司資源的存取權。遺失或竊行動裝置時，該資料可能遭到洩漏。透過Microsoft Exchange 行動裝置信箱原則，您可以新增您的行動裝置密碼需求。這需要使用者輸入密碼來存取其行動裝置。我們建議，除了需要裝置密碼，您設定行動裝置來自動提示的閒置時間後的密碼。裝置密碼\] 和 \[閒置時間鎖定的組合會提供您的公司資料增強的安全性。

除了這些功能、 Exchange Server 2013提供遠端裝置抹除功能。您可以發出遠端裝置抹除命令從Exchange管理命令介面或 Exchange 系統管理中心 (EAC)。使用者可以發出自己遠端裝置抹除命令從MicrosoftOutlook Web App使用者介面。

遠端裝置抹除功能也會包含確認函數中的使用者信箱的同步處理狀態資料寫入時間戳記。這個時間戳記會顯示在Outlook Web App和使用者的行動電話內容\] 對話方塊中的 EAC 中。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遠端裝置抹除可以重設原廠預設狀態的行動電話。雖然遠端裝置抹除通訊協定實作於Exchange 2013只需要刪除的個人公司資料，所有目前的行動裝置製造商解譯為擦去電話上的所有資料的其中一個命令。許多行動裝置作業系統也抹除行動裝置中插入任何儲存卡上的所有資料。如果您正在行動電話上執行遠端裝置抹除您持有並想要保留儲存卡上的資料，建議您啟動遠端裝置抹除之前移除儲存卡。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遠端裝置抹除發生之後，資料復原是很難。但沒有資料移除程序會保留可用以何時新殘餘資料從行動裝置。從行動裝置的資料復原可能仍可以使用複雜的工具。</td>
</tr>
</tbody>
</table>


## 遠端裝置資料清除與本機裝置資料清除

本機裝置抹除行動裝置擦去本身沒有來自伺服器的要求時發生。如果您的組織實作行動裝置信箱原則指定的失敗時的密碼的次數上限，超過的最大值的行動裝置會執行本機裝置抹除。本機裝置抹除的結果是遠端裝置抹除相同。裝置會傳回到其原廠預設狀態。在行動裝置在執行時本機裝置抹除，沒有確認會傳送到Exchange伺服器。


---
title: '郵件原則及符合性: Exchange 2013 Help'
TOCTitle: 郵件原則及符合性
ms:assetid: 65f20a20-27a4-4f6e-9b27-f8705d65b8d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998599(v=EXCHG.150)
ms:contentKeyID: 50473364
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 郵件原則及符合性

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

電子郵件對於所有規模組織中的資訊工作者而言，已成為可靠並普遍的通訊媒介。訊息儲存庫和信箱已成為重要資料的存放庫。對組織而言，規劃郵件原則十分重要，可規定其訊息系統的公平使用，提供如何依原則行動的使用者準則，以及視需求提供可能不受允許的通訊類型詳細資訊。

組織也必須建立管理電子郵件週期的原則，依業務、法律和法規要求的時間長度保留郵件，針對訴訟和調查目的保存電子郵件記錄，並準備搜尋及提供必要的電子郵件記錄來完成 eDiscovery 要求。

敏感資訊外洩，例如智慧財產、貿易機密、商業計畫及由您的組織所收集或處理的個人識別資訊 (PII)，也必須妥善防範。

## Exchange 2013 中的郵件原則及符合性

下表提供 Microsoft Exchange Server 2013 中的郵件原則和符合性功能的概覽，並包含可協助您學習並管理這些功能的主題連結。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>描述</th>
<th>Resources</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>通訊記錄管理 (MRM)</p></td>
<td><p>為了遵循適用的規定或符合法律或業務要求，組織會將電子郵件週期原則納入他們的郵件原則中。應該能透過這些原則解決的常見問題包括：</p>
<ul>
<li><p>郵件的保留期限？</p></li>
<li><p>郵件的保留位置？</p></li>
<li><p>所有郵件是否應該保留相同期限？</p></li>
</ul>
<p>Exchange 2013 包含可讓您實作組織電子郵件週期原則的 MRM 功能。您可以使用 MRM 將統一的保留設定套用到所有郵件、使用自訂保留原則套用信箱的基本保留設定，以及選擇性地允許使用者分類郵件，以保留指定的一段時間。</p></td>
<td><p><a href="messaging-records-management-exchange-2013-help.md">通訊記錄管理</a></p></td>
</tr>
<tr class="even">
<td><p>原有範圍封存</p></td>
<td><p>因為不再需要個人儲存區 (.pst) 檔案，<em>就地封存</em>可協助您重新取得組織郵件資料的控制權，並且能讓使用者將郵件儲存到能夠在 Outlook 2010 和更新版本及 Outlook Web App 中存取的<em>封存信箱</em>。</p></td>
<td><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">就地封存 in Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>原有範圍暫止</p></td>
<td><p>如果合理預期到訴訟的可能性，組織就需要保留與案件相關的電子儲存資訊 (ESI)，包括電子郵件。就地保留功能可讓您搜尋並保存符合查詢參數的郵件。保護郵件不被刪除、修改和竄改，並能無限期地或在一段指定期間內被保留。</p></td>
<td><p><a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">就地保留與訴訟暫止</a></p></td>
</tr>
<tr class="even">
<td><p>原有範圍 eDiscovery</p></td>
<td><p>就地 eDiscovery 讓您能透過您的 Exchange 組織搜尋信箱資料、預覽搜尋結果，並將其複製到探索信箱。</p></td>
<td><p><a href="in-place-ediscovery-exchange-2013-help.md">就地 eDiscovery</a></p></td>
</tr>
<tr class="odd">
<td><p>日誌</p></td>
<td><p>日誌記錄可藉由錄製輸入和輸出電子郵件通訊，協助您的組織回應法律、法規和組織符合性需求。規劃郵件保留和符合性時，務必了解日誌記錄的內容、其如何適用於組織符合性原則，以及 Exchange 2013 如何協助您保護日誌記錄的郵件。</p></td>
<td><p><a href="journaling-exchange-2013-help.md">日誌</a></p></td>
</tr>
<tr class="even">
<td><p>傳輸規則</p></td>
<td><p>使用傳輸規則，您便能尋找通過您組織的郵件之特定情況，然後針對其執行動作。傳輸規則可讓您將訊息原則套用於電子郵件、保護電子郵件、保護通訊系統，並防止資訊外洩。</p></td>
<td><p><a href="mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md">郵件流程或傳輸規則</a></p></td>
</tr>
<tr class="odd">
<td><p>資料外洩防護 (DLP)</p></td>
<td><p>DLP 功能可幫助您保護機密資料並將您的原則和規定告知使用者。DLP 也可協助您防止使用者不小心將敏感資訊傳送給未經授權者。當您設定 DLP 原則時，可以藉由分析郵件系統的內容識別和保護敏感資料，這包括許多相關聯的檔案類型。Exchange 2013 中所提供的 DLP 原則範本以法規標準為基礎，例如 PII 和支付卡產業資料安全性標準 (PCI-DSS)。DLP 可以擴充，讓您加入對組織重要的其他原則。此外，新的原則提示功能可讓您在敏感資料傳送出去之前，通知使用者相關違規原則。</p></td>
<td><p><a href="technical-overview-of-dlp-data-loss-prevention-in-exchange.md">資料遺失防護</a></p></td>
</tr>
<tr class="even">
<td><p>資訊版權管理 (IRM)</p></td>
<td><p>資訊版權管理 (IRM) 使用 Active Directory Rights Management Services (AD RMS)，可針對電子郵件訊息和附件提供持續性的線上及離線保護。</p></td>
<td><p><a href="information-rights-management-exchange-2013-help.md">資訊版權管理</a></p></td>
</tr>
<tr class="odd">
<td><p>S/MIME</p></td>
<td><p>安全多用途網際網路郵件延伸 (S/MIME) 允許擁有 Office 365 信箱以及 Exchange 2013 與 Exchange Online 的人員在其組織內傳送已簽署和加密電子郵件，來協助保護敏感資訊。系統管理員可以透過同步處理 Office 365 與其內部部署伺服器之間的使用者憑證，然後設定 Outlook Online 支援 S/MIME，以針對 Office 365 信箱啟用 S/MIME。</p></td>
<td><p><a href="s-mime-for-message-signing-and-encryption-exchange-2013-help.md">為郵件簽章和加密的 S/MIME</a></p></td>
</tr>
<tr class="even">
<td><p>信箱稽核記錄</p></td>
<td><p>由於信箱可能會包含敏感、高度業務影響 (HBI) 資訊和 PII，因此追蹤哪些人登入組織中的信箱以及執行哪些動作是相當重要的。追蹤信箱擁有者以外的使用者 (稱為委派的使用者) 存取信箱則更為重要。使用信箱稽核記錄，您就可以依信箱擁有者、代理人 (包括具有完整信箱存取權限的系統管理員) 和系統管理員記錄信箱存取。</p></td>
<td><p><a href="mailbox-audit-logging-exchange-2013-help.md">信箱稽核記錄</a></p>
<p><a href="exchange-auditing-reports-exchange-2013-help.md">Exchange 稽核報告</a></p></td>
</tr>
<tr class="odd">
<td><p>系統管理員稽核記錄</p></td>
<td><p>系統管理員稽核記錄i可讓您記錄系統管理員對 Exchange 伺服器和組織設定以及 Exchange 收件者所進行的變更。您可以使用系統管理員稽核記錄作為變更控制程序的一部分，或追蹤設定和收件者的變更和存取，以遵循法規。</p></td>
<td><p><a href="administrator-audit-logging-exchange-2013-help.md">系統管理員稽核記錄</a></p></td>
</tr>
</tbody>
</table>


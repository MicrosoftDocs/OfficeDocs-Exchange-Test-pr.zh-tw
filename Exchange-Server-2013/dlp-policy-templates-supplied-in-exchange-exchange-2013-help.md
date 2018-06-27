---
title: 'Exchange 中提供的 DLP 原則範本: Exchange Online Help'
TOCTitle: Exchange 中提供的 DLP 原則範本
ms:assetid: 7e1917ab-1920-4a52-97d1-7dfe2add6198
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150530(v=EXCHG.150)
ms:contentKeyID: 50472340
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 中提供的 DLP 原則範本

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

在 Microsoft Exchange Server 2013和Exchange Online，您可以使用資料遺失防護 (DLP) 原則範本為起點建置 DLP 原則可協助您滿足您特定的法規和商務原則的需求。您可以修改的範本以符合組織的特定需求。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在生產環境中執行 DLP 原則之前，您應先在測試模式中啟用這些原則。在這類測試期間，建議您設定範例使用者信箱，然後傳送叫用測試原則的測試郵件，以便確認結果。<br />
使用這些原則無法確保與任何法規符合性。在測試完成後，變更必要設定 Exchange 中的資訊傳輸符合貴組織的原則與因此。例如，您可能需要使用已知的業務合作夥伴設定 TLS 或新增更嚴格的傳輸規則動作，例如新增至包含資料的特定類型的郵件的權限保護。</td>
</tr>
</tbody>
</table>


## DLP 可用的範本

下表列出 DLP 原則範本的 Exchange 中。若要深入了解自訂這些範本建立 DLP 原則，請參閱[管理 DLP 原則](manage-dlp-policies-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>範本</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>澳洲財務資料</p></td>
<td><p>協助偵測是否存在普遍會被認為是澳洲財務資料的資訊，包括信用卡與 SWIFT 碼。</p></td>
</tr>
<tr class="even">
<td><p>澳洲醫療記錄法案 (HRIP 法案)</p></td>
<td><p>協助偵測是否存在普遍認為受到澳洲醫療記錄與隱私權資訊 (HRIP) 法案管制的資訊，如醫療帳戶號碼與稅務檔案號碼。</p></td>
</tr>
<tr class="odd">
<td><p>澳洲個人識別資訊 (PII) 資料</p></td>
<td><p>協助偵測是否存在普遍會被認為是澳洲個人識別資訊 (PII) 的資訊，如稅務檔案號碼與駕照。</p></td>
</tr>
<tr class="even">
<td><p>澳洲隱私權法案</p></td>
<td><p>協助偵測是否存在普遍會被認為受到澳洲隱私權法案管制的資訊，如駕照與護照號碼。</p></td>
</tr>
<tr class="odd">
<td><p>加拿大財務資料</p></td>
<td><p>協助偵測是否存在普遍會被認為是加拿大財務資料的資訊，包括銀行帳戶號碼與信用卡。</p></td>
</tr>
<tr class="even">
<td><p>加拿大健康資訊法案 (HIA)</p></td>
<td><p>協助偵測是否存在受到亞伯達省的加拿大健康資訊法案 (HIA) 管制的資訊，包括如護照號碼與健康資訊等資料。</p></td>
</tr>
<tr class="odd">
<td><p>加拿大個人健康法案 (PHIPA) - 安大略省</p></td>
<td><p>協助偵測是否存在受到安大略省的加拿大個人健康資訊保護法案 (PHIPA) 管制的資訊，包括如護照號碼與健康資訊等資料。</p></td>
</tr>
<tr class="even">
<td><p>加拿大個人健康資訊法案 (PHIA) - 馬尼托巴省</p></td>
<td><p>協助偵測是否存在受到馬尼托巴省的加拿大個人健康資訊法案 (PHIA) 管制的資訊，包括如護照號碼與健康資訊等資料。</p></td>
</tr>
<tr class="odd">
<td><p>加拿大個人資訊保護法案 (PIPA)</p></td>
<td><p>協助偵測是否存在受到不列顛哥倫比亞省的加拿大個人資訊保護法案 (PIPA) 管制的資訊，包括如護照號碼與健康資訊等資料。</p></td>
</tr>
<tr class="even">
<td><p>加拿大個人資訊保護法案 (PIPEDA)</p></td>
<td><p>協助偵測是否存在受到加拿大個人資訊保護與電子文件法案 (PIPEDA) 管制的資訊，包括如護照號碼與健康資訊等資料。</p></td>
</tr>
<tr class="odd">
<td><p>加拿大個人識別資訊 (PII) 資料</p></td>
<td><p>協助偵測是否存在普遍會被認為是加拿大個人識別資訊 (PII) 的資訊，如健保 ID 號碼與社會保險號碼。</p></td>
</tr>
<tr class="even">
<td><p>法國資料保護法案</p></td>
<td><p>協助偵測是否存在普遍會被認為受到法國資料保護法案管制的資訊，如健康保險卡號碼。</p></td>
</tr>
<tr class="odd">
<td><p>法國財務資料</p></td>
<td><p>協助偵測是否存在普遍認為是法國財務資訊的資訊，包括如信用卡、帳戶資料與轉帳卡號碼等資訊。</p></td>
</tr>
<tr class="even">
<td><p>法國個人識別資訊 (PII) 資料</p></td>
<td><p>協助偵測是否存在普遍認為是法國個人識別資訊 (PII) 的資訊，包括護照號碼等資訊。</p></td>
</tr>
<tr class="odd">
<td><p>德國財務資料</p></td>
<td><p>協助偵測是否存在普遍認為是德國財務資料的資訊，如 EU 轉帳卡號碼。</p></td>
</tr>
<tr class="even">
<td><p>德國個人識別資訊 (PII) 資料</p></td>
<td><p>協助偵測是否存在普遍認為是德國個人識別資訊 (PII) 的資訊，包括駕照與護照號碼等資訊。</p></td>
</tr>
<tr class="odd">
<td><p>以色列財務資料</p></td>
<td><p>協助偵測是否存在普遍會被認為是以色列財務資料的資訊，包括銀行帳戶號碼與 SWIFT 碼。</p></td>
</tr>
<tr class="even">
<td><p>以色列個人識別資訊 (PII) 資料</p></td>
<td><p>協助偵測是否存在普遍認為是以色列個人識別資訊 (PII) 的資訊，如身分證號碼。</p></td>
</tr>
<tr class="odd">
<td><p>以色列隱私權保護</p></td>
<td><p>協助偵測是否存在普遍會被認為受到以色列隱私權保護法管制的資訊，包括如銀行帳戶號碼或身分證等資訊。</p></td>
</tr>
<tr class="even">
<td><p>日本財務資料</p></td>
<td><p>協助偵測是否存在普遍認為是日本財務資訊的資訊，包括如信用卡、帳戶資料與轉帳卡號碼等資訊。</p></td>
</tr>
<tr class="odd">
<td><p>日本個人識別資訊 (PII) 資料</p></td>
<td><p>協助偵測是否存在普遍認為是日本個人識別資訊 (PII) 的資訊，包括駕照與護照號碼等資訊。</p></td>
</tr>
<tr class="even">
<td><p>日本個人資訊保護法</p></td>
<td><p>協助偵測是否存在受到日本個人資訊保護法管制的資訊，包括如居民登記號碼等資料。</p></td>
</tr>
<tr class="odd">
<td><p>PCI 資料安全性標準 (PCI DSS)</p></td>
<td><p>協助偵測是否存在受到 PCI 資料安全性標準 (PCI DSS) 管制的資訊，包括如信用卡或轉帳卡號碼等資訊。</p></td>
</tr>
<tr class="even">
<td><p>沙烏地阿拉伯 - 反網路犯罪法</p></td>
<td><p>協助偵測是否存在普遍認為受到沙烏地阿拉伯反網路犯罪法管制的資訊，包括跨國銀行帳戶號碼與 SWIFT 碼。</p></td>
</tr>
<tr class="odd">
<td><p>沙烏地阿拉伯財務資料</p></td>
<td><p>協助偵測是否存在普遍會被認為是沙烏地阿拉伯財務資料的資訊，包括跨國銀行帳戶號碼與 SWIFT 碼。</p></td>
</tr>
<tr class="even">
<td><p>沙烏地阿拉伯個人識別資訊 (PII) 資料</p></td>
<td><p>協助偵測是否存在普遍認為是沙烏地阿拉伯個人識別資訊 (PII) 的資訊，如身分證號碼。</p></td>
</tr>
<tr class="odd">
<td><p>英國存取醫療報告法案</p></td>
<td><p>協助偵測是否存在受到英國存取醫療報告法案管制的資訊，包括如國家健康服務號碼等資料。</p></td>
</tr>
<tr class="even">
<td><p>英國資料保護法案</p></td>
<td><p>協助偵測是否存在受到英國資料保護法案管制的資訊，包括如國家保險號碼等資料。</p></td>
</tr>
<tr class="odd">
<td><p>英國財務資料</p></td>
<td><p>協助偵測是否存在普遍認為是英國財務資訊的資訊，包括如信用卡、帳戶資料與轉帳卡號碼等資訊。</p></td>
</tr>
<tr class="even">
<td><p>英國線上個人資訊實務守則 (PIOCP)</p></td>
<td><p>協助偵測是否存在受到英國線上個人資訊實務守則 (PIOCP) 管制的資訊，包括如健康資訊等資料。</p></td>
</tr>
<tr class="odd">
<td><p>英國個人識別資訊 (PII) 資料</p></td>
<td><p>協助偵測是否存在普遍認為是英國個人識別資訊 (PII) 的資訊，包括駕照與護照號碼等資訊。</p></td>
</tr>
<tr class="even">
<td><p>英國隱私權與電子通訊條例</p></td>
<td><p>協助偵測是否存在受到英國隱私權與電子通訊條例管制的資訊，包括如財務資訊等資料。</p></td>
</tr>
<tr class="odd">
<td><p>美國聯邦貿易委員會 (FTC) 消費者規則</p></td>
<td><p>協助偵測是否存在受到美國聯邦貿易委員會 (FTC) 消費者規則管制的資訊，包括如信用卡號碼等資料。</p></td>
</tr>
<tr class="even">
<td><p>美國財務資料</p></td>
<td><p>協助偵測是否存在普遍認為是美國財務資訊的資訊，包括如信用卡、帳戶資料與轉帳卡號碼等資訊。</p></td>
</tr>
<tr class="odd">
<td><p>美國 Gramm-Leach-Bliley 法案 (GLBA)</p></td>
<td><p>協助偵測是否存在受到 Gramm-Leach-Bliley 法案 (GLBA)管制的資訊，包括如社會安全號碼或信用卡號碼等資訊。</p></td>
</tr>
<tr class="even">
<td><p>美國健康保險法案 (HIPAA)</p></td>
<td><p>協助偵測是否存在受到美國健康保險流通與責任法案 (HIPAA) 管制的資訊，包括如社會安全號碼與健康資訊等資料。</p></td>
</tr>
<tr class="odd">
<td><p>美國愛國者法案</p></td>
<td><p>協助偵測是否存在普遍受到美國愛國者法案管制的資訊，包括如信用卡號碼或稅務識別號碼等資訊。</p></td>
</tr>
<tr class="even">
<td><p>美國個人識別資訊 (PII) 資料</p></td>
<td><p>協助偵測是否存在普遍認為是美國個人識別資訊 (PII) 的資訊，包括社會安全號碼與駕照等資訊。</p></td>
</tr>
<tr class="odd">
<td><p>美國國家違規通知法</p></td>
<td><p>協助偵測是否存在受到美國國家違規通知法管制的資訊，包括如社會安全與信用卡號碼等資料。</p></td>
</tr>
<tr class="even">
<td><p>美國國家社會安全號碼保密法</p></td>
<td><p>協助偵測是否存在受到美國國家社會安全號碼保密法管制的資訊，包括如社會安全號碼等資料。</p></td>
</tr>
</tbody>
</table>


## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[從範本建立 DLP 原則](how-to-new-dlp-data-loss-prevention-policy-template.md)

[在 Exchange 中的敏感資訊類型外觀](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)


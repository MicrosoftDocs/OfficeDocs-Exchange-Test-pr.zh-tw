---
title: '建立 DLP 原則偵測附隨報告: Exchange 2013 Help'
TOCTitle: 建立 DLP 原則偵測附隨報告
ms:assetid: 8e807f94-384c-43f5-be6f-06c5587175a0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150534(v=EXCHG.150)
ms:contentKeyID: 50472362
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立 DLP 原則偵測附隨報告

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

在Exchange Server 2013，您可以建立建立 DLP 原則規則集內附隨報告動作。此外，您可以向誰應該傳送報表以及如何處理原始郵件的項目。附隨報告可以包含任何下列的資訊。

## 附隨管理報告的內容

\[產生附隨報告\] 動作讓使用者可以將附隨報告傳送到附隨管理信箱。 如果原則內套用了 \[產生附隨報告\] 動作，每封郵件都會產生一份附隨報告。

下列是附隨報告範本中完整的行名稱清單。 格式欄描述如何識別每個報表中的欄位。 選用欄欄位指定每一個符合規則的報告中可能不會有哪些欄位。 DLP 專屬欄顯示哪些欄位會因為 DLP 功能而存在。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>行</strong> <strong>名稱</strong></p></td>
<td><p><strong>描述</strong></p></td>
<td><p><strong>格式</strong></p></td>
<td><p><strong>選用欄位</strong></p></td>
<td><p><strong>DLP 專屬</strong></p></td>
</tr>
<tr class="even">
<td><p>郵件識別碼</p></td>
<td><p>原始傳送郵件的識別碼</p></td>
<td><p>郵件識別碼： 郵件的識別碼</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Sender</p></td>
<td><p>真正寄件者的原始郵件</p></td>
<td><p>寄件者： 寄件者的電子郵件地址</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>主旨</p></td>
<td><p>原始郵件的主旨</p></td>
<td><p>主旨： 使用者輸入的主旨字串</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>收件者</p></td>
<td><p>收件者或原始郵件的收件者</p>
<p>每一個 [收件者] 行只能含有一個收件者，附隨報告中最多可顯示 10 個收件者。 如有其他收件者，下一個 [收件者] 行會顯示剩餘收件者的數目。</p></td>
<td><p>收件者： 收件者的電子郵件地址</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>副本</p></td>
<td><p>原始郵件的副本電子郵件；此行可選</p>
<p>每一個 [副本] 行只能有一個副本電子郵件地址，附隨報告中最多會顯示 10 個副本電子郵件地址。 如有其他副本地址，下一個 [副本] 行會顯示剩餘副本電子郵件地址的數目。</p></td>
<td><p>副本： 副本收件者的電子郵件地址</p></td>
<td><p>選用</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>密件副本</p></td>
<td><p>原始郵件的密件副本電子郵件地址；此行可選</p>
<p>每一個 [密件副本] 行只能有一個密件副本電子郵件地址，附隨報告中最多會顯示 10 個密件副本電子郵件地址。 如有其他密件副本電子郵件地址，下一個 [密件副本] 行會顯示剩餘密件副本電子郵件地址的數目。</p></td>
<td><p>密件副本： 密件副本收件者的電子郵件地址</p></td>
<td><p>選用</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>嚴重性</p></td>
<td><p>審計規則命中率的嚴重程度；如果多個規則被命中顯示最高嚴重性。</p></td>
<td><p>嚴重性： 低、 中或高</p></td>
<td><p>選用</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>覆寫</p></td>
<td><p>如果郵件被覆寫且有提供覆寫理由就顯示。</p></td>
<td><p>覆寫： 是，理由： IW 輸入理由字串</p></td>
<td><p>選用</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>誤判</p></td>
<td><p>如果郵件被誤判就顯示。</p></td>
<td><p>誤判： 是</p></td>
<td><p>選用</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>資料分類</p></td>
<td><p>原始郵件中發現偵測到的資料分類；此行可選。</p>
<p>每一個資料分類行只有一個偵測到的分類及其計數、可信度和建議的最小信賴等級。 附隨報告中最多會顯示 5 個偵測到的分類。 如果偵測到的分類是親和的，就不會套用計數值，也不會顯示。</p></td>
<td><p>資料分類： 敏感資訊類型，計數： 在郵件中找到的敏感資訊的執行個體： 百分比值，建議最小信賴等級： 百分比值</p></td>
<td><p>選用</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>規則命中</p></td>
<td><p>顯示命中原始郵件的所有規則。</p>
<p>包括被命中的規則名稱、規則所停駐的 DLP 原則 (選用)、郵件因規則所採取的行動、規則中造成規則被命中的資料分類，以及規則的定義。</p></td>
<td><p>規則命中： 規則名稱，DLP 原則： DLP 原則名稱 (如適用的話)，動作： 單一動作，資料分類： 敏感資訊類型，定義： 規則定義 (如適用的話)</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>識別碼相符</p></td>
<td><p>顯示相符的資料分類、郵件中確實相符的內容，以及資料相符的主要證明；此行可選。</p></td>
<td><p>識別碼相符： 敏感資訊類型，值： 敏感資訊的實際值，內容： 郵件中敏感資訊周圍的文字</p></td>
<td><p>選用</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


## 相關資訊

[檢視 DLP 原則偵測報告](view-dlp-policy-detection-reports-exchange-2013-help.md)

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)


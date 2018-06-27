---
title: '遠端網域支援的字元集: Exchange Online Help'
TOCTitle: 遠端網域支援的字元集
ms:assetid: 66023a62-1fd3-4019-be2b-4e7147db148a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998600(v=EXCHG.150)
ms:contentKeyID: 52062330
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 遠端網域支援的字元集

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

傳送至遠端網域的郵件可以指定下列的字元集。

  - 在 Exchange 系統管理中心 (EAC)，在**遠端網域**設定\] 頁面上，選取 \[從**MIME 字元集**和**非 MIME 字元集**\] 下拉式清單的名稱。

  - 在命令介面中使用下表中的 \[名稱\] 欄中的值*CharacterSet*參數或*NonMimeCharacterSet*[Set-RemoteDomain](https://technet.microsoft.com/zh-tw/library/aa997857\(v=exchg.150\)) cmdlet 中的參數。

### 遠端網域組態支援的字元集

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>big5</p></td>
<td><p>繁體中文 (Big5)</p></td>
</tr>
<tr class="even">
<td><p>DIN_66003</p></td>
<td><p>德文 (IA5)</p></td>
</tr>
<tr class="odd">
<td><p>euc-jp</p></td>
<td><p>日文 (EUC)</p></td>
</tr>
<tr class="even">
<td><p>euc-kr</p></td>
<td><p>韓文 (EUC)</p></td>
</tr>
<tr class="odd">
<td><p>GB18030</p></td>
<td><p>簡體中文 (GB18030)</p></td>
</tr>
<tr class="even">
<td><p>gb2312</p></td>
<td><p>簡體中文 (GB2312)</p></td>
</tr>
<tr class="odd">
<td><p>hz-gb-2312</p></td>
<td><p>簡體中文 (HZ)</p></td>
</tr>
<tr class="even">
<td><p>iso-2022-jp</p></td>
<td><p>日文 (JIS)</p></td>
</tr>
<tr class="odd">
<td><p>iso-2022-kr</p></td>
<td><p>韓文 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-1</p></td>
<td><p>西歐語系 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-2</p></td>
<td><p>中歐語系 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-3</p></td>
<td><p>拉丁文 3 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-4</p></td>
<td><p>波羅的海文 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-5</p></td>
<td><p>斯拉夫文 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-6</p></td>
<td><p>阿拉伯文 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-7</p></td>
<td><p>希臘文 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-8</p></td>
<td><p>希伯來文 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-9</p></td>
<td><p>土耳其文 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-13</p></td>
<td><p>愛沙尼亞文 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-15</p></td>
<td><p>拉丁文 9 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>koi8-r</p></td>
<td><p>斯拉夫文 (KOI8-R)</p></td>
</tr>
<tr class="even">
<td><p>koi8-u</p></td>
<td><p>斯拉夫文 (KOI8-U)</p></td>
</tr>
<tr class="odd">
<td><p>ks_c_5601-1987</p></td>
<td><p>韓文 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>NS_4551-1</p></td>
<td><p>挪威文 (IA5)</p></td>
</tr>
<tr class="odd">
<td><p>SEN_850200_B</p></td>
<td><p>瑞典文 (IA5)</p></td>
</tr>
<tr class="even">
<td><p>shift_jis</p></td>
<td><p>日文 (Shift-JIS)</p></td>
</tr>
<tr class="odd">
<td><p>utf-8</p></td>
<td><p>Unicode (UTF-8)</p></td>
</tr>
<tr class="even">
<td><p>windows-1250</p></td>
<td><p>中歐語系 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1251</p></td>
<td><p>斯拉夫文 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1252</p></td>
<td><p>西歐語系 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1253</p></td>
<td><p>希臘文 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1254</p></td>
<td><p>土耳其文 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1255</p></td>
<td><p>希伯來文 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1256</p></td>
<td><p>阿拉伯文 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1257</p></td>
<td><p>波羅的海文 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1258</p></td>
<td><p>越南文 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-874</p></td>
<td><p>泰文 (Windows)</p></td>
</tr>
</tbody>
</table>


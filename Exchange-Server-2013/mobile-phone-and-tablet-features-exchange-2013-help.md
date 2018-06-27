---
title: '行動電話與平板功能: Exchange 2013 Help'
TOCTitle: 行動電話與平板功能
ms:assetid: ad54d9e6-7a1c-4fb0-b5a9-0b042b98ada3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232162(v=EXCHG.150)
ms:contentKeyID: 50554081
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 行動電話與平板功能

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

使用者可以透過 Microsoft Exchange ActiveSync 存取其電子郵件、 行事曆、 連絡人和行動電話、 平板電腦和其他可攜式裝置上的 \[任務資訊。他們也可以使用它來設定其簽章與自動回覆。與 Exchange ActiveSync 搭配使用各種不同的行動電話和裝置。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然我們一致地參照至行動電話以存取Exchange Server 2013的裝置，有許多裝置可存取Exchange 2013但沒有行動電話功能。這些裝置，以及參照此文件中的 「 行動電話 」 的字詞。</td>
</tr>
</tbody>
</table>


## Exchange ActiveSync 相容裝置

使用者可以利用Exchange ActiveSync的豐富型功能來選取與Exchange ActiveSync相容的行動電話。這些行動電話是從許多製造商及許多通信業者。如需詳細資訊，請參閱特定行動電話文件。

與Microsoft Exchange相容的行動電話包括下列各項：

  - **Apple**  Apple iPhone、 iPod Touch 及 iPad 所有支援Exchange ActiveSync。

  - **Windows Phone**  Windows Phone 8、 Windows Phone 7 與舊版所有支援 Exchange ActiveSync。

  - **android**  許多行動電話與平板電腦與 Android 作業系統支援Exchange ActiveSync。不過，這些行動裝置可能無法支援所有可用的行動裝置信箱原則。如需詳細資訊，請參閱[行動裝置信箱原則](mobile-device-mailbox-policies-exchange-2013-help.md)。

## Windows Phone 軟體功能

具有Windows作為其作業系統的電話軟體版本的行動電話了解與 Exchange 2013 進行同步處理時提供的最大的功能。下表列出可用的 Windows Phone 8 和 Windows Phone 7 的行動裝置信箱原則。

### Windows Phone 7 和 8 的功能

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>作業系統</th>
<th>功能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows 8 Phone</p></td>
<td><p>Windows Phone 8 支援下列行動裝置信箱原則：</p>
<ul>
<li><p>允許簡單裝置密碼</p></li>
<li><p>需要英數字元密碼</p></li>
<li><p>已啟用的裝置密碼</p></li>
<li><p>裝置密碼到期</p></li>
<li><p>啟用的 IRM</p></li>
<li><p>最大裝置密碼嘗試失敗</p></li>
<li><p>裝置時間上限鎖定</p></li>
<li><p>裝置密碼複合字元數下限</p></li>
<li><p>最小裝置密碼長度</p></li>
<li><p>需要裝置加密</p></li>
<li><p>遠端清除</p></li>
</ul>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果貴組織使用其他行動裝置信箱原則設定，您需要將<strong>允許非可提供裝置</strong>原則設定為 true。因為仍可進行同步處理其他行動電話和裝置的不符合您的行動裝置原則設定的所有需求可以為您組織的安全性含意。如需詳細資訊，請參閱<a href="mobile-device-mailbox-policies-exchange-2013-help.md">行動裝置信箱原則</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p>Windows Phone 7 行動電話提供支援所有的 Exchange ActiveSync 信箱原則設定的子集合：</p>
<ul>
<li><p>所需的密碼</p></li>
<li><p>密碼最小長度</p></li>
<li><p>最大閒置時間鎖定</p></li>
<li><p>最大裝置密碼嘗試失敗</p></li>
<li><p>允許簡單密碼</p></li>
<li><p>密碼過期</p></li>
<li><p>密碼歷程</p></li>
<li><p>停用抽取式儲存</p></li>
<li><p>停用 IrDA</p></li>
<li><p>停用桌面同步處理</p></li>
<li><p>封鎖遠端桌面</p></li>
<li><p>封鎖網際網路共用</p></li>
</ul></td>
</tr>
</tbody>
</table>


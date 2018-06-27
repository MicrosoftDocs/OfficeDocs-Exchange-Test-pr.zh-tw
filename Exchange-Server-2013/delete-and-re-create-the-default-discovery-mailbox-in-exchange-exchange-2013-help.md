---
title: '刪除並重新建立 Exchange 中預設的探索信箱: Exchange Online Help'
TOCTitle: 刪除並重新建立 Exchange 中預設的探索信箱
ms:assetid: 4bde0b00-bdf7-44b4-ba64-aa062bc10ca2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn750894(v=EXCHG.150)
ms:contentKeyID: 62371313
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 刪除並重新建立 Exchange 中預設的探索信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-05-04_

您可以使用 Exchange 管理命令介面來刪除預設探索信箱、重新建立信箱，然後指派權限給它。

## 我為何想要這樣做？

Exchange Server 2013和Exchange Online、 預設的探索信箱的大小上限為 50 GB。它用來儲存在就地 eDiscovery 搜尋結果。已變更的大小限制之前，組織可能增加為超過 50 GB 的存放區配額。因此，探索信箱無法成長超過 50 gb。有三個預設的探索信箱大於 50 GB 的問題：

  - 不受支援。

  - 無法移轉至 Office 365。

  - 如果是預設的探索信箱中Exchange Server 2010，則無法升級到Exchange Server 2013。

如何解決此問題取決於您是否要從超過 50 GB 的預設探索信箱中儲存搜尋結果。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>您要儲存搜尋結果嗎？</th>
<th>執行</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>否</p></td>
<td><p>依照本主題中的步驟來刪除，然後重新建立預設探索信箱。</p></td>
</tr>
<tr class="even">
<td><p>是</p></td>
<td><p>依照＜<a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">降低探索 Exchange 中信箱的大小</a>＞中的步驟進行。</p></td>
</tr>
</tbody>
</table>


## 使用Exchange 管理命令介面來刪除並重新建立預設的探索信箱

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用Exchange 系統管理中心 (EAC)，因為探索信箱未出現在 EAC 中。</td>
</tr>
</tbody>
</table>


1.  執行下列命令以刪除預設的探索信箱。
    
        Remove-Mailbox "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}"

2.  在要求確認刪除信箱和相對應 Active Directory 使用者物件的訊息中，輸入 **Y**，然後按 Enter 鍵。
    
    當您在下一個步驟中建立探索信箱時，Active Directory 中會建立新的使用者物件。

3.  執行下列命令以重新建立預設的探索信箱。
    
        New-Mailbox -Name "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -Alias "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -DisplayName "Discovery Search Mailbox" -Discovery

4.  執行下列命令，將開啟預設探索信箱和檢視搜尋結果的權限指派給「探索管理」角色群組。
    
        Add-MailboxPermission "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User "Discovery Management" -AccessRights FullAccess -InheritanceType all


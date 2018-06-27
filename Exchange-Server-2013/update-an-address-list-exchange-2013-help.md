---
title: '更新通訊清單: Exchange 2013 Help'
TOCTitle: 更新通訊清單
ms:assetid: 163e7099-cf14-4bb0-a84c-1401e9db670e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996375(v=EXCHG.150)
ms:contentKeyID: 50472622
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.UpdateAddressListWizardForm.ScheduleWizardPage
ms.translationtype: MT
---

# 更新通訊清單

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-14_

通訊清單的收件者和其他 Active Directory 物件的集合。您可以套用的通訊清單時已編輯的地址清單篩選規則。若要更新加入新的收件者並移除不再符合篩選準則的使用者通訊清單的成員資格，您必須套用的地址清單。

如需與通訊清單相關的其他管理工作，請參閱[地址清單程序](address-list-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 此程序可能需要長的時間才能完成收件者地址清單中的數目。

  - 某些通訊清單包含千分位或數萬個收件者根據您的組織與您新增到地址清單的篩選器的大小。更新通訊清單可以需要大量的電腦資源。因此，可能會想要在離峰時間期間更新的地址清單。

  - 若通訊清單包含超過 3,000 個收件者，我們建議您使用 Exchange 管理命令介面來更新通訊清單。

如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

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

## 使用 EAC 來更新通訊清單

1.  瀏覽至 \[組織\] \> \[通訊清單\]。

2.  在清單檢視中，選擇要更新的通訊清單。

3.  在細節窗格中，按一下 \[更新\] 。

## 使用命令介面來更新通訊清單

此範例會更新名為 Washington State 的通訊清單。

    Update-AddressList "Washington State"

如果您有多個具有相同名稱的通訊清單，您必須指定您想要更新的地址清單的完整路徑。例如，如果您要更新的地址清單銷售 「 北美地區 」 底下，但也有 \[Europe Sales 通訊清單，請使用下列命令：

    Update-AddressList "North America\Sales"

如需詳細的語法及參數資訊，請參閱 [Update-AddressList](https://technet.microsoft.com/zh-tw/library/aa997982\(v=exchg.150\))。


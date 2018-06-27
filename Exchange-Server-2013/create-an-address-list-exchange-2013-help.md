---
title: '建立通訊清單: Exchange 2013 Help'
TOCTitle: 建立通訊清單
ms:assetid: e86ba1b7-c41c-4050-bc29-13996cf53c59
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125036(v=EXCHG.150)
ms:contentKeyID: 50474497
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewAddressListWizardForm.AddressListIntroductionPage
ms.translationtype: MT
---

# 建立通訊清單

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-12_

通訊清單的收件者和其他 Active Directory 物件的集合。每個地址清單可以包含一或多個類型的物件 （例如，使用者、 連絡人、 群組、 公用資料夾、 會議及其他資源）。通訊清單也提供給分割區中Active Directory可特定使用者群組的郵件功能之物件的機制。

如需與通訊清單相關的其他管理工作，請參閱[地址清單程序](address-list-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md)主題中的「通訊清單」項目。

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

## 使用 EAC 建立通訊清單

1.  瀏覽至 \[組織\] \> \[通訊清單\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[通訊清單\] 中，輸入名稱並指定收件者類型以加入清單。

3.  根據預設，Exchange 會建立包含您組織中的所有成員的通訊清單。若要建立唯一的自訂地址清單中，按一下 \[**新增規則**\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您不新增規則，則會建立某一個預設通訊清單的副本。</td>
    </tr>
    </tbody>
    </table>


4.  在清單中選取篩選選項 (例如 \[自訂屬性 1\])。

5.  在 \[指定字詞\] 中輸入篩選依據的字詞，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，然後按一下 \[確定\]。
    
    您可以繼續新增數個片語或文字重複步驟 4。篩選是布林值**或**陳述式。例如，您可以建立篩選器，將會套用至其自訂 1 屬性等於**奧**、**艾達**或**華盛頓**的使用者的通訊清單。

6.  （選用）按一下 \[**新增規則**\] 以新增其他篩選器。其他篩選器建立布林值**和**陳述式。更多的篩選器您新增，使用者的通訊清單將會套用至數目較少。

7.  按一下 \[包含預覽收件者通訊清單\]，查看此通訊清單將套用的收件者。

8.  按一下 \[儲存\]。

9.  您將取得地址清單不是一則警告訊息套用直到您更新。根據您的組織與您新增到地址清單的篩選器的大小，某些通訊清單可以包含千分位或數萬個收件者。更新通訊清單可能會影響您的資源、，因此可能會想要在離峰時間期間更新地址。
    
    如需更新通訊清單的詳細資訊，請參閱[更新通訊清單](update-an-address-list-exchange-2013-help.md)。

## 使用命令介面來建立通訊清單

此範例會使用 *RecipientFilter* 參數來建立通訊清單 MyAddressList，並納入屬於信箱使用者且將 `StateOrProvince` 設定為 `Washington` 或 `Oregon` 的收件者。

    New-AddressList -Name MyAddressList -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

此範例會使用內建條件在 All Rooms 父系容器中建立子系通訊清單 Building 34 Meeting Rooms。

    New-AddressList -Name "Building 34 Meeting Rooms" -Container "\All Rooms" -IncludedRecipients Resources -ConditionalCustomAttribute1 "Building 34"

如需詳細的語法及參數資訊，請參閱 [New-AddressList](https://technet.microsoft.com/zh-tw/library/aa996912\(v=exchg.150\))。


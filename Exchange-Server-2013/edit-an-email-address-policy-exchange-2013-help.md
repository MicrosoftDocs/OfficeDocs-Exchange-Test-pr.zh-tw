---
title: '編輯電子郵件地址原則: Exchange 2013 Help'
TOCTitle: 編輯電子郵件地址原則
ms:assetid: cc8b36a0-95f4-43e9-bc64-87646d2e14e4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124580(v=EXCHG.150)
ms:contentKeyID: 50474241
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.EditEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: MT
---

# 編輯電子郵件地址原則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-12-10_

電子郵件地址原則可為收件者 (包含使用者、連絡人和群組) 產生主要與次要的電子郵件地址，以便收件者收發電子郵件。

如欲瞭解更多與角色群組相關的管理工作，請參閱 [電子郵件地址原則程序](email-address-policy-procedures-exchange-2013-help.md)。

## 開始前需要瞭解什麼？

  - 預估完成時間：5 分鐘。

  - 如果使用命令介面建立原則，將無法使用 Exchange 系統管理中心 (EAC) 編輯電子郵件地址原則。

  - 如果使用收件者篩選器建立電子郵件地址原則，您必須使用命令介面來編輯電子郵件地址原則。如需詳細資訊，請參閱[使用收件者篩選器來建立電子郵件地址原則](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子郵件地址和通訊錄](email-addresses-and-address-books-exchange-2013-help.md) 項目中的「電子郵件地址原則」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用 EAC 變更套用原則的收件者

1.  瀏覽至 \[郵件流程\]\> \[電子郵件地址原則\]。

2.  在清單檢視中，選取您要變更的電子郵件地址原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  
    
    在 \[電子郵件地址原則\] 中，按一下 \[套用至\] 並修改設定。

## 使用 EAC 變更電子郵件地址原則的優先順序

使用者可擁有多個相同的電子郵件帳戶 （例如 ayla@exchange.mail.contoso.com 或 ayla@contoso.com） 的 proxy 電子郵件地址。這些電子郵件地址可以再套用的優先順序。例如，請考慮此案例： 您有兩個電子郵件地址原則並將它們指派 1 及 2 的優先順序。如果您建立另一個原則，它會自動指派的優先順序為 3。不過，假設您有兩個原則，而且您指定的其中一個是優先順序為 1，但其他原則建立時指派預設優先順序為 2。在此例中，您所建立的下一個原則將，預設會成為優先順序 2 原則。上一個優先順序 2 將原則指派的優先順序為 3。

1.  瀏覽至 \[郵件流程\]\> \[電子郵件地址原則\]。

2.  選取要變更優先順序的電子郵件地址原則，然後按一下 \[提升優先順序\]![向上箭號圖示](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "向上箭號圖示") 或 \[降低優先順序\]![向下箭號圖示](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "向下箭號圖示")。

## 使用命令介面編輯電子郵件地址原則

此範例會編輯目前有位於 Georgia、Alabama 及 Louisiana 的收件者包含在其中的東南區辦公室電子郵件地址原則，以同時包含位於 Texas 的收件者。

    Set-EmailAddressPolicy -Identity "South East Offices" -ConditionalStateorProvince "Georgia","Alabama","Louisiana","Texas"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然位於 Georgia、Alabama 及 Louisiana 的收件者已套用電子郵件地址原則，仍必須將他們加入參數內，因為參數會覆寫值，而不是將值附加到現有的值。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [Set-EmailAddressPolicy](https://technet.microsoft.com/zh-tw/library/bb124517\(v=exchg.150\))。


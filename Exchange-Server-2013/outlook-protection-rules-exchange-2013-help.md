---
title: 'Outlook 保護規則: Exchange 2013 Help'
TOCTitle: Outlook 保護規則
ms:assetid: bd7d0ad7-1f8e-46da-a74b-58c58f3eff93
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638178(v=EXCHG.150)
ms:contentKeyID: 50474074
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook 保護規則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

每日、 資訊工作者 exchange 電子郵件，包括財務報表及資料、 客戶與員工資訊和機密的產品資訊及規格的機密資訊。在 Microsoft Exchange Server 2013、 Microsoft Outlook、 和 Microsoft OfficeOutlook Web App，使用者可以套用資訊版權管理 (IRM) 保護郵件套用Active Directory Rights Management Services (AD RMS) 權限原則範本。這需要 AD RMS 部署在組織中。如需 AD RMS 的詳細資訊，請參閱 ＜ [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823)。

不過時的使用者選擇要靠左、, 可能傳送訊息以沒有 IRM 保護的純文字。使用電子郵件以主控服務的組織，只有資訊外洩的風險如下一則訊息離開用戶端會路由傳送和儲存組織的界限之外。雖然架設公司的電子郵件可能會有定義完善的程序和以協助降低風險資訊外洩的後一則訊息離開組織的界限檢查、 組織會失去資訊的控制項。Outlook 保護規則可協助保護這種類型的資訊外洩。

如需管理 IRM 的相關管理工作之詳細資訊，請參閱[資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## Outlook 中的自動 IRM 保護

中Exchange 2013、 Outlook保護規則可協助您組織的風險資訊外洩保護透過自動將 IRM 保護套用至Exchange 2013中的郵件。郵件是受 IRM 保護其保留Outlook用戶端之前。此保護也會套用至任何使用支援的檔案格式的附件。

當您建立Outlook保護規則Exchange 2013 server 上時，規則會自動分散至Outlook 2010使用Exchange Web 服務。若要將規則套用Outlook 2010您指定 AD RMS 權限原則範本必須提供使用者電腦上。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果從 AD RMS 伺服器移除權限原則範本，您必須修改使用已移除的範本任何Outlook保護規則。如果將Outlook保護規則會繼續使用已移除、 權限原則範本和停用傳輸解密已在組織中啟用，解密代理程式將無法解密不再可用的範本受到保護的郵件。若為必要項目已停用傳輸解密的傳輸服務會拒絕此郵件並將未傳遞回報 (NDR) 傳送給寄件者。如需停用傳輸解密的詳細資訊，請參閱<a href="transport-decryption-exchange-2013-help.md">傳輸解密</a>。如需 AD RMS 權限原則範本的詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=179455">AD RMS 原則範本考量</a>。<br />
Windows Server 2008和較新版本，而不是可以封存原則範本的權限中刪除。封存的範本仍可授權內容，但已封存的範本建立或修改Outlook保護規則、 時未含的範本清單中。</td>
</tr>
</tbody>
</table>


Outlook保護規則就類似於傳輸保護規則。同時套用根據郵件條件，並同時套用 AD RMS 權限保護範本來保護郵件。不過，傳輸保護規則是由傳輸規則代理程式套用的 Mailbox server 上的傳輸服務中。Outlook保護規則套用Outlook 2010，才能將郵件保留在使用者的電腦。受到Outlook保護規則的郵件會進入傳輸管線搭配已套用 IRM 保護。此外， Outlook保護規則以受保護的郵件也會儲存在寄件者的信箱傳送的項目資料夾中加密的格式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果停用傳輸解密Exchange組織中啟用，是由您組織中使用的 AD RMS 伺服器Outlook保護規則受 IRM 保護的郵件進行解密由解密代理程式上傳輸服務。可以由傳輸規則代理程式及其他安裝上的傳輸服務的傳輸代理程式檢查郵件內容。如需停用傳輸解密的詳細資訊，請參閱<a href="transport-decryption-exchange-2013-help.md">傳輸解密</a>。</td>
</tr>
</tbody>
</table>


當您使用傳輸保護規則時，使用者會擁有一則訊息是否要自動保護上的傳輸服務沒有指示。當Outlook保護規則套用至訊息的Outlook 2010使用者知道是否一則訊息會受 IRM 保護。如有需要，使用者也可以選取不同的權限原則範本。

## 建立 Outlook 保護規則

若要建立Outlook保護規則，您必須使用[New-OutlookProtectionRule](https://technet.microsoft.com/zh-tw/library/dd298182\(v=exchg.150\))指令程式在Exchange Management Shell。如需詳細指示，請參閱[建立 Outlook 保護規則](create-an-outlook-protection-rule-exchange-2013-help.md)。

當建立規則，您可以指定是否使用者可以覆寫它，移除 IRM 保護或套用個規則指定不同的 AD RMS 權限原則範本。如果使用者會覆寫Outlook protection 規則所套用的 IRM 保護， Outlook 2010會在訊息中，可讓您決定使用者已覆寫規則插入`X-MS-Outlook-Client-Rule-Overridden`標頭。

## Outlook 保護規則中的述詞

Outlook 保護規則可讓您使用三個述詞，以便在 Outlook 2010 中自動套用 IRM 保護：

  - **FromDepartment**  *FromDepartment*述詞查詢寄件者的部門屬性在Active Directory和自動 IRM 保護郵件寄件者的部門符合規則中指定的部門。例如，您可以建立自動保護 Research 部門所傳送的所有郵件Outlook保護規則。

  - **SentTo**  您的組織可能需要保護郵件傳送至特定機密的收件者，例如所有公司或財務的通訊群組。您可以使用*SentTo*述詞，建立自動 IRM 保護訊息傳送給指定之收Outlook保護規則。

  - **SentToScope**  *SentToScope*述詞允許您可以建立自動 IRM 保護訊息傳送組織內外Outlook保護規則。例如，您可以使用*SentToScope*述詞與 IRM 保護的郵件傳送給內部使用者在特定部門*FromDepartment*述詞。


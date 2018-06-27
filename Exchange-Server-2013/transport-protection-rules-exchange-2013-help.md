---
title: '傳輸保護規則: Exchange 2013 Help'
TOCTitle: 傳輸保護規則
ms:assetid: 9bd6d049-165e-4e51-a79f-3b8ff409da55
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298166(v=EXCHG.150)
ms:contentKeyID: 50473843
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 傳輸保護規則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

電子郵件和附件逐漸包含等產品規格、 商務策略文件及財務資料、 商務關鍵資訊或個人識別資訊 (PII) 例如連絡人詳細資料、 社會安全編號、 信用卡號和員工記錄。有產業特有及本機規定全球的集合、 儲存及洩漏 PII 的控管的許多部分中的數目。

為了保護機密資訊，請組織建立郵件的原則提供有關如何處理這項資訊的指導方針。在MicrosoftExchange Server 2013，您可以使用傳輸保護規則來實作這些訊息原則檢查郵件內容、 加密機密電子郵件的內容，並使用版權管理控制內容的存取權。

如需管理 IRM 的相關管理工作之詳細資訊，請參閱[資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## 傳輸保護規則和 AD RMS

傳輸保護規則可讓您使用 IRM 保護的郵件傳輸規則所套用的[Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823) (AD RMS) 權限原則範本。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>AD RMS 是使用 Rights Management Service RMS 功能的應用程式及用戶端來保護機密資訊線上及離線的運作方式的資訊保護技術。若要使用 IRM 保護在內部部署Exchange部署中， Exchange 2013需要執行Windows Server 2008或更新版本的 AD RMS 的內部部署。</td>
</tr>
</tbody>
</table>


AD RMS 允許相容啟用 IRM 的應用程式將一致的保護原則套用至使用以 XML 為基礎的原則範本。中Windows Server 2008和更新版本、 AD RMS 伺服器會公開的 Web 服務，可用來列舉並取得範本。Exchange 2013附有 \[不要轉寄\] 範本。

不要轉寄範本套用至郵件、 時只收件者郵件中可以解密郵件。收件者無法將郵件轉寄給任何人、 複製郵件的內容或列印郵件。

在內部部署 AD RMS 中可建立額外的 RMS 範本，以符合組織中的權限保護需求。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果從 AD RMS 伺服器移除權限原則範本時，您必須修改使用已移除的範本任何傳輸保護規則。如果傳輸保護規則會繼續使用已移除權限原則範本、 AD RMS 伺服器將會失敗來授權任何收件者] 的內容和未傳遞回報 (NDR) 會傳遞給寄件者。<br />
Windows Server 2008和較新版本，而不是可以封存原則範本的權限中刪除。封存的範本仍可授權內容，但封存的範本時在建立或修改傳輸保護規則、 未含的範本清單中。</td>
</tr>
</tbody>
</table>


如需建立 AD RMS 範本的詳細資訊，請參閱[AD RMS 權限原則範本部署逐步指南](https://go.microsoft.com/fwlink/p/?linkid=136593)。

## 使用傳輸保護規則自動保護

包含商務關鍵資訊或 PII 訊息可以識別所使用的傳輸規則條件，包括識別例如社會安全編號的文字模式的規則運算式的組合。組織需要不同的保護層級的機密資訊。一些資訊可能會受限於員工、 承包商、 或協力廠商;雖然可能僅限於全職員工的其他資訊。所需的等級的保護可以藉由套用適當的權限原則範本套用至郵件。例如，使用者可能會標示訊息或電子郵件附件公司機密。下圖所示，您可以建立傳輸保護規則檢查郵件內容的單字"Company Confidential"，並自動 IRM 保護的郵件。

如需建立傳輸規則來強制執行權限保護的詳細資訊，請參閱[建立傳輸保護規則](create-a-transport-protection-rule-exchange-2013-help.md)。

## 持續保護電子郵件附件

使用者傳送商務關鍵資訊和 PII 中使用一般 Microsoft Office的檔案格式例如 Microsoft OfficeWord、 Excel及PowerPoint的電子郵件附件。所有這些檔案格式支援持續性的保護透過 IRM，而且您可以確保商務關鍵資訊及這些文件中的 PII 適當保護。傳輸保護規則會套用至電子郵件訊息與附件中支援的檔案格式的相同保護。

## 傳輸規則代理程式和加密代理程式

當您使用 IRM 保護的郵件根據規則條件的傳輸保護規則時上的傳輸服務的傳輸規則代理程式會檢查郵件。如果其符合所有條件及 「 無例外，它的旗標設為受 IRM 保護之訊息。加密代理程式，就會引發**OnRoutedMessage**事件的內建的傳輸代理程式實際將 IRM 保護套用至郵件。加密代理程式對只有 IRM 啟用內部郵件的郵件。如需啟用 IRM 的詳細資訊，請參閱[啟用或停用內部郵件的 IRM](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)。

傳輸服務重新啟動，並加以處理需要 IRM 加密的第一個郵件時, 加密代理程式必須能夠連線至組織中的 AD RMS 伺服器。後續訊息代理程式不需要 AD RMS 伺服器連絡。時加密郵件因為暫時性條件失敗， Exchange會重郵件試三次在 10 分鐘的時間間隔。後三重試次數，如果無法加密訊息，它不被傳遞給收件者。傳送者傳送 NDR。我們建議您在規劃您的 AD RMS 部署高可用性，確保不會影響的郵件流程。

規劃時要使用的傳輸保護規則，您必須考量您想要保護與據以建立規則規劃的資訊類型。在Exchange 2013、 傳輸規則會有大量的述詞可讓您檢查郵件內容，包括支援的附件、 訊息標頭、 寄件者和收件者地址、 部門、 通訊群組成員資格\] 和管理關係的寄件者與收件者及其Active Directory屬性。如需在Exchange 2013中可用的傳輸規則述詞的詳細資訊，請參閱[傳輸規則條件 （述詞）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)。

您也必須考慮的郵件流量在您的組織，並將使用傳輸保護規則受保護的訊息數。將 IRM 保護套用至大量郵件需要更多資源信箱伺服器上。此外，保護大量郵件還是所有郵件也會影響的用戶端經驗，特別是 Microsoft Outlook使用者。


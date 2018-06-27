---
title: '資料遺失防護: Exchange Online Help'
TOCTitle: 資料遺失防護
ms:assetid: 7c8ed3c1-ca91-4d9b-b16b-0a2b8ac89730
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150527(v=EXCHG.150)
ms:contentKeyID: 50472335
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 資料遺失防護

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

深入了解 Exchange Server 2013 和 Exchange Online 中的 DLP 原則，包括其包含項目以及如何進行測試。您也將了解 Exchange DLP 中的新功能。

因為密集使用電子郵件進行包含敏感資料的重要商務通訊，因此資料外洩防護 (DLP) 是企業通訊系統的重要議題。為實施此類資料的合規要求，並管理此類資料在電子郵件中的使用，而不阻礙員工的生產力，DLP 功能讓管理敏感資料較以往更加容易。如需 DLP 的概念概觀，請觀看下列視訊。

> [!VIDEO https://www.microsoft.com/zh-tw/videoplayer/embed/31f2b48e-93ed-4be3-b46d-e7230c0fed8f]

DLP 原則是一組簡單的套件，其中包含許多組條件，結合了您在 Exchange 系統管理中心 (EAC) 中所建立的傳輸規則、動作與例外條件，並加以啟用以篩選電子郵件訊息和附件。您可以建立一個 DLP 原則，但選擇不要啟用它。這讓您能在不影響郵件傳輸的情況下測試您的原則。DLP 原則可完全發揮現有傳輸規則的效用。事實上，在 Microsoft Exchange Server 2013 與 Exchange Online 中已建立許多新類型的傳輸規則，以達成新的 DLP 能力。傳輸規則的重要新功能之一是利用新方法分類機密資訊，此機制可整合到郵件流程處理中。這個新的 DLP 功能會透過關鍵字比對、字典比對、規則運算式評估以及其他內容檢查來執行深入的內容分析，以偵測違反組織 DLP 原則的內容。最新版的 Exchange Online 和 Exchange 2013 SP1 新增了 [文件指紋](overview-of-document-fingerprinting-in-exchange.md)，這可協助您偵測標準表單中的敏感資訊。如需傳輸規則的相關資訊，請參閱 [郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) 或 [Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\)) (Exchange Online) 和 [與傳輸規則整合敏感資訊規則](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)。您也可以使用 Exchange 管理命令介面 Cmdlet 來管理 DLP 原則。如需原則及符合性 Cmdlet 的相關資訊，請參閱[原則及符合性命令指令程式](https://technet.microsoft.com/zh-tw/library/dd298082\(v=exchg.150\))。

除了可自訂的 DLP 原則外，您還可以在電子郵件寄件者寄送違規郵件之前，通知他們可能會違反您的其中一項原則。您可以設定原則提示完成這項作業。原則提示與郵件提示相似，可經由設定在 Microsoft Outlook 2013 用戶端中呈現簡短附註，而該用戶端會向正在建立郵件的人提供可能的原則違規資訊。在最新 Exchange Online 版本和 Exchange 2013 SP1 中，原則提示也會顯示在 Outlook Web App 和 裝置的 OWA 中。如需詳細資訊，請參閱 [原則提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange Online：DLP 是付費功能，需要 Exchange Online 計劃 2 授權。如需詳細資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=286154">Exchange Online 授權</a>。<br />
Exchange 2013：DLP 是需要 Exchange 企業版用戶端存取授權 (CAL) 的高階功能。如需 CAL 和伺服器授權的詳細資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 授權</a>。<br />
<strong>Exchange Enterprise CAL with Services：</strong>如果是具有混合部署的 Exchange Enterprise CAL with Services 客戶，您會有部分信箱為內部部署，並有部分信箱在 Exchange Online 中，請注意行為差異。DLP 原則會套用於 Exchange Online 中。因此，由一位內部部署使用者傳送給另一位內部部署使用者的郵件不會套用 DLP 原則，因為郵件並未離開內部部署的基礎架構。</td>
</tr>
</tbody>
</table>


要尋找與資料外洩防護相關的管理工作嗎？請參閱 [DLP 程序](dlp-procedures-exchange-2013-help.md) (Exchange 2013) 或 [\[Exchange Online\] 的 DLP 程序](https://technet.microsoft.com/zh-tw/library/jj938003\(v=exchg.150\)) (Exchange Online)。

**目錄**

建立保護敏感資料的原則

DLP 原則中的敏感資訊類型

使用傳統郵件分類以外方式來偵測敏感資訊

使用文件指紋偵測敏感表單資料

原則提示通知使用者有關敏感內容期望

關於經 DLP 處理之郵件的資訊

安裝必要條件

相關資訊

## 建立保護敏感資料的原則

資料外洩防護功能可協助您辨識與監控您在原則條件中定義的許多敏感資訊類別，如私人識別碼或信用卡號等。您可以選擇定義您的自訂原則與傳輸規則，或是使用 Microsoft 預先定義的 DLP 原則範本以快速開始。如需更多關於所包含原則範本的資訊，請參閱[Exchange 中提供的 DLP 原則範本](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)。*原則範本*包括一系列您可以選擇的條件、規則與行動，以讓您建立並儲存能協助您檢查郵件的實際 DLP 原則。原則範本是您可以選取或建立您專屬特定規則的模組，用來建立能滿足您的資料外洩防護需求的原則。

現有供您開始使用 DLP 的三種不同方法：

1.  **套用 Microsoft 提供的開箱即用範本。**   開始使用 DLP 原則的最快方式就是使用範本來建立與執行新的原則。能省去您從無到有地建立一組新規則的許多努力。您將需要知道您要檢查哪些類型的資料，或嘗試處理哪些合規法規。您也將需要知道組織對於處理此類資料的期望。於 [Exchange 中提供的 DLP 原則範本](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md) 與 [從範本建立 DLP 原則](how-to-new-dlp-data-loss-prevention-policy-template.md) 取得更多資訊。

2.  **從您的組織外部匯入預先建立的原則檔案。**   您可以匯入已由通訊環境外部的獨立軟體廠商所建立的原則。如此，您便可以延展 DLP 解決方案來滿足業務需求。於 [來自 Microsoft 協力廠商的原則範本](policy-templates-from-microsoft-partners-exchange-2013-help.md)、[定義自己的 DLP 範本和資訊類型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md) 與 [從檔案匯入自訂的 DLP 原則範本](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md) 取得更多資訊。

3.  **不用任何既有條件來建立自訂原則。**   您的企業可能對於監控已知存於通訊系統中的特定類型資料有自己的需求。您可以靠自己完整建立一個自訂原則，以開始檢查並針對您的獨特郵件資料採取行動。您將需要知道 DLP 原則所要執行的環境有何需求與限制，以建立此類自訂原則。於[建立自訂的 DLP 原則](create-a-custom-dlp-policy-exchange-2013-help.md)取得更多資訊。

在您新增原則後，您可以檢閱與變更其規則、讓原則變為非作用中，或完全移除它。這些行動的程序於 [管理 DLP 原則](manage-dlp-policies-exchange-2013-help.md) 主題中均有提供。

## DLP 原則中的敏感資訊類型

在您建立或變更 DLP 原則時，您可以納入包含敏感資訊檢查的規則。[在 Exchange 中的敏感資訊類型外觀](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md) 主題中所列的機密資訊類型可在您的原則中使用。您在原則中建立的條件，例如在採取行動前，某個項目必須被找到的次數，或是在新自訂原則中確實被自訂的動作，以符合您的特定原則需求。如需建立 DLP 原則的相關資訊，請參閱[建立自訂的 DLP 原則](create-a-custom-dlp-policy-exchange-2013-help.md)。如需更多有關整套傳輸規則的資訊，請參閱[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) 或 [Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\)) (Exchange Online)。

為了讓您輕鬆地利用與敏感資訊相關的規則，Microsoft 提供了已包含一些敏感資訊類型的原則範本。然而您無法在原則範本中新增此處所列出的所有敏感資訊類型，因為範本設計旨在協助您把焦點放在組織中最常見的符合性相關資料的類型。如需更多有關預先內建範本的資訊，請參閱[Exchange 中提供的 DLP 原則範本](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)。您可以為組織建立許多 DLP 原則，並且將它們全數啟用，如此許多不同類型的資訊都會受到檢驗。您也可以建立一個不是以現有範本為基礎的 DLP 原則。若要開始建立此類原則，請參閱[建立自訂的 DLP 原則](create-a-custom-dlp-policy-exchange-2013-help.md)。如需更多有關敏感資訊類型的資訊，請參閱[在 Exchange 中的敏感資訊類型外觀](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)。

## 使用文件指紋偵測敏感表單資料

使用 Exchange 2013 SP1 和最新的 Exchange Online 版本，您可以使用[文件指紋](overview-of-document-fingerprinting-in-exchange.md)，根據標準表單輕鬆地建立敏感資訊類型。若要了解如何保護表單資料，請參閱[保護含有文件指紋的表單資料](protect-form-data-with-document-fingerprinting-exchange-2013-help.md)。

## 原則提示通知使用者有關敏感內容期望

您可以使用原則提示通知訊息，通知電子郵件寄件者在撰寫電子郵件訊息時可能會遭遇的規範符合性問題。在 DLP 原則中設定原則提示時，只有當寄件者的電子郵件訊息內容符合您原則中所描述條件時，才會顯示通知訊息。原則提示與在 Microsoft Exchange 2010 中引進的郵件提示相似。如需詳細資訊，請參閱[原則提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)。

## 使用傳統郵件分類以外方式來偵測敏感資訊

與其他傳統郵件分類相比，Exchange 2013 與 Exchange Online 呈現了更能協助您管理郵件和附件資料的方法。DLP 解決方案效力的關鍵因素便是能正確辨識對組織、法規需求、地理位置或其他業務需求而言特有的機密或敏感內容的能力。Exchange 2013 能透過使用新的深入內容分析結構，加上您透過您在 DLP 原則中的規則所建立的偵測標準來達成此目的。在 Exchange 2013 中協助防止資料遺失是仰賴一組正確的敏感資訊規則，如此這些規則才能提供高度的保護，同時將因誤判與誤報所產生的不適當郵件流程中斷減到最小。這些類型的規則被視為整個 DLP 資訊的敏感資訊偵測，在傳輸規則所提供的架構中運作，以啟用 DLP 能力。

若要深入了解這些新功能，請參閱[與傳輸規則整合敏感資訊規則](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)。傳統的郵件分類欄位仍可套用於 Exchange 中的郵件，而這些能與新的敏感資訊偵測在單一的 DLP 原則中結合，或是同時運作，如此它們便能在 Exchange 中獨立進行評估。若要瞭解更多有關傳統 Exchange 2010 郵件分類的資訊，請參閱 TechNet 文件庫中的[瞭解訊息分類](https://go.microsoft.com/fwlink/?linkid=266612)。

## 關於經 DLP 處理之郵件的資訊

若要讓 Exchange 2013 取得在您環境中有關郵件與 DLP 原則偵測的資訊，請參閱 [檢視 DLP 原則偵測報告](view-dlp-policy-detection-reports-exchange-2013-help.md)和[建立 DLP 原則偵測附隨報告](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)。與 DLP 偵測相關的資料，已高度整合到 Exchange 2013 的傳遞回報郵件追蹤工具中。

針對 Exchange Online，請參閱 [檢視 \[Exchange Online\] 的 DLP 原則偵測報告](https://technet.microsoft.com/zh-tw/library/dn904484\(v=exchg.150\)) 和 [建立 \[Exchange Online\] 的 DLP 原則偵測附隨報告](https://technet.microsoft.com/zh-tw/library/dn904486\(v=exchg.150\))。

## 安裝必要條件

若要利用 DLP 功能，您必須設定 Exchange 2013 或 Exchange Online 至少具有一個寄件者信箱。資料外洩防護是付費功能，需要企業版用戶端存取授權 (CAL)。如需開始使用 Exchange 2013 的詳細資訊，請參閱[規劃及部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)。如需開始使用 Exchange Online 的詳細資訊，請參閱[Exchange Online](https://technet.microsoft.com/zh-tw/library/jj200580\(v=exchg.150\))。

## 相關資訊

Exchange 2013

  - [郵件原則及符合性](messaging-policy-and-compliance-exchange-2013-help.md)

  - [DLP 程序](dlp-procedures-exchange-2013-help.md)

  - [檢視 DLP 原則偵測報告](view-dlp-policy-detection-reports-exchange-2013-help.md)

  - [文件指紋](overview-of-document-fingerprinting-in-exchange.md)

  - [原則及符合性命令指令程式](https://technet.microsoft.com/zh-tw/library/dd298082\(v=exchg.150\))

Exchange Online

  - [安全性及規範的 Exchange Online](https://technet.microsoft.com/zh-tw/library/jj200706\(v=exchg.150\))

  - [\[Exchange Online\] 的 DLP 程序](https://technet.microsoft.com/zh-tw/library/jj938003\(v=exchg.150\))

  - [檢視 \[Exchange Online\] 的 DLP 原則偵測報告](https://technet.microsoft.com/zh-tw/library/dn904484\(v=exchg.150\))

  - [文件指紋](overview-of-document-fingerprinting-in-exchange.md)


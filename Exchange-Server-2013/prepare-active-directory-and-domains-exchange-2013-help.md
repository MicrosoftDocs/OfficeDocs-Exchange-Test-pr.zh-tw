---
title: '準備 Active Directory 及網域: Exchange 2013 Help'
TOCTitle: 準備 Active Directory 及網域
ms:assetid: f895e1ce-d766-4352-ac46-ec959c9954a9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125224(v=EXCHG.150)
ms:contentKeyID: 50474627
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 準備 Active Directory 及網域

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

在安裝 Microsoft Exchange Server 2013 之前，您需要準備 Active Directory 樹系及其網域。Exchange 需要準備 Active Directory，以便儲存使用者信箱的相關資訊及組織中的 Exchange 伺服器組態。如果您不熟悉 Active Directory 樹系或網域，請參閱＜[Active Directory 網域服務概觀](https://go.microsoft.com/fwlink/p/?linkid=399226)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不論這是您第一次在環境中安裝 Exchange，或是您已經有舊版的 Exchange Server 正在執行，您需要準備適用於 Exchange 2013 的 Active Directory。您可以參閱 <a href="exchange-2013-active-directory-schema-changes-exchange-2013-help.md">Exchange 2013 Active Directory 架構變更</a>以取得 Exchange 2013 新增至 Active Directory 的新架構類別與屬性的詳細資料，包括 Service Packs (SP) 和 累積更新 (CU) 所做的變更。</td>
</tr>
</tbody>
</table>


有幾種方法可以為 Exchange 準備 Active Directory。第一種是讓 Exchange 2013 安裝精靈為您準備。如果您沒有大型的 Active Directory 部署，也沒有獨立的團隊來管理 Active Directory，則建議使用精靈。您使用的帳戶必須同時為 Schema Admins 與 Enterprise Admins 安全性群組的成員。如需有關如何使用安裝精靈的詳細資訊，請參閱＜[使用安裝精靈安裝 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)＞。

如果有您大型的 Active Directory 部署，或有獨立的團隊來管理 Active Directory，則此主題適合您。遵循本主題的步驟進行可讓您充分掌控每一個準備階段，以及每個步驟的執行人員。例如，Exchange 系統管理員可能沒有擴充 Active Directory 架構所需的權限。

開始之前有哪些須知？

1\. 擴充 Active Directory 架構

2\. 準備 Active Directory

3\. 準備 Active Directory 網域

如何知道這是否正常運作？

想要了解為 Exchange 準備 Active Directory 的情形嗎？請參閱[當 Exchange 2013 安裝好之後，Active Directory 會有什麼變更？](what-changes-in-active-directory-when-exchange-2013-is-installed-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：10-15 分鐘或更久 (不包括 Active Directory 複寫)，視組織規模和子網域數目而定。

  - 您用來執行這些步驟的電腦必須符合 [Exchange 2013 系統需求](exchange-2013-system-requirements-exchange-2013-help.md)。此外，Active Directory 樹系也必須符合＜[Exchange 2013 系統需求](exchange-2013-system-requirements-exchange-2013-help.md)＞的＜網路及目錄伺服器＞一節中的需求。

  - 如果組織有多個 Active Directory 網域，則建議如下：
    
      - 從每個網域中具有 Active Directory 伺服器的 Active Directory 站台執行下列命令。
    
      - 從每個網域中，在具有可寫入通用類別目錄伺服器的 Active Directory 站台安裝第一個 Exchange 伺服器。

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


## 1\. 擴充 Active Directory 架構

讓組織開始使用 Exchange 2013 的第一步是擴充 Active Directory 架構。Exchange 會將許多資訊儲存在 Active Directory 中，但在此之前，需要先加入和更新類別、屬性及其他項目。如果想要了解擴充架構時所發生的變更，請參閱＜[Exchange 2013 Active Directory 架構變更](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)＞。

擴充架構之前，請謹記下列事項：

  - 您的登入帳戶必須為 Schema Admins 和 Enterprise Admins 安全性群組的成員。

  - 您用來執行命令以擴充架構的電腦，必須與架構主機位於相同的 Active Directory 網域和站台。

  - 如果您使用 *DomainController* 參數，務必使用作為架構主機的網域控制站名稱。

  - 擴充 Exchange 架構的唯一方法是使用本主題中的步驟，或使用 Exchange 2013 安裝程式。不支援以其他方法來擴充架構。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您沒有獨立的團隊來管理 Active Directory 架構，請略過此步驟，直接進入準備 Active Directory。如果在步驟 1 中未擴充架構，則步驟 2 的命令會為您擴充架構。如果決定略過步驟 1，您仍然必須謹記上述資訊。</td>
</tr>
</tbody>
</table>


準備好時，請執行下列動作來擴充 Active Directory 架構。如果您有多個 Active Directory 樹系，請確定您登入正確的樹系。

1.  請確定電腦可執行 Exchange 2013 安裝程式。如需有關執行安裝程式的需求，請參閱＜[Exchange 2013 必要條件](exchange-2013-prerequisites-exchange-2013-help.md)＞的＜[Active Directory preparation](exchange-2013-prerequisites-exchange-2013-help.md)＞一節。

2.  開啟 Windows 命令提示字元視窗，移至您已下載 Exchange 安裝檔案的位置。

3.  執行下列命令來擴充架構。
    
        Setup.exe /PrepareSchema /IAcceptExchangeServerLicenseTerms

當安裝程式擴充架構完成之後，您需要稍候讓 Active Directory 將變更複寫到所有網域控制站。如果想要查看複寫進度，您可以使用 `repadmin` 工具。Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 的 `Repadmin` 網域服務工具中包含 Active Directory。如需此工具用法的詳細資訊，請參閱 [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879)。

## 2\. 準備 Active Directory

現在已擴充 Active Directory 架構，您可以為 Exchange 2013 準備其他的 Active Directory 部分。在此步驟中，Exchange 會在用來儲存資訊的 Active Directory 中建立容器、物件和其他項目。所有 Exchange 容器、物件、屬性等，統稱為*「Exchange 組織」*。

在為 Exchange 準備 Active Directory 之前，請謹記下列事項：

  - 您的登入帳戶必須是 Enterprise Admins 安全性群組的成員。如果您因為要讓 *PrepareAD* 命令擴充架構而略過步驟 1，則您使用的帳戶也必須是 Schema Admins 安全性群組的成員。

  - 您用來執行命令的電腦必須與架構主機位於相同的 Active Directory 網域和站台。此電腦也必須以 TCP 連接埠 389 來連接樹系中的所有網域。

  - 請耐心等候，直到 Active Directory 將步驟 1 所做的變更複寫到所有網域控制站之後，再執行此步驟。

當您執行下列命令來為 Exchange 準備 Active Directory 時，您必須命名 Exchange 組織。此名稱專供 Exchange 內部使用，使用者通常無法看到內容。安裝 Exchange 的公司名稱通常作為組織名稱。您使用的名稱不影響 Exchange 的功能，也不會決定您可使用的電子郵件地址。您可以選擇任何您想要的名稱，但請注意下列事項：

  - 您可以使用 A 到 Z 的任何大寫或小寫字母。

  - 您可以使用 0 到 9 的數字。

  - 名稱可以包含空格，但名稱開頭或結尾不能為空格。

  - 您可以在名稱中使用連字號或破折號。

  - 名稱最多 64 個字元，但不能為空白。

  - 設定名稱之後就無法變更。

準備好時，請執行下列動作來為 Exchange 準備 Active Directory。如果您要使用的組織名稱有空格，請以雙引號 (") 括住名稱。

1.  開啟 Windows 命令提示字元視窗，移至您已下載 Exchange 安裝檔案的位置。

2.  執行下列命令：
    
        Setup.exe /PrepareAD /OrganizationName:"<organization name>" /IAcceptExchangeServerLicenseTerms

當安裝程式為 Exchange 準備好 Active Directory 之後，您需要稍候讓 Active Directory 將變更複寫到所有網域控制站。如果想要查看複寫進度，您可以使用 `repadmin` 工具。Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 的 Active Directory 網域服務工具中包含 `repadmin`。如需有關如何使用此工具的詳細資訊，請參閱 [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879)。

## 3\. 準備 Active Directory 網域

為 Exchange 準備好 Active Directory 的最後一步是準備每一個 Active Directory 網域，其中將安裝 Exchange 或放置啟用郵件功能的使用者。此步驟會建立其他容器和安全性群組，並設定權限讓 Exchange 可以存取它們。

如果您的 Active Directory 樹系中有多個網域，則您有許多選擇可準備它們。請選取與您的目的相符的選項。如果您只有一個網域，則可以略過此步驟，因為步驟 2 中的 *PrepareAD* 命令已為您準備好網域。

## 準備我的 Active Directory 樹系中的所有網域

若要準備您的所有 Active Directory 網域，您可以在執行安裝程式時使用 *PrepareAllDomains* 參數。安裝程式會在您的 Active Directory 樹系中準備 Exchange 的每一個網域。

在準備您的 Active Directory 樹系中的所有網域之前，請謹記下列事項：

  - 您使用的帳戶必須是 Enterprise Admins 安全性群組的成員。

  - 等待 Active Directory 將步驟 2 中所做的變更複寫到您的所有網域控制站。如果您不等待，則嘗試準備網域時可能會發生錯誤。

備妥之後，請執行下列動作，為 Exchange 準備好 Active Directory 樹系中的所有網域。

1.  開啟 Windows 命令提示字元視窗，移至您已下載 Exchange 安裝檔案的位置。

2.  執行下列命令：
    
        Setup.exe /PrepareAllDomains /IAcceptExchangeServerLicenseTerms

## 讓我選擇想要準備的 Active Directory 網域

如果您要選擇想要準備的 Active Directory 網域，您可以在執行安裝程式時使用 *PrepareDomain* 參數。使用 *PrepareDomain* 參數時，必須包含您要準備的網域的完整網域名稱 (FQDN)。

在準備您的 Active Directory 樹系中的網域之前，請謹記下列事項：

  - 您使用的帳戶需要權限，視網域何時建立而定。
    
      - **PrepareAD 執行之前建立網域**   如果網域是在您於上述步驟 2 中執行 *PrepareAD* 命令**之前**建立，則您使用的帳戶必須是您要準備的網域中的 Domain Admins 群組的成員。
    
      - **PrepareAD 執行之後建立網域**   如果網域是在您於上述步驟 2 中執行 *PrepareAD* 命令**之後**建立，則您使用的帳戶必須是您要準備的網域中的 1)「組織管理」角色群組的成員和 2) Domain Admins 群組的成員。

  - 等待 Active Directory 將步驟 2 中所做的變更複寫到您的所有網域控制站。如果您不等待，則嘗試準備網域時可能會發生錯誤。

  - 您需要準備每一個將安裝 Exchange 伺服器的網域。您也需要準備任何將包含啟用郵件功能之使用者的網域，即使這些網域不會包含任何 Exchange 伺服器也一樣。

  - 您不需要在已執行 *PrepareAD* 命令的網域中執行 *PrepareDomain* 命令。*PrepareAD* 命令會自動準備該網域。

備妥之後，請執行下列動作，為 Exchange 準備好 Active Directory 樹系中的個別網域。

1.  開啟 Windows 命令提示字元視窗，移至您已下載 Exchange 安裝檔案的位置。

2.  執行下列命令。包含您要準備的網域的 FQDN。如果要準備您正在執行命令的網域，您不需要包含 FQDN。
    
        Setup.exe /PrepareDomain:<FQDN of the domain you want to prepare> /IAcceptExchangeServerLicenseTerms

3.  對於您將安裝 Exchange 伺服器或放置啟用郵件功能之使用者的每一個 Active Directory 網域，重複這些步驟。

## 如何知道這是否正常運作？

完成上述所有步驟之後，您可以檢查來確定一切已順利進行。若要這麼做，您需要使用一個稱為 Active Directory 服務介面編輯器 (ADSI 編輯器) 的工具。在 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 中，ADSI 編輯器隨附於 Active Directory 網域服務工具功能中。如需此工具的詳細資訊，請參閱＜[ADSI 編輯器 (adsiedit.msc)](https://go.microsoft.com/fwlink/p/?linkid=294644)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>除非得到 Microsoft 技術支援人的指示，否則請勿在 ADSI 編輯器中變更任何值。在 ADSI 編輯器中變更任何值可能對 Exchange 組織和 Active Directory 造成無法彌補的損害。</td>
</tr>
</tbody>
</table>


在 Exchange 延伸您的 Active Directory 結構描述，並為 Exchange 準備 Active Directory 之後，數個屬性會更新以顯示準備已完成。請使用下列清單中的資訊，確定這些屬性的值正確。每個屬性必須符合下表中您所安裝之 Exchange 2013 版本的值。

  - 在 **\[架構\]** 命名內容中，確認 **ms-Exch-Schema-Verision-Pt** 上的 **rangeUpper** 屬性，已設為＜Exchange 2013 Active Directory 版本＞表格中您的 Exchange 2013 版本所顯示的值。
    
     

  - 在 **\[設定\]** 命名內容中，確認 CN=\<*您的組織*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*網域*\> 容器中的 **objectVersion** 屬性，已設為＜Exchange 2013 Active Directory 版本＞表格中您的 Exchange 2013 版本所顯示的值。
    
     

  - 在 **\[預設\]** 命名內容中，確認 DC=\<*根網域* 下 \[Microsoft Exchange 系統物件\] 容器中的 **objectVersion** 內容，已設為＜Exchange 2013 Active Directory 版本＞表格中您的 Exchange 2013 版本所顯示的值。
    
     

您也可以檢查 Exchange 安裝記錄檔，確認 Active Directory 準備已成功完成。如需詳細資訊，請參閱 [確認 Exchange 2013 安裝](verify-an-exchange-2013-installation-exchange-2013-help.md)。除非在 Active Directory 站台中完成至少一個 Mailbox server role 和一個 Client Access server role 的安裝，否則無法使用＜[確認 Exchange 2013 安裝](verify-an-exchange-2013-installation-exchange-2013-help.md)＞主題中提及的 **Get-ExchangeServer** 指令程式。

## Exchange 2013 Active Directory 版本

下表顯示每次安裝新版本的 Exchange 2013 時，Active Directory 中會更新的 Exchange 2013 物件。您可以比較看到的物件版本和下表中的值，確認您安裝的 Exchange 2013 版本已在安裝期間順利更新 Active Directory。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>Exchange 版本</th>
<th>rangeUpper</th>
<th>objectVersion</th>
<th>objectVersion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>命名內容</strong></p></td>
<td><p> </p></td>
<td><p>Schema</p></td>
<td><p>Default</p></td>
<td><p>Configuration</p></td>
</tr>
<tr class="even">
<td><p><strong>容器</strong></p></td>
<td><p> </p></td>
<td><p>ms-Exch-Schema-Version-Pt</p></td>
<td><p>Microsoft Exchange 系統物件</p></td>
<td><p>CN=&lt;<em>your organization</em>&gt;, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=&lt;<em>domain</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU10 和更新版本</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>16130</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU9</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU8</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU7</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU6</p></td>
<td><p>15303</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU5</p></td>
<td><p>15300</p></td>
<td><p>13236</p></td>
<td><p>15870</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 SP1</p></td>
<td><p>15292</p></td>
<td><p>13236</p></td>
<td><p>15844</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU3</p></td>
<td><p>15283</p></td>
<td><p>13236</p></td>
<td><p>15763</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 CU2</p></td>
<td><p>15281</p></td>
<td><p>13236</p></td>
<td><p>15688</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU1</p></td>
<td><p>15254</p></td>
<td><p>13236</p></td>
<td><p>15614</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 RTM</p></td>
<td><p>15137</p></td>
<td><p>13236</p></td>
<td><p>15449</p></td>
</tr>
</tbody>
</table>


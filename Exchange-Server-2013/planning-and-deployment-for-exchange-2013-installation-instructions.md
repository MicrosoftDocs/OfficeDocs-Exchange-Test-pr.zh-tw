---
title: '規劃及部署: Exchange 2013 Help'
TOCTitle: 規劃及部署
ms:assetid: 692c59e3-f0b0-4cef-a66e-751aa740abae
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998636(v=EXCHG.150)
ms:contentKeyID: 50473390
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 規劃及部署

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

您需要執行 Exchange 安裝的指引嗎？本文提供規劃和部署 Microsoft Exchange Server 2013 的指引，以及您在部署期間將需要的文章連結。

下列區段包含規劃和部署 Microsoft Exchange Server 2013 相關資訊的連結。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>請務必先閱讀 <a href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange 2013 版本資訊</a>主題，然後再開始部署。版本資訊包含部署期間和之後可能遇到的問題的重要相關資訊。</td>
</tr>
</tbody>
</table>


**目錄**

規劃 Exchange 2013

部署 Exchange 2013 的安裝

瞭解 Exchange 2013 安裝程式

相關資訊

## 規劃 Exchange 2013

使用以下連結存取資訊以協助您規劃如何在您的組織中部署 Exchange Server 2013。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需有關在測試環境中安裝 Exchange 2013 的相關資訊，請參閱本主題稍後的建立測試環境。</td>
</tr>
</tbody>
</table>


  - [Mailbox 和 Client Access server](mailbox-and-client-access-servers-exchange-2013-help.md)  
    瞭解 Exchange 2013 中所包含的信箱和用戶端存取伺服器角色。

<!-- end list -->

  - [Exchange 2013 系統需求](exchange-2013-system-requirements-exchange-2013-help.md)  
    瞭解在您安裝 Exchange 2013 前，您的組織必須滿足的系統需求。

<!-- end list -->

  - [Exchange 2013 必要條件](exchange-2013-prerequisites-exchange-2013-help.md)  
    瞭解 Windows Server 2008 R2 Service Pack 1 (SP1) 或 Windows Server 2012 功能與其他需要安裝的軟體，以成功安裝 Exchange 2013。

<!-- end list -->

  - [Exchange Server 部署助理](exchange-server-deployment-assistant-exchange-2013-help.md)  
    使用此工具來產生可用於規劃、安裝或升級至 Exchange 2013 的自訂檢查清單。有多個案例的指導可用，包括內部部署、混合或雲端部署。

<!-- end list -->

  - [Active Directory](active-directory-exchange-2013-help.md)  
    閱讀此主題以瞭解 Exchange 2013 如何使用 Active Directory ，以及您的 Active Directory 部署如何影響您的 Exchange 部署。

<!-- end list -->

  - [反惡意程式防護](anti-malware-protection-exchange-2013-help.md)  
    閱讀此主題以了解 Exchange 2013 的反惡意程式碼保護選項。

<!-- end list -->

  - [Exchange Server 混合部署](https://technet.microsoft.com/zh-tw/library/jj200581\(v=exchg.150\))  
    閱讀此主題以協助您使用 Microsoft Office 365 來規劃混合部署與您的內部部署 Exchange 2013 組織。

<!-- end list -->

  - [規劃高可用性及站台恢復](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
    閱讀此主題以協助您進行規劃，滿足高可用性和運作持續性需求。

<!-- end list -->

  - [與 SharePoint 和 Lync 整合](integration-with-sharepoint-and-lync-exchange-2013-help.md)  
    閱讀此主題瞭解整合 Exchange 2013、Microsoft SharePoint 2013 和 Microsoft Lync 2013，以啟用跨產品封存、保留和 eDiscovery；站台信箱；驗證； Lync 顯示狀態及更多內容。

<!-- end list -->

  - [整合通訊的規劃](planning-for-unified-messaging-exchange-2013-help.md)  
    閱讀此主題瞭解更多有關 Exchange 2013 整合通訊的規劃。

<!-- end list -->

  - [Exchange 2013 儲存裝置組態選項](exchange-2013-storage-configuration-options-exchange-2013-help.md)  
    閱讀此主題瞭解有關儲存架構、磁碟類型和由 Exchange 2013 信箱伺服器所支持的儲存設定。

<!-- end list -->

  - [Exchange 2013 虛擬化](exchange-2013-virtualization-exchange-2013-help.md)  
    閱讀本主題，以深入了解如何在虛擬化環境中部署 Exchange 2013。

<!-- end list -->

  - [Exchange 2013 中的多重租賃](multi-tenancy-in-exchange-2013-exchange-2013-help.md)  
    請閱讀本主題，以深入了解如何設定 Exchange 2013 來主控多個分離的組織或業務單位，它們通常不共用電子郵件、資料、全域通訊清單 (GAL) 或其他常用的 Exchange 物件。

<!-- end list -->

  - [Exchange 開發技術](https://go.microsoft.com/fwlink/p/?linkid=268448)  
    本主題包含有關應用程式發展介面(API) 之重要資訊的連結，這些介面可用於使用 Exchange 2013 的應用程式。

## 建立測試環境

在第一次安裝 Exchange 2013 之前，建議您在隔離的測試環境中安裝它。此方法可以降低使用者停機的風險以及對實際生產環境的負面影響。

在部署到實際生產環境之前，測試環境將當做新 Exchange 2013 設計的「概念證明」，並且能夠繼續或回復任何實作。具備驗證和測試的專有測試環境可讓您針對未來的實際生產進行預先安裝檢查。透過先在測試環境中進行安裝，我們相信您的組織在完整的生產實作中，成功的可能性更高。

對於許多組織而言，建置測試實驗室的成本可能因為需要複製實際生產環境而相當高。若要降低與原型實驗室關聯的硬體成本，建議透過 Windows Server 2008 R2 或 Windows Server 2012 Hyper-V 技術來使用虛擬化。Hyper-V 允許伺服器虛擬化，可讓多個虛擬作業系統在單一的實體電腦上執行。

如需更多有關 Hyper-V 的詳細資訊，請參閱 [伺服器虛擬化](https://go.microsoft.com/fwlink/p/?linkid=117704)。如需 Microsoft 對於實際執行之硬體虛擬化軟體的 Exchange 2013 支援，請參閱 [Exchange 2013 系統需求](exchange-2013-system-requirements-exchange-2013-help.md) 中的＜硬體虛擬化＞。

## 部署 Exchange 2013 的安裝

部署階段就是指將 Exchange 2013 安裝您組織的階段。開始部署階段之前，您應該先規劃 Exchange 組織。如需詳細資訊，請參閱本主題之前的規劃 Exchange 2013一節。

使用下列連結即可存取必要資訊，以協助您部署 Exchange 2013。

  - [準備 Active Directory 及網域](prepare-active-directory-and-domains-exchange-2013-help.md)  
    瞭解您所須採取的步驟，以準備 Exchange 2013 的 Active Directory 樹系，以及 Exchange 對您的樹系所進行的變更。

<!-- end list -->

  - [使用安裝精靈安裝 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)  
    遵循此主題中的步驟，使用 Exchange 2013 設定精靈將 Exchange 2013 安裝入新的 Exchange 組織。

<!-- end list -->

  - [使用自動模式安裝 Exchange 2013](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)  
    遵循此主題中的步驟，使用 Exchange 2013 自動安裝將 Exchange 2013 安裝入新的 Exchange 組織。

<!-- end list -->

  - [使用設定精靈安裝 Exchange 2013 Edge Transport role](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md)  
    遵循此主題中的步驟，使用 Exchange 2013 安裝精靈將 Exchange 2013 Edge Transport role 安裝到周邊網路。

<!-- end list -->

  - [將 Exchange 2013 升級至最新的累計或服務套件](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)  
    請遵循本主題的步驟，將最新的累計更新或服務套件套用至組織中的 Exchange 2013 伺服器。

<!-- end list -->

  - [從 Exchange 2010 升級至 Exchange 2013](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)  
    請遵循本主題的步驟，將 Exchange 2013 安裝到現有的 Exchange 2010 組織。

<!-- end list -->

  - [從 Exchange 2007 升級至 Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md)  
    請遵循本主題的步驟，將 Exchange 2013 安裝到現有的 Exchange 2007 組織。

<!-- end list -->

  - [部署 Exchange 2013 的多個樹系拓撲](deploy-multiple-forest-topologies-for-exchange-2013-exchange-2013-help.md)  
    請閱讀本主題的資訊，協助您在包含多個 Active Directory 樹系的組織中部署 Exchange 2013。

<!-- end list -->

  - [部署語音信箱和 UM](deploying-voice-mail-and-um-exchange-2013-help.md)  
    關於可幫助您了解部署 Exchange 2013 整合通訊 (不論是新部署或升級) 的資訊，請閱讀本主題。

<!-- end list -->

  - [混合式部署程序](https://technet.microsoft.com/zh-tw/library/jj200788\(v=exchg.150\))  
    閱讀此主題取得能協助您在現有混合部署中部署 Exchange 2013 的資訊。

<!-- end list -->

  - [Exchange 2013 後續安裝工作](exchange-2013-post-installation-tasks-exchange-2013-help.md)  
    瞭解後續安裝工作以完成您的 Exchange 2013 安裝。

## 瞭解 Exchange 2013 安裝程式

您可以使用不同類型和模式的 Exchange 2013 安裝程式，來安裝及維護各種版本的 Exchange 2013。

## Exchange 版本

Exchange 2013 有兩種伺服器版本：Standard Edition 及 Enterprise Edition。這些都是由產品金鑰所定義的授權版本。如需詳細資訊，請參閱 [Exchange 伺服器授權](https://go.microsoft.com/fwlink/p/?linkid=237292)。

## Exchange 安裝程式的類型

對於 Exchange 2013 安裝程式您可以使用下列選項：

  - **Exchange 安裝程式 UI**   不以任何命令列參數執行 Setup.exe ，可提供您由 Exchange 2013 安裝程式精靈所引導的互動式體驗。

  - **Exchange 自動安裝**   以命令列參數執行 Setup.exe，讓您可從互動式命令列或透過指令碼來安裝 Exchange。

Setup.exe 可以從 Exchange 2013 DVD 或下載的來源檔案取得。

## Exchange 安裝程式的模式

Exchange 2013 安裝程式包含數個安裝模式：

  - **Install**   當您安裝新伺服器角色或將伺服器角色新增到現有的安裝 (維護模式) 時，會使用這個模式。您可以從 Exchange 安裝精靈和自動安裝使用此模式。

  - **解除安裝**   當您移除電腦中的 Exchange 安裝時，請使用此模式。您可以從 Exchange 安裝精靈和自動安裝使用此模式。

  - **升級**   如果您已安裝 Exchange，而且正在安裝累計更新或服務套件，請選取此模式。您可以從 Exchange 安裝精靈和自動安裝使用此模式。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Exchange 2013 不支援從舊版 Exchange 就地升級。此模式僅可用於安裝累計更新或服務套件。</td>
    </tr>
    </tbody>
    </table>


  - **RecoverServer** 如果伺服器出現災難性的失敗，且您需要復原資料，請使用此模式。您必須使用與失敗伺服器相同的完整網域名稱 (FQDN) 來安裝伺服器，然後使用 **/m:RecoverServer** 參數執行安裝程式。不必指定要還原的角色。安裝程式會偵測 Active Directory 中的 Exchange 伺服器物件，並自動安裝對應的檔案和組態。復原伺服器之後，便可以還原資料庫並重新設定其他任何設定。若要以 **RecoverServer** 模式執行，則不能在伺服器上安裝 Exchange。Active Directory 中必須有 Exchange Server 物件。您只能在自動安裝期間使用此模式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在您可以使用其他模式之前，必須先完成某一種安裝模式。</td>
</tr>
</tbody>
</table>


## 相關資訊

[Exchange 2013 中的 IPv6 支援](ipv6-support-in-exchange-2013-exchange-2013-help.md)

[Exchange 2013 中的 Exchange 系統管理中心](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)

[Exchange 2013 語言支援](exchange-2013-language-support-exchange-2013-help.md)

[Exchange 2013 整備檢查](exchange-2013-readiness-checks-exchange-2013-help.md)


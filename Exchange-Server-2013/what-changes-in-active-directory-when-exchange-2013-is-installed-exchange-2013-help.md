---
title: '當 Exchange 2013 安裝好之後，Active Directory 會有什麼變更？: Exchange 2013 Help'
TOCTitle: 當 Exchange 2013 安裝好之後，Active Directory 會有什麼變更？
ms:assetid: 07386078-6103-49a2-8698-2d41db9cec95
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn750898(v=EXCHG.150)
ms:contentKeyID: 62371332
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 當 Exchange 2013 安裝好之後，Active Directory 會有什麼變更？

 

_**適用版本：**Exchange Server, Exchange Server 2013_

_**上次修改主題的時間：**2014-05-26_

安裝 Exchange 2013 時會變更 Active Directory 樹系和網域。Exchange 這樣做是為了儲存組織中的 Exchange 伺服器、信箱和 Exchange 相關的其他物件的相關資訊。當您執行 Exchange 2013 安裝精靈時，或在 Exchange 2013 命令列安裝期間執行 *PrepareSchema*、*PrepareAD* 和 *PrepareDomains* 命令時 (關於如何使用這些命令，請參閱＜[準備 Active Directory 及網域](prepare-active-directory-and-domains-exchange-2013-help.md)＞)，將會為您完成這些變更。如果想要了解 Exchange 對 Active Directory 所做的變更，請參閱本主題。其中說明 Exchange 在準備 Active Directory 的每一個步驟中所執行的動作。

為 Exchange 準備 Active Directory 需要完成三個步驟：

  - Extend the Active Directory schema

  - Prepare Active Directory containers, objects, and other items

  - Prepare Active Directory domains

三個步驟都完成之後，Active Directory 樹系即可供 Exchange 2013 使用。請參閱＜[使用安裝精靈安裝 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)＞，以深入了解如何安裝 Exchange 2013。

## 擴充 Active Directory 架構

擴充 Active Directory 架構會加入和更新類別、屬性及其他項目。需要進行這些變更，Exchange 才能建立容器和物件來儲存 Exchange 組織的相關資訊。因為 Exchange 會大幅變更 Active Directory 架構，另有專門的主題討論此步驟。若要了解對架構所做的一切變更，請參閱＜[Exchange 2013 Active Directory 架構變更](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)＞。

在 Active Directory 樹系的第一個 Exchange 2013 伺服器上執行 Exchange 2013 安裝精靈時會自動執行此步驟。當您在樹系中的第一個 Exchange 2013 伺服器上搭配 *PrepareSchema* 命令 (或選擇性地搭配 *PrepareAD* 命令) 來執行 Exchange 2013 命令列安裝時，也會執行此步驟。如需有關如何擴充架構的詳細資訊，請參閱＜[準備 Active Directory 及網域](prepare-active-directory-and-domains-exchange-2013-help.md)＞中的＜[Extend the Active Directory schema](prepare-active-directory-and-domains-exchange-2013-help.md)＞。

Exchange 完成擴充架構之後會設定架構版本，此資訊儲存在 **ms-Exch-Schema-Version-Pt** 屬性中。如果想要確定 Active Directory 架構已成功擴充，您可以檢查此屬性中儲存的值。如果屬性中的值符合您安裝的 Exchange 2013 版本所列出的架構版本，則表示擴充架構成功。如需 Exchange 版本的清單及如何檢查此屬性的值，請參閱＜[準備 Active Directory 及網域](prepare-active-directory-and-domains-exchange-2013-help.md)＞的＜[How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md)＞一節。

## 準備 Active Directory 容器、物件和其他項目

擴充架構後，下一步是在 Active Directory 中加入供 Exchange 用來儲存資訊的所有容器、物件、屬性和其他項目。此步驟所做的大部分變更會套用至整個 Active Directory 樹系。安裝期間執行 *PrepareAD* 命令的本機 Active Directory 網域會發生小部分變更。

以下是對 Active Directory 樹系所做的變更：

  - 在 CN=Services,CN=Configuration,DC=\<*根網域*\> 下建立 Microsoft Exchange 容器 (若尚未存在)。

  - 在 CN=\<*組織名稱*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*根網域*\> 下建立下列容器和物件 (若尚未存在)：
    
      - CN=Address Lists Container
    
      - CN=AddressBook Mailbox Policies
    
      - CN=Addressing
    
      - CN=Administrative Groups
    
      - CN=Approval Applications
    
      - CN=Auth Configuration
    
      - CN=Availability Configuration
    
      - CN=Client Access
    
      - CN=Connections
    
      - CN=ELC Folders Container
    
      - CN=ELC Mailbox Policies
    
      - CN=ExchangeAssistance
    
      - CN=Federation
    
      - CN=Federation Trusts
    
      - CN=Global Settings
    
      - CN=Hybrid Configuration
    
      - CN=Mobile Mailbox Policies
    
      - CN=Mobile Mailbox Settings
    
      - CN=Monitoring Settings
    
      - CN=OWA Mailbox Policies
    
      - CN=Provisioning Policy Container
    
      - CN=Push Notification Settings
    
      - CN=RBAC
    
      - CN=Recipient Policies
    
      - CN=Remote Accounts Policies Container
    
      - CN=Retention Policies Container
    
      - CN=Retention Policy Tag Container
    
      - CN=ServiceEndpoints
    
      - CN=System Policies
    
      - CN=Team Mailbox Provisioning Policies
    
      - CN=Transport Settings
    
      - CN=UM AutoAttendant Container
    
      - CN=UM DialPlan Container
    
      - CN=UM IPGateway Container
    
      - CN=UM Mailbox Policies
    
      - CN=Workload Management Settings

  - 在 CN=Transport Settings,CN=\<*組織名稱*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*根網域*\> 下建立下列容器和物件 (若尚未存在)：
    
      - CN=Accepted Domains
    
      - CN=ControlPoint Config
    
      - CN=DNS Customization
    
      - CN=Interceptor Rules
    
      - CN=Malware Filter
    
      - CN=Message Classifications
    
      - CN=Message Hygiene
    
      - CN=Rules
    
      - CN=MicrosoftExchange329e71ec88ae4615bbc36ab6ce41109e

  - 在 Active Directory 中的整個組態分割上設定權限。

  - 匯入 Rights.ldf 檔案。此檔案會加入安裝 Exchange 和設定 Active Directory 所需的權限。

  - 在樹系的根網域中建立 MicrosoftExchange 安全性群組組織單位 (OU)，並指派權限給它。

  - 在 Microsoft Exchange 安全性群組 OU 內建立下列管理角色群組 (若尚未存在)：
    
      - 規範管理
    
      - 委派安裝
    
      - 探索管理
    
      - 服務台
    
      - 檢疫管理
    
      - 組織管理
    
      - 公用資料夾管理
    
      - 收件者管理
    
      - 記錄管理
    
      - 伺服器管理
    
      - UM 管理
    
      - 僅限檢視組織管理

  - 將 MicrosoftExchange 安全性群組 OU 中建立的新管理角色群組 (在 Active Directory 中顯示為萬用安全性群組 (USG))，加入至 CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*根網域*\> 容器中儲存的 **otherWellKnownObjects** 屬性。

  - 在根網域的 Microsoft Exchange 系統物件容器中建立「整合通訊語音發送者」連絡人。

  - 將執行 *PrepareAD* 指令的網域備妥供 Exchange 2013 使用。如需為 Exchange 準備 Active Directory 網域所執行之動作的相關資訊，請參閱＜Preparing Active Directory domains＞。

  - 設定 Exchange 組織物件的 **msExchProductId** 屬性。如果想要確定 Active Directory 架構已成功擴充，您可以檢查此屬性中儲存的值。如果屬性中的值符合您安裝的 Exchange 2013 版本所列出的架構版本，則表示擴充架構成功。如需 Exchange 版本的清單及如何檢查此屬性的值，請參閱＜[準備 Active Directory 及網域](prepare-active-directory-and-domains-exchange-2013-help.md)＞的＜[How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md)＞一節。

## 準備 Active Directory 網域

為 Exchange 準備好 Active Directory 的最後一步是準備所有 Active Directory 網域，其中將安裝 Exchange 或放置擁有郵箱功能的使用者。在執行 *PrepareAD* 命令的網域中會自動執行此步驟。

以下是對 Active Directory 網域所做的變更：

  - 在 Active Directory 的根網域分割中建立 Microsoft Exchange 系統物件容器 (若尚未存在)。

  - 在 Exchange Servers、Organization Management 和 Authenticated Users 安全性群組的 Microsoft Exchange 系統物件容器上設定權限。

  - 在目前網域中建立 Exchange Install Domain Servers 網域全域群組，並放置於 Microsoft Exchange 系統物件容器中。

  - 將 Exchange Install Domain Servers 群組加入至根網域中的 Exchange Servers USG。

  - 在 Exchange Servers USG 和 Organization Management US 的網域層級上指派權限。

  - 在 DC=\<*根網域*\> 下設定 Microsoft Exchange 系統物件容器中的 **objectVersion** 屬性。如果想要確定 Active Directory 架構已成功擴充，您可以檢查此屬性中儲存的值。如果屬性中的值符合您安裝的 Exchange 2013 版本所列出的架構版本，則表示擴充架構成功。如需 Exchange 版本的清單及如何檢查此屬性的值，請參閱＜[準備 Active Directory 及網域](prepare-active-directory-and-domains-exchange-2013-help.md)＞的＜[How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md)＞一節。


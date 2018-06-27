---
title: '部署 Exchange 2013 的多個樹系拓撲: Exchange 2013 Help'
TOCTitle: 部署 Exchange 2013 的多個樹系拓撲
ms:assetid: d51f2b7d-9045-40cf-8b9f-43787a6fff6d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124734(v=EXCHG.150)
ms:contentKeyID: 51409245
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 部署 Exchange 2013 的多個樹系拓撲

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

本主題提供部署多個樹系拓撲中的 Microsoft Exchange Server 2013的概觀。您會發現下列主旨的相關資訊：

  - **支援的多個樹系拓撲**   Exchange 2013支援兩種類型的多個樹系拓撲： 跨樹系和資源樹系。

  - **GAL 同步處理**   如果您有跨樹系環境，則必須確定任何一個樹系中的 GAL 都包含來自其他樹系的郵件收件者。

  - **跨樹系移動信箱**    Exchange 管理命令介面中的 **New-MoveRequest** 與 **New-MigrationBatch** 指令程式可協助您在不同樹系之間移動信箱。

  - **瞭解多重樹系管理**   瞭解權限模型，以便在樹系之間設定和管理權限。

## 支援的多重樹系拓撲

Exchange 2013 支援下列幾種多重樹系拓撲：

  - **跨樹系**  在跨樹系拓撲是一個以Exchange的多重樹系。這裡是概觀必須部署Exchange 2013的多個樹系拓撲中：
    
    1.  您必須先在每個樹系中安裝Exchange 2013 。如需詳細資訊，請參閱[部署 Exchange 2013 的新安裝](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)。
    
    2.  接下來，您必須同步處理中每個樹系、 收件者，讓每個樹系中全域通訊清單 (GAL) 包含所有同步處理的樹系中的使用者。請參閱 「 GAL 同步處理 」 一節下方的詳細資訊。
    
    3.  最後，您必須設定可用性服務，讓一個樹系中的使用者可以檢視其他樹系中的使用者的可用性資料。如需詳細資訊，請參閱[設定跨樹系拓撲的可用性服務](configure-the-availability-service-for-cross-forest-topologies-exchange-2013-help.md)。
    
    如需在跨樹系拓撲中部署 Exchange 2013 的詳細資料，請參閱[部署跨樹系拓撲中的 Exchange 2013](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md)。

  - **資源樹系**  在資源樹系拓撲是一個Exchange樹系與一個或多個使用者帳戶樹系。以下是您要部署的資源樹系拓撲中的Exchange 2013概觀：
    
    1.  您必須在樹系與Exchange安裝。Exchange樹系中，您必須已停用已Exchange信箱的使用者帳戶。
    
    2.  您必須至少一個包含使用者帳戶的樹系。此樹系應該*不*具備Exchange安裝。
    
    3.  接著，必須將 Exchange 樹系中停用的使用者帳戶與帳戶樹系中的使用者帳戶產生關聯。
    
    如需在資源樹系拓撲中部署 Exchange 2013 的詳細資料，請參閱[部署 Exchange 資源樹系拓撲中的 Exchange 2013](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md)。

## GAL 同步處理

根據預設，GAL 會包含在單一樹系中的郵件收件者。如果您有跨樹系環境，建議使用 Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1) 指定的樹系確定任何 GAL 包含來自其他樹系的郵件收件者。ILM 2007 FP1 會建立郵件使用者代表收來自其他樹系，進而讓使用者檢視其 GAL 中以及傳送郵件。例如使用者樹系 A 顯示為郵件使用者樹系 b，反之亦然。目標樹系中的使用者接著可以選取代表收件者其他樹系中的傳送郵件的郵件使用者物件。

若要啟用「GAL 同步處理」，您必須建立管理代理程式，以便將擁有信箱功能的使用者、連絡人及群組，從指定的 Active Directory 服務匯入集中式的中繼目錄。在中繼目錄中，擁有郵件功能的物件將被當成郵件使用者。群組則代表不具任何相關成員的連絡人。管理代理程式會將這些郵件使用者匯出至指定之目標樹系的組織單位中。

如需 Forefront Identity Manager (FIM) 的詳細資訊，請參閱 ＜ [Forefront Identity Manager 2010](https://go.microsoft.com/fwlink/p/?linkid=279864)。

## 跨樹系移動信箱

在跨樹系拓撲中，您可能會想要將信箱從一個樹系中移至另一個。為達成此目的您必須在Exchange管理命令介面中使用**New-MoveRequest**或**New-MigrationBatch**指令程式。如需跨樹系移動信箱的詳細資訊，請參閱下列主題：

  - [準備跨樹系移動要求的信箱](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [使用命令介面中準備 MoveRequest.ps1 指令碼的跨樹系移動準備信箱](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

  - [準備使用程式碼範例的跨樹系移動信箱](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

## 瞭解多重樹系管理

Exchange 2013 使用新的權限功能來管理多重樹系環境。

Exchange 2013使用角色型存取控制 (RBAC) 權限模型。系統管理員的成員、 管理角色群組和指派使用者、 管理角色指派原則決定每個系統管理員和使用者可以進行的動作。若要了解多個樹系權限，您需要熟悉 RBAC。如需關於 RBAC 角色群組和角色指派原則特別是，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

您可以使用 RBAC 權限模式來設定和管理您的樹系之間的權限。如需多個樹系權限的詳細資訊，請參閱下列主題：

  - [了解多重樹系權限](understanding-multiple-forest-permissions-exchange-2013-help.md)

  - [管理連結的角色群組](manage-linked-role-groups-exchange-2013-help.md)

  - [建立鏡像內建角色群組的連結的角色群組](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)


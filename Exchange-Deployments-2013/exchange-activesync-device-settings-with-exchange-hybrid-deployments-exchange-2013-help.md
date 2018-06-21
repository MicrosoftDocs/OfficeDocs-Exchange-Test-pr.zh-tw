---
title: 'Exchange ActiveSync 裝置設定與 Exchange 混合式部署: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync 裝置設定與 Exchange 混合式部署
ms:assetid: 77f7cd72-2a8a-467e-9ffd-b93f5eeb2f69
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn931281(v=EXCHG.150)
ms:contentKeyID: 64361763
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync 裝置設定與 Exchange 混合式部署

 

_<strong>適用版本：</strong>Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2016-01-27_

Exchange ActiveSync 裝置可以在信箱從 Exchange 內部部署組織移至 Office 365 時自動重新設定。Exchange ActiveSync 會在 Office 365 中尋找新的信箱位置，並更新其組態以直接和 Office 365 交談。Exchange ActiveSync 裝置在成功重新導向至 Office 365 之後，將不會嘗試並連絡內部部署 Exchange 伺服器。除了少數的例外狀況以外 (詳細說明如下)，使用者不再需要手動設定他們的裝置，就可以讓郵件繼續運作。

如果您想要將信箱移至 Office 365，請參閱 [在混合式部署中內部部署與 Exchange Online 組織之間移動信箱](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md)。

如需混合式部署的詳細資訊，請參閱 [Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。

若要使用自動重新導向，您的內部部署伺服器需要執行最新版的 Exchange 2010、Exchange 2013、Exchange 2016，或更新版本。您也需要使用 [混合組態精靈](hybrid-configuration-wizard-exchange-2013-help.md) 來設定您的混合式部署。Exchange ActiveSync 重新導向功能會使用在組織關聯性物件上設定的 網頁型 Outlook 目標 URL。這個物件已在執行混合式組態精靈時進行設定。

如果您的組織符合上述需求，行動裝置應該會在使用者的信箱移動時自動重新導向到 Office 365，而不需要任何其他組態。如需最佳的體驗，請確定使用者的行動裝置正在執行最新版本的作業系統和電子郵件用戶端。某些行動裝置 (例如執行 Android 作業系統的行動裝置) 可能要花比預期還長的時間才能重新導向。此外，某些裝置可能無法正確解譯 Exchange 所傳送的 Exchange ActiveSync 451 重新導向指示。針對這些裝置，使用者仍必須在裝置上手動重新設定或重新建立自己的電子郵件帳戶。如果您有裝置是否支援 Exchange ActiveSync 451 重新導向的相關問題，請連絡裝置製造廠商。

下列案例不支援自動 Exchange ActiveSync 重新導向：

  - 將信箱從 Office 365 移至內部部署 Exchange 組織。

  - 在內部部署 Exchange 組織之間移動信箱。

  - 將信箱從 Exchange 2007 伺服器移至 Office 365。


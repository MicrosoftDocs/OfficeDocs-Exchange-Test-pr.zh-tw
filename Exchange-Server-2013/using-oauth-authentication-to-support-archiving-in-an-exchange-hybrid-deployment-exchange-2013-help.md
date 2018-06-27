---
title: '在 Exchange 混合式部署中使用 OAuth 驗證來支援封存: Exchange 2013 Help'
TOCTitle: 在 Exchange 混合式部署中使用 OAuth 驗證來支援封存
ms:assetid: deb882b1-1ae2-40f3-a71c-423fafe3d66a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn689104(v=EXCHG.150)
ms:contentKeyID: 62248234
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Exchange 混合式部署中使用 OAuth 驗證來支援封存

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

如果您在 Exchange 2013 混合式部署中，且使用 Exchange Online Archiving (EOA) for Exchange Serve，則在升級到 Exchange 2013 累計更新 5 (CU5) 之後，您必須在內部部署與 Exchange Online 組織之間設定 OAuth 驗證。EOA 可讓您提供雲端式封存給具有內部部署信箱的使用者。在此情況下，內部部署信箱伺服器上的通訊記錄管理 (MRM) 助理會套用封存原則，並自動將使用者信箱中的郵件移至雲端式封存。在 Exchange 2013 CU5 中是使用 OAuth 驗證。

如需有關設定 OAuth 驗證的逐步指示，請參閱＜[設定 Exchange 與 Exchange Online 組織之間的 OAuth 驗證](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)＞。

## 什麼是 OAuth 驗證？

OAuth 驗證是伺服器對伺服器的驗證通訊協定，可讓應用程式相互驗證。使用 OAuth 驗證時，不會在電腦之間傳遞使用者認證和密碼。取而代之是經由交換安全性權杖來進行驗證和授權，這樣可授與一段時間的權限來存取一組特定的資源。

OAuth 驗證通常涉及三個對象︰ 單一授權伺服器和需要彼此的兩個領域。安全性權杖會發給由驗證伺服器 （也稱為安全性權杖伺服器） 通訊 ； 需要兩個領域這些語彙基元確認其他領域應信任通訊源自一個領域。使用內部部署 Exchange 組織與 Exchange Online 之間的 OAuth 驗證時，由 Office 365 組織中的Azure Active Directory 存取控制服務 (ACS)提供授權伺服器的函數。例如，在跨部署 eDiscovery 搜尋期間Azure Active Directory ACS發出的權杖的確認系統管理員或法務從 Exchange 內部部署組織能夠存取信箱中的 Exchange Online 組織和之類的事情。

## 設定 OAuth 驗證來支援封存

如前所述，請參閱＜[設定 Exchange 與 Exchange Online 組織之間的 OAuth 驗證](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)＞，以取得在 Exchange 混合式部署中設定 OAuth 驗證來支援封存的相關指示。

如果 Exchange 混合式部署未設定 OAuth，則無法使用封存原則來自動將內部部署組織中使用者主要信箱中的項目，移至 Exchange Online 中使用者的雲端式封存。

## 其他資訊

  - 您也必須將 OAuth 驗證設定為在單一 eDiscovery 搜尋中，對內部部署和雲端式信箱執行跨部門 eDiscovery 搜尋。請參閱[在 Exchange 混合式部署中使用 OAuth 驗證來支援 eDiscovery](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md)。

  - 您也可以設定 OAuth 驗證來允許其他應用程式 (例如 SharePoint 2013 和 Lync Server 2013) 向 Exchange 2013 驗證。如需詳細資訊，請參閱 [設定 SharePoint 2013 與 Lync 2013 的 OAuth 驗證](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md)。

  - 您可以設定 Exchange 2013 和 SharePoint 2013 之間的伺服器對伺服器驗證，讓管理員和法務人員可以使用 SharePoint 2013 的 eDiscovery 中心來搜尋 Exchange 2013 信箱。如需詳細資訊，請參閱 [設定 Exchange for SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)。

  - 您可以設定 Exchange 混合部署中Exchange 2013使用混合組態精靈\]。自訂的逐步說明混合部署設定檢查清單請參閱[Exchange Server Deployment Assistant](https://go.microsoft.com/fwlink/p/?linkid=277105)。


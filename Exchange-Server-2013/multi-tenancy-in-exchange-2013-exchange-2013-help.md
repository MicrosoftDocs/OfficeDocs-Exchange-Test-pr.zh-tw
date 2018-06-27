---
title: 'Exchange 2013 中的多重租賃: Exchange 2013 Help'
TOCTitle: Exchange 2013 中的多重租賃
ms:assetid: df09257d-dd98-4f59-b830-1818cedda15c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ862352(v=EXCHG.150)
ms:contentKeyID: 50554073
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 中的多重租賃

 

_**適用版本：**Exchange Online, Exchange Server, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

在多承租人 （主控） Exchange 2013部署定義一個位置為 Exchange 組織已設定為裝載多個及不連續的組織或業務單位 （承租人） 通常不共用的電子郵件、 資料、 使用者、 全域通訊清單 (Gal) 或其他常用於 Exchange 物件。共用的硬體、 軟體和資源 （全部同時又不承租人之間的邏輯區隔），允許組織利用標準的 Exchange 部署同時提供多承租人功能和服務指派符合其主控需求簡化了程序。

## 在 Exchange 2013 組織中的多重租用

在Exchange 2013，我們繼續支援裝載使用標準、 內部部署 Exchange 安裝類似Exchange 2010 Service Pack 2 (SP2) 中所使用的方法。我們停用`/hosting`模式參數並會強調通訊錄原則 (Abp) 主控管理解決方案和核准的獨立軟體廠商 (Isv) 所提供的自動化工具一起使用。這些解決方案的 Microsoft 核准設定指導方針與作法架構上建置並將會提供 Exchange 組織提供代管服務和功能更容易更完善方式。

Exchange 2013支援多重租用運用下列主要元件與功能：

  - **Active Directory**  而不是擁有個別*ExchangeOrganization* Active Directory 容器的多租用戶 Exchange 組織中各業務單位、 Exchange 2013多重租用支援使用單一*ExchangeOrganization* Active Directory 容器。這可讓更簡單的 Active Directory 結構並減少 Active Directory 與相關的權限問題的可能性。
    
    若要深入了解Exchange 2013Active Directory 變更，請參閱[Active Directory](active-directory-exchange-2013-help.md)。

  - **通訊錄原則 (Abp)**  最早出現在Exchange 2010 SP2、 Abp Exchange 2013中用來控制使用者存取權的通訊清單、 全域通訊清單 (GAL) 及離線通訊錄 (Oab) 的 Exchange 組織中。Abp 會將這些不同的 Active Directory 物件組成單一、 虛擬的物件可以指派給個別使用者，以及建立多重租用戶組織結構沿著這些資源邏輯群組。類似於與其Exchange 2010 SP2 中的Exchange 2013 ABP 功能。
    
    深入了解 Abp Exchange 2013中，請參閱 ＜ [通訊錄原則](address-book-policies-exchange-2013-help.md)。

  - **主控管理解決方案**  使用Exchange 2013提供託管式的 Exchange 解決方案某些管理員有益於使用自訂的主控管理方法。限制的 Exchange 系統管理中心 (EAC)，因為 Microsoft 適用於第三方協助他們在符合指導方針和核准的 framework 託管的Exchange 2013組織控制面板和自動化解決方案的開發。我們建議設定裝載的 Exchange 解決方案的組織運用這些工具來管理主控的組織其中的情況下需要它。
    
    若要深入了解主控管理解決方案，包括已驗證之的解決方案的供應商，請參閱[主控 Exchange Server 2013 與多重租用解決方案和指引](https://go.microsoft.com/fwlink/?linkid=275036)


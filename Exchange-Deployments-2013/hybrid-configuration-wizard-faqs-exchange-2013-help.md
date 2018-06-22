---
title: '混合組態精靈常見問題集: Exchange 2013 Help'
TOCTitle: 混合組態精靈常見問題集
ms:assetid: e911e6e0-e36e-4430-ac36-c745a10d6c26
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt488940(v=EXCHG.150)
ms:contentKeyID: 72045787
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 混合組態精靈常見問題集

 

_<strong>適用版本：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2016-12-09_

Microsoft 已發行新的混合式組態精靈，可以簡化混合式部署的組態，在使用混合式組態時更有彈性，並可確保您永遠執行最新版本的經驗。這個版本的混合式精靈內建至 Exchange 2016 以及從累積更新 10 開始的 Exchange 2013 版本，但是即使您執行較舊的 Exchange 2013 累積更新 (CU) 或 Exchange 2010 Service Pack 3 (SP3)，您仍然可以下載新的精靈。

如需有關 Office 365 混合式組態精靈的詳細資訊，請參閱 Exchange 團隊部落格上的 [Microsoft Office 365 混合式組態精靈簡介](http://go.microsoft.com/fwlink/?linkid=717122)和[適用於 Exchange 2010 的 Office 365 混合式組態精靈](http://go.microsoft.com/fwlink/?linkid=730687)。

若要下載 Office 365 混合式組態精靈，請移至 [http://aka.ms/HybridWizard](http://aka.ms/hybridwizard)。

## 客戶的常見問題集

  - 問：何種版本的 Exchange 支援新的混合式組態精靈？  
    答：您必須要有至少一個伺服器符合下列需求︰
    
      - **Exchange 2010**Exchange 2010 SP3 必須安裝在至少一個執行 Mailbox、Hub Transport 和 Client Access server role 的伺服器上。我們也強烈建議您安裝 Exchange 2010 SP3 的最新可用更新彙總套件。
    
      - **Exchange 2013**最新的 Exchange 2013 CU 必須安裝在至少一個執行 Mailbox 與 Client Access server role 的伺服器上。若您無法安裝最新的 CU，也會立即支援前一版本。不支援較舊的 CU。
    
      - **Exchange 2016**最新版本的 Exchange 2016 必須安裝在至少一個執行 Mailbox server role 的伺服器上。
    
    舉例來說，假設您已在內部部署組織安裝 Exchange 2013 CU8，而目前 Exchange 2013 最新可用的版本是 CU10。為保持可受混合組態支援的狀態，至少需要將您的 Exchange 2013 伺服器升級到最新的 CU9。不過，我們強烈建議您升級至 CU10。
    
    累計更新會以每季一次的頻率發行。因此，若您定期需要額外時間來完成升級作業，請讓您的伺服器保持使用最新的累計更新，以便在時間上有些彈性。

<!-- end list -->

  - 問：此混合式組態精靈是否能夠與 Exchange 2007 搭配使用？  
    答：您可以在您的組織中使用 Exchange 2007 設定混合式部署。不過，若要這樣做，您需要部署一個執行 Exchange 2013 (符合上述需求) 的伺服器。

<!-- end list -->

  - 問：我是否可以選擇新的混合式組態精靈？  
    答：否。新的混合式組態精靈是現今 Exchange 2010、Exchange 2013 和 Exchange 2016 中唯一支援的精靈。

<!-- end list -->

  - 問：我是否可以使用新的混合式組態精靈，將目前的 Exchange 2010 混合式組態升級至 Exchange 2013 或 Exchange 2016  
    答：可以。請確定您有至少一部伺服器符合目前的混合式組態精靈需求，然後加以執行。精靈將會知道您的混合式組態的目前狀態，並順利地引導您完成升級程序。


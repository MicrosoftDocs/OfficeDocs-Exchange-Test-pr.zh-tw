---
title: '在網域控制站上安裝 Exchange 不建議使用: Exchange 2013 Help'
TOCTitle: 在網域控制站上安裝 Exchange 不建議使用
ms:assetid: 48922de2-a68c-4092-96a5-d38c8e5f49f5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.warninginstallexchangerolesondomaincontroller(v=EXCHG.150)
ms:contentKeyID: 50473167
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在網域控制站上安裝 Exchange 不建議使用

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2013-03-22_

Microsoft Exchange Server 2013安裝程式已偵測到您正在嘗試安裝Exchange 2013上之電腦的 Active Directory 網域控制站。在網域控制站上安裝Exchange 2013不建議使用。

若您在網域控制站上安裝 Exchange 2013，請注意下列問題：

  - 不支援為 Active Directory 分割權限設定 Exchange 2013。

  - Exchange 受信任子系統萬用安全性群組 (USG) 新增至 Domain Admins 群組的網域控制站上安裝 Exchange 時。當發生此情況時，網域中的所有 Exchange 伺服器會授都與該網域中的網域系統管理員權限。

  - Exchange Server 與 Active Directory 是這兩種大量消耗資源的應用程式。有必須考量兩正在執行在同一部電腦上的效能影響。

  - 您必須確定安裝 Exchange 2013 的網域控制器是通用類別目錄伺服器。

  - 當網域控制站同時也是通用類別目錄伺服器時，Exchange 服務無法正確啟動。

  - 在伺服器關機或重新啟動之前，如果未停止 Exchange 服務，系統關機將需要花費很長時間。

  - 不支援將網域控制站降級為成員伺服器。

  - 不支援在同時身為 Active Directory 網域控制站的叢集節點上執行 Exchange 2013。

我們建議在成員伺服器上安裝 Exchange 2013。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。


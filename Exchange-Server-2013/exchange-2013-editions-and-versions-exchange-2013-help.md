---
title: 'Exchange 2013：版本: Exchange 2013 Help'
TOCTitle: Exchange 2013：版本
ms:assetid: b563b543-fb3f-4465-9a54-cbfd680aee1f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232170(v=EXCHG.150)
ms:contentKeyID: 50554084
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013：版本

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange Server 2013 有兩種伺服器版本：Standard Edition 及 Enterprise Edition。Enterprise Edition 的量產發行 (RTM) 與累計更新 1 (CU1) 版本可擴充到每台伺服器 50 個裝載資料庫，而累計更新 2 (CU2) 與更新版本可擴充到每台伺服器 100 個裝載資料庫；Standard Edition 則限制為每台伺服器 5 個裝載資料庫。裝載資料庫是指正在使用的資料庫。裝載資料庫可以是為了給用戶端使用而裝載的主動信箱資料庫，或是在復原過程中，為了進行記錄複寫與重播而裝載的被動信箱資料庫。您可以建立超過上述數目限制的資料庫，但最多僅能裝載上述數目的資料庫。復原資料庫不在此限制的計算內。

這些都是由產品金鑰所定義的授權版本。當您輸入有效的授權產品金鑰時，便會建立伺服器的支援版本。產品金鑰只能用於相同版本金鑰的交換和升級，不能用於降級。您可以使用有效的產品金鑰，從 Exchange 2013 評估版 (試用版) 升級為 Standard Edition 或 Enterprise Edition。您也可以使用有效的產品金鑰，從 Standard Edition 升級為 Enterprise Edition。

您也可以使用相同的版本產品金鑰，再授權一次伺服器。例如，假設您有兩部 Standard Edition 伺服器及兩個金鑰，但您不小心將同一個金鑰用於這兩部伺服器，則可將其中一部伺服器的金鑰變更為您發出的另一個金鑰。您不需要重新安裝或重新設定任何項目，即可進行這些動作。在您輸入產品金鑰並重新啟動 Microsoft Exchange Information Store 服務之後，將會反映出對應於該產品金鑰的版本。

試用版到期時，並不會喪失任何功能，所以您可以維護實驗室、示範、訓練及其他非生產環境 120 天以上，而不需重新安裝 Exchange 2013 試用版。

如前所述，您無法使用產品金鑰從 Enterprise Edition 降級為 Standard Edition，也不能用它們還原成試用版。要進行這種類型的降級，只能解除安裝 Exchange 2013、重新安裝 Exchange 2013，並輸入正確的產品金鑰。

## Exchange 2013 版本

如需 Exchange 2013 版本清單及如何下載並升級為 Exchange 2013 最新版的資訊，請參閱下列主題：

  - [Exchange Server 更新：組建編號與發行日期](https://technet.microsoft.com/zh-tw/library/hh135098\(v=exchg.150\))

  - [將 Exchange 2013 升級至最新的累計或服務套件](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)

若要檢視您所執行之 Exchange 2013 版本的組建編號，請在 Exchange 管理命令介面中執行下列命令。

    Get-ExchangeServer | fl name,edition,admindisplayversion

## Exchange 2013 授權類型

Exchange 2013 以伺服器/用戶端存取授權 (CAL) 模式授權，類似於 Exchange 2010 的方式。授權類型如下：

  - **伺服器授權：**一份授權必須指派給每一個執行伺服器軟體的執行個體。伺服器授權以兩種伺服器版本進行販售：Standard Edition 及 Enterprise Edition。

  - **用戶端存取授權 (CAL)：**Exchange 2013 也提供兩種用戶端存取授權 (CAL) 版本，即標準 CAL 與企業 CAL。您可以將各種伺服器版本與 CAL 類型混搭。例如，您可使用 Enterprise CAL 與 Exchange 2013 Standard Edition。同樣地，也可以使用 Standard CAL 搭配 Exchange 2013 Enterprise Edition。

如需 Exchange 授權類型的詳細資訊，請參閱[授權](https://go.microsoft.com/fwlink/p/?linkid=392675)。


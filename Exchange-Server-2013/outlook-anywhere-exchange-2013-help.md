---
title: 'Outlook 無所不在: Exchange 2013 Help'
TOCTitle: Outlook 無所不在
ms:assetid: 9026d461-ec6a-4ef5-ba9d-de33030858f3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123741(v=EXCHG.150)
ms:contentKeyID: 50473724
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook 無所不在

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

在 Microsoft Exchange Server 2013 中，Outlook Anywhere 功能 (以前稱為 RPC over HTTP) 可讓使用 MicrosoftOutlook 2013、Outlook 2010 或 Outlook 2007 的用戶端從企業網路外部，或使用 RPC over HTTP Windows 網路元件透過網際網路連接至 Exchange 伺服器。本主題說明 Outlook Anywhere 功能並列出使用 Outlook Anywhere 的優點。

**目錄**

Outlook 無所不在 及 Exchange 2013

使用 Outlook 無所不在的優點

部署 Outlook 無所不在

管理 Outlook 無所不在

Outlook 無所不在 共存

測試 Outlook 無所不在 連線

## Outlook 無所不在 和 Exchange 2013

Windows RPC over HTTP Proxy 元件 (Outlook Anywhere 用戶端用來連接的元件) 會以 HTTP 層包住遠端程序呼叫 (RPC)。如此可讓流量穿越網路防火牆，而不需要開啟 RPC 連接埠。在 Exchange 2013 中，預設為啟用此功能，因為 Exchange 2013 不允許直接 RPC 連線。

## 使用 Outlook 無所不在 的優點

Outlook Anywhere 可為使用 Outlook 2013、Outlook 2010 或 Outlook 2007 存取您的 Exchange 郵件基礎結構的用戶‎端提供下列優勢：

  - 使用者可透過網際網路從遠端存取 Exchange 伺服器。

  - 您可以使用用於 Outlook Web App 及 MicrosoftExchange ActiveSync 的相同 URL 和命名空間。

  - 您可以使用用於 Outlook Web App 及 Exchange ActiveSync 的相同安全通訊端層 (SSL) 伺服器憑證。

  - 來自 Outlook 的未驗證要求無法存取 Exchange 伺服器。

  - 您不需要使用虛擬私人網路 (VPN) 跨網際網路存取 Exchange 伺服器。

  - 如果已搭配使用 Outlook Web App 與 SSL 或 Exchange ActiveSync 與 SSL，則不需要開啟任何來自網際網路的額外連接埠。

  - 您可以使用 **Test-OutlookConnectivity** Cmdlet 測試 Outlook Anywhere 和 TCP 連接的端對端用戶端連線。

## 部署 Outlook 無所不在

在Exchange 2013 中，依預設會啟用 Outlook 無所不在，因為所有 Outlook 連線都會透過 Outlook 無所不在 發生。若要成功使用 Outlook 無所不在，您部署後唯一必須執行的工作是在用戶端存取伺服器上安裝有效的 SSL 憑證。在您的組織中的信箱伺服器只需要預設的自我簽署 SSL 憑證。

## 管理 Outlook 無所不在

您可以使用 Exchange 系統管理中心或 Exchange 管理命令介面管理 Outlook Anywhere。

## Outlook 無所不在 共存

如果您規劃以與舊版 Exchange Server 共存的情形來安裝 Exchange 2013，則組織中可能還有 Outlook 2003 用戶端。對 Exchange 2013 而言，Outlook 2003 不是支援的用戶端。

在將命名空間移至 Exchange 2013 前，您必須確定所有 Outlook 用戶端都已升級至最低支援的版本。Outlook 無所不在 連線至 Exchange 2013 需要 Outlook 2007 或較新版本，即使目標信箱仍在 Exchange 2007 或 Exchange 2010 上亦然。

如果您目前在 Exchange 2007 或 2010 中使用 Outlook 無所不在，且要允許 Exchange 2013 Client Access Server 將連線代理至 Exchange 2007/2010 伺服器，您必須在貴組織中的所有 Exchange 2007/2010 CAS 上啟用並設定 Outlook 無所不在。不過，如果目前未在 Exchange 2007/2010 環境中使用 Outlook 無所不在，而且不想使用，就不需要在舊版環境中加以啟用。如需對 Exchange Server 2007 上執行的 Client Access Server 啟用 Outlook 無所不在的指示，請參閱[如何啟用 Outlook 無所不在](https://go.microsoft.com/fwlink/p/?linkid=510497)。如需對 Exchange Server 2010 上執行的 Client Access Server 啟用 Outlook 無所不在的指示，請參閱[啟用 Outlook 無所不在](https://go.microsoft.com/fwlink/p/?linkid=510502)。

確定您在 Client Access Server 上啟用 Outlook 無所不在 時，選擇 NTLM 進行 IIS 驗證。

最後，設定 Outlook 無所不在 外部主機名稱，以指向 Exchange 2013 Outlook 無所不在 主機名稱。如需 Exchange Server 2007年的指示，請參閱[如何設定 Outlook 無所不在 的外部主機名稱](https://go.microsoft.com/fwlink/p/?linkid=510530)。如需 Exchange Server 2010 的指示，請參閱[設定 Outlook 無所不在 的外部主機名稱](https://go.microsoft.com/fwlink/p/?linkid=510531)。

## 測試 Outlook 無所不在 連線

您可以執行下列其中一項操作來測試端對端的用戶端 Outlook 連線：

  - 執行 **Test-OutlookConnectivity** Cmdlet。這個 Cmdlet 會測試 Outlook Anywhere (RPC over HTTP) 連線。如果 Cmdlet 測試失敗，輸出將會對失敗的步驟添加附註。如需詳細的語法和參數資訊，請參閱[Test-OutlookConnectivity](https://technet.microsoft.com/zh-tw/library/dd638082\(v=exchg.150\))。

  - 使用 Outlook Remote Connectivity Analyzer (ExRCA) 執行 Exchange Anywhere 連線測試。當您執行這項測試時，會收到一份詳細的摘要，顯示測試失敗的位置，以及修正問題可採取的步驟。如需詳細資訊，請參閱 [Exchange Remote Connectivity Analyzer](exchange-remote-connectivity-analyzer-exchange-2013-help.md)。

這兩項測試會在從自動探索服務取得伺服器設定之後，嘗試透過 Outlook Anywhere 登入。端對端驗證包含下列項目：

  - 測試自動探索連線

  - 驗證 DNS

  - 驗證憑證 (憑證名稱是否符合網站、憑證是否到期以及是否受信任)

  - 檢查防火牆是否正確設定 (ExRCA 會檢查整個防火牆設定。Cmdlet 則會測試 Windows 防火牆組態)。

  - 藉由登入使用者信箱的方式確認用戶端連線


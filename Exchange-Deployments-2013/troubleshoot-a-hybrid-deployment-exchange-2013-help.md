---
title: '疑難排解混合式部署: Exchange 2013 Help'
TOCTitle: 疑難排解混合式部署
ms:assetid: bbae72f3-6a1e-4cbf-80da-d8f73d969c6b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ659053(v=EXCHG.150)
ms:contentKeyID: 50474708
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 疑難排解混合式部署

 

_<strong>適用版本：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2016-04-29_

利用混合式組態精靈在 Exchange 中設定混合式部署可以將混合式部署遇到問題的可能性降到最低。然而，如果混合式組態精靈範圍之外的部分區域設定錯誤，混合式部署中就可能會出現問題。本主題討論下列可能會發生問題的一般區域，並概述驗證或更正問題的基本步驟：

  - 內部部署 Exchange 伺服器

  - 憑證

  - 混合式組態精靈的特定錯誤

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在本主題中，「Exchange 伺服器」指的是下列伺服器：
<ul>
<li><p><strong>用戶端存取伺服器</strong> Exchange 2013 和更舊版本</p></li>
<li><p><strong>信箱伺服器</strong> Exchange 2016 和更新版本</p></li>
</ul></td>
</tr>
</tbody>
</table>


如需其他資訊，請參閱 [Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。

如需其他混合式部署相關的管理工作資訊，請參閱 [混合式部署程序](hybrid-deployment-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：取決於混合式部署的問題類型而有所不同

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[Exchange 及命令介面基礎結構權限](https://technet.microsoft.com/zh-tw/library/dd638114\(v=exchg.150\))主題中的「混合式部署」項目。

  - 本主題中的指引可套用到使用混合式組態精靈設定的混合式部署。不支援以手動方式設定的混合式部署。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](https://technet.microsoft.com/zh-tw/library/jj150484\(v=exchg.150\))。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 疑難排解內部部署 Exchange 伺服器的問題

在混合式部署中，內部部署 Exchange 伺服器的設定通常是大部分的問題可能會發生的區域。通常，需要檢查的區域如下所示：

  - **可用性**   將內部部署 Exchange 伺服器正確發佈到網際網路上，對於混合式部署中的功能正確運作是很重要的。若要讓混合式功能正確運作，您必須設定內部部署防火牆或其他安全性裝置，以允許來自網際網路的輸入存取，可存取內部部署 Exchange 伺服器上的自動探索和 Exchange Web 服務 (EWS) 端點。此外，Exchange 伺服器也必須設定為接受輸入 SMTP 郵件。如果包含在 Office 365 組織中的 Microsoft Exchange Online Protection (EOP) 服務無法連上內部部署 Exchange 伺服器，從 Exchange Online 組織到內部部署組織的安全郵件傳輸將無法正確運作。

  - **憑證**   用來進行 Exchange Online 組織和內部部署組織之間的安全郵件傳輸之數位憑證，需要安裝在所有內部部署且連結網際網路的 Exchange 伺服器 (將與 Exchange Online 通訊) 上、必須由協力廠商憑證授權單位 (CA) 發出、必須尚未過期，而且必須已指派 IIS 和 SMTP 服務。如果不符合這些憑證需求，從 Exchange Online 組織到內部部署組織的安全郵件傳輸會無法正常運作。本主題稍後的「疑難排解憑證的問題」中會提供憑證需求的詳細資訊。

## 如何知道您的 Exchange 伺服器是否已正確設定？

若要驗證您已成功發佈您的內部部署 Exchange 伺服器，請使用 Microsoft 遠端連線分析程式來驗證連線至內部部署 Exchange 伺服器的輸入網際網路連線。執行下列動作：

1.  移至[遠端連線分析程式](https://www.testexchangeconnectivity.com/)工具。

2.  這個步驟適用於 EWS 工作的一般測試，可確認工作正在運作，且已設定 EWS 端點。
    
    執行 \[**Microsoft Exchange Web 服務連線測試**\] 區段中的 \[**同步處理、通知、可用性及自動回覆 (OOF)**\] 測試，並確認沒有任何錯誤。如果發生錯誤，請更正測試所識別的項目。

3.  這個步驟適用於自動探索服務的一般測試，可確認服務正在運作，而且已設定自動探索端點。
    
    執行 **Microsoft Office Outlook 連線測試**一節中的 **Outlook 自動探索**測試，並確認沒有任何錯誤。如果發生錯誤，請更正測試所識別的項目。

4.  這個步驟適用於 SMTP 連線的一般測試，可確認 Exchange 伺服器可以接收輸入網際網路郵件。
    
    執行**網際網路電子郵件測試**一節中的 **輸入 SMTP 電子郵件**測試，並確認沒有任何錯誤。如果發生錯誤，請更正測試所識別的項目。

## 疑難排解憑證的問題

設定安裝於內部部署 Exchange 伺服器上的憑證，可能是混合式部署中發生問題的來源。在大部分的情況下，下列憑證相關的問題會影響混合式功能：

  - **憑證類型**   必須由協力廠商 CA 發出用於安全混合式傳輸且在混合式組態精靈中定義的數位憑證。自我簽署的憑證無法用於混合式傳輸驗證。如果不當選取或指派自我簽署的憑證，Exchange Online 組織和內部部署組織之間的安全郵件傳輸會無法正常運作。

  - **指派服務**   網際網路資訊服務 (IIS) 和簡易郵件傳送通訊協定 (SMTP) 服務必須指派給用於混合式傳輸的數位憑證。如果未指派這些服務，Exchange Online 組織和內部部署組織之間的安全郵件傳輸會無法正常運作。

  - **安裝**   用來進行 Exchange Online 組織和內部部署組織之間的安全郵件傳輸之數位憑證，必須安裝在所有內部部署 Exchange 伺服器上。如果您正在利用 Edge Transport server 部署混合，數位憑證也必須安裝在您的 Edge Transport server 上。如果憑證未安裝在內部部署伺服器上，Exchange Online 組織和內部部署組織之間的安全郵件傳輸會無法正常運作。

  - **到期**   用來進行 Exchange Online 組織和內部部署組織之間的安全郵件傳輸之數位憑證，必須尚未過期。如果憑證已過期，Exchange Online 組織和內部部署組織之間的安全郵件傳輸會無法正常運作。

## 如何知道您的憑證是否已正確設定？

若要驗證混合式郵件傳輸的憑證已在您的內部部署 Exchange 伺服器上正確設定，請執行下列作業：

1.  在內部部署 Exchange 伺服器上，開啟 Exchange 管理命令介面。

2.  在 Exchange 管理命令介面 中，執行下列命令。
    
        Get-ExchangeCertificate| format-list

3.  找出您在混合式組態精靈中所定義之用於安全郵件傳輸的憑證資訊。

4.  請確認下列參數值會指派給憑證：
    
      - **IsSelfSigned 參數**   這個參數值應該是 *False*。
    
      - **RootCAType 參數**   這個參數值應該是 *Third Party*。
    
      - **Services 參數**   這個參數值應該是 *IIS, SMTP*。
    
      - **NotAfter 參數**   這個參數值是憑證到期日。這裡所列出的日期應該尚未過期。

## 疑難排解混合式組態精靈的特定錯誤

如果您在執行混合式組態精靈時收到錯誤，您可以執行幾個簡單的檢查或動作，通常就能解決問題。請參閱下列建議，可解決您在執行混合式組態精靈時可能會遇到的特定訊息或問題。

  - **訊息：「伺服器 \<伺服器名稱\> 上找不到預設接收連接器」**   如果下列屬性中列出之任何 Exchange 伺服器上的接收連接器不接聽 TCP 連接埠 25 上的 IPv4 和 IPv6 通訊協定，就會出現這個訊息：`(Get-HybridConfiguration).ReceivingTransportServers.`
    
      -  
        若要驗證當您執行 `(Get-HybridConfiguration).ReceivingTransportServers.` 時列出的 Exchange 伺服器上的接收連接器擁有正確的繫結，請在 Exchange 管理命令介面 中執行下列命令。
        
            Get-ReceiveConnector -Server <Server Name> | FT Identity, Bindings
        
        您應該會看到下列為 Exchange 伺服器所列出的項目：`{[::]:25, 0.0.0.0:25}`
        
        如果未列出此繫結，您必須使用 **Set-ReceiveConnector** 指令程式的 *Bindings* 參數，將它新增到您的接收連接器。如需詳細資料，請參閱 [Set-ReceiveConnector](https://technet.microsoft.com/zh-tw/library/bb125140\(v=exchg.150\))。


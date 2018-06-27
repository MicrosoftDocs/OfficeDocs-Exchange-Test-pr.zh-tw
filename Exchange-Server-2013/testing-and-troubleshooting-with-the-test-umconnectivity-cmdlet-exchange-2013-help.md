---
title: '利用 Test-umconnectivity 指令程式測試及疑難排解: Exchange 2013 Help'
TOCTitle: 利用 Test-umconnectivity 指令程式測試及疑難排解
ms:assetid: 08e67a99-e37f-4afd-bd58-455b62580af7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa995978(v=EXCHG.150)
ms:contentKeyID: 56271543
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 利用 Test-umconnectivity 指令程式測試及疑難排解

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-06-25_

在安裝 Client Access Server 和 Mailbox Server 並設定整合通訊之後，您可以使用多項診斷測試和電話應用程式軟體來測試整合通訊服務的電話語音連線和作業。

## Test-UMConnectivity

**Test-UMConnectivity** Cmdlet 有數種方式可用來檢查與 Client Access Server 和 Mailbox Server 的連線，視與此 Cmdlet 搭配使用的參數而定。針對測試整合通訊功能，可以使用這些測試：

  - **本機**   **Test-UMConnectivity** Cmdlet 會驗證與相同本機電腦上執行的 Mailbox Server 之間的 VoIP (Voice over IP) 通訊。

  - **本機使用 TUILogon**   **Test-UMConnectivity** Cmdlet 會嘗試與相同電腦上執行的 Mailbox Server 建立 VoIP 通訊。如果順利連線，它會藉由傳送信箱的分機號碼與 PIN，嘗試登入一或多個啟用 UM 功能的信箱。如果提供 *–TUILogon* 參數，則也必須使用適當的測試信箱資訊提供下列參數值：
    
      - *–Phone*   此參數必須含有測試信箱的分機號碼。
    
      - *–PIN*   此參數必須含有啟用 UM 功能之信箱的 PIN。
    
      - *–UMDialPlan   *此參數必須包含與測試信箱連結的撥號對應表。

  - **遠端**   **Test-UMConnectivity** Cmdlet 會嘗試藉由透過 VoIP 閘道撥打電話來連線到遠端 Client Access Server。連線之後，此 Cmdlet 會對遠端 Client Access Server 和媒體路徑執行連線檢查。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>收到下列訊息時應重新啟動 MicrosoftExchange 整合通訊服務，因為這表示服務已停止或未回應。「Test-UMConnectivity 工作在嘗試撥打電話時發生錯誤。詳細資料：無法建立連線。」</td>
    </tr>
    </tbody>
    </table>


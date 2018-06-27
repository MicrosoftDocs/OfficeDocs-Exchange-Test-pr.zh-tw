---
title: '透過訂閱的 Edge Transport Server 設定網際網路郵件流程: Exchange 2013 Help'
TOCTitle: 透過訂閱的 Edge Transport Server 設定網際網路郵件流程
ms:assetid: d12ea770-99ce-4ab4-a373-96f2554641fa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb738158(v=EXCHG.150)
ms:contentKeyID: 61180460
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 透過訂閱的 Edge Transport Server 設定網際網路郵件流程

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

若要建立透過 Edge Transport Server 的網際網路郵件，請向 Active Directory 站台訂閱 Edge Transport Server。這麼做會自動建立網際網路郵件流程所需的兩個傳送連接器：

  - 設定為將輸出電子郵件傳送到所有網際網路網域的傳送連接器。

  - 設定為將輸入電子郵件從 Edge Transport Server 傳送到 Exchange 2013 Mailbox Server 的傳送連接器。

如果不想要向 Active Directory 站台訂閱 Edge Transport Server，則可以手動建立在 Mailbox Server 與 Edge Transport Server 之間建立郵件流程所需的傳送連接器。如需相關資訊，請參閱[不使用 EdgeSync 設定 Edge Transport server 到網際網路郵件流程](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md)。不過，我們建議您儘可能向 Active Directory 站台訂閱 Edge Transport Server。

## 開始之前

  - 預估完成時間：20 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「EdgeSync」項目和「Edge Transport Server」。

  - 為您的組織訂閱 Edge Transport Server 之前，您必須先設定 Exchange 組織的授權網域和電子郵件地址原則。

  - 透過隔開周邊網路與 Exchange 組織的防火牆，啟用安全的 LDAP 連接埠 50636/TCP。Edge Transport Server 必須能夠與訂閱的 Active Directory 站台中的所有 Exchange 2013 Mailbox Server 通訊。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 透過訂閱的 Edge Transport Server 設定網際網路郵件流程

1.  在 Edge Transport Server 上，使用下列語法建立 Edge 訂閱檔案。
    
        New-EdgeSubscription -FileName <FileName>.xml [-Force]
    
    下列範例在 C:\\My Documents 資料夾中建立名為 EdgeSubscriptionInfo.xml 的 Edge 訂閱檔案。*Force* 參數會抑制用以確認將停用命令的提示，以及抑制 Edge Transport Server 的組態資料將被覆寫的警告。
    
        New-EdgeSubscription -FileName "C:\My Documents\EdgeSubscriptionInfo.xml" -Force

2.  將產生的 Edge 訂閱檔案複製到您訂閱 Edge Transport Server 的 Active Directory 站台中的 Mailbox Server。

3.  在 Mailbox Server 上，使用下列語法匯入 Edge 訂閱檔案。
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "<FileName>.xml" -Encoding Byte -ReadCount 0)) -Site <SiteName>
    
    此範例從 D:\\Data 資料夾匯入名為 EdgeSubscriptionInfo.xml 的 Edge 訂閱檔案，並且向名為 "Default-First-Site-Name" 的 Active Directory 站台訂閱 Edge Transport Server。
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "D:\Data\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -Site "Default-First-Site-Name"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以使用 <em>CreateInternetSendConnector</em> 或 <em>CreateInboundSendConnector</em> 參數，防止自動建立一或兩個必要的傳送連接器。如需詳細資訊，請參閱<a href="edge-subscriptions-exchange-2013-help.md">Edge 訂閱</a>。</td>
    </tr>
    </tbody>
    </table>


4.  在 Mailbox Server 上，執行下列命令以開始第一次 EdgeSync 同步處理。
    
        Start-EdgeSynchronization

5.  完成時，強烈建議您同時從 Edge Transport Server 和 Mailbox Server 中刪除 Edge 訂閱檔案。Edge 訂閱檔案包含在 LDAP 通訊處理期間使用的認證相關資訊。


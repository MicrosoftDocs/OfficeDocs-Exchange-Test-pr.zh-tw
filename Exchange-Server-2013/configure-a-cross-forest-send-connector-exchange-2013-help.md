---
title: '設定跨樹系傳送連接器: Exchange 2013 Help'
TOCTitle: 設定跨樹系傳送連接器
ms:assetid: 7840d172-071e-4f13-9379-2fe1eee1a7cc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945053(v=EXCHG.150)
ms:contentKeyID: 52062553
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定跨樹系傳送連接器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-02-21_

在Active Directory、*樹系*都代表您的目錄服務的外邊界。您可以建立傳送連接器啟用樹系之間的通訊。在本例中為連接器會使用基本驗證。

如需與設定連接器相關的其他管理工作，請參閱[連接器](connectors-exchange-2013-help.md)。

對於案例感興趣一角與使用此程序？請參閱下列主題：

  - [部署跨樹系拓撲中的 Exchange 2013](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間：20 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳送連接器」項目和「接收連接器」項目。

  - 如果您要開始安裝，請參閱[部署 Exchange 2013 的新安裝](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) 。安裝後您可以使用本主題的步驟來建立連接器來設定跨樹系拓撲。

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


## 您要執行的工作

## 在每個樹系中建立使用者帳戶

您必須使用基本驗證的每個樹系中建立使用者帳戶。在每個樹系中建立帳戶並將每一個用來進行通訊的 Exchange Server 的萬用安全性群組。這個帳戶傳送連接器所用以驗證其他樹系中的伺服器接收郵件。例如，提供使用者帳戶具有使用者主體名稱 (UPN) FourthCoffee@Contoso.com 身分必須是用來進行驗證 Fourth Coffee 網域中的 Exchange server 當郵件傳送至 Contoso 網域中的 Exchange server 的認證。

## 使用 EAC 來建立傳送連接器以將郵件路由傳送至 Exchange 2013 樹系

使用基本驗證建立跨樹系郵件流程。

1.  在 EAC 中，瀏覽至 \[**郵件流程**\>**傳送連接器**。按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[**新的傳送連接器**精靈\] 中指定的傳送連接器的名稱，然後選取**Internal類型**。按一下 \[**下一步**\]。

3.  選擇 \[**透過智慧主機路由傳送郵件**，並再按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[**新增智慧主機**\] 視窗中，指定第二個樹系中，例如 64.4.6.100 目標伺服器的 IP 位址。按一下 \[**儲存**並再**下一步**\]。
    
    **智慧主機驗證**，請選擇 \[**基本驗證**，並提供使用者名稱和密碼。此處您可以透過 TLS 的安全通訊選擇**優惠僅之後啟動 TLS 的基本驗證**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您使用透過 TLS 的基本驗證，則必須將目標伺服器設定為使用 X.509 憑證。</td>
    </tr>
    </tbody>
    </table>


4.  \[**位址空間**，按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[**新增網域**\] 視窗中，確定 SMTP 列為**類型**。**完全完整網域名稱 (FQDN)**\] 中，輸入接收網域，如 fourthcoffee.com。按一下 \[**儲存**並再**下一步**\]。

5.  **來源伺服器**上，按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[**選取伺服器**\] 視窗中，選擇要使用並按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")的伺服器。按一下 \[**確定\]**。

6.  按一下 \[**完成**\]。連接器會出現在清單中的傳送連接器。

建立傳送連接器之後，請將郵件傳送到原始的樹系的第二個樹系中建立的傳送連接器。在此例中完全完整網域名稱 (FQDN) 您指定將第一個樹系的網域名稱。例如，contoso.com。

## 使用命令介面設定傳送連接器的權限

此範例在命令介面中使用 Enable-CrossForestConnector.ps1 指令檔，設定傳送連接器的權限，以供在跨樹系拓撲中使用。

    .\Enable-CrossForestConnector.ps1 -Connector "Cross-Forest" -user "ANONYMOUS LOGON"

## 如何才能了解這是否正常運作？

若要確認您已成功建立電子郵件路由到第二個樹系、 從 （您可以使用 Outlook Web App） 您組織中使用者傳送訊息到您指定的**地址空間**的網域的傳送連接器。如果收件者收到郵件，您已成功設定的傳送連接器。

## 相關資訊

[建立電子郵件傳送至網際網路的傳送連接器](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[傳送連接器](send-connectors-exchange-2013-help.md)


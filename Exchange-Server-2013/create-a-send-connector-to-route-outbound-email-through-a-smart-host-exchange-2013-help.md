---
title: '建立傳送連接器路由傳送到智慧主機的外寄電子郵件: Exchange 2013 Help'
TOCTitle: 建立傳送連接器路由傳送到智慧主機的外寄電子郵件
ms:assetid: 4a9ef08e-bd62-4c6b-8790-d24fb0f8f24b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673059(v=EXCHG.150)
ms:contentKeyID: 50473182
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立傳送連接器路由傳送到智慧主機的外寄電子郵件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-02-07_

在某些情況下，您可能想要透過協力廠商智慧主控來路由傳輸電子郵件，例如您擁有對於輸出郵件執行原則檢查的網路裝置的情況。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>第三方智慧主機必須使用 SMTP 的傳輸。如果沒有，您應該使用的外部連接器或傳遞代理程式連接器。</td>
</tr>
</tbody>
</table>


對於案例感興趣一角與使用此程序？請參閱下列主題：

  - [設定郵件流程和用戶端存取](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳送連接器」項目。

  - 如果您要開始安裝，請參閱[部署 Exchange 2013 的新安裝](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) 。在安裝之後您可以使用本主題中的步驟來建立輸出連接器。

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


## 使用 EAC 來建立傳送連接器以路由傳輸透過智慧型主機輸出電子郵件

1.  在 EAC 中，瀏覽至 \[郵件流程\] \> \[傳送連接器\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[**新增傳送連接器**精靈\] 中指定的傳送連接器的名稱，然後選取**自訂類型**。當您想要路由傳送訊息到電腦未執行 Microsoft Exchange Server 2013通常選擇此選項。按一下 \[**下一步**\]。

3.  選擇 \[**透過智慧主機路由傳送郵件**，並再按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[**新增智慧主機**\] 視窗中，指定 IP 位址，例如 192.168.100.1 或完整的網域名稱 (FQDN)，例如 contoso.com。按一下 \[**儲存**\]。
    
    **智慧主機驗證**，請選擇 \[智慧主機所需的驗證類型\]。如果您選擇**基本驗證**，您必須提供使用者名稱和密碼。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若您選擇基本驗證，因為使用者名稱與密碼以純文字傳送，我們建議您使用加密連線。</td>
    </tr>
    </tbody>
    </table>


4.  \[**位址空間**，按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[**新增網域**\] 視窗中，確定 SMTP 列為**類型**。針對 \[**完全完整網域名稱 (FQDN)**\] 中，輸入 \* 若要指定這個傳送連接器套用到傳送至任何網域的郵件。按一下 \[**儲存**\]。

5.  **來源伺服器**上，按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[**選取伺服器**\] 視窗中，選擇伺服器並按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。按一下 \[**確定\]**。

6.  按一下 \[完成\]。

建立傳送連接器之後，它會出現在 \[傳送連接器\] 清單中。

## 如何才能了解這是否正常運作？

若要確認您已成功建立路由傳送到智慧主機的外寄電子郵件的傳送連接器，從 （您可以使用 Outlook Web App） 您組織中的使用者傳送訊息到您指定的**位址空間**的網域。如果收件者收到郵件，您已成功設定的傳送連接器。

## 相關資訊

[建立電子郵件傳送至網際網路的傳送連接器](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[傳送連接器](send-connectors-exchange-2013-help.md)


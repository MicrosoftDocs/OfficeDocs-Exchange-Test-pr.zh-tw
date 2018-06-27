---
title: '部署 Exchange 資源樹系拓撲中的 Exchange 2013: Exchange 2013 Help'
TOCTitle: 部署 Exchange 資源樹系拓撲中的 Exchange 2013
ms:assetid: 537a7b2b-d002-40a6-84ae-fd02635f9e23
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998031(v=EXCHG.150)
ms:contentKeyID: 51409195
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 部署 Exchange 資源樹系拓撲中的 Exchange 2013

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

本主題說明如何部署 Microsoft Exchange 2013Exchange資源樹系拓撲中。Exchange資源樹系也稱為專用的Exchange樹系。本主題假設您不需要現有Exchange 2013拓撲。

下圖顯示含有資源樹系的 Exchange 組織。

**含有 Exchange 資源樹系之 Exchange 組織的範例**

![具有資源樹系的複雜 Exchange 組織](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "具有資源樹系的複雜 Exchange 組織")

## 開始之前有哪些須知？

若要Exchange 2013中執行下列程序，確認您具備下列：

  - 您有下列兩種Active Directory樹系：
    
      - 一個樹系中會包含您組織的使用者帳戶。此程序，在此樹系會呼叫*帳戶樹系*。
    
      - 一個樹系中不包含使用者帳戶，但尚未沒有Exchange安裝。此程序，在此樹系會呼叫*Exchange 樹系*。您將在此樹系中安裝Exchange 2013使用程序。

  - 您已正確設定網域名稱系統 (DNS) 名稱解析為跨樹系組織中。若要檢查您已正確設定 DNS，ping 來自其他樹系或樹系組織中的每個樹系。如需設定 DNS 的詳細資訊，請參閱 ＜ [DNS Server 作業指南](https://go.microsoft.com/fwlink/p/?linkid=282295)。

## 部署 Exchange 資源樹系拓撲中的 Exchange 2013

1.  從Exchange樹系的網域控制站，建立傳出的單向信任，讓Exchange樹系信任帳戶樹系。詳細步驟請參閱[建立信任的兩側單向、 傳出，樹系信任](https://go.microsoft.com/fwlink/p/?linkid=69130)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>雖然建議您建立的樹系信任，您可以建立的樹系信任或外部信任。如果您建立的外部信任，當您在步驟 3 中建立連結的信箱新信箱精靈] 的 [<strong>主圖形帳戶</strong>] 頁面上，您必須指定可存取信任樹系中的網域控制站的使用者帳戶。您無法使用與您目前登入認證。如果您使用<strong>New-Mailbox</strong>指令程式建立連結的信箱，您必須指定使用<em>LinkedCredential</em>參數可存取信任樹系中的網域控制站的使用者帳戶。</td>
    </tr>
    </tbody>
    </table>


2.  Exchange樹系中安裝Exchange 2013。安裝Exchange一般的相同方式在單一樹系案例。如需如何安裝Exchange 2013的詳細步驟，請參閱下列主題：
    
      - [部署 Exchange 2013 的新安裝](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [使用安裝精靈安裝 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

3.  Exchange樹系中，每個使用者帳戶樹系已為信箱在Exchange樹系中建立的外部帳戶相關聯的信箱。詳細步驟請參閱[管理連結的信箱](manage-linked-mailboxes-exchange-2013-help.md)。


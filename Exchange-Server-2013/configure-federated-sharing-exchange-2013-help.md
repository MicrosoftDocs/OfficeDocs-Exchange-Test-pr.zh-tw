---
title: '設定同盟共用: Exchange 2013 Help'
TOCTitle: 設定同盟共用
ms:assetid: b25ae450-def3-4797-a5fc-6e9bcee71a5d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657483(v=EXCHG.150)
ms:contentKeyID: 50474010
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定同盟共用

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

使用者可以利用 Exchange Server 2013 中的同盟共用，與外部同盟組織中的收件者共用資訊。包括共用可供排程的空閒/忙碌 (也稱為行事曆可用性) 資訊，或依業務關係的本質，共用更詳細的行事曆資訊。若要深入了解同盟共用，請參閱[共用](sharing-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此 Exchange Server 2013 功能與中國的 21Vianet 所運作的 Office 365 不完全相容，部分功能可能受限。如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解 21Vianet 運作的 Office 365</a>。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 完成此工作的預估時間：1 小時。

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

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


## 該怎麼做？

## 步驟 1：建立和設定同盟信任

同盟信任會建立Exchange 2013組織和Azure Active Directory驗證系統之間的信任關係，並且是同盟共用的必要條件。

如需詳細指示，請參閱[設定同盟信任](configure-a-federation-trust-exchange-2013-help.md)。

## 步驟 2：建立組織關係

組織關聯性可讓使用者在 Exchange 組織共用行事曆空閒/忙碌資訊與其他同盟 Exchange 組織的同盟共用的一部分。兩個同盟的Exchange 2013組織之間或同盟的Exchange 2013組織和同盟的Exchange 2010組織之間可以設定同盟共用。

如需詳細指示，請參閱[建立組織關聯性](create-an-organization-relationship-exchange-2013-help.md)。

## 步驟 3：建立共用原則

共用原則可讓使用者自行建立，與不同類型的外部使用者對其行事曆資訊進行人員對人員共用。共用原則支援與外部同盟組織、外部非同盟組織以及具有網際網路存取的個人共用行事曆和連絡人資訊。如果您不需要設定人員對人員或連絡人共用 (僅限組織層級共用)，則不需要設定共用原則。

如需詳細指示，請參閱[建立共用原則](create-a-sharing-policy-exchange-2013-help.md)。

## 步驟 4：設定自動探索公用 DNS 記錄

您需要將別名正式名稱 (CNAME) 資源記錄新增至面向公用網路的 DNS。新的 CNAME 記錄應指向執行自動探索服務的網際網路對向 Exchange 2013 用戶端存取伺服器。

如需有關如何新增 CNAME 記錄的詳細指示，請參閱公用 DNS 記錄的主機服務。這通常是網際網路型服務，也可以主控您的網域網站。


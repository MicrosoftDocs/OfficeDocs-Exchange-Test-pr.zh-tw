---
title: 'Active Directory 準備 Exchange 2010_NoE12ServerWarning 之後無法安裝 Exchange 2007 角色: Exchange 2013 Help'
TOCTitle: Active Directory 準備 Exchange 2010_NoE12ServerWarning 之後無法安裝 Exchange 2007 角色
ms:assetid: 4e579f69-0de9-421c-ba31-4e63a25e6a45
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.noe12serverwarning(v=EXCHG.150)
ms:contentKeyID: 50473095
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory 準備 Exchange 2010\_NoE12ServerWarning 之後無法安裝 Exchange 2007 角色

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

當您執行 Microsoft Exchange Server 2010**Setup /PrepareAD**時，Microsoft Exchange Server Analyzer 工具會查詢現有Active Directory拓撲來決定是否要有任何 Microsoft Exchange Server 2007伺服器角色。如果不會偵測Exchange 2007伺服器角色，您會收到下列警告訊息：


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>若要準備透過 'Setup /PrepareAD' 及角色已偵測到此拓撲中沒有 Exchange Server 2007 組織的 Exchange Server 2010 將要安裝程式。此作業之後會以安裝所有的 Exchange Server 2007 角色無法運用。</p></td>
</tr>
</tbody>
</table>


在部署之前Exchange Server 2010、 考慮下列因素可能需要您部署Exchange 2007伺服器與部署Exchange 2007之前安裝的所有伺服器角色：

  - **協力廠商或內部開發的應用程式**  應用程式開發的Exchange 2003不可能會與Exchange 2010、 相容與因此需要升級或取代。您可以維護這些應用程式及Exchange 2003； 在相關聯的使用者人數移到Exchange 2007;或使用Exchange 2010相容版本取代的軟體。

  - **共存或移轉需求**  如果您打算將信箱移轉至您的組織，您可以部署Exchange 2007並使用 Microsoft 傳輸者套件，您也可以使用協力廠商共存或遷移解決方案。若要下載 Microsoft 傳輸者套件，請移至[Microsoft 傳輸者套件](http://go.microsoft.com/fwlink/?linkid=82688)位於 Microsoft 下載中心 」。

此外時評估貴組織的選項，請確定您已考慮下列問題：

  - 您必須在策略備妥Exchange 2003達到支援結束之前移動Exchange 2010依存的應用程式吗？如需詳細資訊，請造訪 Microsoft 支援生命週期網站頁面 ([https://go.microsoft.com/fwlink/?LinkID=55839](https://go.microsoft.com/fwlink/?linkid=55839))。

  - 您的策略是否需要 WebDAV 和 Web 服務共存 (Exchange 2007) 吗？

  - 您已考慮支援 Exchange 或其他 Microsoft 技術可讓您以符合共存或移轉需求的協力廠商產品吗？

  - 什麼是硬體生命週期方法 （繼續使用現有相同數目的 32 位元伺服器與購買新的 64 位元伺服器盡）？

  - 什麼是您的計劃進行移轉 （儘可能與移轉的分時期的策略中快速移轉的所有伺服器）？同樣地，為何您時間表的不同版本的Exchange共存？

如果您決定需要部署Exchange 2007伺服器部署Exchange 2010之前，部署的所有伺服器角色與單一Exchange 2007是足夠讓組織中的未來Exchange 2007伺服器的部署。若要將Exchange 2003組織部署Exchange 2007伺服器，遵循下列步驟：

1.  執行Exchange 2007**Setup /PrepareSchema**。

2.  執行Exchange 2007**Setup /PrepareAD**。

3.  包含的收件者、 Exchange 2003伺服器\] 或 \[無法Exchange伺服器所使用的通用類別目錄的所有網域上執行Exchange 2007**Setup /PrepareDomain** 。

4.  安裝所有的四個伺服器角色 （Hub Transport、 Client Access、 Mailbox 及整合通訊） Exchange 2007伺服器。


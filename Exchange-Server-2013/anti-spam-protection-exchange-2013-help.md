---
title: '反垃圾郵件保護: Exchange 2013 Help'
TOCTitle: 反垃圾郵件保護
ms:assetid: 6af88a08-687d-40b1-8b22-80704184403d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ218660(v=EXCHG.150)
ms:contentKeyID: 50473436
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 反垃圾郵件保護

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-06_

*垃圾郵件*或惡意的寄件者使用各種技術 （英文） 的垃圾電子郵件傳送至您的組織。任何單一工具或程序，即可以去除所有的垃圾郵件。不過，Microsoft Exchange Server 2013提供分層、 multipronged、 及面向方法來減少這些不想要的訊息。Exchange 使用傳輸代理程式提供反垃圾郵件保護及Exchange 2013中可用的內建代理程式會從 Microsoft Exchange Server 2010較不變。

如需反垃圾郵件功能和更容易管理，您可以選取要購買 Microsoft Exchange Online Protection (EOP)。如需 EOP 和Exchange 2013功能的比較，請參閱[Exchange Server 2013 上 Exchange Online Protection 中反垃圾郵件功能的優點](benefits-of-anti-spam-features-in-exchange-online-protection-over-exchange-server-2013-exchange-2013-help.md)。若要深入了解Office 365反垃圾郵件保護，請參閱[Office 365 電子郵件反垃圾郵件保護](https://support.office.com/en-us/article/office-365-email-anti-spam-protection-6a601501-a6a8-4559-b2e7-56b59c96a586?ui=en-us%26rs=en-us%26ad=us)。

如需 Exchange 2013 內建的反惡意程式碼功能的相關資訊，請參閱[反惡意程式防護](anti-malware-protection-exchange-2013-help.md)。

**目錄**

Anti-spam agents on Mailbox servers

Anti-spam agents on Edge Transport servers

Anti-spam stamps

Strategy for anti-spam approach

## Mailbox Server 的反垃圾郵件代理程式

通常您會啟用 mailbox server 上的反垃圾郵件代理程式如果您的組織都不會有 Edge Transport server，或沒有任何先前的反垃圾郵件篩選之前接受傳入訊息。如需詳細資訊，請參閱[啟用信箱伺服器上的反垃圾郵件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

所有傳輸代理程式，例如每個反垃圾郵件代理程式指派的優先順序值。較低值表示較高的優先順序，因此通常、 優先順序 1 的反垃圾郵件代理程式將優先順序 9 時對之前的反垃圾郵件代理程式的訊息。不過，反垃圾郵件代理程式已註冊所在的 SMTP 事件也是非常重要的決定反垃圾郵件代理程式處理郵件的順序。低優先順序反垃圾郵件代理程式登錄在早期傳輸管線中的 SMTP 事件會處理高優先順序反垃圾郵件代理程式登錄在 SMTP 事件稍後傳輸管線中的前一則訊息。

依據反垃圾郵件代理程式預設的優先順序值，以及在傳輸管道中已註冊反垃圾郵件代理程式的 SMTP 事件，以下清單會針對代理程式和其套用至 Mailbox Server 郵件的預設順序進行說明：

1.  **寄件者篩選器代理程式**  寄件者篩選會比較在郵件的寄件者 ︰ SMTP 命令以系統管理員定義的寄件者或寄件者的網域會禁止傳送郵件給組織內送郵件採取的任何決定何種動作\] 清單。如需詳細資訊，請參閱[寄件者篩選](sender-filtering-exchange-2013-help.md)。

2.  **寄件者識別碼代理程式**  寄件者識別碼依賴傳送伺服器的 IP 位址和旨在負責地址 (PRA) 來決定是否寄件者詐騙或不寄件者。如需詳細資訊，請參閱[寄件者識別碼](sender-id-exchange-2013-help.md)。

3.  **內容篩選器代理程式**  內容篩選評估郵件的內容。如需詳細資訊，請參閱[內容篩選](content-filtering-exchange-2013-help.md)。
    
    垃圾郵件隔離區是可以降低風險遺失合法未正確分類為垃圾郵件的郵件內容篩選器代理程式的功能。垃圾郵件隔離區提供的會被識別為垃圾郵件和，不應該傳遞給組織內部的使用者信箱的郵件的暫存的儲存位置。如需詳細資訊，請參閱[垃圾郵件隔離](spam-quarantine-exchange-2013-help.md)。
    
    內容篩選也會對安全清單彙總功能。安全清單彙總從 Microsoft Outlook 和 Outlook Web App 的使用者設定的反垃圾郵件安全清單收集資料，並讓內容篩選器代理程式可以使用此資料。如需詳細資訊，請參閱[安全清單彙總](safelist-aggregation-exchange-2013-help.md)。

4.  **通訊協定分析代理程式**  通訊協定分析代理程式為基礎代理程式可實作寄件者信譽功能。寄件者信譽依賴關於內送郵件採取的任何決定何種巨集指令，傳送伺服器的 IP 位址的持續性資料。寄件者信譽等級 (SRL) 會計算衍生自郵件分析與外部測試的數個寄件者特性。如需詳細資訊，請參閱[寄件者信譽和通訊協定分析代理程式](sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md)。

回到頁首

## Anti-spam agents on Edge Transport servers

如果您的組織已安裝在周邊網路的 Edge Transport server，所有可用的信箱伺服器的反垃圾郵件代理程式會安裝並啟用 Edge Transport server 上的預設值。不過，下列反垃圾郵件代理程式可用只在 Edge Transport server 上：

  - **連線篩選代理程式**  連線篩選會檢查嘗試傳送訊息來決定何種巨集指令，內送郵件採取的任何遠端伺服器的 IP 位址。連線篩選使用 IP 封鎖清單、 IP 允許清單、 IP 封鎖清單提供者服務及 IP 允許清單提供者服務來決定是否應封鎖或允許連線 IP。如需詳細資訊，請參閱[在 Edge Transport Server 上的連線篩選](connection-filtering-on-edge-transport-servers-exchange-2013-help.md)。

  - **收件者篩選器代理程式**  收件者篩選會比較在 RCPT TO 郵件收件者 ︰ SMTP 命令以系統管理員所定義的收件者封鎖清單。如果找到相符項目，就不允許郵件進入組織。收件者篩選器也比較本機收件者的目錄來決定是否傳送郵件給有效收件者的內送郵件上的收件者。有效的收件者無法傳送給一則訊息，當郵件被拒絕。如需詳細資訊，請參閱[Edge Transport Server 上的收件者篩選](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>雖然收件者篩選器代理程式是可在信箱伺服器上，您不應該進行設定。收件者篩選信箱伺服器上包含其他有效收件者在郵件中偵測一個無效或封鎖收件者，當郵件被拒絕。如果您在信箱伺服器上安裝的反垃圾郵件代理程式，預設會啟用收件者篩選器代理程式。不過，它不被設定為封鎖任何收件者。</td>
    </tr>
    </tbody>
    </table>


  - **附件篩選代理程式**  附件篩選封鎖根據附件檔案名稱、 副檔名或檔案 MIME 內容類型的郵件。您可以設定附件篩選來封鎖郵件和其附件，若要刪除附件並允許郵件通過，或以無訊息方式刪除郵件和其附件。如需詳細資訊，請參閱[Edge Transport server 上的附件篩選](attachment-filtering-on-edge-transport-servers-exchange-2013-help.md)。

依據反垃圾郵件代理程式預設的優先順序值，以及傳輸管道中已註冊反垃圾郵件的 SMTP 事件，以下為代理程式套用至 Edge Transport Server 的預設順序：

1.  連線篩選代理程式

2.  寄件者篩選器代理程式

3.  收件者篩選器代理程式

4.  寄件者識別碼代理程式

5.  內容篩選器代理程式

6.  寄件者信譽的通訊協定分析代理程式

7.  附件篩選代理程式

回到頁首

## 反垃圾郵件戳記

反垃圾郵件戳記可協助您診斷套用診斷的中繼資料、 或戳記，例如特定寄件者的資訊、 拼圖驗證結果，以及內容篩選結果，郵件通過時篩選來自網際網路的內送的郵件的反垃圾郵件功能的垃圾郵件相關的問題。如需詳細資訊，請參閱[反垃圾郵件戳記](anti-spam-stamps-exchange-2013-help.md)。

回到頁首

## 反垃圾郵件方法的策略

如何設定反垃圾郵件功能並建立您的反垃圾郵件代理程式設定加強策略會要求您規劃及謹慎計算。若設為其最不積極的層級的所有反垃圾郵件篩選器，並設定拒絕所有的可疑郵件的所有反垃圾郵件功能，您正在較可能拒絕不垃圾郵件的郵件。換句話說，如果您不要在足以不積極的層級設定的反垃圾郵件篩選器並不需要設定垃圾郵件信賴等級 (SCL) 閾值不夠低，可能就無法看到減少進入組織垃圾郵件。

它會拒絕郵件時 Exchange 偵測到連線篩選代理程式、 收件者篩選器代理程式或寄件者篩選器代理程式的錯誤訊息的最佳作法。這個方法是優於隔離這類郵件或將中繼資料，例如反垃圾郵件戳記指派給這類郵件。連線篩選代理程式及收件者篩選器代理程式自動封鎖的個別篩選器所識別的訊息。寄件者篩選器代理程式是可設定。

此最佳作法是建議使用，因為 SCL 底層連線篩選、 收件者篩選或寄件者篩選是較高。例如，與寄件者篩選，其中管理員已設定特定的寄件者封鎖，沒有理由來指派寄件者篩選到這類郵件的資料，而以繼續處理它們。在大多數的組織應拒絕封鎖的郵件。（如果您不想拒絕郵件，您有用已將其置於 \[封鎖的寄件者清單上。）

相同的邏輯適用於即時封鎖清單服務和收件者篩選，雖然基礎信賴不是高達 IP 封鎖清單。您應該注意的進一步的郵件流程路徑郵件一起出差、 更機率的誤判，因為反垃圾郵件功能的評估多個變數。因此，您可能會發現是否更積極反垃圾郵件鏈結中設定第一個數個反垃圾郵件功能，您可以減少在垃圾郵件的大量。因此，您將儲存處理、 頻寬及磁碟資源，讓您可以處理更多不明確的郵件。

最終，您必須要監視的反垃圾郵件功能的整體效率。如果您監視小心，您可以繼續調整以為您的環境以及共同運作的反垃圾郵件功能。使用這個方法，您應該規劃的反垃圾郵件功能的許多非積極設定在啟動時。這個方法可讓您將誤報數目降至最低。當您監視及調整的反垃圾郵件功能，您會變得更積極有關垃圾郵件和您的組織經驗的垃圾郵件攻擊的類型。

回到頁首

## 請參閱


[Office 365 電子郵件反垃圾郵件保護](https://support.office.com/en-us/article/office-365-email-anti-spam-protection-6a601501-a6a8-4559-b2e7-56b59c96a586?ui=en-us%26rs=en-us%26ad=us)


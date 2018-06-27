---
title: 'Exchange Server 2013 上 Exchange Online Protection 中反垃圾郵件功能的優點: Exchange 2013 Help'
TOCTitle: Exchange Server 2013 上 Exchange Online Protection 中反垃圾郵件功能的優點
ms:assetid: 00e37a3c-3fbc-488f-bdad-d52a3c80fd72
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673032(v=EXCHG.150)
ms:contentKeyID: 50472447
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange Server 2013 上 Exchange Online Protection 中反垃圾郵件功能的優點

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-05-26_

使用 Exchange 反垃圾郵件保護而非 Microsoft Exchange Server 2013，充分運用 Microsoft Exchange Server 2010為相同的內建反垃圾郵件功能且在雲端 （Microsoft Exchange Online或 Microsoft Exchange Online Protection） 的好處如下：

  - **更多控制及更輕鬆地設定**  管理員可以使用Exchange 系統管理中心 (EAC) web 式管理主控台以便自訂垃圾郵件篩選設定使其最佳符合組織的需求。Exchange Server 2013中有任何反垃圾郵件使用者介面。EOP 反垃圾郵件保護功能都包含在Exchange Online

  - **更有力的連線篩選**  在Exchange 2013、 連線篩選 IP 允許清單與 IP 封鎖清單是只有當您在周邊網路中安裝 Edge Transport server。如需詳細資訊，請參閱[Edge Transport Server](edge-transport-servers-exchange-2013-help.md)。雲端中，您可以選擇略過垃圾郵件篩選上從信任的寄件者 （來自各種與協力廠商來源收集）、 確保的這些訊息未遭標示為垃圾郵件傳送的電子郵件訊息。而且、 託管的篩選服務會使用 Microsoft 自己封鎖清單及清單彙總從廠商提供更大 IP 層級篩選。

  - **更有力的內容篩選**  可輕鬆將內容篩選原則設定為：
    
      - 篩選以特定語言編寫的郵件。
    
      - 篩選寄自特定國家或地區的郵件。
    
      - 將大量電子郵件訊息（例如廣告與行銷郵件）標記為垃圾郵件。
    
      - 搜尋郵件中的屬性，若符合特定的進階垃圾郵件選項屬性則對該郵件採取行動。若您對於網路釣魚有疑慮，這些選項中部分提供結合寄件者識別碼與 SPF 科技的功能，可驗證並確認郵件不會遭到詐騙。
    
    除上列可設定於 EAC 中的內容篩選選項外，主控篩選服務將使用額外的 URL 清單來封鎖郵件內文中包含特定 URL 的可疑郵件。

  - **更快的更新**  垃圾郵件更新以更快的速度傳播於網路中。在 Exchange Server 2013 中每個月皆會有兩次更新，而服務則是每小時會有多次更新。

  - **外寄郵件篩選**  如果您使用託管服務來傳送外寄電子郵件，則一律會進行外寄垃圾郵件篩選，藉以保護使用此服務的組織與其預定的收件者。


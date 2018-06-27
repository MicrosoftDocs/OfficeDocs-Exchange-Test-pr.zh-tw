---
title: '檢閱您組織中的語音信箱通話: Exchange Online Help'
TOCTitle: 檢閱您組織中的語音信箱通話
ms:assetid: f6fdbe17-d1d2-442a-aa13-06b908d9c33a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ659073(v=EXCHG.150)
ms:contentKeyID: 50554087
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢閱您組織中的語音信箱通話

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以使用通話統計資料報告檢視類型與組織中的 Exchange 伺服器所處理的傳入呼叫的狀態資訊。「 報告 」 提供有關轉寄給或您的組織發出由整合通訊 (UM) 呼叫統計資訊。您可以使用這項資訊來追蹤容量規劃中的使用情況、 監視及疑難排解的可用性和音訊品質 UM，並疑難排解通話失敗。

本主題回答這些問題：

  - How do I get call statistics for UM?

  - How do I interpret UM call statistics?

如需與 UM 報告相關的其他工作，請參閱 [UM 報告程序](um-reports-procedures-exchange-2013-help.md)。

## 如何取得 UM 的呼叫統計資料？

1.  在 Exchange 系統管理中心 (EAC) 中，按一下 **\[整合通訊\]** \> **\[更多選項\]**![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示") \> **\[呼叫統計資料\]**。

2.  選擇您想要包含在報表中的資訊。報表會自動更新當您選取任何下列選項：
    
      - **顯示：**選擇要檢視的呼叫統計資料類型：
        
          - **每日 (90 天)：**選取 \[每日\] 可查看過去 90 天所有通話的詳細資料。
        
          - **每月 (12 個月)：**選取 \[每月\] 可查看過去 12 個月的每月通話摘要。
        
          - **全部：**選取 \[全部\] 可查看自從 UM 開始處理通話以來所收到之所有通話的結合統計資料。
    
      - **UM 撥號對應表：**如果您想要將報告中的資料限制為僅限特定 UM 撥號對應表中的通話，請選取該撥號對應表。
    
      - **UM IP 閘道器**  如果您想要限制只在特定的 UM IP 閘道呼叫報表中的資料，請選取該閘道。如果您先選取 UM 撥號對應表，只選取 UM 撥號對應表相關聯的 UM IP 閘道都可在清單中。

3.  若要取得音訊品質的更多詳細報告中的列，選取的資料列，按一下 \[**音訊品質詳細資料**。如需如何轉譯音訊品質的詳細資訊，請參閱[調查組織中的語音通話的音訊品質](investigate-the-audio-quality-of-voice-calls-in-your-organization-exchange-2013-help.md)。

4.  若要將報告複製至剪貼簿，請按一下 \[複製\]。

5.  若為「每日」報告，您可以將特定日期的詳細資料匯出至 .csv 檔案。
    
    1.  選取日期，然後按一下 \[匯出日期\]。
    
    2.  在 \[檔案下載\] 確認方塊中，按一下 \[開啟\] 或 \[儲存\]。
    
    匯出的檔案會命名為 um\_cdr\_*YYYY-MM-DD*.csv、 *YYYY-MM-DD*所在年、 月和日上次執行報表。如需詳細資訊，請參閱[解譯語音信箱通話記錄](interpret-voice-mail-call-records-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在報告頁面上，您可以下載 Microsoft Excel 範本，用於匯入特定日期的 .csv 檔案。</td>
    </tr>
    </tbody>
    </table>


回到頁首

## 如何解譯 UM 呼叫統計資料？

「UM 呼叫統計資料」報告包含下列資訊：

  - **日期**  UTC 通話資料的日期。日期格式取決於您所選擇的報告和地區設定的類型。您可以選擇下列選項：
    
      - **---：**顯示所有通話。
    
      - **MMM/YY**  通話的月份。例如，Jan/13。
    
      - **MM/DD/YY**  呼叫的日期。例如 6/23/13。

  - **總數：**在該日期中，選取之 UM 撥號對應表或 UM IP 閘道的通話總數。

  - **語音訊息：**由 UM 代表使用者接聽，而且來電者有留下語音訊息之來電所佔的百分比。

  - **未接：**由 UM 代表使用者接聽，而來電者未留下語音訊息以致產生未接來電通知之來電所佔的百分比。

  - **Outlook 語音存取：**由使用者登入 UM (而且已驗證) 以存取電子郵件、行事曆和語音訊息之來電所佔的百分比。

  - **外寄**  已由發出或轉接 UM 代表已驗證或未經過驗證的使用者的通話百分比。此統計資料包含尋找我、 在電話上播放和電話問候語通話類型上播放。

  - **自動語音應答：**由 UM 自動語音應答接聽之來電所佔的百分比。

  - **傳真：**由重新導向至傳真協力程式之來電所佔的百分比。

  - **其他**  任何其他連入或放置呼叫執行不屬於任何上述類別中的百分比。這些電話包括撥打 Outlook 語音存取號碼使用者未登入與未經過驗證的位置。

  - **失敗或已拒絕**  失敗或拒絕由 UM 的通話百分比。請注意通話失敗不被計算兩次。例如，如果 Outlook 語音存取呼叫失敗，其是只計算失敗通話，以及不為 Outlook 語音存取通話。

  - **音訊品質：**組織在選取時段內整體音訊品質的圖形表示。

回到頁首

## 相關資訊

[調查組織中的語音通話的音訊品質](investigate-the-audio-quality-of-voice-calls-in-your-organization-exchange-2013-help.md)

[解譯語音信箱通話記錄](interpret-voice-mail-call-records-exchange-2013-help.md)


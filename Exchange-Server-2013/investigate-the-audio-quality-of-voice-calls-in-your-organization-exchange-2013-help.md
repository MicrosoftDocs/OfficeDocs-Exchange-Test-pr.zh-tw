---
title: '調查組織中的語音通話的音訊品質: Exchange Online Help'
TOCTitle: 調查組織中的語音通話的音訊品質
ms:assetid: 8a87694b-1678-4a01-859f-5ad3b2c73db5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ659069(v=EXCHG.150)
ms:contentKeyID: 50554024
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 調查組織中的語音通話的音訊品質

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-21_

如果您的組織發生 Unified Messaging (UM) 呼叫與語音郵件訊息的音訊品質問題，請使用呼叫統計資料報告以協助您瞭解問題的肇因。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不涵蓋報告中的因素會受通話的音訊品質。例如，如果您的 Exchange 伺服器負載大量記憶體或 CPU 負載量，使用者可能會報告收訊不良通話品質即使報告顯示實用的音訊品質。</td>
</tr>
</tbody>
</table>


有關與呼叫統計資料相關的額外工作，請參閱 [UM 報告程序](um-reports-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md) 主題中的「UM 呼叫資料與摘要報告命令程式」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 使用 EAC 以取得您組織的音訊品質統計資料

1.  在 EAC 中，瀏覽到 \[整合通訊\]\> \[更多選項\]![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示") \> \[呼叫統計資料\]。

2.  選擇要包含在報表中的呼叫統計資料。報表會自動更新當您選取任何下列的選項。
    
      - **顯示：**選擇要檢視的呼叫統計資料類型：
        
          - **每日 (90 天)：**選取 \[每日\] 可查看過去 90 天所有通話的詳細資料。
        
          - **每月 (12 個月)：**選取 \[每月\] 可查看過去 12 個月的每月通話摘要。
        
          - **全部：**選取 \[全部\] 可查看自從 UM 開始處理通話以來所收到之所有通話的結合統計資料。
    
      - **UM 撥號對應表：**如果您想要將報告中的資料限制為僅限特定 UM 撥號對應表中的通話，請選取該撥號對應表。
    
      - **UM IP 閘道器**  如果您想要限制只在特定的 UM IP 閘道呼叫報表中的資料，請選取該 UM IP 閘道器。如果您先選取 UM 撥號對應表，只選取 UM 撥號對應表相關聯的 UM IP 閘道都可在清單中。

3.  若要取得音訊品質的更多詳細報告中的列，選取的資料列，按一下 \[**音訊品質詳細資料**。是下列資訊：
    
      - **日期與時間**   擷取呼叫統計資料的 UTC 日期與時間。
    
      - **UM 撥號對應表**   包括在統計資料中的呼叫撥號對應表。
    
      - **UM IP 閘道**   包括在統計資料中，回應呼叫的 UM IP 閘道。
    
      - **NMOS**  網路平均意見分數 (NMOS) 的通話。NMOS 指出如何良好的音訊品質有關該通話為介於 1 到 5，具有正在實用的 5 規模上的號碼。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>可能的通話的最大 NMOS 是取決於所使用的音訊轉碼器。NMOS 可能無法極短通話所少於 10 秒的 long。</td>
        </tr>
        </tbody>
        </table>
    
      - **NMOS 效能下降**  從上方的值可能正在使用的音訊轉碼器的 NMOS 的音訊降低量。例如，如果來電的 NMOS 效能下降值是 1.2 NMOS 報告通話所 3.3，該特定的通話的最大的 NMOS 就是 4.5 (1.2 + 3.3)。
    
      - **抖動**   該呼叫的資料封包抵達的平均變動。
    
      - **封包遺失**  資料封包遺失所選通話的平均百分比。封包遺失是可靠性的相對值的連線。
    
      - **來回**  平均來回分數，選取通話的音訊 （毫秒）。來回分數措施連接上的延遲。
    
      - **連續遺失持續時間**   選取呼叫的封包遺失之平均持續時間。
    
      - **範例數**   用於計算平均的採樣呼叫數。

4.  如需特定呼叫的詳細音訊品質度量，請參閱 [調查的使用者的語音通話的音訊品質](investigate-the-audio-quality-of-voice-calls-for-a-user-exchange-2013-help.md)。


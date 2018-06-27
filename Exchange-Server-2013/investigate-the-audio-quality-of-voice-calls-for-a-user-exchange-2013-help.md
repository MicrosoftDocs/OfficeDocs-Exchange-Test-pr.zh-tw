---
title: '調查的使用者的語音通話的音訊品質: Exchange Online Help'
TOCTitle: 調查的使用者的語音通話的音訊品質
ms:assetid: 0c945886-3cfa-423e-9b46-0d6b1584a145
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ659059(v=EXCHG.150)
ms:contentKeyID: 50553932
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 調查的使用者的語音通話的音訊品質

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-21_

如果使用者回報其整合通訊 (UM) 通話的音訊品質發生問題，您可以使用「使用者通話記錄」報告來協助您了解造成問題的原因。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不涵蓋報告中的因素會受通話的音訊品質。例如，如果您的 Exchange 伺服器遭遇大量記憶體或 CPU 負載，使用者可能會報告收訊不良通話品質即使報告顯示實用的音訊品質。</td>
</tr>
</tbody>
</table>


如需了解有關 UM 報告的其他工作，請參閱 [UM 報告程序](um-reports-procedures-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

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


## 使用 EMC 取得已啟用 UM 之使用者的通話記錄

1.  在 EAC 中瀏覽至 \[整合通訊\] \> \[更多選項\]![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示") \> \[使用者通話記錄\]。

2.  按一下 \[選取使用者\]，然後選取您想要取得哪一位使用者的資料。

3.  若要取得音訊品質的更多詳細報告中的列，選取的資料列，按一下 \[**音訊品質詳細資料**。是下列資訊：
    
      - **日期和時間**   通話的日期和時間 (根據選定使用者在 Outlook Web App 中設定的時區)。
    
      - **使用者**   選取的使用者。
    
      - **UM 撥號對應表**   通話的撥號對應表。
    
      - **UM IP 閘道**   用於通話的 UM IP 閘道。
    
      - **音訊轉碼器**   通話期間使用的音訊轉碼器。
    
      - **NMOS**  網路平均意見分數 (NMOS) 的通話。NMOS 指出如何良好的音訊品質有關該通話為介於 1 到 5，具有正在實用的 5 規模上的號碼。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>可能的通話的最大 NMOS 取決於所使用的音訊轉碼器。NMOS 可能無法極短通話所少於 10 秒的 long。</td>
        </tr>
        </tbody>
        </table>
    
      - **NMOS 效能下降**  從上方的值可能正在使用的音訊轉碼器的 NMOS 的音訊降低量。例如，如果來電的 NMOS 效能下降值是 1.2 NMOS 報告通話所 3.3，該特定的通話的最大的 NMOS 就是 4.5 (1.2 + 3.3)。
    
      - **抖動**   該呼叫的資料封包抵達的平均變動。
    
      - **封包遺失**  資料封包遺失所選通話的平均百分比。封包遺失是可靠性的相對值的連線。
    
      - **來回**  平均來回分數，選取通話的音訊 （毫秒）。來回分數措施連接上的延遲。
    
      - **連續遺失持續時間**   選取呼叫的封包遺失之平均持續時間。


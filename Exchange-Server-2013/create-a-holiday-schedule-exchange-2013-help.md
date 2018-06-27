---
title: '若要建立假日排程: Exchange Online Help'
TOCTitle: 若要建立假日排程
ms:assetid: 0c5c51e4-5b51-451b-ab93-2cebf644dc96
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb266921(v=EXCHG.150)
ms:contentKeyID: 50472541
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 若要建立假日排程

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-19_

您可以定義您的組織將會關閉假日和其他情況的日期與時間。開始日期和結束日期之間您指定、 來電者連絡整合通訊 (UM) 自動語音應答會聽到歡迎您的假日會指定當您設定假日排程。來電者聽到您所指定的假日問候語之後，來電者會播放的非上班時間問候語和功能表提示。

您也可以建立假日排程中現有的假日排程。當您建立多個假日排程時，整合通訊可讓您重疊排定的假日時間。例如，您可以定義從年 12 月 15 日至年 12 月 31 當您的組織將會關閉的情況下，但您可以定義其他的假日排程和年 12 月第 24 透過年 12 月 26 假日排程。來電者撥入時的自動語音應答從年 12 月 15 日至 23rd 年 12 月和年 12 月 27 透過年 12 月 31 日，他們將出現您指定此排程的假日問候語。例如，"我們是目前已關閉的情況。"來電者撥入時的自動語音應答從年 12 月第 24 透過年 12 月 26 日，他們將出現與另一個假日問候語，例如"我們目前關閉 for business，讓我們員工可以使用其系列享受假日。 」

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 自動語音應答」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 自動語音應答。如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

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


## 您要執行的工作

## 使用 EAC 指定 UM 自動語音應答的假期排程

1.  在 EAC 中，瀏覽至 \[**整合通訊**\> **UM 撥號對應表**。在清單檢視中，選取您想要變更 UM 撥號對應表，然後按一下工具列上的 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[ **UM 撥號對應表**\] 頁面上 \[ **UM 自動語音應答**，選取您要設定的假日排程的 UM 自動語音應答。在工具列上，按一下 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 自動語音應答\]** 頁面 \> **\[上班時間\]** 的 **\[假期排程\]** 下，按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在 \[新增假日\] 頁面上，設定下列項目：
    
      - **名稱：**輸入您的假期排程名稱。
    
      - **假日問候語**  瀏覽至您想要作為您的問候語的.wav 檔。這是必要的欄位。
    
      - **開始日期**  使用此清單中選取您想要啟動之假日的日期。在此清單中所指定日期的午夜起點假日排程。
    
      - **結束日期**  使用此清單中選取您希望假日結束的日期。這份清單中指定的日期下午 11:59，將會結束假日排程。

5.  在您設定假期排程後，按一下 \[確定\]，然後按兩次 \[儲存\]。

## 使用命令介面指定 UM 自動語音應答的假期排程

此範例會設定名為 `MyUMAutoAttendant` 的 UM 自動語音應答，其上班時間已設為 10:45 到 13:15 (星期日)、09:00 到 17:00 (星期一) 和 09:00 到 16:30 (星期六)，而假期時間及其關聯的問候語則設為 2013 年 1 月 2 日的「新年」，以及從 2013 年 4 月 24 日到 2013 年 4 月 28 日的「大樓封閉施工」。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"


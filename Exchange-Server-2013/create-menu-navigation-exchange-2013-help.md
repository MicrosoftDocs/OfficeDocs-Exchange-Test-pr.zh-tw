---
title: '建立功能表導覽: Exchange Online Help'
TOCTitle: 建立功能表導覽
ms:assetid: 3cfc9a01-0a61-4d15-9561-621568dc30d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997471(v=EXCHG.150)
ms:contentKeyID: 50472927
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.AutoAttendantKeyMappingControl
ms.translationtype: MT
---

# 建立功能表導覽

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-05_

您可以使用**新的功能表導覽項目**頁面來建立單一或多個關鍵對應的商務或非上班時間主功能表提示自動語音應答。您可以定義時電話鍵盤上按下按鍵，例如呼叫轉接至分機號碼或另一個自動語音應答所執行的動作。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

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

## 使用 EAC 來設定 UM 自動語音應答導覽功能表

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[ **UM 撥號對應表**\] 頁面上 \[ **UM 自動語音應答**，選取您要建立功能表導覽的 UM 自動語音應答。在工具列上，按一下 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[ **UM 自動語音應答**\] 頁面上按一下 \[**功能表導覽**、 選取 \[**啟用上班時間功能表導覽**\] 或 \[**啟用非上班時間功能表導覽**，和 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在 \[**新的功能表導覽項目**\] 頁面上設定下列項目：
    
      - **提示**  使用此方塊可輸入新的瀏覽功能表的名稱。只顯示適用於導覽功能表名稱。這是必要的欄位。
        
        若要指定多個新的瀏覽功能表，因為我們建議您使用您的按鍵對應的有意義的名稱。按鍵對應名稱的最大長度是 64 個字元，而且它可以包含空格。不過，它不能包含任何下列字元："/ \\ \[\]:; |= , + \* ?\< \>。
    
      - **當按下此按鍵**  若要啟用關鍵對應使用此清單。按鍵對應是來電者按下有執行特定作業，例如的自動語音應答轉接來電者至另一個自動語音應答或操作員的數字金鑰。根據預設，不定義任何項目。
        
        使用下拉式清單中選取來電者必須按下的數字鍵 （從 1 到 9)。零 (0) 保留為自動語音應答運算子。
        
        如果您從下拉式清單中選取**逾時時間**，它可讓來電者轉接至分機號碼或另一個自動語音應答如果它們不在電話鍵盤上按下某個按鍵。例如，「 請保持在列上與將會由下一個可用的人接聽您的來電 」。預設值為 5 秒。如果您啟用此選項時，會建立空白的按鍵對應。
    
      - **播放下列音訊檔案**  使用此選項的來電者選取先前錄製的音訊檔案。按一下 \[**變更**\] 及 \[**瀏覽\]**找出的音訊檔案。
    
      - **執行此額外動作**   選取下列其中一個選項，定義您要自動語音應答針對來電者執行的動作：
        
          - **無**  如果您不想要自動語音應答來電轉接至分機或另一個自動語音應答，或留下訊息給使用者，請使用此選項。
        
          - **轉接到這個分機**  選取此選項可讓來電轉接至分機號碼。如果您啟用此選項，用於\] 方塊中輸入副檔名會將轉接通話。此欄位可讓僅限數字的字元。它不能包含任何下列字元："/ \\ \[\]:; |= , + \* ?\< \>。
        
          - **轉接到這個 UM 自動語音應答**  選取此選項可將電話轉接到自動語音應答。按一下 \[**瀏覽\]**找出您想要使用的自動語音應答。啟用此選項之前，您必須先建立及設定的自動語音應答。當您建立 UM 自動語音應答的父/子結構時使用此選項。
        
          - **留下語音訊息給這位使用者**  選取此選項可讓來電者留下語音郵件訊息的使用者而言是在同一個撥號對應作為您正在設定 UM 自動語音應答。當來電者的自動語音應答功能表選擇這個選項時，系統會提示他們將留下語音訊息所選使用者。按一下 \[**瀏覽\]**找出已啟用 UM 的使用者。
        
          - **宣告公司地點**  選取此選項可讓來電者選擇一個自動語音應答功能表選項和聽到公司的 UM 自動語音應答上設定的位置。若要啟用此選項可正常運作，您必須先將公司地點**商務位置**\] 方塊中輸入 \[**一般**\] 頁面上的 UM 自動語音應答。
        
          - **宣告的營業時間**  選取此選項可讓來電者選擇一個自動語音應答功能表選項和聽到的作業已在 UM 自動語音應答設定營業時間。若要啟用此選項可正常運作，您必須先在**上班時間**\] 頁面上的 UM 自動語音應答上設定營業時間。

5.  按一下 \[確定\] 來建立新的功能表導覽。

6.  在 \[UM 自動語音應答\] 頁面上，按一下 \[儲存\] 儲存您的變更。

## 使用命令介面來設定 UM 自動語音應答對應

此範例會啟用上班時間按鍵對應，讓：

  - 當來電者按 1 時，他們會轉接至另一個名為`SalesAutoAttendant`的 UM 自動語音應答。

  - 當他們按下 2 時\] 他們會將轉接至分機號碼 12345 支援。

  - 當他們按下 3 時\] 時就會傳送給另一個自動語音應答播放音訊檔。

<!-- end list -->

    Set-UMAutoAttendant -id MyAutoAttendant -BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

此範例會將逗點分隔值 (.csv) 檔案中所定義的按鍵對應。您必須先建立.csv 檔案與下列標題和正確的項目： \< 金鑰 \> \< 描述 \> \[\< 副檔名 \>\] \[\< 自動語音應答名稱 \>\]、 \[\< promptfilenamepath \>\] \[\< asrphrase1; asrphrase2 \>\]、 \[\< leavevoicemailfor \>\] \[\< transfertomailbox \>\]。括號中的值是選擇性的。建立.csv 檔案之後, 匯入之.csv 檔案使用**Import-csv**指令程式。

    $o = Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    Set-UMAutoAttendant MyAutoAttendant -BusinessHoursKeyMapping $o

本範例會從現有的 UM 自動語音應答的按鍵對應匯出成.csv 檔案，並再將相同的按鍵對應匯入另一個 UM 自動語音應答。您可能也將按鍵對應匯出成.csv 檔案、 編輯或修改.csv 檔案中的關鍵對應以及然後將這些按鍵對應匯入另一個 UM 自動語音應答。

    $aa = Get-UMAutoAttendant -id MyAutoAttendant
    $aa1 = Get-UMAutoAttendant -id MyAutoAttendant2
    $aa.BusinessHoursKeyMapping | Export-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    $aa1.BusinessHoursKeyMapping = (Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv")


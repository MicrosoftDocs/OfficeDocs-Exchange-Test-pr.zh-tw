---
title: '設定撥號代碼: Exchange Online Help'
TOCTitle: 設定撥號代碼
ms:assetid: e5b5efee-b734-4f70-8357-11be07b23bd0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124992(v=EXCHG.150)
ms:contentKeyID: 51409251
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定撥號代碼

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以設定撥號代碼、 電話首碼及用以由整合通訊撥號對應表已啟用 um 之使用者的來電及撥出電話號碼格式。在大多數情況下，您將與撥號代碼、 首碼及電話語音網路上目前設定的數字格式設定撥號對應表。

撥號代碼和電話首碼可用來決定正確的號碼來撥打已啟用 UM 之使用者所撥出電話的撥號對應表。*Outdialing*是用來描述的 UM 撥號對應表中的使用者起始撥出電話的程序的字詞。數字格式用於在國家或地區、 國際電話或雙引號括撥號對應表的電話的來電。您可以設定撥號對應表來比對國家/地區及國際號碼的傳入呼叫號碼格式。當您設定的國家/地區及國際號碼格式時，您可以限制使用者撥號對應表與連結的來電。

如需與撥出相關的其他管理工作，請參閱[讓使用者能夠進行的通話程序](allowing-users-to-make-calls-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。 如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

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

## 使用 EAV 來設定撥號代碼、首碼及號碼格式

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  選取您要管理的 UM 撥號對應表，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\]頁面上，按一下 \[設定\]。

4.  在 **\[UM 撥號對應表\]** 頁面 \> **\[撥號代碼\]** 上，設定下列選項：
    
      - **外線存取碼**
    
      - **國際存取碼**
    
      - **國際電話首碼**
    
      - **國家/地區碼**

5.  在 **\[在撥號對應表之間撥號的號碼格式\]** 下方，設定下列項目：
    
      - **國家/地區號碼格式**
    
      - **國際電話號碼格式**
    
      - **相同撥號對應表內來電的號碼格式**   若要新增號碼格式，請按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

6.  按一下 **\[儲存\]** 以儲存變更。

## 使用命令介面來設定撥號代碼、首碼及號碼格式

本範例使用國內或地區號碼格式、國際號碼格式及下列撥號代碼，來設定名為 `MyUMDialPlan` 的 UM 撥號對應表：

  - 9 是外線存取碼

  - 011 是國際存取碼

  - 1 是國際電話首碼

  - 1 是國碼或地區碼

<!-- end list -->

    Set-UMDialPlan -Identity MyUMDialPlan -OutsideLineAccessCode 9 -InternationalAccessCode 011 -NationalNumberPrefix 1 CountryorRegionCode 1 -InCountryOrRegionNumberFormat 1425xxxxxxx -InternationalNumberFormat 441425xxxxxxx


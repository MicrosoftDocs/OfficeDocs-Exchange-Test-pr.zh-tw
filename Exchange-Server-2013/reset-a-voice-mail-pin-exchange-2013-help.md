---
title: '重設語音信箱 pin 碼: Exchange Online Help'
TOCTitle: 重設語音信箱 pin 碼
ms:assetid: bf07e6e7-01d2-4933-bff5-c615cc21a480
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124404(v=EXCHG.150)
ms:contentKeyID: 50554090
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.ResetUnifiedMessagingPinPropertyControl
ms.translationtype: MT
---

# 重設語音信箱 pin 碼

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

不在他們的信箱使用 Outlook 語音存取，因為他們嘗試使用不正確的 pin 碼多次登入或他們忘記其 PIN 鎖定已啟用整合通訊 UM 語音郵件使用者時您可以使用下列程序之一來重設使用者的 pin 碼。當重設使用者的Outlook語音存取 PIN 時，您可以設定 UM 以自動產生 PIN 或您可以手動指定的 pin 碼。新的 PIN 傳送給使用者的電子郵件。您可以指定其他 PIN 選項，例如需要使用者在第一次登入時重設其 pin 碼。使用者也可以重設使用Outlook或Outlook Web App其 UM PIN。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要存取已啟用 UM 的信箱，Outlook 語音存取使用者需要使用按鍵式、 也稱為複頻式訊號 (DTMF) 的輸入。語音辨識不適用於 PIN 輸入。</td>
</tr>
</tbody>
</table>


如需與 Outlook 語音存取 PIN 碼相關的其他工作，請參閱 [PIN 安全性程序](pin-security-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

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

## 使用 EAC 重設整合通訊 PIN 碼

1.  在 EAC 中，瀏覽至 \[**收件者**。在清單檢視中，選取您要檢視的使用者信箱。

2.  在詳細資料窗格的 \[電話和語音功能\] 下，按一下 \[整合通訊\] 下的 \[檢視詳細資料\]。

3.  在 \[UM 信箱\] 頁面上，按一下 \[UM 信箱設定\] 下的 \[重設 PIN 碼\]。

4.  在 \[重設 UM 信箱 PIN 碼\] 頁面上，使用下列選項來重設啟用 UM 之使用者的 PIN 碼：
    
      - **自動產生的 PIN**  使用此選項會自動產生之使用者所使用來存取使用Outlook語音存取其信箱的 pin 碼。根據預設，會啟用此設定。
        
        會以電子郵件至使用者的信箱傳送自動產生的 PIN。他們收到 PIN 和登入信箱之後，他們將提示您變更這些更熟悉的 PIN PIN。
        
        Outlook Web App與 Microsoft Outlook 也可讓使用者重設其 pin 碼。PIN 會自動產生根據使用者的信箱與關聯的 UM 信箱原則所設定的 PIN 原則。我們建議您自動產生的Outlook語音存取使用者的 Pin。
    
      - **類型 PIN**  使用此選項以手動方式指定Outlook語音存取使用者的 PIN。預設會停用此設定。
        
        如果您指定使用者的 PIN，PIN 會傳送電子郵件至使用者的信箱中。他們收到 PIN 和登入信箱之後，他們可以變更 PIN Outlook語音存取中設定個人選項。不過，在Outlook Web App \] 和 \[Microsoft Outlook 中，沒有選項可以手動指定的 pin 碼。
    
      - **需要使用者在重設其 PIN 第一次登入**  若要要求使用者在其第一次登入 Outlook 語音存取時重設其 PIN 使用此選項。根據預設，會啟用此選項。
        
        如果您選取 \[自動產生使用者的 PIN\] 選項，您可以啟用此選項可要求使用者在第一次登入Outlook語音存取時變更其 pin 碼。這有助於保護使用者的 PIN。

5.  按一下 \[儲存\]。

## 使用命令介面重設整合通訊 PIN 碼

此範例會為 Tony Smith 將語音信箱 PIN 碼重設為 1985848。但是，當使用者第一次登入 Outlook 語音存取時，必須變更此 PIN 碼。

    Set-UMMailboxPIN -Identity tonysmith@contoso.com -PIN 1985848 -PinExpired $true


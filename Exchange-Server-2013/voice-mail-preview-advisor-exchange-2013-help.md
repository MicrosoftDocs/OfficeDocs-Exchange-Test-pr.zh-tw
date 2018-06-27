---
title: '語音郵件預覽顧問: Exchange Online Help'
TOCTitle: 語音郵件預覽顧問
ms:assetid: 0957dd54-df6d-4b50-9db5-4757f548b899
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee364730(v=EXCHG.150)
ms:contentKeyID: 51409152
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 語音郵件預覽顧問

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

MicrosoftExchange 整合通訊 (UM) 包含呼叫語音郵件預覽使用自動語音辨識 (ASR) 將語音郵件音訊檔的文字版本新增到語音郵件訊息的功能。ASR 不是完全精確，尤其是當它是透過電話含有未知的聲音及雜音用於錄製音訊時。有些組織需要可持續無錯誤的 （或附近-無錯誤的） 的語音訊息的文字記錄。語音郵件預覽協力廠商程式可協助這類組織符合這些需求。

語音郵件預覽使用[Microsoft 語音技術](http://go.microsoft.com/fwlink/p/?linkid=187348)提供音訊錄製的文字版本。語音郵件文字會顯示在MicrosoftOutlook Web App、 Outlook 2010或更新版本、 及其他電子郵件程式內的電子郵件訊息。

根據預設，當您啟用 UM 的使用者在內部部署或混合式部署語音郵件預覽就會傳送若已安裝支援的 UM 語言套件。當您啟用 um 的使用者Exchange Online中時，會安裝所有的 UM 語言套件。不過，語音郵件預覽不支援在已安裝的所有語言。

有提供增強的記錄支援和服務的語音郵件預覽功能的語音郵件預覽協力廠商。這些協力廠商採用更正語音郵件 transcriptions 使用 ASR 所建立的人員。每個語音郵件預覽協力廠商必須符合一組認證來與 Exchange UM 交互操作硬體需求。

如果您決定語音郵件預覽傳送給您的使用者不正確足夠、 您可以連絡第一列在[Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=281966)並簽署向上與其在其他成本認證語音郵件預覽夥伴。

**目錄**

概觀

Exchange Unified Messaging Voice Mail Partner program

Voice Mail Preview partners certified for Exchange Unified Messaging

Configuring Voice Mail Preview partners

VoIP or media gateways and IP PBX support

## 概觀

當整合通訊記錄的語音訊息的音訊時，它使用 ASR 的音訊檔案，從建立語音郵件預覽文字，然後送出整個語音郵件進行傳遞給使用者。建立每個語音訊息、 整合通訊會決定訊息所含的語音郵件預覽信賴的等級。它會測量完善音效錄製中的符合文字、 數字及郵件中的片語。如果系統輕鬆找到相符項目，都會高信賴等級。更高的信賴等級聯通常較高的精確度。

語音郵件預覽文字的正確性取決於許多因素及有時無法控制這些因素。不過，文字是可能是更精確的時機：

  - 留下的語音訊息較為簡單，且來電者並未使用俚語、技術性的行話或不常用的字詞。

  - 來電者使用的語言，輕鬆辨識及轉譯由語音郵件系統。一般而言，語音訊息 left 的來電者不太快速或太小說話和沒有強式重音將會產生更精確的句子和片語。

  - 語音訊息沒有背景雜音和回音，而且音訊沒有不連貫。

使用 Unified Messaging 的大部分客戶尋找語音信箱預覽是正確的使用者。不過，錄製透過電話進行未知的聲音及背景雜音套用 ASR、 時語音郵件預覽文字通常不是完全正確。如果可持續低信賴的層級或接收語音郵件預覽未很精確，可能會增加的精確度語音郵件預覽的使用者會收到如下：

  - 註冊語音信箱預覽協力程式中的語音轉譯服務。

  - 您已註冊與語音郵件預覽協力廠商之後，設定協力廠商為與 UM 搭配使用。如需如何設定 UM 語音郵件預覽協力廠商的詳細資訊，請參閱[設定使用者的語音郵件預覽合作夥伴服務](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md)。

當您註冊與語音郵件預覽的合作夥伴間時，貴組織中的 Exchange 伺服器語音將郵件重新導向與附加到語音郵件預覽協力廠商語音訊息的產生語音郵件預覽文字和送出至使用者信箱的語音訊息的音訊檔案。語音郵件預覽協力廠商所產生的語音郵件預覽文字的電子郵件然後送出至以傳遞給收件者的信箱在組織中的 Exchange 伺服器。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建議您打算部署整合通訊的所有客戶都取得協助的 UM 專家。UM 專員可協助您確保已順利地轉換到 UM 從舊版的語音信箱系統。執行新部署或升級舊版的語音郵件系統要求 VoIP 閘道、 IP Pbx、 Pbx、 工作階段邊界控制器 (Sbc) 相關的重要知識和整合通訊。如需如何連絡 UM 專家的詳細資訊，請參閱<a href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 整合通訊 (UM) 專家</a>或<a href="https://go.microsoft.com/fwlink/p/?linkid=261951">整合通訊的 Microsoft Pinpoint</a>。</td>
</tr>
</tbody>
</table>


回到頁首

## Exchange 整合通訊語音信箱合作夥伴方案

若要成為認證成為相互溝通與 Exchange UM 語音郵件預覽協力廠商、 合作夥伴必須實作語音郵件預覽交互操作性規格中所包含的需求與協力廠商解決方案必須獨立的憑證廠商微軟認證。如果您感興趣認證來使用 Exchange UM 您記錄服務、 送出要求[的 Exchange 整合通訊語音郵件預覽合作夥伴](mailto:vmppp@microsoft.com)。

## 已通過 Exchange 整合通訊認證的語音信箱預覽合作夥伴

如果您已將部署整合通訊您組織中與您在這裡尋找認證的語音郵件預覽協力廠商提供記錄支援服務，請參閱[Microsoft PinPoint](https://go.microsoft.com/fwlink/p/?linkid=281966)。這些軟體廠商經過為互通與 Exchange UM。

## 設定語音信箱預覽合作夥伴

已設定 UM 之後，它會將音訊的語音郵件轉寄給專屬的語音郵件預覽協力廠商，然後取得音訊檔並建立的語音郵件預覽文字中。不過，若要允許使用者接收其語音郵件語音郵件預覽在他們的信箱，必須設定 UM 信箱原則、 使用者關聯的 UM 信箱原則，然後有使用者確認他們可以在Outlook 2010或更新版本或是Outlook Web App其語音郵件中接收語音郵件預覽。如需如何設定 UM 語音郵件預覽協力廠商的詳細資訊，請參閱[設定使用者的語音郵件預覽合作夥伴服務](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md)。

## VoIP 或媒體閘道和 IP PBX 支援

您的組織設定 VoIP 閘道器、 IP Pbx 是必須以成功部署整合通訊語音郵件預覽合作夥伴正確完成很難部署工作。可協助您設定 VoIP 閘道器、 IP Pbx 的資訊及設定方式的相關的最新資訊，請參閱[Exchange 2013 的電話語音 advisor](telephony-advisor-for-exchange-2013-exchange-2013-help.md)或[支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)。

測試的互通性的 Exchange UM 與 VoIP 閘道已與Microsoft Unified Communications 開啟互通性計劃整合。如需詳細資訊，請參閱[Microsoft Unified Communications 開啟互通性計劃](https://go.microsoft.com/fwlink/p/?linkid=132071)。

回到頁首


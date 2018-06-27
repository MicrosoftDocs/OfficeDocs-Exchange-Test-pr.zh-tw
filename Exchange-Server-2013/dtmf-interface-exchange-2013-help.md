---
title: 'DTMF 介面: Exchange Online Help'
TOCTitle: DTMF 介面
ms:assetid: 2c7c9d8a-ed12-4dcf-a5b7-3cea0e785e49
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996919(v=EXCHG.150)
ms:contentKeyID: 54652553
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DTMF 介面

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

在整合通訊 (UM) 中，來電者可以使用雙音多頻 (DTMF，也稱為按鍵) 和語音輸入來與系統進行互動。來電者可以使用的方法是根據 UM 撥號對應表及自動語音應答的設定方式而定。

DTMF 介面讓來電者在撥打撥號對應表上設定的 Outlook 語音存取號碼，或是撥打自動語音應答上設定的電話號碼時，可以使用電話鍵台尋找使用者，以及瀏覽 UM 功能表系統。本主題討論 DTMF 介面，以及來電者如何使用它來尋找使用者，並瀏覽 UM 語音信箱功能表系統。

**目錄**

DTMF overview

UM dial plans and dial by name

DTMF maps

DTMF maps for users who aren't enabled for Unified Messaging

DTMF maps for users who are enabled for Unified Messaging

For more information

## DTMF 概觀

DTMF 需要來電者在電話鍵台上，按下對應到整合通訊功能表選項的按鍵，或是使用按鍵上的字母拼出名稱或別名，以輸入使用者的名稱或電子郵件別名。來電者使用 DTMF 的原因可能是因為尚未啟用自動語音辨識 (ASR)，或是因為他們嘗試使用語音命令卻失敗。不論如何，都會使用 DTMF 輸入來瀏覽功能表以及搜尋使用者。

根據預設，在 UM 中，DTMF 輸入會在撥號對應表上使用，而且會是 UM 自動語音應答的預設來電者介面。

來電者可以針對下列用途使用 DTMF 輸入：

  - 使用 Outlook 語音存取的撥號對應表撥入存取。

  - 撥號對應表目錄查閱及搜尋，以尋找使用者。

  - 未啟用語音的自動語音應答。

  - 自動語音應答已啟用語音功能，但不一定已設定 DTMF 後援自動語音應答。

  - DTMF 後援自動語音應答 (未啟用語音)。

## UM 撥號對應表及依名稱撥號

當您建立 UM 撥號對應表時，可以設定主要和次要的輸入方法，讓來電者在搜尋使用者或是想要與使用者連絡時，可以用來查閱名稱。這些設定位於撥號對應表的 **\[設定\]** 頁面，稱為 **\[搜尋名稱的主要方法\]** 以及 **\[搜尋名稱的次要方法\]**。搜尋名稱的主要和次要方法都能使用下列選項：

  - 姓氏 名字

  - 名字 姓氏

  - SMTP 位址

此外，搜尋名稱的次要方法還能使用 **\[無\]** 選項。

預設會選取 **\[名字 姓氏\]** 作為搜尋名稱的主要方法，**\[SMTP 位址\]** 則選為搜尋名稱的次要方法。因此，當來電者撥入 UM 撥號對應表上設定的 Outlook 語音存取號碼時，會播放撥號對應表的歡迎訊息，總機會說出例如：「歡迎使用 Contoso Outlook 語音存取」。如要存取信箱，請輸入分機。如欲聯絡某人，請按井字鍵。」當來電者按井字鍵後，系統會回應「請拼出您要呼叫之人員的姓名，從姓氏開始。或是，若要拼寫人員的電子郵件別名，請按兩次井字鍵。」在此案例中，根據您撥號對應表的設定方式而定，系統會接著提示來電者先輸入使用者的姓氏，再輸入使用者的名字 (姓氏 名字)，或拼出他們的電子郵件別名 (不包含網域名稱)。例如，如果使用者電子郵件別名是 tsmith@contoso.com，則來電者要輸入 tsmith。

如果您因為預設設定不符需要而想變更此設定，可以將它變更為讓來電者先輸入使用者電子郵件別名，或是輸入使用者的名字，再輸入姓氏。在此案例中，您會將 **\[搜尋名稱的主要方法\]** 設定為 **\[SMTP 位址\]**，並將 **\[搜尋名稱的次要方法\]** 設定為 **\[姓氏 名字\]**。依名稱撥號方法的設定也會套用到與撥號對應表關聯的任何 UM 自動語音應答。來電者若要能夠使用 DTMF 輸入或電話鍵台上的按鍵來輸入使用者的名稱，則您組織的目錄內必須要有該使用者的 DTMF 對應和值存在。

如需如何變更 UM 撥號對應表上的依主要名稱撥號方法和依次要名稱撥號方法的詳細資訊，請參閱[設定 Outlook 語音存取使用者要搜尋的主要方法](configure-the-primary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md)及[設定 Outlook 語音存取使用者要搜尋的次要方法](configure-the-secondary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md)。

回到頁首

## DTMF 對應

在 Exchange 組織中，名稱為 **msExchUMDtmfMap** 的屬性會與目錄中建立的每個使用者關聯。整合通訊會使用這個屬性，將使用者的名字、姓氏和電子郵件別名對應到一組號碼。此對應稱為 DTMF 對應。DTMF 對應讓來電者能在電話鍵台上，輸入對應至使用者名稱或電子郵件別名的字母。這個屬性包含了針對使用者的名字加姓氏、姓氏加名字，以及電子郵件別名，建立 DTMF 對應時所需的值。

下表顯示針對名為 Tony Smith 且已啟用 UM 功能的使用者 (其別名為 tsmith@contoso.com)，將儲存在 Active Directory 的 **msExchUMDtmfMap** 屬性中的 DTMF 對應值。

**為名為 Tony Smith 且已啟用 UM 功能的使用者，儲存 DTMF 值**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>目錄項目</th>
<th>使用者名稱</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>firstNameLastName:866976484</p></li>
</ul></td>
<td><p>tonysmith</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>lastNameFirstName:764848669</p></li>
</ul></td>
<td><p>smithtony</p></td>
</tr>
<tr class="odd">
<td><ul>
<li><p>emailAddress:876484</p></li>
</ul></td>
<td><p>tsmith</p></td>
</tr>
</tbody>
</table>


名稱和電子郵件別名可能會包含其他非英數字元，例如逗號、連字號、底線或句點。此類字元不會用於使用者的 DTMF 對應中。例如，如果 Tony Smith 的電子郵件別名是 tony-smith@contoso.com，則 DTMF 對應值將是 866976484，且不會包含連字號。不過，如果使用者的電子郵件別名包含數字，例如 tonysmith123@contoso.com，則數字會用於建立的 DTMF 對應中。tonysmith123 的 DTMF 對應將會是 866976484123。

必須要有使用者的 DTMF 對應存在，來電者才能輸入使用者的名稱或電子郵件別名。不過，並非所有使用者都會具有與其使用者帳戶關聯的 DTMF 對應。

回到頁首

## 未啟用整合通訊之使用者的 DTMF 對應

根據預設，使用者 (包括擁有信箱功能的使用者) 不會啟用整合通訊。**msExchUMDtmfMap** 屬性會為尚未啟用 UM 的使用者，填入 DTMF 對應所需要的值。依預設，建立使用者的信箱時會為所有使用者建立下列 DTMF 對應：

1.  emailAddress

2.  firstNameLastName

3.  lastNameFirstName

如果使用者的帳戶沒有定義 DTMF 對應值，來電者在從 UM 自動語音應答功能表按電話按鍵或執行目錄搜尋時，將無法連絡使用者。此外，已啟用 UM 的使用者也將無法傳送訊息或轉接來電給沒有 DTMF 對應的使用者，除非他們可以使用自動語音辨識 (ASR)。若要讓來電者能夠轉接來電或使用電話鍵台來連絡未啟用 UM 的使用者，您需要為那些使用者建立 DTMF 對應的必要值。您可以搭配使用 **Set-User** 指令程式與 *-CreateDtmfMap* 參數，來建立及更新單一使用者的 DTMF 對應，或者如果使用者名稱已在建立 DTMF 對應之後變更，則更新使用者的 DTMF 對應。您可以選擇使用這個指令程式建立 Exchange 管理命令介面指令碼，以更新多位使用者的 DTMF 對應值。

如需 **Set-User** 指令程式的相關資訊，請參閱 [Set-User](https://technet.microsoft.com/zh-tw/library/aa998221\(v=exchg.150\))。

回到頁首

## 已啟用整合通訊之使用者的 DTMF 對應

根據預設，當為使用者啟用整合通訊時，會為他們建立 DTMF 對應。如此可讓來自外部來電者、未啟用 UM 的使用者，以及其他使用電話鍵台拼出使用者名稱或電子郵件別名且已啟用 UM 的使用者等的來電，都能夠轉接給已啟用 UM 的使用者。

為已啟用 UM 的使用者建立 DTMF 對應值後，來電者便可以使用目錄搜尋功能。來電者在使用電話鍵台時，會在下列情況下使用目錄搜尋：

  - 在他們撥入 Outlook 語音存取號碼時識別或搜尋使用者。

  - 在他們撥入 UM 自動語音應答時，尋找或轉接來電給已啟用 UM 的使用者。

如需如何為使用者啟用整合通訊的相關資訊，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

有時使用者的名字、姓氏或電子郵件別名，會在使用者已啟用 UM 之後變更。使用者的 DTMF 對應值將不會自動更新。如果來電者輸入了使用者的新名字或電子郵件別名，且使用者的 DTMF 對應並未更新以反映名字或電子郵件別名的變更，則來電者將無法在目錄中尋找使用者、寄送訊息給使用者，或是將來電轉接到該使用者。如果您必須在使用者已啟用 UM 後更新其 DTMF 對應，可以搭配使用 **Set-User** 指令程式與 *-CreateDtmfMap* 參數。您也可以使用這個指令程式建立 Exchange 管理命令介面指令碼，以更新多位已啟用 UM 之使用者的 DTMF 對應。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建議您不要使用 ADSI Edit 之類的工具手動變更使用者的 DTMF 值，因為可能會導致設定不一致或是其他的錯誤。建議您只用 <strong>Set-UMService</strong> 指令程式或 <strong>Set-User</strong> 指令程式來為使用者建立或更新 DTMF 對應。</td>
</tr>
</tbody>
</table>


## 相關資訊

[Adsiedit 概觀 （英文)](https://go.microsoft.com/fwlink/p/?linkid=73175)


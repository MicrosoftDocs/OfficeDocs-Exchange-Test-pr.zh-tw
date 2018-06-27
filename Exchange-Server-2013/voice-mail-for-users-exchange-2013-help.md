---
title: '使用者的語音信箱: Exchange Online Help'
TOCTitle: 使用者的語音信箱
ms:assetid: 48e1f43b-fb7e-4a52-a2cb-0fb5da6ca65f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997885(v=EXCHG.150)
ms:contentKeyID: 50473057
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用者的語音信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-19_

使用整合通訊 (UM)、 Exchange 組織中的使用者可以接收所有其電子郵件和語音訊息中一個信箱。整合通訊功能和語音信箱功能增加使用者產能及啟用整個組織中更靈活訊息。

當您新增使用者至您的組織時，您要授與建立信箱或連線至現有的信箱使用者的選項。使用者建立信箱或使用者連線至現有的信箱之後，您可以啟用信箱整合通訊，以便使用者可以使用的語音郵件系統及其隨附的語音信箱功能。之後使用者啟用整合通訊，所有的電子郵件、 語音信箱和傳真訊息將會傳遞至使用者的信箱。使用 Microsoft Office Outlook 2007或更新版本、 Outlook Web App、 啟用 Microsoft ExchangeActiveSync或一般的行動電話或行動電話，使用者可以存取其電子郵件、 語音訊息、 個人連絡人和行事曆資訊。

**目錄**

語音信箱使用者屬性

語音信箱使用者和其他 UM 元件之間的關係

Extension numbers and SIP addresses

Using the EAC to enable a user for UM and voice mail

Using the Shell to enable a user for UM and voice mail

Disabling UM for a user

## 語音信箱使用者屬性

使用者必須具有信箱他們可以啟用整合通訊之前。但是，根據預設，具有信箱的使用者未啟用整合通訊。使用者已啟用 UM 的之後，您可以管理、 修改和設定 UM 內容及為他們的語音信箱功能。您可以啟用使用者的整合通訊使用 EAC 或命令介面。如需詳細資訊，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。若要讓多個 UM 使用者，請使用 EAC 或**Enable-UMMailbox**指令程式Exchange管理命令介面中。

## 語音信箱使用者和其他 UM 元件之間的關係

當您啟用使用者的整合通訊時，使用者必須具有相關聯或連結至現有的 UM 信箱原則，並您必須為他們提供的分機號碼。您可以使用**Enable-UMMailbox**指令程式在命令介面或由使用者啟用整合通訊時選取的 UM 信箱原則關聯的 UM 信箱原則使用者。根據預設，當您建立 UM 撥號對應表，會建立新的 UM 信箱原則。要修改此原則或另一個原則可建立及連結至撥號對應表來決定哪些功能或設定會套用至使用者或使用者群組。

UM 信箱原則包含如撥號限制及使用者的 PIN 原則的設定。建立 UM 信箱原則之後，必須與只有一個 UM 撥號對應表相關聯。任何 Exchange 伺服器可以接聽來電並提供語音信箱服務給連結任何已啟用 UM 的使用者與 UM 撥號對應表。使用者已啟用整合通訊之後，在 UM 信箱原則的設定會套用至已啟用 UM 的使用者。

## 分機號碼和 SIP 位址

當您啟用使用者的整合通訊時，您必須定義至少一個分機號碼整合通訊用以送出的語音信箱時將使用者的信箱。使用者啟用整合通訊之後，您可以將次要分機號碼新增至使用者的信箱或修改或移除這些使用者的信箱上設定Exchange整合通訊 proxy 位址 （EUM proxy 位址） 或新增或移除使用者的其他或次要延伸模組在 EAC 中。您也可以移除 EUM proxy 位址，在 EAC 中移除的主要的分機號碼，但是建議您不要移除。移除的主要的分機號碼不會允許正確轉接至使用者信箱的通話。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>可為已啟用 UM 的使用者新增的次要分機號碼數量沒有限制，但是一個使用者只可以有一個主要分機號碼。</td>
</tr>
</tbody>
</table>


已啟用 UM 之使用者的信箱可以與一個 UM 撥號對應表相關聯。已啟用 UM 的使用者可以指派下列：

  - 單一撥號對應表上的單一主要分機號碼、工作階段初始通訊協定 (SIP) 位址或 E.164 位址。

  - 單一撥號對應表上的多個次要分機號碼、SIP 位址或 E.164 位址。

  - 兩個不同撥號對應表上的多個主要分機號碼、SIP 位址或 E.164 位址。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每個分機號碼、SIP 地址以及 E.164 號碼在撥號對應表內需為唯一，且撥號對應表內的號碼位數將用於所有與撥號對應表連結的使用者。</td>
</tr>
</tbody>
</table>


例如，已啟用 UM 之使用者經常從傳送紐約到東京。使用者的信箱相關聯紐約撥號對應表及使用者的信箱上設定單一的分機號碼。第二個的分機號碼被設定在使用者的信箱的東京撥號對應表。當來電者可以是分機號碼的撥號對應表和留下語音訊息給使用者時、 語音訊息會傳送到相同的已啟用 UM 的信箱。

回到頁首

## 使用 EAC 來啟用使用者 UM 與語音信箱

建立使用者的 Exchange 信箱之後，您可以使用 EAC 中**檢視詳細資料\]**下**整合通訊**設定 UM 信箱設定。當您啟用使用者時，有數個您要設定的設定：

1.  **SIP 位址**  這是使用者的 SIP 位址。如果您正在啟用 UM 之使用者指派給 UM 信箱原則連結至 SIP URI 撥號對應表會看到此設定。當您正在整合 Office Communications Server 2007 R2 或 Microsoft Lync Server 使用的 SIP URI 撥號對應表。當您將使用者指派給 UM 信箱原則連結至 SIP URI 或撥號對應表 E.164 時，則您仍也必須為使用者輸入分機號碼。主要的分機號碼會在使用者用以存取 Outlook 語音存取。

2.  \[分機號碼\]   您應該手動輸入您正在啟用 UM 的使用者分機號碼。
    
    您必須為使用者提供有效的分機號碼且符合撥號對應表上指定的數字數目。您只可以輸入數字字元或數字從 1 到 20。典型的分機號碼 3 到 7 位數字長，且設定在撥號對應表與 UM 信箱原則是連結和指派給使用者。

3.  **使用者的 PIN 設定：**
    
      - **自動產生的 PIN**  此設定會自動產生用於透過 Outlook 語音存取語音信箱存取已啟用 UM 之使用者的 PIN。這是預設設定。當您按一下此按鈕時，PIN 會自動產生 PIN 原則指派給使用者的 UM 信箱原則上設定為基礎。我們建議您使用此設定可協助保護使用者的 PIN。PIN 傳送給他們收到之後他們正在啟用 UM 的歡迎訊息中的使用者。根據預設，他們必須先登入他們的信箱若要取得其語音信箱時變更此 PIN。
    
      - \[輸入 PIN 碼\]   此設定將讓您手動指定讓使用者使用的 PIN 碼，以存取語音信箱系統。
        
        PIN 必須符合在已啟用 UM 的使用者相關聯的 UM 信箱原則上設定 PIN 原則設定。例如，如果 UM 信箱原則設定為接受包含七個或多個字的 Pin，您在此方塊中輸入的 pin 碼必須至少七位數字的 long。
    
      - **需要使用者在重設其 PIN 第一次登入**  此設定會強制使用者從第一次使用 Outlook 語音存取電話存取語音信箱系統時重設其語音信箱 pin 碼。將提示時輸入更熟悉給他們的 PIN。它會強制已啟用 UM 的使用者在第一次登入時以協助防止未經授權存取其資料與收件匣變更其 PIN 安全性的最佳作法。預設會選取此核取方塊。

## 使用命令介面來啟用使用者 UM 與語音信箱

本範例在 tonysmith@contoso.com 的信箱上啟用整合通訊與語音信箱，並手動設定使用者的分機與 PIN，然後將名為 `MyUMMailboxPolicy` 的 UM 信箱原則指派給使用者的信箱。

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -PINExpired $true

本範例在 tonysmith@contoso.com 的信箱上啟用整合通訊與語音信箱，並指派名為 `MyUMMailboxPolicy` 的 UM 信箱原則指派給使用者的信箱。

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -SIPResourceIdentifier "tonysmith@contoso.com" -PINExpired $true

## 停用使用者的 UM

當您停用整合通訊的使用者時，當來電者會執行目錄搜尋使用 UM 自動語音應答功能表或使用Outlook語音存取可能仍會列出使用者帳戶。來電者可以找到使用者在目錄中，但是當嘗試連絡使用者，他們正在採取回至整合通訊中的主功能表。這可能會造成來電者也變得與系統。您可以防止來電者使用目錄搜尋來連絡已停用整合通訊的連接至另一個語音郵件系統的使用者、 將使用者從 UM 自動語音應答的目錄搜尋、 移除或移除的使用者帳戶的使用者。

已啟用 UM 的使用者帳戶已停用整合通訊之後，使用者可能仍有存取使用Outlook Voice Access 或 Microsoft Outlook個別啟用 UM 的信箱。這可能發生時不一致的目錄中的所有修訂。若要減少使用者即使帳戶已停用整合通訊取得信箱的存取權的風險，您可以手動強制複寫發生或從使用者的信箱移除使用者已停用整合通訊的所有整合通訊的資訊。


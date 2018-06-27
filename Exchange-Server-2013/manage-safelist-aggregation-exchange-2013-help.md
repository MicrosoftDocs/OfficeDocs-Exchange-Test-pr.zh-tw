---
title: '管理安全清單彙總: Exchange 2013 Help'
TOCTitle: 管理安全清單彙總
ms:assetid: 5ac17168-f411-4cb7-ae98-ebefb865b210
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998280(v=EXCHG.150)
ms:contentKeyID: 50473247
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理安全清單彙總

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

*「安全清單彙總」* 是指 Microsoft Outlook 與 Microsoft Exchange Server 2013 皆共有的反垃圾郵件功能。此功能蒐集來自安全的收件者清單、安全的寄件者清單、封鎖的寄件者清單、以及 Outlook 使用者設定的聯絡人資料，且讓此資料可為 Exchange 反垃圾郵件代理程式所用。安全清單彙總可以協助減少執行反垃圾郵件代理程式的 Exchange 伺服器所執行之反垃圾郵件篩選中的誤判執行個體。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md) 主題中的「收件者佈建權限」章節以及 [反垃圾郵件和反惡意程式的權限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) 主題中的「反垃圾郵件功能」章節。

  - 您只能使用命令介面來執行此程序。

  - 預設在 Mailbox Server 的 Transport 服務中未啟用反垃圾郵件功能。通常只有在您的 Exchange 組織接受內送郵件之前未進行任何事前的反垃圾郵件篩選的情況下，您才會在 Mailbox Server 上啟用反垃圾郵件功能。如需詳細資訊，請參閱[啟用信箱伺服器上的反垃圾郵件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - 請注意執行 **Update-SafeList** 指令程式時可能產生的網路和複寫流量。對頻繁使用安全清單的多個信箱執行此命令，可能會產生大量的流量。建議您若要對多個信箱執行此命令，應該在離峰、非上班時間執行命令。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用命令介面來設定信箱安全清單集合限制

可設定一個使用者可設定的最大安全寄件者與封鎖的寄件者數量。根據預設，使用者可以設定最多 5,000 個安全寄件者和 500 個封鎖的寄件者。

若要設定最大安全寄件者與封鎖的寄件者數量，請執行下列命令：

    Set-Mailbox <MailboxIdentity> -MaxSafeSenders <Integer> -MaxBlockedSenders <Integer>

此範例會將信箱 john@contoso.com 的安全寄件者上限設為 2,000，而封鎖的寄件者上限設為 200。

    Set-Mailbox john@contoso.com -MaxSafeSenders 2000 -MaxBlockedSenders 200

## 如何知道這是否正常運作？

若要驗證您是否已成功設定信箱安全清單限制，請執行下列命令：

1.  執行下列命令：
    
        Get-Mailbox <Identity> | Format-List Name,Max*Senders

2.  請確認顯示的值符合您所設定的值。

## 使用命令介面執行 Update-Safelist 命令

在 Exchange 2013 中，安全清單彙總將自動完成，所以您無需排定或手動執行 **Update-Safelist** 指令程式。但是，您有時可能想要執行此指令程式來測試安全清單彙總。

此範例會為信箱 john@contoso.com 編寫至 Active Directory 的安全寄件者清單。

    Update-Safelist john@contoso.com -Type SafeSenders

如需詳細的語法及參數資訊，請參閱 [Update-SafeList](https://technet.microsoft.com/zh-tw/library/bb125034\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要驗證您是否已成功設定安全清單彙總，請執行以下步驟：

## 步驟 1：使用命令介面來驗證篩選器代理程式是否於 Exchange 伺服器中啟用

1.  執行下列命令：
    
        Get-ContentFilterConfig | Format-List Enabled

2.  如果輸出顯示 *Enabled* 參數為 `True`，則表示已啟用內容篩選。若沒有，請執行以下命令來啟用 Exchange 伺服器上的內容篩選以及內容篩選代理程式：
    
        Set-ContentFilterConfig -Enabled $true

## 步驟 2：(選用) 使用 ADSI Edit 來驗證安全清單彙總資料是否複寫至 Edge Transport Server

此步驟僅在您於周邊網路的 Edge Transport Server 上執行內容篩選器代理程式時需要。

您可於 Edge Transport Server 上的 Active Lightweight Directory Services (AD LDS) 執行個體中檢視使用者物件，以驗證安全清單集合資料已為此用者物件更新，且 Microsoft Exchange EdgeSync 服務已複寫至 AD LDS 執行個體。

每個使用者物件有三個安全清單集合屬性：

  - **msExchSafeRecipientsHash**  此屬性儲存使用者之安全收件者清單集合的雜湊。

  - **msExchSafeSendersHash**  此屬性儲存使用者之安全寄件者清單集合的雜湊。

  - **msExchBlockedSendersHash**  此屬性儲存使用者之封鎖的寄件者清單集合的雜湊。

如果屬性上有十六進位字串 (如 `0xac 0xbd 0x03 0xca`)，即已更新使用者物件。如果屬性的值為 `<Not Set>`，表示未更新屬性。

您可以使用 AD LDS Active Directory 服務介面 (ADSI) 編輯嵌入式管理單元來搜尋及檢視屬性。

## 步驟 3：傳送測試郵件以驗證安全清單彙總是否正確運作

若要測試安全清單彙總功能是否正常，需自安全的寄件者傳送一封郵件給自己，否則會遭到內容篩選封鎖。如果安全清單彙總正在運作中，郵件應該會送達您的收件匣。

1.  尋找可用的現有外部電子郵件帳號或於免費的網路電子郵件供應商（如 Microsoft Hotmail）建立新的電子郵件帳號。

2.  將該帳號新增至 Microsoft Outlook 中。

3.  使用 **Update-SafeList** 指令程式將安全清單集合自該信箱複製至 Active Directory。

4.  選用：若您正在執行周邊網路中的 Edge Transport Server 內容篩選代理程式，請執行 **Start-EdgeSynchronization** 指令程式來強制 EdgeSync 複寫。

5.  在您的內容篩選組態中新增特定單字做為封鎖片語。如需詳細步驟，請參閱[管理內容篩選](manage-content-filtering-exchange-2013-help.md)。

6.  從步驟 1 的外部電子郵件帳號傳送一封郵件至您的 Exchange 信箱，其中需包含您在步驟 5 中設定的封鎖詞語。
    
    若郵件成功傳遞至您的收件匣，即代表安全清單彙總功能正常運作。


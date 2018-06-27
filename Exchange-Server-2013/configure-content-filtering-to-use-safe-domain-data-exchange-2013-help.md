---
title: '設定內容篩選要使用安全網域資料: Exchange 2013 Help'
TOCTitle: 設定內容篩選要使用安全網域資料
ms:assetid: 1ee2b663-b4f3-4fef-8954-986f2d820924
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn467930(v=EXCHG.150)
ms:contentKeyID: 59637254
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定內容篩選要使用安全網域資料

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-12-16_

安全網域資料是儲存在使用者的安全寄件者清單中的整個網域 (例如 @contoso.com)。根據預設，內容篩選器代理程式不會使用安全網域資料以識別允許略過內容篩選的寄件者。

此預設的設定有助於減少垃圾郵件傳遞至您的組織。例如，使用者可能會將大量電子郵件提供者的網域新增至其安全的寄件者清單。如果這個網域經常使用或詐騙的垃圾郵件，並從該網域中任何寄件者的郵件如果內容篩選設定為使用安全網域資料標示為安全的訊息，會傳遞給您組織中的收件者。

我們建議您不要修改預設設定在大多數情況下。不過，您可以設定儲存在Active Directory及由內容篩選標示為安全的郵件使用者的安全網域資料。若要這樣做，您需要修改 MSExchangeMailboxAssistants.exe.config XML 應用程式設定檔與 Microsoft Exchange 信箱助理員服務，依照本主題稍後的相關聯。當您進行變更此設定時，安全網域的雜湊資料並儲存在每個使用者的**msExchSafeSenderHash**使用者物件屬性中Active Directory安全清單彙總的一部分。內容篩選器代理程式可以使用安全網域資料標示為安全網域中寄件者的郵件。如需安全清單彙總的詳細資訊，請參閱[安全清單彙總](safelist-aggregation-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘

  - Exchange 權限無法套用於此主題的程序。在 Exchange 伺服器的作業系統中執行這些程序。

  - 儲存至 MSExchangeMailboxAssistants.exe.config 檔案的變更會套用之後重新啟動 Microsoft Exchange 信箱助理員服務。

  - 在您安裝 Exchange 累計更新 (CU) 後，將會覆寫您在 Exchange XML 應用程式組態檔 (例如 Client Access Server 上的 web.config 檔案，或 Mailbox Server 上的 EdgeTransport.exe.config 檔案) 中任何自訂的個別伺服器設定。請務必儲存此資訊，以便安裝後能輕易地重新設定伺服器。在安裝 Exchange CU 後，您必須重新配置這些設定。

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


## 使用命令提示字元中設定要使用安全網域資料的內容篩選

1.  在 \[命令提示字元\] 視窗中開啟 MSExchangeMailboxAssistants.exe.config 檔案在 \[記事本\] 執行下列命令：
    
        Notepad %ExchangeInstallPath%Bin\MSExchangeMailboxAssistants.exe.config

2.  找出檔案結尾處*\</appsettings\>*機碼並貼上*\</appsettings\>*按鍵之前的下列機碼：
    
        <add key="IncludeSafeDomains" value="true" />

3.  完成時，儲存並關閉 MSExchangeMailboxAssistants.exe.config 檔案。

4.  執行下列命令以重新啟動 Microsoft Exchange 信箱助理員服務：
    
        net stop MSExchangeMailboxAssistants && net start MSExchangeMailboxAssistants

## 如何知道這是否正常運作？

若要確認您已成功設定要使用安全網域資料的內容篩選，請執行下列動作：

1.  確認將網域新增至使用者的安全寄件者清單在 Outlook 中已更新Active Directory中的使用者的**msExchSafeSenderHash**屬性。若要這樣做，ADSIEdit.exe 或 LDP.exe 中檢視屬性、 在 Outlook 中開啟使用者的信箱、 將網域新增至安全的寄件者清單、 執行命令`Update-Safelist <username>`，並確認**msExchSafeSenderHash**的原始和目前值是不同。

2.  安全網域資料儲存在Active Directory之後，傳送測試郵件從該網域中的外部寄件者至您的組織中的使用者。確認郵件已標示為安全檢查郵件標頭中的反垃圾郵件標頭欄位。


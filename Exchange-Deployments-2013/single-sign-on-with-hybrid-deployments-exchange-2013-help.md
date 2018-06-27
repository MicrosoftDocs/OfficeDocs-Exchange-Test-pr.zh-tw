---
title: '單一登入與混合式部署: Exchange 2013 Help'
TOCTitle: 單一登入與混合式部署
ms:assetid: 050606f9-718d-4a1f-b7a6-50b08c6e9e07
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh563846(v=EXCHG.150)
ms:contentKeyID: 50474695
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 單一登入與混合式部署

 

_<strong>適用版本：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2016-01-29_

單一登入功能可讓使用者以單一使用者名稱與密碼進入內部部署與 Office 365 組織。單一登入可提供使用者熟悉的單一登入體驗，並讓管理員能輕鬆地透過內部部署 Active Directory 管理工具來管理 Exchange Online 組織信箱的帳戶原則。雖然您不需要在啟用單一登入時設定混合部署，不過強烈建議您這麼做。沒有單一登入，使用者必須記住兩組不同的認證，一組用於內部部署組織，一組用於 Office 365。以下是單一登入的其他幾個優點：

  - **Exchange Online 封存**   部署單一登入時，內部部署 Outlook 使用者在首次存取 Exchange Online 組織中的已封存內容時，系統會提示他們提供認證。不過，使用者隨後可以選擇「儲存密碼」以暫時避免往後再出現認證提示，而只會在他們的內部部署帳戶密碼變更時，系統才會再次提示他們提供認證。如果 Exchange 組織未部署單一登入，且已啟用 Exchange Online 封存，內部部署使用者主體名稱 (UPN) 必須符合其 Exchange Online 帳戶，而且系統將在使用者存取其封存時，一律提示他們提供其內部部署認證。

  - **原則控制**   您可以透過 Active Directory 控制帳戶原則，讓您能夠管理密碼原則、工作站限制、鎖定控制等等，而不必另外在 Office 365 組織中執行其他工作。

  - **降低支援要求**   遺忘密碼是所有公司中最常見的支援要求原因。如果使用者需要記住較少的密碼，遺忘的可能性會較低。

部署單一登入時，您會有兩個選項：密碼同步處理和 Active Directory 同盟服務 (AD FS)。這兩個選項皆由 Azure Active Directory Connect 提供。強烈建議使用密碼同步處理方法，除非您有需要 AD FS 的特定需求。密碼同步處理提供和 AD FS 相同的許多優點，且可省去部署的複雜。下表提供個選項的常見優點和缺點。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，如果您部署 AD FS，而網際網路因為任何原因無法連線到您的內部部署 AD FS 伺服器，Office 365 會切換使用密碼同步處理來驗證使用者。這樣一來，即使您的內部部署無法使用，也能讓具備 Office 365 信箱的使用者繼續不中斷地工作。</td>
</tr>
</tbody>
</table>


若要深入了解每個選項，請參閱 [Azure AD Connect 使用者登入選項](http://go.microsoft.com/fwlink/p/?linkid=723514)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>單一登入方法</p></th>
<th><p>優點</p></th>
<th><p>缺點</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>密碼同步處理 (建議選項)</p></td>
<td><ul>
<li><p>明顯沒有 AD FS 那麼複雜</p></li>
<li><p>即使您的內部部署 Active Directory 無法使用，使用者還是可以登入 Office 365。</p></li>
<li><p>部署密碼同步處理需要較少的其他伺服器。</p></li>
<li><p>不需要協力廠商憑證。</p></li>
<li><p>不需要透過 AD FS 從外部存取您的內部部署 Active Directory。</p></li>
<li><p>通常可以在幾小時內完成部署。</p></li>
</ul></td>
<td><ul>
<li><p>停用內部部署 Active Directory 中的使用者帳戶並不會在 Office 365 中停用它。您必須在 Office 365 管理入口網站中手動停用帳戶。</p></li>
<li><p>需要內部部署 Active Directory。不支援其他目錄服務。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AD FS</p></td>
<td><ul>
<li><p>密碼變更會立刻生效。</p></li>
<li><p>停用內部部署 Active Directory 中的使用者會同時停用其內部部署網路存取和其 Office 365 帳戶。</p></li>
<li><p>支援 Active Directory 以外的目錄服務。</p></li>
<li><p>支援非常龐大且不同的部署。</p></li>
<li><p>支援雙重要素驗證。</p></li>
</ul></td>
<td><ul>
<li><p>需要更多伺服器，其中至少一個必須位於您的周邊網路。</p></li>
<li><p>需要公用 IP 位址和 TCP 連接埠 443 都必須能夠在您的防火牆上開啟。</p></li>
<li><p>若要偵測帳戶密碼變更或近期曾啟用或停用帳戶，必須要具備與內部部署 Active Directory 的連線能力。</p></li>
</ul></td>
</tr>
</tbody>
</table>


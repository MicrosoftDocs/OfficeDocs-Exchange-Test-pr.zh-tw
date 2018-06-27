---
title: '行動裝置信箱原則: Exchange 2013 Help'
TOCTitle: 行動裝置信箱原則
ms:assetid: 9317b3bc-44a1-4e54-bc51-4f0b194b6a55
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123783(v=EXCHG.150)
ms:contentKeyID: 50473775
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 行動裝置信箱原則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-06-16_

在 MicrosoftExchange Server 2013 中，您可以建立行動裝置信箱原則，對一群使用者套用一組共通的原則或安全性設定。在 Exchange ActiveSync 組織中部署 Exchange 2013 之後，您可以建立新的行動裝置信箱原則，或修改現有的原則。當您安裝 Exchange 2013 時，會建立一個預設的行動裝置信箱原則。系統將自動分配此預設的行動裝置信箱原則給所有使用者。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Windows Phone 7 行動電話只支援所有 Exchange ActiveSync 信箱原則設定的子集。如需完整清單，請參閱Windows Phone 7 Synchronization。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>iOS7 指紋辨識器不支援作為裝置密碼。如果您讓指紋辨識器保護 iOS7 裝置，而且行動裝置信箱原則需要密碼，則還是需要建立和輸入密碼。</td>
</tr>
</tbody>
</table>


## 行動裝置信箱原則概述

您可以使用行動裝置信箱原則來管理許多不同的設定。其中包含下列各項：

  - 需要密碼

  - 指定密碼長度下限

  - 需要在密碼中使用數字或特殊字元

  - 指定在要求使用者重新輸入密碼之前，裝置可以維持閒置的時間

  - 在密碼錯誤幾次之後清除裝置

如需您可設定之所有設定的相關資訊，請參閱\&quot;行動裝置原則設定\&quot;。

## 管理 Exchange ActiveSync 信箱原則

行動裝置信箱原則可以在 Exchange 系統管理中心 (EAC) 或 Exchange 管理命令介面中建立。如果您在 EAC 中建立原則，則只能設定可用設定的子集。您可以使用命令介面設定其餘的設定。

## Windows Phone 7 同步處理

如果您的組織中有 Windows Phone 7 行動電話，則在設定某些 Exchange ActiveSync 信箱原則屬性時，這些電話會遇到同步處理問題。若要讓 Windows Phone 7 行動電話與 Exchange 信箱同步處理，請將 **AllowNonProvisionableDevices** 屬性設為 True，或只設定下列 Exchange ActiveSync 信箱原則屬性：

  - AllowSimplePassword

  - BlockInternetSharing

  - BlockRemoteDesktop

  - DisableDesktopSync

  - DisableIrDA

  - DisableRemovableStorage

  - DeviceWipeThreshold

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - PasswordExpiration

  - PasswordHistory

  - PasswordRequired

## 行動裝置信箱原則設定

下表概述您可以使用行動裝置信箱原則來指定的設定。

### 行動裝置信箱原則設定

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>允許 Bluetooth</p></td>
<td><p>此設定指定行動裝置是否允許藍芽連線。可用的選項為 [停用]、[僅限免持聽筒] 及 [允許]。預設值為 [允許]。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="even">
<td><p>允許瀏覽器</p></td>
<td><p>此設定指定行動裝置上是否允許 Pocket Internet Explorer。此設定不會影響行動裝置上安裝的第三方瀏覽器。預設值為 <code>$true</code>。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="odd">
<td><p>允許照相機</p></td>
<td><p>此設定指定是否可以使用行動裝置照相機。預設值為 <code>$true</code>。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="even">
<td><p>允許用戶電子郵件</p></td>
<td><p>此設定指定行動裝置使用者是否可以設定個人電子郵件帳戶 （POP3 或 IMAP4） 行動裝置上。預設值為<code>$true</code>。此設定不會控制存取權使用協力廠商的行動裝置電子郵件程式的電子郵件帳戶。 Exchange Enterprise 用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="odd">
<td><p>允許桌面同步</p></td>
<td><p>此設定指定行動裝置與桌上型電腦是否可透過纜線、藍芽或 IrDA 連線進行同步處理。預設值為 <code>$true</code>。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="even">
<td><p>允許外部裝置管理</p></td>
<td><p>此設定指定是否允許以外部裝置管理程式來管理行動裝置。</p></td>
</tr>
<tr class="odd">
<td><p>允許 HTML 電子郵件</p></td>
<td><p>此設定指定與行動裝置進行同步處理的電子郵件是否可為 HTML 格式。如果此設定設為 <code>$false</code>，表示所有電子郵件都會轉換為純文字。</p></td>
</tr>
<tr class="even">
<td><p>允許網際網路共用</p></td>
<td><p>此設定指定行動裝置是否可以作為桌上型電腦或可攜式電腦的數據機。預設值為 <code>$true</code>。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="odd">
<td><p>AllowIrDA</p></td>
<td><p>此設定指定是否可對行動裝置建立紅外線連線。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="even">
<td><p>允許行動 OTA 更新</p></td>
<td><p>此設定指定行動裝置信箱原則設定是否可以透過手機資料連線傳送到行動裝置中。預設值為 <code>$true</code>。</p></td>
</tr>
<tr class="odd">
<td><p>允許非可提供裝置</p></td>
<td><p>此設定指定是否允許可能不支援的所有原則設定的應用程式的行動裝置使用Exchange ActiveSync連接到Exchange 2013 。允許非可提供行動裝置有安全性含意。例如，某些非可提供裝置可能無法實作組織的密碼需求。</p></td>
</tr>
<tr class="even">
<td><p>允許 POPIMAPEmail</p></td>
<td><p>此設定會指定使用者是否可以設定 POP3 或 IMAP4 電子郵件帳戶行動裝置上。預設值為<code>$true</code>。此設定不會控制與協力廠商電子郵件程式存取。</p></td>
</tr>
<tr class="odd">
<td><p>允許遠端桌面</p></td>
<td><p>此設定指定行動裝置是否可以初始化遠端桌面連線。預設值為 <code>$true</code>。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="even">
<td><p>允許簡單密碼</p></td>
<td><p>此設定決定是否允許使用簡單密碼，例如 1111 或 1234。預設值是 <code>$true</code>。</p></td>
</tr>
<tr class="odd">
<td><p>允許 S/MIME 加密演算法交涉</p></td>
<td><p>此設定指定行動裝置的郵件應用程式是否可以交涉加密演算法萬一收件者憑證不支援指定的加密演算法。</p></td>
</tr>
<tr class="even">
<td><p>允許 S/MIME 軟體憑證</p></td>
<td><p>此設定指定是否允許在行動裝置上使用 S/MIME 軟體憑證。</p></td>
</tr>
<tr class="odd">
<td><p>允許儲存卡</p></td>
<td><p>此設定指定行動裝置是否可以存取儲存卡上所儲存的資訊。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="even">
<td><p>允許簡訊</p></td>
<td><p>此設定指定是否允許來自行動裝置的文字訊息。預設值為 <code>$true</code>。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="odd">
<td><p>允許未簽署的應用程式</p></td>
<td><p>此設定指定是否可以在行動裝置上安裝未簽署的應用程式。預設值為 <code>$true</code>。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="even">
<td><p>允許未簽署的安裝套件</p></td>
<td><p>此設定指定是否可以在行動裝置上執行未簽署的安裝套件。預設值為 <code>$true</code>。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="odd">
<td><p>允許 Wi-Fi</p></td>
<td><p>此設定指定裝行動置上是否允許無線網際網路存取。預設值為 <code>$true</code>。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="even">
<td><p>需要英數字元密碼</p></td>
<td><p>此設定要求密碼必須包含數字與非數字字元。預設值為 <code>$true</code>。</p></td>
</tr>
<tr class="odd">
<td><p>核准的應用程式清單</p></td>
<td><p>此設定儲存可以在行動行動上執行的已核准應用程式的清單。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
<tr class="even">
<td><p>已啟用附件</p></td>
<td><p>此設定允許將附件下載至行動裝置。預設值為 <code>$true</code>。</p></td>
</tr>
<tr class="odd">
<td><p>已啟用裝置加密</p></td>
<td><p>此設定啟用行動裝置的加密功能。並非所有行動裝置都可以強制加密。如需詳細資訊，請參閱裝置和行動作業系統文件。</p></td>
</tr>
<tr class="even">
<td><p>裝置原則重新整理間隔</p></td>
<td><p>此設定指定從伺服器傳送行動裝置信箱原則到行動裝置的頻率。</p></td>
</tr>
<tr class="odd">
<td><p>啟用的 IRM</p></td>
<td><p>此設定指定是否在行動裝置上啟用資訊版權管理 (IRM)。</p></td>
</tr>
<tr class="even">
<td><p>附件大小上限</p></td>
<td><p>此設定控制可下載至行動裝置之附件的大小上限。預設值為無限制。</p></td>
</tr>
<tr class="odd">
<td><p>行事曆保留篩選上限</p></td>
<td><p>此設定指定可與行動裝置進行同步處理的行事曆天數最大範圍。下列是公認的值：</p>
<ol>
<li><p>全部</p></li>
<li><p>OneDay</p></li>
<li><p>ThreeDays</p></li>
<li><p>OneWeek</p></li>
<li><p>TwoWeeks</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>電子郵件保留篩選上限</p></td>
<td><p>此設定指定電子郵件項目同步至行動裝置的最多天數。下列是公認的值：</p>
<ol>
<li><p>全部</p></li>
<li><p>OneDay</p></li>
<li><p>ThreeDays</p></li>
<li><p>OneWeek</p></li>
<li><p>TwoWeeks</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>電子郵件內文截斷大小上限</p></td>
<td><p>此設定指定電子郵件同步至行動裝置時截斷的大小上限。此值以 KB 計算。</p></td>
</tr>
<tr class="even">
<td><p>電子郵件 HTML 內文截斷大小上限</p></td>
<td><p>此設定指定 HTML 電子郵件同步至行動裝置時截斷的大小上限。此值以 KB 計算。</p></td>
</tr>
<tr class="odd">
<td><p>閒置時間鎖定上限</p></td>
<td><p>此設定指定行動裝置可為非使用中的時間長度，超過此時間長度則會要求輸入密碼以重新啟用行動裝置。您可以輸入介於 30 秒到 1 小時之間的任何間隔。此預設值為 15 分鐘。</p></td>
</tr>
<tr class="even">
<td><p>密碼失敗的嘗試上限</p></td>
<td><p>此設定指定使用者能夠針對行動裝置嘗試輸入正確密碼的次數。您可以輸入 4 到 16 之間的任何數字。預設值為 8。</p></td>
</tr>
<tr class="odd">
<td><p>最少的密碼複雜字元</p></td>
<td><p>此設定指定行動裝置密碼中的所需的字元組數。字元組為：</p>
<ul>
<li><p>小寫字母。</p></li>
<li><p>大寫字母。</p></li>
<li><p>數字 0 至 9。</p></li>
<li><p>特殊字元 （例如，驚嘆號引號）。</p></li>
</ul>
<p>您可以輸入 1 到 4 之間的任何數字。預設值為 1。</p>
<p>Windows Phone 8 裝置此設定會指定在密碼中的所需要的字元組數。例如，值為 3 需要從任何的字元組三個至少一個字元。</p>
<p>Windows Phone 10 裝置此設定可指定下列密碼複雜性需求：</p>
<ol>
<li><p>僅限數字。</p></li>
<li><p>數字及小寫字母。</p></li>
<li><p>數字、 小寫字母和大寫字母。</p></li>
<li><p>數字、 小寫字母大寫字母和特殊字元。</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>最小密碼長度</p></td>
<td><p>此裝置指定行動裝置密碼中字元數的下限。您可以輸入 1 到 16 之間的任何數字。預設值為 4。</p></td>
</tr>
<tr class="odd">
<td><p>已啟用密碼</p></td>
<td><p>此設定會啟用行動裝置密碼。</p></td>
</tr>
<tr class="even">
<td><p>密碼過期</p></td>
<td><p>此設定允許系統管理員設定一段時間，超過這段時間之後必須變更行動裝置密碼。</p></td>
</tr>
<tr class="odd">
<td><p>密碼歷程</p></td>
<td><p>此設定指定可以儲存在使用者信箱中的先前密碼數。使用者無法再使用儲存的密碼。</p></td>
</tr>
<tr class="even">
<td><p>已啟用密碼復原</p></td>
<td><p>啟用此設定時，行動裝置會產生復原密碼，此密碼會傳送至伺服器。如果使用者忘記行動裝置密碼，復原密碼可用來解除鎖定行動裝置，而且可讓使用者建立新的行動裝置密碼。</p></td>
</tr>
<tr class="odd">
<td><p>需要裝置加密</p></td>
<td><p>此設定指定是否需要裝置加密。如果設為 <code>$true</code>，裝置裝置必須可以支援和執行加密，才能與伺服器進行同步處理。</p></td>
</tr>
<tr class="even">
<td><p>需要加密的 S/MIME 郵件</p></td>
<td><p>此設定指定 S/MIME 郵件是否必須加密。預設值為 <code>$false</code>。</p></td>
</tr>
<tr class="odd">
<td><p>需要加密 S/MIME 演算法</p></td>
<td><p>此說定指定加密 S/MIME 郵件時必須使用的必要演算法。</p></td>
</tr>
<tr class="even">
<td><p>漫遊時需要手動同步處理</p></td>
<td><p>此設定指定行動裝置在漫遊時是否必須手動同步處理。允許漫遊時自動同步處理通常會導致行動裝置資料計劃的資料成本大於預期。</p></td>
</tr>
<tr class="odd">
<td><p>需要簽署的 S/MIME 演算法</p></td>
<td><p>此設定指定簽署郵件時必須使用的必要演算法。</p></td>
</tr>
<tr class="even">
<td><p>需要簽署的 S/MIME 郵件</p></td>
<td><p>此設定指定行動裝置是否必須傳送簽署的 S/MIME 郵件。</p></td>
</tr>
<tr class="odd">
<td><p>需要儲存卡加密</p></td>
<td><p>此設定指定儲存卡是否必須加密。並非所有行動裝置作業系統都支援儲存卡加密。如需詳細資訊，請參閱行動裝置和行動作業系統文件。</p></td>
</tr>
<tr class="even">
<td><p>未核准的 InROM 應用程式清單</p></td>
<td><p>此設定指定無法在 ROM 中執行的應用程式清單。需要有 Exchange 企業版用戶端存取授權，才能變更此設定的值。</p></td>
</tr>
</tbody>
</table>


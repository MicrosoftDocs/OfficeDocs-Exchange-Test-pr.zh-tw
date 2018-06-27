---
title: '在 Outlook for iOS 及 Android 使用基本驗證的帳戶設定: Exchange 2013 Help'
TOCTitle: 在 Outlook for iOS 及 Android 使用基本驗證的帳戶設定
ms:assetid: 013dbe8c-30de-4c9c-baa9-75081b9229e8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt829322(v=EXCHG.150)
ms:contentKeyID: 74518387
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Outlook for iOS 及 Android 使用基本驗證的帳戶設定

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2018-04-30_

**摘要：** 如何在 Exchange 2013 組織中的使用者可以快速地設定其 Outlook iOS 及 Android 使用基本驗證的帳戶。

Outlook iOS 及 Android 提供 Exchange 系統管理員帳戶設定 「 推送"到其使用基本驗證透過 ActiveSync 通訊協定的內部部署使用者的能力。此功能適用於任何行動裝置管理 (MDM) 提供者提供者 for Android 使用[受管理的應用程式設定](https://developer.apple.com/library/content/samplecode/sc2279/introduction/intro.html)通道 iOS 或[Android 在企業中](https://developer.android.com/samples/apprestrictions/index.html)的通道。

內部使用者在 Microsoft Intune 中註冊，您可以部署在 Azure 入口網站中使用 Intune 的帳戶組態設定。

之後已建立帳戶設定及使用者註冊使用者的裝置的 iOS Outlook 及 Android 會偵測的帳戶是""且然後會提示使用者將帳戶新增。使用者必須輸入才能完成安裝程序的唯一資訊是其密碼。然後，使用者的信箱內容會載入並使用者即可開始使用該應用程式。

下列圖像顯示使用者安裝程序的範例之後已在 Intune Azure 入口網站中設定 Outlook for iOS 及 android （英文）。

![Outlook for iOS 和內部部署 Android 的帳戶設定](images/Mt829322.04bd56f2-5c45-4268-8762-436994acd656(EXCHG.150).png "Outlook for iOS 和內部部署 Android 的帳戶設定")

## 建立應用程式設定原則的 iOS Outlook 和使用 Microsoft Intune android （英文）

如果您使用 Microsoft Intune 做為您的行動裝置管理提供者，下列步驟可讓您將部署您運用 ActiveSync 通訊協定的基本驗證的內部部署信箱的帳戶組態設定。設定建立之後，您可以依照下一步\] 區段中指定組態設定的使用者群組指派設定。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您組織中的使用者會使用 iOS 及 Android 工時裝置，您需要建立不同的應用程式設定原則的每個平台。</td>
</tr>
</tbody>
</table>


1.  登入 Azure 入口網站。

2.  選取 \[**多個服務 \> 監控 + 管理 \> Intune**。

3.  在 \[管理\] 清單的**行動應用程式**blade，選取 \[**應用程式設定的原則**。

4.  在**應用程式設定原則**blade 中，選擇 \[**新增\]**。

5.  在**新增應用程式設定**blade 中，輸入應用程式組態設定的**名稱**、 及選擇性**描述**。

6.  **裝置註冊**類型選擇**受管理裝置**。

7.  **平台**，選擇 \[ **iOS**或**Android 工作**。

8.  選擇 \[**關聯的應用程式**，然後，在**Targeted apps** blade 中，選擇 \[ **IOS 的 Microsoft Outlook** \] 或 \[ **Microsoft Outlook for android （英文)**。

9.  按一下**\[確定\]**回到**新增應用程式設定**blade。

10. 選擇 \[**設定**\]。在**設定**blade，以定義將提供的 iOS Outlook 與 Android 設定關鍵值組。您輸入的關鍵值組所定義稍後在本文中的機碼值組\] 區段中。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要輸入關鍵值組，您可以使用設定設計或輸入 XML 屬性清單之間選擇。</td>
    </tr>
    </tbody>
    </table>


11. 當您已完成時，選擇**\[確定\]**。

12. 在**新增應用程式設定**blade 中，選擇 \[**建立**\]。

新建立的設定原則將會顯示在**應用程式設定原則**blade。

## 指派組態設定

您可以指派您在前一節的 Azure Active Directory 中的使用者群組建立的設定。當使用者已安裝的 Microsoft Outlook 應用程式時、 應用程式將變成由您指定的設定。若要執行這項作業：

1.  在 \[Intune 行動應用程式管理儀表板**行動應用程式**blade、 選擇 \[**應用程式設定原則**。

2.  從應用程式設定原則清單中選取的一個您想要指派，然後按**工作分派**。

3.  在**指派**blade 中，選擇 \[**選取群組**。

4.  在**選取群組**blade，選取您想要將指派應用程式設定 」 原則，然後選擇 \[**選取**，然後**儲存**Azure AD 群組。

## 關鍵值組

當您建立應用程式設定 」 原則 Azure 入口網站中或透過 MDM 提供者時，您將需要下列關鍵值組：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機碼</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailAccountName</p></td>
<td><p>此值會指定電子郵件帳戶顯示名稱將出現在其裝置上的使用者。</p>
<p><strong>公認的值</strong>： 字串</p>
<p><strong>如果未指定預設</strong>： &lt; 空白 &gt;</p>
<p><strong>範例</strong>： user@companyname.com</p>
<p><strong>Intune 權杖 *</strong>: {{username}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.EmailAddress</p></td>
<td><p>此值會指定用來傳送與接收郵件的電子郵件地址。</p>
<p><strong>公認的值</strong>： 字串</p>
<p><strong>如果未指定預設</strong>： &lt; 空白 &gt;</p>
<p><strong>範例</strong>： user@companyname.com</p>
<p><strong>Intune 權杖 *</strong>: {{郵件}}</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailUPN</p></td>
<td><p>此值會指定將用來驗證之帳戶的電子郵件設定檔的使用者主體名稱。</p>
<p><strong>公認的值</strong>： 字串</p>
<p><strong>如果未指定預設</strong>： &lt; 空白 &gt;</p>
<p><strong>範例</strong>： userupn@companyname.com</p>
<p><strong>Intune 權杖 *</strong>: {{userprincipalname}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.ServerAuthentication</p></td>
<td><p>此值會指定使用者的驗證方法。</p>
<p><strong>公認的值</strong>： '使用者名稱和密碼';' 憑證 '</p>
<p><strong>如果未指定預設</strong>: '使用者名稱和密碼'</p>
<p><strong>範例</strong>： '使用者名稱和密碼'</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.ServerHostName</p></td>
<td><p>此值會指定您的 Exchange 伺服器的主機名稱。</p>
<p><strong>公認的值</strong>： 字串</p>
<p><strong>如果未指定預設</strong>： &lt; 空白 &gt;</p></td>
</tr>
</tbody>
</table>


**\***Microsoft Intune 使用者可以使用會展開並根據 MDM 註冊使用者正確的值的 token。如需詳細資訊，請參閱[新增應用程式設定原則的受管理的 iOS 裝置](https://docs.microsoft.com/en-us/intune/app-configuration-policies-use-ios)。


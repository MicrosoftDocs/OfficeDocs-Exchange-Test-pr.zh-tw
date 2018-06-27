---
title: '建立共用原則: Exchange 2013 Help'
TOCTitle: 建立共用原則
ms:assetid: cae8cab0-6265-448b-8add-5202cdb20678
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657494(v=EXCHG.150)
ms:contentKeyID: 50474252
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立共用原則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

您可以使用共用原則，控制 Exchange 組織中的使用者如何與組織外的使用者共用行事曆資訊。共用原則可讓使用者自行建立，與不同類型的外部使用者對其行事曆資訊進行人員對人員共用。這些原則支援與外部同盟組織 (如 Office 365 或其他內部部署 Exchange 組織)、外部非同盟組織以及可存取網際網路的個人共用行事曆資訊。若要將特定的共用原則套用至使用者，請參閱[將共用原則套用至信箱](apply-a-sharing-policy-to-mailboxes-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建立共用原則是其中一個設定 Exchange 組織中的同盟共用的數個步驟。您必須設定內部部署 Exchange 組織的Azure Active Directory驗證系統的同盟信任之前可以與其他同盟 Exchange 組織共用行事曆資訊。同盟信任不一定網際網路共用原則。</td>
</tr>
</tbody>
</table>


若要深入了解同盟共用，請參閱[共用](sharing-exchange-2013-help.md)。

如需與同盟相關的其他管理工作，請參閱[同盟程序](federation-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「 行事曆與共用權限？[收件者權限](recipients-permissions-exchange-2013-help.md)主題中的一節。

  - 以下是在同盟 Exchange 組織之間共用原則的需求：
    
      - Exchange 2013用戶端存取伺服器需存在於每個 Exchange 組織。其中一個組織有Exchange 2013 Client Access server 和其他一個組織有Exchange 2010 SP3 或更新版本的用戶端存取伺服器的 Exchange 組織之間也支援共用原則。
    
      - 每個 Exchange 組織與Azure AD驗證系統建立同盟信任。如需詳細資訊，請參閱[設定同盟信任](configure-a-federation-trust-exchange-2013-help.md)。
    
      - 每個 Exchange 組織都已設定同盟組織識別碼。用於產生使用者電子郵件地址的網域已新增至組織識別碼。
    
      - 使用者信箱位於Exchange 2013 Mailbox server 或每個 Exchange 組織的Exchange 2010 Mailbox server 上。
    
      - 只有 Outlook 2010 (含) 以上版本及 Outlook Web App 使用者才能建立共用邀請。

  - 以下是與非同盟 Exchange 組織或個人共用原則的需求：
    
      - Exchange 2013 用戶端存取伺服器需在共用使用者行事曆資訊的 Exchange 組織中。
    
      - 使用者信箱位於共用使用者行事曆資訊的 Exchange 組織中設置的 Exchange 2013 信箱伺服器上。
    
      - 必須啟用 Exchange 2013 用戶端存取伺服器，才能存取 Outlook Web App。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 使用 EAC 建立共用原則

1.  瀏覽至 \[組織\]\> \[共用\]。

2.  在清單檢視的 \[個人共用\] 下，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 \[新增共用原則\] 的 \[原則名稱\] 方塊中輸入共用原則的好記名稱。

4.  按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 來指定共用原則的共用規則。

5.  在 \[共用規則\] 中，選取下列其中一個選項來指定要與其共用的網域：
    
      - **與所有網域共用**
    
      - **與特定網域共用**

6.  如果您選取了 \[與特定網域共用\]，請輸入要共用的網域名稱。如果您需要為此共用原則輸入多個網域，請儲存第一個網域的設定，然後編輯共用規則以新增其他網域。

7.  若要定義要對原則強制執行的行事曆共用層級，請勾選 \[共用您的行事曆資料夾\] 核取方塊，然後選取下列其中一個選項：
    
      - **僅行事曆空閒/忙碌的時間資訊**
    
      - **行事曆空閒/忙碌的時間、主旨與地點資訊**
    
      - **所有的行事曆約會資訊，包括時間、主旨、位置和標題**

8.  按一下 \[儲存\] 設定共用原則的規則。

9.  如果要將此共用原則設定為 Exchange 組織中使用的預設共用原則，請選取 \[設定此原則成為我的預設共用原則\]。

10. 按一下 \[儲存\] 建立共用原則。

## 使用 EAC 允許所有使用者共用完整的行事曆詳細資料

您可以編輯預設共用原則，允許所有使用者與組織外的人共用完整的行事曆詳細資料。

1.  瀏覽至 \[組織\]\> \[共用\]。

2.  在清單檢視的 \[個人共用\]下，選取 \[預設共用原則\]，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[共用原則\] 對話方塊中，選取 \[與所有網域共用\]，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  在 \[共用規則\] 對話方塊的 \[指定要共用的資訊\] 下，選取 \[所有的行事曆約會資訊，包括時間、主旨、位置和標題\]，然後按一下 \[儲存\]。

5.  在 \[共用原則\] 對話方塊中，按一下 \[儲存\] 設定共用原則的規則。

## 使用命令介面來建立共用原則

  - 這個範例會為外部同盟網域 contoso.com 建立共用原則 Contoso。這個原則可讓 contoso.com 網域中的使用者查看您的使用者的詳細行事曆可用性 (空閒/忙碌) 資訊。預設會啟用這個原則。
    
        New-SharingPolicy -Name "Contoso" -Domains contoso.com: CalendarSharingFreeBusyDetail

  - 此範例會針對兩個不同的同盟網域 (contoso.com 和 woodgrovebank.com) 建立共用原則 ContosoWoodgrove，並為每個網域設定不同的共用動作。這個原則已停用。
    
        New-SharingPolicy -Name "ContosoWoodgrove" -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'woodgrovebank.com: CalendarSharingFreeBusyDetail -Enabled $false

  - 此範例會為含有用戶端存取伺服器 CAS01 與信箱伺服器 MAIL01 的 Exchange 組織建立共用原則 Anonymous，並針對有限的行事曆可用性資訊設定共用動作。這個原則可讓您 Exchange 組織中的使用者寄送連結給擁有網際網路存取權的使用者，邀請其檢視自己的行事曆可用性資訊。已啟用原則。
    
    1.  設定 MAIL01 的 Web Proxy URL。
        
            Set-ExchangeServer -Identity "Mail01" -InternetWebProxy "<Webproxy URL>"
    
    2.  在 CAS01 上啟用發行虛擬目錄。
        
            Set-OwaVirtualDirectory -Identity "CAS01" -ExternalURL "<URL for CAS01>" -CalendarPublishingEnabled $true
    
    3.  建立共用原則 Anonymous，並設定有限的行事曆資訊共用。
        
            New-SharingPolicy -Name "Anonymous" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

如需詳細的語法及參數資訊，請參閱下列主題：

  - [New-SharingPolicy](https://technet.microsoft.com/zh-tw/library/dd298186\(v=exchg.150\))

  - [Set-ExchangeServer](https://technet.microsoft.com/zh-tw/library/bb123716\(v=exchg.150\))

  - [Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-tw/library/bb123515\(v=exchg.150\))

## 如何知道這是否正常運作？

若要驗證您是否已成功建立共用原則，請執行下列命令介面命令來確認共用原則資訊。

    Get-SharingPolicy <policy name> | format-list

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


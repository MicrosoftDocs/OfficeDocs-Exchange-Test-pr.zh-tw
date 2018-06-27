---
title: '啟用網際網路行事曆發佈: Exchange 2013 Help'
TOCTitle: 啟用網際網路行事曆發佈
ms:assetid: b4c71696-52bb-492c-8259-0e419acd0bbc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ853046(v=EXCHG.150)
ms:contentKeyID: 50554086
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用網際網路行事曆發佈

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-08-22_

**摘要：** 若要啟用與外部組織共用行事曆空閒/忙碌資訊的 OWA 使用者在 Exchange 2013 組織中使用這些程序。

Microsoft Exchange Server 2013 組織中的使用者可以與非 Exchange 組織中的使用者和可存取網際網路的其他人，共用行事曆可用性 (空閒/忙碌) 資訊。網際網路行事曆發佈可提供較大的彈性，並增加能夠共用行事曆可用性資訊的使用者數量。

啟用網際網路行事曆發佈包含三個一般步驟：

1.  設定 Web proxy URL （這是步驟只需要如果 URL 已存在於您的組織中的 Web proxy 否則請跳至步驟 2） 的信箱伺服器。

2.  啟用 Client Access Server 的發佈虛擬目錄。

3.  特別針對網際網路行事曆發佈建立一個專用的共用原則，或更新預設的共用原則來支援 \[匿名\] 網域。任一種方法都可讓 Exchange 組織中的使用者邀請其他可存取網際網路的使用者來存取所發佈的 URL，以檢視有限的行事曆可用性資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>後完成步驟 3，使用者則須將其從 Outlook 行事曆發佈。行事曆發佈會建立使用者可提供給其組織外部人員的 Url。一個 URL 可讓訂閱行事曆使用 Outlook 或 Outlook Web 應用程式及其他屬性可讓收件者檢視在網頁瀏覽器中的行事曆的收件者。每位使用者可以控制其他人可以看到多少詳細資料。</td>
</tr>
</tbody>
</table>


如需與共用原則相關的其他管理工作，請參閱[共用原則](sharing-policies-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：15 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「行事曆與共用權限」項目。

  - Exchange 2013 用戶端存取伺服器需存在於共用使用者行事曆資訊的 Exchange 組織中。

  - 使用者信箱位於共用使用者行事曆資訊之 Exchange 組織中的 Exchange 2013 信箱伺服器上。

  - 只有 Outlook 2010 (含) 以上版本及 Outlook Web App 使用者才能建立共用邀請。

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


## 該怎麼做？

## 步驟 1：使用命令介面設定 Web Proxy URL

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這是僅限必要步驟如果您組織中已經存在的 Web proxy URL。如果不是，請跳至步驟 2。<br />
您無法使用 Exchange 系統管理中心 (EMC) 來設定 Web Proxy URL。</td>
</tr>
</tbody>
</table>


此範例在 Mailbox Server MAIL01 上設定 Web Proxy URL。

    Set-ExchangeServer -Identity "MAIL01" -InternetWebProxy "<Webproxy URL>"

如需詳細的語法及參數資訊，請參閱 [Set-ExchangeServer](https://technet.microsoft.com/zh-tw/library/bb123716\(v=exchg.150\))。

## 如何才能了解此步驟是否正常運作？

若要驗證您是否已成功設定 Web Proxy URL，請執行下列命令介面命令，然後確認 *InternetWebProxy* 參數資訊。

    Get-ExchangeServer | format-list

## 步驟 2：使用命令介面啟用發佈虛擬目錄

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 來啟用發佈虛擬目錄。</td>
</tr>
</tbody>
</table>


此範例在 Client Access Server CAS01 上啟用發佈虛擬目錄。

    Set-OwaVirtualDirectory -Identity "CAS01\owa (Default Web Site)" -ExternalUrl "<URL for CAS01>" -CalendarEnabled $true

身分識別`CAS01\owa (Default Web Site)`所在的伺服器名稱和 Outlook Web App 虛擬目錄。

如需詳細的語法及參數資訊，請參閱 [Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-tw/library/bb123515\(v=exchg.150\))。

## 如何才能了解此步驟是否正常運作？

若要驗證您是否已成功啟用發佈虛擬目錄，請執行下列命令介面命令，然後確認 *ExternalURL* 參數資訊。

    Get-OwaVirtualDirectory | format-list

## 步驟 3： 建立或設定專用於網際網路行事曆發佈共用原則

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>步驟 3 中的下列選項僅適用於 Exchange Online 環境。</td>
</tr>
</tbody>
</table>


您必須選擇建立共用原則的網際網路行事曆發佈 （選項 1） 或設定預設共用原則網際網路行事曆發佈 （選項 2）。 使用這兩個選項您需要使用 EAC 或命令介面中的選擇。

## 做法 1： 建立專用於網際網路行事曆發佈共用原則

如果您想建立專用於網際網路行事曆發佈的共用原則，請完成下列步驟。

## 使用 EAC

1.  瀏覽至 \[組織\]\> \[共用\]。

2.  在清單檢視的 \[個人共用\] 下，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 \[共用原則\] 中，於 \[原則名稱\] 欄位中輸入共用原則的易記名稱 (例如 **Internet**)。

4.  按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 來定義共用原則的共用規則。

5.  在 \[共用規則\] 中，按一下 \[與特定網域共用\]，然後在相應欄位中輸入 **Anonymous**。

6.  若要指定對於共用原則強制執行的行事曆共用層級，請勾選 \[共用您的行事曆資料夾\] 核取方塊，然後選取下列其中一項：
    
      - **僅行事曆空閒/忙碌的時間資訊**
    
      - **行事曆空閒/忙碌的時間、主旨與地點資訊**
    
      - **所有的行事曆約會資訊，包括時間、主旨、位置和標題**

7.  按一下 \[儲存\] 設定共用原則的規則。

8.  在 \[共用原則\] 中，按一下 \[儲存\] 來建立原則。

## 使用命令介面

此範例會建立名為 Internet 的網際網路行事曆發佈共用原則，並將該原則設定為只共用可用性資訊。已啟用原則。

    New-SharingPolicy -Name "Internet" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

此範例將共用原則網際網路新增至使用者信箱。

    Set-Mailbox -Identity <user name> -SharingPolicy "Internet"

此範例將共用原則網際網路新增至組織單位 (OU)。

    Set-Mailbox -OrganizationalUnit <OU name> -SharingPolicy "Internet"

如需詳細的語法及參數資訊，請參閱 [New-SharingPolicy](https://technet.microsoft.com/zh-tw/library/dd298186\(v=exchg.150\)) 與 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 如何才能了解此步驟是否正常運作？

若要驗證您是否已成功建立共用原則，請執行下列命令介面命令來確認共用原則資訊。

    Get-SharingPolicy <policy name> | format-list

## 選項 2： 設定的預設共用原則網際網路行事曆發佈

如果您想設定網際網路行事曆發佈的預設共用原則，請完成下列步驟。

## 使用 EAC

1.  瀏覽至 \[組織\] \> \[共享\]。

2.  在清單檢視的 \[個人共用\]下，選取 \[預設共用原則\]，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[共用原則\] ，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 將共用規則新增至原則。

4.  在 \[共用規則\] 中，按一下 \[與特定網域共用\]，然後在相應欄位中輸入 **Anonymous**。

5.  若要指定對於共用原則強制執行的行事曆共用層級，請勾選 \[共用您的行事曆資料夾\] 核取方塊，然後選取下列其中一項：
    
      - **僅行事曆空閒/忙碌的時間資訊**
    
      - **行事曆空閒/忙碌的時間、主旨與地點資訊**
    
      - **所有的行事曆約會資訊，包括時間、主旨、位置和標題**

6.  按一下 \[儲存\] 設定共用原則的規則。

7.  在 \[共用原則\] 中，按一下 \[儲存\] 來儲存變更。

## 使用命令介面

此範例會更新預設共用原則，並設定為只共用可用性資訊。已啟用原則。

    Set-SharingPolicy -Name "Default Sharing Policy" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 如何才能了解此步驟是否正常運作？

若要驗證您是否已成功更新預設共用原則，請執行下列命令介面命令來確認共用原則資訊。

    Get-SharingPolicy <policy name> | format-list


---
title: '在混合式部署中內部部署與 Exchange Online 組織之間移動信箱: Exchange 2013 Help'
TOCTitle: 在混合式部署中內部部署與 Exchange Online 組織之間移動信箱
ms:assetid: d6289f7b-f67e-48db-9570-9fd3c9547548
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/o365e_hrcmoverequest_fl312271(v=EXCHG.150)
ms:contentKeyID: 51407021
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在混合式部署中內部部署與 Exchange Online 組織之間移動信箱

 

_<strong>適用版本：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2017-10-02_

利用 Exchange 型混合式部署，您可以選擇將內部部署 Exchange 信箱移至 Exchange Online 組織，或將 Exchange Online 信箱移至Exchange 組織。當您在內部部署和 Exchange Online 組織之間移動信箱時，您會使用移轉批次來執行遠端信箱移動的要求。這種方法可讓您移動現有的信箱，而不是建立新的使用者信箱並匯入使用者資訊。這種方法不同於將使用者信箱從內部部署 Exchange 組織移轉到 Exchange Online 做為完整 Exchange 遷移至雲端的一部份。本主題中討論的信箱移動是系統管理 Exchange 管理的一部份，其為內部部署 Exchange 和 Exchange Online 組織之間長期共存的關係。

如需將內部部署 Exchange 組織移轉至 Exchange Online 的詳細資訊，請參閱[將多個電子郵件帳戶移轉到 Office 365 的方法](https://go.microsoft.com/fwlink/p/?linkid=524030)。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須設定內部部署 Exchange 和 Exchange Online 組織之間的混合式部署，以完成本主題中的信箱移動程序。如需混合式部署的詳細資訊，請參閱 <a href="exchange-server-hybrid-deployments-exchange-2013-help.md">Exchange Server 混合部署</a>。<br />
<br />
在您將已啟用整合通訊 (UM) 的信箱移至 Exchange Online 之前，您必須確定內部部署商務用 Skype 2015、商務用 Skype Online 和 Exchange Online，都符合<a href="hybrid-deployment-prerequisites-exchange-2013-help.md">混合部署必要條件</a>中指定的需求。如需如何將您的內部部署 UM 信箱原則對應至 Exchange Online 中的原則，請參閱 <a href="https://technet.microsoft.com/zh-tw/library/bb124903(v=exchg.150)">Set-UMMailboxPolicy</a>。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘用來設定移轉批次，但是完成移轉的總時間要根據包含在每個移轉批次中的信箱數目而定。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[收件者權限](https://technet.microsoft.com/zh-tw/library/dd638132\(v=exchg.150\)) 主題中的「信箱移動及移轉權限」一節。

  - 混合式部署設定在您的內部部署與 Exchange Online 組織之間。

  - 如果您是執行 Exchange 2013，請確定信箱複寫 Proxy 服務 (MRSProxy) 已在您的內部部署 Exchange 2013 用戶端存取伺服器上啟用。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](https://technet.microsoft.com/zh-tw/library/jj150484\(v=exchg.150\))。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 步驟 1： 建立移轉端點

在 Exchange 混合式部署中執行登入和登出遠端移動移轉之前，建議您先建立 Exchange 遠端移轉端點。移轉端點含有正在執行 MRS proxy 服務 (和 Exchange Online 之間執行遠端移動移轉的必要項) 的內部部署 Exchange 伺服器連結設定。

如需逐步程序，請參閱 建立遷移端點。

## 步驟 2： 啟用 MRSProxy 服務

如果您的內部部署 Exchange 2013 用戶端存取伺服器尚未啟用 MRSProxy 服務，請遵循 Exchange 系統管理中心 (EAC) 中的下列步驟：

1.  開啟 EAC 並導覽至 \[**伺服器**\] \> \[**虛擬目錄**\]。

2.  選取用戶端存取伺服器，選取 **EWS** 虛擬目錄，然後按一下 \[**編輯**\] ![編輯圖示](images/JJ906432.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  選取 **\[啟用 MRS Proxy\]** 核取方塊，然後按一下 **\[儲存\]**。

## 步驟 3： 使用 EAC 移動信箱

您可以在 Exchange 伺服器上，使用 EAC 中 **Office 365** 索引標籤上的遠端移動移轉精靈，將內部部署組織中的現有使用者信箱移至 Exchange Online 組織，或將 Exchange Online 信箱移至內部部署組織。選擇下列其中一個程序：

## 將內部部署信箱移至 Exchange Online

您可以在 Exchange 伺服器上，使用 EAC 中 **Office 365** 索引標籤上的遠端移動移轉精靈，將內部部署組織中的現有使用者信箱移至 Exchange Online 組織。請遵循下列步驟：

1.  開啟 EAC，然後導覽至 \[**Office 365**\] \> \[**收件者**\] \> \[**移轉**\]。

2.  按一下 \[**新增**\] ![加入圖示](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，然後選取 \[**移轉至 Exchange Online**\]。

3.  在 \[**選取移轉類型**\] 頁面上，選取 \[**遠端移動移轉**\]，然後按 \[**下一步**\]。

4.  在 \[**選取使用者**\] 頁面上，按一下 \[**新增**\]  ![加入圖示](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，選取要移至 Office 365 的內部部署使用者，然後依序按一下 \[**新增**\] 和 \[**確定**\]。按 \[**下一步**\]。

5.  在 \[**輸入 Windows 使用者帳戶認證**\] 頁面上的 \[**內部部署管理員名稱**\] 文字欄位中，輸入內部部署管理員帳戶名稱，然後在 \[**內部部署管理員密碼**\] 文字欄位中輸入與此帳戶相關聯的密碼。例如：“corp\\administrator” 和密碼。按 \[**下一步**\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您已經建立移轉端點，您會收到這個步驟的端點確認提示。如果您已建立兩個以上的移轉端點，您必須從移轉端點下拉式功能表中選擇端點。</td>
    </tr>
    </tbody>
    </table>


6.  當精靈確認移轉端點後，請確認您內部部署 Exchange 伺服器的 FDQN 已列於 **\[確認移轉端點\]** 頁面上。例如：「mail.contoso.com」。按 **\[下一步\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>當您選取要移至 Exchange Online 的多個信箱時，Exchange 伺服器上的 MRSProxy 服務會自動節流處理信箱移動要求。完成信箱移動的總時間取決於選取的信箱總數、信箱大小及 MRSProxy 的組態。若要深入了解自訂 MRSProxy，請參閱：<a href="https://technet.microsoft.com/zh-tw/library/bb232205(v=exchg.150)">郵件節流</a>。</td>
    </tr>
    </tbody>
    </table>


7.  在 \[**移動設定**\] 頁面上的 \[**新移轉批次名稱**\] 文字欄位中，輸入移轉批次的名稱。使用向下箭號 ![向下箭號圖示](images/JJ906432.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "向下箭號圖示") 來選取 \[**要移轉至 Office 365 的信箱目標傳遞網域**\]。在大部分的混合式部署中，此為 Exchange Online 組織信箱所使用的主要 SMTP 網域。例如，contoso.mail.onmicrosoft.com。請確認 \[**將主要信箱連同封存信箱一起移動**\] 選項已選取，然後按 \[**下一步**\]。

8.  在 **\[啟動批次\]** 頁面上，至少選取一個要接收批次完成報告的收件者。請確認 **\[自動啟動批次\]** 選項已選取，然後選取 **\[自動完成移轉批次\]** 核取方塊。按一下 **\[新增\]**。

## 將 Exchange Online 信箱移至內部部署組織

您可以在 Exchange 伺服器上，使用 EAC 上 **Office 365** 索引標籤中的遠端移動移轉精靈，將內部部署組織中的現有使用者信箱移至 Exchange Online 組織：

1.  開啟 EAC 並導覽至 \[**Office 365**\] \> \[**收件者**\] \> \[**移轉**\]。

2.  按一下 \[**新增**\] ![加入圖示](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，然後選取 \[**從 Exchange Online 移轉**\]。

3.  在 \[**選取使用者**\] 頁面上，選取 \[**選取您想要移動的使用者**\]，然後按 \[**下一步**\]。

4.  在 \[**選取使用者**\] 頁面上，按一下 \[**新增**\] ![加入圖示](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，選取要移至內部部署組織的 Exchange Online 使用者，然後依序按一下 \[**新增**\] 和 \[**確定**\]。按 \[**下一步**\]。

5.  當精靈確認移轉端點後，請確認您內部部署 Exchange 伺服器的 FDQN 已列於 **\[確認移轉端點\]** 頁面上。例如：「mail.contoso.com」。按 **\[下一步\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>當您選取要移至 Exchange Online 的多個信箱時，Exchange 伺服器上的 MRSProxy 服務會自動節流處理信箱移動要求。完成信箱移動的總時間取決於選取的信箱總數、信箱大小及 MRSProxy 的內容。若要深入了解自訂 MRSProxy，請參閱<a href="https://technet.microsoft.com/zh-tw/library/bb232205(v=exchg.150)">郵件節流</a>。</td>
    </tr>
    </tbody>
    </table>


6.  在 \[移動設定\] 頁面上的 \[新移轉批次名稱\] 文字欄位中，輸入移轉批次的名稱。然後在 \[要移轉至 Office 365 的信箱目標傳遞網域\] 欄位中輸入目標傳遞網域。在大部分的混合式部署中，此為內部部署與 Exchange Online 組織信箱所使用的主要 SMTP 網域。例如，contoso.com。

7.  選擇是否也要移動選取之使用者的封存信箱，然後輸入您想要在 \[**目標資料庫**\] 文字欄位中將此信箱移至其中的資料庫名稱。例如，信箱資料庫 123456789。按 \[**下一步**\]。

8.  在 \[**啟動批次**\] 頁面上，至少選取一個要接收批次完整報告的收件者。請確認已選取 \[**自動啟動批次**\]，然後選取 \[**自動完成移轉批次**\] 核取方塊。按一下 \[**新增**\]。

## 步驟 4： 移除已完成的移轉批次

信箱移動完成之後，建議您移除已完成的移轉批次，如果相同的使用者再次移動，可將錯誤的可能性降至最低。

移除已完成的移轉批次：

1.  開啟 EAC 並導覽至 \[**Office 365**\] \> \[**收件者**\] \> \[**移轉**\]。

2.  移除已完成的移轉批次，然後按一下 \[**刪除**\] ![刪除圖示](images/JJ906432.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

3.  在刪除警告確認對話方塊中，按一下 \[**是**\]。

## 步驟 5：重新啟用 網頁型 Outlook 的離線存取

網頁型 Outlook (之前稱為 Outlook Web App) 中的離線存取能讓使用者在未連接網路的情況下存取自己的信箱。如果您將 Exchange 信箱移轉至 Exchange Online，使用者必須重設瀏覽器中的離線存取設定，才能離線使用 網頁型 Outlook。如需關於 網頁型 Outlook 中的離線存取、支援它的瀏覽器，以及如何開啟該功能的詳細資訊，請參閱[離線使用 Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=286942)。

## 如何才能了解這是否正常運作？

在您將現有的使用者信箱在內部部署和 Exchange Online 組織之間移動時，您會看到遠端移動精靈的順利完成訊息，此為信箱移動作業如預期完成的第一個指示。

信箱移動程序需要數分鐘的時間才會完成，您也可以開啟 EAC，然後選取 \[**Office 365**\] \> \[**收件者**\] \> \[**移轉**\]，以顯示遠端移動精靈中所選信箱的移動狀態，即可確認移動作業正確運作。在信箱移動期間，\[**狀態**\] 的值會顯示 \[**正在同步處理**\]，當信箱已順利移至內部部署或 Exchange Online 組織時，該值會顯示 \[**已完成**\]。

在信箱移動完成之後，您可以確認信箱內容，以檢查位於內部部署或 Exchange Online 組織上的遠端信箱是否已順利建立。若要執行該操作，請在內部部署組織或 Exchange 組織的 EAC 中，導覽至 \[**收件者**\] \> \[**信箱**\]。使用者信箱應會顯示 \[**Office 365**\] 的 \[**信箱類型**\] (若為 Exchange Online 信箱) 以及 \[**使用者**\] (若為內部部署信箱)。

您也可以在 Exchange 管理命令介面中執行下列指令程式，以確認移轉批次的狀態。

    Get-MigrationBatch -Identity <batch name>

有問題嗎？在 Office 365 論壇中尋求協助。若要存取此論壇，您需要以具有雲端式服務系統管理員存取權的帳戶登入。此論壇的網址為：[Office 365 論壇](https://go.microsoft.com/fwlink/p/?linkid=201915)

## 初次使用 Office 365 嗎？


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Dn249373.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="LinkedIn Learning 的短圖示" alt="LinkedIn Learning 的短圖示" /> <strong>初次使用 Office 365？</strong><br />
探索 LinkedIn Learning 提供的 <a href="https://support.office.com/zh-tw/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> 免費影片課程。</p></td>
</tr>
</tbody>
</table>


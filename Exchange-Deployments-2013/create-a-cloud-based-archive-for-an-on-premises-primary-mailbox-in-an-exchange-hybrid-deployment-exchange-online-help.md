---
title: '在 Exchange 混合式部署中建立內部部署主要信箱的雲端式封存: Exchange Online Help'
TOCTitle: 在混合式部署中建立內部部署主要信箱的雲端式封存
ms:assetid: ecc0a687-6c05-47bd-a079-a43d83cba9ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt791517(v=EXCHG.150)
ms:contentKeyID: 74253377
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Exchange 混合式部署中建立內部部署主要信箱的雲端式封存

 

_<strong>適用版本：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2017-01-20_

在 Exchange 混合式部署中，您可以透過 Exchange Online 內的雲端式封存信箱設定內部部署主要信箱。

步驟 1：啟用主要內部部署信箱的雲端式封存

步驟 2：確認雲端式封存信箱已經建立

(選擇性) 執行目錄同步處理

## 開始之前

  - 內部部署信箱的使用者必須在您的 Office 365 組織內有一個帳戶。

  - 您必須為 Office 365 使用者帳戶指派 Exchange Server 適用的 Exchange Online Archiving 授權。步驟 1 中的程序中已包含指派授權的步驟。

  - 當您在步驟 1 啟用雲端式封存信箱後，可能需要 30 分鐘來佈建雲端式封存信箱。這是因為雲端式封存信箱是在目錄同步處理的過程中建立，而您的內部部署 Active Directory 已與 Office 365 中的 AzureActive Directory (Azure AD) 進行同步。依預設，目錄同步處理會每 30 分鐘執行一次。

## 步驟 1：啟用主要內部部署信箱的雲端式封存信箱

使用下列其中一個程序，來啟用內部部署信箱的雲端式封存信箱。在 Exchange 系統管理中心、您的內部部署 Exchange 組織以及 Office 365 系統管理中心執行這些步驟。

建立新使用者的雲端式封存信箱

為現有使用者建立雲端式封存信箱

## 為新使用者建立雲端式封存信箱

1.  在您內部部署組織內的 EAC 中，前往 \[收件者\]  \> \[信箱\]。

2.  按一下\[新增\]![加入圖示](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") \> \[使用者信箱\]。

3.  在 \[新的使用者信箱\] 頁面上，為新的或現有的使用者建立信箱。如需建立使用者信箱的相關資訊，請參閱[建立使用者信箱](https://technet.microsoft.com/zh-tw/library/jj991919\(v=exchg.150\))。

4.  按一下\[更多選項\]以啟用雲端式封存信箱。

5.  在 \[封存\]下，按一下 \[針對此使用者建立就地封存\] 核取方塊，然後再按一下 \[雲端式封存\]。系統會顯示將在封存信箱中佈建的網域名稱。
    
    ![在 \[封存\] 下按一下核取方塊，然後按一下 \[雲端式封存\]](images/Mt791517.43d0473e-30ad-4021-94bc-a9c5449f43ba(EXCHG.150).png "在 [封存] 下按一下核取方塊，然後按一下 [雲端式封存]")  

6.  按一下\[儲存\] 以建立信箱和雲端式封存。
    
    請注意，在 \[信箱\] 頁面中，所選取信箱的 \[信箱類型\] 欄位中會顯示 \[使用者 (封存)\] 的值。

7.  請稍候 30 分鐘，進行目錄同步處理以在 Office 365 中建立對應的使用者帳戶。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ906432.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在 Office 365 系統管理中心 中，移至 [健康情況] &gt; [目錄同步作業狀態] 以查看上次目錄同步處理執行的時間。</td>
    </tr>
    </tbody>
    </table>


8.  確認了您在建立新的內部部署信箱之後才執行目錄同步處理作業，在 Office 365 系統管理中心中，移至 \[使用者\] \> \[作用中使用者\]，然後選取為新內部部署信箱建立的新 Office 365 使用者帳戶。

9.  在隨即出現的使用者內容頁面，按一下 \[產品授權\] 一節中的 \[編輯\]。
    
    ![在詳細資料窗格中按一下 \[編輯\]，以指派授權給選取的使用者](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "在詳細資料窗格中按一下 [編輯]，以指派授權給選取的使用者")  

10. 在 \[位置\] 下拉式功能表下，選取使用者的位置。

11. 展開 Office 365 企業授權清單，然後指派 **Exchange Server 適用的 Exchange Online Archiving** 授權，並儲存所做的變更。
    
    在使用者清單內的 \[狀態\] 欄位中，請注意授權現在已指派給使用者。

12. 同樣地，請稍候 30 分鐘，進行目錄同步處理以佈建雲端式封存信箱。請執行步驟 2，以查看如何確認雲端式封存信箱已建立。建立封存信箱之後，使用者可以使用 Outlook 或 網頁型 Outlook 來存取它。

回到頁首

## 為現有使用者建立雲端式封存信箱

1.  在 Office 365 系統管理中心 中，移至 \[使用者\] \> \[作用中使用者\]，然後選取您想要建立雲端式封存信箱的使用者帳戶。

2.  在隨即出現的使用者內容頁面，按一下 \[產品授權\] 一節中的 \[編輯\]。
    
    ![在詳細資料窗格中按一下 \[編輯\]，以指派授權給選取的使用者](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "在詳細資料窗格中按一下 [編輯]，以指派授權給選取的使用者")  

3.  在 \[位置\] 下拉式功能表下，選取使用者的位置。

4.  展開 Office 365 企業授權清單，然後指派 **Exchange Server 適用的 Exchange Online Archiving** 授權，並儲存所做的變更。
    
    在使用者清單內的 \[狀態\] 欄位中，請注意授權現在已指派給使用者。

5.  在您內部部署組織內的 EAC 中，前往 \[收件者\]  \> \[信箱\]。

6.  在信箱清單中，選取您剛指派授權的使用者。

7.  在詳細資料窗格的 \[就地封存\] 下，按一下 \[啟用\]。
    
    ![在詳細資料窗格中按一下 \[啟用\]，以啟用選取使用者的封存信箱](images/Mt791517.17ce99f7-d154-4e21-bec1-c938af1d4a0a(EXCHG.150).png "在詳細資料窗格中按一下 [啟用]，以啟用選取使用者的封存信箱")  

8.  在 \[建立就地封存\]頁面上，按一下 \[雲端式封存\]，然後按一下 \[確定\]。系統會顯示將在封存信箱中佈建的網域名稱。
    
    ![在 \[建立就地封存\] 頁面上，按一下 \[雲端式封存\]](images/Mt791517.9ad047c9-ef47-47df-93cc-0fab872f1ae1(EXCHG.150).png "在 [建立就地封存] 頁面上，按一下 [雲端式封存]")  
    
    請注意，在 \[信箱\] 頁面中，所選取信箱的 \[信箱類型\] 欄位中會顯示 \[使用者 (封存)\] 的值。

9.  請稍候 30 分鐘，進行目錄同步處理以建立雲端式封存信箱。請執行步驟 2，以查看如何確認雲端式封存信箱已建立。建立封存信箱之後，使用者可以使用 Outlook 或 網頁型 Outlook 來存取它。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ906432.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在 Office 365 系統管理中心中，移至 [健康情況] &gt; [目錄同步作業狀態] 以查看上次目錄同步處理執行的時間。</td>
    </tr>
    </tbody>
    </table>


回到頁首

## 步驟 2：確認雲端式封存信箱已經建立

如先前所解釋，從您啟用雲端式封存信箱到信箱真正建立，中間可能會有延遲。這是因為需要執行目錄同步處理以建立雲端式封存信箱。這是確認雲端式封存信箱是否已經建立的一些方法。

Exchange Online在組織中，執行下列 PowerShell 命令來顯示使用者的封存信箱與相關的屬性。若要連接至Exchange Online使用遠端 PowerShell，請參閱 ＜ [Connect to Exchange Online PowerShell](https://go.microsoft.com/fwlink/?/linkid=396554)。

    Get-MailUser <cloud mail user> | FL *archive*

當雲端式封存信箱佈建遭到擱置及封存信箱已經建立之後，下列螢幕擷取畫面會顯示傳回的屬性。

**目錄同步處理佈建雲端式封存信箱之前的郵件使用者屬性**

![已佈建雲端式封存之前的雲端式郵件使用者屬性](images/Mt791517.c6a42713-f061-4761-93c1-2b5478953e46(EXCHG.150).png "已佈建雲端式封存之前的雲端式郵件使用者屬性")

目錄同步處理佈建雲端式封存之前，*ArchiveStatus* 屬性已設定為 `None`。另外請注意，*ArchiveGuid* 和 *ArchiveName* 屬性為空。

**目錄同步處理佈建雲端式封存信箱之後的郵件使用者屬性**

![已佈建雲端式封存之後的雲端式郵件使用者屬性](images/Mt791517.005fcc87-6253-4218-aafc-50f212de54fa(EXCHG.150).png "已佈建雲端式封存之後的雲端式郵件使用者屬性")

目錄同步佈建雲端式封存之後，*ArchiveStatus* 屬性會設定為 `Active`，而 *ArchiveGuid* 和 *ArchiveName* 屬性會填入。此時，使用者將能夠在 Outlook 或 網頁型 Outlook中存取其雲端式封存信箱。

![使用者可以存取其 Outlook 或在 Web 上的 Outlook 中的雲端式封存信箱](images/Mt791517.8777bc4d-05c3-4489-8d8c-ff5429a0b2c3(EXCHG.150).png "使用者可以存取其 Outlook 或在 Web 上的 Outlook 中的雲端式封存信箱")

您也可以在您的內部部署 Exchange 組織中，執行下列的 PowerShell 命令，以顯示與使用者雲端式封存信箱相關的屬性。

    Get-Mailbox <on-premises user mailbox> | FL *archive*

**目錄同步處理佈建雲端式封存信箱之前的內部部署信箱屬性**

![已佈建雲端式封存之前的信箱屬性](images/Mt791517.d5625bc8-03de-439a-8a0a-051ff537a0bf(EXCHG.150).png "已佈建雲端式封存之前的信箱屬性")

目錄同步處理佈建雲端式封存之前，*ArchiveStatus* 屬性已設定為 `None`，且 *ArchiveState* 屬性已設定為 `HostedPending`。

**目錄同步處理佈建雲端式封存信箱之後的內部部署信箱屬性**

![已佈建雲端式封存之後的信箱屬性](images/Mt791517.9b42d562-1b0a-4722-97aa-35d0ef6f9372(EXCHG.150).png "已佈建雲端式封存之後的信箱屬性")

目錄同步佈建雲端式封存之後， *ArchiveStatus* 屬性會設定為 `Active`， *ArchiveState* 屬性會設定為 `HostedProvisioned`。此時，使用者將能夠在 Outlook 或 網頁型 Outlook 中存取其雲端式封存信箱。

回到頁首

## (選擇性) 執行目錄同步處理

如先前所述，雲端式封存信箱是由目錄同步處理的程序所建立。依預設，您的內部部署 Active Directory 會以每 30 分鐘一次的頻率，與 Office 365 中的 Azure AD 進行同步。您可以移至 Office 365 系統管理中心 中的 \[健康情況\] \> \[目錄同步作業狀態\]，查看上次執行目錄同步的時間。

在某些情況下，您可能想在下次排定的同步作業前開始目錄同步，以佈建雲端式封存信箱。若要這麼做，您可以在安裝 Azure AD Connect 的伺服器上執行下列 PowerShell 命令。

    Start-ADSyncSyncCycle -PolicyType Delta

如需詳細資訊，請參閱 [Azure AD Connect 同步作業：排程器](https://go.microsoft.com/fwlink/p/?linkid=836813)。

回到頁首


---
title: '委派安裝 Exchange 2013 server: Exchange 2013 Help'
TOCTitle: 委派安裝 Exchange 2013 server
ms:assetid: f2fc8680-0c7c-4a29-b8f5-d77404fec280
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201741(v=EXCHG.150)
ms:contentKeyID: 62615189
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 委派安裝 Exchange 2013 server

 

_**適用版本：**Exchange Online, Exchange Server, Exchange Server 2013_

_**上次修改主題的時間：**2014-07-31_

Exchange Server 2013可讓您不Exchange 2013組織管理角色群組之成員的人員委派Exchange伺服器的安裝。這通常是很有幫助大型公司中安裝及設定伺服器的人員其中不相同管理服務，例如Exchange的人員。如果此聲音想要執行的某個項目，本主題會為您。

一般而言， Exchange安裝時，安裝它的人員需要[組織管理](organization-management-exchange-2013-help.md)角色群組的成員。這是因為Exchange安裝時，變更Active Directory，而且只有Exchange 、 身為系統管理員 「 組織管理角色群組的成員，可以進行這些變更。下列清單說明所做的變更：

  - **CN=Servers,CN=Exchange Administrative Group (FYDIBOHF23SPDLT),CN=Administrative Groups,CN=\<Organization Name\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<Root Domain\>**組態磁碟分割中建立伺服器物件。

  - 下列的存取控制項目 (Ace) 會新增至 「 委派安裝 」 角色群組的組態磁碟分割內的伺服器物件：
    
      - 伺服器物件和其子物件完全控制權限
    
      - 拒絕存取控制項目傳送為延伸權利
    
      - 拒絕存取控制項目接收做為延伸權利
    
      - 拒絕 CreateChild 與 DeleteChild 權限的Exchange公用資料夾儲存區物件
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>公用資料夾管理在組織層級;因此，建立與刪除公用資料夾儲存區的僅限於Exchange系統管理員。</td>
    </tr>
    </tbody>
    </table>


  - 伺服器Active Directory電腦帳戶新增至Exchange伺服器群組。

  - 將伺服器新增為Exchange系統管理中心中佈建伺服器。

中大型公司的人員，安裝及設定新的伺服器通常不Exchange系統管理員。若要讓他們能夠安裝Exchange、 Exchange系統管理員可以*佈建*Active Directory中的伺服器。佈建伺服器、 時的所有變更為新的Exchange伺服器運作所需進行Active Directory分別從Exchange的電腦上的實際安裝。Exchange系統管理員可以Active Directory小時\] 或 \[偶數天前新電腦上安裝Exchange中佈建的新伺服器。伺服器之後已佈建、 安裝必須只是要安裝Exchange[委派安裝](delegated-setup-exchange-2013-help.md)角色群組的成員之人員。委派安裝 」 角色群組只允許安裝已佈建的伺服器的成員。

時使用的思考委派安裝，請記住下列：

  - 至少一個Exchange 2013伺服器必須已安裝之前可委派安裝的其他伺服器。安裝第一部伺服器的人員必須能夠Exchange管理員。如需詳細資訊，請參閱[檢查清單： 執行 Exchange 2013 全新安裝](checklist-perform-a-new-installation-of-exchange-2013-exchange-2013-help.md)。

  - 委派的使用者無法解除安裝Exchange伺服器。若要解除安裝Exchange伺服器，您必須Exchange管理員。

## 如何佈建 Exchange 2013 伺服器？

若要佈建Exchange的伺服器，您需要使用Exchange 2013命令列安裝程式。如果您不是非常熟悉Windows命令提示字元處，請不要擔心。本主題將引導您完成完全您需要做些什麼。我們一開始之前，以下是一些謹記下列事項：

  - 您需要佈建伺服器組織管理角色群組的成員。

  - 您應該會有Exchange 2013的最新版本。您可以取得[更新 Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md)下載連結。

您需要使用佈建伺服器的命令會取決於是否要從您正在佈建的電腦執行安裝程式或您是否正在執行它從另一部電腦。選擇此命令中找出您正在執行安裝程式的下列步驟：

1.  按Windows鍵 + 'R' 若要開啟 \[**執行**\] 視窗。

2.  在 \[**開啟**\]，輸入**cmd.exe**，並按 Enter 以開啟**Windows 命令提示字元**。

3.  下載並展開Exchange 2013安裝檔案的位置變更到目錄。如果安裝檔案位於`C:\Downloads\Exchange 2013`，使用下列命令。
    
        CD "C:\Downloads\Exchange 2013"

4.  選擇 \[找出您正在執行安裝程式的命令：
    
      - **如果您正在執行佈建的電腦上的安裝程式**，請執行下列命令：
        
            Setup.exe /NewProvisionedServer /IAcceptExchangeServerLicenseTerms
    
      - **如果您正在執行安裝程式在另一部電腦上的**，執行下列命令：
        
            Setup.exe /NewProvisionedServer:<ComputerName> /IAcceptExchangeServerLicenseTerms

5.  佈建伺服器之後，您需要確定您已新增應該能夠以委派安裝 」 角色群組的佈建伺服器上安裝Exchange的使用者。若要了解如何將使用者新增至角色群組，請參閱[Add members to a role group](manage-role-group-members-exchange-2013-help.md)。

當您完成這些步驟時，電腦將為已準備好用於安裝Exchange 。可以使用[使用安裝精靈安裝 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)中的步驟已佈建伺服器上安裝Exchange 2013 。

## 如何知道這是否正常運作？

若要確定伺服器已正確佈建Exchange，您可以執行下列動作：

1.  移至 \[**開始**\> \[**系統管理工具**\]，並再開啟 \[ **Active Directory 使用者及電腦**。

2.  選取 \[ **Microsoft Exchange Security Groups**、 按兩下 \[ **Exchange 伺服器**\]，然後選取 \[**成員**\] 索引標籤。

3.  在 \[**成員**\] 索引標籤查看您剛佈建的伺服器已列為安全性群組的成員。

如果您的伺服器已列為Exchange伺服器安全性群組的成員，它已正確佈建。某人身為 「 委派安裝 」 角色群組的成員現在可以在該伺服器上安裝Exchange 。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。


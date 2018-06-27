---
title: '至 AD RMS 超級使用者群組新增同盟信箱: Exchange 2013 Help'
TOCTitle: 至 AD RMS 超級使用者群組新增同盟信箱
ms:assetid: 44618df9-54f0-4474-a450-dcba48a02901
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee424431(v=EXCHG.150)
ms:contentKeyID: 50473032
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 至 AD RMS 超級使用者群組新增同盟信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

下列 Microsoft Exchange Server 2013資訊版權管理 (IRM) 功能的啟用，您必須將同盟信箱 （ Exchange 2013安裝程式所建立的系統信箱） 新增至貴組織的[Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx)叢集中的超級使用者群組：

  - Microsoft OfficeOutlook Web App 中的 IRM

  - Exchange ActiveSync中的 IRM

  - 日誌報告解密

  - 傳輸解密

擁有郵件功能的通訊群組可以設定為超級使用者群組中的通訊群組的 AD 您成員會授與擁有者時所要求的授權從 AD RMS 叢集使用授權。這可讓其解密發佈該叢集中的所有與 RMS 受保護的內容。是否使用現有通訊群組或建立通訊群組，以及將它設定為在 AD RMS 超級使用者群組，我們建議您針對此目的而專為通訊群組並設定適當設定核准、 稽核、 及監視成員資格變更。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>設定 AD RMS 超級使用者群組允許解密受 IRM 保護之內容的群組成員。我們建議您以控制及監視群組成員資格採取適當的量值並啟用稽核追蹤成員資格變更。您也可以限制不想要的變更群組成員資格做為受限制的群組使用群組原則設定群組。如需詳細資訊，請參閱 ＜<a href="https://technet.microsoft.com/en-us/library/cc756802(v=ws.10).aspx">受限制的群組原則設定</a>。</td>
</tr>
</tbody>
</table>


若欲瞭解更多與 IRM 相關的管理工作，請參閱 [資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「通訊群組」項目。

  - AD RMS 叢集必須部署於 Active Directory 樹系中。

  - 如果進階使用者群組已在 AD RMS 叢集上執行，通訊群組的成員資格以任何修改可能需要 24 小時的時間以重新整理的 AD RMS 叢集。這是快取叢集中的群組成員資格的結果。

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

## 步驟 1： 使用命令介面將同盟信箱新增至通訊群組

如果建立並設定為在 AD RMS 叢集超級使用者群組的通訊群組，您可以新增Exchange 2013同盟信箱為該群組的成員。如果未設定超級使用者群組，您必須建立通訊群組並新增同盟信箱的成員身分。

1.  建立通訊群組專用做為 AD RMS 超級使用者群組。如需詳細資訊，請參閱[建立並管理通訊群組](create-and-manage-distribution-groups-exchange-2013-help.md)。

2.  將使用者**FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042**新增至新的通訊群組。同盟信箱位於系統信箱與因此在 EAC 中不可見。若要將其新增至通訊群組，您必須使用命令介面從[Add-DistributionGroupMember](https://technet.microsoft.com/zh-tw/library/bb124340\(v=exchg.150\))指令程式。
    
    此範例會將同盟信箱新增至 ADRMSSuperUsers 通訊群組。
    
        Add-DistributionGroupMember ADRMSSuperUsers -Member FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042

如需詳細的語法及參數資訊，請參閱 [Add-DistributionGroupMember](https://technet.microsoft.com/zh-tw/library/bb124340\(v=exchg.150\))。

## 步驟 2： 使用 AD RMS 超級使用者群組設定

AD RMS 叢集上執行下列程序。用來執行此程序的帳戶必須是 AD RMS 伺服器上的 AD RMS Enterprise Administrators 本機群組的成員。

1.  開啟 Active Directory Rights Management Services 主控台並展開 AD RMS 叢集。

2.  在主控台樹狀目錄中展開 \[安全性原則\]，然後按一下 \[超級使用者\]。

3.  在執行窗格中，按一下 \[啟用超級使用者\]。

4.  在結果窗格中，按一下 \[變更超級使用者群組\] 以開啟 \[超級使用者\] 內容頁。

5.  在 \[超級使用者群組\] 方塊中，輸入您在先前程序建立之通訊群組的電子郵件地址，或按一下 \[瀏覽\] 以選取通訊群組。

## 如何才能了解這是否正常運作？

在您將同盟信箱新增至一個新的或現有通訊群組時，請使用 [Get-DistributionGroupMember](https://technet.microsoft.com/zh-tw/library/aa996367\(v=exchg.150\)) 指令程式來檢查群組的會員資格。

如需如何檢查通訊群組成員資格的範例，請參閱 **Get-DistributionGroupMember**中的 [Examples](https://technet.microsoft.com/zh-tw/aa996367\(exchg.150\)#examples)。

使用 AD RMS 超級使用者群組設定後，您可以使用下列方法來確認已正確設定超級使用者群組。此外，您可以使用[Test-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979798\(v=exchg.150\))指令程式來確認 IRM 功能。

  - 使用 AD RMS 主控台來確認是否將群組正確設定為超級使用者群組。

  - 在 AD RMS 伺服器上執行下列 PowerShell 命令來擷取超級使用者群組。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Windows Server 2008 R2 和更新版本上可取得 ADRMSAdmin PowerShell 模組。</td>
    </tr>
    </tbody>
    </table>
    
        Import-Module ADRMSAdmin
        New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost 
        Get-ItemProperty -Path MyRmsAdmin:\SecurityPolicy\SuperUser


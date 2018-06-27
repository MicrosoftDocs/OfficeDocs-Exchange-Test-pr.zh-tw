---
title: '準備使用程式碼範例的跨樹系移動信箱: Exchange 2013 Help'
TOCTitle: 準備使用程式碼範例的跨樹系移動信箱
ms:assetid: f35ac7a5-bb84-4653-b6d0-65906e93627b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee861124(v=EXCHG.150)
ms:contentKeyID: 50474582
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 準備使用程式碼範例的跨樹系移動信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange 2013支援信箱移動和移轉使用**New-MoveRequest**與**New-MigrationBatch** cmdlet。您也可以透過 Exchange 系統管理中心 (EAC) 移動信箱。您可以從來源Exchange樹系信箱移至目標Exchange 2010樹系。

若要執行**New-MoveRequest**，郵件使用者必須存在於目標Exchange樹系中與郵件使用者必須具有一組最小必要的Active Directory屬性。您可以自訂您的 Microsoft Identity Lifecycle Manager (ILM) 2007年部署目標Exchange樹系中建立所需的郵件使用者。本主題所述的是 ILM 型規則延伸模組範例程式碼示範如何將自訂目前 ILM 部署目標Exchange 2013樹系中建立所需擁有郵件功能的使用者。

如需準備跨樹系移動的詳細資訊，包括必要的 Active Directory 屬性的描述，請參閱[準備跨樹系移動要求的信箱](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 從 \[[準備線上信箱移動](https://go.microsoft.com/fwlink/p/?linkid=177882) \] 頁面上的 Microsoft 下載中心下載的範例程式碼。

  - 若要執行的範例程式碼，您需要 ILM 2007 Feature Pack 1 Service Pack 1 (SP1)。若要下載此 feature pack，請參閱 Microsoft 知識庫文章 977791、 [Service Pack 1 （組建 3.3.1139.2） 是可供 Identity 生命週期 Manager 2007 Feature Pack 1](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=977791)。

  - 您還需要下列各項：
    
      - 執行 Exchange 2013 的來源樹系 (信箱目前所在樹系)。
    
      - 已安裝 Exchange 2013 的目標樹系 (信箱移動的目標)。

  - 要連線到Exchange 2013目標樹系，您必須具有適當的權限來呼叫**UpdateRecipient**指令程式。如需您所需的權限，請查看[收件者權限](recipients-permissions-exchange-2013-help.md)主題的 「 收件者佈建權限 」 一節。

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

## 步驟 1： 安裝的是 ILM 範例程式碼

1.  在 Microsoft 的Visual Studio 2008年、 開啟 Microsoft.Exchange.Sample.OneWayGALSync.sln 檢視的範例程式碼。程式碼範例包含下列內容：
    
      - Microsoft.MetadirectoryServicesEx.dll 是隨附於下的是 ILM 2007 FP1 SP1 的二進位檔案"\\Program Files\\Microsoft Identity 整合 Server\\Bin\\Assemblies？。它參照的範例程式碼。
    
      - 範例程式碼會參考 OneWaySync.xml。
    
      - ILMServerConfig 資料夾包含來源管理代理程式 (MA)、目標 MA 及 ILM Metaverse (MV) 的 ILM 組態檔案。
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll 和 Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll （所構成的範例程式碼） 受到"\\obj\\Debug？

2.  在 ILM 伺服器上，將下列內容複製到 \\Program Files\\Microsoft Identity Integration Server\\Extensions：
    
      - OneWaySync.xml
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll

3.  編輯檔案複製至步驟 1 到您要建立郵件使用者的目標Exchange樹系中指定 TargetOU 容器 distinguishedName (DN) 中的 \[ILM 延伸\] 資料夾的 OneWaySync.xml。您可以使用 LDP.exe 或 ADSIEdit.exe 瀏覽 TargetOU 容器如果您不知道其名稱的功能。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果是和 ILM GalSync 2007 一起使用這個範例，請從 GalSync2007 管理的容器清單中排除這個容器。</td>
    </tr>
    </tbody>
    </table>


4.  在 ILM Identity Manager 主控台中，移至 \[**檔案**\> 從資料夾 ILMServerConfig 匯入 ILM 伺服器組態的**匯入伺服器設定**。此巨集指令會匯入 Metaverse 結構描述及佈建的規則以及兩個Active Directory管理代理程式。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在匯入過程中，您必須提供樹系名稱和認證，並比對來源和目標 ADMA 中匯入的 Active Directory 管理代理程式 (ADMA) 的磁碟分割和您的組態中的磁碟分割名稱。</td>
    </tr>
    </tbody>
    </table>


5.  為支援Exchange 2013目標樹系中，在**建立管理代理程式**\] 頁面上**設定延伸模組**\] 窗格中，ADMA 在**佈建的**下拉式清單中選取**Exchange 2013**然後Exchange 2010用戶端存取伺服器遠端 Windows PowerShell URI 中輸入**Exchange 2013 RPS URI**。
    
    **建立管理代理程式頁**
    
    ![管理代理程式 Exchange 2010 佈建](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "管理代理程式 Exchange 2010 佈建")  

6.  在 ILM Identity Manager 主控台上**建立管理代理程式**\] 窗格中，開啟來源樹系的管理代理程式**屬性**。選取 \[**設定目錄磁碟分割**精靈\]，然後按一下 \[選取的容器，將會包含您要移至目標樹系的信箱的**容器**。清除所有的其他容器，亦即範圍只管理此一個容器管理代理程式的選擇。同樣地，目標樹系 MA，選取的容器之擁有郵件功能的使用者在佈建，亦即 TargetOU 步驟 2 中所指定。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果是和 ILM GalSync 2007 一起使用這個範例，請從 GalSync 2007 管理的容器清單中排除這些容器。</td>
    </tr>
    </tbody>
    </table>


7.  在目標 MA 上執行初始完整匯入 (僅限接移)，讓 ILM 找得到在步驟 2 中指定的 TargetOU。

## 步驟 2： 在目標 Exchange 樹系中建立郵件使用者

您已經安裝了範例程式碼，請使用下列程序在目標 Exchange 樹系中建立必要的郵件使用者，以便能夠執行 **New-MoveRequest** 以執行線上信箱移動。

1.  來源樹系中，使用 Exchange 系統管理中心的 \[安裝的是 ILM 範例程式碼\] 步驟 4 中所選取的容器中建立信箱使用者。您也可以使用Active Directory使用者及電腦將現有的信箱使用者移至容器。

2.  執行在來源 MA 上執行的差異匯入與差異同步處理以尋找新增至來源容器的信箱，並將郵件使用者佈建到目標 MA。

3.  在目標 MA 上執行匯出執行，將步驟 1 中佈建的郵件使用者匯出到目標 Active Directory。

4.  在目標 MA 上執行差異匯入，以確認在步驟 2 中匯出的變更。

5.  在目標樹系中開啟 Exchange 管理命令介面，並使用 **New-MoveRequest** 指令程式從來源樹系移動信箱。

## 如何才能了解這是否正常運作？

若要驗證您是否已成功完成遷移，執行下列操作：

  - 在目標樹系中，確認您從來源樹系移動的使用者有出現在目標樹系中。


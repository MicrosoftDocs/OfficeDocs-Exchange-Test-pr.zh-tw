---
title: '匯出及匯入保留標記: Exchange Online Help'
TOCTitle: 匯出及匯入保留標記
ms:assetid: 18405ea2-7ccc-475e-bd84-8b040e17bf44
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ907307(v=EXCHG.150)
ms:contentKeyID: 51409159
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 匯出及匯入保留標記

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2017-11-15_

在以下數個案例中，您可能想要匯出或匯入保留標記：

  - 跨多樹系Exchange組織中所有伺服器套用相同保留原則

  - 在混合部署中套用相同的保留原則，其中有些信箱在您的內部部署 Exchange 組織中，有些在 Exchange Online 中。

  - 套用Exchange封存案例，其中具有內部Exchange 2010或更新版本的信箱使用者會具有雲端式封存中的保留原則。

在這些案例中，受管理的資料夾助理員可在某個項目或信箱移到另一個組織時，正確地處理套用保留標記的項目。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要讓兩個組織之間的保留標記和保留原則維持同步，在每次變更來源組織中的保留標記或原則時，您必須執行這個程序，從來源組織匯出保留標記和原則，以及將它們匯入到目的組織。<br />
您不能選取特定的保留標記] 或 [要匯出的原則。匯出 RetentionTags.ps1 指令碼會從組織匯出所有的保留標記和原則。</td>
</tr>
</tbody>
</table>


如需與通訊記錄管理相關的其他管理工作，請參閱[通訊記錄管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「郵件記錄管理」項目。

  - 本主題中的程序取決於下列三個資料夾中的檔案`%ExchangeInstallPath%Scripts`Exchange伺服器上：
    
      - Export-RetentionTags.ps1
    
      - Import-RetentionTags.ps1
    
      - MigrateRetentionTags.strings.psd1

  - 您不能選取特定的保留標記\] 或 \[匯出或匯入的原則。匯出 RetentionTags.ps1 指令碼會從組織匯出所有的保留標記和原則。匯入 RetentionTags.ps1 指令碼會匯入所有的保留標記和原則中之 XML 檔案所匯入、 取代所有現有的保留標記和Exchange組織中的原則。

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


## 步驟 1： 匯出內部部署 Exchange 組織中的保留標記

1.  執行此Exchange 管理命令介面命令，以將目錄變更為您Exchange安裝路徑中的**指令碼**子目錄。
    
        Cd $Env:ExchangeInstallPath\Scripts

2.  執行 Export-RetentionTags.ps1 指令碼，將保留標記匯出至 XML 檔案。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您正在匯入或匯出至Exchange Online的保留標記和保留原則，您必須連線 Windows PowerShell 工作階段到Exchange Online。如需詳細資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/jj984289(v=exchg.150)">使用遠端 PowerShell 連線到 Exchange Online</a>。</td>
    </tr>
    </tbody>
    </table>
    
        .\Export-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"

## 如何才能了解這是否正常運作？

若要確認您是否已成功匯出保留標記和保留原則，請執行下列動作：

1.  瀏覽至您在要匯出的命令中指定的路徑，並確認是否已建立具有所指定名稱的 XML 檔案。

2.  您可以選擇性地利用文字編輯器來開啟 XML 檔案，以檢閱其內容。

## 步驟 2： 匯入至 Exchange 組織的保留標記

1.  執行此Exchange 管理命令介面命令，以將目錄變更為您Exchange安裝路徑中的**指令碼**子目錄。
    
        Cd $Env:ExchangeInstallPath\Scripts

2.  執行 Import-RetentionTags.ps1 指令碼，從先前匯出的 XML 檔案中匯入保留標記。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您正在匯入或匯出至Exchange Online的保留標記和保留原則，您必須連線 Windows PowerShell 工作階段到Exchange Online。如需詳細資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/jj984289(v=exchg.150)">使用遠端 PowerShell 連線到 Exchange Online</a>。</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>執行此指令碼針對Exchange Online、 時可能會提示您確認您想要執行軟體來自不受信任的發行者。確認發行者的名稱顯示為 [ <code>CN=Microsoft Corporation, OU=MOPR, O=Microsoft Corporation, L=Redmond, S=Washington, C=US</code>、] 和 [ <strong>R</strong>允許一次執行指令碼或<strong>A</strong>到一定會執行。</td>
    </tr>
    </tbody>
    </table>
    
        .\Import-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"

## 如何才能了解這是否正常運作？

若要確認您是否已成功匯入保留標記和保留原則，請執行下列動作：

1.  在 EAC 中，瀏覽至 \[**相符性管理**\>**保留標記**，並確認已成功匯保留標記。瀏覽至 \[**相符性管理**\>**保留原則**，並確認已成功匯保留原則。

2.  若要確認已建立的標記及原則使用**Get-RetentionPolicy**和**Get-RetentionPolicyTag**指令程式。如需有關如何擷取保留標記和保留原則的範例，請參閱範例[Get-RetentionPolicyTag](https://technet.microsoft.com/zh-tw/library/dd298009\(v=exchg.150\))和[Get-RetentionPolicy](https://technet.microsoft.com/zh-tw/library/dd298086\(v=exchg.150\))中。


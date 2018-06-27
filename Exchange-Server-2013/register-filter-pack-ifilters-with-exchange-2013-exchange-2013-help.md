---
title: '對 Exchange 2013 註冊 Filter Pack IFilter: Exchange 2013 Help'
TOCTitle: 對 Exchange 2013 註冊 Filter Pack IFilter
ms:assetid: 0338980f-3a64-49d3-bc3c-bf6f10f88cb4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ837174(v=EXCHG.150)
ms:contentKeyID: 50553927
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 對 Exchange 2013 註冊 Filter Pack IFilter

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

含有附件掃描條件的傳輸規則會在分析附件內容時執行文字擷取。Exchange 2013 可掃描最常用的原生附件類型。透過使用 Exchange 2013 註冊 IFilter，可納入其他附件類型。本主題顯示如何註冊由 Microsoft 和協力廠商提供者所發行的 IFilter。

在您註冊特定檔案類型的 IFilter 之後，含有附件處理條件的傳輸規則將可以掃描這些附件。因此，這些檔案類型將不再觸發 *AttachmentIsUnsupported* 條件。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題所列出的程序涵蓋在 Exchange Server 上修改登錄。不正確編輯登錄會造成嚴重問題，可能需要重新安裝作業系統。如因不正確編輯登錄造成任何問題，這些問題可能無法解決。編輯登錄前請先備份所有珍貴資料。<br />
這些程序還需要您在您的信箱伺服器上停止並重新啟動 Microsoft Exchange Transport 服務。</td>
</tr>
</tbody>
</table>


如需與傳輸規則相關的其他管理工作，請參閱[管理郵件流程規則](manage-mail-flow-rules-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：每部伺服器 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的「Exchange Server 組態設定」項目。

  - 您必須在已安裝 Exchange 2013 Mailbox server role 的伺服器上執行下列程序。如果您在執行這些程序後新增信箱伺服器，您必須在新佈建的伺服器上再次執行這些程序。

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


## 您要執行的工作

## 註冊 Microsoft Office 2010 Filter Pack

依預設，Exchange 傳輸規則不支援下列 Office 檔案類型：

  - Office OneNote

  - Office Publisher

如果您想支援這些檔案，必須部署 Microsoft Office 2010 Filter Pack。此 Filter Pack 未在 Exchange 2013 安裝時部署，它不是部署的必要條件。

## 部署 Microsoft Office 2010 Filter Pack

部署 Office 2010 Filter Pack 由兩大步驟組成：

  - 下載和安裝 Filter Pack，使用 Windows (搜尋) 註冊 IFilter。

  - 修改註冊，以便使用 Exchange 2013 註冊 Ifilter。這將允許 Exchange 支援檔案格式的附件掃描。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須在組織中所有的信箱伺服器上執行此程序。</td>
</tr>
</tbody>
</table>


1.  下載並從[Microsoft 下載中心](https://go.microsoft.com/fwlink/?linkid=191548)儲存 Microsoft Office 2010 Filter Pack (`FilterPack64bit.exe`)。

2.  在您的信箱伺服器上執行 `FilterPack64bit.exe` 檔案，並遵循指示完成安裝。

3.  啟動登錄編輯程式，並尋找下列登錄子機碼：
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID

4.  在 \[CLSID\] 底下新增 OneNote 檔案的子機碼，如下所示：
    
    1.  在 \[CLSID\] 上按一下滑鼠右鍵，指向 \[新增\]，然後按一下 \[機碼\]。
    
    2.  將新機碼的名稱變更為 `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`。
    
    3.  按一下剛才建立的機碼並設定安裝 Office 2010 Filter Pack 的 \[(預設)\] 值。依預設，Filter Pack 會安裝在 `C:\Program Files\Common Files\Microsoft Shared\Filters\ONIFilter.dll`。
    
    4.  以滑鼠右鍵按一下 \[{B8D12492-CE0F-40AD-83EA-099A03D493F1}\]，指向 \[新增\]，再按一下 \[字串值\]。
    
    5.  命名新字串值 `ThreadingModel` 並設定為 `Both`。

5.  在 \[CLSID\] 底下新增 Publisher 檔案的子機碼，如下所示：
    
    1.  在 \[CLSID\] 上按一下滑鼠右鍵，指向 \[新增\]，然後按一下 \[機碼\]。
    
    2.  將新機碼的名稱變更為 `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`。
    
    3.  按一下剛才建立的機碼並設定安裝 Office 2010 Filter Pack 的 \[(預設)\] 值。依預設，Filter Pack 會安裝在 `C:\Program Files\Common Files\Microsoft Shared\Filters\PUBFILT.dll`。
    
    4.  以滑鼠右鍵按一下 \[{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}\]，指向 \[新增\]，然後按一下 \[字串值\]。
    
    5.  命名新字串值 `ThreadingModel` 並設定為 `Both`。

6.  找到下列登錄機碼：
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters

7.  在 \[篩選器\] 底下新增 .one 副檔名的子機碼，如下所示。
    
    1.  在 \[篩選器\] 上按一下滑鼠右鍵，指向 \[新增\]，然後按一下 \[機碼\]。
    
    2.  將新機碼的名稱變更為 `.one`。
    
    3.  按一下剛才建立的機碼並設定 \[(預設)\] 值為 `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`。

8.  在 \[篩選器\] 底下新增 .pub 副檔名的子機碼，如下所示：
    
    1.  在 \[篩選器\] 上按一下滑鼠右鍵，指向 \[新增\]，然後按一下 \[機碼\]。
    
    2.  將新機碼的名稱變更為 `.pub`。
    
    3.  按一下剛才建立的機碼並設定 \[(預設)\] 值為 `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`。

9.  關閉登錄編輯程式。

10. 在信箱伺服器上，以指定的順序先停止再重新啟動下列服務：
    
    1.  停止 Microsoft Exchange Transport 服務。
    
    2.  停止 Microsoft 篩選管理服務。
    
    3.  啟動 Microsoft 篩選管理服務。
    
    4.  啟動 Microsoft Exchange 傳輸服務。

## 如何知道這是否正常運作？

若要確認是否已成功註冊 Microsoft Office 2010 Filter Pack IFilter，請執行下列動作：

1.  建立具有下列內容的傳輸規則。如需如何建立傳輸規則的詳細指示，請參閱[管理郵件流程規則](manage-mail-flow-rules-exchange-2013-help.md)。
    
      - 寄件者是您的信箱。
    
      - 任何附件的內容包含「測試 IFilter」。
    
      - 產生事件報告並將它傳送至您的信箱。

2.  建立含有「測試 IFilter」片語的 OneNote 檔案，並將它附加至新的電子郵件訊息，然後傳送給您自己。

3.  針對剛才建立的規則，確認您收到傳輸規則事件報告。這可確認規則引擎能夠分析 OneNote 檔案的內容。

4.  搭配 Publisher 檔案重複步驟 2 和 3。

## 註冊協力廠商 IFilter 以支援其他檔案格式

您可以註冊其他協力廠商 IFilter，擴充其他檔案類型的附件掃描功能。在每一部信箱伺服器上安裝並註冊檔案類型的 IFilter，可新增其他檔案支援。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Microsoft 尚未使用傳輸規則測試協力廠商 IFilter，因此建議您先在測試環境中部署和測試任何協力廠商 IFilter，再部署至實際執行環境。</td>
</tr>
</tbody>
</table>


## 部署 Adobe PDF IFilter

此程序將示範如何部署[Adobe PDF IFilter](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025)傳輸規則中支援的 PDF 附件處理。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013 預設會支援傳輸規則中的 PDF 檔案掃描。簡單使用此處的 PDF 範例，說明您可以如何使用協力廠商 IFilter 來擴充支援其他檔案類型。</td>
</tr>
</tbody>
</table>


1.  下載[Adobe PDF IFilter](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025)與然後按照安裝指示。

2.  啟動登錄編輯程式，並尋找下列子機碼：
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID

3.  在 \[CLSID\] 底下新增 PDF 檔案的子機碼，如下所示：
    
    1.  在 \[CLSID\] 上按一下滑鼠右鍵，指向 \[新增\]，然後按一下 \[機碼\]。
    
    2.  將新機碼的名稱變更為 `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>每一個 IFilter 都具有唯一的類別識別碼 (CLSID)。您可以在安裝文件中找到您註冊的 IFilter 的 CLSID，或在登錄的 <code>HKEY_CLASSES_ROOT\CLSID</code> 機碼底下搜尋副檔名。</td>
        </tr>
        </tbody>
        </table>
    
    3.  按一下剛才建立的機碼並設定安裝 PDF IFilter 的 \[(預設)\] 值。依預設，PDF IFilter 會安裝在 `C:\Program Files\Adobe\Adobe PDF IFilter 9 for 64-bit platforms\bin\PDFFilter.dll`。

4.  找到下列登錄機碼：
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters

5.  在 \[篩選器\] 底下新增 .pdf 副檔名的子機碼，如下所示：
    
    1.  在 \[篩選器\] 上按一下滑鼠右鍵，指向 \[新增\]，然後按一下 \[機碼\]。
    
    2.  將新機碼的名稱變更為 `.pdf`。
    
    3.  按一下剛才建立的機碼並設定 \[(預設)\] 值為 `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`。

6.  關閉登錄編輯程式。

7.  在信箱伺服器上，以指定的順序先停止再重新啟動下列服務：
    
    1.  停止 Microsoft Exchange Transport 服務。
    
    2.  停止 Microsoft 篩選管理服務。
    
    3.  啟動 Microsoft 篩選管理服務。
    
    4.  啟動 Microsoft Exchange 傳輸服務。

## 如何知道這是否正常運作？

使用此主題稍早How do you know this worked?章節中所列出的相同程序，以 Adobe PDF 檔案替代 Publisher 檔案。

## 相關資訊

[使用傳輸規則檢查郵件附件](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[傳輸規則條件 （述詞）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[傳輸規則動作](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)


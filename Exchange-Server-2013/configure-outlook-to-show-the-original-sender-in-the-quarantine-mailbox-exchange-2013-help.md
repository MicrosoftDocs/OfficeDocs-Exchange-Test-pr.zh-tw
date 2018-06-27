---
title: '將 Outlook 設定為顯示隔離信箱中的原始寄件者: Exchange 2013 Help'
TOCTitle: 將 Outlook 設定為顯示隔離信箱中的原始寄件者
ms:assetid: 9249425d-1b06-48a0-ad95-c4eefb641ff4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee861109(v=EXCHG.150)
ms:contentKeyID: 50473759
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將 Outlook 設定為顯示隔離信箱中的原始寄件者

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

垃圾郵件隔離是內容篩選器代理程式的功能，可以降低遺失合法郵件的風險。垃圾郵件隔離提供暫時儲存位置，用來存放識別為垃圾郵件以及不應該傳遞至組織內使用者信箱的郵件。

當郵件達到垃圾郵件隔離閾值，就會包裝在未傳遞回報 (NDR) 中，並傳遞至垃圾郵件隔離信箱。因為隔離的郵件是以 NDR 形式儲存在隔離信箱中，所以會將組織的郵件管理員地址列為所有郵件的 \[寄件者:\] 地址。不過，如果欄位清單中有原始寄件者地址、原始收件者地址和原始垃圾郵件信賴等級 (SCL)，找出您要復原的郵件就會比較容易。

預設情況下，您不能在 Microsoft Outlook 中選擇這些欄位。在您可以將這些欄位新增到郵件檢視前，您必須先建立可以將原始寄件者、原始收信者和原始 SCL 作為選用欄位新增的 Outlook 表單。建立此自訂表單後，您可設定 Outlook 在郵件檢視中顯示這些欄位。

## 開始之前有哪些須知？

  - 此程序預估完成時間：15 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「信箱存取」項目。

  - 此程序會要求您先設定反垃圾郵件隔離信箱。如需詳細資訊，請參閱[設定垃圾郵件隔離信箱](configure-a-spam-quarantine-mailbox-exchange-2013-help.md)。

  - 若要存取隔離信箱，您需要設定該信箱的 Outlook 設定檔及再開啟 \[使用 Outlook 信箱。如需設定和使用多個 Outlook 設定檔的詳細資訊，請參閱[概觀 （英文) 的 Outlook 電子郵件設定檔](https://go.microsoft.com/fwlink/p/?linkid=178975)。

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

## 步驟 1：使用 \[記事本\] 建立一個自訂的 Outlook 表單

1.  打開 \[記事本\]，並將下面的代碼複製到文件中。
    
        [Description]
        MessageClass=IPM.Note
        CLSID={00020D31-0000-0000-C000-000000000046}
        DisplayName=Quarantine Extension Form
        Category=Standard
        Subcategory=Form
        Comment=This form allows the Original Sender (ReceivedRepresentingEmailAddress), Original Recipient (To), and Original SCL (OriginalScl) values to be viewed as columns.
        LargeIcon=IPML.ico
        SmallIcon=IPMS.ico
        Version=3.0
        Locale=enu
        Hidden=1
        Owner=Microsoft Corporation
        Contact=Your Name
        
        [Platforms]
        Platform1=Win16
        Platform2=NTx86
        Platform9=Win95
        
        [Platform.Win16]
        CPU=ix86
        OSVersion=Win3.1
        
        [Platform.NTx86]
        CPU=ix86
        OSVersion=WinNT3.5
        
        [Platform.Win95]
        CPU=ix86
        OSVersion=Win95
        
        [Properties]
        Property01=ReceivedRepresentingEmailAddress
        Property02=DisplayTo
        Property03=OriginalScl
        
        [Property.ReceivedRepresentingEmailAddress]
        Type=31
        NmidInteger=0x0078
        DisplayName=ReceivedRepresentingEmailAddress
        
        [Property.DisplayTo]
        Type=31
        NmidInteger=0x0E04
        DisplayName=DisplayTo
        
        [Property.OriginalScl]
        Type=3
        NmidPropset={41F28F13-83F4-4114-A584-EEDB5A6B0BFF}
        NmidString=OriginalScl
        DisplayName=OriginalScl
        
        [Verbs]
        Verb1=1
        
        [Verb.1]
        DisplayName=&Open
        Code=0
        Flags=0
        Attribs=2
        
        [Extensions]
        Extensions1=1
        
        [Extension.1]
        Type=31
        NmidPropset={00020D0C-0000-0000-C000-000000000046}
        NmidInteger=1
        Value=1000000000000000

2.  使用以下的值將檔案儲存在您的 Office 表單資料夾中：
    
      - **路徑**   *\<Office 安裝路徑\>*\\\<*OfficeVersion\>*\\Forms\\*\<LCID\>*
        
          - *\<Office 安裝路徑\>*   對於在 32 位元版 Microsoft Windows 中執行的 32 位元版 Office，或在 64 位元版 Microsoft Windows 中執行的 64 位元版 Office，預設路徑為 `C:\Program Files\Microsoft Office`。對於在 64 位元版 Microsoft Windows 中執行的 32 位元版 Office，預設路徑為 `C:\Program Files (x86)\Microsoft Office`。
        
          - *\<OfficeVersion\>*   對於 Outlook 2007，此值為 `Office12`。若是 Outlook 2010，值為 `Office14`。若是 Outlook 2013，值為 `Office15`。
        
          - *\<LCID\>*   這是您的地區識別碼 (LCID) 值。例如，美式英文的 LCID 為 1033。如需更多資訊，請參閱 [KB221435：在 Word 中支援的地區識別碼清單](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=221435)。
    
      - **名稱**   對於此程序其餘部分，請假定檔案名為 `QTNE.cfg`。檔案的名稱並不重要，但務必在該值加上括弧，以便可以 QTNE.cfg 而不是 QTNE.cfg.txt 儲存檔案。
    
    例如，對於安裝在 64 位元版 Windows 中的 32 位元美式英文版的 Outlook 2013，將檔案儲存為：
    
        "C:\Program Files (x86)\Microsoft Office\Office15\Forms\1033\QTNE.cfg"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果 Windows 使用者存取控制 (UAC) 會防止您儲存檔案中的正確位置，先儲存至暫時的位置，並加以複製。</td>
    </tr>
    </tbody>
    </table>


## 步驟 2：設定 Outlook 以使用自訂的 Outlook 表單

根據您電腦上安裝的 Outlook 版本，使用以下其中一個程序。

## 設定 Outlook 2010 或 Outlook 2013

1.  在 Outlook 2010 或 Outlook 2013 中，按一下 \[檔案\] \> \[選項\] \> \[進階\]。

2.  在 \[開發商\] 區段中，按一下\[自訂表單\]。

3.  在 \[選項\] 對話方塊中按一下 \[管理表單\]。

4.  在 \[**表單管理員**\] 對話方塊中，按一下 \[**安裝**\]。瀏覽至`QTNE.cfg`檔案的位置、 選取它，並按一下 \[**開啟\]**。在**表單內容**\] 對話方塊中，檢閱資訊，並再按一下 \[將安裝在個人表單檔案庫中的 \[隔離擴充表單的**\[確定\]** 。

5.  在 \[表單管理員\] 對話方塊中按一下 \[關閉\]。按兩下 **\[確定\]** 以關閉其餘對話方塊並回到 Outlook 主介面。

6.  在收件匣 **\[郵件\]** 檢視的 **\[首頁\]** 索引標籤上，用滑鼠右鍵按一下欄位標題列 (可能需要擴大郵件清單的寬度才能看到欄位)，然後選取 **\[檢視設定\]**。

7.  在 \[進階檢視設定\] 對話方塊中，按一下 \[欄位\]。

8.  捲動到 \[顯示欄\] 對話方塊中的 \[選擇可用欄\] 下拉式清單的最下面，然後選擇 \[表單\]。

9.  在 \[請對此資料夾選取企業表單\] 對話方塊的 \[選取的表單\] 欄位中，選取 \[郵件\] 並按一下 \[移除\]。在 \[個人表單\] 欄位中選取 \[隔離擴充表單\]，然後按一下 \[新增\]。完成後，按一下 \[關閉\]。

10. 在 \[顯示欄\] 對話方塊的 \[可用欄位\] 區段中，選取以下列一或多個欄位，並於選取每一個欄位後按一下 \[新增\]：
    
      - **ReceivedRepresentingEmailAddress**   原始寄件者
    
      - **DisplayTo**  原始收件者 （請注意，這會顯示為**以**之後將其新增）
    
      - **OriginalScl**   原始 SCL
    
    使用 \[**移動**\] 或 \[**下移**\] 按鈕欄在檢視中。為了獲得最佳結果之後 \[**附件**\] 欄位中,，並**從**欄位之前的位置三個新的欄位。完成時，按一下 \[按兩次返回主要Outlook介面的**\[確定\]** 。

## 設定 Outlook 2007

1.  在 Outlook 2007 中，按一下 \[工具\] \> \[選項\]。

2.  在 \[選項\] 對話方塊中按一下 \[其他\] 索引標籤，然後按一下 \[一般\] 下的 \[進階選項\]。

3.  在 \[進階選項\] 對話方塊中按一下 \[自訂表單\]，然後按一下 \[自訂表單\] 對話方塊中的 \[管理表單\]。

4.  在 \[**表單管理員**\] 對話方塊中，按一下 \[**安裝**\]。瀏覽至`QTNE.cfg`檔案的位置、 選取它，並按一下 \[**開啟\]**。在**表單內容**\] 對話方塊中，檢閱資訊，並再按一下 \[將安裝在個人表單檔案庫中的 \[隔離擴充表單的**\[確定\]** 。

5.  關閉 \[**表單管理員**\] 對話方塊，然後按三次**\[確定\]**關閉其餘對話方塊並返回主要Outlook 2007介面。

6.  在**郵件**檢視中的收件匣，以滑鼠右鍵按一下 \[欄標題\] 資料列 （您可能需要展開郵件清單以查看資料行的寬度），然後選取**自訂目前檢視。**

7.  在**自訂檢視： 訊息**對話方塊\] 方塊中，按一下 \[**顯示欄位**。

8.  在 \[**顯示欄位**\] 對話方塊中**選取 \[可用欄位**\] 下拉式清單中，捲動到清單結尾並選取 \[**表單**\]。

9.  在 \[請對此資料夾選取企業表單\] 對話方塊的 \[選取的表單\] 欄位中，選取 \[郵件\] 並按一下 \[移除\]。在 \[個人表單\] 欄位中選取 \[隔離擴充表單\]，然後按一下 \[新增\]。完成後，按一下 \[關閉\]。

10. 在 \[**顯示欄位**\] 對話方塊的 \[**可用欄位**\] 區段中選取一或多個下列欄位並選取每一個欄位後按一下 \[**新增\]** 。
    
      - **ReceivedRepresentingEmailAddress**   原始寄件者
    
      - **DisplayTo**  原始收件者 （請注意，這會顯示為**以**之後將其新增）
    
      - **OriginalScl**   原始 SCL
    
    使用 \[**移動**\] 或 \[**下移**\] 按鈕欄在檢視中。為了獲得最佳結果之後 \[**附件**\] 欄位中,，並**從**欄位之前的位置三個新的欄位。完成時，按一下 \[按兩次返回主要Outlook 2007介面的**\[確定\]** 。

## 如何才能了解這是否正常運作？

如果您使用 Outlook 時在垃圾郵件隔離信箱中看見隔離郵件的原始寄件者、原始收件者或原始 SCL 值，此程序可解決您的問題。


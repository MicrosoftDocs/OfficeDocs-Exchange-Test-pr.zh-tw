---
title: '匯出信箱稽核記錄: Exchange Online Help'
TOCTitle: 匯出信箱稽核記錄
ms:assetid: b458a95a-3321-4647-8884-cf97f8e7186a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150552(v=EXCHG.150)
ms:contentKeyID: 50472413
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 匯出信箱稽核記錄

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

如果信箱已啟用信箱稽核，每當擁有者以外的使用者存取信箱時，Microsoft Exchange 就會在*「信箱稽核記錄」*中記錄相關資訊。每個記錄項目都包括下列相關資訊：存取信箱的人員和時間、非擁有者所執行的動作，以及動作是否成功完成。信箱稽核記錄預設會保留在信箱中 90 天。您可以使用信箱稽核記錄來判斷是否擁有者以外的使用者存取了信箱。

當您從信箱稽核記錄中匯出項目時，Microsoft Exchange 會將這些項目儲存在 XML 檔案中，然後附加到傳送至指定收件者的電子郵件。

**目錄**

開始之前

設定信箱稽核記錄

匯出信箱稽核記錄

檢視信箱稽核記錄

其他資訊

## 開始之前

  - 每項程序的預估完成時間：時間是變數。在 Exchange Online 中，信箱稽核記錄會在您匯出之後的幾天內傳送。

  - 在Exchange Online，您必須使用遠端 Windows PowerShell 來執行許多程序本主題中。如需詳細資訊，請參閱[使用遠端 PowerShell 連線到 Exchange Online](https://technet.microsoft.com/zh-tw/library/jj984289\(v=exchg.150\))。

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 設定信箱稽核記錄

您必須針對想要稽核的每一個信箱啟用信箱稽核記錄，然後才可以匯出及檢視信箱稽核記錄。您還必須設定 Microsoft Outlook Web App 允許 XML 附件使用 Outlook Web App 存取稽核記錄。

## 步驟 1：啟用信箱稽核記錄

您必須針對想要執行非擁有者信箱存取報告的每個信箱啟用信箱稽核記錄。如果未針對信箱啟用信箱稽核記錄，當您匯出信箱稽核記錄時，就不會得到該信箱的任何結果。

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「信箱稽核記錄」項目。

若要針對單一信箱啟用信箱稽核記錄，請在命令介面中執行命令。

    Set-Mailbox <Identity> -AuditEnabled $true

若要針對組織內的所有使用者信箱啟用信箱稽核記錄，請執行下列命令。

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}

    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

## 步驟 2：設定 Outlook Web App 允許 XML 附件

當您匯出信箱稽核記錄時，Microsoft Exchange 會將稽核記錄 (也就是 XML 檔案) 附加到電子郵件。但是，Outlook Web App 預設會封鎖 XML 附件。若要存取匯出的稽核記錄，您必須使用 Microsoft Outlook 或設定 Outlook Web App 允許 XML 附件。

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「Outlook Web App 信箱原則」項目。

請執行下列程序在Outlook Web App中允許 XML 附件。在Exchange Server 2013，使用值`Default`*Identity*參數。

1.  執行下列命令以將 XML 新增至允許的Outlook Web App中的檔案類型清單。
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -AllowedFileTypes @{add='.xml'}

2.  執行下列命令以移除Outlook Web App中封鎖的檔案類型清單中的 XML。
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -BlockedFileTypes @{remove='.xml'}

## 如何知道這是否正常運作？

若要確認是否已成功設定信箱稽核記錄，請執行下列操作：

1.  執行下列命令，確認已設定信箱的稽核記錄。
    
        Get-Mailbox | FL Name,AuditEnabled
    
    已啟用提供驗證 *AuditEnabled* 屬性信箱稽核記錄的 `True` 值。

2.  執行下列命令來確認Outlook Web App中允許 XML 附件。
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty AllowedFileTypes
    
    確認 `.xml` 包含在允許的檔案類型清單中。

3.  執行下列命令來確認已從Outlook Web App中封鎖的檔案清單中移除 XML 附件。
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty BlockedFileTypes
    
    確認該`.xml`不包含在封鎖的檔案類型清單中。

回到頁首

## 匯出信箱稽核記錄

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的「僅檢視系統管理員稽核記錄」項目。

1.  在 Exchange 系統管理中心 (EAC) 中，移至 \[**相符性管理**\>**稽核**。

2.  按一下 \[匯出信箱稽核記錄\]。

3.  設定下列搜尋準則，匯出信箱稽核記錄中的項目：
    
      - **開始和結束日期：**選取要併入匯出檔案中之項目的日期範圍。
    
      - **要搜尋稽核記錄的信箱：**選取要擷取稽核記錄項目的信箱。
    
      - **非擁有者存取的類型：**選取下列其中一個選項來定義要擷取項目的非擁有者存取類型：
        
          - **所有非擁有者**   搜尋組織內的系統管理員和委派的使用者以及 Exchange Online 中 Microsoft 資料中心系統管理員的存取。
        
          - **外部使用者**：搜尋 Microsoft 資料中心系統管理員的存取。
        
          - **系統管理員和委派的使用者**：搜尋組織內的系統管理員和委派的使用者的存取。
        
          - **系統管理員**：搜尋組織內系統管理員的存取。
    
      - **收件者：**選取要將信箱稽核記錄傳送給哪些使用者。

4.  按一下 \[匯出\]。
    
    Microsoft Exchange 會擷取信箱稽核記錄中符合您搜尋準則的項目，並將這些項目儲存在名為 SearchResult.xml 的檔案中，然後在送給指定之收件者的電子郵件中附加這個 XML 檔案。

## 如何知道這是否正常運作？

登入已的傳送信箱稽核記錄。如果您已成功匯出稽核記錄，您會收到從 Exchange 傳送的訊息。在Exchange Online，可能需要幾天內收到此訊息。信箱稽核記錄 （名為 SearchResult.xml） 會附加到此訊息。如果您已正確設定 Outlook Web App 允許 XML 附件，您可以下載附加的 XML 檔案。

回到頁首

## 檢視信箱稽核記錄

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的「僅檢視系統管理員稽核記錄」項目。

若要將儲存並檢視 SearchResult.xml 檔案：

1.  登入已傳送信箱稽核記錄的信箱。

2.  在收件匣中，開啟含有 Microsoft Exchange 傳送之 XML 檔案附件的郵件。請注意，電子郵件的內文包含了搜尋準則。

3.  按一下附件並選取要下載的 XML 檔案。

4.  在 Microsoft Excel 中開啟 SearchResult.xml。

回到頁首

## 其他資訊

  - **稽核記錄的信箱中的項目**  下列範例會顯示從信箱稽核記錄 SearchResult.xml 檔案中所包含的項目。每個項目加上**\< 事件 \>** XML 標記並結束於**\< / 事件 \>** XML 標記。此項目顯示的系統管理員將清除郵件主旨，「**通知的訴訟保留**」 從 David 的信箱中的 \[可復原的項目\] 資料夾上 2010 年 4 月 30 日。
    
        <Event MailboxGuid="6d4fbdae-e3ae-4530-8d0b-f62a14687939" 
          Owner="PPLNSL-dom\david50001-1363917750" 
          LastAccessed="2010-04-30T11:01:55.140625-07:00" 
          Operation="HardDelete" 
          OperationResult="Succeeded" 
          LogonType="Admin"
         FolderId="0000000073098C3277988F4CB882F5B82EBF64610100A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000"
          FolderPathName="\Recoverable Items\Deletions"
          ClientInfoString="Client=OWA;Action=ViaProxy" 
          ClientIPAddress="10.196.241.168" 
          InternalLogonType="Owner"
          MailboxOwnerUPN="david@contoso.com"
          MailboxOwnerSid="S-1-5-21-290112810-296651436-1966561949-1151" 
          CrossMailboxOperation="false" 
          LogonUserDN="Administrator"
          LogonUserSid="S-1-5-21-290112810-296651436-1966561949-1149">
          <SourceItems>
           <ItemId="0000000073098C3277988F4CB882F5B82EBF64610700A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000A7C317F68C24304BBD18ABE1F185E79B00000026BD540"
            Subject="Notification of litigation hold"
            FolderPathName="\Recoverable Items\Deletions" /> 
          </SourceItems>
        </Event>

  - **稽核記錄的信箱中的實用欄位**  以下是在信箱稽核記錄中的實用欄位的描述。它們可協助您識別信箱的非擁有者存取權的每個執行個體的特定資訊。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>欄位</th>
    <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Owner</strong></p></td>
    <td><p>非擁有者存取之信箱的擁有者。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>LastAccessed</strong></p></td>
    <td><p>存取信箱的日期和時間。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Operation</strong></p></td>
    <td><p>非擁有者執行的動作。如需詳細資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/jj156300(v=exchg.150)">深入了解執行非擁有者信箱存取報告</a>中的＜哪些內容會記錄在信箱稽核記錄中？＞一節。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OperationResult</strong></p></td>
    <td><p>非擁有者執行的動作成功還是失敗。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonType</strong></p></td>
    <td><p>非擁有者的存取類型。其中包括系統管理員、代理人和外部人員。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>FolderPathName</strong></p></td>
    <td><p>資料夾的名稱，其中包含受到非擁有者所影響的郵件。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>ClientInfoString</strong></p></td>
    <td><p>有關非擁有者存取信箱所使用之郵件用戶端的資訊。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ClientIPAddress</strong></p></td>
    <td><p>非擁有者存取信箱所使用之電腦的 IP 位址。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>InternalLogonType</strong></p></td>
    <td><p>非擁有者存取這個信箱所使用之帳戶的登入類型。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>MailboxOwnerUPN</strong></p></td>
    <td><p>信箱擁有者的電子郵件地址。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonUserDN</strong></p></td>
    <td><p>非擁有者的顯示名稱。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Subject</strong></p></td>
    <td><p>受到非擁有者所影響之電子郵件的主旨行。</p></td>
    </tr>
    </tbody>
    </table>
    
    回到頁首


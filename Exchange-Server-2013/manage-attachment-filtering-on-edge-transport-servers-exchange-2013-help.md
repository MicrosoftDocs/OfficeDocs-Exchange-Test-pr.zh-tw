---
title: '管理 Edge Transport server 上的附件篩選: Exchange 2013 Help'
TOCTitle: 管理 Edge Transport server 上的附件篩選
ms:assetid: 2ec91cc6-6ade-48ee-88bb-66153874393d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997139(v=EXCHG.150)
ms:contentKeyID: 60828710
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理 Edge Transport server 上的附件篩選

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

附件篩選功能由只能在 Edge Transport Server 上使用的附件篩選器代理程式所提供。附件篩選可防止電子郵件中所附加的檔案進入您的組織中。您可以設定一或多個附件篩選器項目，以依附件檔案名稱來篩選附件。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [反垃圾郵件和反惡意程式的權限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)中的「反垃圾郵件功能」項目和[郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸代理程式」項目

  - 您在 Edge Transport Server 上對附件篩選所做的組態變更，只會對本機電腦產生效用。如果您的周邊網路中有多部 Edge Transport Server，您必須個別在每部 Edge Transport Server 上設定附件篩選。

  - 您只能使用命令介面來執行此程序。

  - 當您停用附件篩選，並重新啟動 Microsoft Exchange Transport 服務時，所有附件篩選功能都會停止運作。

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

## 使用命令介面啟用或停用附件篩選

當您啟用或停用附件篩選代理程式時，必須在您重新啟動 Microsoft Exchange Transport 服務後，變更才會生效。在 Edge Transport Server 上重新啟動 Microsoft Exchange Transport 服務時，會暫時中斷該伺服器上的郵件流程。

若要停用附件篩選功能，請執行下列命令：

    Disable-TransportAgent "Attachment Filtering Agent"

若要啟用附件篩選，請執行下列命令：

    Enable-TransportAgent "Attachment Filtering Agent"

在啟用或停用附件篩選後，請執行下列命令，以重新啟動 Microsoft Exchange Transport 服務：

    Restart-Service MSExchangeTransport

## 如何知道這是否正常運作？

若要確認您是否已順利啟用或停用附件篩選，請執行下列作業：

1.  執行下列命令：
    
        Get-TransportAgent "Attachment Filtering Agent"

2.  如果 **\[已啟用\]** 的值為 `True`，表示已啟用附件篩選。如果值為 `False`，則表示附件篩選是停用的。

## 使用命令介面檢視附件篩選項目

附件篩選項目可定義您要阻絕在組織以外的郵件附件。若要檢視附件篩選代理程式所使用的附件篩選項目，請執行下列命令：

    Get-AttachmentFilterEntry | Format-Table

若要檢視特定的 MIME 內容類型項目，請使用下列語法：

    Get-AttachmentFilteringEntry ContentType:<MIMEContentType>

例如，若要檢視 JPEG 影像的內容類型項目，請執行下列命令：

    Get-AttachmentFilteringEntry ContentType:image/jpeg

若要檢視特定的檔案名稱或副檔名項目，請使用下列語法：

    Get-AttachmentFilteringEntry FileName:<FileName or FileNameExtension>

例如，若要檢視 JPEG 附件的副檔名項目，請執行下列命令：

    Get-AttachmentFilteringEntry FileName:*.jpg

## 使用命令介面新增附件篩選項目

若要新增會依 MIME 內容類型篩選附件的附件篩選項目，請使用下列語法：

    Add-AttachmentFilterEntry -Name <MIMEContentType> -Type ContentType

下列範例會新增篩選 JPEG 影像的 MIME 內容類型項目。

    Add-AttachmentFilterEntry -Name image/jpeg -Type ContentType

若要新增會依檔案名稱或附檔名篩選附件的附件篩選項目，請使用下列語法：

    Add-AttachmentFilterEntry -Name <FileName or FileNameExtension> -Type FileName

下列範例會篩選具有.jpg 副檔名的附件。

    Add-AttachmentFilterEntry -Name *.jpg -Type FileName

## 如何知道這是否正常運作？

若要確認您已順利新增附件篩選項目，請執行下列作業：

1.  執行下列命令，以確認篩選項目是否存在。
    
        Get-AttachmentFilterEntry | Format-Table

2.  在簡訊中加入禁止的附件，並將其從外部信箱傳送給內部收件者，然後確認該郵件是否遭到拒絕、移除或刪除。

## 使用命令介面移除附件篩選項目

若要移除依 MIME 內容類型篩選附件的附件篩選項目，請使用下列語法：

    Remove-AttachmentFilterEntry ContentType:<ContentType>

下列範例會移除 JPEG 影像的 MIME 內容類型項目。

    Remove-AttachmentFilterEntry ContentType:image/jpeg

若要移除依檔案名稱或附檔名篩選附件的附件篩選項目，請使用下列語法：

    Remove-AttachmentFilterEntry FileName:<FileName or FileNameExtension>

下列範例會移除.jpg 副檔名的檔案名稱項目。

    Remove-AttachmentFilterEntry FileName:*.jpg

## 如何知道這是否正常運作？

若要確認您已順利移除附件篩選項目，請執行下列作業：

1.  執行下列命令，以確認篩選項目是否已移除。
    
        Get-AttachmentFilterEntry | Format-Table

2.  在簡訊中加入允許的附件，並將其從外部信箱傳送給內部收件者，然後確認該郵件是否連同附件順利傳遞。

## 使用命令介面檢視附件篩選動作

若要檢視在郵件中偵測到禁止附件時所採取的附件篩選動作，請執行下列命令：

    Get-AttachmentFilterListConfig

## 使用命令介面設定附件篩選動作

若要設定在郵件中偵測到禁止附件時所將採取的附件篩選動作，請使用下列語法：

    Set-AttachmentFilterListConfig [-Action <Reject | Strip | SilentDelete>] [-RejectResponse "<Message text>"] [-AdminMessage "<Replacement file text>"] [-ExceptionConnectors <ConnectorGUID>]

本範例會對附件篩選組態進行下列變更：

  - 拒絕 (封鎖) 含有禁止附件的郵件。

  - 對拒絕的郵件使用自訂回應。

<!-- end list -->

    Set-AttachmentFilterListConfig -Action Reject -RejectResponse "This message contains a prohibited attachment. Your message can't be delivered. Please resend the message without the attachment."

如需詳細資訊，請參閱[Set-AttachmentFilterListConfig](https://technet.microsoft.com/zh-tw/library/bb123483\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否已順利設定附件篩選動作，請在簡訊中加入禁止的附件，並將其從外部信箱傳送給內部收件者，然後確認該郵件和附件是否如預期進行處理。


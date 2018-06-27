---
title: '回復公用資料夾移轉從 Exchange 2013 至 Exchange Online: Exchange Online Help'
TOCTitle: 回復公用資料夾移轉從 Exchange 2013 至 Exchange Online
ms:assetid: bcd54aa0-aa45-4c68-b504-1475842d4b96
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt798259(v=EXCHG.150)
ms:contentKeyID: 74432751
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 回復公用資料夾移轉從 Exchange 2013 至 Exchange Online

 

_**上次修改主題的時間：**2017-03-20_

**摘要：** 請遵循下列步驟以您的公用資料夾基礎結構返回其 Exchange 2013 內部部署組織中的移轉前狀態。

如果您執行發生問題與公用資料夾遷移至 Exchange Online 或任何其他原因需要重新啟動 Exchange 2013 公用資料夾，請遵循下列步驟。

## 回復移轉

請注意是否您回復移轉，您會失去在 Exchange Online 移轉後，透過用戶端或透過電子郵件的郵件功能的公用資料夾至 \[公用資料夾已新增任何內容。若要儲存此內容，您可以將移轉後的公用資料夾內容匯出至.pst 檔案，可以再匯入內部部署公用資料夾回復完成時。

1.  Exchange 內部部署環境中，執行下列命令來解除鎖定您 Exchange 2013 公用資料夾 （請注意，解除鎖定可能需要數小時）：
    
        Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false -PublicFoldersEnabled Local 

2.  Exchange 內部部署環境中，將回復任何郵件功能的公用資料夾已由 SetMailPublicFolderExternalAddress.ps1 更新`ExternalEmailAddress` (使用中的指令碼*步驟 8： 測試並解除鎖定 Exchange Online 中的公用資料夾*[使用批次移轉至 Exchange 2013 公用資料夾移轉至 Exchange Online](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md)的)。您可以參照要識別已修改過的指令碼所建立的摘要檔案或使用產生稍早在相同的批次 migriont 程序中的檔案 OnPrem\_MEPF.xml 檔案來取得所有擁有郵件功能的公用資料夾的原始內容。

3.  在 Exchange Online PowerShell 中執行下列命令來移除所有的 Exchange Online 的公用資料夾和信箱：
    
        Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
        Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true

4.  若要將公用資料夾流量重新導向回內部部署 (Exchange 2013) 的 Exchange Online 環境中執行下列命令：
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote

5.  讓您的 Exchange Online 使用者可以存取其重新設定存取內部部署公用資料夾，請參閱[設定混合式部署的 Exchange 2013 公用資料夾](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)的指示。


---
title: '設定驗證 S/MIME 的虛擬憑證集合: Exchange Online Help'
TOCTitle: 設定驗證 S/MIME 的虛擬憑證集合
ms:assetid: 04a616e6-197c-490c-ae8c-c8d5f0f0b3dd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn626155(v=EXCHG.150)
ms:contentKeyID: 61212766
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定驗證 S/MIME 的虛擬憑證集合

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

如果您是租用戶系統管理員，您將必須設定用來驗證 S/MIME 憑證的虛擬憑證集合。此虛擬憑證集合會設定為具有 SST 副檔名的憑證存放區檔案類型。此 SST 檔案中包含所有在驗證 S/MIME 憑證時所將使用的根憑證和中繼憑證。

## 建立及儲存 SST

您只能使用命令介面來執行此程序。 若要了解如何在內部部署 Exchange 組織中開啟 Exchange 管理命令介面，請參閱[開啟命令介面。](https://technet.microsoft.com/zh-tw/library/dd638134\(v=exchg.150\))。 若要了解如何使用 Windows PowerShell 連線到 Exchange Online，請參閱[連線到 Exchange Online Protection PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554)。

身為管理員，您可以建立此 SST 檔案匯出憑證從信任的電腦使用`Export-Certificate` cmdlet 並指定為 SST 的類型。如需詳細資訊`Export-Certificate`指令程式，查看[匯出憑證](https://technet.microsoft.com/en-us/library/hh848628.aspx)參考主題。

SST 檔案產生後，請使用 `Set-Smimeconfig` 指令程式與 *-SMIMECertificateIssuingCA* 參數，將其儲存在虛擬憑證存放區中。例如：`Set-SmimeConfig -SMIMECertificateIssuingCA (Get-Content filename.sst -Encoding Byte)`

## 確保憑證的有效性

Exchange 2013 SP1 首先會檢查 SST 檔案，然後再驗證憑證。如果驗證失敗，它會查看本機電腦憑證存放區，以驗證憑證。這是 Exchange 2013 SP1 的新行為，與舊版的 Exchange 不同。在 Exchange Online 中，驗證時將只會使用 SST。

## 相關資訊

[為郵件簽章和加密的 S/MIME](s-mime-for-message-signing-and-encryption-exchange-2013-help.md)

[Get-SmimeConfig](https://technet.microsoft.com/zh-tw/library/dn554257\(v=exchg.150\))


---
title: '建立數位憑證要求: Exchange 2013 Help'
TOCTitle: 建立數位憑證要求
ms:assetid: efb00de7-070b-46bf-a2fc-00d07ae085c1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125165(v=EXCHG.150)
ms:contentKeyID: 52062610
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立數位憑證要求

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-02-21_

在Exchange Server 2013，您可以管理使用 EAC 或命令介面的憑證。EAC 中包含新的憑證管理使用者介面。透過這個新的 UI，您可以建立新的憑證、 編輯現有的憑證，或移除的憑證。

## 開始之前有哪些須知？

  - 預估完成時間： 10 分鐘加上的憑證授權單位回應的時間。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「Client Access Server 安全性」項目。

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


## 您要執行的工作

## 使用 EAC 建立新的憑證要求

1.  在 EAC 中，瀏覽至 **\[伺服器\]** \> **\[憑證\]**。

2.  在 **\[選取伺服器\]** 清單中，選取您要建立憑證的伺服器，然後按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 **\[新增 Exchange 憑證\]** 精靈中，選擇 **\[建立向憑證授權單位索取憑證的要求\]** 或 **\[建立自我簽署憑證\]**，然後選取 **\[下一步\]**。

4.  針對憑證輸入易記的名稱，然後選取 **\[下一步\]**。

5.  如果您沒有選擇的自我簽署的憑證，而且想萬用字元憑證，選取標示為**要求萬用字元憑證**\] 方塊中，輸入根網域，例如 \*。 contoso.com，然後選取 \[**下一步\]**。如果您選擇的自我簽署的憑證，請略過此步驟。

6.  選取要套用此憑證的伺服器，然後選取 **\[下一步\]**。

7.  指定要包含在憑證中的網域，然後選取 **\[下一步\]**。

8.  確認包含的網域正確無誤。如果您選擇的自我簽署的憑證，請選取 \[**完成**\]。否則請選取 \[**下一步**\]。

9.  輸入組織名稱、部門名稱、程式或位置、縣或市以及國家或地區，然後選取 **\[下一步\]**。

10. 輸入憑證要求的儲存位置，然後選取 **\[完成\]**。

若您未選取自我簽署憑證，則必須傳送憑證要求檔案至憑證授權單位進行處理。

## 使用命令介面建立新的憑證要求

執行下列命令。

    $reqfile = New-ExchangeCertificate -GenerateRequest -SubjectName "C=US,o=Contoso,cn=contosotocert" -DomainName "contoso.com" -PrivateKeyExportable $true

    $reqfile | out-file c:\certreq.txt

## 如何才能了解這是否正常運作？

如果您建立的自我簽署的憑證，新建立的憑證會出現在憑證管理 UI。如果您建立的憑證要求的憑證授權單位的憑證要求檔案都會在您指定的位置。將此檔案傳送至憑證授權單位。


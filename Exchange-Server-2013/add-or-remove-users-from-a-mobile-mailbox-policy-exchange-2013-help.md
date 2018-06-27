---
title: '新增或移除使用者從行動裝置信箱原則: Exchange 2013 Help'
TOCTitle: 新增或移除使用者從行動裝置信箱原則
ms:assetid: 4ca8e395-c074-4165-b788-16fae3e2ccab
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997929(v=EXCHG.150)
ms:contentKeyID: 50473190
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 新增或移除使用者從行動裝置信箱原則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-07-16_

行動裝置信箱原則可讓您將一組通用的安全性與行動裝置設定套用至使用者群組。您可以建立多個行動裝置信箱原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您在安裝 Microsoft Exchange Server 2013 時，將建立預設行動裝置信箱原則且所有使用者會自動指派此原則。</td>
</tr>
</tbody>
</table>


若欲瞭解更多與行動裝置信箱原則相關的管理工作，請參閱 [行動裝置信箱原則](mobile-device-mailbox-policies-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱主題中的「行動裝置信箱原則」[用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)項目。

  - 您必須擁有一個可於 \[行動\] \> \[行動裝置信箱原則\] 中的 EAC 使用的行動裝置信箱原則。

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

## 變更使用者的行動裝置信箱原則

您可以使用 EAC 或命令介面來變更使用者的行動裝置信箱原則。

## 使用 EAC 來變更使用者的行動裝置信箱原則

使用 EAC 來變更單一使用者的行動裝置信箱原則。

1.  在 EAC 中，按一下 \[收件者\] \> \[信箱\] 然後選擇信箱。

2.  在 \[詳細資料\] 窗格中，拉動捲軸至 \[電話與語音功能\] 然後選擇 \[檢視詳細資料\] 來顯示 \[行動裝置詳細資料\] 畫面。

3.  會顯示目前已指派之行動裝置信箱原則。若要變更行動裝置信箱原則，請按一下 \[**瀏覽**\]。

4.  從清單中選擇適合的行動裝置信箱原則，按一下 \[確定\] 然後按一下 \[儲存\]。

## 使用命令原則來新增使用者的行動裝置信箱原則

您可以變更**Set-CASMailbox**指令程式使用命令介面中的單一使用者的行動裝置信箱原則。

1.  在命令介面中，執行下列命令。
    
        Set-CASMailbox -Identity tony@contoso.com -ActiveSyncMailboxPolicy "Sales" 

## 如何才能了解這是否正常運作？

若要確認是否已成功變更使用者的行動裝置信箱原則，請執行下列其中一項：

1.  在 EAC 中，按一下 \[**收件者**\>**信箱**，然後選擇 \[特定收件者。在 \[詳細資料\] 窗格中，向下捲動**電話與語音功能**然後按一下 \[**檢視詳細資料**。

2.  在命令介面中，執行下列命令。
    
        Get-CASMailbox -Identity tony@contoso.com 

## 同時變更多個使用者的行動裝置信箱原則

若您想要同時變更多個使用者的行動裝置信箱原則，可使用 EAC 中的大量編輯功能或使用命令介面來變更使用者篩選設定的行動裝置信箱原則。

## 使用 EAC 中的大量編輯功能來變更多個使用者的行動裝置信箱原則

您可以使用大量編輯功能同時更新多個使用者的行動裝置信箱原則。

1.  在 EAC 中，按一下 \[收件者\] \> \[信箱\]。

2.  選擇多個使用者。

3.  在 \[詳細資料\] 窗格中，向下拉動捲軸至 \[Exchange ActiveSync\] 然後按一下 \[更新原則\]。

4.  按一下 \[瀏覽\] 來選擇行動裝置信箱原則。

5.  按一下 \[確定\]，然後按一下 \[儲存。

## 使用命令介面來變更使用者篩選設定的行動裝置信箱原則

您可以使用命令介面來變更這個篩選過的一組使用者的行動裝置信箱原則。您可篩選屬性各種不同的使用者。

1.  在命令介面中，執行下列命令。
    
        Get-Mailbox | where { $_.CustomAttribute1 -match "Manager"
         } | Set-CASMailbox -activesyncmailboxpolicy(Get-ActiveSyncMailboxPolicy "Contoso").Identity
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以改用<code>CustomAttribute1</code>任何<strong>Get-Mailbox</strong>物件上的內容。若要檢視的完整清單，請輸入： <code>Get-Mailbox username |fl</code>。</td>
    </tr>
    </tbody>
    </table>


## 如何才能了解這是否正常運作？

若要確認是否已成功變更使用者的行動裝置信箱原則，請執行下列其中一項：

1.  在 EAC 中，按一下 \[**收件者**\>**信箱**，並選擇特定收件者。在 \[詳細資料\] 窗格中，向下捲動**電話與語音功能**然後按一下 \[**檢視詳細資料**。

2.  在命令介面中，執行下列命令。
    
        Get-CASMailbox -Identity tony@contoso.com


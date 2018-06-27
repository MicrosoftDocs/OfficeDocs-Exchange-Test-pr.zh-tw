---
title: '建立使用者的撥號規則: Exchange Online Help'
TOCTitle: 建立使用者的撥號規則
ms:assetid: c11e3d62-3eb1-4d7e-8741-9bede593e2df
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ898502(v=EXCHG.150)
ms:contentKeyID: 51409213
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立使用者的撥號規則

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-03-09_

撥號規則群組包含撥號規則項目。撥號規則可用來修改電話號碼，再將它傳送至內部電話系統 (PBX) 或 IP PBX 針對撥出電話。撥號規則做兩種用途：

  - 指定可針對撥出電話撥打的號碼。當您建立的撥號規則時，您會指定可以撥打的號碼格式。拒絕不符合其中一個格式所指定的任何數字。如果您未設定任何撥號規則，來電者可放置在組織內的通話，但無法撥打任何撥出電話。

  - 這些轉換之前先傳送至內部部署電話系統撥打的號碼。撥號規則可以除去號碼從或新增至撥打的號碼的數字。例如，您可以使用撥號規則新增電話系統外線存取碼或以新增或移除長途或本機號碼的國家/地區碼。

若要指定您想要允許的 UM 撥號對應表的撥出電話的類型，您可以建立撥號規則群組具有撥號規則，然後利用這些授權 Outlook 語音存取使用者和撥入 UM 自動語音應答的來電者的撥出電話。您建立不同的撥號規則群組國家/地區及國際電話。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要整合 UM 與 Microsoft Lync Server，建議您至少建立一個撥號規則群組，然後在 SIP URI 撥號對應表、UM 信箱原則與 UM 自動語音應答上授權該撥號規則群組，以允許將所有的撥出電話轉接至 Lync Server。</td>
</tr>
</tbody>
</table>


如需了解其他的撥出管理工作，請參閱[讓使用者能夠進行的通話程序](allowing-users-to-make-calls-procedures-exchange-2013-help.md)。

## 常用撥號規則的範例


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>號碼模式</strong></p></td>
<td><p><strong>撥打的號碼</strong></p></td>
<td><p><strong>何時需要使用這個撥號規則？</strong></p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>*</p></td>
<td><p>允許所有撥出電話。</p></td>
</tr>
<tr class="odd">
<td><p>1425xxxxxxx</p></td>
<td><p>91425xxxxxxx</p></td>
<td><p>防止在使用者忘記撥打外線存取碼時撥打到內部分機或發生錯誤。</p></td>
</tr>
<tr class="even">
<td><p>1xxxxxxxxxx</p></td>
<td><p>1xxxxxxxxxx</p></td>
<td><p>允許所有號碼都以 1 當做開頭。</p></td>
</tr>
<tr class="odd">
<td><p>xxxxxxx</p></td>
<td><p>1425xxxxxxx</p></td>
<td><p>在 7 位數號碼中增加 1 和當地區碼 425。</p></td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間： 少於 3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。 如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 如果您將 UM 信箱原則將套用撥號規則群組，您必須請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 如果您將套用撥號規則群組到 UM 自動語音應答，您必須請確認已建立 UM 自動語音應答。如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

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


## 使用 EAC 建立撥號規則

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\]頁面上，按一下 \[設定\]。

3.  在 **\[UM 撥號對應表\]** 頁面 \> **\[撥號規則\]** 上，按一下位於 **\[國內/地區撥號規則\]** 或 **\[國際撥號規則\]** 下方的 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在 **\[新增撥號規則\]** 頁面，輸入下列資訊：
    
      - **撥號規則名稱**  輸入名稱撥號規則群組您要此規則的一部分。若要將它與其他規則的合併，使用相同的群組名稱。若要建立新的撥號規則群組，請輸入新的唯一名稱。
    
      - **轉換 （號碼遮罩） 的號碼模式**  輸入轉換之前撥號，例如 91425xxxxxxx 之號碼模式。如果來電者撥打比對的數字，UM 轉換將它對撥打的號碼之前先進行呼叫。輸入僅限數字和萬用字元 (x)。號碼模式也稱為*號碼遮罩*。
    
      - **Dialed 數**輸入要撥打的號碼。只使用數字和萬用字元 (x) 數字模式 9xxxxxxx 相同。從原始使用者所撥的號碼的數字會替換萬用字元 (x)。確定撥號號碼中的萬用字元數目的號碼模式的萬用字元數相同。
    
      - **註解**輸入註解或此撥號規則的描述。您可以使用註解來說明規則的作用，例如"Add a 9 來撥出電話"。

5.  按一下**\[確定\]**儲存撥號規則\]。您可以輸入規則\]，繼續使用同一個您想要一起授權規則的撥號規則群組名稱。


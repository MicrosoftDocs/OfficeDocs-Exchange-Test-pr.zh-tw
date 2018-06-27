---
title: '匯入地址修正 Edge Transport server 上的項目: Exchange 2013 Help'
TOCTitle: 匯入地址修正 Edge Transport server 上的項目
ms:assetid: bd0942c6-9c66-4b4c-b9bc-2f5f783def76
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb331966(v=EXCHG.150)
ms:contentKeyID: 61060516
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 匯入地址修正 Edge Transport server 上的項目

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

您可以使用逗點分隔值 (CSV) 檔案大量建立地址修正資訊或將它匯入至 Edge Transport Server。下列清單描述需要您這麼做的常見案例：

  - 您要取代 Edge Transport Server 的地址修正解決方案。

  - 您與協力廠商解決方案提供者簽訂合約，而他要求您修正其電子郵件地址。

  - 您收購了另一家公司，因而需要暫時修正所收購公司中的電子郵件地址。

您可以使用任何文字編輯器 (如記事本) 或應用程式 (如 Microsoft Excel) 來建立 CSV 檔案。如本主題所述格式化檔案，並將它儲存成 .csv 檔案。

CSV 檔案的第一列或*「標題列」*會列出參數名稱。每個參數都是以逗號分隔。下表描述必要參數和選用參數。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要或選用</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>地址修正項目的唯一描述性名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>InternalAddress</em></p></td>
<td><p>必要</p></td>
<td><p>想要變更的地址。您可以使用下列值：</p>
<ul>
<li><p>單一電子郵件地址 (chris@contoso.com)</p></li>
<li><p>單一網域或子網域 (contoso.com 或 sales.contoso.com)</p></li>
<li><p>網域及所有子網域 (*.contoso.com)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>ExternalAddress</em></p></td>
<td><p>必要</p></td>
<td><p>您想要的最終電子郵件地址。您可以使用下列值：</p>
<ul>
<li><p>單一電子郵件地址 (如果您為 <em>InternalAddress</em> 指定單一電子郵件地址)</p></li>
<li><p><em>InternalAddress</em> 之其他所有值的單一網域或子網域</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ExceptionList</em></p></td>
<td><p>選用</p></td>
<td><p>只適用於修正網域及所有子網域 (*.contoso.com) 中的電子郵件地址。指定想要排除不進行地址修正的一個或多個子網域。請使用雙引號括住值，並用逗號隔開各個值。例如，<code>&quot;marketing.contoso.com&quot;</code> 或 <code>&quot;marketing.contoso.com,legal.contoso.com&quot;</code>。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundOnly</em></p></td>
<td><p>選用</p></td>
<td><p><code>False</code> 表示在輸入及輸出郵件上寫入地址。<code>True</code> 表示只在輸出郵件上修正地址，而且您需要針對受影響的收件者手動將修正的電子郵件地址設定為 Proxy 地址。</p>
<p>預設值為 <code>False</code>，但是如果 <em>InternalAddress</em> 包含萬用字元 (*.contoso.com)，則必須將它設為 <code>True</code>。</p>
<p>CSV 檔案中的 <em>OutboundOnly</em> 參數值是 <code>True</code> 或 <code>False</code>，而不是 <code>$True</code> 或 <code>$False</code>。</p></td>
</tr>
</tbody>
</table>


標題列下的每一列都代表個別的地址修正項目。每一列中值的順序必須與標頭列中參數名稱的順序相同。每個值都以逗號分隔。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：30 分鐘

  - 請確定您了解地址修正的後果。例如，修正的電子郵件地址在 Exchange 組織中必須是唯一的，而且您可能需要對受影響的收件者設定 Proxy 地址。如需詳細資訊，請參閱[地址修正 Edge Transport server 上](address-rewriting-on-edge-transport-servers-exchange-2013-help.md)及[管理 Edge Transport server 上的地址修正](manage-address-rewriting-on-edge-transport-servers-exchange-2013-help.md)。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「地址修正代理程式」項目。

  - 如果您有多個 Edge Transport Server，建議您使用本主題中的程序，將地址修正項目匯入至單一 Edge Transport Server，然後將該 Edge Transport Server 的組態複製到組織中的其他 Edge Transport Server。如需如何複製 Edge Transport Server 的相關資訊，請參閱[Edge Transport server 複製的組態](edge-transport-server-cloned-configuration-exchange-2013-help.md)。

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


## 該怎麼做？

## 步驟 1：建立 CSV 檔案

當您建立 CSV 檔案時，請考慮下列項目：

  - 如果您在 CSV 檔案中指定選用參數的值，則每一列都必須包括該欄的值。如果您想要建立多個地址修正項目 (其中有些項目有選用參數，有些項目則沒有)，則需要將那些地址修正項目分成兩個不同的 CSV 檔案，然後分別匯入每個 CSV 檔案。

  - 如果 CSV 檔案包含非 ASCII 字元，請一定要以 UTF-8 編碼或其他 Unicode 編碼儲存該 CSV 檔案。根據應用程式而定，當電腦的系統地區設定與 CSV 檔案中所用的語言相符時，以 UTF-8 編碼或其他 Unicode 編碼儲存 CSV 檔案可能會比較容易。

下列範例顯示如何在填入 CSV 檔案時，同時包含選用的 *ExceptionList* 及 *OutboundOnly* 參數：

    Name,InternalAddress,ExternalAddress,ExceptionList,OutboundOnly
    "Wingtip UK",*.wingtiptoys.co.uk,tailspintoys.com,"legal.wingtiptoys.co.uk,finance.wingtiptoys.co.uk,support.wingtiptoys.co.uk",True
    "Wingtip USA",*.wingtiptoys.com,tailspintoys.com,"legal.wingtiptoys.com,finance.wingtiptoys.com,support.wingtiptoys.com,corp.wingtiptoys.com",True
    "Wingtip Canada",*.wingtiptoys.ca,tailspintoys.com,"legal.wingtiptoys.ca,finance.wingtiptoys.ca,support.wingtiptoys.ca",True

## 步驟 2：匯入 CSV 檔案

若要匯入 CSV 檔案，請使用下列語法：

    Import-Csv <FileNameAndPath> | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

此範例會從 C:\\My Documents\\ImportAddressRewriteEntries.csv 匯入地址修正項目。

    Import-Csv "C:\My Documents\ImportAddressRewriteEntries.csv" | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

## 如何才能了解此步驟是否正常運作？

若要確認您已順利從 CSV 檔案匯入地址修正項目，請執行下列作業：

1.  若要查看所有地址修正項目，請執行命令 `Get-AddressRewriteEntry`。

2.  若要查看特定地址修正項目的詳細資料，請執行命令 `Get-AddressRewriteEntry <AddressRewriteIdentity> | Format-List`。


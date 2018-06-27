---
title: '系統管理員稽核記錄檔結構: Exchange 2013 Help'
TOCTitle: 系統管理員稽核記錄檔結構
ms:assetid: 87e259c9-c884-4d53-bd78-d13f2300d73e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff459251(v=EXCHG.150)
ms:contentKeyID: 50554023
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 系統管理員稽核記錄檔結構

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

系統管理員稽核記錄檔包含的所有 cmdlet 和參數中Exchange管理命令介面和Exchange系統管理中心 (EAC) 所執行的記錄。若要建立隨選，時正在執行時系統管理員稽核記錄報告在 EAC 中，或您在命令介面中執行**New-AdminAuditLogSearch**指令程式。如需稽核記錄的詳細資訊，請參閱[系統管理員稽核記錄](administrator-audit-logging-exchange-2013-help.md)。

稽核記錄是 XML 檔案並可包含多個稽核記錄項目。下表說明每個 XML 標記以及其關聯的屬性。

要尋找與系統管理員稽核記錄相關的管理工作嗎？請參閱[管理系統管理員稽核記錄](manage-administrator-audit-logging-exchange-2013-help.md)。

### 稽核記錄檔 XML 標記和屬性

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>屬性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;</code></p>
<p></p></td>
<td><p><code>N/A</code></p></td>
<td><p>這是 XML 文件宣告標籤。並包含每個稽核記錄檔 XML 檔案中包含的 XML 版本號碼和的字元編碼值。</p></td>
</tr>
<tr class="even">
<td><p><code>SearchResults</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>此標籤包含在 XML 檔中所有稽核記錄項目。<code>Event</code>標記為此標籤的子項。</p>
<p>有一個<code>SearchResults</code>標記每個 XML 檔案。</p></td>
</tr>
<tr class="odd">
<td><p><code>Event</code></p></td>
<td><p><code> </code></p></td>
<td><p>此標籤包含個別的指令程式的稽核記錄項目。此標籤包含<code>Caller</code>、 <code>Cmdlet</code>、 <code>ObjectModified</code>、 <code>RunDate</code>、 <code>Succeeded</code>、 <code>Error</code>及<code>OriginatingServer</code>屬性。<code>CmdletParameters</code>和<code>ModifiedProperties</code>標記為此標籤的子系。</p>
<p>有一個<code>Event</code>標記每稽核記錄項目。</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Caller</code></p></td>
<td><p>此屬性包含在<code>Cmdlet</code>屬性中執行指令程式之使用者的使用者帳戶。</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Cmdlet</code></p></td>
<td><p>此屬性包含在<code>Caller</code>屬性中之使用者所執行的指令程式的名稱。</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>ObjectModified</code></p></td>
<td><p>此屬性包含<code>Cmdlet</code>屬性中指定 cmdlet 所修改的物件。<code>ModifiedProperties</code>標籤會顯示哪些屬性已修改此物件上。</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>RunDate</code></p></td>
<td><p>此屬性包含的日期和時間<code>Cmdlet</code>屬性在 cmdlet 執行的時間。</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Succeeded</code></p></td>
<td><p>此屬性會指定是否在<code>Cmdlet</code>屬性指令程式執行成功。此值為<code>True</code>或<code>False</code>。</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Error</code></p></td>
<td><p>此屬性包含如果無法成功完成<code>Cmdlet</code>屬性中的指令程式產生的錯誤訊息。如果已不發生任何錯誤，此值是設定為<code>None</code>。</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>OriginatingServer</code></p></td>
<td><p>此屬性包含在其<code>Cmdlet</code>屬性中指定此 cmdlet 所執行的伺服器。</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletParameters</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>此標籤含有所有指定當此 cmdlet 所執行的參數。<code>Parameter</code>標記為此標籤的子項。</p>
<p>沒有<code>Event</code>標記每一個<code>CmdletParameters</code>標籤。</p></td>
</tr>
<tr class="even">
<td><p><code>Parameter</code></p></td>
<td><p><code> </code></p></td>
<td><p>此標籤包含個別的參數來指定當此 cmdlet 所執行。此標籤含有<code>Name</code>及<code>Value</code>屬性。</p>
<p>可以個別<code>CmdletParameters</code>標記的多個<code>Parameter</code>標籤。</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Name</code></p></td>
<td><p>此屬性包含參數來指定在執行此指令程式的名稱。</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Value</code></p></td>
<td><p>此屬性包含在<code>Name</code>屬性中指定此參數提供值。</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>此標籤含有所有已執行此指令程式所修改的屬性。<code>Property</code>標記為此標籤的子項。</p>
<p>沒有<code>Event</code>標記每一個<code>ModifiedProperties</code>標籤。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果<strong>Set-AdminAuditLogConfig</strong>指令程式上的<em>LogLevel</em>參數設為<code>Verbose</code>僅填入此標籤。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><code>Property</code></p></td>
<td><p><code> </code></p></td>
<td><p>此標籤包含此 cmdlet 所執行時所指定的個別屬性。此標籤包含<code>Name</code>、 <code>OldValue</code>，以及<code>NewValue</code>屬性。</p>
<p>可以個別<code>ModifiedProperties</code>標記的多個<code>Property</code>標籤。</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Name</code></p></td>
<td><p>此屬性包含當此 cmdlet 所執行已修改的屬性名稱。</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>OldValue</code></p></td>
<td><p>此屬性包含已變更前<code>Name</code>屬性中指定的屬性中所包含的值。</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>NewValue</code></p></td>
<td><p>此屬性包含在<code>Name</code>屬性的屬性已變更為的值。</p></td>
</tr>
</tbody>
</table>


## 範例稽核記錄項目

下列是一般的稽核記錄項目範例。根據記錄項目中的資訊，我們知道下列發生：

  - 在 10/18/2012 下午 3:48 太平洋日光節約時間 (UTC 7)，使用者`Administrator`執行指令程式**Set-Mailbox**。

  - 當**Set-Mailbox** cmdlet 所執行已提供下列兩個參數：
    
      - *Identity* `david`的值
    
      - *ProhibitSendReceiveQuota* `10GB`的值

  - 已修改兩個物件`david`上的下列屬性：
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>因為<code>Set-AdminAuditLogConfig</code>指令程式上的<em>LogLevel</em>參數設為 [ <code>Verbose</code>在本例中修改的屬性會儲存稽核記錄檔。</td>
    </tr>
    </tbody>
    </table>
    
      - *ProhibitSendReceiveQuota* `10GB`，以取代`35GB`舊值的新值

  - 沒有任何錯誤成功完成作業。

<!-- end list -->

    <?xml version="1.0" encoding="utf-8"?>
    <SearchResults>
    
      <Event Caller="corp.e15a.contoso.com/Users/Administrator" Cmdlet="Set-Mailbox" ObjectModified="corp.e15a.contoso.com/Users/david" RunDate="2012-10-18T15:48:15-07:00" Succeeded="true" Error="None" OriginatingServer="WIN8MBX (15.00.0516.032)">
        <CmdletParameters>
          <Parameter Name="Identity" Value="david" />
          <Parameter Name="ProhibitSendReceiveQuota" Value="10 GB (10,737,418,240 bytes)" />
        </CmdletParameters>
        <ModifiedProperties>
          <Property Name="ProhibitSendReceiveQuota" OldValue="35 GB (37,580,963,840 bytes)" NewValue="10 GB (10,737,418,240 bytes)" />
        </ModifiedProperties>
      </Event>
    </SearchResults>


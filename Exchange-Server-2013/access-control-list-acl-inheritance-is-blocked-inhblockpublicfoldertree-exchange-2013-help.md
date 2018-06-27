---
title: '存取控制清單 (ACL) 繼承是 blocked_InhBlockPublicFolderTree: Exchange 2013 Help'
TOCTitle: 存取控制清單 (ACL) 繼承是 blocked_InhBlockPublicFolderTree
ms:assetid: e3b89c8a-d6f8-4864-8bf0-35a78ce87cc4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.inhblockpublicfoldertree(v=EXCHG.150)
ms:contentKeyID: 50474462
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 存取控制清單 (ACL) 繼承是 blocked\_InhBlockPublicFolderTree

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2015-03-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 或 Exchange Server 2010 安裝程式無法繼續因為尚未能夠傳播的必要權限。

Exchange 安裝程式需要的權限繼承會啟用下列 Exchange 物件：

  - 部署 Exchange 組織物件

  - Exchange Administrative Group 物件

  - Exchange 伺服器 container 物件

  - Exchange 通訊清單物件

  - Exchange 公用資料夾物件

  - Exchange 公用資料夾樹狀目錄中物件

若要啟用的這些物件的權限繼承的失敗可能會導致郵件流程問題、 儲存裝載問題及其他服務中斷。

若要解決此問題，請確定 「 允許權限傳播到此物件及子物件 」 設定已啟用的物件，然後重新執行 Exchange Server 2007 或 Exchange 2010 安裝程式。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>若要重新啟用 Exchange 組態物件使用 Exchange Server 2003 Exchange 系統管理員權限繼承</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>設定登錄參數以啟用 [<strong>安全性</strong>] 索引標籤的物件屬性] 方塊中的 Exchange 系統管理員。</p>
<ol>
<li><p>啟動登錄編輯程式 (Regedt32.exe)。</p></li>
<li><p>在登錄中找到下列機碼：</p>
<p><strong>HKEY_CURRENT_USER\Software\Microsoft\Exchange\EXAdmin</strong></p></li>
<li><p>在 [<strong>編輯</strong>] 功能表上按一下 [<strong>新增</strong>]，然後新增下列登錄值：</p>
<p><strong>數值名稱</strong>： ShowSecurityPage</p>
<p><strong>資料類型</strong>： REG_DWORD</p>
<p><strong>基數</strong>︰ 二進位</p>
<p><strong>值</strong>： 1</p></li>
<li><p>結束登錄編輯程式。</p></li>
</ol>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，在組態物件的屬性] 方塊中未啟用 [<strong>安全性</strong>] 索引標籤。</td>
</tr>
</tbody>
</table>

</li>
<li><p>開啟 [Exchange 系統管理員、 尋找物件有問題、 物件上按一下滑鼠右鍵並選取 [<strong>內容</strong>]。</p></li>
<li><p>選取 [<strong>安全性</strong>] 索引標籤，然後按一下 [<strong>進階]</strong>。</p></li>
<li><p>選取 [<strong>允許從傳播到此物件及所有子物件的父項繼承權限</strong>重新啟用權限繼承。</p></li>
<li><p>重新啟動 Exchange 伺服器。</p></li>
</ol></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您不正確地修改 Active Directory 物件的屬性使用 ADSI Edit、 LDP 工具或其他 LDAP 第 3 版用戶端時，您可能會導致嚴重問題。這些問題可能會要求您安裝 Microsoft Windows Server™ 2003年、 Exchange 伺服器，或兩者。修改自行承擔 Active Directory 物件屬性。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>若要重新啟用 Exchange 組態物件使用 ADSIEdit 從 Exchange Server 2007 或 Exchange Server 2010 的權限繼承</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>安裝 ADSI 編輯器。</p></li>
<li><p>啟動 [Adsi 編輯器]。按一下 [<strong>開始]</strong>、 按一下 [<strong>執行</strong>]、 [文字] 方塊中輸入<strong>adsiedit.msc</strong> ，然後按一下 [確定]。</p></li>
<li><p>瀏覽至上述的物件、 物件上按一下滑鼠右鍵並選取 [<strong>內容</strong>]。</p></li>
<li><p>選取 [<strong>安全性</strong>] 索引標籤，然後按一下 [<strong>進階]</strong>。</p></li>
<li><p>選取 [<strong>允許從傳播到此物件及所有子物件的父項繼承權限</strong>重新啟用權限繼承。</p></li>
<li><p>選取 [<strong>確定]</strong>兩次，以套用變更]。</p></li>
<li><p>等待 Active Directory 複寫傳播變更或強制執行 Active Directory 複寫遵循 Microsoft 知識庫文章 232072，&quot;初始化複寫之間 Active Directory 直接複寫協力廠商 」 (<a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=232072" class="uri">http://go.microsoft.com/fwlink/?linkid=3052&amp;kbid=232072</a>) 中的指導。</p></li>
</ol></td>
</tr>
</tbody>
</table>


---
title: '簡化 Office 365 Hybrid 的 Outlook Web App URL: Exchange 2013 Help'
TOCTitle: 簡化 Office 365 Hybrid 的 Outlook Web App URL
ms:assetid: 19449aee-3796-4298-90c6-c7579b8d2f7a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt791749(v=EXCHG.150)
ms:contentKeyID: 74259172
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 簡化 Office 365 Hybrid 的 Outlook Web App URL

 

_**上次修改主題的時間：** 2016-11-11_


了解如何為混合式環境中的雲端信箱使用者設定 網頁型 Outlook (Outlook Web App) 的 URL。

組織從內部部署 Exchange 移至 Office 365 的主要考量，就是使用者體驗。使用者需要不受干擾地存取他們的信箱，不論他們的信箱移動的位置及時間為何。有了這個概念，可使兩者共存的 網頁型 Outlook (先前稱為 Outlook Web App) 便非常重要。

試想以下情景︰公司使用混合式部署，將其中一些信箱從內部部署 Exchange 移至 Office 365。在星期五進行移動之前，使用者可以利用 URL https://mail.contoso.com/owa 存取他們的內部部署信箱。在星期一移動完成之後，當相同的使用者嘗試使用該 URL 存取其信箱時，就會發生錯誤。

若要使用 網頁型 Outlook 讓受影響的使用者連線到他們的信箱，您有兩個選項︰

  - **告訴使用者新的 URL (例如，https://outlook.com/owa/contoso.com)** 使用此選項會有以下問題︰
    
      - URL 較為複雜。
    
      - 對受影響的使用者來說不是很完美的體驗。

  - **在組織關聯性中設定 TargetOWAUrl 設定**   使用此選項會有以下問題︰
    
      - 雲端信箱的端點為外部端點 (而非使用者預期的網域)。
    
      - 端點需要 URL 中的網域 (以區別 Office 365 商務和 outlook.com 消費者供應項目)。
    
      - 端點會導致使用者看到憑證不符的警告。

若要減少使用雲端信箱時的問題，請執行下列步驟：

1.  **在 DNS 中建立指向 mail.office365.com 的 CNAME 記錄 (例如 cloudowa.contoso.com)**
    
      - 請確定您已在內部和外部 (公用) DNS 中建立此 CNAME 記錄，因為使用者可能會從內部或外部網際網路連線來連線。
    
      - 在我們的範例中，我們在要求中使用網域 contoso.com ( cloudowa 部分會被捨棄)。這表示您不需要在 URL 中指定網域。

2.  **在內部部署組織關聯性中設定 網頁型 Outlook 重新導向**   若要這樣做，請在內部部署 Exchange 中的 Exchange 管理命令介面 中使用以下語法：
    
        Set-OrganizationRelationship -TargetOWAUrl http://<CNAME value>/owa
    
    例如，如果您在步驟 1 中建立的 CNAME 記錄是 cloudowa.contoso.com，請執行下列命令︰
    
        Set-OrganizationRelationship -TargetOWAUrl http://cloudowa.contoso.com/owa
    
    **注意：**
    
      - 使用 http，而不是 https。
    
      - 組織關聯性會需要行尾值 /owa，而使用者則毋須在 URL 中輸入 /owa。

## 多個驗證提示

使用者可能會根據以下條件收到多個驗證提示︰

  - 使用者連線的地方 (內部或外部網際網路連線)。

  - 電腦是否已加入網域。

  - 您是否正在混合式環境中使用識別身分同盟。

下表說明使用者預期的驗證提示體驗。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>驗證方法</th>
<th>用戶端電腦</th>
<th>驗證提示體驗</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>識別身分同盟</p></td>
<td><p>內部網際網路連線</p></td>
<td><p>單一提示</p></td>
</tr>
<tr class="even">
<td><p>識別身分同盟</p></td>
<td><p>外部網際網路連線</p></td>
<td><p>雙重提示</p></td>
</tr>
<tr class="odd">
<td><p>無識別身分同盟</p></td>
<td><p>已加入網域 (內部或外部)</p></td>
<td><p>雙重提示</p></td>
</tr>
<tr class="even">
<td><p>有或沒有識別身分同盟</p></td>
<td><p>未加入網域 (內部或外部)</p></td>
<td><p>雙重提示</p></td>
</tr>
</tbody>
</table>


**注意：** 識別身分同盟要求按照主題 [https://go.microsoft.com/fwlink/p/?linkid=834460](https://go.microsoft.com/fwlink/p/?linkid=83446) 所述，在 Internet Explorer 內部網路區域內設定 AD FS 端點，AD FS 需按照一般 Office 365 指導方針設定。


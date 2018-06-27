---
title: 'DLP 規則如何套用至評估郵件: Exchange Online Help'
TOCTitle: DLP 規則如何套用至評估郵件
ms:assetid: 1ac77020-26ff-410c-ab09-4f28a99d67a1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn329050(v=EXCHG.150)
ms:contentKeyID: 56269011
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DLP 規則如何套用至評估郵件

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

您可以在 Microsoft Exchange 資料遺失防護 (DLP) 原則中設定敏感資訊規則，以偵測電子郵件中極為特定的資料。本主題將協助您了解套用這些規則的方式及評估郵件的方式。您如果知道規則的強制執行方式，將有助於避免電子郵件使用者的工作流程遭到無謂中斷，同時使 DLP 偵測展現高度準確性。讓我們以 Microsoft 提供的信用卡資訊規則為例。當您啟動傳輸規則或 DLP 原則時，Exchange 傳輸規則代理程式會根據您建立的規則集檢查所有由使用者傳送的郵件。

## 明確了解您的需求

假設您必須對郵件中的信用卡資訊採取行動。您在發現這些資訊時採取的行動並不在本主題的討論範圍，但是如果您想了解那方面的資訊，可以參閱[郵件流程規則動作在 Exchange Online](https://technet.microsoft.com/zh-tw/library/jj919237\(v=exchg.150\))。在儘可能確認的狀況下，您必須確定在郵件中偵測到的內容真的是信用卡資料，而非僅是一組長得像信用卡資料的數字，例如訂位代碼或車牌號碼。為了符合此需求，讓我們清楚指定下列資訊應歸類為信用卡。

**    Margie’s Travel,  
    I have received updated credit card information for Spencer.  
    Spencer Badillo  
    Visa:4111 1111 1111 1111  
    Expires:2/2012  
    Please update his travel profile.**

讓我們清楚指定下列資訊不應歸類為信用卡。

**    Hi Alex,  
    I expect to be in Hawaii too.My booking code is 1234 1234 1234 1234 and I’ll be there on 3/2012.  
    Regards, Lisa**

下列 XML 片段顯示目前在 Exchange 所提供的敏感資訊規則中如何定義先前表達的需求，以及此片段是如何內嵌在其中一個提供的 DLP 原則範本中。

    <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085" patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>

## 您解決方案中的模式比對

先前顯示的 XML 規則定義包含了模式比對，可改善規則只偵測到重要資訊而未偵測到相關模糊資訊的可能性。如需 DLP 規則與範例之 XML 架構的詳細資訊，請參閱[定義自己的 DLP 範本和資訊類型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)。

在信用卡規則中，有個代表了模式的 XML 程式碼區段，其中包含一個主要識別碼比對和其他一些佐證性證據。這三項需求的說明如下：

1.  `<IdMatch idRef="Func_credit_card" />  ` — 這表示必須符合某個內部定義的函數 (名稱為 credit card)。此函數包含下列兩項驗證：
    
    1.  它會比對規則運算式 (在此例子中是用於比對 16 碼) ，其中可能還包含一些變化，例如空格分隔符號 (以便也比對到 **4111 1111 1111 1111**)，或是連字號分隔符號 (以便也比對到 **4111-1111-1111-1111**)。
    
    2.  此函數會對這 16 位數評估 Lhun 的總和檢查碼演算法，以確定這組數字真的很有可能是信用卡號。
    
    3.  它需要有必要比對，在此比對後才會評估佐證性證據。

2.  `<Any minMatches="1">  ` — 此區段表示至少需要存在下列一項證據。

3.  佐證性證據可以符合下列三者之一：
    
    `<Match idRef="Keyword_cc_verification" />`
    
    `<Match idRef="Keyword_cc_name" />`
    
    `<Match idRef="Func_expiration_date" />`
    
    這三項純粹表示需要有一份信用卡關鍵字、信用卡名稱或到期日的清單。到期日是以內部另一個函數來定義及評估。

## 根據規則來評估內容的程序

下列五個步驟代表 Exchange 將電子郵件拿來與您的規則比較的步驟。就我們的範例信用卡規則而言，所採取的步驟如下。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>步驟</th>
<th>動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1. 取得內容</p></td>
<td><p>Spencer Badillo</p>
<p>Visa：4111 1111 1111 1111</p>
<p>過期：2/2012</p></td>
</tr>
<tr class="even">
<td><p>2. 規則運算式分析</p></td>
<td><p>4111 1111 1111 1111 -&gt; 偵測到 16 位數的數字</p></td>
</tr>
<tr class="odd">
<td><p>3. 函數分析</p></td>
<td><ul>
<li><p>4111 1111 1111 1111 -&gt; 符合總和檢查碼</p></li>
<li><p>1234 1234 1234 1234 -&gt; 不符合</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>4. 其他辨識項</p></td>
<td><ol>
<li><p>關鍵字 Visa 接近數字。</p></li>
<li><p>日期 (2/2012) 的規則運算式接近數字。</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>5. Verdict</p></td>
<td><ol>
<li><p>有符合總和檢查碼的規則運算式。</p></li>
<li><p>額外的證據可增加信賴。</p></li>
</ol>
<p></p></td>
</tr>
</tbody>
</table>


Microsoft 設定的這個規則規定，電子郵件內容必須出現佐證性證據 (例如關鍵字)，才能符合此規則。因此，下列電子郵件內容不會被偵測為包含信用卡：

**    Margie’s Travel,  
    I have received updated information for Spencer.  
    Spencer Badillo  
    4111 1111 1111 1111  
    Please update his travel profile.**

您可以使用自訂規則來定義不含額外證據的模式，如下個範例所示。這會偵測只含信用卡號而不含佐證性證據的郵件。

``` 
      <Pattern confidenceLevel="85">
         <IdMatch idRef="Func_credit_card" />
      </Pattern>
    </Entity>
```

本文對於信用卡的說明同樣也可以延伸至其他敏感資訊規則。若要查看 Microsoft 在 Exchange 中提供之規則的完整清單，請在 Exchange 管理命令介面中以下列方式使用 [Get-ClassificationRuleCollection](https://technet.microsoft.com/zh-tw/library/jj218696\(v=exchg.150\)) 指令程式：

    $rule_collection = Get-ClassificationRuleCollection

    $rule_collection[0].SerializedClassificationRuleCollection | Set-Content oob_classifications.xml -Encoding byte

## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\))

[使用 PowerShell 與 Exchange 2013 (Exchange 管理命令介面)](https://technet.microsoft.com/zh-tw/library/bb123778\(v=exchg.150\))

[Exchange Online PowerShell](https://technet.microsoft.com/zh-tw/library/jj200677\(v=exchg.150\))


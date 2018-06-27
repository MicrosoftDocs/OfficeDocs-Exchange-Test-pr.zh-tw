---
title: '了解管理角色指派: Exchange 2013 Help'
TOCTitle: 了解管理角色指派
ms:assetid: 1dc33dd6-52fb-4852-a5ce-027bc73e1d8f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335131(v=EXCHG.150)
ms:contentKeyID: 50472666
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 了解管理角色指派

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-10-04_

*管理角色指派*，也就是在 Microsoft Exchange Server 2013中的角色型存取控制 (RBAC) 權限模型的一部分，是管理角色與角色受託人之間的連結。*角色受託人*為角色群組、 角色指派原則、 使用者或萬用安全性群組 (USG)。角色必須指派給角色受託人為其才會生效。如需 RBAC 的詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題著重於進階 RBAC 功能。如果您要管理基本 Exchange 2013 權限，例如使用 Exchange 系統管理中心 (EAC) 新增和移除角色群組的成員、建立和修改角色群組，或建立和修改角色指派原則，請參閱<a href="permissions-exchange-2013-help.md">權限</a>。</td>
</tr>
</tbody>
</table>


本主題討論指派的角色群組和角色指派原則的角色及直接角色指派給使用者和 Usg。它不會會談的角色群組或角色指派原則給使用者的工作分派。如需有關角色群組和角色指派原則已指派給使用者的權限的建議的方式，請參閱下列主題：

  - [了解管理角色群組](understanding-management-role-groups-exchange-2013-help.md)

  - [了解管理角色指派原則](understanding-management-role-assignment-policies-exchange-2013-help.md)

您可以建立下列類型的角色指派，這些指派會在本主題稍後的內容中詳細說明：

  - Regular and delegating role assignments

  - Exclusive role assignments

## 管理角色指派

當您變更角色指派時，所做的變更可能會之間角色群組和角色指派原則。新增、 移除或修改角色指派至或來自這些角色 assignees，您可以控制哪些權限會授與給系統管理員和事實上開啟及關閉管理的相關功能的使用者。

您也可能會想要角色直接指派給使用者或 Usg。這是更進階的工作可讓您定義細微的層級權限會授與您的使用者。雖然這提供彈性，也會增加權限模型的複雜性。例如，如果使用者變更工作，您可能需要手動重新指派給該使用者另一位使用者的角色。這就是為什麼我們建議您先使用權限提供給您的使用者角色群組和角色指派原則。您可以將角色指派給角色群組或角色指派原則，然後剛新增或移除角色群組的成員或視需要變更角色指派原則。

您可以新增、 移除及啟用角色指派、 修改現有的角色指派，在 「 管理範圍和移至其他角色 assignees 的角色指派。將角色指派給角色群組、 角色指派原則、 使用者和 Usg 的程序主要是針對每個角色受託人相同。以下是唯一的例外狀況：

  - 角色指派原則只能被指派給使用者管理角色。

  - 角色指派原則無法被指派委派角色指派。

  - 建立角色指派原則的角色指派時，無法指定管理範圍。

如需管理角色指派的詳細資訊，請參閱下列主題：

  - 角色群組：
    
      - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - 角色指派原則：
    
      - [管理角色指派原則](manage-role-assignment-policies-exchange-2013-help.md)
    
      - [變更角色指派](change-a-role-assignment-exchange-2013-help.md)

  - 使用者及 USG：
    
      - [將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)
    
      - [移除使用者或 USG 的角色](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)
    
      - [變更角色指派](change-a-role-assignment-exchange-2013-help.md)
    
      - [角色範圍變更](change-a-role-scope-exchange-2013-help.md)
    
      - [委派角色指派](delegate-role-assignments-exchange-2013-help.md)

## 一般和委派角色指派

一般角色指派可讓角色受託人存取管提供相關的管理角色的管理角色項目。如果多個管理角色指派給角色受託人，從每個管理角色的管理角色項目是彙總及套用。這表示如果傳輸規則和日誌記錄角色指派角色受託人，則會結合，和所有相關的管理角色項目會指定給角色受託人。如果角色受託人的角色群組或角色指派原則、 角色所提供的權限然後指定以指派給角色群組或角色指派原則的使用者。如需管理角色和角色項目的詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

委派角色指派不會授與存取管理功能。委派角色指派讓角色受託人將指定的角色指派給其他角色 assignees。角色群組角色受託人時，任何角色群組的成員可將角色指派給其他角色受託人。根據預設，只有組織管理角色群組具有能夠將角色指派給其他角色 assignees。僅限使用者安裝Exchange 2013是預設 「 組織管理角色群組的成員。您可以，但是新增其他使用者依需要此角色群組或建立其他角色群組和指派委派角色指派給這些群組。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>委派角色指派可讓角色 assignees 委派管理角色至其他角色 assignees。這不會啟用使用者委派角色群組。如需有關角色群組委派的詳細資訊，請參閱<a href="understanding-management-role-groups-exchange-2013-help.md">了解管理角色群組</a>。</td>
</tr>
</tbody>
</table>


如果您希望使用者可以管理功能，並將授與使用該功能之權限的角色指派給其他使用者，請進行下列指派：

1.  為每個管理角色進行一般角色指派，以授與需要管理之功能的存取權。

2.  為每個您允許指派給其他角色受託人的管理角色，進行委派角色指派。

為一般和委派角色指派的角色受託人不需要相同。例如，使用者已指派傳輸規則角色使用一般角色指派的角色群組的成員。這可讓使用者管理傳輸規則功能。但未指派使用者委派角色指派的傳輸規則角色讓使用者無法將此角色指派給其他使用者。不過，使用者是指定給使用委派角色指派的日誌記錄管理角色的角色群組的成員。使用者為其成員的角色群組沒有日誌記錄角色的一般角色指派但因為已定義委派角色指派，使用者可以將角色指派給其他角色 assignees。

## 管理範圍

當您建立 \[一般\] 或 \[將委派的管理角色指派時，您必須以限制使用者可以操控物件建立工作分派與管理範圍的選項。您可以建立收件者範圍或組態的範圍。收件者範圍可讓您控制人員可以操控信箱、 郵件使用者、 通訊群組、 等等。組態範圍可讓您控制可操作伺服器和資料庫的人員。

收件者和組態範圍可讓您分割伺服器、 資料庫或組織中的收件者物件的管理。例如，收件者範圍可以新增至角色指派，讓管理員可以在溫哥華只可以管理相同的 office 中的收件者。伺服器設定範圍無法新增至不同的角色指派，讓管理員可以在雪梨只能夠管理其Active Directory網站中的伺服器。

範圍啟用指派給使用者群組與可讓您直接其中系統管理員可以執行其管理的權限。這可讓您建立對應至地理或組織界限的權限模型。

您可以建立工作分派與預先定義的範圍，或者您可以將自訂的範圍新增至工作分派。可以使用本身的工作分派上可用的選項套用預先定義的範圍，例如限制只有他信箱或通訊群組、 使用者。或者，您可以建立自訂的收件者或組態範圍並再將該範圍新增至角色指派。自訂範圍提供您更細緻掌控物件會包含在範圍中的方式。

您不能在相同的工作分派指定預先定義及自訂範圍。您也不能混合獨佔和定期在相同的工作分派的範圍。

每個角色指派只能有一個收件者範圍和一個組態範圍。如果您想要將一個以上的收件者範圍或一個組態範圍套用相同的管理角色的角色受託人，您必須建立多個角色指派。

未自訂或預先定義範圍、 角色指派限於本身角色所定義的收件者和設定範圍。這些範圍稱為隱含的範圍。預先定義或自訂的範圍沒有任何角色指派繼承其關聯的角色不明確的範圍。

如需範圍的詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

## 獨佔角色指派

當您建立獨佔範圍關聯的角色指派時建立獨佔角色指派。獨佔範圍類似規則範圍並啟用角色 assignees 管理符合獨佔範圍的收件者。不過，與一般範圍不同所有其他角色 assignees 拒絕讓您管理收件者，即使收件者會比對套用至其角色指派的範圍。當您想要限制誰可以管理幾個系統管理員的收件者可以是很有用。只有這些特定的系統管理員可以管理收件者及所有其他管理員已拒絕存取。

例如，假設下列情況：

  - John 是在 Contoso 主管。其信箱比對呼叫 VIP 使用者的相關聯的 VIP 受限制的獨佔指派獨佔範圍。

  - John 的信箱還包含在名爲 Redmond Users 的一般範圍中，該範圍與 Redmond Administration 一般指派相關聯。

  - Bill 是與 VIP Restricted 獨佔指派關聯的系統管理員。

  - Chris 是與 Redmond Administration 一般指派關聯的系統管理員。

因為 John 的信箱會比對 VIP 使用者獨佔範圍、 僅限 Bill 可以管理其信箱。即使 John 的信箱也會比對 Redmond 使用者一般範圍、 Chris 並未關聯 VIP 受限制的獨佔工作分派。因此， Exchange拒絕 Chris 管理 John 的信箱的能力。Chris 管理 John 的信箱，如 Chris 必須被指派獨佔工作分派具有獨佔範圍符合 John 的信箱。

如需相關資訊，請參閱[了解獨佔範圍](understanding-exclusive-scopes-exchange-2013-help.md)。


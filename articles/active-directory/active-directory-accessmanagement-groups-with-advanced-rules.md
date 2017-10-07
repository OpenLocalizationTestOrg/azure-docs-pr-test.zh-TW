---
title: "Azure Active Directory 中的物件屬性中的動態基礎 aaaPopulate 群組 |Microsoft 文件"
description: "如何為的 toocreate 進階規則的群組成員資格包括支援運算式規則運算子和參數。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 04813a42-d40a-48d6-ae96-15b7e5025884
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: fe22829118ed8f5137a619d93fa6f9bf80835863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="populate-groups-dynamically-based-on-object-attributes"></a>根據物件屬性以動態方式填入群組
hello Azure 傳統入口網站為您提供 hello 能力 tooenable 更複雜屬性為基礎群組動態成員資格 Azure Active Directory (Azure AD)。  

當使用者或裝置的變更的任何屬性，hello 系統才會評估所有的動態群組規則在目錄 toosee hello 變更會觸發任何群組加入或移除。 如果使用者或裝置滿足群組上的規則，就會將他們新增為該群組的成員。 如果它們不會再滿足 hello 規則，則會將它移除。

> [!NOTE]
> - 您可以為安全性群組或 Office 365 群組的動態成員資格設定規則。
>
> - 此功能的每個使用者成員加入的 tooat 至少有一個動態群組需要有 Azure AD Premium P1 的授權。
>
> - 您可以為裝置或使用者建立動態群組，但無法建立同時包含使用者和裝置物件的規則。

> - Hello 當時不可能 toocreate 裝置群組會根據擁有使用者的屬性。 裝置成員資格規則可以只參考立即屬性的裝置 hello 目錄中的物件。

## <a name="toocreate-an-advanced-rule"></a>toocreate 進階規則
1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**，然後開啟您的組織目錄。
2. 選取 hello**群組**索引標籤，然後再開啟 hello 想 tooedit 的群組。
3. 選取 hello**設定**索引標籤，選取 hello**進階的規則**選項，然後再輸入 hello 進階規則 hello 文字方塊中。

## <a name="constructing-hello-body-of-an-advanced-rule"></a>建構進階規則的 hello 主體
您可以建立 hello 群組的動態成員資格的 hello 進階的規則基本上是二進位運算式包含三個部分，並產生 true 或 false 的結果。 hello 三個部分是：

* 左側的參數
* 二進位運算子
* 右側的常數

完整的進階的規則看起來類似 toothis: (leftParameter binaryOperator"RightConstant")、 雙引號 hello 左右括號為必要的 hello 整個二進位運算式時，所需的 hello 右常數和 hello 語法hello user.property 是左的參數。 進階的規則可以包含一個以上的二進位運算式分隔 hello-和、-或，和-不是邏輯運算子。
hello 以下是正確建構的進階規則的範例：

* (user.department -eq "Sales") -or (user.department -eq "Marketing")
* (user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")

Hello 的支援的參數和運算式規則運算子的完整清單，請參閱下列各節。


請注意，hello 屬性必須在前面加上 hello 正確的物件類型： 使用者或裝置。
hello 以下規則會導致 hello 驗證失敗： 郵件-ne null

會 hello 正確的規則：

user.mail –ne null

hello hello 主體進階規則的總長度不能超過 2048年個字元。

> [!NOTE]
> 字串和 regex 運算都不區分大小寫。
> 包含引號 " 的字串應該使用 ' 字元逸出，例如 user.department -eq \`"Sales"。
> 只能將引號用於字串類型值，而且只能使用英文引號。
>
>

## <a name="supported-expression-rule-operators"></a>支援的運算式規則運算子
hello 下表列出所有 hello 支援運算式規則運算子的進階規則的 hello hello 主體中使用其語法 toobe:

| 運算子 | 語法 |
| --- | --- |
| Not Equals |-ne |
| Equals |-eq |
| Not Starts With |-notStartsWith |
| 開頭為 |-startsWith |
| Not Contains |-notContains |
| Contains |-contains |
| Not Match |-notMatch |
| Match |-match |
| 在 | -in |
| 不在 | -notIn |

## <a name="operator-precedence"></a>運算子優先順序

以下列出所有的運算子優先順序較低的 toohigher 從每、 同一行中的運算子會在相同的優先順序-任何-all-或-和-不-eq-ne-startsWith-notStartsWith-包含-notContains-符合 – notMatch--notIn 中

不管有沒有連字號前置詞，均可使用所有運算子。

請注意，不一定需要括號，您只需要 tooadd 括號優先順序，例如不符合您的需求時：

   user.department –eq "Marketing" –and user.country –eq "US"

相當於：

   (user.department –eq "Marketing") –and (user.country –eq "US")

## <a name="using-hello--in-and--notin-operators"></a>使用 hello-在和-notIn 運算子

如果您想要針對不同的值數目的使用者屬性 toocompare hello 值可以使用 hello-中或-notIn 運算子。 以下是範例-運算子中使用 hello:

    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]

請記下的 hello hello 使用"["和"]"hello 開頭和結尾 hello 值清單。 這個條件評估 tooTrue 的 hello user.department 等於 hello 清單中的 hello 值的其中一個值。

## <a name="query-error-remediation"></a>查詢錯誤補救
hello 下表列出可能出現的錯誤和如何 toocorrect 它們發生

| 查詢剖析錯誤 | 錯誤的使用方式 | 更正的使用方式 |
| --- | --- | --- |
| 錯誤：不支援屬性。 |(user.invalidProperty -eq "Value") |(user.department -eq "value")<br/>屬性應符合一項來自 hello[支援屬性清單](#supported-properties)。 |
| 錯誤：屬性不支援運算子。 |(user.accountEnabled -contains true) |(user.accountEnabled -eq true)<br/>屬性屬於布林類型。 使用支援的 hello 運算子 (-eq 或-ne) 的布林型別，從清單上方的 hello。 |
| 錯誤：查詢編譯錯誤。 |(user.department -eq "Sales") -and (user.department -eq "Marketing")(user.userPrincipalName -match "*@domain.ext") |(user.department -eq "Sales") -and (user.department -eq "Marketing")<br/>邏輯運算子應該符合其中一個支援的 hello 上述的屬性清單。(user.userPrincipalName-比對 」。 *@domain.ext") 或 (user.userPrincipalName-比對"@domain.ext$") 在規則運算式中的錯誤。 |
| 錯誤：二進位運算式不是正確的格式。 |(user.department –eq “Sales”) (user.department -eq "Sales")(user.department-eq"Sales") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>查詢有多個錯誤。 括號不在正確的位置。 |
| 錯誤：設定動態成員資格時發生未知的錯誤。 |(user.accountEnabled -eq "True" AND user.userPrincipalName -contains "alias@domain") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>查詢有多個錯誤。 括號不在正確的位置。 |

## <a name="supported-properties"></a>支援的屬性
hello 以下是您可以使用您的進階規則中的所有 hello 使用者內容：

### <a name="properties-of-type-boolean"></a>布林型別的屬性
允許的運算子

* -eq
* -ne

| 屬性 | 允許的值 | 使用量 |
| --- | --- | --- |
| accountEnabled |true false |user.accountEnabled -eq true |
| dirSyncEnabled |true false |user.dirSyncEnabled -eq true |

### <a name="properties-of-type-string"></a>字串類型的屬性
允許的運算子

* -eq
* -ne
* -notStartsWith
* -startsWith
* -contains
* -notContains
* -match
* -notMatch
* -in
* -notIn

| 屬性 | 允許的值 | 使用量 |
| --- | --- | --- |
| city |任何字串值或 $null |(user.city -eq "value") |
| country |任何字串值或 $null |(user.country -eq "value") |
| companyName | 任何字串值或 $null | (user.companyName -eq "value") |
| department |任何字串值或 $null |(user.department -eq "value") |
| displayName |任何字串值 |(user.displayName -eq "value") |
| facsimileTelephoneNumber |任何字串值或 $null |(user.facsimileTelephoneNumber -eq "value") |
| givenName |任何字串值或 $null |(user.givenName -eq "value") |
| jobTitle |任何字串值或 $null |(user.jobTitle -eq "value") |
| mail |任何字串值或 $null （hello 使用者 SMTP 位址） |(user.mail -eq "value") |
| mailNickName |任何字串值 （hello 使用者的郵件別名） |(user.mailNickName -eq "value") |
| mobile |任何字串值或 $null |(user.mobile -eq "value") |
| objectId |Hello 使用者物件的 GUID |(user.objectId -eq "1111111-1111-1111-1111-111111111111") |
| onPremisesSecurityIdentifier | 已從同步處理的使用者，在內部部署安全性識別碼 (SID) 內部 toohello 雲端。 |(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111") |
| passwordPolicies |None DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword |(user.passwordPolicies -eq "DisableStrongPassword") |
| physicalDeliveryOfficeName |任何字串值或 $null |(user.physicalDeliveryOfficeName -eq "value") |
| postalCode |任何字串值或 $null |(user.postalCode -eq "value") |
| preferredLanguage |ISO 639-1 code |(user.preferredLanguage -eq "en-US") |
| sipProxyAddress |任何字串值或 $null |(user.sipProxyAddress -eq "value") |
| state |任何字串值或 $null |(user.state -eq "value") |
| streetAddress |任何字串值或 $null |(user.streetAddress -eq "value") |
| surname |任何字串值或 $null |(user.surname -eq "value") |
| telephoneNumber |任何字串值或 $null |(user.telephoneNumber -eq "value") |
| usageLocation |兩個字母的國家 (地區) 代碼 |(user.usageLocation -eq "US") |
| userPrincipalName |任何字串值 |(user.userPrincipalName -eq "alias@domain") |
| userType |member guest $null |(user.userType -eq "Member") |

### <a name="properties-of-type-string-collection"></a>字串集合類型的屬性
允許的運算子

* -contains
* -notContains

| 屬性 | 允許的值 | 使用量 |
| --- | --- | --- |
| otherMails |任何字串值 |(user.otherMails -contains "alias@domain") |
| proxyAddresses |SMTP: alias@domain smtp: alias@domain |(user.proxyAddresses -contains "SMTP: alias@domain") |

## <a name="multi-value-properties"></a>多重值屬性
允許的運算子

* -任何 （滿足 hello 集合中的至少一個項目符合 hello 條件時）
* -（符合所有 hello 集合中的所有項目符合 hello 條件時）

| 屬性 | 值 | 使用量 |
| --- | --- | --- |
| assignedPlans |Hello 集合中的每個物件會公開下列字串屬性的 hello: capabilityStatus、 服務、 servicePlanId |user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled") |

多重值屬性是 hello 之物件的集合相同的型別。 您可以使用-任何和-所有運算子 tooapply 條件 tooone 或 hello 的所有集合中項目的 hello，分別。 例如：

assignedPlans 是多重值屬性，其中列出 toohello 使用者指派的所有服務方案。 hello，下列運算式會選取擁有 hello Exchange Online (計劃 2) 服務計劃也處於啟用狀態的使用者：

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

（hello Guid 識別碼識別 hello Exchange Online (計劃 2) 的服務方案）。

> [!NOTE]
> 這非常有用，如果您想要 tooidentify 所有使用者的 Office 365 （或其他 Microsoft 線上服務） 已啟用功能，如範例 tootarget 其與特定的一組原則。

hello 下列運算式會選取任何 hello （由服務名稱"SCO"識別） 的 Intune 服務相關聯的服務方案的所有使用者：
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a>使用 Null 值

toospecify 規則中的 null 值時，您可以使用"null"或 $null。 範例：

   user.mail –ne null is equivalent to user.mail –ne $null

## <a name="extension-attributes-and-custom-attributes"></a>擴充屬性和自訂屬性
動態成員資格規則支援擴充屬性和自訂屬性。

擴充屬性從內部部署 Windows Server AD 同步處理，並採取 hello 格式的"ExtensionAttributeX"，其中 X 等於 1-15。
以下是使用擴充屬性的規則範例：

(user.extensionAttribute15 -eq "Marketing")

從內部部署 Windows Server AD 或連接 SaaS 應用程式與 hello hello 格式的同步處理自訂屬性"user.extension_[GUID]\__ [Attribute]"，其中 [GUID] 是 hello 唯一識別項在 AAD 中的 hello 應用程式，AAD 和 [屬性] 中的建立的 hello 屬性為其建立 hello hello 屬性名稱。
以下是使用自訂屬性的規則範例：

user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  

hello 自訂屬性名稱可以在 hello 目錄藉由查詢使用者的屬性使用圖表總管，並搜尋 hello 屬性名稱。

## <a name="direct-reports-rule"></a>「直屬員工」規則
您可以建立一個群組，其中包含某位經理的所有直屬員工。 當 hello 經理的直屬員工在 hello 未來變更時，會自動調整 hello 群組的成員資格。

> [!NOTE]
> 1. Hello 規則 toowork，請確定 hello**經理識別碼**屬性已正確設定您的租用戶中的使用者。 您可以檢查 hello 目前值，使用者在其**設定檔索引標籤**。
> 2. 此規則只支援**直屬**員工。 它是目前不可能 toocreate 的巢狀階層，例如包含直屬員工和其報告的群組的群組。

**tooconfigure hello 群組**

1. 遵循的步驟 1-5 從區段[toocreate hello 進階規則](#to-create-the-advanced-rule)，然後選取**成員資格類型**的**動態使用者**。
2. 在 hello**動態成員資格規則**刀鋒視窗中，輸入 hello 規則以 hello，請使用下列語法：

    *Direct Reports for "{obectID_of_manager}"*

    有效規則的範例：
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is hello objectID of hello manager. hello object ID can be found on manager's **Profile tab**.
3. 在儲存之後 hello 規則，以 hello 的所有使用者都指定 toohello 群組會加入經理識別碼值。

## <a name="using-attributes-toocreate-rules-for-device-objects"></a>將裝置物件使用屬性 toocreate 規則
您也可以建立規則以在群組中選取成員資格的裝置物件。 可以使用下列裝置屬性的 hello:

| 屬性              | 允許的值                  | 使用量                                                       |
|-------------------------|---------------------------------|-------------------------------------------------------------|
| accountEnabled          | true false                      | (device.accountEnabled -eq true)                            |
| displayName             | 任何字串值                | (device.displayName -eq "Rob Iphone”)                       |
| deviceOSType            | 任何字串值                | (device.deviceOSType -eq "IOS")                             |
| deviceOSVersion         | 任何字串值                | (device.OSVersion -eq "9.1")                                |
| deviceCategory          | 任何字串值                | (device.deviceCategory -eq "")                              |
| deviceManufacturer      | 任何字串值                | (device.deviceManufacturer -eq "Microsoft")                 |
| deviceModel             | 任何字串值                | (device.deviceModel -eq "IPhone 7+")                        |
| deviceOwnership         | 任何字串值                | (device.deviceOwnership -eq "")                             |
| domainName              | 任何字串值                | (device.domainName -eq "contoso.com")                       |
| enrollmentProfileName   | 任何字串值                | (device.enrollmentProfileName -eq "")                       |
| isRooted                | true false                      | (device.deviceOSType -eq true)                              |
| managementType          | 任何字串值                | (device.managementType -eq "")                              |
| organizationalUnit      | 任何字串值                | (device.organizationalUnit -eq "")                          |
| deviceId                | 有效的 deviceId                | (device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d") |
| objectId                | 有效的 AAD objectId            | (device.objectId -eq "76ad43c9-32c5-45e8-a272-7b58b58f596d") |

> [!NOTE]
> 無法在 hello Azure 傳統入口網站中使用 hello 「 簡單規則 」 的下拉式清單中建立這些裝置的規則。
>
>

## <a name="next-steps"></a>後續步驟
這些文章提供有關 Azure Active Directory 的其他資訊。

* [疑難排解群組的動態成員資格](active-directory-accessmanagement-troubleshooting.md)
* [使用 Azure Active Directory 群組來管理存取 tooresources](active-directory-manage-groups.md)
* [設定群組設定的 Azure Active Directory Cmdlet](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

---
title: "Azure Active Directory 中的屬性對應的運算式 aaaWriting |Microsoft 文件"
description: "了解如何 toouse 運算式對應 tootransform 屬性值可接受的格式期間自動化佈建 Azure Active Directory 中的 SaaS 應用程式物件。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: b13c51cd-1bea-4e5e-9791-5d951a518943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: markvi
ms.openlocfilehash: caa0dd8144f6e5279a869e015ed75bd24169d585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a>在 Azure Active Directory 中撰寫屬性對應的運算式
當您設定佈建 tooa SaaS 應用程式時，其中一種您可以指定的屬性對應的 hello 類型是為運算式對應。 這些項目，您必須撰寫類似指令碼運算式，可讓您 tootransform 使用者資料成 hello SaaS 應用程式可以接受的格式。

## <a name="syntax-overview"></a>語法概觀
hello 進行屬性對應的運算式語法是讓人聯想到 Visual Basic for Applications (VBA) 函數。

* hello 整個運算式必須定義以函數名稱，後面接著括號括住的引數所組成： <br>
  *FunctionName(<<argument 1>>,<<argument N>>)*
* 您可以在函式內互相巢狀函式。 例如： <br> *FunctionOne(FunctionTwo(<<argument1>>))*
* 您可以將三種不同類型的引數傳入函式：
  
  1. 屬性，必須以方括弧括住。 例如：[attributeName]
  2. 字串常數，必須以雙引號括住。 例如："United States"
  3. 其他函式。 例如：FunctionOne(<<argument1>>, FunctionTwo(<<argument2>>))
* 字串常數，如果您需要反斜線 (\) 或引號 （"） 在 hello 字串中，則必須逸出 hello 反斜線 (\) 符號。 例如："公司名稱：\"Contoso\""

## <a name="list-of-functions"></a>函式的清單
[Append](#append) &nbsp;&nbsp;&nbsp;&nbsp; [FormatDateTime](#formatdatetime) &nbsp;&nbsp;&nbsp;&nbsp; [Join](#join) &nbsp;&nbsp;&nbsp;&nbsp; [Mid](#mid) &nbsp;&nbsp;&nbsp;&nbsp; [Not](#not) &nbsp;&nbsp;&nbsp;&nbsp; [將](#replace) &nbsp;&nbsp;&nbsp;&nbsp; [StripSpaces](#stripspaces) &nbsp;&nbsp;&nbsp;&nbsp; [Switch](#switch)

- - -
### <a name="append"></a>Append
**函式：**<br> Append(source, suffix)

**說明：**<br> 接受來源字串值，並且附加 hello 尾碼 toohello 結尾。

**參數：**<br> 

| 名稱 | 必要 / 重複 | 型別 | 注意事項 |
| --- | --- | --- | --- |
| **source** |必要 |String |通常從 hello 來源物件的 hello 屬性名稱 |
| **suffix** |必要 |String |hello 想 tooappend toohello 結尾 hello 來源值的字串。 |

- - -
### <a name="formatdatetime"></a>FormatDateTime
**函式：**<br>  FormatDateTime(source, inputFormat, outputFormat)

**說明：**<br> 從一種格式取出日期字串，並將它轉換成不同的格式。

**參數：**<br> 

| 名稱 | 必要 / 重複 | 型別 | 注意事項 |
| --- | --- | --- | --- |
| **source** |必要 |String |通常 hello hello 來源物件屬性的名稱。 |
| **inputFormat** |必要 |String |Hello 來源值的預期的格式。 如需支援的格式，請參閱 [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)。 |
| **outputFormat** |必要 |String |Hello 輸出日期的格式。 |

- - -
### <a name="join"></a>Join
**函式：**<br> Join(separator, source1, source2, …)

**說明：**<br> Join （） 是類似的 tooAppend()，不同之處在於它結合多個**來源**成單一字串，值的字串和每個值會分開**分隔符號**字串。

如果 hello 來源值的其中一個是多重值屬性，則該屬性中的每個值會聯結在一起，分隔 hello 分隔符號值。

**參數：**<br> 

| 名稱 | 必要 / 重複 | 型別 | 注意事項 |
| --- | --- | --- | --- |
| **separator** |必要 |String |它們會串連成一個字串時，字串會使用 tooseparate 來源值。 如果不需要分隔符號，可以是 ""。 |
| **source1  … sourceN ** |必要，變動次數 |String |字串值 toobe 聯結在一起。 |

- - -
### <a name="mid"></a>Mid
**函式：**<br> Mid(source, start, length)

**說明：**<br> 傳回子字串 hello 來源值。 子字串會包含只對某些 hello 來源字串 hello 字元的字串。

**參數：**<br> 

| 名稱 | 必要 / 重複 | 型別 | 注意事項 |
| --- | --- | --- | --- |
| **source** |必要 |String |通常 hello 屬性的名稱。 |
| **start** |必要 |integer |索引中 hello**來源**應該在此處開始的子字串的字串。 Hello 字串中的第一個字元必須索引為 1，第二個字元將會有索引 2，依此類推。 |
| **length** |必要 |integer |Hello 子字串的長度。 若長度結尾處之外 hello**來源**字串函數會傳回子字串從**啟動**索引到結尾**來源**字串。 |

- - -
### <a name="not"></a>否
**函式：**<br> Not(source)

**說明：**<br> 翻轉 hello 布林值為 hello**來源**。 如果 **source** 值為 "*True*"，則傳回 "*False*"。 反之則傳回 "*True*"。

**參數：**<br> 

| 名稱 | 必要 / 重複 | 型別 | 注意事項 |
| --- | --- | --- | --- |
| **source** |必要 |Boolean String |預期的 **source** 值為 "True" 或 "False"。 |

- - -
### <a name="replace"></a>將
**函式：**<br> ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)

**說明：**<br>
取代字串內的值。 此函數的作用視提供的 hello 參數而定：

* 提供 **oldValue** 和 **replacementValue** 時：
  
  * OldValue hello 來源中的所有項目取代 replacementValue
* 提供 **oldValue** 和 **template** 時：
  
  * 會取代所有出現的 hello **oldValue**在 hello**範本**以 hello**來源**值
* 提供 **oldValueRegexPattern**、**oldValueRegexGroupName**、**replacementValue** 時：
  
  * 取代相符的 oldValueRegexPattern replacementValue 與 hello 來源字串中的所有值
* 提供 **oldValueRegexPattern**、**oldValueRegexGroupName**、**replacementPropertyName** 時：
  
  * 如果 **source** 有值，則傳回 **source**
  * 如果**來源**沒有值，會使用**oldValueRegexPattern**和**oldValueRegexGroupName** tooextract 取代值，從與 hello 屬性**replacementPropertyName**。 Hello 結果為傳回取代值

**參數：**<br> 

| 名稱 | 必要 / 重複 | 型別 | 注意事項 |
| --- | --- | --- | --- |
| **source** |必要 |String |通常 hello hello 來源物件屬性的名稱。 |
| **oldValue** |選用 |String |值取代 toobe**來源**或**範本**。 |
| **regexPattern** |選用 |String |Regex 模式中被取代的 hello 值 toobe**來源**。 或者，使用 replacementPropertyName 時，模式 tooextract 從取代內容的值。 |
| **regexGroupName** |選用 |String |Hello 群組內的名稱**regexpattern 中**。 只有當使用了 replacementPropertyName 時，我們才會從取代屬性擷取此群組的值做為 replacementValue。 |
| **replacementValue** |選用 |String |新值 tooreplace 舊專案使用。 |
| **replacementAttributeName** |選用 |String |Hello 屬性 toobe 用於當來源沒有任何值的取代值的名稱。 |
| **template** |選用 |String |當**範本**提供值，則會尋找**oldValue**內部 hello 範本，並取代為原始值。 |

- - -
### <a name="stripspaces"></a>StripSpaces
**函式：**<br> StripSpaces(source)

**說明：**<br> 移除開頭空格 ("") 字元 hello 從來源字串。

**參數：**<br> 

| 名稱 | 必要 / 重複 | 型別 | 注意事項 |
| --- | --- | --- | --- |
| **source** |必要 |String |**來源**值 tooupdate。 |

- - -
### <a name="switch"></a>Switch
**函式：**<br> Switch(source, defaultValue, key1, value1, key2, value2, …)

**說明：**<br> 當 **source** 值符合某個 **key** 時，傳回該 **key** 的 **value**。 如果 **source** 值不符合任何 key，則傳回 **defaultValue**。  **key** 和 **value** 參數必須永遠成對出現。 hello 函式一律預期出現雙數的參數。

**參數：**<br> 

| 名稱 | 必要 / 重複 | 型別 | 注意事項 |
| --- | --- | --- | --- |
| **source** |必要 |String |**來源**值 tooupdate。 |
| **defaultValue** |選用 |String |預設值 toobe 來源不符合任何 key 時使用。 可以是空字串 ("")。 |
| **key** |必要 |String |**索引鍵**toocompare**來源**具有值。 |
| **value** |必要 |String |取代值 hello**來源**hello 相符的索引鍵。 |

## <a name="examples"></a>範例
### <a name="strip-known-domain-name"></a>刪去已知的網域名稱
您需要 toostrip 從使用者的電子郵件 tooobtain 使用者名稱的已知的網域名稱。 <br>
例如，如果"contoso.com"hello 網域，您可以使用下列運算式 hello:

**運算式：** <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

**範例輸入/輸出：** <br>

* **輸入** (mail)："john.doe@contoso.com"
* **輸出**："john.doe"

### <a name="append-constant-suffix-toouser-name"></a>附加常數後置詞 toouser 名稱
如果您使用 Salesforce 沙箱，您可能需要其他尾碼 tooall tooappend 您的使用者名稱才能同步處理它們。

**運算式：** <br>
`Append([userPrincipalName], ".test"))`

**範例輸入/輸出：** <br>

* **輸入**：(userPrincipalName)："John.Doe@contoso.com"
* **輸出**："John.Doe@contoso.com.test"

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a>串連部分名字和姓氏產生使用者別名
您必須利用使用者名字的前 3 個字母和使用者的姓氏的前 5 個字母的 toogenerate 使用者別名。

**運算式：** <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

**範例輸入/輸出：** <br>

* **輸入** (givenName)："John"
* **輸入** (surname)："Doe"
* **輸出**："JohDoe"

### <a name="output-date-as-a-string-in-a-certain-format"></a>以特定格式將日期輸出為字串
您想 toosend 日期 tooa SaaS 應用程式的特定格式。 <br>
例如，您會想 tooformat 日期 servicenow。

**運算式：** <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

**範例輸入/輸出：**

* **輸入** (extensionAttribute1)："20150123105347.1Z"
* **輸出**："2015-01-23"

### <a name="replace-a-value-based-on-predefined-set-of-options"></a>根據預先定義的一組選項取代值
您需要 toodefine hello 的時區時間 hello 使用者儲存在 Azure AD 中的 hello 狀態碼為基礎。 <br>
如果 hello 狀態碼不符合任何預先定義的 hello 選項，使用預設值是"Australia/Sydney"。

**運算式：** <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

**範例輸入/輸出：**

* **輸入** (state)："QLD"
* **輸出**："Australia/Brisbane"

## <a name="related-articles"></a>相關文章
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [自動化使用者佈建/取消佈建 tooSaaS 應用程式](active-directory-saas-app-provisioning.md)
* [自訂使用者佈建的屬性對應](active-directory-saas-customizing-attribute-mappings.md)
* [適用於使用者佈建的範圍篩選器](active-directory-saas-scoping-filters.md)
* [使用 SCIM tooenable 自動佈建的 Azure Active Directory tooapplications 來自使用者和群組](active-directory-scim-provisioning.md)
* [帳戶佈建通知](active-directory-saas-account-provisioning-notifications.md)
* [如何教學課程清單 tooIntegrate SaaS 應用程式](active-directory-saas-tutorial-list.md)


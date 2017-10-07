---
title: "Azure AD Connect 同步：函式參考 | Microsoft Docs"
description: "Azure AD Connect 同步處理中宣告式佈建運算式的參考。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a>Azure AD Connect 同步處理：函式參考
在 Azure AD Connect，函式會是同步處理期間使用的 toomanipulate 屬性值。  
使用下列格式的 hello 表示 hello 的 hello 函式的語法：  
`<output type> FunctionName(<input type> <position name>, ..)`

如果函式是多載的且接受多種語法，即會列出所有的有效語法。  
hello 函式強型別，並確認 hello 類型傳入的相符項目記錄的 hello 型別。  
如果 hello 類型不符合，則會擲回錯誤。

hello，請使用下列語法以表示 hello 類型：

*  – 二進位
*  – 布林值
*  – UTC 日期/時間
*  – 已知常數的列舉
* **exp** – 運算式，也就是預期 tooevaluate tooa 布林值
* **mvbin** – 多重值的二進位
* **mvstr** – 多重值的字串
* **mvref** – 多重值的參考
* **num** – 數值
* **ref** – 參考
* **str** – 字串
* **var** – (幾乎) 任何其他類型的變體
* **void** – 不會傳回值

hello 函式與 hello 類型**mvbin**， **mvstr**，和**mvref**只能搭配多重值屬性。 類型為 **bin**、**str** 和 **ref** 的函式可用於單一值和多重值的屬性。

## <a name="functions-reference"></a>函式參考
| 函數的清單 |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **憑證** | | | | |
| [CertExtensionOids](#certextensionoids) |[CertFormat](#certformat) |[CertFriendlyName](#certfriendlyname) |[CertHashString](#certhashstring) | |
| [CertIssuer](#certissuer) |[CertIssuerDN](#certissuerdn) |[CertIssuerOid](#certissueroid) |[CertKeyAlgorithm](#certkeyalgorithm) | |
| [CertKeyAlgorithmParams](#certkeyalgorithmparams) |[CertNameInfo](#certnameinfo) |[CertNotAfter](#certnotafter) |[CertNotBefore](#certnotbefore) | |
| [CertPublicKeyOid](#certpublickeyoid) |[CertPublicKeyParametersOid](#certpublickeyparametersoid) |[CertSerialNumber](#certserialnumber) |[CertSignatureAlgorithmOid](#certsignaturealgorithmoid) | |
| [CertSubject](#certsubject) |[CertSubjectNameDN](#certsubjectnamedn) |[CertSubjectNameOid](#certsubjectnameoid) |[CertThumbprint](#certthumbprint) | |
[ CertVersion](#certversion) |[IsCert](#iscert) | | | |
| **轉換** | | | | |
| [CBool](#cbool) |[CDate](#cdate) |[CGuid](#cguid) |[ConvertFromBase64](#convertfrombase64) | |
| [ConvertToBase64](#converttobase64) |[ConvertFromUTF8Hex](#convertfromutf8hex) |[ConvertToUTF8Hex](#converttoutf8hex) |[CNum](#cnum) | |
| [CRef](#cref) |[CStr](#cstr) |[StringFromGuid](#StringFromGuid) |[StringFromSid](#stringfromsid) | |
| **日期 / 時間** | | | | |
| [DateAdd](#dateadd) |[DateFromNum](#datefromnum) |[FormatDateTime](#formatdatetime) |[Now](#now) | |
| [NumFromDate](#numfromdate) | | | | |
| **目錄** | | | | |
| [DNComponent](#dncomponent) |[DNComponentRev](#dncomponentrev) |[EscapeDNComponent](#escapedncomponent) | | |
| **評估** | | | | |
| [IsBitSet](#isbitset) |[IsDate](#isdate) |[IsEmpty](#isempty) |[IsGuid](#isguid) | |
| [IsNull](#isnull) |[IsNullOrEmpty](#isnullorempty) |[IsNumeric](#isnumeric) |[IsPresent](#ispresent) | |
| [IsString](#isstring) | | | | |
| **數學運算** | | | | |
| [BitAnd](#bitand) |[BitOr](#bitor) |[RandomNum](#randomnum) | | |
| **多重值** | | | | |
| [Contains](#contains) |[Count](#count) |[Item](#item) |[ItemOrNull](#itemornull) | |
| [Join](#join) |[RemoveDuplicates](#removeduplicates) |[Split](#split) | | |
| **程式流程** | | | | |
| [Error](#error) |[IIF](#iif) |[選取](#select) |[Switch](#switch) | |
| [其中](#where) |[With](#with) | | | |
| **文字** | | | | |
| [GUID](#guid) |[InStr](#instr) |[InStrRev](#instrrev) |[LCase](#lcase) | |
| [Left](#left) |[Len](#len) |[LTrim](#ltrim) |[Mid](#mid) | |
| [PadLeft](#padleft) |[PadRight](#padright) |[PCase](#pcase) |[Replace](#replace) | |
| [ReplaceChars](#replacechars) |[Right](#right) |[RTrim](#rtrim) |[Trim](#trim) | |
| [UCase](#ucase) |[Word](#word) | | | |

- - -
### <a name="bitand"></a>BitAnd
**說明：**  
hello BitAnd 函式會設定指定的位元的值。

**語法：**  
`num BitAnd(num value1, num value2)`

* value1，value2：應該使用 AND 連結在一起的數值

**備註：**  
此函式會將這兩個參數 toohello 二進位表示，轉換和位元設定為：

* 0-如果一或兩個 hello 對應位元*遮罩*和*旗標*為 0
* 1-如果兩個 hello 對應位元都是 1。

換句話說，它會傳回 0 在所有情況下，除非 hello 這兩個參數的對應位元是 1。

**範例：**  
`BitAnd(&HF, &HF7)`  
因為十六進位"F"和"F7"評估 toothis 值會傳回 7。

- - -
### <a name="bitor"></a>BitOr
**說明：**  
hello BitOr 函式會設定指定的位元的值。

**語法：**  
`num BitOr(num value1, num value2)`

* value1，value2：應該使用 OR 連結在一起的數值

**備註：**  
此函式會將這兩個參數 toohello 二進位表示，轉換，並設定位元 too1，如果一或兩個 hello 遮罩和旗標的對應位元為 1 和 too0 如果兩個 hello 對應位元為 0。 換句話說，它會傳回 1 在所有情況下，除了 hello 這兩個參數的對應位元是 0。

- - -
### <a name="cbool"></a>CBool
**說明：**  
hello CBool 函式會傳回布林值根據 hello 評估運算式

**語法：**  
`bool CBool(exp Expression)`

**備註：**  
如果 hello 運算式會評估 tooa 則為非零值，然後 CBool 會傳回 True，否則它會傳回 False。

**範例：**  
`CBool([attrib1] = [attrib2])`  

傳回 True，如果兩個屬性都有 hello 相同的值。

- - -
### <a name="cdate"></a>CDate
**說明：**  
hello CDate 函數從字串傳回 UTC DateTime。 DateTime 不是同步處理中的原生屬性類型，但有部分函式會用到。

**語法：**  
`dt CDate(str value)`

* Value：包含日期、時間和選擇性時區的字串

**備註：**  
hello 傳回字串一律是 utc 格式。

**範例：**  
`CDate([employeeStartTime])`  
傳回根據 hello 員工的開始時間的 DateTime

`CDate("2013-01-10 4:00 PM -8")`  
傳回代表 "2013-01-11 12:00 AM" 的 DateTime








- - -
### <a name="certextensionoids"></a>CertExtensionOids
**說明：**  
傳回 hello 所有 hello 重要的延伸的憑證物件的 Oid 值。

**語法：**  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certformat"></a>CertFormat
**說明：**  
傳回 hello hello 格式的這個 X.509v3 憑證的名稱。

**語法：**  
`str CertFormat(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certfriendlyname"></a>CertFriendlyName
**說明：**  
傳回 hello 別名相關聯的憑證。

**語法：**  
`str CertFriendlyName(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certhashstring"></a>CertHashString
**說明：**  
傳回做為十六進位字串 hello hello X.509v3 憑證的 SHA1 雜湊值。

**語法：**  
`str CertHashString(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certissuer"></a>CertIssuer
**說明：**  
傳回 hello hello 憑證授權單位發出 hello X.509v3 憑證的名稱。

**語法：**  
`str CertIssuer(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certissuerdn"></a>CertIssuerDN
**說明：**  
傳回 hello hello 憑證簽發者辨別的名稱。

**語法：**  
`str CertIssuerDN(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certissueroid"></a>CertIssuerOid
**說明：**  
傳回 hello hello 憑證簽發者的 Oid。

**語法：**  
`str CertIssuerOid(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certkeyalgorithm"></a>CertKeyAlgorithm
**說明：**  
傳回這個 X.509v3 憑證做為字串的 hello 金鑰演算法資訊。

**語法：**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certkeyalgorithmparams"></a>CertKeyAlgorithmParams
**說明：**  
傳回做為十六進位字串的 hello hello X.509v3 憑證金鑰演算法參數。

**語法：**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certnameinfo"></a>CertNameInfo
**說明：**  
傳回 hello 主旨和簽發者名稱從憑證。

**語法：**  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。
*   X509NameType: hello X509NameType hello 主體值。
*   includesIssuerName: true tooinclude hello 簽發者名稱。否則為 false。

- - -
### <a name="certnotafter"></a>CertNotAfter
**說明：**  
傳回 hello 日期之後，憑證便不再有效的當地時間。

**語法：**  
`dt CertNotAfter(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certnotbefore"></a>CertNotBefore
**說明：**  
憑證生效的當地時間傳回 hello 日期。

**語法：**  
`dt CertNotBefore(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certpublickeyoid"></a>CertPublicKeyOid
**說明：**  
傳回 hello hello hello X.509v3 憑證公開金鑰的 Oid。

**語法：**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certpublickeyparametersoid"></a>CertPublicKeyParametersOid
**說明：**  
傳回 hello hello 公開金鑰參數 hello X.509v3 憑證的 Oid。

**語法：**  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certserialnumber"></a>CertSerialNumber
**說明：**  
傳回 hello 序號 hello X.509v3 憑證。

**語法：**  
`str CertSerialNumber(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certsignaturealgorithmoid"></a>CertSignatureAlgorithmOid
**說明：**  
傳回 hello hello 演算法的 Oid 用 toocreate hello 簽章的憑證。

**語法：**  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certsubject"></a>CertSubject
**說明：**  
取得 hello 來自憑證的主旨辨別的名稱。

**語法：**  
`str CertSubject(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certsubjectnamedn"></a>CertSubjectNameDN
**說明：**  
傳回 hello 來自憑證的主旨辨別的名稱。

**語法：**  
`str CertSubjectNameDN(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certsubjectnameoid"></a>CertSubjectNameOid
**說明：**  
傳回 hello hello 來自憑證的主體名稱的 Oid。

**語法：**  
`str CertSubjectNameOid(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certthumbprint"></a>CertThumbprint
**說明：**  
傳回 hello 憑證的指紋。

**語法：**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="certversion"></a>CertVersion
**說明：**  
傳回 hello X.509 格式版本的憑證。

**語法：**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。

- - -
### <a name="cguid"></a>CGuid
**說明：**  
hello CGuid 函數將 GUID tooits 二進位表示法 hello 字串表示轉換。

**語法：**  
`bin CGuid(str GUID)`

* 使用此模式格式化的字串：xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 或 {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

- - -
### <a name="contains"></a>Contains
**說明：**  
hello Contains 函數內尋找字串的多重值屬性

**語法：**  
`num Contains (mvstring attribute, str search)` - 區分大小寫  
`num Contains (mvstring attribute, str search, enum Casetype)`  
`num Contains (mvref attribute, str search)` - 區分大小寫

* 屬性： hello 多重值的屬性 toosearch。
* 搜尋： toofind hello 屬性中的字串。
* Casetype：CaseInsensitive 或 CaseSensitive。

其中 hello 找不到字串 hello 多重值屬性中傳回的索引。 如果找不到 hello 字串，則傳回 0。

**備註：**  
對於多重值的字串屬性 hello 搜尋會尋找 hello 值子字串。  
若為參考屬性 hello 搜尋的字串必須完全符合 hello 值 toobe 被視為相符。

**範例：**  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
如果 hello proxyAddresses 屬性具有主要電子郵件地址 (以大寫"SMTP:")，然後傳回 hello proxyAddress 屬性，否則會傳回錯誤。

- - -
### <a name="convertfrombase64"></a>ConvertFromBase64
**說明：**  
hello ConvertFromBase64 函數將 hello 指定 base64 編碼值 tooa 規則的字串。

**語法：**  
`str ConvertFromBase64(str source)` - 假設使用 Unicode 進行編碼  
`str ConvertFromBase64(str source, enum Encoding)`

* source：Base64 編碼的字串  
* Encoding：Unicode、ASCII、UTF8

**範例**  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

這兩個範例都會傳回 "*Hello world!*"

- - -
### <a name="convertfromutf8hex"></a>ConvertFromUTF8Hex
**說明：**  
hello ConvertFromUTF8Hex 函數將 hello 指定的 UTF8 十六進位編碼值 tooa 字串。

**語法：**  
`str ConvertFromUTF8Hex(str source)`

* source：UTF8 2 個位元組的編碼字串

**備註：**  
hello 差異此函式和 ConvertFromBase64([],UTF8) hello 結果是易記的 hello DN 屬性。  
Azure Active Directory 會使用此格式做為 DN。

**範例：**  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
傳回 "*Hello world!*"

- - -
### <a name="converttobase64"></a>ConvertToBase64
**說明：**  
hello ConvertToBase64 函數將轉換字串 tooa Unicode base64 字串。  
將 hello 值陣列使用 base-64 位數編碼的整數 tooits 相等字串表示的轉換。

**語法：**  
`str ConvertToBase64(str source)`

**範例：**  
`ConvertToBase64("Hello world!")`  
傳回 "SABlAGwAbABvACAAdwBvAHIAbABkACEA"

- - -
### <a name="converttoutf8hex"></a>ConvertToUTF8Hex
**說明：**  
hello ConvertToUTF8Hex 函數將轉換字串 tooa UTF8 十六進位編碼值。

**語法：**  
`str ConvertToUTF8Hex(str source)`

**備註：**  
Azure Active directory 使用此函式的 hello 輸出格式作為 DN 屬性格式。

**範例：**  
`ConvertToUTF8Hex("Hello world!")`  
傳回 48656C6C6F20776F726C6421

- - -
### <a name="count"></a>Count
**說明：**  
hello Count 函數傳回多重值屬性中的 hello 項目數

**語法：**  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a>CNum
**說明：**  
hello CNum 函數接受字串，並傳回數值資料類型。

**語法：**  
`num CNum(str value)`

- - -
### <a name="cref"></a>CRef
**說明：**  
轉換字串 tooa 參考屬性

**語法：**  
`ref CRef(str value)`

**範例：**  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a>CStr
**說明：**  
hello CStr 函式將 tooa 字串資料類型轉換。

**語法：**  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* value：可以是數值、參考屬性或布林值。

**範例：**  
`CStr([dn])`  
可能傳回 "cn=Joe,dc=contoso,dc=com"

- - -
### <a name="dateadd"></a>DateAdd
**說明：**  
傳回包含日期 toowhich 已加入指定的時間間隔。

**語法：**  
`dt DateAdd(str interval, num value, dt date)`

* 間隔： 字串是 hello 想 tooadd 的時間間隔的運算式。 hello 字串必須有一個 hello 下列值：
  * yyyy 年
  * q 季
  * m 月
  * y 一年中第幾天
  * d 日
  * w 工作日
  * ww 周
  * h 小時
  * n 分鐘
  * s 秒
* 值： hello 數目要 tooadd 的單位。 它可以是正數 （tooget 日期在未來的 hello） 或負 （tooget 日期在過去的 hello）。
* 日期： 日期時間表示的日期 toowhich hello 間隔加入。

**範例：**  
`DateAdd("m", 3, CDate("2001-01-01"))`  
新增 3 個月，並傳回代表 "2001-04-01" 的 DateTime。

- - -
### <a name="datefromnum"></a>DateFromNum
**說明：**  
hello DateFromNum 函數將 AD 日期格式 tooa DateTime 型別中的值轉換。

**語法：**  
`dt DateFromNum(num value)`

**範例：**  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
傳回代表 2012-01-01 23:00:00 的 DateTime

- - -
### <a name="dncomponent"></a>DNComponent
**說明：**  
hello DNComponent 函數會傳回指定之 DN 元件謔韺 hello 值。

**語法：**  
`str DNComponent(ref dn, num ComponentNumber)`

* dn: hello 參考屬性 toointerpret
* 在 hello DN tooreturn ComponentNumber: hello 元件

**範例：**  
`DNComponent([dn],1)`  
如果 dn 為 "cn=Joe,ou=…"，就會傳回 Joe

- - -
### <a name="dncomponentrev"></a>DNComponentRev
**說明：**  
hello DNComponentRev 函數會傳回指定之 DN 元件從右邊 （hello 尾端） hello 值。

**語法：**  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* dn: hello 參考屬性 toointerpret
* ComponentNumber-hello DN tooreturn 中的 hello 元件
* Options：DC - 忽略所有含 "dc=" 的元件

**範例：**  
如果 dn 是 "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com"，則  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
兩者都傳回 US。

- - -
### <a name="error"></a>Error
**說明：**  
hello 錯誤函式是使用的 tooreturn 自訂錯誤。

**語法：**  
`void Error(str ErrorMessage)`

**範例：**  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
如果 hello 屬性 accountName 不存在，擲回錯誤，hello 物件上。

- - -
### <a name="escapedncomponent"></a>EscapeDNComponent
**說明：**  
hello EscapeDNComponent 函數接受 DN 的一個元件，並能夠以 LDAP 表示逸出。

**語法：**  
`str EscapeDNComponent(str value)`

**範例：**  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
可確保即使 hello displayName 屬性具有 LDAP 中必須逸出的字元，可以在 LDAP 目錄中建立 hello 物件。

- - -
### <a name="formatdatetime"></a>FormatDateTime
**說明：**  
hello FormatDateTime 函式是使用的 tooformat DateTime tooa 字串與指定的格式

**語法：**  
`str FormatDateTime(dt value, str format)`

* 值： hello 日期時間格式的值
* 格式： 字串，表示要 hello 格式 tooconvert。

**備註：**  
hello 可能的值為 hello 格式可以在這裡找到：[使用者定義日期/時間格式 （Format 函數）](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)

**範例：**  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
結果是 "2007-12-25"。

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
會產生 "20140905081453.0Z"

- - -
### <a name="guid"></a>GUID
**說明：**  
hello 函式 GUID 會產生新的隨機 GUID

**語法：**  
`str GUID()`

- - -
### <a name="iif"></a>IIF
**說明：**  
hello IIF 函數傳回的一組指定的條件為基礎的可能值的其中一個。

**語法：**  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* 條件： 任何值或運算式可以評估 tootrue 或 false。
* valueIfTrue: hello tootrue 評估 hello 條件，如果傳回值。
* valueIfFalse: hello toofalse 評估 hello 條件，如果傳回值。

**範例：**  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 如果 hello 使用者是實習生，會傳回 hello 別名"t-"的使用者加入 toohello 開頭，否則傳回現況的 hello 使用者的別名。

- - -
### <a name="instr"></a>InStr
**說明：**  
hello InStr 函數在字串中尋找 hello 的子字串的第一個出現項目

**語法：**  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* stringcheck: toobe 搜尋的字串
* stringmatch: toobe 找到的字串
* 開始： 開始位置 toofind hello 子字串
* compare：vbTextCompare 或 vbBinaryCompare

**備註：**  
傳回 hello 位置找 hello substring 或 0 如果找不到。

**範例：**  
`InStr("hello quick brown fox","quick")`  
/ / 評估 too5

`InStr("repEated","e",3,vbBinaryCompare)`  
評估 too7

- - -
### <a name="instrrev"></a>InStrRev
**說明：**  
hello InStrRev 函數在字串中尋找子字串 hello 最後一個項目

**語法：**  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* stringcheck: toobe 搜尋的字串
* stringmatch: toobe 找到的字串
* 開始： 開始位置 toofind hello 子字串
* compare：vbTextCompare 或 vbBinaryCompare

**備註：**  
傳回 hello 位置找 hello substring 或 0 如果找不到。

**範例：**  
`InStrRev("abbcdbbbef","bb")`  
傳回 7

- - -
### <a name="isbitset"></a>IsBitSet
**說明：**  
hello IsBitSet 函數測試的位元設定

**語法：**  
`bool IsBitSet(num value, num flag)`

* 值： 數值。 flag： 具有 hello 的數字值的位元 toobe 評估

**範例：**  
`IsBitSet(&HF,4)`  
因為以十六進位值"F"hello 設定位元"4"，則傳回 True

- - -
### <a name="isdate"></a>IsDate
**說明：**  
如果 hello 運算式可以評估為 DateTime 型別，然後 hello IsDate 函數會評估 tooTrue。

**語法：**  
`bool IsDate(var Expression)`

**備註：**  
如果 cdate （） 可以成功，請使用 toodetermine。

- - -
### <a name="iscert"></a>IsCert
**說明：**  
如果.NET X509Certificate2 憑證物件可以序列化 hello 未經處理資料，則傳回 true。

**語法：**  
`bool CertThumbprint(binary certificateRawData)`  
*   certificateRawData：X.509 憑證的位元組陣列表示。 編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。
- - -
### <a name="isempty"></a>IsEmpty
**說明：**  
如果 hello 屬性存在於 hello CS 或 MV 中，但會評估 tooan 空字串，然後 hello IsEmpty 函數會評估 tooTrue。

**語法：**  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a>IsGuid
**說明：**  
如果 hello 字串無法轉換的 tooa GUID，IsGuid 函數會 hello 評估 tootrue。

**語法：**  
`bool IsGuid(str GUID)`

**備註：**  
GUID 定義為下列其中一種模式的字串： xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 或 {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

如果 cguid （） 可以成功，請使用 toodetermine。

**範例：**  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
如果 hello StrAttribute 是 GUID 格式，傳回的二進位表示法，否則會傳回 Null。

- - -
### <a name="isnull"></a>IsNull
**說明：**  
如果 hello 運算式評估 tooNull，則 hello IsNull 函數會傳回 true。

**語法：**  
`bool IsNull(var Expression)`

**備註：**  
屬性，Null 表示 hello hello 屬性不存在。

**範例：**  
`IsNull([displayName])`  
如果 hello 屬性不存在於 hello CS 或 MV 中，則傳回 True。

- - -
### <a name="isnullorempty"></a>IsNullOrEmpty
**說明：**  
如果 hello 運算式為 null 或空字串，則 hello IsNullOrEmpty 函數會傳回 true。

**語法：**  
`bool IsNullOrEmpty(var Expression)`

**備註：**  
屬性，這會評估 tooTrue 如果 hello 屬性不存在或雖然存在但為空字串。  
此函式的 hello 反向名為 IsPresent。

**範例：**  
`IsNullOrEmpty([displayName])`  
如果 hello 屬性不存在，或為空字串 hello CS 或 MV 中的，則傳回 True。

- - -
### <a name="isnumeric"></a>IsNumeric
**說明：**  
hello IsNumeric 函數傳回布林值，指出是否可以當做數字 類型中評估運算式。

**語法：**  
`bool IsNumeric(var Expression)`

**備註：**  
如果 cnum （） 可以成功 tooparse hello 運算式，請使用 toodetermine。

- - -
### <a name="isstring"></a>IsString
**說明：**  
如果 hello 運算式可以評估的 tooa 字串類型，則 hello 別，IsString 函數會評估 tooTrue。

**語法：**  
`bool IsString(var expression)`

**備註：**  
如果 cstr （） 可以是成功 tooparse hello 運算式，請使用 toodetermine。

- - -
### <a name="ispresent"></a>IsPresent
**說明：**  
如果 hello 運算式評估 tooa 不是 Null，而不是空的字串，然後 hello 的 IsPresent 函數會傳回 true。

**語法：**  
`bool IsPresent(var expression)`

**備註：**  
此函式的 hello 反向名為 IsNullOrEmpty。

**範例：**  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a>Item
**說明：**  
hello Item 函數從多重值字串/屬性，傳回一個項目。

**語法：**  
`var Item(mvstr attribute, num index)`

* attribute：多重值的屬性
* 索引： hello 多重值字串中的索引 tooan 項目。

**備註：**  
hello Item 函數適合與 hello Contains 函數一起因為 hello 第二個函式傳回 hello 多重值屬性中的 hello 索引 tooan 項目。

如果索引超出範圍，即會擲回錯誤。

**範例：**  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
傳回 hello 主要電子郵件地址。

- - -
### <a name="itemornull"></a>ItemOrNull
**說明：**  
hello ItemOrNull 函數從多重值字串/屬性，傳回一個項目。

**語法：**  
`var ItemOrNull(mvstr attribute, num index)`

* attribute：多重值的屬性
* 索引： hello 多重值字串中的索引 tooan 項目。

**備註：**  
hello ItemOrNull 函數適合與 Contains 函數 hello 因為 hello 第二個函式傳回 hello 多重值屬性中的 hello 索引 tooan 項目。

如果索引超出範圍，則會傳回 Null 值。

- - -
### <a name="join"></a>Join
**說明：**  
hello Join 函數接受多重值的字串，並傳回單一值的字串與指定插入每個項目之間的分隔符號。

**語法：**  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* 屬性： 多重值的屬性包含字串 toobe 聯結。
* 分隔符號： 任何字串，傳回字串 hello 中的，使用的 tooseparate hello 子字串。 如果省略，hello 空格字元 ("") 會使用。 如果 Delimiter 是零長度字串 ("") 或執行任何動作，而不使用分隔符號串連 hello 清單中的所有項目。

**備註**  
沒有 hello Join 和 Split 函數之間的同位檢查。 hello Join 函數接受字串陣列，並結合使用分隔符號字串，tooreturn 單一字串。 hello Split 函數接受字串，並分隔在 hello 分隔符號，tooreturn 字串陣列。 不過，主要的差別是 Join 可以使用任何分隔符號字串來串連字串，Split 只能使用單一字元分隔符號來分隔字串。

**範例：**  
`Join([proxyAddresses],",")`  
可能傳回："SMTP:john.doe@contoso.com,smtp:jd@contoso.com"

- - -
### <a name="lcase"></a>LCase
**說明：**  
hello LCase 函數將字串 toolower 案例中的所有字元都轉換。

**語法：**  
`str LCase(str value)`

**範例：**  
`LCase("TeSt")`  
傳回 "test"。

- - -
### <a name="left"></a>Left
**說明：**  
hello Left 的函數從字串 hello 左側傳回指定的字元數。

**語法：**  
`str Left(str string, num NumChars)`

* 字串： hello tooreturn 字元字串
* NumChars： 數字，識別 hello 從 hello 開頭 （左邊） 字串的字元 tooreturn 數目

**備註：**  
字串，包含 hello 前面 numChars 個字元字串中：

* 如果 numChars = 0，會傳回空字串。
* 如果 numChars < 0，會傳回輸入字串。
* 如果 string 為 Null，會傳回空字串。

如果字串包含字元少於 numChars 中指定的 hello 數字，則會傳回字串的相同 toostring （也就，包含參數 1 中的所有字元）。

**範例：**  
`Left("John Doe", 3)`  
傳回 "Joh"。

- - -
### <a name="len"></a>Len
**說明：**  
hello Len 函數會傳回字串中的字元數。

**語法：**  
`num Len(str value)`

**範例：**  
`Len("John Doe")`  
傳回 8

- - -
### <a name="ltrim"></a>LTrim
**說明：**  
hello LTrim 函數從字串中移除開頭空白字元。

**語法：**  
`str LTrim(str value)`

**範例：**  
`LTrim(" Test ")`  
傳回 "Test"

- - -
### <a name="mid"></a>Mid
**說明：**  
hello Mid 函數從字串中指定位置傳回指定的字元數。

**語法：**  
`str Mid(str string, num start, num NumChars)`

* 字串： hello tooreturn 字元字串
* 開始： 數字，識別 hello 開始 tooreturn 字元字串中的位置
* NumChars： 數字，識別 hello 字元 tooreturn 從字串中的位置數目

**備註：**  
從 string 中的位置 start 開始傳回 numChars 個字元。  
包含從 string 中的位置 start 起算的 numChars 個字元的字串：

* 如果 numChars = 0，會傳回空字串。
* 如果 numChars < 0，會傳回輸入字串。
* 如果啟動 > hello 字串的長度，傳回輸入的字串。
* 如果 start < = 0，會傳回輸入字串。
* 如果 string 為 Null，會傳回空字串。

如果 string 中從位置 start 起算所剩餘的字元數不足 numChar 個字元，即會盡可能地傳回許多字元。

**範例：**  
`Mid("John Doe", 3, 5)`  
傳回 "hn Do"。

`Mid("John Doe", 6, 999)`  
傳回 "Doe"

- - -
### <a name="now"></a>Now
**說明：**  
hello 現在函式會傳回指定 hello 目前的日期和時間，根據 tooyour 電腦的系統日期和時間的日期時間。

**語法：**  
`dt Now()`

- - -
### <a name="numfromdate"></a>NumFromDate
**說明：**  
hello NumFromDate 函數傳回 AD 日期格式的日期。

**語法：**  
`num NumFromDate(dt value)`

**範例：**  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
傳回 129699324000000000

- - -
### <a name="padleft"></a>PadLeft
**說明：**  
hello PadLeft 函式左填補字串 tooa 指定使用提供的填補字元的長度。

**語法：**  
`str PadLeft(str string, num length, str padCharacter)`

* 字串： hello 字串 toopad。
* 長度： 整數，代表 hello 預期字串的長度。
* padCharacter： 字串，其中包含單一字元 toouse 為 hello 填補字元

**備註：**

* 如果字串 hello 長度小於 length，padCharacter 則重複地附加的 toohello 開頭 （左邊） 字串的長度等於 toolength 之前。
* PadCharacter 可以是空白字元，但不能是 Null 值。
* 如果字串 hello 長度大於長度等於 tooor，字串會原封不動地傳回。
* 如果字串的長度大於或等於 toolength，則傳回字串的相同 toostring。
* 如果字串 hello 長度小於 length，hello 的新字串所需長度會傳回包含以 padCharacter 填補的字串。
* 如果字串為 null，hello 函式會傳回空字串。

**範例：**  
`PadLeft("User", 10, "0")`  
傳回 "000000User"。

- - -
### <a name="padright"></a>PadRight
**說明：**  
hello PadRight 函數的右填補字串 tooa 指定使用提供的填補字元的長度。

**語法：**  
`str PadRight(str string, num length, str padCharacter)`

* 字串： hello 字串 toopad。
* 長度： 整數，代表 hello 預期字串的長度。
* padCharacter： 字串，其中包含單一字元 toouse 為 hello 填補字元

**備註：**

* 如果 hello 字串的長度小於 length，則 padCharacter 是字串的重複地附加的 toohello 尾端 （右邊） 直到長度等於 toolength。
* PadCharacter 可以是空白字元，但不能是 Null 值。
* 如果字串 hello 長度大於長度等於 tooor，字串會原封不動地傳回。
* 如果字串的長度大於或等於 toolength，則傳回字串的相同 toostring。
* 如果字串 hello 長度小於 length，hello 的新字串所需長度會傳回包含以 padCharacter 填補的字串。
* 如果字串為 null，hello 函式會傳回空字串。

**範例：**  
`PadRight("User", 10, "0")`  
傳回 "User000000"。

- - -
### <a name="pcase"></a>PCase
**說明：**  
hello PCase 函數將轉換 hello 第一個字元在字串 tooupper 的情況下，每個空格分隔字組和其他所有字元都轉換 toolower 案例。

**語法：**  
`String PCase(string)`

**備註：**

* 此函式目前未提供適當的大小寫 tooconvert 全部大寫，例如為縮寫字的單字。

**範例：**  
`PCase("TEsT")`  
傳回 "test"。

`PCase(LCase("TEST"))`  
傳回 "Test"

- - -
### <a name="randomnum"></a>RandomNum
**說明：**  
hello RandomNum 函數會傳回一個隨機數字之間指定的時間間隔。

**語法：**  
`num RandomNum(num start, num end)`

* 開始： 數字識別 hello 下限 hello 隨機值 toogenerate
* 結束： 數字識別 hello 上限 hello 隨機值 toogenerate

**範例：**  
`Random(100,999)`  
可傳回 734。

- - -
### <a name="removeduplicates"></a>RemoveDuplicates
**說明：**  
hello RemoveDuplicates 函數接受多重值的字串，並確定每個值是唯一的。

**語法：**  
`mvstr RemoveDuplicates(mvstr attribute)`

**範例：**  
`RemoveDuplicates([proxyAddresses])`  
傳回處理過的 proxyAddress 屬性，其中已移除所有重複的值。

- - -
### <a name="replace"></a>Replace
**說明：**  
hello Replace 函數會取代所有出現的字串 tooanother 字串。

**語法：**  
`str Replace(str string, str OldValue, str NewValue)`

* 字串： 字串 tooreplace 中的值。
* OldValue: hello 字串 toosearch 如和 tooreplace。
* 若要 NewValue: hello 字串 tooreplace。

**備註：**  
hello 函式會辨識下列特殊符號的 hello:

* \n – 新行
* \r – 歸位字元
* \t – 定位字元

**範例：**  
`Replace([address],"\r\n",", ")`  
CRLF 取代為逗號和空格，而且可能會太導致"其中一個 Microsoft 的方式，Redmond，WA，USA"

- - -
### <a name="replacechars"></a>ReplaceChars
**說明：**  
hello ReplaceChars 函數取代字元在 hello ReplacePattern 字串中找到的所有項的目。

**語法：**  
`str ReplaceChars(str string, str ReplacePattern)`

* 字串： 字串 tooreplace 中的字元。
* ReplacePattern： 字串，包含字元 tooreplace 的字典。

hello 格式為 {source1}: {target1}，{source2}: {target2}，{sourceN}，{targetN} 來源的 hello 字元 toofind 和目標 hello 字串 tooreplace 與位置。

**備註：**

* hello 函數接受每個項目定義的來源，並將它們取代為 hello 目標。
* hello 來源必須剛好只有一個 (unicode) 字元。
* hello 來源不可為空白或長度超過一個字元 （剖析錯誤）。
* hello 目標可以有多個字元，例如.ö： oe、 β： ss。
* hello 目標可以是空白，表示應移除用 hello 字元。
* hello 來源會區分大小寫，而且必須完全相符。
* hello，（逗號） 和: （冒號） 是保留的字元，無法使用這個函式取代。
* 空間和 hello ReplacePattern 字串中的其他空白字元都會被忽略。

**範例：**  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
傳回 Raksmorgas

`ReplaceChars("O’Neil",%ReplaceString%)`  
移除定義的 toobe 是傳回"ONeil"，hello 單一刻度。

- - -
### <a name="right"></a>Right
**說明：**  
hello Right 函數會傳回指定的字元數從 hello 正確 （結尾） 的字串。

**語法：**  
`str Right(str string, num NumChars)`

* 字串： hello tooreturn 字元字串
* NumChars： 數字，識別 hello 從 hello 尾端 （右邊） 字串的字元 tooreturn 數目

**備註：**  
從字串 hello 最後位置傳回 NumChars 個字元。

字串，包含 hello 最後 numChars 個字元字串中：

* 如果 numChars = 0，會傳回空字串。
* 如果 numChars < 0，會傳回輸入字串。
* 如果 string 為 Null，會傳回空字串。

如果字串包含較少的字元，超過 hello NumChars 中指定數字，則會傳回字串的相同 toostring。

**範例：**  
`Right("John Doe", 3)`  
傳回 "Doe"。

- - -
### <a name="rtrim"></a>RTrim
**說明：**  
hello RTrim 函數從字串中移除尾端空白。

**語法：**  
`str RTrim(str value)`

**範例：**  
`RTrim(" Test ")`  
傳回 "Test"。

- - -
### <a name="select"></a>選取
**說明：**  
在以指定函式為基礎的多重值屬性 (或運算式的輸出) 中處理所有值。

**語法：**  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* 項目： 表示 hello 多重值屬性中的項目
* 屬性： hello 多重值的屬性
* expression：傳回值集合的運算式
* 條件： 可以處理 hello 屬性中的項目任何函式

**範例：**  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
傳回所有 hello 值 hello 多重值的屬性 otherPhone 後已移除連字號 （-）。

- - -
### <a name="split"></a>Split
**說明：**  
hello Split 函數接受以分隔符號分隔的字串，並使它多重值的字串。

**語法：**  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* 值： hello 與分隔符號字元 tooseparate 的字串。
* 分隔符號： 單一字元 toobe 做為 hello 分隔符號。
* limit：可以傳回的值數目上限。

**範例：**  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
傳回具有 2 個元素的多重值的字串 hello proxyAddress 屬性很有用。

- - -
### <a name="stringfromguid"></a>StringFromGuid
**說明：**  
hello StringFromGuid 函數接受二進位 GUID 並將它轉換 tooa 字串

**語法：**  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a>StringFromSid
**說明：**  
hello StringFromSid 函數將轉換位元組陣列，包含安全性識別元 tooa 字串。

**語法：**  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a>Switch
**說明：**  
hello Switch 函式是使用的 tooreturn 評估的條件所根據的單一值。

**語法：**  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* expr： 您想 tooevaluate 的 Variant 運算式。
* 值： 值 toobe 傳回 hello 對應的運算式為 True 時。

**備註：**  
hello 交換器函式引數清單所組成的運算式和值組。 hello 運算式都會從左 tooright，評估並傳回第一個運算式 tooevaluate tooTrue hello 與相關聯的 hello 值。 如果 hello 組件的配對不正確，就會發生執行階段錯誤。

例如，如果 expr1 為 True，Switch 就會傳回 value1。 如果 expr-1 為 False，但 expr-2 為 True，Switch 就會傳回 value-2，依此類推。

在下列情況下，參數會傳回 Nothing︰

* Hello 運算式都為 True。
* hello 的第一個 True 運算式具有對應值是 Null。

雖然 Switch 只會傳回其中一個運算式，但它會評估所有運算式。 基於這個理由，您應該留意非預期的副作用。 例如，如果 hello 任何運算式的評估導致除以零的錯誤，就會發生錯誤。

值，也可以是 hello 誤差函數會傳回自訂字串。

**範例：**  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
傳回一些主要城市採用說出 hello 語言，否則會傳回錯誤。

- - -
### <a name="trim"></a>Trim
**說明：**  
hello Trim 函數移除開頭和尾端空白字元的字串。

**語法：**  
`str Trim(str value)`  

**範例：**  
`Trim(" Test ")`  
傳回 "test"。

`Trim([proxyAddresses])`  
移除開頭和尾端空白 hello proxyAddress 屬性中每個值。

- - -
### <a name="ucase"></a>UCase
**說明：**  
hello UCase 函數將字串 tooupper 案例中的所有字元都轉換。

**語法：**  
`str UCase(str string)`

**範例：**  
`UCase("TeSt")`  
傳回 "test"。

- - -
### <a name="where"></a>Where

**說明：**  
傳回以指定條件為基礎的多重值屬性 (或運算式的輸出) 的值子集。

**語法：**  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* 項目： 表示 hello 多重值屬性中的項目
* 屬性： hello 多重值的屬性
* 條件： 可以是任何運算式評估 tootrue 或 false
* expression：傳回值集合的運算式

**範例：**  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
傳回不過期的 hello 多重值的屬性 userCertificate hello 憑證的值。

- - -
### <a name="with"></a>With
**說明：**  
hello 函式與使用變數 toorepresent 子運算式會出現一次或多次 hello 複雜運算式中，提供方式 toosimplify 複雜的運算式。

**語法：**
`With(var variable, exp subExpression, exp complexExpression)`  
* 變數： 代表 hello 子運算式。
* subExpression：變數代表的子運算式。
* complexExpression：複雜的運算式。

**範例：**  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
在功能上等同於：  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
Hello userCertificate 屬性中傳回的只是未到期的憑證值。


- - -
### <a name="word"></a>Word
**說明：**  
hello Word 函式會傳回包含在字串中，根據參數所描述 hello 分隔符號 toouse 和 hello 文字數字 tooreturn 的單字。

**語法：**  
`str Word(str string, num WordNumber, str delimiters)`

* 字串： hello 字串 tooreturn 特定詞彙。
* WordNumber：一個數字，用於識別可傳回的字數。
* 分隔符號： 字串，表示應該使用的 tooidentify 單字的 hello 分隔符號

**備註：**  
每個字串 hello hello 字元在分隔符號所分隔的字串中的字元就識別為單字：

* 如果 number < 1，會傳回空字串。
* 如果 string 為 Null，會傳回空字串。

如果 string 所含的字數少於 number 個字，或者 string 不包含任何 delimeters 所識別的單字，就會傳回空字串。

**範例：**  
`Word("hello quick brown fox",3," ")`  
傳回 "brown"

`Word("This,string!has&many separators",3,",!&#")`  
會傳回 "has"

## <a name="additional-resources"></a>其他資源
* [了解宣告式佈建運算式](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [Azure AD Connect 同步處理：自訂同步處理選項](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

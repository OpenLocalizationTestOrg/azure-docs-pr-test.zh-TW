---
title: "Azure AD Connect：宣告式佈建運算式 | Microsoft Docs"
description: "說明 hello 宣告式佈建運算式。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 516bcf1991c608d33aefc19551254d8b2bfc024f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a>Azure AD Connect 同步處理：了解宣告式佈建運算式
Azure AD Connect 同步處理是以 Forefront Identity Manager 2010 中最先引進的宣告式佈建為基礎。 它可讓您 tooimplement hello 需要 toowrite 不完整的身分識別整合商業邏輯編譯的程式碼。

宣告式佈建不可或缺的一部分是 hello 屬性流程中使用的運算式語言。 使用 hello 語言是 Microsoft® Visual Basic® for Applications (VBA) 的子集。 此語言用於 Microsoft Office，而且擁有 VBScript 經驗的使用者也可以辨識它。 hello 宣告式佈建運算式語言 」 只使用函數，並不是結構化的語言。 沒有任何方法或陳述式。 改為巢狀函式 tooexpress 控制程式流程。

如需詳細資訊，請參閱[歡迎 toohello Visual Basic for Applications 語言參考適用於 Office 2013](https://msdn.microsoft.com/library/gg264383.aspx)。

hello 屬性是強型別。 函式只接受 hello 正確型別的屬性。 它也區分大小寫。 函式名稱和屬性名稱兩者都必須有正確的大小寫，否則會擲回錯誤。

## <a name="language-definitions-and-identifiers"></a>語言定義和識別項
* 函式名稱後面接著以括弧括住的引數：FunctionName(argument 1, argument N)。
* 屬性以方括弧識別：[attributeName]
* 參數以百分比符號識別：%ParameterName%
* 字串常數以引號括住：例如 "Contoso" (注意：必須使用一般引號 ""，而非智慧引號 “”)
* 不需要引號和預期的 toobe 十進位表示數字值。 十六進位值前面會加上 &H。 例如，98052、&HFF
* 布林值以兩個常數表示：True、False。
* 內建常數和常值只以其名稱表示：NULL、CRLF、IgnoreThisFlow

### <a name="functions"></a>Functions
宣告式佈建會使用許多函數 tooenable hello 可能性 tootransform 屬性值。 這些函式可以巢狀，因此 hello 某個函數的結果會傳遞 tooanother 函式中。

`Function1(Function2(Function3()))`

hello 函式完整清單位於 hello[函數參考](active-directory-aadconnectsync-functions-reference.md)。

### <a name="parameters"></a>參數
參數由連接器或由系統管理員使用 PowerShell 定義。 參數通常包含不同於系統 toosystem 的值，例如位於中的 hello hello 網域 hello 使用者名稱。 這些參數可用於屬性流程中。

hello Active Directory 連接器提供的 hello 輸入同步處理規則的下列參數：

| 參數名稱 | 註解 |
| --- | --- |
| Domain.Netbios |Hello 網域目前正在匯入，例如 FABRIKAMSALES 的 Netbios 格式 |
| Domain.FQDN |Hello 網域目前正在匯入，例如 sales.fabrikam.com 的 FQDN 格式 |
| Domain.LDAP |LDAP 格式的 hello 網域目前正在匯入，例如 DC = sales，DC = fabrikam，DC = com |
| Forest.Netbios |Hello 樹系名稱目前正在匯入，例如 FABRIKAMCORP Netbios 格式 |
| Forest.FQDN |Hello 樹系名稱目前正在匯入，例如 fabrikam.com FQDN 格式 |
| Forest.LDAP |LDAP 格式的 hello 樹系名稱目前正在匯入，例如 DC = fabrikam，DC = com |

hello 系統提供 hello 下列參數，其中使用的 tooget hello 識別碼 hello 連接器目前正在執行：  
`Connector.ID`

填入 hello metaverse 屬性網域 hello hello 使用者所在位置的 hello 網域 netbios 名稱的範例如下：  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a>運算子
可以使用下列運算子的 hello:

* **比較**：<、<=、<>、=、>、>=
* **數學**：+、-、\*、-
* **字串**：& (串連)
* **邏輯**：&& (且)、|| (或)
* **評估順序**：( )

運算子是評估的左的 tooright 而且具有 hello 相同評估優先權。 也就是說，hello \* （乘數） 不會評估前-（減號）。 2\*(5 + 3) 不是相同 hello 2\*5 + 3。 hello 括弧 （） 會使用 toochange hello 評估順序保留時 tooright 評估順序並不適合。

## <a name="multi-valued-attributes"></a>多重值屬性
hello 函式可以處理單一值及多重值屬性。 對於多重值屬性，hello 函式的每個值上運作，並套用 hello 相同函式 tooevery 值。

例如：  
`Trim([proxyAddresses])`執行 Trim hello proxyAddress 屬性中的每個值。  
`Word([proxyAddresses],1,"@") & "@contoso.com"`針對每個值與@-sign，取代 hello 網域@contoso.com。  
`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`尋找 hello SIP 位址，並將它從 hello 值移除。

## <a name="next-steps"></a>後續步驟
* 深入了解 hello 組態模型[了解宣告式佈建](active-directory-aadconnectsync-understanding-declarative-provisioning.md)。
* 請參閱如何宣告式佈建須使用-蜪鎏中[了解 hello 預設組態](active-directory-aadconnectsync-understanding-default-configuration.md)。
* 請參閱 toomake 實際變更使用中的宣告式佈建[toomake 變更 toohello 預設組態的方式](active-directory-aadconnectsync-change-the-configuration.md)。

**概觀主題**

* [Azure AD Connect 同步處理：了解及自訂同步處理](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

**參考主題**

* [Azure AD Connect 同步處理：函式參考](active-directory-aadconnectsync-functions-reference.md)


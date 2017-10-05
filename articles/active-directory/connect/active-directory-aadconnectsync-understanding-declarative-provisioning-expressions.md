---
title: "Azure AD Connect：宣告式佈建運算式 | Microsoft Docs"
description: "說明宣告式佈建運算式。"
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
ms.openlocfilehash: e3a03a97b10e04fb85261620879b2102e1db8465
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a><span data-ttu-id="4be65-103">Azure AD Connect 同步處理：了解宣告式佈建運算式</span><span class="sxs-lookup"><span data-stu-id="4be65-103">Azure AD Connect sync: Understanding Declarative Provisioning Expressions</span></span>
<span data-ttu-id="4be65-104">Azure AD Connect 同步處理是以 Forefront Identity Manager 2010 中最先引進的宣告式佈建為基礎。</span><span class="sxs-lookup"><span data-stu-id="4be65-104">Azure AD Connect sync builds on declarative provisioning first introduced in Forefront Identity Manager 2010.</span></span> <span data-ttu-id="4be65-105">它可讓您實作完整的身分識別整合商務邏輯，而不需要撰寫已編譯的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4be65-105">It allows you to implement your complete identity integration business logic without the need to write compiled code.</span></span>

<span data-ttu-id="4be65-106">宣告式佈建最主要的部分是在屬性流程中使用運算式語言。</span><span class="sxs-lookup"><span data-stu-id="4be65-106">An essential part of declarative provisioning is the expression language used in attribute flows.</span></span> <span data-ttu-id="4be65-107">使用的語言是 Microsoft® Visual Basic® for Applications (VBA) 的子集。</span><span class="sxs-lookup"><span data-stu-id="4be65-107">The language used is a subset of Microsoft® Visual Basic® for Applications (VBA).</span></span> <span data-ttu-id="4be65-108">此語言用於 Microsoft Office，而且擁有 VBScript 經驗的使用者也可以辨識它。</span><span class="sxs-lookup"><span data-stu-id="4be65-108">This language is used in Microsoft Office and users with experience of VBScript will also recognize it.</span></span> <span data-ttu-id="4be65-109">宣告式佈建運算式語言只會使用函式，而不是結構化語言。</span><span class="sxs-lookup"><span data-stu-id="4be65-109">The Declarative Provisioning Expression Language is only using functions and is not a structured language.</span></span> <span data-ttu-id="4be65-110">沒有任何方法或陳述式。</span><span class="sxs-lookup"><span data-stu-id="4be65-110">There are no methods or statements.</span></span> <span data-ttu-id="4be65-111">函式會改為巢狀函式來表示程式流程。</span><span class="sxs-lookup"><span data-stu-id="4be65-111">Functions are instead nested to express program flow.</span></span>

<span data-ttu-id="4be65-112">如需詳細資訊，請參閱 [歡迎使用適用於 Office 2013 的 Visual Basic for Applications 語言參考](https://msdn.microsoft.com/library/gg264383.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4be65-112">For more details, see [Welcome to the Visual Basic for Applications language reference for Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).</span></span>

<span data-ttu-id="4be65-113">屬性是強型別。</span><span class="sxs-lookup"><span data-stu-id="4be65-113">The attributes are strongly typed.</span></span> <span data-ttu-id="4be65-114">函式只會接受正確類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="4be65-114">A function only accepts attributes of the correct type.</span></span> <span data-ttu-id="4be65-115">它也區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="4be65-115">It is also case-sensitive.</span></span> <span data-ttu-id="4be65-116">函式名稱和屬性名稱兩者都必須有正確的大小寫，否則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="4be65-116">Both function names and attribute names must have proper casing or an error is thrown.</span></span>

## <a name="language-definitions-and-identifiers"></a><span data-ttu-id="4be65-117">語言定義和識別項</span><span class="sxs-lookup"><span data-stu-id="4be65-117">Language definitions and Identifiers</span></span>
* <span data-ttu-id="4be65-118">函式名稱後面接著以括弧括住的引數：FunctionName(argument 1, argument N)。</span><span class="sxs-lookup"><span data-stu-id="4be65-118">Functions have a name followed by arguments in brackets: FunctionName(argument 1, argument N).</span></span>
* <span data-ttu-id="4be65-119">屬性以方括弧識別：[attributeName]</span><span class="sxs-lookup"><span data-stu-id="4be65-119">Attributes are identified by square brackets: [attributeName]</span></span>
* <span data-ttu-id="4be65-120">參數以百分比符號識別：%ParameterName%</span><span class="sxs-lookup"><span data-stu-id="4be65-120">Parameters are identified by percent signs: %ParameterName%</span></span>
* <span data-ttu-id="4be65-121">字串常數以引號括住：例如 "Contoso" (注意：必須使用一般引號 ""，而非智慧引號 “”)</span><span class="sxs-lookup"><span data-stu-id="4be65-121">String constants are surrounded by quotes: For example, "Contoso" (Note: must use straight quotes "" and not smart quotes “”)</span></span>
* <span data-ttu-id="4be65-122">數值不加引號，而且必須是十進位。</span><span class="sxs-lookup"><span data-stu-id="4be65-122">Numeric values are expressed without quotes and expected to be decimal.</span></span> <span data-ttu-id="4be65-123">十六進位值前面會加上 &H。</span><span class="sxs-lookup"><span data-stu-id="4be65-123">Hexadecimal values are prefixed with &H.</span></span> <span data-ttu-id="4be65-124">例如，98052、&HFF</span><span class="sxs-lookup"><span data-stu-id="4be65-124">For example, 98052, &HFF</span></span>
* <span data-ttu-id="4be65-125">布林值以兩個常數表示：True、False。</span><span class="sxs-lookup"><span data-stu-id="4be65-125">Boolean values are expressed with constants: True, False.</span></span>
* <span data-ttu-id="4be65-126">內建常數和常值只以其名稱表示：NULL、CRLF、IgnoreThisFlow</span><span class="sxs-lookup"><span data-stu-id="4be65-126">Built-in constants and literals are expressed with only their name: NULL, CRLF, IgnoreThisFlow</span></span>

### <a name="functions"></a><span data-ttu-id="4be65-127">Functions</span><span class="sxs-lookup"><span data-stu-id="4be65-127">Functions</span></span>
<span data-ttu-id="4be65-128">宣告式佈建會使用許多函式，來啟用轉換屬性值的可能性。</span><span class="sxs-lookup"><span data-stu-id="4be65-128">Declarative provisioning uses many functions to enable the possibility to transform attribute values.</span></span> <span data-ttu-id="4be65-129">這些函式可以是巢狀的，因此，來自某一個函式的結果會傳遞到另一個函式。</span><span class="sxs-lookup"><span data-stu-id="4be65-129">These functions can be nested so the result from one function is passed in to another function.</span></span>

`Function1(Function2(Function3()))`

<span data-ttu-id="4be65-130">如需函式的完整清單，請參閱 [函式參考](active-directory-aadconnectsync-functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="4be65-130">The complete list of functions can be found in the [function reference](active-directory-aadconnectsync-functions-reference.md).</span></span>

### <a name="parameters"></a><span data-ttu-id="4be65-131">參數</span><span class="sxs-lookup"><span data-stu-id="4be65-131">Parameters</span></span>
<span data-ttu-id="4be65-132">參數由連接器或由系統管理員使用 PowerShell 定義。</span><span class="sxs-lookup"><span data-stu-id="4be65-132">A parameter is defined either by a Connector or by an administrator using PowerShell.</span></span> <span data-ttu-id="4be65-133">參數通常會包含隨系統而不同的值，例如使用者所在的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4be65-133">Parameters usually contain values that are different from system to system, for example the name of the domain the user is located in.</span></span> <span data-ttu-id="4be65-134">這些參數可用於屬性流程中。</span><span class="sxs-lookup"><span data-stu-id="4be65-134">These parameters can be used in attribute flows.</span></span>

<span data-ttu-id="4be65-135">Active Directory 連接器對於輸入同步處理規則提供下列參數：</span><span class="sxs-lookup"><span data-stu-id="4be65-135">The Active Directory Connector provided the following parameters for inbound Synchronization Rules:</span></span>

| <span data-ttu-id="4be65-136">參數名稱</span><span class="sxs-lookup"><span data-stu-id="4be65-136">Parameter Name</span></span> | <span data-ttu-id="4be65-137">註解</span><span class="sxs-lookup"><span data-stu-id="4be65-137">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="4be65-138">Domain.Netbios</span><span class="sxs-lookup"><span data-stu-id="4be65-138">Domain.Netbios</span></span> |<span data-ttu-id="4be65-139">目前正在匯入之網域的 NetBIOS 格式，例如 FABRIKAMSALES</span><span class="sxs-lookup"><span data-stu-id="4be65-139">Netbios format of the domain currently being imported, for example FABRIKAMSALES</span></span> |
| <span data-ttu-id="4be65-140">Domain.FQDN</span><span class="sxs-lookup"><span data-stu-id="4be65-140">Domain.FQDN</span></span> |<span data-ttu-id="4be65-141">目前正在匯入之網域的 FQDN 格式，例如 sales.fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="4be65-141">FQDN format of the domain currently being imported, for example sales.fabrikam.com</span></span> |
| <span data-ttu-id="4be65-142">Domain.LDAP</span><span class="sxs-lookup"><span data-stu-id="4be65-142">Domain.LDAP</span></span> |<span data-ttu-id="4be65-143">目前正在匯入之網域的 LDAP 格式，例如 DC=sales,DC=fabrikam,DC=com</span><span class="sxs-lookup"><span data-stu-id="4be65-143">LDAP format of the domain currently being imported, for example DC=sales,DC=fabrikam,DC=com</span></span> |
| <span data-ttu-id="4be65-144">Forest.Netbios</span><span class="sxs-lookup"><span data-stu-id="4be65-144">Forest.Netbios</span></span> |<span data-ttu-id="4be65-145">目前正在匯入之樹系名稱的 Netbios 格式，例如 FABRIKAMCORP</span><span class="sxs-lookup"><span data-stu-id="4be65-145">Netbios format of the forest name currently being imported, for example FABRIKAMCORP</span></span> |
| <span data-ttu-id="4be65-146">Forest.FQDN</span><span class="sxs-lookup"><span data-stu-id="4be65-146">Forest.FQDN</span></span> |<span data-ttu-id="4be65-147">目前正在匯入之樹系名稱的 FQDN 格式，例如 fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="4be65-147">FQDN format of the forest name currently being imported, for example fabrikam.com</span></span> |
| <span data-ttu-id="4be65-148">Forest.LDAP</span><span class="sxs-lookup"><span data-stu-id="4be65-148">Forest.LDAP</span></span> |<span data-ttu-id="4be65-149">目前正在匯入之樹系名稱的 LDAP 格式，例如 DC=fabrikam,DC=com</span><span class="sxs-lookup"><span data-stu-id="4be65-149">LDAP format of the forest name currently being imported, for example DC=fabrikam,DC=com</span></span> |

<span data-ttu-id="4be65-150">系統會提供下列參數，用來取得目前正在執行之連接器的識別碼：</span><span class="sxs-lookup"><span data-stu-id="4be65-150">The system provides the following parameter, which is used to get the identifier of the Connector currently running:</span></span>  
`Connector.ID`

<span data-ttu-id="4be65-151">以下範例會以使用者所在網域的 netbios 名稱填入 Metaverse 屬性網域：</span><span class="sxs-lookup"><span data-stu-id="4be65-151">Here is an example that populates the metaverse attribute domain with the netbios name of the domain where the user is located:</span></span>  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a><span data-ttu-id="4be65-152">運算子</span><span class="sxs-lookup"><span data-stu-id="4be65-152">Operators</span></span>
<span data-ttu-id="4be65-153">可以使用下列運算子：</span><span class="sxs-lookup"><span data-stu-id="4be65-153">The following operators can be used:</span></span>

* <span data-ttu-id="4be65-154">**比較**：<、<=、<>、=、>、>=</span><span class="sxs-lookup"><span data-stu-id="4be65-154">**Comparison**: <, <=, <>, =, >, >=</span></span>
* <span data-ttu-id="4be65-155">**數學**：+、-、\*、-</span><span class="sxs-lookup"><span data-stu-id="4be65-155">**Mathematics**: +, -, \*, -</span></span>
* <span data-ttu-id="4be65-156">**字串**：& (串連)</span><span class="sxs-lookup"><span data-stu-id="4be65-156">**String**: & (concatenate)</span></span>
* <span data-ttu-id="4be65-157">**邏輯**：&& (且)、|| (或)</span><span class="sxs-lookup"><span data-stu-id="4be65-157">**Logical**: && (and), || (or)</span></span>
* <span data-ttu-id="4be65-158">**評估順序**：( )</span><span class="sxs-lookup"><span data-stu-id="4be65-158">**Evaluation order**: ( )</span></span>

<span data-ttu-id="4be65-159">運算子會由左至右進行評估，且具有相同的評估優先順序。</span><span class="sxs-lookup"><span data-stu-id="4be65-159">Operators are evaluated left to right and have the same evaluation priority.</span></span> <span data-ttu-id="4be65-160">也就是，不會在 - (減號) 之前評估 \* (乘數)。</span><span class="sxs-lookup"><span data-stu-id="4be65-160">That is, the \* (multiplier) is not evaluated before - (subtraction).</span></span> <span data-ttu-id="4be65-161">2\*(5+3) 與 2\*5+3 不同。</span><span class="sxs-lookup"><span data-stu-id="4be65-161">2\*(5+3) is not the same as 2\*5+3.</span></span> <span data-ttu-id="4be65-162">若由左至右的評估順序不適當，則可使用括弧 () 來變更評估順序。</span><span class="sxs-lookup"><span data-stu-id="4be65-162">The brackets ( ) are used to change the evaluation order when left to right evaluation order isn't appropriate.</span></span>

## <a name="multi-valued-attributes"></a><span data-ttu-id="4be65-163">多重值屬性</span><span class="sxs-lookup"><span data-stu-id="4be65-163">Multi-valued attributes</span></span>
<span data-ttu-id="4be65-164">函式可以在單一值和多重值屬性上操作。</span><span class="sxs-lookup"><span data-stu-id="4be65-164">The functions can operate on both single-valued and multi-valued attributes.</span></span> <span data-ttu-id="4be65-165">對於多重值屬性，函式會在每個值上進行操作並將相同的函式套用到每個值。</span><span class="sxs-lookup"><span data-stu-id="4be65-165">For multi-valued attributes, the function operates over every value and applies the same function to every value.</span></span>

<span data-ttu-id="4be65-166">例如，</span><span class="sxs-lookup"><span data-stu-id="4be65-166">For example:</span></span>  
<span data-ttu-id="4be65-167">`Trim([proxyAddresses])` 在 proxyAddress 屬性中執行每個值的 Trim。</span><span class="sxs-lookup"><span data-stu-id="4be65-167">`Trim([proxyAddresses])` Do a Trim of every value in the proxyAddress attribute.</span></span>  
<span data-ttu-id="4be65-168">`Word([proxyAddresses],1,"@") & "@contoso.com"`針對每個值與@-sign，取代網域@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="4be65-168">`Word([proxyAddresses],1,"@") & "@contoso.com"` For every value with an @-sign, replace the domain with @contoso.com.</span></span>  
<span data-ttu-id="4be65-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` 尋找 SIP 位址並從各值中移除。</span><span class="sxs-lookup"><span data-stu-id="4be65-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` Look for the SIP-address and remove it from the values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4be65-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4be65-170">Next steps</span></span>
* <span data-ttu-id="4be65-171">如需組態模型的詳細資訊，請參閱 [了解宣告式佈建](active-directory-aadconnectsync-understanding-declarative-provisioning.md)。</span><span class="sxs-lookup"><span data-stu-id="4be65-171">Read more about the configuration model in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>
* <span data-ttu-id="4be65-172">如需了解如何立即使用宣告式佈建，請參閱 [了解預設組態](active-directory-aadconnectsync-understanding-default-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="4be65-172">See how declarative provisioning is used out-of-box in [Understanding the default configuration](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
* <span data-ttu-id="4be65-173">如需了解如何使用宣告式佈建進行實際變更，請參閱 [如何變更預設組態](active-directory-aadconnectsync-change-the-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="4be65-173">See how to make a practical change using declarative provisioning in [How to make a change to the default configuration](active-directory-aadconnectsync-change-the-configuration.md).</span></span>

<span data-ttu-id="4be65-174">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="4be65-174">**Overview topics**</span></span>

* [<span data-ttu-id="4be65-175">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="4be65-175">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="4be65-176">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4be65-176">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

<span data-ttu-id="4be65-177">**參考主題**</span><span class="sxs-lookup"><span data-stu-id="4be65-177">**Reference topics**</span></span>

* [<span data-ttu-id="4be65-178">Azure AD Connect 同步處理：函式參考</span><span class="sxs-lookup"><span data-stu-id="4be65-178">Azure AD Connect sync: Functions Reference</span></span>](active-directory-aadconnectsync-functions-reference.md)


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
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a><span data-ttu-id="727c9-103">Azure AD Connect 同步處理：了解宣告式佈建運算式</span><span class="sxs-lookup"><span data-stu-id="727c9-103">Azure AD Connect sync: Understanding Declarative Provisioning Expressions</span></span>
<span data-ttu-id="727c9-104">Azure AD Connect 同步處理是以 Forefront Identity Manager 2010 中最先引進的宣告式佈建為基礎。</span><span class="sxs-lookup"><span data-stu-id="727c9-104">Azure AD Connect sync builds on declarative provisioning first introduced in Forefront Identity Manager 2010.</span></span> <span data-ttu-id="727c9-105">它可讓您 tooimplement hello 需要 toowrite 不完整的身分識別整合商業邏輯編譯的程式碼。</span><span class="sxs-lookup"><span data-stu-id="727c9-105">It allows you tooimplement your complete identity integration business logic without hello need toowrite compiled code.</span></span>

<span data-ttu-id="727c9-106">宣告式佈建不可或缺的一部分是 hello 屬性流程中使用的運算式語言。</span><span class="sxs-lookup"><span data-stu-id="727c9-106">An essential part of declarative provisioning is hello expression language used in attribute flows.</span></span> <span data-ttu-id="727c9-107">使用 hello 語言是 Microsoft® Visual Basic® for Applications (VBA) 的子集。</span><span class="sxs-lookup"><span data-stu-id="727c9-107">hello language used is a subset of Microsoft® Visual Basic® for Applications (VBA).</span></span> <span data-ttu-id="727c9-108">此語言用於 Microsoft Office，而且擁有 VBScript 經驗的使用者也可以辨識它。</span><span class="sxs-lookup"><span data-stu-id="727c9-108">This language is used in Microsoft Office and users with experience of VBScript will also recognize it.</span></span> <span data-ttu-id="727c9-109">hello 宣告式佈建運算式語言 」 只使用函數，並不是結構化的語言。</span><span class="sxs-lookup"><span data-stu-id="727c9-109">hello Declarative Provisioning Expression Language is only using functions and is not a structured language.</span></span> <span data-ttu-id="727c9-110">沒有任何方法或陳述式。</span><span class="sxs-lookup"><span data-stu-id="727c9-110">There are no methods or statements.</span></span> <span data-ttu-id="727c9-111">改為巢狀函式 tooexpress 控制程式流程。</span><span class="sxs-lookup"><span data-stu-id="727c9-111">Functions are instead nested tooexpress program flow.</span></span>

<span data-ttu-id="727c9-112">如需詳細資訊，請參閱[歡迎 toohello Visual Basic for Applications 語言參考適用於 Office 2013](https://msdn.microsoft.com/library/gg264383.aspx)。</span><span class="sxs-lookup"><span data-stu-id="727c9-112">For more details, see [Welcome toohello Visual Basic for Applications language reference for Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).</span></span>

<span data-ttu-id="727c9-113">hello 屬性是強型別。</span><span class="sxs-lookup"><span data-stu-id="727c9-113">hello attributes are strongly typed.</span></span> <span data-ttu-id="727c9-114">函式只接受 hello 正確型別的屬性。</span><span class="sxs-lookup"><span data-stu-id="727c9-114">A function only accepts attributes of hello correct type.</span></span> <span data-ttu-id="727c9-115">它也區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="727c9-115">It is also case-sensitive.</span></span> <span data-ttu-id="727c9-116">函式名稱和屬性名稱兩者都必須有正確的大小寫，否則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="727c9-116">Both function names and attribute names must have proper casing or an error is thrown.</span></span>

## <a name="language-definitions-and-identifiers"></a><span data-ttu-id="727c9-117">語言定義和識別項</span><span class="sxs-lookup"><span data-stu-id="727c9-117">Language definitions and Identifiers</span></span>
* <span data-ttu-id="727c9-118">函式名稱後面接著以括弧括住的引數：FunctionName(argument 1, argument N)。</span><span class="sxs-lookup"><span data-stu-id="727c9-118">Functions have a name followed by arguments in brackets: FunctionName(argument 1, argument N).</span></span>
* <span data-ttu-id="727c9-119">屬性以方括弧識別：[attributeName]</span><span class="sxs-lookup"><span data-stu-id="727c9-119">Attributes are identified by square brackets: [attributeName]</span></span>
* <span data-ttu-id="727c9-120">參數以百分比符號識別：%ParameterName%</span><span class="sxs-lookup"><span data-stu-id="727c9-120">Parameters are identified by percent signs: %ParameterName%</span></span>
* <span data-ttu-id="727c9-121">字串常數以引號括住：例如 "Contoso" (注意：必須使用一般引號 ""，而非智慧引號 “”)</span><span class="sxs-lookup"><span data-stu-id="727c9-121">String constants are surrounded by quotes: For example, "Contoso" (Note: must use straight quotes "" and not smart quotes “”)</span></span>
* <span data-ttu-id="727c9-122">不需要引號和預期的 toobe 十進位表示數字值。</span><span class="sxs-lookup"><span data-stu-id="727c9-122">Numeric values are expressed without quotes and expected toobe decimal.</span></span> <span data-ttu-id="727c9-123">十六進位值前面會加上 &H。</span><span class="sxs-lookup"><span data-stu-id="727c9-123">Hexadecimal values are prefixed with &H.</span></span> <span data-ttu-id="727c9-124">例如，98052、&HFF</span><span class="sxs-lookup"><span data-stu-id="727c9-124">For example, 98052, &HFF</span></span>
* <span data-ttu-id="727c9-125">布林值以兩個常數表示：True、False。</span><span class="sxs-lookup"><span data-stu-id="727c9-125">Boolean values are expressed with constants: True, False.</span></span>
* <span data-ttu-id="727c9-126">內建常數和常值只以其名稱表示：NULL、CRLF、IgnoreThisFlow</span><span class="sxs-lookup"><span data-stu-id="727c9-126">Built-in constants and literals are expressed with only their name: NULL, CRLF, IgnoreThisFlow</span></span>

### <a name="functions"></a><span data-ttu-id="727c9-127">Functions</span><span class="sxs-lookup"><span data-stu-id="727c9-127">Functions</span></span>
<span data-ttu-id="727c9-128">宣告式佈建會使用許多函數 tooenable hello 可能性 tootransform 屬性值。</span><span class="sxs-lookup"><span data-stu-id="727c9-128">Declarative provisioning uses many functions tooenable hello possibility tootransform attribute values.</span></span> <span data-ttu-id="727c9-129">這些函式可以巢狀，因此 hello 某個函數的結果會傳遞 tooanother 函式中。</span><span class="sxs-lookup"><span data-stu-id="727c9-129">These functions can be nested so hello result from one function is passed in tooanother function.</span></span>

`Function1(Function2(Function3()))`

<span data-ttu-id="727c9-130">hello 函式完整清單位於 hello[函數參考](active-directory-aadconnectsync-functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="727c9-130">hello complete list of functions can be found in hello [function reference](active-directory-aadconnectsync-functions-reference.md).</span></span>

### <a name="parameters"></a><span data-ttu-id="727c9-131">參數</span><span class="sxs-lookup"><span data-stu-id="727c9-131">Parameters</span></span>
<span data-ttu-id="727c9-132">參數由連接器或由系統管理員使用 PowerShell 定義。</span><span class="sxs-lookup"><span data-stu-id="727c9-132">A parameter is defined either by a Connector or by an administrator using PowerShell.</span></span> <span data-ttu-id="727c9-133">參數通常包含不同於系統 toosystem 的值，例如位於中的 hello hello 網域 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="727c9-133">Parameters usually contain values that are different from system toosystem, for example hello name of hello domain hello user is located in.</span></span> <span data-ttu-id="727c9-134">這些參數可用於屬性流程中。</span><span class="sxs-lookup"><span data-stu-id="727c9-134">These parameters can be used in attribute flows.</span></span>

<span data-ttu-id="727c9-135">hello Active Directory 連接器提供的 hello 輸入同步處理規則的下列參數：</span><span class="sxs-lookup"><span data-stu-id="727c9-135">hello Active Directory Connector provided hello following parameters for inbound Synchronization Rules:</span></span>

| <span data-ttu-id="727c9-136">參數名稱</span><span class="sxs-lookup"><span data-stu-id="727c9-136">Parameter Name</span></span> | <span data-ttu-id="727c9-137">註解</span><span class="sxs-lookup"><span data-stu-id="727c9-137">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="727c9-138">Domain.Netbios</span><span class="sxs-lookup"><span data-stu-id="727c9-138">Domain.Netbios</span></span> |<span data-ttu-id="727c9-139">Hello 網域目前正在匯入，例如 FABRIKAMSALES 的 Netbios 格式</span><span class="sxs-lookup"><span data-stu-id="727c9-139">Netbios format of hello domain currently being imported, for example FABRIKAMSALES</span></span> |
| <span data-ttu-id="727c9-140">Domain.FQDN</span><span class="sxs-lookup"><span data-stu-id="727c9-140">Domain.FQDN</span></span> |<span data-ttu-id="727c9-141">Hello 網域目前正在匯入，例如 sales.fabrikam.com 的 FQDN 格式</span><span class="sxs-lookup"><span data-stu-id="727c9-141">FQDN format of hello domain currently being imported, for example sales.fabrikam.com</span></span> |
| <span data-ttu-id="727c9-142">Domain.LDAP</span><span class="sxs-lookup"><span data-stu-id="727c9-142">Domain.LDAP</span></span> |<span data-ttu-id="727c9-143">LDAP 格式的 hello 網域目前正在匯入，例如 DC = sales，DC = fabrikam，DC = com</span><span class="sxs-lookup"><span data-stu-id="727c9-143">LDAP format of hello domain currently being imported, for example DC=sales,DC=fabrikam,DC=com</span></span> |
| <span data-ttu-id="727c9-144">Forest.Netbios</span><span class="sxs-lookup"><span data-stu-id="727c9-144">Forest.Netbios</span></span> |<span data-ttu-id="727c9-145">Hello 樹系名稱目前正在匯入，例如 FABRIKAMCORP Netbios 格式</span><span class="sxs-lookup"><span data-stu-id="727c9-145">Netbios format of hello forest name currently being imported, for example FABRIKAMCORP</span></span> |
| <span data-ttu-id="727c9-146">Forest.FQDN</span><span class="sxs-lookup"><span data-stu-id="727c9-146">Forest.FQDN</span></span> |<span data-ttu-id="727c9-147">Hello 樹系名稱目前正在匯入，例如 fabrikam.com FQDN 格式</span><span class="sxs-lookup"><span data-stu-id="727c9-147">FQDN format of hello forest name currently being imported, for example fabrikam.com</span></span> |
| <span data-ttu-id="727c9-148">Forest.LDAP</span><span class="sxs-lookup"><span data-stu-id="727c9-148">Forest.LDAP</span></span> |<span data-ttu-id="727c9-149">LDAP 格式的 hello 樹系名稱目前正在匯入，例如 DC = fabrikam，DC = com</span><span class="sxs-lookup"><span data-stu-id="727c9-149">LDAP format of hello forest name currently being imported, for example DC=fabrikam,DC=com</span></span> |

<span data-ttu-id="727c9-150">hello 系統提供 hello 下列參數，其中使用的 tooget hello 識別碼 hello 連接器目前正在執行：</span><span class="sxs-lookup"><span data-stu-id="727c9-150">hello system provides hello following parameter, which is used tooget hello identifier of hello Connector currently running:</span></span>  
`Connector.ID`

<span data-ttu-id="727c9-151">填入 hello metaverse 屬性網域 hello hello 使用者所在位置的 hello 網域 netbios 名稱的範例如下：</span><span class="sxs-lookup"><span data-stu-id="727c9-151">Here is an example that populates hello metaverse attribute domain with hello netbios name of hello domain where hello user is located:</span></span>  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a><span data-ttu-id="727c9-152">運算子</span><span class="sxs-lookup"><span data-stu-id="727c9-152">Operators</span></span>
<span data-ttu-id="727c9-153">可以使用下列運算子的 hello:</span><span class="sxs-lookup"><span data-stu-id="727c9-153">hello following operators can be used:</span></span>

* <span data-ttu-id="727c9-154">**比較**：<、<=、<>、=、>、>=</span><span class="sxs-lookup"><span data-stu-id="727c9-154">**Comparison**: <, <=, <>, =, >, >=</span></span>
* <span data-ttu-id="727c9-155">**數學**：+、-、\*、-</span><span class="sxs-lookup"><span data-stu-id="727c9-155">**Mathematics**: +, -, \*, -</span></span>
* <span data-ttu-id="727c9-156">**字串**：& (串連)</span><span class="sxs-lookup"><span data-stu-id="727c9-156">**String**: & (concatenate)</span></span>
* <span data-ttu-id="727c9-157">**邏輯**：&& (且)、|| (或)</span><span class="sxs-lookup"><span data-stu-id="727c9-157">**Logical**: && (and), || (or)</span></span>
* <span data-ttu-id="727c9-158">**評估順序**：( )</span><span class="sxs-lookup"><span data-stu-id="727c9-158">**Evaluation order**: ( )</span></span>

<span data-ttu-id="727c9-159">運算子是評估的左的 tooright 而且具有 hello 相同評估優先權。</span><span class="sxs-lookup"><span data-stu-id="727c9-159">Operators are evaluated left tooright and have hello same evaluation priority.</span></span> <span data-ttu-id="727c9-160">也就是說，hello \* （乘數） 不會評估前-（減號）。</span><span class="sxs-lookup"><span data-stu-id="727c9-160">That is, hello \* (multiplier) is not evaluated before - (subtraction).</span></span> <span data-ttu-id="727c9-161">2\*(5 + 3) 不是相同 hello 2\*5 + 3。</span><span class="sxs-lookup"><span data-stu-id="727c9-161">2\*(5+3) is not hello same as 2\*5+3.</span></span> <span data-ttu-id="727c9-162">hello 括弧 （） 會使用 toochange hello 評估順序保留時 tooright 評估順序並不適合。</span><span class="sxs-lookup"><span data-stu-id="727c9-162">hello brackets ( ) are used toochange hello evaluation order when left tooright evaluation order isn't appropriate.</span></span>

## <a name="multi-valued-attributes"></a><span data-ttu-id="727c9-163">多重值屬性</span><span class="sxs-lookup"><span data-stu-id="727c9-163">Multi-valued attributes</span></span>
<span data-ttu-id="727c9-164">hello 函式可以處理單一值及多重值屬性。</span><span class="sxs-lookup"><span data-stu-id="727c9-164">hello functions can operate on both single-valued and multi-valued attributes.</span></span> <span data-ttu-id="727c9-165">對於多重值屬性，hello 函式的每個值上運作，並套用 hello 相同函式 tooevery 值。</span><span class="sxs-lookup"><span data-stu-id="727c9-165">For multi-valued attributes, hello function operates over every value and applies hello same function tooevery value.</span></span>

<span data-ttu-id="727c9-166">例如：</span><span class="sxs-lookup"><span data-stu-id="727c9-166">For example:</span></span>  
<span data-ttu-id="727c9-167">`Trim([proxyAddresses])`執行 Trim hello proxyAddress 屬性中的每個值。</span><span class="sxs-lookup"><span data-stu-id="727c9-167">`Trim([proxyAddresses])` Do a Trim of every value in hello proxyAddress attribute.</span></span>  
<span data-ttu-id="727c9-168">`Word([proxyAddresses],1,"@") & "@contoso.com"`針對每個值與@-sign，取代 hello 網域@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="727c9-168">`Word([proxyAddresses],1,"@") & "@contoso.com"` For every value with an @-sign, replace hello domain with @contoso.com.</span></span>  
<span data-ttu-id="727c9-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`尋找 hello SIP 位址，並將它從 hello 值移除。</span><span class="sxs-lookup"><span data-stu-id="727c9-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` Look for hello SIP-address and remove it from hello values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="727c9-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="727c9-170">Next steps</span></span>
* <span data-ttu-id="727c9-171">深入了解 hello 組態模型[了解宣告式佈建](active-directory-aadconnectsync-understanding-declarative-provisioning.md)。</span><span class="sxs-lookup"><span data-stu-id="727c9-171">Read more about hello configuration model in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>
* <span data-ttu-id="727c9-172">請參閱如何宣告式佈建須使用-蜪鎏中[了解 hello 預設組態](active-directory-aadconnectsync-understanding-default-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="727c9-172">See how declarative provisioning is used out-of-box in [Understanding hello default configuration](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
* <span data-ttu-id="727c9-173">請參閱 toomake 實際變更使用中的宣告式佈建[toomake 變更 toohello 預設組態的方式](active-directory-aadconnectsync-change-the-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="727c9-173">See how toomake a practical change using declarative provisioning in [How toomake a change toohello default configuration](active-directory-aadconnectsync-change-the-configuration.md).</span></span>

<span data-ttu-id="727c9-174">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="727c9-174">**Overview topics**</span></span>

* [<span data-ttu-id="727c9-175">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="727c9-175">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="727c9-176">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="727c9-176">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

<span data-ttu-id="727c9-177">**參考主題**</span><span class="sxs-lookup"><span data-stu-id="727c9-177">**Reference topics**</span></span>

* [<span data-ttu-id="727c9-178">Azure AD Connect 同步處理：函式參考</span><span class="sxs-lookup"><span data-stu-id="727c9-178">Azure AD Connect sync: Functions Reference</span></span>](active-directory-aadconnectsync-functions-reference.md)


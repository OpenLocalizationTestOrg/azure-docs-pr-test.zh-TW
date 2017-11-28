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
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="bb640-103">Azure AD Connect 同步處理：函式參考</span><span class="sxs-lookup"><span data-stu-id="bb640-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="bb640-104">在 Azure AD Connect，函式會是同步處理期間使用的 toomanipulate 屬性值。</span><span class="sxs-lookup"><span data-stu-id="bb640-104">In Azure AD Connect, functions are used toomanipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="bb640-105">使用下列格式的 hello 表示 hello 的 hello 函式的語法：</span><span class="sxs-lookup"><span data-stu-id="bb640-105">hello Syntax of hello functions is expressed using hello following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="bb640-106">如果函式是多載的且接受多種語法，即會列出所有的有效語法。</span><span class="sxs-lookup"><span data-stu-id="bb640-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="bb640-107">hello 函式強型別，並確認 hello 類型傳入的相符項目記錄的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="bb640-107">hello functions are strongly typed and they verify that hello type passed in matches hello documented type.</span></span>  
<span data-ttu-id="bb640-108">如果 hello 類型不符合，則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="bb640-108">If hello type does not match, an error is thrown.</span></span>

<span data-ttu-id="bb640-109">hello，請使用下列語法以表示 hello 類型：</span><span class="sxs-lookup"><span data-stu-id="bb640-109">hello types are expressed with hello following syntax:</span></span>

* <span data-ttu-id="bb640-110"> – 二進位</span><span class="sxs-lookup"><span data-stu-id="bb640-110">**bin** – Binary</span></span>
* <span data-ttu-id="bb640-111"> – 布林值</span><span class="sxs-lookup"><span data-stu-id="bb640-111">**bool** – Boolean</span></span>
* <span data-ttu-id="bb640-112"> – UTC 日期/時間</span><span class="sxs-lookup"><span data-stu-id="bb640-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="bb640-113"> – 已知常數的列舉</span><span class="sxs-lookup"><span data-stu-id="bb640-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="bb640-114">**exp** – 運算式，也就是預期 tooevaluate tooa 布林值</span><span class="sxs-lookup"><span data-stu-id="bb640-114">**exp** – Expression, which is expected tooevaluate tooa Boolean</span></span>
* <span data-ttu-id="bb640-115">**mvbin** – 多重值的二進位</span><span class="sxs-lookup"><span data-stu-id="bb640-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="bb640-116">**mvstr** – 多重值的字串</span><span class="sxs-lookup"><span data-stu-id="bb640-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="bb640-117">**mvref** – 多重值的參考</span><span class="sxs-lookup"><span data-stu-id="bb640-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="bb640-118">**num** – 數值</span><span class="sxs-lookup"><span data-stu-id="bb640-118">**num** – Numeric</span></span>
* <span data-ttu-id="bb640-119">**ref** – 參考</span><span class="sxs-lookup"><span data-stu-id="bb640-119">**ref** – Reference</span></span>
* <span data-ttu-id="bb640-120">**str** – 字串</span><span class="sxs-lookup"><span data-stu-id="bb640-120">**str** – String</span></span>
* <span data-ttu-id="bb640-121">**var** – (幾乎) 任何其他類型的變體</span><span class="sxs-lookup"><span data-stu-id="bb640-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="bb640-122">**void** – 不會傳回值</span><span class="sxs-lookup"><span data-stu-id="bb640-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="bb640-123">hello 函式與 hello 類型**mvbin**， **mvstr**，和**mvref**只能搭配多重值屬性。</span><span class="sxs-lookup"><span data-stu-id="bb640-123">hello functions with hello types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="bb640-124">類型為 **bin**、**str** 和 **ref** 的函式可用於單一值和多重值的屬性。</span><span class="sxs-lookup"><span data-stu-id="bb640-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="bb640-125">函式參考</span><span class="sxs-lookup"><span data-stu-id="bb640-125">Functions Reference</span></span>
| <span data-ttu-id="bb640-126">函數的清單</span><span class="sxs-lookup"><span data-stu-id="bb640-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="bb640-127">**憑證**</span><span class="sxs-lookup"><span data-stu-id="bb640-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="bb640-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="bb640-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="bb640-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="bb640-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="bb640-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="bb640-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="bb640-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="bb640-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="bb640-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="bb640-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="bb640-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="bb640-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="bb640-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="bb640-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="bb640-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="bb640-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="bb640-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="bb640-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="bb640-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="bb640-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="bb640-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="bb640-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="bb640-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="bb640-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="bb640-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="bb640-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="bb640-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="bb640-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="bb640-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="bb640-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="bb640-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="bb640-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="bb640-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="bb640-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="bb640-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="bb640-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="bb640-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="bb640-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="bb640-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="bb640-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="bb640-148"> CertVersion</span><span class="sxs-lookup"><span data-stu-id="bb640-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="bb640-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="bb640-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="bb640-150">**轉換**</span><span class="sxs-lookup"><span data-stu-id="bb640-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="bb640-151">CBool</span><span class="sxs-lookup"><span data-stu-id="bb640-151">CBool</span></span>](#cbool) |[<span data-ttu-id="bb640-152">CDate</span><span class="sxs-lookup"><span data-stu-id="bb640-152">CDate</span></span>](#cdate) |[<span data-ttu-id="bb640-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="bb640-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="bb640-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="bb640-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="bb640-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="bb640-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="bb640-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="bb640-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="bb640-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="bb640-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="bb640-158">CNum</span><span class="sxs-lookup"><span data-stu-id="bb640-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="bb640-159">CRef</span><span class="sxs-lookup"><span data-stu-id="bb640-159">CRef</span></span>](#cref) |[<span data-ttu-id="bb640-160">CStr</span><span class="sxs-lookup"><span data-stu-id="bb640-160">CStr</span></span>](#cstr) |[<span data-ttu-id="bb640-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="bb640-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="bb640-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="bb640-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="bb640-163">**日期 / 時間**</span><span class="sxs-lookup"><span data-stu-id="bb640-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="bb640-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="bb640-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="bb640-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="bb640-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="bb640-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="bb640-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="bb640-167">Now</span><span class="sxs-lookup"><span data-stu-id="bb640-167">Now</span></span>](#now) | |
| [<span data-ttu-id="bb640-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="bb640-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="bb640-169">**目錄**</span><span class="sxs-lookup"><span data-stu-id="bb640-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="bb640-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="bb640-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="bb640-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="bb640-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="bb640-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="bb640-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="bb640-173">**評估**</span><span class="sxs-lookup"><span data-stu-id="bb640-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="bb640-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="bb640-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="bb640-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="bb640-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="bb640-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="bb640-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="bb640-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="bb640-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="bb640-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="bb640-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="bb640-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="bb640-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="bb640-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="bb640-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="bb640-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="bb640-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="bb640-182">IsString</span><span class="sxs-lookup"><span data-stu-id="bb640-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="bb640-183">**數學運算**</span><span class="sxs-lookup"><span data-stu-id="bb640-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="bb640-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="bb640-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="bb640-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="bb640-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="bb640-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="bb640-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="bb640-187">**多重值**</span><span class="sxs-lookup"><span data-stu-id="bb640-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="bb640-188">Contains</span><span class="sxs-lookup"><span data-stu-id="bb640-188">Contains</span></span>](#contains) |[<span data-ttu-id="bb640-189">Count</span><span class="sxs-lookup"><span data-stu-id="bb640-189">Count</span></span>](#count) |[<span data-ttu-id="bb640-190">Item</span><span class="sxs-lookup"><span data-stu-id="bb640-190">Item</span></span>](#item) |[<span data-ttu-id="bb640-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="bb640-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="bb640-192">Join</span><span class="sxs-lookup"><span data-stu-id="bb640-192">Join</span></span>](#join) |[<span data-ttu-id="bb640-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="bb640-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="bb640-194">Split</span><span class="sxs-lookup"><span data-stu-id="bb640-194">Split</span></span>](#split) | | |
| <span data-ttu-id="bb640-195">**程式流程**</span><span class="sxs-lookup"><span data-stu-id="bb640-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="bb640-196">Error</span><span class="sxs-lookup"><span data-stu-id="bb640-196">Error</span></span>](#error) |[<span data-ttu-id="bb640-197">IIF</span><span class="sxs-lookup"><span data-stu-id="bb640-197">IIF</span></span>](#iif) |[<span data-ttu-id="bb640-198">選取</span><span class="sxs-lookup"><span data-stu-id="bb640-198">Select</span></span>](#select) |[<span data-ttu-id="bb640-199">Switch</span><span class="sxs-lookup"><span data-stu-id="bb640-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="bb640-200">其中</span><span class="sxs-lookup"><span data-stu-id="bb640-200">Where</span></span>](#where) |[<span data-ttu-id="bb640-201">With</span><span class="sxs-lookup"><span data-stu-id="bb640-201">With</span></span>](#with) | | | |
| <span data-ttu-id="bb640-202">**文字**</span><span class="sxs-lookup"><span data-stu-id="bb640-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="bb640-203">GUID</span><span class="sxs-lookup"><span data-stu-id="bb640-203">GUID</span></span>](#guid) |[<span data-ttu-id="bb640-204">InStr</span><span class="sxs-lookup"><span data-stu-id="bb640-204">InStr</span></span>](#instr) |[<span data-ttu-id="bb640-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="bb640-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="bb640-206">LCase</span><span class="sxs-lookup"><span data-stu-id="bb640-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="bb640-207">Left</span><span class="sxs-lookup"><span data-stu-id="bb640-207">Left</span></span>](#left) |[<span data-ttu-id="bb640-208">Len</span><span class="sxs-lookup"><span data-stu-id="bb640-208">Len</span></span>](#len) |[<span data-ttu-id="bb640-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="bb640-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="bb640-210">Mid</span><span class="sxs-lookup"><span data-stu-id="bb640-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="bb640-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="bb640-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="bb640-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="bb640-212">PadRight</span></span>](#padright) |[<span data-ttu-id="bb640-213">PCase</span><span class="sxs-lookup"><span data-stu-id="bb640-213">PCase</span></span>](#pcase) |[<span data-ttu-id="bb640-214">Replace</span><span class="sxs-lookup"><span data-stu-id="bb640-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="bb640-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="bb640-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="bb640-216">Right</span><span class="sxs-lookup"><span data-stu-id="bb640-216">Right</span></span>](#right) |[<span data-ttu-id="bb640-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="bb640-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="bb640-218">Trim</span><span class="sxs-lookup"><span data-stu-id="bb640-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="bb640-219">UCase</span><span class="sxs-lookup"><span data-stu-id="bb640-219">UCase</span></span>](#ucase) |[<span data-ttu-id="bb640-220">Word</span><span class="sxs-lookup"><span data-stu-id="bb640-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="bb640-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="bb640-221">BitAnd</span></span>
<span data-ttu-id="bb640-222">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-222">**Description:**</span></span>  
<span data-ttu-id="bb640-223">hello BitAnd 函式會設定指定的位元的值。</span><span class="sxs-lookup"><span data-stu-id="bb640-223">hello BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="bb640-224">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="bb640-225">value1，value2：應該使用 AND 連結在一起的數值</span><span class="sxs-lookup"><span data-stu-id="bb640-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="bb640-226">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-226">**Remarks:**</span></span>  
<span data-ttu-id="bb640-227">此函式會將這兩個參數 toohello 二進位表示，轉換和位元設定為：</span><span class="sxs-lookup"><span data-stu-id="bb640-227">This function converts both parameters toohello binary representation and sets a bit to:</span></span>

* <span data-ttu-id="bb640-228">0-如果一或兩個 hello 對應位元*遮罩*和*旗標*為 0</span><span class="sxs-lookup"><span data-stu-id="bb640-228">0 - if one or both of hello corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="bb640-229">1-如果兩個 hello 對應位元都是 1。</span><span class="sxs-lookup"><span data-stu-id="bb640-229">1 - if both of hello corresponding bits are 1.</span></span>

<span data-ttu-id="bb640-230">換句話說，它會傳回 0 在所有情況下，除非 hello 這兩個參數的對應位元是 1。</span><span class="sxs-lookup"><span data-stu-id="bb640-230">In other words, it returns 0 in all cases except when hello corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="bb640-231">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="bb640-232">因為十六進位"F"和"F7"評估 toothis 值會傳回 7。</span><span class="sxs-lookup"><span data-stu-id="bb640-232">Returns 7 because hexadecimal "F" AND "F7" evaluate toothis value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="bb640-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="bb640-233">BitOr</span></span>
<span data-ttu-id="bb640-234">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-234">**Description:**</span></span>  
<span data-ttu-id="bb640-235">hello BitOr 函式會設定指定的位元的值。</span><span class="sxs-lookup"><span data-stu-id="bb640-235">hello BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="bb640-236">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="bb640-237">value1，value2：應該使用 OR 連結在一起的數值</span><span class="sxs-lookup"><span data-stu-id="bb640-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="bb640-238">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-238">**Remarks:**</span></span>  
<span data-ttu-id="bb640-239">此函式會將這兩個參數 toohello 二進位表示，轉換，並設定位元 too1，如果一或兩個 hello 遮罩和旗標的對應位元為 1 和 too0 如果兩個 hello 對應位元為 0。</span><span class="sxs-lookup"><span data-stu-id="bb640-239">This function converts both parameters toohello binary representation and sets a bit too1 if one or both of hello corresponding bits in mask and flag are 1, and too0 if both of hello corresponding bits are 0.</span></span> <span data-ttu-id="bb640-240">換句話說，它會傳回 1 在所有情況下，除了 hello 這兩個參數的對應位元是 0。</span><span class="sxs-lookup"><span data-stu-id="bb640-240">In other words, it returns 1 in all cases except where hello corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="bb640-241">CBool</span><span class="sxs-lookup"><span data-stu-id="bb640-241">CBool</span></span>
<span data-ttu-id="bb640-242">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-242">**Description:**</span></span>  
<span data-ttu-id="bb640-243">hello CBool 函式會傳回布林值根據 hello 評估運算式</span><span class="sxs-lookup"><span data-stu-id="bb640-243">hello CBool function returns a Boolean based on hello evaluated expression</span></span>

<span data-ttu-id="bb640-244">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="bb640-245">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-245">**Remarks:**</span></span>  
<span data-ttu-id="bb640-246">如果 hello 運算式會評估 tooa 則為非零值，然後 CBool 會傳回 True，否則它會傳回 False。</span><span class="sxs-lookup"><span data-stu-id="bb640-246">If hello expression evaluates tooa nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="bb640-247">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="bb640-248">傳回 True，如果兩個屬性都有 hello 相同的值。</span><span class="sxs-lookup"><span data-stu-id="bb640-248">Returns True if both attributes have hello same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="bb640-249">CDate</span><span class="sxs-lookup"><span data-stu-id="bb640-249">CDate</span></span>
<span data-ttu-id="bb640-250">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-250">**Description:**</span></span>  
<span data-ttu-id="bb640-251">hello CDate 函數從字串傳回 UTC DateTime。</span><span class="sxs-lookup"><span data-stu-id="bb640-251">hello CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="bb640-252">DateTime 不是同步處理中的原生屬性類型，但有部分函式會用到。</span><span class="sxs-lookup"><span data-stu-id="bb640-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="bb640-253">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="bb640-254">Value：包含日期、時間和選擇性時區的字串</span><span class="sxs-lookup"><span data-stu-id="bb640-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="bb640-255">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-255">**Remarks:**</span></span>  
<span data-ttu-id="bb640-256">hello 傳回字串一律是 utc 格式。</span><span class="sxs-lookup"><span data-stu-id="bb640-256">hello returned string is always in UTC.</span></span>

<span data-ttu-id="bb640-257">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="bb640-258">傳回根據 hello 員工的開始時間的 DateTime</span><span class="sxs-lookup"><span data-stu-id="bb640-258">Returns a DateTime based on hello employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="bb640-259">傳回代表 "2013-01-11 12:00 AM" 的 DateTime</span><span class="sxs-lookup"><span data-stu-id="bb640-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="bb640-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="bb640-260">CertExtensionOids</span></span>
<span data-ttu-id="bb640-261">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-261">**Description:**</span></span>  
<span data-ttu-id="bb640-262">傳回 hello 所有 hello 重要的延伸的憑證物件的 Oid 值。</span><span class="sxs-lookup"><span data-stu-id="bb640-262">Returns hello Oid values of all hello critical extensions of a certificate object.</span></span>

<span data-ttu-id="bb640-263">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="bb640-264">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-265">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-265">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="bb640-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="bb640-266">CertFormat</span></span>
<span data-ttu-id="bb640-267">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-267">**Description:**</span></span>  
<span data-ttu-id="bb640-268">傳回 hello hello 格式的這個 X.509v3 憑證的名稱。</span><span class="sxs-lookup"><span data-stu-id="bb640-268">Returns hello name of hello format of this X.509v3 certificate.</span></span>

<span data-ttu-id="bb640-269">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="bb640-270">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-271">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-271">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="bb640-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="bb640-272">CertFriendlyName</span></span>
<span data-ttu-id="bb640-273">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-273">**Description:**</span></span>  
<span data-ttu-id="bb640-274">傳回 hello 別名相關聯的憑證。</span><span class="sxs-lookup"><span data-stu-id="bb640-274">Returns hello associated alias for a certificate.</span></span>

<span data-ttu-id="bb640-275">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="bb640-276">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-277">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-277">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="bb640-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="bb640-278">CertHashString</span></span>
<span data-ttu-id="bb640-279">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-279">**Description:**</span></span>  
<span data-ttu-id="bb640-280">傳回做為十六進位字串 hello hello X.509v3 憑證的 SHA1 雜湊值。</span><span class="sxs-lookup"><span data-stu-id="bb640-280">Returns hello SHA1 hash value for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="bb640-281">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="bb640-282">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-283">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-283">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="bb640-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="bb640-284">CertIssuer</span></span>
<span data-ttu-id="bb640-285">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-285">**Description:**</span></span>  
<span data-ttu-id="bb640-286">傳回 hello hello 憑證授權單位發出 hello X.509v3 憑證的名稱。</span><span class="sxs-lookup"><span data-stu-id="bb640-286">Returns hello name of hello certificate authority that issued hello X.509v3 certificate.</span></span>

<span data-ttu-id="bb640-287">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="bb640-288">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-289">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-289">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="bb640-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="bb640-290">CertIssuerDN</span></span>
<span data-ttu-id="bb640-291">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-291">**Description:**</span></span>  
<span data-ttu-id="bb640-292">傳回 hello hello 憑證簽發者辨別的名稱。</span><span class="sxs-lookup"><span data-stu-id="bb640-292">Returns hello distinguished name of hello certificate issuer.</span></span>

<span data-ttu-id="bb640-293">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="bb640-294">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-295">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-295">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="bb640-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="bb640-296">CertIssuerOid</span></span>
<span data-ttu-id="bb640-297">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-297">**Description:**</span></span>  
<span data-ttu-id="bb640-298">傳回 hello hello 憑證簽發者的 Oid。</span><span class="sxs-lookup"><span data-stu-id="bb640-298">Returns hello Oid of hello certificate issuer.</span></span>

<span data-ttu-id="bb640-299">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="bb640-300">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-301">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-301">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="bb640-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="bb640-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="bb640-303">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-303">**Description:**</span></span>  
<span data-ttu-id="bb640-304">傳回這個 X.509v3 憑證做為字串的 hello 金鑰演算法資訊。</span><span class="sxs-lookup"><span data-stu-id="bb640-304">Returns hello key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="bb640-305">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="bb640-306">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-307">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-307">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="bb640-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="bb640-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="bb640-309">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-309">**Description:**</span></span>  
<span data-ttu-id="bb640-310">傳回做為十六進位字串的 hello hello X.509v3 憑證金鑰演算法參數。</span><span class="sxs-lookup"><span data-stu-id="bb640-310">Returns hello key algorithm parameters for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="bb640-311">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="bb640-312">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-313">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-313">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="bb640-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="bb640-314">CertNameInfo</span></span>
<span data-ttu-id="bb640-315">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-315">**Description:**</span></span>  
<span data-ttu-id="bb640-316">傳回 hello 主旨和簽發者名稱從憑證。</span><span class="sxs-lookup"><span data-stu-id="bb640-316">Returns hello subject and issuer names from a certificate.</span></span>

<span data-ttu-id="bb640-317">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="bb640-318">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-319">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-319">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="bb640-320">X509NameType: hello X509NameType hello 主體值。</span><span class="sxs-lookup"><span data-stu-id="bb640-320">X509NameType: hello X509NameType value for hello subject.</span></span>
*   <span data-ttu-id="bb640-321">includesIssuerName: true tooinclude hello 簽發者名稱。否則為 false。</span><span class="sxs-lookup"><span data-stu-id="bb640-321">includesIssuerName: true tooinclude hello issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="bb640-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="bb640-322">CertNotAfter</span></span>
<span data-ttu-id="bb640-323">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-323">**Description:**</span></span>  
<span data-ttu-id="bb640-324">傳回 hello 日期之後，憑證便不再有效的當地時間。</span><span class="sxs-lookup"><span data-stu-id="bb640-324">Returns hello date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="bb640-325">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="bb640-326">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-327">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-327">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="bb640-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="bb640-328">CertNotBefore</span></span>
<span data-ttu-id="bb640-329">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-329">**Description:**</span></span>  
<span data-ttu-id="bb640-330">憑證生效的當地時間傳回 hello 日期。</span><span class="sxs-lookup"><span data-stu-id="bb640-330">Returns hello date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="bb640-331">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="bb640-332">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-333">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-333">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="bb640-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="bb640-334">CertPublicKeyOid</span></span>
<span data-ttu-id="bb640-335">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-335">**Description:**</span></span>  
<span data-ttu-id="bb640-336">傳回 hello hello hello X.509v3 憑證公開金鑰的 Oid。</span><span class="sxs-lookup"><span data-stu-id="bb640-336">Returns hello Oid of hello public key for hello X.509v3 certificate.</span></span>

<span data-ttu-id="bb640-337">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="bb640-338">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-339">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-339">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="bb640-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="bb640-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="bb640-341">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-341">**Description:**</span></span>  
<span data-ttu-id="bb640-342">傳回 hello hello 公開金鑰參數 hello X.509v3 憑證的 Oid。</span><span class="sxs-lookup"><span data-stu-id="bb640-342">Returns hello Oid of hello public key parameters for hello X.509v3 certificate.</span></span>

<span data-ttu-id="bb640-343">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="bb640-344">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-345">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-345">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="bb640-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="bb640-346">CertSerialNumber</span></span>
<span data-ttu-id="bb640-347">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-347">**Description:**</span></span>  
<span data-ttu-id="bb640-348">傳回 hello 序號 hello X.509v3 憑證。</span><span class="sxs-lookup"><span data-stu-id="bb640-348">Returns hello serial number of hello X.509v3 certificate.</span></span>

<span data-ttu-id="bb640-349">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="bb640-350">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-351">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-351">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="bb640-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="bb640-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="bb640-353">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-353">**Description:**</span></span>  
<span data-ttu-id="bb640-354">傳回 hello hello 演算法的 Oid 用 toocreate hello 簽章的憑證。</span><span class="sxs-lookup"><span data-stu-id="bb640-354">Returns hello Oid of hello algorithm used toocreate hello signature of a certificate.</span></span>

<span data-ttu-id="bb640-355">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="bb640-356">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-357">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-357">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="bb640-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="bb640-358">CertSubject</span></span>
<span data-ttu-id="bb640-359">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-359">**Description:**</span></span>  
<span data-ttu-id="bb640-360">取得 hello 來自憑證的主旨辨別的名稱。</span><span class="sxs-lookup"><span data-stu-id="bb640-360">Gets hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="bb640-361">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="bb640-362">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-363">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-363">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="bb640-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="bb640-364">CertSubjectNameDN</span></span>
<span data-ttu-id="bb640-365">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-365">**Description:**</span></span>  
<span data-ttu-id="bb640-366">傳回 hello 來自憑證的主旨辨別的名稱。</span><span class="sxs-lookup"><span data-stu-id="bb640-366">Returns hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="bb640-367">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="bb640-368">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-369">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-369">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="bb640-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="bb640-370">CertSubjectNameOid</span></span>
<span data-ttu-id="bb640-371">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-371">**Description:**</span></span>  
<span data-ttu-id="bb640-372">傳回 hello hello 來自憑證的主體名稱的 Oid。</span><span class="sxs-lookup"><span data-stu-id="bb640-372">Returns hello Oid of hello subject name from a certificate.</span></span>

<span data-ttu-id="bb640-373">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="bb640-374">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-375">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-375">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="bb640-376">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="bb640-376">CertThumbprint</span></span>
<span data-ttu-id="bb640-377">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-377">**Description:**</span></span>  
<span data-ttu-id="bb640-378">傳回 hello 憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="bb640-378">Returns hello thumbprint of a certificate.</span></span>

<span data-ttu-id="bb640-379">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="bb640-380">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-381">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-381">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="bb640-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="bb640-382">CertVersion</span></span>
<span data-ttu-id="bb640-383">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-383">**Description:**</span></span>  
<span data-ttu-id="bb640-384">傳回 hello X.509 格式版本的憑證。</span><span class="sxs-lookup"><span data-stu-id="bb640-384">Returns hello X.509 format version of a certificate.</span></span>

<span data-ttu-id="bb640-385">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="bb640-386">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-387">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-387">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="bb640-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="bb640-388">CGuid</span></span>
<span data-ttu-id="bb640-389">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-389">**Description:**</span></span>  
<span data-ttu-id="bb640-390">hello CGuid 函數將 GUID tooits 二進位表示法 hello 字串表示轉換。</span><span class="sxs-lookup"><span data-stu-id="bb640-390">hello CGuid function converts hello string representation of a GUID tooits binary representation.</span></span>

<span data-ttu-id="bb640-391">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="bb640-392">使用此模式格式化的字串：xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 或 {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="bb640-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="bb640-393">Contains</span><span class="sxs-lookup"><span data-stu-id="bb640-393">Contains</span></span>
<span data-ttu-id="bb640-394">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-394">**Description:**</span></span>  
<span data-ttu-id="bb640-395">hello Contains 函數內尋找字串的多重值屬性</span><span class="sxs-lookup"><span data-stu-id="bb640-395">hello Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="bb640-396">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-396">**Syntax:**</span></span>  
<span data-ttu-id="bb640-397">`num Contains (mvstring attribute, str search)` - 區分大小寫</span><span class="sxs-lookup"><span data-stu-id="bb640-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="bb640-398">`num Contains (mvref attribute, str search)` - 區分大小寫</span><span class="sxs-lookup"><span data-stu-id="bb640-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="bb640-399">屬性： hello 多重值的屬性 toosearch。</span><span class="sxs-lookup"><span data-stu-id="bb640-399">attribute: hello multi-valued attribute toosearch.</span></span>
* <span data-ttu-id="bb640-400">搜尋： toofind hello 屬性中的字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-400">search: string toofind in hello attribute.</span></span>
* <span data-ttu-id="bb640-401">Casetype：CaseInsensitive 或 CaseSensitive。</span><span class="sxs-lookup"><span data-stu-id="bb640-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="bb640-402">其中 hello 找不到字串 hello 多重值屬性中傳回的索引。</span><span class="sxs-lookup"><span data-stu-id="bb640-402">Returns index in hello multi-valued attribute where hello string was found.</span></span> <span data-ttu-id="bb640-403">如果找不到 hello 字串，則傳回 0。</span><span class="sxs-lookup"><span data-stu-id="bb640-403">0 is returned if hello string is not found.</span></span>

<span data-ttu-id="bb640-404">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-404">**Remarks:**</span></span>  
<span data-ttu-id="bb640-405">對於多重值的字串屬性 hello 搜尋會尋找 hello 值子字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-405">For multi-valued string attributes, hello search finds substrings in hello values.</span></span>  
<span data-ttu-id="bb640-406">若為參考屬性 hello 搜尋的字串必須完全符合 hello 值 toobe 被視為相符。</span><span class="sxs-lookup"><span data-stu-id="bb640-406">For reference attributes, hello searched string must exactly match hello value toobe considered a match.</span></span>

<span data-ttu-id="bb640-407">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="bb640-408">如果 hello proxyAddresses 屬性具有主要電子郵件地址 (以大寫"SMTP:")，然後傳回 hello proxyAddress 屬性，否則會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="bb640-408">If hello proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return hello proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="bb640-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="bb640-409">ConvertFromBase64</span></span>
<span data-ttu-id="bb640-410">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-410">**Description:**</span></span>  
<span data-ttu-id="bb640-411">hello ConvertFromBase64 函數將 hello 指定 base64 編碼值 tooa 規則的字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-411">hello ConvertFromBase64 function converts hello specified base64 encoded value tooa regular string.</span></span>

<span data-ttu-id="bb640-412">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-412">**Syntax:**</span></span>  
<span data-ttu-id="bb640-413">`str ConvertFromBase64(str source)` - 假設使用 Unicode 進行編碼</span><span class="sxs-lookup"><span data-stu-id="bb640-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="bb640-414">source：Base64 編碼的字串</span><span class="sxs-lookup"><span data-stu-id="bb640-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="bb640-415">Encoding：Unicode、ASCII、UTF8</span><span class="sxs-lookup"><span data-stu-id="bb640-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="bb640-416">**範例**</span><span class="sxs-lookup"><span data-stu-id="bb640-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="bb640-417">這兩個範例都會傳回 "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="bb640-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="bb640-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="bb640-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="bb640-419">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-419">**Description:**</span></span>  
<span data-ttu-id="bb640-420">hello ConvertFromUTF8Hex 函數將 hello 指定的 UTF8 十六進位編碼值 tooa 字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-420">hello ConvertFromUTF8Hex function converts hello specified UTF8 Hex encoded value tooa string.</span></span>

<span data-ttu-id="bb640-421">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="bb640-422">source：UTF8 2 個位元組的編碼字串</span><span class="sxs-lookup"><span data-stu-id="bb640-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="bb640-423">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-423">**Remarks:**</span></span>  
<span data-ttu-id="bb640-424">hello 差異此函式和 ConvertFromBase64([],UTF8) hello 結果是易記的 hello DN 屬性。</span><span class="sxs-lookup"><span data-stu-id="bb640-424">hello difference between this function and ConvertFromBase64([],UTF8) in that hello result is friendly for hello DN attribute.</span></span>  
<span data-ttu-id="bb640-425">Azure Active Directory 會使用此格式做為 DN。</span><span class="sxs-lookup"><span data-stu-id="bb640-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="bb640-426">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="bb640-427">傳回 "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="bb640-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="bb640-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="bb640-428">ConvertToBase64</span></span>
<span data-ttu-id="bb640-429">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-429">**Description:**</span></span>  
<span data-ttu-id="bb640-430">hello ConvertToBase64 函數將轉換字串 tooa Unicode base64 字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-430">hello ConvertToBase64 function converts a string tooa Unicode base64 string.</span></span>  
<span data-ttu-id="bb640-431">將 hello 值陣列使用 base-64 位數編碼的整數 tooits 相等字串表示的轉換。</span><span class="sxs-lookup"><span data-stu-id="bb640-431">Converts hello value of an array of integers tooits equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="bb640-432">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="bb640-433">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="bb640-434">傳回 "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span><span class="sxs-lookup"><span data-stu-id="bb640-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="bb640-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="bb640-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="bb640-436">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-436">**Description:**</span></span>  
<span data-ttu-id="bb640-437">hello ConvertToUTF8Hex 函數將轉換字串 tooa UTF8 十六進位編碼值。</span><span class="sxs-lookup"><span data-stu-id="bb640-437">hello ConvertToUTF8Hex function converts a string tooa UTF8 Hex encoded value.</span></span>

<span data-ttu-id="bb640-438">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="bb640-439">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-439">**Remarks:**</span></span>  
<span data-ttu-id="bb640-440">Azure Active directory 使用此函式的 hello 輸出格式作為 DN 屬性格式。</span><span class="sxs-lookup"><span data-stu-id="bb640-440">hello output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="bb640-441">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="bb640-442">傳回 48656C6C6F20776F726C6421</span><span class="sxs-lookup"><span data-stu-id="bb640-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="bb640-443">Count</span><span class="sxs-lookup"><span data-stu-id="bb640-443">Count</span></span>
<span data-ttu-id="bb640-444">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-444">**Description:**</span></span>  
<span data-ttu-id="bb640-445">hello Count 函數傳回多重值屬性中的 hello 項目數</span><span class="sxs-lookup"><span data-stu-id="bb640-445">hello Count function returns hello number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="bb640-446">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="bb640-447">CNum</span><span class="sxs-lookup"><span data-stu-id="bb640-447">CNum</span></span>
<span data-ttu-id="bb640-448">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-448">**Description:**</span></span>  
<span data-ttu-id="bb640-449">hello CNum 函數接受字串，並傳回數值資料類型。</span><span class="sxs-lookup"><span data-stu-id="bb640-449">hello CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="bb640-450">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="bb640-451">CRef</span><span class="sxs-lookup"><span data-stu-id="bb640-451">CRef</span></span>
<span data-ttu-id="bb640-452">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-452">**Description:**</span></span>  
<span data-ttu-id="bb640-453">轉換字串 tooa 參考屬性</span><span class="sxs-lookup"><span data-stu-id="bb640-453">Converts a string tooa reference attribute</span></span>

<span data-ttu-id="bb640-454">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="bb640-455">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="bb640-456">CStr</span><span class="sxs-lookup"><span data-stu-id="bb640-456">CStr</span></span>
<span data-ttu-id="bb640-457">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-457">**Description:**</span></span>  
<span data-ttu-id="bb640-458">hello CStr 函式將 tooa 字串資料類型轉換。</span><span class="sxs-lookup"><span data-stu-id="bb640-458">hello CStr function converts tooa string data type.</span></span>

<span data-ttu-id="bb640-459">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="bb640-460">value：可以是數值、參考屬性或布林值。</span><span class="sxs-lookup"><span data-stu-id="bb640-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="bb640-461">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="bb640-462">可能傳回 "cn=Joe,dc=contoso,dc=com"</span><span class="sxs-lookup"><span data-stu-id="bb640-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="bb640-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="bb640-463">DateAdd</span></span>
<span data-ttu-id="bb640-464">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-464">**Description:**</span></span>  
<span data-ttu-id="bb640-465">傳回包含日期 toowhich 已加入指定的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="bb640-465">Returns a Date containing a date toowhich a specified time interval has been added.</span></span>

<span data-ttu-id="bb640-466">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="bb640-467">間隔： 字串是 hello 想 tooadd 的時間間隔的運算式。</span><span class="sxs-lookup"><span data-stu-id="bb640-467">interval: String expression that is hello interval of time you want tooadd.</span></span> <span data-ttu-id="bb640-468">hello 字串必須有一個 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="bb640-468">hello string must have one of hello following values:</span></span>
  * <span data-ttu-id="bb640-469">yyyy 年</span><span class="sxs-lookup"><span data-stu-id="bb640-469">yyyy Year</span></span>
  * <span data-ttu-id="bb640-470">q 季</span><span class="sxs-lookup"><span data-stu-id="bb640-470">q Quarter</span></span>
  * <span data-ttu-id="bb640-471">m 月</span><span class="sxs-lookup"><span data-stu-id="bb640-471">m Month</span></span>
  * <span data-ttu-id="bb640-472">y 一年中第幾天</span><span class="sxs-lookup"><span data-stu-id="bb640-472">y Day of year</span></span>
  * <span data-ttu-id="bb640-473">d 日</span><span class="sxs-lookup"><span data-stu-id="bb640-473">d Day</span></span>
  * <span data-ttu-id="bb640-474">w 工作日</span><span class="sxs-lookup"><span data-stu-id="bb640-474">w Weekday</span></span>
  * <span data-ttu-id="bb640-475">ww 周</span><span class="sxs-lookup"><span data-stu-id="bb640-475">ww Week</span></span>
  * <span data-ttu-id="bb640-476">h 小時</span><span class="sxs-lookup"><span data-stu-id="bb640-476">h Hour</span></span>
  * <span data-ttu-id="bb640-477">n 分鐘</span><span class="sxs-lookup"><span data-stu-id="bb640-477">n Minute</span></span>
  * <span data-ttu-id="bb640-478">s 秒</span><span class="sxs-lookup"><span data-stu-id="bb640-478">s Second</span></span>
* <span data-ttu-id="bb640-479">值： hello 數目要 tooadd 的單位。</span><span class="sxs-lookup"><span data-stu-id="bb640-479">value: hello number of units you want tooadd.</span></span> <span data-ttu-id="bb640-480">它可以是正數 （tooget 日期在未來的 hello） 或負 （tooget 日期在過去的 hello）。</span><span class="sxs-lookup"><span data-stu-id="bb640-480">It can be positive (tooget dates in hello future) or negative (tooget dates in hello past).</span></span>
* <span data-ttu-id="bb640-481">日期： 日期時間表示的日期 toowhich hello 間隔加入。</span><span class="sxs-lookup"><span data-stu-id="bb640-481">date: DateTime representing date toowhich hello interval is added.</span></span>

<span data-ttu-id="bb640-482">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="bb640-483">新增 3 個月，並傳回代表 "2001-04-01" 的 DateTime。</span><span class="sxs-lookup"><span data-stu-id="bb640-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="bb640-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="bb640-484">DateFromNum</span></span>
<span data-ttu-id="bb640-485">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-485">**Description:**</span></span>  
<span data-ttu-id="bb640-486">hello DateFromNum 函數將 AD 日期格式 tooa DateTime 型別中的值轉換。</span><span class="sxs-lookup"><span data-stu-id="bb640-486">hello DateFromNum function converts a value in AD’s date format tooa DateTime type.</span></span>

<span data-ttu-id="bb640-487">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="bb640-488">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="bb640-489">傳回代表 2012-01-01 23:00:00 的 DateTime</span><span class="sxs-lookup"><span data-stu-id="bb640-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="bb640-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="bb640-490">DNComponent</span></span>
<span data-ttu-id="bb640-491">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-491">**Description:**</span></span>  
<span data-ttu-id="bb640-492">hello DNComponent 函數會傳回指定之 DN 元件謔韺 hello 值。</span><span class="sxs-lookup"><span data-stu-id="bb640-492">hello DNComponent function returns hello value of a specified DN component going from left.</span></span>

<span data-ttu-id="bb640-493">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="bb640-494">dn: hello 參考屬性 toointerpret</span><span class="sxs-lookup"><span data-stu-id="bb640-494">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="bb640-495">在 hello DN tooreturn ComponentNumber: hello 元件</span><span class="sxs-lookup"><span data-stu-id="bb640-495">ComponentNumber: hello component in hello DN tooreturn</span></span>

<span data-ttu-id="bb640-496">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="bb640-497">如果 dn 為 "cn=Joe,ou=…"，就會傳回 Joe</span><span class="sxs-lookup"><span data-stu-id="bb640-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="bb640-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="bb640-498">DNComponentRev</span></span>
<span data-ttu-id="bb640-499">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-499">**Description:**</span></span>  
<span data-ttu-id="bb640-500">hello DNComponentRev 函數會傳回指定之 DN 元件從右邊 （hello 尾端） hello 值。</span><span class="sxs-lookup"><span data-stu-id="bb640-500">hello DNComponentRev function returns hello value of a specified DN component going from right (hello end).</span></span>

<span data-ttu-id="bb640-501">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="bb640-502">dn: hello 參考屬性 toointerpret</span><span class="sxs-lookup"><span data-stu-id="bb640-502">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="bb640-503">ComponentNumber-hello DN tooreturn 中的 hello 元件</span><span class="sxs-lookup"><span data-stu-id="bb640-503">ComponentNumber - hello component in hello DN tooreturn</span></span>
* <span data-ttu-id="bb640-504">Options：DC - 忽略所有含 "dc=" 的元件</span><span class="sxs-lookup"><span data-stu-id="bb640-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="bb640-505">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-505">**Example:**</span></span>  
<span data-ttu-id="bb640-506">如果 dn 是 "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com"，則</span><span class="sxs-lookup"><span data-stu-id="bb640-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="bb640-507">兩者都傳回 US。</span><span class="sxs-lookup"><span data-stu-id="bb640-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="bb640-508">Error</span><span class="sxs-lookup"><span data-stu-id="bb640-508">Error</span></span>
<span data-ttu-id="bb640-509">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-509">**Description:**</span></span>  
<span data-ttu-id="bb640-510">hello 錯誤函式是使用的 tooreturn 自訂錯誤。</span><span class="sxs-lookup"><span data-stu-id="bb640-510">hello Error function is used tooreturn a custom error.</span></span>

<span data-ttu-id="bb640-511">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="bb640-512">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="bb640-513">如果 hello 屬性 accountName 不存在，擲回錯誤，hello 物件上。</span><span class="sxs-lookup"><span data-stu-id="bb640-513">If hello attribute accountName is not present, throw an error on hello object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="bb640-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="bb640-514">EscapeDNComponent</span></span>
<span data-ttu-id="bb640-515">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-515">**Description:**</span></span>  
<span data-ttu-id="bb640-516">hello EscapeDNComponent 函數接受 DN 的一個元件，並能夠以 LDAP 表示逸出。</span><span class="sxs-lookup"><span data-stu-id="bb640-516">hello EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="bb640-517">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="bb640-518">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="bb640-519">可確保即使 hello displayName 屬性具有 LDAP 中必須逸出的字元，可以在 LDAP 目錄中建立 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="bb640-519">Makes sure hello object can be created in an LDAP directory even if hello displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="bb640-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="bb640-520">FormatDateTime</span></span>
<span data-ttu-id="bb640-521">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-521">**Description:**</span></span>  
<span data-ttu-id="bb640-522">hello FormatDateTime 函式是使用的 tooformat DateTime tooa 字串與指定的格式</span><span class="sxs-lookup"><span data-stu-id="bb640-522">hello FormatDateTime function is used tooformat a DateTime tooa string with a specified format</span></span>

<span data-ttu-id="bb640-523">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="bb640-524">值： hello 日期時間格式的值</span><span class="sxs-lookup"><span data-stu-id="bb640-524">value: a value in hello DateTime format</span></span>
* <span data-ttu-id="bb640-525">格式： 字串，表示要 hello 格式 tooconvert。</span><span class="sxs-lookup"><span data-stu-id="bb640-525">format: a string representing hello format tooconvert to.</span></span>

<span data-ttu-id="bb640-526">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-526">**Remarks:**</span></span>  
<span data-ttu-id="bb640-527">hello 可能的值為 hello 格式可以在這裡找到：[使用者定義日期/時間格式 （Format 函數）](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="bb640-527">hello possible values for hello format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="bb640-528">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="bb640-529">結果是 "2007-12-25"。</span><span class="sxs-lookup"><span data-stu-id="bb640-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="bb640-530">會產生 "20140905081453.0Z"</span><span class="sxs-lookup"><span data-stu-id="bb640-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="bb640-531">GUID</span><span class="sxs-lookup"><span data-stu-id="bb640-531">GUID</span></span>
<span data-ttu-id="bb640-532">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-532">**Description:**</span></span>  
<span data-ttu-id="bb640-533">hello 函式 GUID 會產生新的隨機 GUID</span><span class="sxs-lookup"><span data-stu-id="bb640-533">hello function GUID generates a new random GUID</span></span>

<span data-ttu-id="bb640-534">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="bb640-535">IIF</span><span class="sxs-lookup"><span data-stu-id="bb640-535">IIF</span></span>
<span data-ttu-id="bb640-536">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-536">**Description:**</span></span>  
<span data-ttu-id="bb640-537">hello IIF 函數傳回的一組指定的條件為基礎的可能值的其中一個。</span><span class="sxs-lookup"><span data-stu-id="bb640-537">hello IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="bb640-538">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="bb640-539">條件： 任何值或運算式可以評估 tootrue 或 false。</span><span class="sxs-lookup"><span data-stu-id="bb640-539">condition: any value or expression that can be evaluated tootrue or false.</span></span>
* <span data-ttu-id="bb640-540">valueIfTrue: hello tootrue 評估 hello 條件，如果傳回值。</span><span class="sxs-lookup"><span data-stu-id="bb640-540">valueIfTrue: If hello condition evaluates tootrue, hello returned value.</span></span>
* <span data-ttu-id="bb640-541">valueIfFalse: hello toofalse 評估 hello 條件，如果傳回值。</span><span class="sxs-lookup"><span data-stu-id="bb640-541">valueIfFalse: If hello condition evaluates toofalse, hello returned value.</span></span>

<span data-ttu-id="bb640-542">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="bb640-543">如果 hello 使用者是實習生，會傳回 hello 別名"t-"的使用者加入 toohello 開頭，否則傳回現況的 hello 使用者的別名。</span><span class="sxs-lookup"><span data-stu-id="bb640-543">If hello user is an intern, returns hello alias of a user with "t-" added toohello beginning of it, else returns hello user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="bb640-544">InStr</span><span class="sxs-lookup"><span data-stu-id="bb640-544">InStr</span></span>
<span data-ttu-id="bb640-545">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-545">**Description:**</span></span>  
<span data-ttu-id="bb640-546">hello InStr 函數在字串中尋找 hello 的子字串的第一個出現項目</span><span class="sxs-lookup"><span data-stu-id="bb640-546">hello InStr function finds hello first occurrence of a substring in a string</span></span>

<span data-ttu-id="bb640-547">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="bb640-548">stringcheck: toobe 搜尋的字串</span><span class="sxs-lookup"><span data-stu-id="bb640-548">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="bb640-549">stringmatch: toobe 找到的字串</span><span class="sxs-lookup"><span data-stu-id="bb640-549">stringmatch: string toobe found</span></span>
* <span data-ttu-id="bb640-550">開始： 開始位置 toofind hello 子字串</span><span class="sxs-lookup"><span data-stu-id="bb640-550">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="bb640-551">compare：vbTextCompare 或 vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="bb640-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="bb640-552">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-552">**Remarks:**</span></span>  
<span data-ttu-id="bb640-553">傳回 hello 位置找 hello substring 或 0 如果找不到。</span><span class="sxs-lookup"><span data-stu-id="bb640-553">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="bb640-554">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-554">**Example:**</span></span>  
`InStr("hello quick brown fox","quick")`  
<span data-ttu-id="bb640-555">/ / 評估 too5</span><span class="sxs-lookup"><span data-stu-id="bb640-555">Evalues too5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="bb640-556">評估 too7</span><span class="sxs-lookup"><span data-stu-id="bb640-556">Evaluates too7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="bb640-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="bb640-557">InStrRev</span></span>
<span data-ttu-id="bb640-558">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-558">**Description:**</span></span>  
<span data-ttu-id="bb640-559">hello InStrRev 函數在字串中尋找子字串 hello 最後一個項目</span><span class="sxs-lookup"><span data-stu-id="bb640-559">hello InStrRev function finds hello last occurrence of a substring in a string</span></span>

<span data-ttu-id="bb640-560">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="bb640-561">stringcheck: toobe 搜尋的字串</span><span class="sxs-lookup"><span data-stu-id="bb640-561">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="bb640-562">stringmatch: toobe 找到的字串</span><span class="sxs-lookup"><span data-stu-id="bb640-562">stringmatch: string toobe found</span></span>
* <span data-ttu-id="bb640-563">開始： 開始位置 toofind hello 子字串</span><span class="sxs-lookup"><span data-stu-id="bb640-563">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="bb640-564">compare：vbTextCompare 或 vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="bb640-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="bb640-565">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-565">**Remarks:**</span></span>  
<span data-ttu-id="bb640-566">傳回 hello 位置找 hello substring 或 0 如果找不到。</span><span class="sxs-lookup"><span data-stu-id="bb640-566">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="bb640-567">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="bb640-568">傳回 7</span><span class="sxs-lookup"><span data-stu-id="bb640-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="bb640-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="bb640-569">IsBitSet</span></span>
<span data-ttu-id="bb640-570">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-570">**Description:**</span></span>  
<span data-ttu-id="bb640-571">hello IsBitSet 函數測試的位元設定</span><span class="sxs-lookup"><span data-stu-id="bb640-571">hello function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="bb640-572">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="bb640-573">值： 數值。 flag： 具有 hello 的數字值的位元 toobe 評估</span><span class="sxs-lookup"><span data-stu-id="bb640-573">value: a numeric value that is evaluated.flag: a numeric value that has hello bit toobe evaluated</span></span>

<span data-ttu-id="bb640-574">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="bb640-575">因為以十六進位值"F"hello 設定位元"4"，則傳回 True</span><span class="sxs-lookup"><span data-stu-id="bb640-575">Returns True because bit "4" is set in hello hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="bb640-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="bb640-576">IsDate</span></span>
<span data-ttu-id="bb640-577">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-577">**Description:**</span></span>  
<span data-ttu-id="bb640-578">如果 hello 運算式可以評估為 DateTime 型別，然後 hello IsDate 函數會評估 tooTrue。</span><span class="sxs-lookup"><span data-stu-id="bb640-578">If hello expression can be evaluates as a DateTime type, then hello IsDate function evaluates tooTrue.</span></span>

<span data-ttu-id="bb640-579">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="bb640-580">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-580">**Remarks:**</span></span>  
<span data-ttu-id="bb640-581">如果 cdate （） 可以成功，請使用 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="bb640-581">Used toodetermine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="bb640-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="bb640-582">IsCert</span></span>
<span data-ttu-id="bb640-583">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-583">**Description:**</span></span>  
<span data-ttu-id="bb640-584">如果.NET X509Certificate2 憑證物件可以序列化 hello 未經處理資料，則傳回 true。</span><span class="sxs-lookup"><span data-stu-id="bb640-584">Returns true if hello raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="bb640-585">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="bb640-586">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="bb640-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="bb640-587">編碼的二進位 (DER) 或 Base64 編碼 X.509 資料，可以是 hello 位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-587">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="bb640-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="bb640-588">IsEmpty</span></span>
<span data-ttu-id="bb640-589">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-589">**Description:**</span></span>  
<span data-ttu-id="bb640-590">如果 hello 屬性存在於 hello CS 或 MV 中，但會評估 tooan 空字串，然後 hello IsEmpty 函數會評估 tooTrue。</span><span class="sxs-lookup"><span data-stu-id="bb640-590">If hello attribute is present in hello CS or MV but evaluates tooan empty string, then hello IsEmpty function evaluates tooTrue.</span></span>

<span data-ttu-id="bb640-591">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="bb640-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="bb640-592">IsGuid</span></span>
<span data-ttu-id="bb640-593">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-593">**Description:**</span></span>  
<span data-ttu-id="bb640-594">如果 hello 字串無法轉換的 tooa GUID，IsGuid 函數會 hello 評估 tootrue。</span><span class="sxs-lookup"><span data-stu-id="bb640-594">If hello string could be converted tooa GUID, then hello IsGuid function evaluated tootrue.</span></span>

<span data-ttu-id="bb640-595">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="bb640-596">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-596">**Remarks:**</span></span>  
<span data-ttu-id="bb640-597">GUID 定義為下列其中一種模式的字串： xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 或 {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="bb640-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="bb640-598">如果 cguid （） 可以成功，請使用 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="bb640-598">Used toodetermine if CGuid() can be successful.</span></span>

<span data-ttu-id="bb640-599">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="bb640-600">如果 hello StrAttribute 是 GUID 格式，傳回的二進位表示法，否則會傳回 Null。</span><span class="sxs-lookup"><span data-stu-id="bb640-600">If hello StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="bb640-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="bb640-601">IsNull</span></span>
<span data-ttu-id="bb640-602">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-602">**Description:**</span></span>  
<span data-ttu-id="bb640-603">如果 hello 運算式評估 tooNull，則 hello IsNull 函數會傳回 true。</span><span class="sxs-lookup"><span data-stu-id="bb640-603">If hello expression evaluates tooNull, then hello IsNull function returns true.</span></span>

<span data-ttu-id="bb640-604">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="bb640-605">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-605">**Remarks:**</span></span>  
<span data-ttu-id="bb640-606">屬性，Null 表示 hello hello 屬性不存在。</span><span class="sxs-lookup"><span data-stu-id="bb640-606">For an attribute, a Null is expressed by hello absence of hello attribute.</span></span>

<span data-ttu-id="bb640-607">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="bb640-608">如果 hello 屬性不存在於 hello CS 或 MV 中，則傳回 True。</span><span class="sxs-lookup"><span data-stu-id="bb640-608">Returns True if hello attribute is not present in hello CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="bb640-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="bb640-609">IsNullOrEmpty</span></span>
<span data-ttu-id="bb640-610">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-610">**Description:**</span></span>  
<span data-ttu-id="bb640-611">如果 hello 運算式為 null 或空字串，則 hello IsNullOrEmpty 函數會傳回 true。</span><span class="sxs-lookup"><span data-stu-id="bb640-611">If hello expression is null or an empty string, then hello IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="bb640-612">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="bb640-613">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-613">**Remarks:**</span></span>  
<span data-ttu-id="bb640-614">屬性，這會評估 tooTrue 如果 hello 屬性不存在或雖然存在但為空字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-614">For an attribute, this would evaluate tooTrue if hello attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="bb640-615">此函式的 hello 反向名為 IsPresent。</span><span class="sxs-lookup"><span data-stu-id="bb640-615">hello inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="bb640-616">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="bb640-617">如果 hello 屬性不存在，或為空字串 hello CS 或 MV 中的，則傳回 True。</span><span class="sxs-lookup"><span data-stu-id="bb640-617">Returns True if hello attribute is not present or is an empty string in hello CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="bb640-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="bb640-618">IsNumeric</span></span>
<span data-ttu-id="bb640-619">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-619">**Description:**</span></span>  
<span data-ttu-id="bb640-620">hello IsNumeric 函數傳回布林值，指出是否可以當做數字 類型中評估運算式。</span><span class="sxs-lookup"><span data-stu-id="bb640-620">hello IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="bb640-621">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="bb640-622">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-622">**Remarks:**</span></span>  
<span data-ttu-id="bb640-623">如果 cnum （） 可以成功 tooparse hello 運算式，請使用 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="bb640-623">Used toodetermine if CNum() can be successful tooparse hello expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="bb640-624">IsString</span><span class="sxs-lookup"><span data-stu-id="bb640-624">IsString</span></span>
<span data-ttu-id="bb640-625">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-625">**Description:**</span></span>  
<span data-ttu-id="bb640-626">如果 hello 運算式可以評估的 tooa 字串類型，則 hello 別，IsString 函數會評估 tooTrue。</span><span class="sxs-lookup"><span data-stu-id="bb640-626">If hello expression can be evaluated tooa string type, then hello IsString function evaluates tooTrue.</span></span>

<span data-ttu-id="bb640-627">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="bb640-628">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-628">**Remarks:**</span></span>  
<span data-ttu-id="bb640-629">如果 cstr （） 可以是成功 tooparse hello 運算式，請使用 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="bb640-629">Used toodetermine if CStr() can be successful tooparse hello expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="bb640-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="bb640-630">IsPresent</span></span>
<span data-ttu-id="bb640-631">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-631">**Description:**</span></span>  
<span data-ttu-id="bb640-632">如果 hello 運算式評估 tooa 不是 Null，而不是空的字串，然後 hello 的 IsPresent 函數會傳回 true。</span><span class="sxs-lookup"><span data-stu-id="bb640-632">If hello expression evaluates tooa string that is not Null and is not empty, then hello IsPresent function returns true.</span></span>

<span data-ttu-id="bb640-633">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="bb640-634">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-634">**Remarks:**</span></span>  
<span data-ttu-id="bb640-635">此函式的 hello 反向名為 IsNullOrEmpty。</span><span class="sxs-lookup"><span data-stu-id="bb640-635">hello inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="bb640-636">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="bb640-637">Item</span><span class="sxs-lookup"><span data-stu-id="bb640-637">Item</span></span>
<span data-ttu-id="bb640-638">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-638">**Description:**</span></span>  
<span data-ttu-id="bb640-639">hello Item 函數從多重值字串/屬性，傳回一個項目。</span><span class="sxs-lookup"><span data-stu-id="bb640-639">hello Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="bb640-640">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="bb640-641">attribute：多重值的屬性</span><span class="sxs-lookup"><span data-stu-id="bb640-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="bb640-642">索引： hello 多重值字串中的索引 tooan 項目。</span><span class="sxs-lookup"><span data-stu-id="bb640-642">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="bb640-643">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-643">**Remarks:**</span></span>  
<span data-ttu-id="bb640-644">hello Item 函數適合與 hello Contains 函數一起因為 hello 第二個函式傳回 hello 多重值屬性中的 hello 索引 tooan 項目。</span><span class="sxs-lookup"><span data-stu-id="bb640-644">hello Item function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="bb640-645">如果索引超出範圍，即會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="bb640-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="bb640-646">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="bb640-647">傳回 hello 主要電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="bb640-647">Returns hello primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="bb640-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="bb640-648">ItemOrNull</span></span>
<span data-ttu-id="bb640-649">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-649">**Description:**</span></span>  
<span data-ttu-id="bb640-650">hello ItemOrNull 函數從多重值字串/屬性，傳回一個項目。</span><span class="sxs-lookup"><span data-stu-id="bb640-650">hello ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="bb640-651">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="bb640-652">attribute：多重值的屬性</span><span class="sxs-lookup"><span data-stu-id="bb640-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="bb640-653">索引： hello 多重值字串中的索引 tooan 項目。</span><span class="sxs-lookup"><span data-stu-id="bb640-653">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="bb640-654">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-654">**Remarks:**</span></span>  
<span data-ttu-id="bb640-655">hello ItemOrNull 函數適合與 Contains 函數 hello 因為 hello 第二個函式傳回 hello 多重值屬性中的 hello 索引 tooan 項目。</span><span class="sxs-lookup"><span data-stu-id="bb640-655">hello ItemOrNull function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="bb640-656">如果索引超出範圍，則會傳回 Null 值。</span><span class="sxs-lookup"><span data-stu-id="bb640-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="bb640-657">Join</span><span class="sxs-lookup"><span data-stu-id="bb640-657">Join</span></span>
<span data-ttu-id="bb640-658">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-658">**Description:**</span></span>  
<span data-ttu-id="bb640-659">hello Join 函數接受多重值的字串，並傳回單一值的字串與指定插入每個項目之間的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="bb640-659">hello Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="bb640-660">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="bb640-661">屬性： 多重值的屬性包含字串 toobe 聯結。</span><span class="sxs-lookup"><span data-stu-id="bb640-661">attribute: Multi-valued attribute containing strings toobe joined.</span></span>
* <span data-ttu-id="bb640-662">分隔符號： 任何字串，傳回字串 hello 中的，使用的 tooseparate hello 子字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-662">delimiter: Any string, used tooseparate hello substrings in hello returned string.</span></span> <span data-ttu-id="bb640-663">如果省略，hello 空格字元 ("") 會使用。</span><span class="sxs-lookup"><span data-stu-id="bb640-663">If omitted, hello space character (" ") is used.</span></span> <span data-ttu-id="bb640-664">如果 Delimiter 是零長度字串 ("") 或執行任何動作，而不使用分隔符號串連 hello 清單中的所有項目。</span><span class="sxs-lookup"><span data-stu-id="bb640-664">If Delimiter is a zero-length string ("") or Nothing, all items in hello list are concatenated with no delimiters.</span></span>

<span data-ttu-id="bb640-665">**備註**</span><span class="sxs-lookup"><span data-stu-id="bb640-665">**Remarks**</span></span>  
<span data-ttu-id="bb640-666">沒有 hello Join 和 Split 函數之間的同位檢查。</span><span class="sxs-lookup"><span data-stu-id="bb640-666">There is parity between hello Join and Split functions.</span></span> <span data-ttu-id="bb640-667">hello Join 函數接受字串陣列，並結合使用分隔符號字串，tooreturn 單一字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-667">hello Join function takes an array of strings and joins them using a delimiter string, tooreturn a single string.</span></span> <span data-ttu-id="bb640-668">hello Split 函數接受字串，並分隔在 hello 分隔符號，tooreturn 字串陣列。</span><span class="sxs-lookup"><span data-stu-id="bb640-668">hello Split function takes a string and separates it at hello delimiter, tooreturn an array of strings.</span></span> <span data-ttu-id="bb640-669">不過，主要的差別是 Join 可以使用任何分隔符號字串來串連字串，Split 只能使用單一字元分隔符號來分隔字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="bb640-670">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="bb640-671">可能傳回："SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="bb640-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="bb640-672">LCase</span><span class="sxs-lookup"><span data-stu-id="bb640-672">LCase</span></span>
<span data-ttu-id="bb640-673">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-673">**Description:**</span></span>  
<span data-ttu-id="bb640-674">hello LCase 函數將字串 toolower 案例中的所有字元都轉換。</span><span class="sxs-lookup"><span data-stu-id="bb640-674">hello LCase function converts all characters in a string toolower case.</span></span>

<span data-ttu-id="bb640-675">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="bb640-676">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="bb640-677">傳回 "test"。</span><span class="sxs-lookup"><span data-stu-id="bb640-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="bb640-678">Left</span><span class="sxs-lookup"><span data-stu-id="bb640-678">Left</span></span>
<span data-ttu-id="bb640-679">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-679">**Description:**</span></span>  
<span data-ttu-id="bb640-680">hello Left 的函數從字串 hello 左側傳回指定的字元數。</span><span class="sxs-lookup"><span data-stu-id="bb640-680">hello Left function returns a specified number of characters from hello left of a string.</span></span>

<span data-ttu-id="bb640-681">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="bb640-682">字串： hello tooreturn 字元字串</span><span class="sxs-lookup"><span data-stu-id="bb640-682">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="bb640-683">NumChars： 數字，識別 hello 從 hello 開頭 （左邊） 字串的字元 tooreturn 數目</span><span class="sxs-lookup"><span data-stu-id="bb640-683">NumChars: a number identifying hello number of characters tooreturn from hello beginning (left) of string</span></span>

<span data-ttu-id="bb640-684">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-684">**Remarks:**</span></span>  
<span data-ttu-id="bb640-685">字串，包含 hello 前面 numChars 個字元字串中：</span><span class="sxs-lookup"><span data-stu-id="bb640-685">A string containing hello first numChars characters in string:</span></span>

* <span data-ttu-id="bb640-686">如果 numChars = 0，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="bb640-687">如果 numChars < 0，會傳回輸入字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="bb640-688">如果 string 為 Null，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-688">If string is null, return empty string.</span></span>

<span data-ttu-id="bb640-689">如果字串包含字元少於 numChars 中指定的 hello 數字，則會傳回字串的相同 toostring （也就，包含參數 1 中的所有字元）。</span><span class="sxs-lookup"><span data-stu-id="bb640-689">If string contains fewer characters than hello number specified in numChars, a string identical toostring (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="bb640-690">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="bb640-691">傳回 "Joh"。</span><span class="sxs-lookup"><span data-stu-id="bb640-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="bb640-692">Len</span><span class="sxs-lookup"><span data-stu-id="bb640-692">Len</span></span>
<span data-ttu-id="bb640-693">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-693">**Description:**</span></span>  
<span data-ttu-id="bb640-694">hello Len 函數會傳回字串中的字元數。</span><span class="sxs-lookup"><span data-stu-id="bb640-694">hello Len function returns number of characters in a string.</span></span>

<span data-ttu-id="bb640-695">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="bb640-696">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="bb640-697">傳回 8</span><span class="sxs-lookup"><span data-stu-id="bb640-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="bb640-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="bb640-698">LTrim</span></span>
<span data-ttu-id="bb640-699">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-699">**Description:**</span></span>  
<span data-ttu-id="bb640-700">hello LTrim 函數從字串中移除開頭空白字元。</span><span class="sxs-lookup"><span data-stu-id="bb640-700">hello LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="bb640-701">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="bb640-702">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="bb640-703">傳回 "Test"</span><span class="sxs-lookup"><span data-stu-id="bb640-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="bb640-704">Mid</span><span class="sxs-lookup"><span data-stu-id="bb640-704">Mid</span></span>
<span data-ttu-id="bb640-705">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-705">**Description:**</span></span>  
<span data-ttu-id="bb640-706">hello Mid 函數從字串中指定位置傳回指定的字元數。</span><span class="sxs-lookup"><span data-stu-id="bb640-706">hello Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="bb640-707">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="bb640-708">字串： hello tooreturn 字元字串</span><span class="sxs-lookup"><span data-stu-id="bb640-708">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="bb640-709">開始： 數字，識別 hello 開始 tooreturn 字元字串中的位置</span><span class="sxs-lookup"><span data-stu-id="bb640-709">start: a number identifying hello starting position in string tooreturn characters from</span></span>
* <span data-ttu-id="bb640-710">NumChars： 數字，識別 hello 字元 tooreturn 從字串中的位置數目</span><span class="sxs-lookup"><span data-stu-id="bb640-710">NumChars: a number identifying hello number of characters tooreturn from position in string</span></span>

<span data-ttu-id="bb640-711">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-711">**Remarks:**</span></span>  
<span data-ttu-id="bb640-712">從 string 中的位置 start 開始傳回 numChars 個字元。</span><span class="sxs-lookup"><span data-stu-id="bb640-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="bb640-713">包含從 string 中的位置 start 起算的 numChars 個字元的字串：</span><span class="sxs-lookup"><span data-stu-id="bb640-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="bb640-714">如果 numChars = 0，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="bb640-715">如果 numChars < 0，會傳回輸入字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="bb640-716">如果啟動 > hello 字串的長度，傳回輸入的字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-716">If start > hello length of string, return input string.</span></span>
* <span data-ttu-id="bb640-717">如果 start < = 0，會傳回輸入字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="bb640-718">如果 string 為 Null，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-718">If string is null, return empty string.</span></span>

<span data-ttu-id="bb640-719">如果 string 中從位置 start 起算所剩餘的字元數不足 numChar 個字元，即會盡可能地傳回許多字元。</span><span class="sxs-lookup"><span data-stu-id="bb640-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="bb640-720">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="bb640-721">傳回 "hn Do"。</span><span class="sxs-lookup"><span data-stu-id="bb640-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="bb640-722">傳回 "Doe"</span><span class="sxs-lookup"><span data-stu-id="bb640-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="bb640-723">Now</span><span class="sxs-lookup"><span data-stu-id="bb640-723">Now</span></span>
<span data-ttu-id="bb640-724">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-724">**Description:**</span></span>  
<span data-ttu-id="bb640-725">hello 現在函式會傳回指定 hello 目前的日期和時間，根據 tooyour 電腦的系統日期和時間的日期時間。</span><span class="sxs-lookup"><span data-stu-id="bb640-725">hello Now function returns a DateTime specifying hello current date and time, according tooyour computer's system date and time.</span></span>

<span data-ttu-id="bb640-726">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="bb640-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="bb640-727">NumFromDate</span></span>
<span data-ttu-id="bb640-728">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-728">**Description:**</span></span>  
<span data-ttu-id="bb640-729">hello NumFromDate 函數傳回 AD 日期格式的日期。</span><span class="sxs-lookup"><span data-stu-id="bb640-729">hello NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="bb640-730">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="bb640-731">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="bb640-732">傳回 129699324000000000</span><span class="sxs-lookup"><span data-stu-id="bb640-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="bb640-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="bb640-733">PadLeft</span></span>
<span data-ttu-id="bb640-734">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-734">**Description:**</span></span>  
<span data-ttu-id="bb640-735">hello PadLeft 函式左填補字串 tooa 指定使用提供的填補字元的長度。</span><span class="sxs-lookup"><span data-stu-id="bb640-735">hello PadLeft function left-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="bb640-736">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="bb640-737">字串： hello 字串 toopad。</span><span class="sxs-lookup"><span data-stu-id="bb640-737">string: hello string toopad.</span></span>
* <span data-ttu-id="bb640-738">長度： 整數，代表 hello 預期字串的長度。</span><span class="sxs-lookup"><span data-stu-id="bb640-738">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="bb640-739">padCharacter： 字串，其中包含單一字元 toouse 為 hello 填補字元</span><span class="sxs-lookup"><span data-stu-id="bb640-739">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="bb640-740">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-740">**Remarks:**</span></span>

* <span data-ttu-id="bb640-741">如果字串 hello 長度小於 length，padCharacter 則重複地附加的 toohello 開頭 （左邊） 字串的長度等於 toolength 之前。</span><span class="sxs-lookup"><span data-stu-id="bb640-741">If hello length of string is less than length, then padCharacter is repeatedly appended toohello beginning (left) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="bb640-742">PadCharacter 可以是空白字元，但不能是 Null 值。</span><span class="sxs-lookup"><span data-stu-id="bb640-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="bb640-743">如果字串 hello 長度大於長度等於 tooor，字串會原封不動地傳回。</span><span class="sxs-lookup"><span data-stu-id="bb640-743">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="bb640-744">如果字串的長度大於或等於 toolength，則傳回字串的相同 toostring。</span><span class="sxs-lookup"><span data-stu-id="bb640-744">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="bb640-745">如果字串 hello 長度小於 length，hello 的新字串所需長度會傳回包含以 padCharacter 填補的字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-745">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="bb640-746">如果字串為 null，hello 函式會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-746">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="bb640-747">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="bb640-748">傳回 "000000User"。</span><span class="sxs-lookup"><span data-stu-id="bb640-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="bb640-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="bb640-749">PadRight</span></span>
<span data-ttu-id="bb640-750">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-750">**Description:**</span></span>  
<span data-ttu-id="bb640-751">hello PadRight 函數的右填補字串 tooa 指定使用提供的填補字元的長度。</span><span class="sxs-lookup"><span data-stu-id="bb640-751">hello PadRight function right-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="bb640-752">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="bb640-753">字串： hello 字串 toopad。</span><span class="sxs-lookup"><span data-stu-id="bb640-753">string: hello string toopad.</span></span>
* <span data-ttu-id="bb640-754">長度： 整數，代表 hello 預期字串的長度。</span><span class="sxs-lookup"><span data-stu-id="bb640-754">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="bb640-755">padCharacter： 字串，其中包含單一字元 toouse 為 hello 填補字元</span><span class="sxs-lookup"><span data-stu-id="bb640-755">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="bb640-756">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-756">**Remarks:**</span></span>

* <span data-ttu-id="bb640-757">如果 hello 字串的長度小於 length，則 padCharacter 是字串的重複地附加的 toohello 尾端 （右邊） 直到長度等於 toolength。</span><span class="sxs-lookup"><span data-stu-id="bb640-757">If hello length of string is less than length, then padCharacter is repeatedly appended toohello end (right) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="bb640-758">PadCharacter 可以是空白字元，但不能是 Null 值。</span><span class="sxs-lookup"><span data-stu-id="bb640-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="bb640-759">如果字串 hello 長度大於長度等於 tooor，字串會原封不動地傳回。</span><span class="sxs-lookup"><span data-stu-id="bb640-759">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="bb640-760">如果字串的長度大於或等於 toolength，則傳回字串的相同 toostring。</span><span class="sxs-lookup"><span data-stu-id="bb640-760">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="bb640-761">如果字串 hello 長度小於 length，hello 的新字串所需長度會傳回包含以 padCharacter 填補的字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-761">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="bb640-762">如果字串為 null，hello 函式會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-762">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="bb640-763">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="bb640-764">傳回 "User000000"。</span><span class="sxs-lookup"><span data-stu-id="bb640-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="bb640-765">PCase</span><span class="sxs-lookup"><span data-stu-id="bb640-765">PCase</span></span>
<span data-ttu-id="bb640-766">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-766">**Description:**</span></span>  
<span data-ttu-id="bb640-767">hello PCase 函數將轉換 hello 第一個字元在字串 tooupper 的情況下，每個空格分隔字組和其他所有字元都轉換 toolower 案例。</span><span class="sxs-lookup"><span data-stu-id="bb640-767">hello PCase function converts hello first character of each space delimited word in a string tooupper case, and all other characters are converted toolower case.</span></span>

<span data-ttu-id="bb640-768">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="bb640-769">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-769">**Remarks:**</span></span>

* <span data-ttu-id="bb640-770">此函式目前未提供適當的大小寫 tooconvert 全部大寫，例如為縮寫字的單字。</span><span class="sxs-lookup"><span data-stu-id="bb640-770">This function does not currently provide proper casing tooconvert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="bb640-771">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="bb640-772">傳回 "test"。</span><span class="sxs-lookup"><span data-stu-id="bb640-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="bb640-773">傳回 "Test"</span><span class="sxs-lookup"><span data-stu-id="bb640-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="bb640-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="bb640-774">RandomNum</span></span>
<span data-ttu-id="bb640-775">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-775">**Description:**</span></span>  
<span data-ttu-id="bb640-776">hello RandomNum 函數會傳回一個隨機數字之間指定的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="bb640-776">hello RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="bb640-777">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="bb640-778">開始： 數字識別 hello 下限 hello 隨機值 toogenerate</span><span class="sxs-lookup"><span data-stu-id="bb640-778">start: a number identifying hello lower limit of hello random value toogenerate</span></span>
* <span data-ttu-id="bb640-779">結束： 數字識別 hello 上限 hello 隨機值 toogenerate</span><span class="sxs-lookup"><span data-stu-id="bb640-779">end: a number identifying hello upper limit of hello random value toogenerate</span></span>

<span data-ttu-id="bb640-780">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="bb640-781">可傳回 734。</span><span class="sxs-lookup"><span data-stu-id="bb640-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="bb640-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="bb640-782">RemoveDuplicates</span></span>
<span data-ttu-id="bb640-783">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-783">**Description:**</span></span>  
<span data-ttu-id="bb640-784">hello RemoveDuplicates 函數接受多重值的字串，並確定每個值是唯一的。</span><span class="sxs-lookup"><span data-stu-id="bb640-784">hello RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="bb640-785">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="bb640-786">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="bb640-787">傳回處理過的 proxyAddress 屬性，其中已移除所有重複的值。</span><span class="sxs-lookup"><span data-stu-id="bb640-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="bb640-788">Replace</span><span class="sxs-lookup"><span data-stu-id="bb640-788">Replace</span></span>
<span data-ttu-id="bb640-789">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-789">**Description:**</span></span>  
<span data-ttu-id="bb640-790">hello Replace 函數會取代所有出現的字串 tooanother 字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-790">hello Replace function replaces all occurrences of a string tooanother string.</span></span>

<span data-ttu-id="bb640-791">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="bb640-792">字串： 字串 tooreplace 中的值。</span><span class="sxs-lookup"><span data-stu-id="bb640-792">string: A string tooreplace values in.</span></span>
* <span data-ttu-id="bb640-793">OldValue: hello 字串 toosearch 如和 tooreplace。</span><span class="sxs-lookup"><span data-stu-id="bb640-793">OldValue: hello string toosearch for and tooreplace.</span></span>
* <span data-ttu-id="bb640-794">若要 NewValue: hello 字串 tooreplace。</span><span class="sxs-lookup"><span data-stu-id="bb640-794">NewValue: hello string tooreplace to.</span></span>

<span data-ttu-id="bb640-795">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-795">**Remarks:**</span></span>  
<span data-ttu-id="bb640-796">hello 函式會辨識下列特殊符號的 hello:</span><span class="sxs-lookup"><span data-stu-id="bb640-796">hello function recognizes hello following special monikers:</span></span>

* <span data-ttu-id="bb640-797">\n – 新行</span><span class="sxs-lookup"><span data-stu-id="bb640-797">\n – New Line</span></span>
* <span data-ttu-id="bb640-798">\r – 歸位字元</span><span class="sxs-lookup"><span data-stu-id="bb640-798">\r – Carriage Return</span></span>
* <span data-ttu-id="bb640-799">\t – 定位字元</span><span class="sxs-lookup"><span data-stu-id="bb640-799">\t – Tab</span></span>

<span data-ttu-id="bb640-800">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="bb640-801">CRLF 取代為逗號和空格，而且可能會太導致"其中一個 Microsoft 的方式，Redmond，WA，USA"</span><span class="sxs-lookup"><span data-stu-id="bb640-801">Replaces CRLF with a comma and space, and could lead too"One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="bb640-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="bb640-802">ReplaceChars</span></span>
<span data-ttu-id="bb640-803">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-803">**Description:**</span></span>  
<span data-ttu-id="bb640-804">hello ReplaceChars 函數取代字元在 hello ReplacePattern 字串中找到的所有項的目。</span><span class="sxs-lookup"><span data-stu-id="bb640-804">hello ReplaceChars function replaces all occurrences of characters found in hello ReplacePattern string.</span></span>

<span data-ttu-id="bb640-805">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="bb640-806">字串： 字串 tooreplace 中的字元。</span><span class="sxs-lookup"><span data-stu-id="bb640-806">string: A string tooreplace characters in.</span></span>
* <span data-ttu-id="bb640-807">ReplacePattern： 字串，包含字元 tooreplace 的字典。</span><span class="sxs-lookup"><span data-stu-id="bb640-807">ReplacePattern: a string containing a dictionary with characters tooreplace.</span></span>

<span data-ttu-id="bb640-808">hello 格式為 {source1}: {target1}，{source2}: {target2}，{sourceN}，{targetN} 來源的 hello 字元 toofind 和目標 hello 字串 tooreplace 與位置。</span><span class="sxs-lookup"><span data-stu-id="bb640-808">hello format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is hello character toofind and target hello string tooreplace with.</span></span>

<span data-ttu-id="bb640-809">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-809">**Remarks:**</span></span>

* <span data-ttu-id="bb640-810">hello 函數接受每個項目定義的來源，並將它們取代為 hello 目標。</span><span class="sxs-lookup"><span data-stu-id="bb640-810">hello function takes each occurrence of defined sources and replaces them with hello targets.</span></span>
* <span data-ttu-id="bb640-811">hello 來源必須剛好只有一個 (unicode) 字元。</span><span class="sxs-lookup"><span data-stu-id="bb640-811">hello source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="bb640-812">hello 來源不可為空白或長度超過一個字元 （剖析錯誤）。</span><span class="sxs-lookup"><span data-stu-id="bb640-812">hello source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="bb640-813">hello 目標可以有多個字元，例如.ö： oe、 β： ss。</span><span class="sxs-lookup"><span data-stu-id="bb640-813">hello target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="bb640-814">hello 目標可以是空白，表示應移除用 hello 字元。</span><span class="sxs-lookup"><span data-stu-id="bb640-814">hello target can be empty indicating that hello character should be removed.</span></span>
* <span data-ttu-id="bb640-815">hello 來源會區分大小寫，而且必須完全相符。</span><span class="sxs-lookup"><span data-stu-id="bb640-815">hello source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="bb640-816">hello，（逗號） 和: （冒號） 是保留的字元，無法使用這個函式取代。</span><span class="sxs-lookup"><span data-stu-id="bb640-816">hello , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="bb640-817">空間和 hello ReplacePattern 字串中的其他空白字元都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="bb640-817">Spaces and other white characters in hello ReplacePattern string are ignored.</span></span>

<span data-ttu-id="bb640-818">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="bb640-819">傳回 Raksmorgas</span><span class="sxs-lookup"><span data-stu-id="bb640-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="bb640-820">移除定義的 toobe 是傳回"ONeil"，hello 單一刻度。</span><span class="sxs-lookup"><span data-stu-id="bb640-820">Returns "ONeil", hello single tick is defined toobe removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="bb640-821">Right</span><span class="sxs-lookup"><span data-stu-id="bb640-821">Right</span></span>
<span data-ttu-id="bb640-822">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-822">**Description:**</span></span>  
<span data-ttu-id="bb640-823">hello Right 函數會傳回指定的字元數從 hello 正確 （結尾） 的字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-823">hello Right function returns a specified number of characters from hello right (end) of a string.</span></span>

<span data-ttu-id="bb640-824">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="bb640-825">字串： hello tooreturn 字元字串</span><span class="sxs-lookup"><span data-stu-id="bb640-825">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="bb640-826">NumChars： 數字，識別 hello 從 hello 尾端 （右邊） 字串的字元 tooreturn 數目</span><span class="sxs-lookup"><span data-stu-id="bb640-826">NumChars: a number identifying hello number of characters tooreturn from hello end (right) of string</span></span>

<span data-ttu-id="bb640-827">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-827">**Remarks:**</span></span>  
<span data-ttu-id="bb640-828">從字串 hello 最後位置傳回 NumChars 個字元。</span><span class="sxs-lookup"><span data-stu-id="bb640-828">NumChars characters are returned from hello last position of string.</span></span>

<span data-ttu-id="bb640-829">字串，包含 hello 最後 numChars 個字元字串中：</span><span class="sxs-lookup"><span data-stu-id="bb640-829">A string containing hello last numChars characters in string:</span></span>

* <span data-ttu-id="bb640-830">如果 numChars = 0，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="bb640-831">如果 numChars < 0，會傳回輸入字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="bb640-832">如果 string 為 Null，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-832">If string is null, return empty string.</span></span>

<span data-ttu-id="bb640-833">如果字串包含較少的字元，超過 hello NumChars 中指定數字，則會傳回字串的相同 toostring。</span><span class="sxs-lookup"><span data-stu-id="bb640-833">If string contains fewer characters than hello number specified in NumChars, a string identical toostring is returned.</span></span>

<span data-ttu-id="bb640-834">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="bb640-835">傳回 "Doe"。</span><span class="sxs-lookup"><span data-stu-id="bb640-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="bb640-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="bb640-836">RTrim</span></span>
<span data-ttu-id="bb640-837">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-837">**Description:**</span></span>  
<span data-ttu-id="bb640-838">hello RTrim 函數從字串中移除尾端空白。</span><span class="sxs-lookup"><span data-stu-id="bb640-838">hello RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="bb640-839">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="bb640-840">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="bb640-841">傳回 "Test"。</span><span class="sxs-lookup"><span data-stu-id="bb640-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="bb640-842">選取</span><span class="sxs-lookup"><span data-stu-id="bb640-842">Select</span></span>
<span data-ttu-id="bb640-843">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-843">**Description:**</span></span>  
<span data-ttu-id="bb640-844">在以指定函式為基礎的多重值屬性 (或運算式的輸出) 中處理所有值。</span><span class="sxs-lookup"><span data-stu-id="bb640-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="bb640-845">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="bb640-846">項目： 表示 hello 多重值屬性中的項目</span><span class="sxs-lookup"><span data-stu-id="bb640-846">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="bb640-847">屬性： hello 多重值的屬性</span><span class="sxs-lookup"><span data-stu-id="bb640-847">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="bb640-848">expression：傳回值集合的運算式</span><span class="sxs-lookup"><span data-stu-id="bb640-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="bb640-849">條件： 可以處理 hello 屬性中的項目任何函式</span><span class="sxs-lookup"><span data-stu-id="bb640-849">condition: any function that can process an item in hello attribute</span></span>

<span data-ttu-id="bb640-850">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="bb640-851">傳回所有 hello 值 hello 多重值的屬性 otherPhone 後已移除連字號 （-）。</span><span class="sxs-lookup"><span data-stu-id="bb640-851">Return all hello values in hello multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="bb640-852">Split</span><span class="sxs-lookup"><span data-stu-id="bb640-852">Split</span></span>
<span data-ttu-id="bb640-853">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-853">**Description:**</span></span>  
<span data-ttu-id="bb640-854">hello Split 函數接受以分隔符號分隔的字串，並使它多重值的字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-854">hello Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="bb640-855">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="bb640-856">值： hello 與分隔符號字元 tooseparate 的字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-856">value: hello string with a delimiter character tooseparate.</span></span>
* <span data-ttu-id="bb640-857">分隔符號： 單一字元 toobe 做為 hello 分隔符號。</span><span class="sxs-lookup"><span data-stu-id="bb640-857">delimiter: single character toobe used as hello delimiter.</span></span>
* <span data-ttu-id="bb640-858">limit：可以傳回的值數目上限。</span><span class="sxs-lookup"><span data-stu-id="bb640-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="bb640-859">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="bb640-860">傳回具有 2 個元素的多重值的字串 hello proxyAddress 屬性很有用。</span><span class="sxs-lookup"><span data-stu-id="bb640-860">Returns a multi-valued string with 2 elements useful for hello proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="bb640-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="bb640-861">StringFromGuid</span></span>
<span data-ttu-id="bb640-862">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-862">**Description:**</span></span>  
<span data-ttu-id="bb640-863">hello StringFromGuid 函數接受二進位 GUID 並將它轉換 tooa 字串</span><span class="sxs-lookup"><span data-stu-id="bb640-863">hello StringFromGuid function takes a binary GUID and converts it tooa string</span></span>

<span data-ttu-id="bb640-864">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="bb640-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="bb640-865">StringFromSid</span></span>
<span data-ttu-id="bb640-866">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-866">**Description:**</span></span>  
<span data-ttu-id="bb640-867">hello StringFromSid 函數將轉換位元組陣列，包含安全性識別元 tooa 字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-867">hello StringFromSid function converts a byte array containing a security identifier tooa string.</span></span>

<span data-ttu-id="bb640-868">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="bb640-869">Switch</span><span class="sxs-lookup"><span data-stu-id="bb640-869">Switch</span></span>
<span data-ttu-id="bb640-870">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-870">**Description:**</span></span>  
<span data-ttu-id="bb640-871">hello Switch 函式是使用的 tooreturn 評估的條件所根據的單一值。</span><span class="sxs-lookup"><span data-stu-id="bb640-871">hello Switch function is used tooreturn a single value based on evaluated conditions.</span></span>

<span data-ttu-id="bb640-872">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="bb640-873">expr： 您想 tooevaluate 的 Variant 運算式。</span><span class="sxs-lookup"><span data-stu-id="bb640-873">expr: Variant expression you want tooevaluate.</span></span>
* <span data-ttu-id="bb640-874">值： 值 toobe 傳回 hello 對應的運算式為 True 時。</span><span class="sxs-lookup"><span data-stu-id="bb640-874">value: Value toobe returned if hello corresponding expression is True.</span></span>

<span data-ttu-id="bb640-875">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-875">**Remarks:**</span></span>  
<span data-ttu-id="bb640-876">hello 交換器函式引數清單所組成的運算式和值組。</span><span class="sxs-lookup"><span data-stu-id="bb640-876">hello Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="bb640-877">hello 運算式都會從左 tooright，評估並傳回第一個運算式 tooevaluate tooTrue hello 與相關聯的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="bb640-877">hello expressions are evaluated from left tooright, and hello value associated with hello first expression tooevaluate tooTrue is returned.</span></span> <span data-ttu-id="bb640-878">如果 hello 組件的配對不正確，就會發生執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="bb640-878">If hello parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="bb640-879">例如，如果 expr1 為 True，Switch 就會傳回 value1。</span><span class="sxs-lookup"><span data-stu-id="bb640-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="bb640-880">如果 expr-1 為 False，但 expr-2 為 True，Switch 就會傳回 value-2，依此類推。</span><span class="sxs-lookup"><span data-stu-id="bb640-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="bb640-881">在下列情況下，參數會傳回 Nothing︰</span><span class="sxs-lookup"><span data-stu-id="bb640-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="bb640-882">Hello 運算式都為 True。</span><span class="sxs-lookup"><span data-stu-id="bb640-882">None of hello expressions are True.</span></span>
* <span data-ttu-id="bb640-883">hello 的第一個 True 運算式具有對應值是 Null。</span><span class="sxs-lookup"><span data-stu-id="bb640-883">hello first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="bb640-884">雖然 Switch 只會傳回其中一個運算式，但它會評估所有運算式。</span><span class="sxs-lookup"><span data-stu-id="bb640-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="bb640-885">基於這個理由，您應該留意非預期的副作用。</span><span class="sxs-lookup"><span data-stu-id="bb640-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="bb640-886">例如，如果 hello 任何運算式的評估導致除以零的錯誤，就會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="bb640-886">For example, if hello evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="bb640-887">值，也可以是 hello 誤差函數會傳回自訂字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-887">Value can also be hello Error function, which would return a custom string.</span></span>

<span data-ttu-id="bb640-888">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="bb640-889">傳回一些主要城市採用說出 hello 語言，否則會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="bb640-889">Returns hello language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="bb640-890">Trim</span><span class="sxs-lookup"><span data-stu-id="bb640-890">Trim</span></span>
<span data-ttu-id="bb640-891">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-891">**Description:**</span></span>  
<span data-ttu-id="bb640-892">hello Trim 函數移除開頭和尾端空白字元的字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-892">hello Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="bb640-893">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="bb640-894">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="bb640-895">傳回 "test"。</span><span class="sxs-lookup"><span data-stu-id="bb640-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="bb640-896">移除開頭和尾端空白 hello proxyAddress 屬性中每個值。</span><span class="sxs-lookup"><span data-stu-id="bb640-896">Removes leading and trailing spaces for each value in hello proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="bb640-897">UCase</span><span class="sxs-lookup"><span data-stu-id="bb640-897">UCase</span></span>
<span data-ttu-id="bb640-898">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-898">**Description:**</span></span>  
<span data-ttu-id="bb640-899">hello UCase 函數將字串 tooupper 案例中的所有字元都轉換。</span><span class="sxs-lookup"><span data-stu-id="bb640-899">hello UCase function converts all characters in a string tooupper case.</span></span>

<span data-ttu-id="bb640-900">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="bb640-901">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="bb640-902">傳回 "test"。</span><span class="sxs-lookup"><span data-stu-id="bb640-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="bb640-903">Where</span><span class="sxs-lookup"><span data-stu-id="bb640-903">Where</span></span>

<span data-ttu-id="bb640-904">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-904">**Description:**</span></span>  
<span data-ttu-id="bb640-905">傳回以指定條件為基礎的多重值屬性 (或運算式的輸出) 的值子集。</span><span class="sxs-lookup"><span data-stu-id="bb640-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="bb640-906">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="bb640-907">項目： 表示 hello 多重值屬性中的項目</span><span class="sxs-lookup"><span data-stu-id="bb640-907">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="bb640-908">屬性： hello 多重值的屬性</span><span class="sxs-lookup"><span data-stu-id="bb640-908">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="bb640-909">條件： 可以是任何運算式評估 tootrue 或 false</span><span class="sxs-lookup"><span data-stu-id="bb640-909">condition: any expression that can be evaluated tootrue or false</span></span>
* <span data-ttu-id="bb640-910">expression：傳回值集合的運算式</span><span class="sxs-lookup"><span data-stu-id="bb640-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="bb640-911">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="bb640-912">傳回不過期的 hello 多重值的屬性 userCertificate hello 憑證的值。</span><span class="sxs-lookup"><span data-stu-id="bb640-912">Return hello certificate values in hello multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="bb640-913">With</span><span class="sxs-lookup"><span data-stu-id="bb640-913">With</span></span>
<span data-ttu-id="bb640-914">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-914">**Description:**</span></span>  
<span data-ttu-id="bb640-915">hello 函式與使用變數 toorepresent 子運算式會出現一次或多次 hello 複雜運算式中，提供方式 toosimplify 複雜的運算式。</span><span class="sxs-lookup"><span data-stu-id="bb640-915">hello With function provides a way toosimplify a complex expression by using a variable toorepresent a subexpression which appears one or more times in hello complex expression.</span></span>

<span data-ttu-id="bb640-916">**語法：**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="bb640-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="bb640-917">變數： 代表 hello 子運算式。</span><span class="sxs-lookup"><span data-stu-id="bb640-917">variable: Represents hello subexpression.</span></span>
* <span data-ttu-id="bb640-918">subExpression：變數代表的子運算式。</span><span class="sxs-lookup"><span data-stu-id="bb640-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="bb640-919">complexExpression：複雜的運算式。</span><span class="sxs-lookup"><span data-stu-id="bb640-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="bb640-920">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="bb640-921">在功能上等同於：</span><span class="sxs-lookup"><span data-stu-id="bb640-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="bb640-922">Hello userCertificate 屬性中傳回的只是未到期的憑證值。</span><span class="sxs-lookup"><span data-stu-id="bb640-922">Which returns only unexpired certificate values in hello userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="bb640-923">Word</span><span class="sxs-lookup"><span data-stu-id="bb640-923">Word</span></span>
<span data-ttu-id="bb640-924">**說明：**</span><span class="sxs-lookup"><span data-stu-id="bb640-924">**Description:**</span></span>  
<span data-ttu-id="bb640-925">hello Word 函式會傳回包含在字串中，根據參數所描述 hello 分隔符號 toouse 和 hello 文字數字 tooreturn 的單字。</span><span class="sxs-lookup"><span data-stu-id="bb640-925">hello Word function returns a word contained within a string, based on parameters describing hello delimiters toouse and hello word number tooreturn.</span></span>

<span data-ttu-id="bb640-926">**語法：**</span><span class="sxs-lookup"><span data-stu-id="bb640-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="bb640-927">字串： hello 字串 tooreturn 特定詞彙。</span><span class="sxs-lookup"><span data-stu-id="bb640-927">string: hello string tooreturn a word from.</span></span>
* <span data-ttu-id="bb640-928">WordNumber：一個數字，用於識別可傳回的字數。</span><span class="sxs-lookup"><span data-stu-id="bb640-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="bb640-929">分隔符號： 字串，表示應該使用的 tooidentify 單字的 hello 分隔符號</span><span class="sxs-lookup"><span data-stu-id="bb640-929">delimiters: a string representing hello delimiter(s) that should be used tooidentify words</span></span>

<span data-ttu-id="bb640-930">**備註：**</span><span class="sxs-lookup"><span data-stu-id="bb640-930">**Remarks:**</span></span>  
<span data-ttu-id="bb640-931">每個字串 hello hello 字元在分隔符號所分隔的字串中的字元就識別為單字：</span><span class="sxs-lookup"><span data-stu-id="bb640-931">Each string of characters in string separated by hello one of hello characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="bb640-932">如果 number < 1，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="bb640-933">如果 string 為 Null，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="bb640-934">如果 string 所含的字數少於 number 個字，或者 string 不包含任何 delimeters 所識別的單字，就會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="bb640-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="bb640-935">**範例：**</span><span class="sxs-lookup"><span data-stu-id="bb640-935">**Example:**</span></span>  
`Word("hello quick brown fox",3," ")`  
<span data-ttu-id="bb640-936">傳回 "brown"</span><span class="sxs-lookup"><span data-stu-id="bb640-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="bb640-937">會傳回 "has"</span><span class="sxs-lookup"><span data-stu-id="bb640-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb640-938">其他資源</span><span class="sxs-lookup"><span data-stu-id="bb640-938">Additional Resources</span></span>
* [<span data-ttu-id="bb640-939">了解宣告式佈建運算式</span><span class="sxs-lookup"><span data-stu-id="bb640-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="bb640-940">Azure AD Connect 同步處理：自訂同步處理選項</span><span class="sxs-lookup"><span data-stu-id="bb640-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="bb640-941">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb640-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

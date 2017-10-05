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
ms.openlocfilehash: 926f52ef64eb79205dbfb344edc7d9bece2a6947
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="deb6c-103">Azure AD Connect 同步處理：函式參考</span><span class="sxs-lookup"><span data-stu-id="deb6c-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="deb6c-104">在 Azure AD Connect 中，函數是用來在同步處理期間操作屬性值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-104">In Azure AD Connect, functions are used to manipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="deb6c-105">函式的語法可使用下列格式來表示：</span><span class="sxs-lookup"><span data-stu-id="deb6c-105">The Syntax of the functions is expressed using the following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="deb6c-106">如果函式是多載的且接受多種語法，即會列出所有的有效語法。</span><span class="sxs-lookup"><span data-stu-id="deb6c-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="deb6c-107">函式是強型別的，且會確認傳入的類型與記載的類型相符。</span><span class="sxs-lookup"><span data-stu-id="deb6c-107">The functions are strongly typed and they verify that the type passed in matches the documented type.</span></span>  
<span data-ttu-id="deb6c-108">如果類型不符，即會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="deb6c-108">If the type does not match, an error is thrown.</span></span>

<span data-ttu-id="deb6c-109">類型可以使用下列語法來表示：</span><span class="sxs-lookup"><span data-stu-id="deb6c-109">The types are expressed with the following syntax:</span></span>

* <span data-ttu-id="deb6c-110"> – 二進位</span><span class="sxs-lookup"><span data-stu-id="deb6c-110">**bin** – Binary</span></span>
* <span data-ttu-id="deb6c-111"> – 布林值</span><span class="sxs-lookup"><span data-stu-id="deb6c-111">**bool** – Boolean</span></span>
* <span data-ttu-id="deb6c-112"> – UTC 日期/時間</span><span class="sxs-lookup"><span data-stu-id="deb6c-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="deb6c-113"> – 已知常數的列舉</span><span class="sxs-lookup"><span data-stu-id="deb6c-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="deb6c-114"> – Expression, which is ected to evaluate to a Boolean</span><span class="sxs-lookup"><span data-stu-id="deb6c-114">**exp** – Expression, which is expected to evaluate to a Boolean</span></span>
* <span data-ttu-id="deb6c-115">**mvbin** – 多重值的二進位</span><span class="sxs-lookup"><span data-stu-id="deb6c-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="deb6c-116">**mvstr** – 多重值的字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="deb6c-117">**mvref** – 多重值的參考</span><span class="sxs-lookup"><span data-stu-id="deb6c-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="deb6c-118">**num** – 數值</span><span class="sxs-lookup"><span data-stu-id="deb6c-118">**num** – Numeric</span></span>
* <span data-ttu-id="deb6c-119">**ref** – 參考</span><span class="sxs-lookup"><span data-stu-id="deb6c-119">**ref** – Reference</span></span>
* <span data-ttu-id="deb6c-120">**str** – 字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-120">**str** – String</span></span>
* <span data-ttu-id="deb6c-121">**var** – (幾乎) 任何其他類型的變體</span><span class="sxs-lookup"><span data-stu-id="deb6c-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="deb6c-122">**void** – 不會傳回值</span><span class="sxs-lookup"><span data-stu-id="deb6c-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="deb6c-123">類型為 **mvbin**、**mvstr** 和 **mvref** 的函式僅可用於多重值的屬性。</span><span class="sxs-lookup"><span data-stu-id="deb6c-123">The functions with the types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="deb6c-124">類型為 **bin**、**str** 和 **ref** 的函式可用於單一值和多重值的屬性。</span><span class="sxs-lookup"><span data-stu-id="deb6c-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="deb6c-125">函式參考</span><span class="sxs-lookup"><span data-stu-id="deb6c-125">Functions Reference</span></span>
| <span data-ttu-id="deb6c-126">函數的清單</span><span class="sxs-lookup"><span data-stu-id="deb6c-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="deb6c-127">**憑證**</span><span class="sxs-lookup"><span data-stu-id="deb6c-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="deb6c-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="deb6c-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="deb6c-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="deb6c-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="deb6c-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="deb6c-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="deb6c-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="deb6c-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="deb6c-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="deb6c-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="deb6c-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="deb6c-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="deb6c-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="deb6c-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="deb6c-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="deb6c-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="deb6c-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="deb6c-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="deb6c-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="deb6c-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="deb6c-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="deb6c-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="deb6c-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="deb6c-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="deb6c-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="deb6c-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="deb6c-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="deb6c-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="deb6c-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="deb6c-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="deb6c-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="deb6c-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="deb6c-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="deb6c-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="deb6c-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="deb6c-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="deb6c-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="deb6c-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="deb6c-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="deb6c-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="deb6c-148"> CertVersion</span><span class="sxs-lookup"><span data-stu-id="deb6c-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="deb6c-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="deb6c-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="deb6c-150">**轉換**</span><span class="sxs-lookup"><span data-stu-id="deb6c-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="deb6c-151">CBool</span><span class="sxs-lookup"><span data-stu-id="deb6c-151">CBool</span></span>](#cbool) |[<span data-ttu-id="deb6c-152">CDate</span><span class="sxs-lookup"><span data-stu-id="deb6c-152">CDate</span></span>](#cdate) |[<span data-ttu-id="deb6c-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="deb6c-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="deb6c-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="deb6c-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="deb6c-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="deb6c-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="deb6c-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="deb6c-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="deb6c-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="deb6c-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="deb6c-158">CNum</span><span class="sxs-lookup"><span data-stu-id="deb6c-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="deb6c-159">CRef</span><span class="sxs-lookup"><span data-stu-id="deb6c-159">CRef</span></span>](#cref) |[<span data-ttu-id="deb6c-160">CStr</span><span class="sxs-lookup"><span data-stu-id="deb6c-160">CStr</span></span>](#cstr) |[<span data-ttu-id="deb6c-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="deb6c-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="deb6c-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="deb6c-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="deb6c-163">**日期 / 時間**</span><span class="sxs-lookup"><span data-stu-id="deb6c-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="deb6c-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="deb6c-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="deb6c-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="deb6c-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="deb6c-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="deb6c-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="deb6c-167">Now</span><span class="sxs-lookup"><span data-stu-id="deb6c-167">Now</span></span>](#now) | |
| [<span data-ttu-id="deb6c-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="deb6c-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="deb6c-169">**目錄**</span><span class="sxs-lookup"><span data-stu-id="deb6c-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="deb6c-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="deb6c-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="deb6c-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="deb6c-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="deb6c-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="deb6c-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="deb6c-173">**評估**</span><span class="sxs-lookup"><span data-stu-id="deb6c-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="deb6c-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="deb6c-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="deb6c-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="deb6c-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="deb6c-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="deb6c-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="deb6c-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="deb6c-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="deb6c-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="deb6c-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="deb6c-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="deb6c-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="deb6c-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="deb6c-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="deb6c-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="deb6c-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="deb6c-182">IsString</span><span class="sxs-lookup"><span data-stu-id="deb6c-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="deb6c-183">**數學運算**</span><span class="sxs-lookup"><span data-stu-id="deb6c-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="deb6c-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="deb6c-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="deb6c-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="deb6c-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="deb6c-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="deb6c-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="deb6c-187">**多重值**</span><span class="sxs-lookup"><span data-stu-id="deb6c-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="deb6c-188">Contains</span><span class="sxs-lookup"><span data-stu-id="deb6c-188">Contains</span></span>](#contains) |[<span data-ttu-id="deb6c-189">Count</span><span class="sxs-lookup"><span data-stu-id="deb6c-189">Count</span></span>](#count) |[<span data-ttu-id="deb6c-190">Item</span><span class="sxs-lookup"><span data-stu-id="deb6c-190">Item</span></span>](#item) |[<span data-ttu-id="deb6c-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="deb6c-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="deb6c-192">Join</span><span class="sxs-lookup"><span data-stu-id="deb6c-192">Join</span></span>](#join) |[<span data-ttu-id="deb6c-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="deb6c-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="deb6c-194">Split</span><span class="sxs-lookup"><span data-stu-id="deb6c-194">Split</span></span>](#split) | | |
| <span data-ttu-id="deb6c-195">**程式流程**</span><span class="sxs-lookup"><span data-stu-id="deb6c-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="deb6c-196">Error</span><span class="sxs-lookup"><span data-stu-id="deb6c-196">Error</span></span>](#error) |[<span data-ttu-id="deb6c-197">IIF</span><span class="sxs-lookup"><span data-stu-id="deb6c-197">IIF</span></span>](#iif) |[<span data-ttu-id="deb6c-198">選取</span><span class="sxs-lookup"><span data-stu-id="deb6c-198">Select</span></span>](#select) |[<span data-ttu-id="deb6c-199">Switch</span><span class="sxs-lookup"><span data-stu-id="deb6c-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="deb6c-200">其中</span><span class="sxs-lookup"><span data-stu-id="deb6c-200">Where</span></span>](#where) |[<span data-ttu-id="deb6c-201">With</span><span class="sxs-lookup"><span data-stu-id="deb6c-201">With</span></span>](#with) | | | |
| <span data-ttu-id="deb6c-202">**文字**</span><span class="sxs-lookup"><span data-stu-id="deb6c-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="deb6c-203">GUID</span><span class="sxs-lookup"><span data-stu-id="deb6c-203">GUID</span></span>](#guid) |[<span data-ttu-id="deb6c-204">InStr</span><span class="sxs-lookup"><span data-stu-id="deb6c-204">InStr</span></span>](#instr) |[<span data-ttu-id="deb6c-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="deb6c-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="deb6c-206">LCase</span><span class="sxs-lookup"><span data-stu-id="deb6c-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="deb6c-207">Left</span><span class="sxs-lookup"><span data-stu-id="deb6c-207">Left</span></span>](#left) |[<span data-ttu-id="deb6c-208">Len</span><span class="sxs-lookup"><span data-stu-id="deb6c-208">Len</span></span>](#len) |[<span data-ttu-id="deb6c-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="deb6c-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="deb6c-210">Mid</span><span class="sxs-lookup"><span data-stu-id="deb6c-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="deb6c-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="deb6c-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="deb6c-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="deb6c-212">PadRight</span></span>](#padright) |[<span data-ttu-id="deb6c-213">PCase</span><span class="sxs-lookup"><span data-stu-id="deb6c-213">PCase</span></span>](#pcase) |[<span data-ttu-id="deb6c-214">Replace</span><span class="sxs-lookup"><span data-stu-id="deb6c-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="deb6c-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="deb6c-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="deb6c-216">Right</span><span class="sxs-lookup"><span data-stu-id="deb6c-216">Right</span></span>](#right) |[<span data-ttu-id="deb6c-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="deb6c-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="deb6c-218">Trim</span><span class="sxs-lookup"><span data-stu-id="deb6c-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="deb6c-219">UCase</span><span class="sxs-lookup"><span data-stu-id="deb6c-219">UCase</span></span>](#ucase) |[<span data-ttu-id="deb6c-220">Word</span><span class="sxs-lookup"><span data-stu-id="deb6c-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="deb6c-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="deb6c-221">BitAnd</span></span>
<span data-ttu-id="deb6c-222">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-222">**Description:**</span></span>  
<span data-ttu-id="deb6c-223">BitAnd 函式會在值中設定指定的位元。</span><span class="sxs-lookup"><span data-stu-id="deb6c-223">The BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="deb6c-224">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="deb6c-225">value1，value2：應該使用 AND 連結在一起的數值</span><span class="sxs-lookup"><span data-stu-id="deb6c-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="deb6c-226">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-226">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-227">此函式會將這兩個參數轉換為二進位表示法，並將某一個位元設為：</span><span class="sxs-lookup"><span data-stu-id="deb6c-227">This function converts both parameters to the binary representation and sets a bit to:</span></span>

* <span data-ttu-id="deb6c-228">0 - 如果 *mask* 和 *flag* 中有一個對應位元或這兩者為 0</span><span class="sxs-lookup"><span data-stu-id="deb6c-228">0 - if one or both of the corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="deb6c-229">1 - 如果這兩個對應位元都是 1。</span><span class="sxs-lookup"><span data-stu-id="deb6c-229">1 - if both of the corresponding bits are 1.</span></span>

<span data-ttu-id="deb6c-230">換句話說，除非這兩個參數的對應位元都是 1，否則在所有情況下都會傳回 0。</span><span class="sxs-lookup"><span data-stu-id="deb6c-230">In other words, it returns 0 in all cases except when the corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="deb6c-231">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="deb6c-232">傳回 7，因為十六進位 "F" AND "F7" 會評估為此值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-232">Returns 7 because hexadecimal "F" AND "F7" evaluate to this value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="deb6c-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="deb6c-233">BitOr</span></span>
<span data-ttu-id="deb6c-234">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-234">**Description:**</span></span>  
<span data-ttu-id="deb6c-235">BitOr 函式會在值中設定指定的位元。</span><span class="sxs-lookup"><span data-stu-id="deb6c-235">The BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="deb6c-236">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="deb6c-237">value1，value2：應該使用 OR 連結在一起的數值</span><span class="sxs-lookup"><span data-stu-id="deb6c-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="deb6c-238">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-238">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-239">此函式會將這兩個參數轉換成二進位表示法，而且，如果 mask 和 flag 中有一個的對應位元為 1 或兩者都是，就會將某一個位元設為 1，如果這兩個對應位元都為 0，則會設為 0。</span><span class="sxs-lookup"><span data-stu-id="deb6c-239">This function converts both parameters to the binary representation and sets a bit to 1 if one or both of the corresponding bits in mask and flag are 1, and to 0 if both of the corresponding bits are 0.</span></span> <span data-ttu-id="deb6c-240">換句話說，除非這兩個參數的對應位元都是 0，否則在所有情況下都會傳回 1。</span><span class="sxs-lookup"><span data-stu-id="deb6c-240">In other words, it returns 1 in all cases except where the corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="deb6c-241">CBool</span><span class="sxs-lookup"><span data-stu-id="deb6c-241">CBool</span></span>
<span data-ttu-id="deb6c-242">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-242">**Description:**</span></span>  
<span data-ttu-id="deb6c-243">CBool 函式會根據評估的運算式傳回布林值</span><span class="sxs-lookup"><span data-stu-id="deb6c-243">The CBool function returns a Boolean based on the evaluated expression</span></span>

<span data-ttu-id="deb6c-244">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="deb6c-245">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-245">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-246">如果運算式評估為非零值，CBool 就會傳回 True，否則會傳回 False。</span><span class="sxs-lookup"><span data-stu-id="deb6c-246">If the expression evaluates to a nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="deb6c-247">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="deb6c-248">如果這兩個屬性的值相同，即會傳回 True。</span><span class="sxs-lookup"><span data-stu-id="deb6c-248">Returns True if both attributes have the same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="deb6c-249">CDate</span><span class="sxs-lookup"><span data-stu-id="deb6c-249">CDate</span></span>
<span data-ttu-id="deb6c-250">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-250">**Description:**</span></span>  
<span data-ttu-id="deb6c-251">CDate 函式會傳回字串的 UTC DateTime。</span><span class="sxs-lookup"><span data-stu-id="deb6c-251">The CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="deb6c-252">DateTime 不是同步處理中的原生屬性類型，但有部分函式會用到。</span><span class="sxs-lookup"><span data-stu-id="deb6c-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="deb6c-253">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="deb6c-254">Value：包含日期、時間和選擇性時區的字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="deb6c-255">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-255">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-256">傳回的字串一律以 UTC 來表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-256">The returned string is always in UTC.</span></span>

<span data-ttu-id="deb6c-257">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="deb6c-258">根據員工的開始時間傳回 DateTime</span><span class="sxs-lookup"><span data-stu-id="deb6c-258">Returns a DateTime based on the employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="deb6c-259">傳回代表 "2013-01-11 12:00 AM" 的 DateTime</span><span class="sxs-lookup"><span data-stu-id="deb6c-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="deb6c-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="deb6c-260">CertExtensionOids</span></span>
<span data-ttu-id="deb6c-261">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-261">**Description:**</span></span>  
<span data-ttu-id="deb6c-262">傳回所有憑證物件重要延伸模組的 Oid 值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-262">Returns the Oid values of all the critical extensions of a certificate object.</span></span>

<span data-ttu-id="deb6c-263">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-264">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-265">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-265">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="deb6c-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="deb6c-266">CertFormat</span></span>
<span data-ttu-id="deb6c-267">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-267">**Description:**</span></span>  
<span data-ttu-id="deb6c-268">傳回此 X.509v3 憑證的格式名稱。</span><span class="sxs-lookup"><span data-stu-id="deb6c-268">Returns the name of the format of this X.509v3 certificate.</span></span>

<span data-ttu-id="deb6c-269">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-270">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-271">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-271">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="deb6c-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="deb6c-272">CertFriendlyName</span></span>
<span data-ttu-id="deb6c-273">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-273">**Description:**</span></span>  
<span data-ttu-id="deb6c-274">傳回憑證的相關聯別名。</span><span class="sxs-lookup"><span data-stu-id="deb6c-274">Returns the associated alias for a certificate.</span></span>

<span data-ttu-id="deb6c-275">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-276">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-277">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-277">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="deb6c-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="deb6c-278">CertHashString</span></span>
<span data-ttu-id="deb6c-279">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-279">**Description:**</span></span>  
<span data-ttu-id="deb6c-280">為傳回 X.509v3 憑證的 SHA1 雜湊值作為十六進位字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-280">Returns the SHA1 hash value for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="deb6c-281">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-282">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-283">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-283">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="deb6c-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="deb6c-284">CertIssuer</span></span>
<span data-ttu-id="deb6c-285">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-285">**Description:**</span></span>  
<span data-ttu-id="deb6c-286">傳回發出 X.509v3 憑證的憑證授權單位名稱。</span><span class="sxs-lookup"><span data-stu-id="deb6c-286">Returns the name of the certificate authority that issued the X.509v3 certificate.</span></span>

<span data-ttu-id="deb6c-287">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-288">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-289">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-289">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="deb6c-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="deb6c-290">CertIssuerDN</span></span>
<span data-ttu-id="deb6c-291">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-291">**Description:**</span></span>  
<span data-ttu-id="deb6c-292">傳回憑證簽發者的辨別名稱。</span><span class="sxs-lookup"><span data-stu-id="deb6c-292">Returns the distinguished name of the certificate issuer.</span></span>

<span data-ttu-id="deb6c-293">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-294">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-295">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-295">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="deb6c-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="deb6c-296">CertIssuerOid</span></span>
<span data-ttu-id="deb6c-297">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-297">**Description:**</span></span>  
<span data-ttu-id="deb6c-298">傳回憑證簽發者的 Oid。</span><span class="sxs-lookup"><span data-stu-id="deb6c-298">Returns the Oid of the certificate issuer.</span></span>

<span data-ttu-id="deb6c-299">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-300">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-301">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-301">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="deb6c-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="deb6c-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="deb6c-303">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-303">**Description:**</span></span>  
<span data-ttu-id="deb6c-304">傳回此 X.509v3 憑證的金鑰演算法資訊作為字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-304">Returns the key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="deb6c-305">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-306">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-307">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-307">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="deb6c-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="deb6c-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="deb6c-309">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-309">**Description:**</span></span>  
<span data-ttu-id="deb6c-310">傳回此 X.509v3 憑證的金鑰演算法參數作為十六進位字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-310">Returns the key algorithm parameters for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="deb6c-311">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-312">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-313">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-313">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="deb6c-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="deb6c-314">CertNameInfo</span></span>
<span data-ttu-id="deb6c-315">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-315">**Description:**</span></span>  
<span data-ttu-id="deb6c-316">傳回憑證的主體與簽發者名稱。</span><span class="sxs-lookup"><span data-stu-id="deb6c-316">Returns the subject and issuer names from a certificate.</span></span>

<span data-ttu-id="deb6c-317">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="deb6c-318">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-319">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-319">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="deb6c-320">X509NameType：主體的 X509NameType 值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-320">X509NameType: The X509NameType value for the subject.</span></span>
*   <span data-ttu-id="deb6c-321">includesIssuerName：true 則包含簽發者名稱，否則為 false。</span><span class="sxs-lookup"><span data-stu-id="deb6c-321">includesIssuerName: true to include the issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="deb6c-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="deb6c-322">CertNotAfter</span></span>
<span data-ttu-id="deb6c-323">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-323">**Description:**</span></span>  
<span data-ttu-id="deb6c-324">傳回憑證失效的當地時間日期。</span><span class="sxs-lookup"><span data-stu-id="deb6c-324">Returns the date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="deb6c-325">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-326">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-327">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-327">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="deb6c-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="deb6c-328">CertNotBefore</span></span>
<span data-ttu-id="deb6c-329">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-329">**Description:**</span></span>  
<span data-ttu-id="deb6c-330">傳回憑證開始生效的當地時間日期。</span><span class="sxs-lookup"><span data-stu-id="deb6c-330">Returns the date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="deb6c-331">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-332">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-333">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-333">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="deb6c-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="deb6c-334">CertPublicKeyOid</span></span>
<span data-ttu-id="deb6c-335">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-335">**Description:**</span></span>  
<span data-ttu-id="deb6c-336">傳回 X.509v3 憑證公開金鑰的 Oid。</span><span class="sxs-lookup"><span data-stu-id="deb6c-336">Returns the Oid of the public key for the X.509v3 certificate.</span></span>

<span data-ttu-id="deb6c-337">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-338">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-339">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-339">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="deb6c-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="deb6c-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="deb6c-341">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-341">**Description:**</span></span>  
<span data-ttu-id="deb6c-342">傳回 X.509v3 憑證公開金鑰參數的 Oid。</span><span class="sxs-lookup"><span data-stu-id="deb6c-342">Returns the Oid of the public key parameters for the X.509v3 certificate.</span></span>

<span data-ttu-id="deb6c-343">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-344">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-345">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-345">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="deb6c-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="deb6c-346">CertSerialNumber</span></span>
<span data-ttu-id="deb6c-347">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-347">**Description:**</span></span>  
<span data-ttu-id="deb6c-348">傳回 X.509v3 憑證的序號。</span><span class="sxs-lookup"><span data-stu-id="deb6c-348">Returns the serial number of the X.509v3 certificate.</span></span>

<span data-ttu-id="deb6c-349">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-350">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-351">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-351">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="deb6c-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="deb6c-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="deb6c-353">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-353">**Description:**</span></span>  
<span data-ttu-id="deb6c-354">傳回建立憑證簽章所用演算法的 Oid。</span><span class="sxs-lookup"><span data-stu-id="deb6c-354">Returns the Oid of the algorithm used to create the signature of a certificate.</span></span>

<span data-ttu-id="deb6c-355">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-356">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-357">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-357">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="deb6c-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="deb6c-358">CertSubject</span></span>
<span data-ttu-id="deb6c-359">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-359">**Description:**</span></span>  
<span data-ttu-id="deb6c-360">取得憑證的主體辨別名稱。</span><span class="sxs-lookup"><span data-stu-id="deb6c-360">Gets the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="deb6c-361">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-362">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-363">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-363">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="deb6c-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="deb6c-364">CertSubjectNameDN</span></span>
<span data-ttu-id="deb6c-365">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-365">**Description:**</span></span>  
<span data-ttu-id="deb6c-366">傳回憑證的主體辨別名稱。</span><span class="sxs-lookup"><span data-stu-id="deb6c-366">Returns the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="deb6c-367">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-368">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-369">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-369">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="deb6c-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="deb6c-370">CertSubjectNameOid</span></span>
<span data-ttu-id="deb6c-371">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-371">**Description:**</span></span>  
<span data-ttu-id="deb6c-372">傳回憑證主體名稱的 Oid。</span><span class="sxs-lookup"><span data-stu-id="deb6c-372">Returns the Oid of the subject name from a certificate.</span></span>

<span data-ttu-id="deb6c-373">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-374">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-375">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-375">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="deb6c-376">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="deb6c-376">CertThumbprint</span></span>
<span data-ttu-id="deb6c-377">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-377">**Description:**</span></span>  
<span data-ttu-id="deb6c-378">傳回憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="deb6c-378">Returns the thumbprint of a certificate.</span></span>

<span data-ttu-id="deb6c-379">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-380">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-381">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-381">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="deb6c-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="deb6c-382">CertVersion</span></span>
<span data-ttu-id="deb6c-383">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-383">**Description:**</span></span>  
<span data-ttu-id="deb6c-384">傳回憑證的 X.509 格式版本。</span><span class="sxs-lookup"><span data-stu-id="deb6c-384">Returns the X.509 format version of a certificate.</span></span>

<span data-ttu-id="deb6c-385">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-386">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-387">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-387">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="deb6c-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="deb6c-388">CGuid</span></span>
<span data-ttu-id="deb6c-389">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-389">**Description:**</span></span>  
<span data-ttu-id="deb6c-390">CGuid 函式會將 GUID 的字串表示法轉換為二進位表示法。</span><span class="sxs-lookup"><span data-stu-id="deb6c-390">The CGuid function converts the string representation of a GUID to its binary representation.</span></span>

<span data-ttu-id="deb6c-391">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="deb6c-392">使用此模式格式化的字串：xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 或 {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="deb6c-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="deb6c-393">Contains</span><span class="sxs-lookup"><span data-stu-id="deb6c-393">Contains</span></span>
<span data-ttu-id="deb6c-394">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-394">**Description:**</span></span>  
<span data-ttu-id="deb6c-395">Contains 函式會在多重值屬性內尋找字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-395">The Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="deb6c-396">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-396">**Syntax:**</span></span>  
<span data-ttu-id="deb6c-397">`num Contains (mvstring attribute, str search)` - 區分大小寫</span><span class="sxs-lookup"><span data-stu-id="deb6c-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="deb6c-398">`num Contains (mvref attribute, str search)` - 區分大小寫</span><span class="sxs-lookup"><span data-stu-id="deb6c-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="deb6c-399">attribute：要搜尋的多重值屬性。</span><span class="sxs-lookup"><span data-stu-id="deb6c-399">attribute: the multi-valued attribute to search.</span></span>
* <span data-ttu-id="deb6c-400">search：要在屬性中尋找的字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-400">search: string to find in the attribute.</span></span>
* <span data-ttu-id="deb6c-401">Casetype：CaseInsensitive 或 CaseSensitive。</span><span class="sxs-lookup"><span data-stu-id="deb6c-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="deb6c-402">傳回在多重值屬性中找到字串的索引。</span><span class="sxs-lookup"><span data-stu-id="deb6c-402">Returns index in the multi-valued attribute where the string was found.</span></span> <span data-ttu-id="deb6c-403">如果找不到該字串，即會傳回 0。</span><span class="sxs-lookup"><span data-stu-id="deb6c-403">0 is returned if the string is not found.</span></span>

<span data-ttu-id="deb6c-404">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-404">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-405">針對多重值字串屬性，搜尋會在值中尋找子字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-405">For multi-valued string attributes, the search finds substrings in the values.</span></span>  
<span data-ttu-id="deb6c-406">針對參考屬性，搜尋的字串必須完全符合要被視為相符的值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-406">For reference attributes, the searched string must exactly match the value to be considered a match.</span></span>

<span data-ttu-id="deb6c-407">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="deb6c-408">如果 proxyAddresses 屬性具有主要電子郵件地址 (以大寫 "SMTP:" 表示)，就會傳回 proxyAddress 屬性，否則會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="deb6c-408">If the proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return the proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="deb6c-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="deb6c-409">ConvertFromBase64</span></span>
<span data-ttu-id="deb6c-410">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-410">**Description:**</span></span>  
<span data-ttu-id="deb6c-411">ConvertFromBase64 函式會將指定的 base64 編碼值轉換為一般字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-411">The ConvertFromBase64 function converts the specified base64 encoded value to a regular string.</span></span>

<span data-ttu-id="deb6c-412">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-412">**Syntax:**</span></span>  
<span data-ttu-id="deb6c-413">`str ConvertFromBase64(str source)` - 假設使用 Unicode 進行編碼</span><span class="sxs-lookup"><span data-stu-id="deb6c-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="deb6c-414">source：Base64 編碼的字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="deb6c-415">Encoding：Unicode、ASCII、UTF8</span><span class="sxs-lookup"><span data-stu-id="deb6c-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="deb6c-416">**範例**</span><span class="sxs-lookup"><span data-stu-id="deb6c-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="deb6c-417">這兩個範例都會傳回 "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="deb6c-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="deb6c-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="deb6c-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="deb6c-419">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-419">**Description:**</span></span>  
<span data-ttu-id="deb6c-420">ConvertFromUTF8Hex 函式會將指定的 UTF8 十六進位編碼值轉換為字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-420">The ConvertFromUTF8Hex function converts the specified UTF8 Hex encoded value to a string.</span></span>

<span data-ttu-id="deb6c-421">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="deb6c-422">source：UTF8 2 個位元組的編碼字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="deb6c-423">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-423">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-424">此函式與 ConvertFromBase64([],UTF8) 之間的差異在於結果支援 DN 屬性。</span><span class="sxs-lookup"><span data-stu-id="deb6c-424">The difference between this function and ConvertFromBase64([],UTF8) in that the result is friendly for the DN attribute.</span></span>  
<span data-ttu-id="deb6c-425">Azure Active Directory 會使用此格式做為 DN。</span><span class="sxs-lookup"><span data-stu-id="deb6c-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="deb6c-426">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="deb6c-427">傳回 "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="deb6c-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="deb6c-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="deb6c-428">ConvertToBase64</span></span>
<span data-ttu-id="deb6c-429">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-429">**Description:**</span></span>  
<span data-ttu-id="deb6c-430">ConvertToBase64 函式會將字串轉換為 Unicode Base64 字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-430">The ConvertToBase64 function converts a string to a Unicode base64 string.</span></span>  
<span data-ttu-id="deb6c-431">將整數陣列的值轉換為其對等的字串表示法，此表示法是以 Base-64 數字編碼的。</span><span class="sxs-lookup"><span data-stu-id="deb6c-431">Converts the value of an array of integers to its equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="deb6c-432">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="deb6c-433">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="deb6c-434">傳回 "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span><span class="sxs-lookup"><span data-stu-id="deb6c-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="deb6c-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="deb6c-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="deb6c-436">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-436">**Description:**</span></span>  
<span data-ttu-id="deb6c-437">ConvertToUTF8Hex 函式會將字串轉換為 UTF8 十六進位編碼值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-437">The ConvertToUTF8Hex function converts a string to a UTF8 Hex encoded value.</span></span>

<span data-ttu-id="deb6c-438">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="deb6c-439">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-439">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-440">Azure Active Directory 會使用此函式的輸出格式做為 DN 屬性格式。</span><span class="sxs-lookup"><span data-stu-id="deb6c-440">The output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="deb6c-441">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="deb6c-442">傳回 48656C6C6F20776F726C6421</span><span class="sxs-lookup"><span data-stu-id="deb6c-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="deb6c-443">Count</span><span class="sxs-lookup"><span data-stu-id="deb6c-443">Count</span></span>
<span data-ttu-id="deb6c-444">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-444">**Description:**</span></span>  
<span data-ttu-id="deb6c-445">Count 函式會傳回多重值屬性中的元素個數</span><span class="sxs-lookup"><span data-stu-id="deb6c-445">The Count function returns the number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="deb6c-446">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="deb6c-447">CNum</span><span class="sxs-lookup"><span data-stu-id="deb6c-447">CNum</span></span>
<span data-ttu-id="deb6c-448">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-448">**Description:**</span></span>  
<span data-ttu-id="deb6c-449">CNum 函式會取得字串，並傳回數值資料類型。</span><span class="sxs-lookup"><span data-stu-id="deb6c-449">The CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="deb6c-450">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="deb6c-451">CRef</span><span class="sxs-lookup"><span data-stu-id="deb6c-451">CRef</span></span>
<span data-ttu-id="deb6c-452">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-452">**Description:**</span></span>  
<span data-ttu-id="deb6c-453">將字串轉換為參考屬性</span><span class="sxs-lookup"><span data-stu-id="deb6c-453">Converts a string to a reference attribute</span></span>

<span data-ttu-id="deb6c-454">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="deb6c-455">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="deb6c-456">CStr</span><span class="sxs-lookup"><span data-stu-id="deb6c-456">CStr</span></span>
<span data-ttu-id="deb6c-457">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-457">**Description:**</span></span>  
<span data-ttu-id="deb6c-458">CStr 函式會轉換為字串資料類型。</span><span class="sxs-lookup"><span data-stu-id="deb6c-458">The CStr function converts to a string data type.</span></span>

<span data-ttu-id="deb6c-459">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="deb6c-460">value：可以是數值、參考屬性或布林值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="deb6c-461">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="deb6c-462">可能傳回 "cn=Joe,dc=contoso,dc=com"</span><span class="sxs-lookup"><span data-stu-id="deb6c-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="deb6c-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="deb6c-463">DateAdd</span></span>
<span data-ttu-id="deb6c-464">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-464">**Description:**</span></span>  
<span data-ttu-id="deb6c-465">傳回日期，其中包含已新增指定時間間隔的日期。</span><span class="sxs-lookup"><span data-stu-id="deb6c-465">Returns a Date containing a date to which a specified time interval has been added.</span></span>

<span data-ttu-id="deb6c-466">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="deb6c-467">interval：字串運算式，此為您想要加入的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="deb6c-467">interval: String expression that is the interval of time you want to add.</span></span> <span data-ttu-id="deb6c-468">字串必須具有下列其中一個值：</span><span class="sxs-lookup"><span data-stu-id="deb6c-468">The string must have one of the following values:</span></span>
  * <span data-ttu-id="deb6c-469">yyyy 年</span><span class="sxs-lookup"><span data-stu-id="deb6c-469">yyyy Year</span></span>
  * <span data-ttu-id="deb6c-470">q 季</span><span class="sxs-lookup"><span data-stu-id="deb6c-470">q Quarter</span></span>
  * <span data-ttu-id="deb6c-471">m 月</span><span class="sxs-lookup"><span data-stu-id="deb6c-471">m Month</span></span>
  * <span data-ttu-id="deb6c-472">y 一年中第幾天</span><span class="sxs-lookup"><span data-stu-id="deb6c-472">y Day of year</span></span>
  * <span data-ttu-id="deb6c-473">d 日</span><span class="sxs-lookup"><span data-stu-id="deb6c-473">d Day</span></span>
  * <span data-ttu-id="deb6c-474">w 工作日</span><span class="sxs-lookup"><span data-stu-id="deb6c-474">w Weekday</span></span>
  * <span data-ttu-id="deb6c-475">ww 周</span><span class="sxs-lookup"><span data-stu-id="deb6c-475">ww Week</span></span>
  * <span data-ttu-id="deb6c-476">h 小時</span><span class="sxs-lookup"><span data-stu-id="deb6c-476">h Hour</span></span>
  * <span data-ttu-id="deb6c-477">n 分鐘</span><span class="sxs-lookup"><span data-stu-id="deb6c-477">n Minute</span></span>
  * <span data-ttu-id="deb6c-478">s 秒</span><span class="sxs-lookup"><span data-stu-id="deb6c-478">s Second</span></span>
* <span data-ttu-id="deb6c-479">value：您想要加入的單位數。</span><span class="sxs-lookup"><span data-stu-id="deb6c-479">value: The number of units you want to add.</span></span> <span data-ttu-id="deb6c-480">它可以是正數 (用以取得未來的日期) 或負數 (用以取得過去的日期)。</span><span class="sxs-lookup"><span data-stu-id="deb6c-480">It can be positive (to get dates in the future) or negative (to get dates in the past).</span></span>
* <span data-ttu-id="deb6c-481">date：DateTime 代表要加入間隔的日期。</span><span class="sxs-lookup"><span data-stu-id="deb6c-481">date: DateTime representing date to which the interval is added.</span></span>

<span data-ttu-id="deb6c-482">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="deb6c-483">新增 3 個月，並傳回代表 "2001-04-01" 的 DateTime。</span><span class="sxs-lookup"><span data-stu-id="deb6c-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="deb6c-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="deb6c-484">DateFromNum</span></span>
<span data-ttu-id="deb6c-485">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-485">**Description:**</span></span>  
<span data-ttu-id="deb6c-486">DateFromNum 函式會將 AD 日期格式的值轉換為 DateTime 類型。</span><span class="sxs-lookup"><span data-stu-id="deb6c-486">The DateFromNum function converts a value in AD’s date format to a DateTime type.</span></span>

<span data-ttu-id="deb6c-487">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="deb6c-488">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="deb6c-489">傳回代表 2012-01-01 23:00:00 的 DateTime</span><span class="sxs-lookup"><span data-stu-id="deb6c-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="deb6c-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="deb6c-490">DNComponent</span></span>
<span data-ttu-id="deb6c-491">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-491">**Description:**</span></span>  
<span data-ttu-id="deb6c-492">DNComponent 函式會從左邊傳回指定 DN 元件的值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-492">The DNComponent function returns the value of a specified DN component going from left.</span></span>

<span data-ttu-id="deb6c-493">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="deb6c-494">dn：要解譯的參考屬性</span><span class="sxs-lookup"><span data-stu-id="deb6c-494">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="deb6c-495">ComponentNumber：DN 中要傳回的元件</span><span class="sxs-lookup"><span data-stu-id="deb6c-495">ComponentNumber: The component in the DN to return</span></span>

<span data-ttu-id="deb6c-496">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="deb6c-497">如果 dn 為 "cn=Joe,ou=…"，就會傳回 Joe</span><span class="sxs-lookup"><span data-stu-id="deb6c-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="deb6c-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="deb6c-498">DNComponentRev</span></span>
<span data-ttu-id="deb6c-499">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-499">**Description:**</span></span>  
<span data-ttu-id="deb6c-500">DNComponentRev 函式會從右邊 (結尾處) 傳回指定 DN 元件的值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-500">The DNComponentRev function returns the value of a specified DN component going from right (the end).</span></span>

<span data-ttu-id="deb6c-501">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="deb6c-502">dn：要解譯的參考屬性</span><span class="sxs-lookup"><span data-stu-id="deb6c-502">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="deb6c-503">ComponentNumber - DN 中要傳回的元件</span><span class="sxs-lookup"><span data-stu-id="deb6c-503">ComponentNumber - The component in the DN to return</span></span>
* <span data-ttu-id="deb6c-504">Options：DC - 忽略所有含 "dc=" 的元件</span><span class="sxs-lookup"><span data-stu-id="deb6c-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="deb6c-505">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-505">**Example:**</span></span>  
<span data-ttu-id="deb6c-506">如果 dn 是 "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com"，則</span><span class="sxs-lookup"><span data-stu-id="deb6c-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="deb6c-507">兩者都傳回 US。</span><span class="sxs-lookup"><span data-stu-id="deb6c-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="deb6c-508">Error</span><span class="sxs-lookup"><span data-stu-id="deb6c-508">Error</span></span>
<span data-ttu-id="deb6c-509">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-509">**Description:**</span></span>  
<span data-ttu-id="deb6c-510">Error 函式是用來傳回自訂錯誤。</span><span class="sxs-lookup"><span data-stu-id="deb6c-510">The Error function is used to return a custom error.</span></span>

<span data-ttu-id="deb6c-511">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="deb6c-512">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="deb6c-513">如果 accountName 屬性不存在，即會擲回有關物件的錯誤。</span><span class="sxs-lookup"><span data-stu-id="deb6c-513">If the attribute accountName is not present, throw an error on the object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="deb6c-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="deb6c-514">EscapeDNComponent</span></span>
<span data-ttu-id="deb6c-515">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-515">**Description:**</span></span>  
<span data-ttu-id="deb6c-516">EscapeDNComponent 函式會接受 DN 的一個元件並逸出它，以便在 LDAP 中顯示它。</span><span class="sxs-lookup"><span data-stu-id="deb6c-516">The EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="deb6c-517">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="deb6c-518">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="deb6c-519">確保即使 displayName 屬性具有必須在 LDAP 中逸出的字元，還是能夠在 LDAP 目錄中建立物件。</span><span class="sxs-lookup"><span data-stu-id="deb6c-519">Makes sure the object can be created in an LDAP directory even if the displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="deb6c-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="deb6c-520">FormatDateTime</span></span>
<span data-ttu-id="deb6c-521">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-521">**Description:**</span></span>  
<span data-ttu-id="deb6c-522">FormatDateTime 函式可用來將 DateTime 格式化為具有指定格式的字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-522">The FormatDateTime function is used to format a DateTime to a string with a specified format</span></span>

<span data-ttu-id="deb6c-523">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="deb6c-524">value：DateTime 格式的值</span><span class="sxs-lookup"><span data-stu-id="deb6c-524">value: a value in the DateTime format</span></span>
* <span data-ttu-id="deb6c-525">format：字串，表示要轉換的目標格式。</span><span class="sxs-lookup"><span data-stu-id="deb6c-525">format: a string representing the format to convert to.</span></span>

<span data-ttu-id="deb6c-526">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-526">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-527">您可以在此處找到格式的可能值：[使用者定義日期/時間格式 (Format 函式)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="deb6c-527">The possible values for the format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="deb6c-528">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="deb6c-529">結果是 "2007-12-25"。</span><span class="sxs-lookup"><span data-stu-id="deb6c-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="deb6c-530">會產生 "20140905081453.0Z"</span><span class="sxs-lookup"><span data-stu-id="deb6c-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="deb6c-531">GUID</span><span class="sxs-lookup"><span data-stu-id="deb6c-531">GUID</span></span>
<span data-ttu-id="deb6c-532">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-532">**Description:**</span></span>  
<span data-ttu-id="deb6c-533">函式 GUID 會產生新的隨機 GUID</span><span class="sxs-lookup"><span data-stu-id="deb6c-533">The function GUID generates a new random GUID</span></span>

<span data-ttu-id="deb6c-534">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="deb6c-535">IIF</span><span class="sxs-lookup"><span data-stu-id="deb6c-535">IIF</span></span>
<span data-ttu-id="deb6c-536">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-536">**Description:**</span></span>  
<span data-ttu-id="deb6c-537">IIF 函式會根據指定的條件傳回其中一組可能值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-537">The IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="deb6c-538">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="deb6c-539">condition：可評估為 True 或 False 的任何值或運算式。</span><span class="sxs-lookup"><span data-stu-id="deb6c-539">condition: any value or expression that can be evaluated to true or false.</span></span>
* <span data-ttu-id="deb6c-540">valueIfTrue：條件評估為 True 時所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-540">valueIfTrue: If the condition evaluates to true, the returned value.</span></span>
* <span data-ttu-id="deb6c-541">valueIfFalse：條件評估為 false 時所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-541">valueIfFalse: If the condition evaluates to false, the returned value.</span></span>

<span data-ttu-id="deb6c-542">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="deb6c-543">如果使用者是實習生，就會傳回開頭加上 "t-" 的使用者別名，否則會依原樣傳回使用者的別名。</span><span class="sxs-lookup"><span data-stu-id="deb6c-543">If the user is an intern, returns the alias of a user with "t-" added to the beginning of it, else returns the user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="deb6c-544">InStr</span><span class="sxs-lookup"><span data-stu-id="deb6c-544">InStr</span></span>
<span data-ttu-id="deb6c-545">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-545">**Description:**</span></span>  
<span data-ttu-id="deb6c-546">InStr 函式會在字串中尋找第一個出現的子字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-546">The InStr function finds the first occurrence of a substring in a string</span></span>

<span data-ttu-id="deb6c-547">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="deb6c-548">stringcheck：要搜尋的字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-548">stringcheck: string to be searched</span></span>
* <span data-ttu-id="deb6c-549">stringmatch：要尋找的字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-549">stringmatch: string to be found</span></span>
* <span data-ttu-id="deb6c-550">start：開始尋找子字串的位置</span><span class="sxs-lookup"><span data-stu-id="deb6c-550">start: starting position to find the substring</span></span>
* <span data-ttu-id="deb6c-551">compare：vbTextCompare 或 vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="deb6c-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="deb6c-552">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-552">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-553">會傳回找到子字串的位置，如果找不到，則傳回 0。</span><span class="sxs-lookup"><span data-stu-id="deb6c-553">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="deb6c-554">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-554">**Example:**</span></span>  
`InStr("The quick brown fox","quick")`  
<span data-ttu-id="deb6c-555">評估為 5</span><span class="sxs-lookup"><span data-stu-id="deb6c-555">Evalues to 5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="deb6c-556">評估為 7</span><span class="sxs-lookup"><span data-stu-id="deb6c-556">Evaluates to 7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="deb6c-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="deb6c-557">InStrRev</span></span>
<span data-ttu-id="deb6c-558">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-558">**Description:**</span></span>  
<span data-ttu-id="deb6c-559">InStrRev 函式會在字串中尋找最後一個出現的子字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-559">The InStrRev function finds the last occurrence of a substring in a string</span></span>

<span data-ttu-id="deb6c-560">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="deb6c-561">stringcheck：要搜尋的字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-561">stringcheck: string to be searched</span></span>
* <span data-ttu-id="deb6c-562">stringmatch：要尋找的字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-562">stringmatch: string to be found</span></span>
* <span data-ttu-id="deb6c-563">start：開始尋找子字串的位置</span><span class="sxs-lookup"><span data-stu-id="deb6c-563">start: starting position to find the substring</span></span>
* <span data-ttu-id="deb6c-564">compare：vbTextCompare 或 vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="deb6c-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="deb6c-565">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-565">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-566">會傳回找到子字串的位置，如果找不到，則傳回 0。</span><span class="sxs-lookup"><span data-stu-id="deb6c-566">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="deb6c-567">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="deb6c-568">傳回 7</span><span class="sxs-lookup"><span data-stu-id="deb6c-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="deb6c-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="deb6c-569">IsBitSet</span></span>
<span data-ttu-id="deb6c-570">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-570">**Description:**</span></span>  
<span data-ttu-id="deb6c-571">IsBitSet 函式會測試是否已設定位元</span><span class="sxs-lookup"><span data-stu-id="deb6c-571">The function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="deb6c-572">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="deb6c-573">value：評估的數值。flag：具有要評估之位元的數值</span><span class="sxs-lookup"><span data-stu-id="deb6c-573">value: a numeric value that is evaluated.flag: a numeric value that has the bit to be evaluated</span></span>

<span data-ttu-id="deb6c-574">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="deb6c-575">因為位元 "4" 是使用十六進位值 "F" 所設定，所以會傳回 True</span><span class="sxs-lookup"><span data-stu-id="deb6c-575">Returns True because bit "4" is set in the hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="deb6c-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="deb6c-576">IsDate</span></span>
<span data-ttu-id="deb6c-577">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-577">**Description:**</span></span>  
<span data-ttu-id="deb6c-578">如果運算式可評估為 DateTime 類型，則 IsDate 函式會評估為 True。</span><span class="sxs-lookup"><span data-stu-id="deb6c-578">If the expression can be evaluates as a DateTime type, then the IsDate function evaluates to True.</span></span>

<span data-ttu-id="deb6c-579">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="deb6c-580">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-580">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-581">用來判斷 CDate() 是否可能成功。</span><span class="sxs-lookup"><span data-stu-id="deb6c-581">Used to determine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="deb6c-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="deb6c-582">IsCert</span></span>
<span data-ttu-id="deb6c-583">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-583">**Description:**</span></span>  
<span data-ttu-id="deb6c-584">如果原始資料可以序列化為 .NET X509Certificate2 憑證物件，則傳回 true。</span><span class="sxs-lookup"><span data-stu-id="deb6c-584">Returns true if the raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="deb6c-585">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="deb6c-586">certificateRawData：X.509 憑證的位元組陣列表示。</span><span class="sxs-lookup"><span data-stu-id="deb6c-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="deb6c-587">位元組陣列可以是編碼的二進位 (DER) 或 Base64 編碼的 X.509 資料。</span><span class="sxs-lookup"><span data-stu-id="deb6c-587">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="deb6c-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="deb6c-588">IsEmpty</span></span>
<span data-ttu-id="deb6c-589">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-589">**Description:**</span></span>  
<span data-ttu-id="deb6c-590">如果屬性存在於 CS 或 MV 中，但評估為空字串，則 IsEmpty 函式會評估為 True。</span><span class="sxs-lookup"><span data-stu-id="deb6c-590">If the attribute is present in the CS or MV but evaluates to an empty string, then the IsEmpty function evaluates to True.</span></span>

<span data-ttu-id="deb6c-591">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="deb6c-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="deb6c-592">IsGuid</span></span>
<span data-ttu-id="deb6c-593">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-593">**Description:**</span></span>  
<span data-ttu-id="deb6c-594">如果字串可轉換為 GUID，則 IsGuid 函式會評估為 True。</span><span class="sxs-lookup"><span data-stu-id="deb6c-594">If the string could be converted to a GUID, then the IsGuid function evaluated to true.</span></span>

<span data-ttu-id="deb6c-595">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="deb6c-596">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-596">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-597">GUID 定義為下列其中一種模式的字串： xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 或 {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="deb6c-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="deb6c-598">用來判斷 CGuid() 是否可能成功。</span><span class="sxs-lookup"><span data-stu-id="deb6c-598">Used to determine if CGuid() can be successful.</span></span>

<span data-ttu-id="deb6c-599">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="deb6c-600">如果 StrAttribute 具有 GUID 格式，即會傳回二進位表示法，否則會傳回 Null。</span><span class="sxs-lookup"><span data-stu-id="deb6c-600">If the StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="deb6c-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="deb6c-601">IsNull</span></span>
<span data-ttu-id="deb6c-602">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-602">**Description:**</span></span>  
<span data-ttu-id="deb6c-603">如果運算式評估為 Null，則 IsNull 函式會傳回 True。</span><span class="sxs-lookup"><span data-stu-id="deb6c-603">If the expression evaluates to Null, then the IsNull function returns true.</span></span>

<span data-ttu-id="deb6c-604">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="deb6c-605">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-605">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-606">針對屬性，Null 表示該屬性不存在。</span><span class="sxs-lookup"><span data-stu-id="deb6c-606">For an attribute, a Null is expressed by the absence of the attribute.</span></span>

<span data-ttu-id="deb6c-607">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="deb6c-608">如果屬性不存在於 CS 或 MV 中，即會傳回 True。</span><span class="sxs-lookup"><span data-stu-id="deb6c-608">Returns True if the attribute is not present in the CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="deb6c-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="deb6c-609">IsNullOrEmpty</span></span>
<span data-ttu-id="deb6c-610">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-610">**Description:**</span></span>  
<span data-ttu-id="deb6c-611">如果運算式為 Null 或空字串，則 IsNullOrEmpty 函式會傳回 True。</span><span class="sxs-lookup"><span data-stu-id="deb6c-611">If the expression is null or an empty string, then the IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="deb6c-612">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="deb6c-613">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-613">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-614">針對屬性，如果屬性不存在，或存在但為空字串，即會評估為 True。</span><span class="sxs-lookup"><span data-stu-id="deb6c-614">For an attribute, this would evaluate to True if the attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="deb6c-615">此函式的相反函式名稱為 IsPresent。</span><span class="sxs-lookup"><span data-stu-id="deb6c-615">The inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="deb6c-616">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="deb6c-617">如果屬性不存在於 CS 或 MV 中或為空字串，即會傳回 True。</span><span class="sxs-lookup"><span data-stu-id="deb6c-617">Returns True if the attribute is not present or is an empty string in the CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="deb6c-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="deb6c-618">IsNumeric</span></span>
<span data-ttu-id="deb6c-619">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-619">**Description:**</span></span>  
<span data-ttu-id="deb6c-620">IsNumeric 函式會傳回布林值，指出運算式是否可評估為數字類型。</span><span class="sxs-lookup"><span data-stu-id="deb6c-620">The IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="deb6c-621">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="deb6c-622">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-622">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-623">用來判斷 CNum() 是否可成功剖析運算式。</span><span class="sxs-lookup"><span data-stu-id="deb6c-623">Used to determine if CNum() can be successful to parse the expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="deb6c-624">IsString</span><span class="sxs-lookup"><span data-stu-id="deb6c-624">IsString</span></span>
<span data-ttu-id="deb6c-625">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-625">**Description:**</span></span>  
<span data-ttu-id="deb6c-626">如果運算式可評估為字串類型，則 IsString 函式會評估為 True。</span><span class="sxs-lookup"><span data-stu-id="deb6c-626">If the expression can be evaluated to a string type, then the IsString function evaluates to True.</span></span>

<span data-ttu-id="deb6c-627">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="deb6c-628">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-628">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-629">用來判斷 CStr() 是否可成功剖析運算式。</span><span class="sxs-lookup"><span data-stu-id="deb6c-629">Used to determine if CStr() can be successful to parse the expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="deb6c-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="deb6c-630">IsPresent</span></span>
<span data-ttu-id="deb6c-631">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-631">**Description:**</span></span>  
<span data-ttu-id="deb6c-632">如果運算式評估為非 Null 且不是空字串，則 IsPresent 函式會傳回 True。</span><span class="sxs-lookup"><span data-stu-id="deb6c-632">If the expression evaluates to a string that is not Null and is not empty, then the IsPresent function returns true.</span></span>

<span data-ttu-id="deb6c-633">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="deb6c-634">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-634">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-635">這個函式的相反函式名稱為 IsNullOrEmpty。</span><span class="sxs-lookup"><span data-stu-id="deb6c-635">The inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="deb6c-636">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="deb6c-637">Item</span><span class="sxs-lookup"><span data-stu-id="deb6c-637">Item</span></span>
<span data-ttu-id="deb6c-638">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-638">**Description:**</span></span>  
<span data-ttu-id="deb6c-639">Item 函式會從多重值字串/屬性傳回一個項目。</span><span class="sxs-lookup"><span data-stu-id="deb6c-639">The Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="deb6c-640">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="deb6c-641">attribute：多重值的屬性</span><span class="sxs-lookup"><span data-stu-id="deb6c-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="deb6c-642">index：多重值字串中項目的索引。</span><span class="sxs-lookup"><span data-stu-id="deb6c-642">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="deb6c-643">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-643">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-644">Item 函式可以與 Contains 函式搭配使用，因為後者會將索引傳回多重值屬性中的項目。</span><span class="sxs-lookup"><span data-stu-id="deb6c-644">The Item function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="deb6c-645">如果索引超出範圍，即會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="deb6c-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="deb6c-646">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="deb6c-647">會傳回主要電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="deb6c-647">Returns the primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="deb6c-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="deb6c-648">ItemOrNull</span></span>
<span data-ttu-id="deb6c-649">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-649">**Description:**</span></span>  
<span data-ttu-id="deb6c-650">ItemOrNull 函式會從多重值字串/屬性傳回一個項目。</span><span class="sxs-lookup"><span data-stu-id="deb6c-650">The ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="deb6c-651">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="deb6c-652">attribute：多重值的屬性</span><span class="sxs-lookup"><span data-stu-id="deb6c-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="deb6c-653">index：多重值字串中項目的索引。</span><span class="sxs-lookup"><span data-stu-id="deb6c-653">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="deb6c-654">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-654">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-655">ItemOrNull 函式可以與 Contains 函式搭配使用，因為後者會將索引傳回多重值屬性中的項目。</span><span class="sxs-lookup"><span data-stu-id="deb6c-655">The ItemOrNull function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="deb6c-656">如果索引超出範圍，則會傳回 Null 值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="deb6c-657">Join</span><span class="sxs-lookup"><span data-stu-id="deb6c-657">Join</span></span>
<span data-ttu-id="deb6c-658">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-658">**Description:**</span></span>  
<span data-ttu-id="deb6c-659">Join 函式會接受多重值的字串，並傳回單一值的字串，其中每個項目之間都插入指定的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="deb6c-659">The Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="deb6c-660">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="deb6c-661">attribute：包含要聯結之字串的多重值屬性。</span><span class="sxs-lookup"><span data-stu-id="deb6c-661">attribute: Multi-valued attribute containing strings to be joined.</span></span>
* <span data-ttu-id="deb6c-662">delimiter：任何字串，可用來分隔傳回字串中的子字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-662">delimiter: Any string, used to separate the substrings in the returned string.</span></span> <span data-ttu-id="deb6c-663">如果省略，即會使用空格字元 (" ")。</span><span class="sxs-lookup"><span data-stu-id="deb6c-663">If omitted, the space character (" ") is used.</span></span> <span data-ttu-id="deb6c-664">如果分隔符號是零長度字串 ("") 或 Nothing，就不會使用分隔符號來串連清單中的所有項目。</span><span class="sxs-lookup"><span data-stu-id="deb6c-664">If Delimiter is a zero-length string ("") or Nothing, all items in the list are concatenated with no delimiters.</span></span>

<span data-ttu-id="deb6c-665">**備註**</span><span class="sxs-lookup"><span data-stu-id="deb6c-665">**Remarks**</span></span>  
<span data-ttu-id="deb6c-666">Join 和 Split 函式之間有同位。</span><span class="sxs-lookup"><span data-stu-id="deb6c-666">There is parity between the Join and Split functions.</span></span> <span data-ttu-id="deb6c-667">Join 函式可接受字串陣列，並使用分隔符號字串來聯結它們，以傳回單一字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-667">The Join function takes an array of strings and joins them using a delimiter string, to return a single string.</span></span> <span data-ttu-id="deb6c-668">Split 函式會取得字串並以分隔符號來分隔，以傳回字串陣列。</span><span class="sxs-lookup"><span data-stu-id="deb6c-668">The Split function takes a string and separates it at the delimiter, to return an array of strings.</span></span> <span data-ttu-id="deb6c-669">不過，主要的差別是 Join 可以使用任何分隔符號字串來串連字串，Split 只能使用單一字元分隔符號來分隔字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="deb6c-670">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="deb6c-671">可能傳回："SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="deb6c-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="deb6c-672">LCase</span><span class="sxs-lookup"><span data-stu-id="deb6c-672">LCase</span></span>
<span data-ttu-id="deb6c-673">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-673">**Description:**</span></span>  
<span data-ttu-id="deb6c-674">LCase 函式會將字串中的所有字元轉換為小寫。</span><span class="sxs-lookup"><span data-stu-id="deb6c-674">The LCase function converts all characters in a string to lower case.</span></span>

<span data-ttu-id="deb6c-675">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="deb6c-676">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="deb6c-677">傳回 "test"。</span><span class="sxs-lookup"><span data-stu-id="deb6c-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="deb6c-678">Left</span><span class="sxs-lookup"><span data-stu-id="deb6c-678">Left</span></span>
<span data-ttu-id="deb6c-679">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-679">**Description:**</span></span>  
<span data-ttu-id="deb6c-680">Left 函式會從字串左邊傳回指定的字元數。</span><span class="sxs-lookup"><span data-stu-id="deb6c-680">The Left function returns a specified number of characters from the left of a string.</span></span>

<span data-ttu-id="deb6c-681">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="deb6c-682">string：要傳回字元的字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-682">string: the string to return characters from</span></span>
* <span data-ttu-id="deb6c-683">NumChars：數字，識別從 string 開頭 (左邊) 傳回的字元數</span><span class="sxs-lookup"><span data-stu-id="deb6c-683">NumChars: a number identifying the number of characters to return from the beginning (left) of string</span></span>

<span data-ttu-id="deb6c-684">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-684">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-685">包含 string 中前 numChars 個字元的字串：</span><span class="sxs-lookup"><span data-stu-id="deb6c-685">A string containing the first numChars characters in string:</span></span>

* <span data-ttu-id="deb6c-686">如果 numChars = 0，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="deb6c-687">如果 numChars < 0，會傳回輸入字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="deb6c-688">如果 string 為 Null，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-688">If string is null, return empty string.</span></span>

<span data-ttu-id="deb6c-689">如果 string 包含的字元數比 numChars 中指定的數目少，即會傳回與 string 完全相同的字串 (也就是，包含參數 1 中的所有字元)。</span><span class="sxs-lookup"><span data-stu-id="deb6c-689">If string contains fewer characters than the number specified in numChars, a string identical to string (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="deb6c-690">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="deb6c-691">傳回 "Joh"。</span><span class="sxs-lookup"><span data-stu-id="deb6c-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="deb6c-692">Len</span><span class="sxs-lookup"><span data-stu-id="deb6c-692">Len</span></span>
<span data-ttu-id="deb6c-693">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-693">**Description:**</span></span>  
<span data-ttu-id="deb6c-694">Len 函式會傳回字串中的字元數。</span><span class="sxs-lookup"><span data-stu-id="deb6c-694">The Len function returns number of characters in a string.</span></span>

<span data-ttu-id="deb6c-695">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="deb6c-696">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="deb6c-697">傳回 8</span><span class="sxs-lookup"><span data-stu-id="deb6c-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="deb6c-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="deb6c-698">LTrim</span></span>
<span data-ttu-id="deb6c-699">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-699">**Description:**</span></span>  
<span data-ttu-id="deb6c-700">LTrim 函式會從字串中移除開頭空白字元。</span><span class="sxs-lookup"><span data-stu-id="deb6c-700">The LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="deb6c-701">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="deb6c-702">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="deb6c-703">傳回 "Test"</span><span class="sxs-lookup"><span data-stu-id="deb6c-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="deb6c-704">Mid</span><span class="sxs-lookup"><span data-stu-id="deb6c-704">Mid</span></span>
<span data-ttu-id="deb6c-705">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-705">**Description:**</span></span>  
<span data-ttu-id="deb6c-706">Mid 函式會從字串中的指定位置傳回指定的字元數。</span><span class="sxs-lookup"><span data-stu-id="deb6c-706">The Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="deb6c-707">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="deb6c-708">string：要傳回字元的字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-708">string: the string to return characters from</span></span>
* <span data-ttu-id="deb6c-709">start：數字，可識別 string 中要傳回字元的起始位置</span><span class="sxs-lookup"><span data-stu-id="deb6c-709">start: a number identifying the starting position in string to return characters from</span></span>
* <span data-ttu-id="deb6c-710">NumChars：數字，可識別要從 string 中的位置傳回的字元數</span><span class="sxs-lookup"><span data-stu-id="deb6c-710">NumChars: a number identifying the number of characters to return from position in string</span></span>

<span data-ttu-id="deb6c-711">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-711">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-712">從 string 中的位置 start 開始傳回 numChars 個字元。</span><span class="sxs-lookup"><span data-stu-id="deb6c-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="deb6c-713">包含從 string 中的位置 start 起算的 numChars 個字元的字串：</span><span class="sxs-lookup"><span data-stu-id="deb6c-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="deb6c-714">如果 numChars = 0，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="deb6c-715">如果 numChars < 0，會傳回輸入字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="deb6c-716">如果 start > 字串的長度，會傳回輸入字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-716">If start > the length of string, return input string.</span></span>
* <span data-ttu-id="deb6c-717">如果 start < = 0，會傳回輸入字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="deb6c-718">如果 string 為 Null，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-718">If string is null, return empty string.</span></span>

<span data-ttu-id="deb6c-719">如果 string 中從位置 start 起算所剩餘的字元數不足 numChar 個字元，即會盡可能地傳回許多字元。</span><span class="sxs-lookup"><span data-stu-id="deb6c-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="deb6c-720">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="deb6c-721">傳回 "hn Do"。</span><span class="sxs-lookup"><span data-stu-id="deb6c-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="deb6c-722">傳回 "Doe"</span><span class="sxs-lookup"><span data-stu-id="deb6c-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="deb6c-723">Now</span><span class="sxs-lookup"><span data-stu-id="deb6c-723">Now</span></span>
<span data-ttu-id="deb6c-724">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-724">**Description:**</span></span>  
<span data-ttu-id="deb6c-725">Now 函式會根據您電腦的系統日期和時間，傳回指定目前日期和時間的 DateTime。</span><span class="sxs-lookup"><span data-stu-id="deb6c-725">The Now function returns a DateTime specifying the current date and time, according to your computer's system date and time.</span></span>

<span data-ttu-id="deb6c-726">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="deb6c-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="deb6c-727">NumFromDate</span></span>
<span data-ttu-id="deb6c-728">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-728">**Description:**</span></span>  
<span data-ttu-id="deb6c-729">NumFromDate 函式會以 AD 的日期格式傳回日期。</span><span class="sxs-lookup"><span data-stu-id="deb6c-729">The NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="deb6c-730">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="deb6c-731">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="deb6c-732">傳回 129699324000000000</span><span class="sxs-lookup"><span data-stu-id="deb6c-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="deb6c-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="deb6c-733">PadLeft</span></span>
<span data-ttu-id="deb6c-734">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-734">**Description:**</span></span>  
<span data-ttu-id="deb6c-735">PadLeft 函式會使用提供的填補字元，將字串左側填補到指定的長度。</span><span class="sxs-lookup"><span data-stu-id="deb6c-735">The PadLeft function left-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="deb6c-736">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="deb6c-737">string：要填補的字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-737">string: the string to pad.</span></span>
* <span data-ttu-id="deb6c-738">length：表示 string 所需長度的整數。</span><span class="sxs-lookup"><span data-stu-id="deb6c-738">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="deb6c-739">padCharacter：字串，由用來做為填補字元的單一字元所組成</span><span class="sxs-lookup"><span data-stu-id="deb6c-739">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="deb6c-740">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-740">**Remarks:**</span></span>

* <span data-ttu-id="deb6c-741">如果 string 的長度小於 length，則會將 padCharacter 重複附加至 string 的開頭 (左邊)，直到它的長度等於 length 為止。</span><span class="sxs-lookup"><span data-stu-id="deb6c-741">If the length of string is less than length, then padCharacter is repeatedly appended to the beginning (left) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="deb6c-742">PadCharacter 可以是空白字元，但不能是 Null 值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="deb6c-743">如果 string 的長度等於或大於 length，就會以原樣傳回 string。</span><span class="sxs-lookup"><span data-stu-id="deb6c-743">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="deb6c-744">如果 string 的長度大於或等於 length，即會傳回與 string 完全相同的字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-744">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="deb6c-745">如果 string 的長度小於 length，則會傳回所需長度的新字串，包含使用 padCharacter 填補的 string。</span><span class="sxs-lookup"><span data-stu-id="deb6c-745">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="deb6c-746">如果 string 為 Null，函式即會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-746">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="deb6c-747">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="deb6c-748">傳回 "000000User"。</span><span class="sxs-lookup"><span data-stu-id="deb6c-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="deb6c-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="deb6c-749">PadRight</span></span>
<span data-ttu-id="deb6c-750">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-750">**Description:**</span></span>  
<span data-ttu-id="deb6c-751">PadRight 函式會使用提供的填補字元，將字串右側填補到指定的長度。</span><span class="sxs-lookup"><span data-stu-id="deb6c-751">The PadRight function right-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="deb6c-752">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="deb6c-753">string：要填補的字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-753">string: the string to pad.</span></span>
* <span data-ttu-id="deb6c-754">length：表示 string 所需長度的整數。</span><span class="sxs-lookup"><span data-stu-id="deb6c-754">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="deb6c-755">padCharacter：字串，由用來做為填補字元的單一字元所組成</span><span class="sxs-lookup"><span data-stu-id="deb6c-755">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="deb6c-756">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-756">**Remarks:**</span></span>

* <span data-ttu-id="deb6c-757">如果 string 的長度小於 length，則會將 padCharacter 重複附加至 string 的結尾 (右邊)，直到它的長度等於 length 為止。</span><span class="sxs-lookup"><span data-stu-id="deb6c-757">If the length of string is less than length, then padCharacter is repeatedly appended to the end (right) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="deb6c-758">PadCharacter 可以是空白字元，但不能是 Null 值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="deb6c-759">如果 string 的長度等於或大於 length，就會以原樣傳回 string。</span><span class="sxs-lookup"><span data-stu-id="deb6c-759">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="deb6c-760">如果 string 的長度大於或等於 length，即會傳回與 string 完全相同的字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-760">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="deb6c-761">如果 string 的長度小於 length，則會傳回所需長度的新字串，包含使用 padCharacter 填補的 string。</span><span class="sxs-lookup"><span data-stu-id="deb6c-761">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="deb6c-762">如果 string 為 Null，函式即會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-762">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="deb6c-763">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="deb6c-764">傳回 "User000000"。</span><span class="sxs-lookup"><span data-stu-id="deb6c-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="deb6c-765">PCase</span><span class="sxs-lookup"><span data-stu-id="deb6c-765">PCase</span></span>
<span data-ttu-id="deb6c-766">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-766">**Description:**</span></span>  
<span data-ttu-id="deb6c-767">PCase 函式會將字串中每個空格分隔之單字的第一個字元轉換為大寫，並將其他所有字元轉換為小寫。</span><span class="sxs-lookup"><span data-stu-id="deb6c-767">The PCase function converts the first character of each space delimited word in a string to upper case, and all other characters are converted to lower case.</span></span>

<span data-ttu-id="deb6c-768">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="deb6c-769">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-769">**Remarks:**</span></span>

* <span data-ttu-id="deb6c-770">此函式目前未提供可轉換全大寫文字 (例如縮略字) 的正確大小寫。</span><span class="sxs-lookup"><span data-stu-id="deb6c-770">This function does not currently provide proper casing to convert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="deb6c-771">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="deb6c-772">傳回 "test"。</span><span class="sxs-lookup"><span data-stu-id="deb6c-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="deb6c-773">傳回 "Test"</span><span class="sxs-lookup"><span data-stu-id="deb6c-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="deb6c-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="deb6c-774">RandomNum</span></span>
<span data-ttu-id="deb6c-775">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-775">**Description:**</span></span>  
<span data-ttu-id="deb6c-776">RandomNum 函式會傳回指定區間內的隨機數字。</span><span class="sxs-lookup"><span data-stu-id="deb6c-776">The RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="deb6c-777">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="deb6c-778">start：可識別要產生之隨機值下限的數字</span><span class="sxs-lookup"><span data-stu-id="deb6c-778">start: a number identifying the lower limit of the random value to generate</span></span>
* <span data-ttu-id="deb6c-779">end：可識別要產生之隨機值上限的數字</span><span class="sxs-lookup"><span data-stu-id="deb6c-779">end: a number identifying the upper limit of the random value to generate</span></span>

<span data-ttu-id="deb6c-780">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="deb6c-781">可傳回 734。</span><span class="sxs-lookup"><span data-stu-id="deb6c-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="deb6c-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="deb6c-782">RemoveDuplicates</span></span>
<span data-ttu-id="deb6c-783">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-783">**Description:**</span></span>  
<span data-ttu-id="deb6c-784">RemoveDuplicates 函式會接受多重值的字串，並確定每個值都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="deb6c-784">The RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="deb6c-785">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="deb6c-786">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="deb6c-787">傳回處理過的 proxyAddress 屬性，其中已移除所有重複的值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="deb6c-788">Replace</span><span class="sxs-lookup"><span data-stu-id="deb6c-788">Replace</span></span>
<span data-ttu-id="deb6c-789">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-789">**Description:**</span></span>  
<span data-ttu-id="deb6c-790">Replace 函式會將所有出現的字串取代為另一個字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-790">The Replace function replaces all occurrences of a string to another string.</span></span>

<span data-ttu-id="deb6c-791">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="deb6c-792">string：要取代其值的字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-792">string: A string to replace values in.</span></span>
* <span data-ttu-id="deb6c-793">OldValue：要搜尋並取代的字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-793">OldValue: The string to search for and to replace.</span></span>
* <span data-ttu-id="deb6c-794">NewValue：要取代的字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-794">NewValue: The string to replace to.</span></span>

<span data-ttu-id="deb6c-795">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-795">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-796">這個函式會辨識下列特殊的 Moniker：</span><span class="sxs-lookup"><span data-stu-id="deb6c-796">The function recognizes the following special monikers:</span></span>

* <span data-ttu-id="deb6c-797">\n – 新行</span><span class="sxs-lookup"><span data-stu-id="deb6c-797">\n – New Line</span></span>
* <span data-ttu-id="deb6c-798">\r – 歸位字元</span><span class="sxs-lookup"><span data-stu-id="deb6c-798">\r – Carriage Return</span></span>
* <span data-ttu-id="deb6c-799">\t – 定位字元</span><span class="sxs-lookup"><span data-stu-id="deb6c-799">\t – Tab</span></span>

<span data-ttu-id="deb6c-800">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="deb6c-801">使用逗號和空格來取代 CRLF，並且可產生 "One Microsoft Way, Redmond, WA, USA"</span><span class="sxs-lookup"><span data-stu-id="deb6c-801">Replaces CRLF with a comma and space, and could lead to "One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="deb6c-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="deb6c-802">ReplaceChars</span></span>
<span data-ttu-id="deb6c-803">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-803">**Description:**</span></span>  
<span data-ttu-id="deb6c-804">ReplaceChars 函式會取代 ReplacePattern 字串中找到的所有出現的字元。</span><span class="sxs-lookup"><span data-stu-id="deb6c-804">The ReplaceChars function replaces all occurrences of characters found in the ReplacePattern string.</span></span>

<span data-ttu-id="deb6c-805">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="deb6c-806">string：要取代字元的字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-806">string: A string to replace characters in.</span></span>
* <span data-ttu-id="deb6c-807">ReplacePattern：字串，包含要取代之字元的字典。</span><span class="sxs-lookup"><span data-stu-id="deb6c-807">ReplacePattern: a string containing a dictionary with characters to replace.</span></span>

<span data-ttu-id="deb6c-808">格式為 {source1}:{target1},{source2}:{target2},{sourceN},{targetN}，其中 source 為要尋找的字元，而 target 則為要取代的字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-808">The format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is the character to find and target the string to replace with.</span></span>

<span data-ttu-id="deb6c-809">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-809">**Remarks:**</span></span>

* <span data-ttu-id="deb6c-810">此函式會取得已定義之來源的每個出現項目，並使用目標來取代它們。</span><span class="sxs-lookup"><span data-stu-id="deb6c-810">The function takes each occurrence of defined sources and replaces them with the targets.</span></span>
* <span data-ttu-id="deb6c-811">來源必須是一個 (unicode) 字元。</span><span class="sxs-lookup"><span data-stu-id="deb6c-811">The source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="deb6c-812">來源不能是空字串或超過一個字元 (剖析錯誤)。</span><span class="sxs-lookup"><span data-stu-id="deb6c-812">The source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="deb6c-813">目標可以有多個字元，例如 ö:oe、β:ss。</span><span class="sxs-lookup"><span data-stu-id="deb6c-813">The target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="deb6c-814">目標可以空白，表示應移除此字元。</span><span class="sxs-lookup"><span data-stu-id="deb6c-814">The target can be empty indicating that the character should be removed.</span></span>
* <span data-ttu-id="deb6c-815">來源是區分大小寫且必須完全相符。</span><span class="sxs-lookup"><span data-stu-id="deb6c-815">The source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="deb6c-816">, (逗號) 和 : (冒號) 是保留字元，無法使用這個函式來取代。</span><span class="sxs-lookup"><span data-stu-id="deb6c-816">The , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="deb6c-817">系統會忽略空格和 ReplacePattern 字串中的其他空白字元。</span><span class="sxs-lookup"><span data-stu-id="deb6c-817">Spaces and other white characters in the ReplacePattern string are ignored.</span></span>

<span data-ttu-id="deb6c-818">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="deb6c-819">傳回 Raksmorgas</span><span class="sxs-lookup"><span data-stu-id="deb6c-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="deb6c-820">傳回 "ONeil"，已將單一撇號定義為要移除。</span><span class="sxs-lookup"><span data-stu-id="deb6c-820">Returns "ONeil", the single tick is defined to be removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="deb6c-821">Right</span><span class="sxs-lookup"><span data-stu-id="deb6c-821">Right</span></span>
<span data-ttu-id="deb6c-822">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-822">**Description:**</span></span>  
<span data-ttu-id="deb6c-823">Right 函式會從字串右邊 (結尾處) 傳回指定的字元數。</span><span class="sxs-lookup"><span data-stu-id="deb6c-823">The Right function returns a specified number of characters from the right (end) of a string.</span></span>

<span data-ttu-id="deb6c-824">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="deb6c-825">string：要傳回字元的字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-825">string: the string to return characters from</span></span>
* <span data-ttu-id="deb6c-826">NumChars：數字，可識別要從 string 結尾 (右邊) 傳回的字元數</span><span class="sxs-lookup"><span data-stu-id="deb6c-826">NumChars: a number identifying the number of characters to return from the end (right) of string</span></span>

<span data-ttu-id="deb6c-827">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-827">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-828">會從 string 的最後一個位置傳回 NumChars 個字元。</span><span class="sxs-lookup"><span data-stu-id="deb6c-828">NumChars characters are returned from the last position of string.</span></span>

<span data-ttu-id="deb6c-829">包含 string 中最後 numChars 個字元的字串：</span><span class="sxs-lookup"><span data-stu-id="deb6c-829">A string containing the last numChars characters in string:</span></span>

* <span data-ttu-id="deb6c-830">如果 numChars = 0，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="deb6c-831">如果 numChars < 0，會傳回輸入字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="deb6c-832">如果 string 為 Null，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-832">If string is null, return empty string.</span></span>

<span data-ttu-id="deb6c-833">如果 string 包含的字元數比 numChars 中指定的數目少，即會傳回與 string 完全相同的字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-833">If string contains fewer characters than the number specified in NumChars, a string identical to string is returned.</span></span>

<span data-ttu-id="deb6c-834">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="deb6c-835">傳回 "Doe"。</span><span class="sxs-lookup"><span data-stu-id="deb6c-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="deb6c-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="deb6c-836">RTrim</span></span>
<span data-ttu-id="deb6c-837">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-837">**Description:**</span></span>  
<span data-ttu-id="deb6c-838">RTrim 函式會從字串移除結尾空白字元。</span><span class="sxs-lookup"><span data-stu-id="deb6c-838">The RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="deb6c-839">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="deb6c-840">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="deb6c-841">傳回 "Test"。</span><span class="sxs-lookup"><span data-stu-id="deb6c-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="deb6c-842">選取</span><span class="sxs-lookup"><span data-stu-id="deb6c-842">Select</span></span>
<span data-ttu-id="deb6c-843">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-843">**Description:**</span></span>  
<span data-ttu-id="deb6c-844">在以指定函式為基礎的多重值屬性 (或運算式的輸出) 中處理所有值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="deb6c-845">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="deb6c-846">item：表示多重值屬性中的項目</span><span class="sxs-lookup"><span data-stu-id="deb6c-846">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="deb6c-847">attribute：多重值屬性</span><span class="sxs-lookup"><span data-stu-id="deb6c-847">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="deb6c-848">expression：傳回值集合的運算式</span><span class="sxs-lookup"><span data-stu-id="deb6c-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="deb6c-849">condition：可以在屬性中處理項目的任何函式</span><span class="sxs-lookup"><span data-stu-id="deb6c-849">condition: any function that can process an item in the attribute</span></span>

<span data-ttu-id="deb6c-850">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="deb6c-851">傳回移除連字號 (-) 後，多重值屬性 otherPhone 中所有值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-851">Return all the values in the multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="deb6c-852">Split</span><span class="sxs-lookup"><span data-stu-id="deb6c-852">Split</span></span>
<span data-ttu-id="deb6c-853">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-853">**Description:**</span></span>  
<span data-ttu-id="deb6c-854">Split 函式會接受以分隔符號分隔的字串，並使其成為多重值的字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-854">The Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="deb6c-855">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="deb6c-856">value：以分隔符號字元分隔的字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-856">value: the string with a delimiter character to separate.</span></span>
* <span data-ttu-id="deb6c-857">delimiter：用來做為分隔符號的單一字元。</span><span class="sxs-lookup"><span data-stu-id="deb6c-857">delimiter: single character to be used as the delimiter.</span></span>
* <span data-ttu-id="deb6c-858">limit：可以傳回的值數目上限。</span><span class="sxs-lookup"><span data-stu-id="deb6c-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="deb6c-859">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="deb6c-860">傳回多重值的字串，其中包含 2 個 proxyAddress 屬性可用的元素。</span><span class="sxs-lookup"><span data-stu-id="deb6c-860">Returns a multi-valued string with 2 elements useful for the proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="deb6c-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="deb6c-861">StringFromGuid</span></span>
<span data-ttu-id="deb6c-862">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-862">**Description:**</span></span>  
<span data-ttu-id="deb6c-863">StringFromGuid 函式會接受二進位 GUID，並將其轉換為字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-863">The StringFromGuid function takes a binary GUID and converts it to a string</span></span>

<span data-ttu-id="deb6c-864">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="deb6c-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="deb6c-865">StringFromSid</span></span>
<span data-ttu-id="deb6c-866">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-866">**Description:**</span></span>  
<span data-ttu-id="deb6c-867">StringFromSid 函式會將包含安全性識別碼的位元組陣列轉換為字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-867">The StringFromSid function converts a byte array containing a security identifier to a string.</span></span>

<span data-ttu-id="deb6c-868">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="deb6c-869">Switch</span><span class="sxs-lookup"><span data-stu-id="deb6c-869">Switch</span></span>
<span data-ttu-id="deb6c-870">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-870">**Description:**</span></span>  
<span data-ttu-id="deb6c-871">Switch 函式可用來根據評估的條件傳回單一值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-871">The Switch function is used to return a single value based on evaluated conditions.</span></span>

<span data-ttu-id="deb6c-872">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="deb6c-873">expr：您想要評估的 Variant 運算式。</span><span class="sxs-lookup"><span data-stu-id="deb6c-873">expr: Variant expression you want to evaluate.</span></span>
* <span data-ttu-id="deb6c-874">value：當對應的運算式為 True 時要傳回的值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-874">value: Value to be returned if the corresponding expression is True.</span></span>

<span data-ttu-id="deb6c-875">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-875">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-876">Switch 函式引數清單是由運算式和值的配對所組成。</span><span class="sxs-lookup"><span data-stu-id="deb6c-876">The Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="deb6c-877">運算式是以從左到右的方式進行評估，並會傳回與要評估為 True 的第一個運算式相關聯的值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-877">The expressions are evaluated from left to right, and the value associated with the first expression to evaluate to True is returned.</span></span> <span data-ttu-id="deb6c-878">如果未正確配對組件，就會發生執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="deb6c-878">If the parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="deb6c-879">例如，如果 expr1 為 True，Switch 就會傳回 value1。</span><span class="sxs-lookup"><span data-stu-id="deb6c-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="deb6c-880">如果 expr-1 為 False，但 expr-2 為 True，Switch 就會傳回 value-2，依此類推。</span><span class="sxs-lookup"><span data-stu-id="deb6c-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="deb6c-881">在下列情況下，參數會傳回 Nothing︰</span><span class="sxs-lookup"><span data-stu-id="deb6c-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="deb6c-882">沒有任何運算式為 True。</span><span class="sxs-lookup"><span data-stu-id="deb6c-882">None of the expressions are True.</span></span>
* <span data-ttu-id="deb6c-883">第一個 True 運算式具有對應值 Null。</span><span class="sxs-lookup"><span data-stu-id="deb6c-883">The first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="deb6c-884">雖然 Switch 只會傳回其中一個運算式，但它會評估所有運算式。</span><span class="sxs-lookup"><span data-stu-id="deb6c-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="deb6c-885">基於這個理由，您應該留意非預期的副作用。</span><span class="sxs-lookup"><span data-stu-id="deb6c-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="deb6c-886">例如，如果任何運算式的評估會產生除以零的錯誤，就會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="deb6c-886">For example, if the evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="deb6c-887">Value 也可以是會傳回自訂字串的 Error 函式。</span><span class="sxs-lookup"><span data-stu-id="deb6c-887">Value can also be the Error function, which would return a custom string.</span></span>

<span data-ttu-id="deb6c-888">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="deb6c-889">傳回一些主要城市中所使用的語言，否則會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="deb6c-889">Returns the language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="deb6c-890">Trim</span><span class="sxs-lookup"><span data-stu-id="deb6c-890">Trim</span></span>
<span data-ttu-id="deb6c-891">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-891">**Description:**</span></span>  
<span data-ttu-id="deb6c-892">Trim 函式會從字串移除開頭和結尾的空白字元。</span><span class="sxs-lookup"><span data-stu-id="deb6c-892">The Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="deb6c-893">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="deb6c-894">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="deb6c-895">傳回 "test"。</span><span class="sxs-lookup"><span data-stu-id="deb6c-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="deb6c-896">會移除 proxyAddress 屬性中每個值的開頭和結尾空格。</span><span class="sxs-lookup"><span data-stu-id="deb6c-896">Removes leading and trailing spaces for each value in the proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="deb6c-897">UCase</span><span class="sxs-lookup"><span data-stu-id="deb6c-897">UCase</span></span>
<span data-ttu-id="deb6c-898">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-898">**Description:**</span></span>  
<span data-ttu-id="deb6c-899">UCase 函式會將字串中的所有字元轉換為大寫。</span><span class="sxs-lookup"><span data-stu-id="deb6c-899">The UCase function converts all characters in a string to upper case.</span></span>

<span data-ttu-id="deb6c-900">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="deb6c-901">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="deb6c-902">傳回 "test"。</span><span class="sxs-lookup"><span data-stu-id="deb6c-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="deb6c-903">Where</span><span class="sxs-lookup"><span data-stu-id="deb6c-903">Where</span></span>

<span data-ttu-id="deb6c-904">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-904">**Description:**</span></span>  
<span data-ttu-id="deb6c-905">傳回以指定條件為基礎的多重值屬性 (或運算式的輸出) 的值子集。</span><span class="sxs-lookup"><span data-stu-id="deb6c-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="deb6c-906">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="deb6c-907">item：表示多重值屬性中的項目</span><span class="sxs-lookup"><span data-stu-id="deb6c-907">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="deb6c-908">attribute：多重值屬性</span><span class="sxs-lookup"><span data-stu-id="deb6c-908">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="deb6c-909">condition：可評估為 True 或 False 的任何運算式</span><span class="sxs-lookup"><span data-stu-id="deb6c-909">condition: any expression that can be evaluated to true or false</span></span>
* <span data-ttu-id="deb6c-910">expression：傳回值集合的運算式</span><span class="sxs-lookup"><span data-stu-id="deb6c-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="deb6c-911">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="deb6c-912">傳回未過期的多重值屬性 userCertificate 中的憑證值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-912">Return the certificate values in the multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="deb6c-913">With</span><span class="sxs-lookup"><span data-stu-id="deb6c-913">With</span></span>
<span data-ttu-id="deb6c-914">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-914">**Description:**</span></span>  
<span data-ttu-id="deb6c-915">With 函式可以簡化複雜的運算式，使用變數代表在複雜運算式中會出現一或多次的子運算式。</span><span class="sxs-lookup"><span data-stu-id="deb6c-915">The With function provides a way to simplify a complex expression by using a variable to represent a subexpression which appears one or more times in the complex expression.</span></span>

<span data-ttu-id="deb6c-916">**語法：**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="deb6c-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="deb6c-917">variable：代表子運算式。</span><span class="sxs-lookup"><span data-stu-id="deb6c-917">variable: Represents the subexpression.</span></span>
* <span data-ttu-id="deb6c-918">subExpression：變數代表的子運算式。</span><span class="sxs-lookup"><span data-stu-id="deb6c-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="deb6c-919">complexExpression：複雜的運算式。</span><span class="sxs-lookup"><span data-stu-id="deb6c-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="deb6c-920">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="deb6c-921">在功能上等同於：</span><span class="sxs-lookup"><span data-stu-id="deb6c-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="deb6c-922">只傳回 UserCertificate 屬性中未過期的憑證值。</span><span class="sxs-lookup"><span data-stu-id="deb6c-922">Which returns only unexpired certificate values in the userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="deb6c-923">Word</span><span class="sxs-lookup"><span data-stu-id="deb6c-923">Word</span></span>
<span data-ttu-id="deb6c-924">**說明：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-924">**Description:**</span></span>  
<span data-ttu-id="deb6c-925">Word 函式會根據描述要使用之分隔符號及要傳回之字數的參數，傳回字串內含的單字。</span><span class="sxs-lookup"><span data-stu-id="deb6c-925">The Word function returns a word contained within a string, based on parameters describing the delimiters to use and the word number to return.</span></span>

<span data-ttu-id="deb6c-926">**語法：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="deb6c-927">string：要傳回單字的字串</span><span class="sxs-lookup"><span data-stu-id="deb6c-927">string: the string to return a word from.</span></span>
* <span data-ttu-id="deb6c-928">WordNumber：一個數字，用於識別可傳回的字數。</span><span class="sxs-lookup"><span data-stu-id="deb6c-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="deb6c-929">delimiters：字串，表示應用來識別單字的分隔符號</span><span class="sxs-lookup"><span data-stu-id="deb6c-929">delimiters: a string representing the delimiter(s) that should be used to identify words</span></span>

<span data-ttu-id="deb6c-930">**備註：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-930">**Remarks:**</span></span>  
<span data-ttu-id="deb6c-931">string 內以 delimiters 其中一個字元來分隔之字元的每個字串，都會被識別為單字：</span><span class="sxs-lookup"><span data-stu-id="deb6c-931">Each string of characters in string separated by the one of the characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="deb6c-932">如果 number < 1，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="deb6c-933">如果 string 為 Null，會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="deb6c-934">如果 string 所含的字數少於 number 個字，或者 string 不包含任何 delimeters 所識別的單字，就會傳回空字串。</span><span class="sxs-lookup"><span data-stu-id="deb6c-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="deb6c-935">**範例：**</span><span class="sxs-lookup"><span data-stu-id="deb6c-935">**Example:**</span></span>  
`Word("The quick brown fox",3," ")`  
<span data-ttu-id="deb6c-936">傳回 "brown"</span><span class="sxs-lookup"><span data-stu-id="deb6c-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="deb6c-937">會傳回 "has"</span><span class="sxs-lookup"><span data-stu-id="deb6c-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="deb6c-938">其他資源</span><span class="sxs-lookup"><span data-stu-id="deb6c-938">Additional Resources</span></span>
* [<span data-ttu-id="deb6c-939">了解宣告式佈建運算式</span><span class="sxs-lookup"><span data-stu-id="deb6c-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="deb6c-940">Azure AD Connect 同步處理：自訂同步處理選項</span><span class="sxs-lookup"><span data-stu-id="deb6c-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="deb6c-941">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="deb6c-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

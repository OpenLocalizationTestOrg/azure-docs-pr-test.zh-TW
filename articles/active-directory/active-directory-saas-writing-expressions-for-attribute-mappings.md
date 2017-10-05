---
title: "在 Azure Active Directory 中撰寫屬性對應的運算式 | Microsoft Docs"
description: "了解在 Azure Active Directory 中自動化佈建 SaaS 應用程式物件的期間，如何使用運算式對應將屬性值轉換成可接受的格式。"
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
ms.openlocfilehash: c944a355c07b96c27dcdd477f625638284eabdf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a><span data-ttu-id="d4362-103">在 Azure Active Directory 中撰寫屬性對應的運算式</span><span class="sxs-lookup"><span data-stu-id="d4362-103">Writing Expressions for Attribute Mappings in Azure Active Directory</span></span>
<span data-ttu-id="d4362-104">當您設定佈建到 SaaS 應用程式時，您可以指定的其中一種屬性對應類型是運算式對應。</span><span class="sxs-lookup"><span data-stu-id="d4362-104">When you configure provisioning to a SaaS application, one of the types of attribute mappings that you can specify is an expression mapping.</span></span> <span data-ttu-id="d4362-105">您必須撰寫類似指令碼的運算式，以便讓您將使用者的資料轉換成 SaaS 應用程式更能接受的格式。</span><span class="sxs-lookup"><span data-stu-id="d4362-105">For these, you must write a script-like expression that allows you to transform your users’ data into formats that are more acceptable for the SaaS application.</span></span>

## <a name="syntax-overview"></a><span data-ttu-id="d4362-106">語法概觀</span><span class="sxs-lookup"><span data-stu-id="d4362-106">Syntax Overview</span></span>
<span data-ttu-id="d4362-107">屬性對應的運算式語法是 Visual Basic for Applications (VBA) 函式。</span><span class="sxs-lookup"><span data-stu-id="d4362-107">The syntax for Expressions for Attribute Mappings is reminiscent of Visual Basic for Applications (VBA) functions.</span></span>

* <span data-ttu-id="d4362-108">整個運算式必須以函式定義，由函式名稱後面接著以括號括住的引數組成：</span><span class="sxs-lookup"><span data-stu-id="d4362-108">The entire expression must be defined in terms of functions, which consist of a name followed by arguments in parentheses:</span></span> <br><span data-ttu-id="d4362-109">
  *FunctionName(<<argument 1>>,<<argument N>>)*</span><span class="sxs-lookup"><span data-stu-id="d4362-109">
*FunctionName(<<argument 1>>,<<argument N>>)*</span></span>
* <span data-ttu-id="d4362-110">您可以在函式內互相巢狀函式。</span><span class="sxs-lookup"><span data-stu-id="d4362-110">You may nest functions within each other.</span></span> <span data-ttu-id="d4362-111">例如：</span><span class="sxs-lookup"><span data-stu-id="d4362-111">For example:</span></span> <br> <span data-ttu-id="d4362-112">*FunctionOne(FunctionTwo(<<argument1>>))*</span><span class="sxs-lookup"><span data-stu-id="d4362-112">*FunctionOne(FunctionTwo(<<argument1>>))*</span></span>
* <span data-ttu-id="d4362-113">您可以將三種不同類型的引數傳入函式：</span><span class="sxs-lookup"><span data-stu-id="d4362-113">You can pass three different types of arguments into functions:</span></span>
  
  1. <span data-ttu-id="d4362-114">屬性，必須以方括弧括住。</span><span class="sxs-lookup"><span data-stu-id="d4362-114">Attributes, which must be enclosed in square square brackets.</span></span> <span data-ttu-id="d4362-115">例如：[attributeName]</span><span class="sxs-lookup"><span data-stu-id="d4362-115">For example: [attributeName]</span></span>
  2. <span data-ttu-id="d4362-116">字串常數，必須以雙引號括住。</span><span class="sxs-lookup"><span data-stu-id="d4362-116">String constants, which must be enclosed in double quotes.</span></span> <span data-ttu-id="d4362-117">例如："United States"</span><span class="sxs-lookup"><span data-stu-id="d4362-117">For example: "United States"</span></span>
  3. <span data-ttu-id="d4362-118">其他函式。</span><span class="sxs-lookup"><span data-stu-id="d4362-118">Other Functions.</span></span> <span data-ttu-id="d4362-119">例如：FunctionOne(<<argument1>>, FunctionTwo(<<argument2>>))</span><span class="sxs-lookup"><span data-stu-id="d4362-119">For example: FunctionOne(<<argument1>>, FunctionTwo(<<argument2>>))</span></span>
* <span data-ttu-id="d4362-120">對於字串常數，如果您在字串中需要反斜線 ( \ ) 或引號 ( " ) ，則必須使用反斜線 ( \ ) 符號逸出。</span><span class="sxs-lookup"><span data-stu-id="d4362-120">For string constants, if you need a backslash ( \ ) or quotation mark ( " ) in the string, it must be escaped with the backslash ( \ ) symbol.</span></span> <span data-ttu-id="d4362-121">例如："公司名稱：\"Contoso\""</span><span class="sxs-lookup"><span data-stu-id="d4362-121">For example: "Company name: \"Contoso\""</span></span>

## <a name="list-of-functions"></a><span data-ttu-id="d4362-122">函式的清單</span><span class="sxs-lookup"><span data-stu-id="d4362-122">List of Functions</span></span>
<span data-ttu-id="d4362-123">[Append](#append) &nbsp;&nbsp;&nbsp;&nbsp; [FormatDateTime](#formatdatetime) &nbsp;&nbsp;&nbsp;&nbsp; [Join](#join) &nbsp;&nbsp;&nbsp;&nbsp; [Mid](#mid) &nbsp;&nbsp;&nbsp;&nbsp; [Not](#not) &nbsp;&nbsp;&nbsp;&nbsp; [將](#replace) &nbsp;&nbsp;&nbsp;&nbsp; [StripSpaces](#stripspaces) &nbsp;&nbsp;&nbsp;&nbsp; [Switch](#switch)</span><span class="sxs-lookup"><span data-stu-id="d4362-123">[Append](#append) &nbsp;&nbsp;&nbsp;&nbsp; [FormatDateTime](#formatdatetime) &nbsp;&nbsp;&nbsp;&nbsp; [Join](#join) &nbsp;&nbsp;&nbsp;&nbsp; [Mid](#mid) &nbsp;&nbsp;&nbsp;&nbsp; [Not](#not) &nbsp;&nbsp;&nbsp;&nbsp; [Replace](#replace) &nbsp;&nbsp;&nbsp;&nbsp; [StripSpaces](#stripspaces) &nbsp;&nbsp;&nbsp;&nbsp; [Switch](#switch)</span></span>

- - -
### <a name="append"></a><span data-ttu-id="d4362-124">Append</span><span class="sxs-lookup"><span data-stu-id="d4362-124">Append</span></span>
<span data-ttu-id="d4362-125">**函式：**</span><span class="sxs-lookup"><span data-stu-id="d4362-125">**Function:**</span></span><br> <span data-ttu-id="d4362-126">Append(source, suffix)</span><span class="sxs-lookup"><span data-stu-id="d4362-126">Append(source, suffix)</span></span>

<span data-ttu-id="d4362-127">**說明：**</span><span class="sxs-lookup"><span data-stu-id="d4362-127">**Description:**</span></span><br> <span data-ttu-id="d4362-128">取出 source 字串值並在結尾附加尾碼。</span><span class="sxs-lookup"><span data-stu-id="d4362-128">Takes a source string value and appends the suffix to the end of it.</span></span>

<span data-ttu-id="d4362-129">**參數：**</span><span class="sxs-lookup"><span data-stu-id="d4362-129">**Parameters:**</span></span><br> 

| <span data-ttu-id="d4362-130">名稱</span><span class="sxs-lookup"><span data-stu-id="d4362-130">Name</span></span> | <span data-ttu-id="d4362-131">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="d4362-131">Required/ Repeating</span></span> | <span data-ttu-id="d4362-132">型別</span><span class="sxs-lookup"><span data-stu-id="d4362-132">Type</span></span> | <span data-ttu-id="d4362-133">注意事項</span><span class="sxs-lookup"><span data-stu-id="d4362-133">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4362-134">**source**</span><span class="sxs-lookup"><span data-stu-id="d4362-134">**source**</span></span> |<span data-ttu-id="d4362-135">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-135">Required</span></span> |<span data-ttu-id="d4362-136">String</span><span class="sxs-lookup"><span data-stu-id="d4362-136">String</span></span> |<span data-ttu-id="d4362-137">通常為 source 物件的屬性名稱</span><span class="sxs-lookup"><span data-stu-id="d4362-137">Usually name of the attribute from the source object</span></span> |
| <span data-ttu-id="d4362-138">**suffix**</span><span class="sxs-lookup"><span data-stu-id="d4362-138">**suffix**</span></span> |<span data-ttu-id="d4362-139">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-139">Required</span></span> |<span data-ttu-id="d4362-140">String</span><span class="sxs-lookup"><span data-stu-id="d4362-140">String</span></span> |<span data-ttu-id="d4362-141">您想要附加至 source 值結尾的字串。</span><span class="sxs-lookup"><span data-stu-id="d4362-141">The string that you want to append to the end of the source value.</span></span> |

- - -
### <a name="formatdatetime"></a><span data-ttu-id="d4362-142">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="d4362-142">FormatDateTime</span></span>
<span data-ttu-id="d4362-143">**函式：**</span><span class="sxs-lookup"><span data-stu-id="d4362-143">**Function:**</span></span><br> <span data-ttu-id="d4362-144">FormatDateTime(source, inputFormat, outputFormat)</span><span class="sxs-lookup"><span data-stu-id="d4362-144">FormatDateTime(source, inputFormat, outputFormat)</span></span>

<span data-ttu-id="d4362-145">**說明：**</span><span class="sxs-lookup"><span data-stu-id="d4362-145">**Description:**</span></span><br> <span data-ttu-id="d4362-146">從一種格式取出日期字串，並將它轉換成不同的格式。</span><span class="sxs-lookup"><span data-stu-id="d4362-146">Takes a date string from one format and converts it into a different format.</span></span>

<span data-ttu-id="d4362-147">**參數：**</span><span class="sxs-lookup"><span data-stu-id="d4362-147">**Parameters:**</span></span><br> 

| <span data-ttu-id="d4362-148">名稱</span><span class="sxs-lookup"><span data-stu-id="d4362-148">Name</span></span> | <span data-ttu-id="d4362-149">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="d4362-149">Required/ Repeating</span></span> | <span data-ttu-id="d4362-150">型別</span><span class="sxs-lookup"><span data-stu-id="d4362-150">Type</span></span> | <span data-ttu-id="d4362-151">注意事項</span><span class="sxs-lookup"><span data-stu-id="d4362-151">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4362-152">**source**</span><span class="sxs-lookup"><span data-stu-id="d4362-152">**source**</span></span> |<span data-ttu-id="d4362-153">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-153">Required</span></span> |<span data-ttu-id="d4362-154">String</span><span class="sxs-lookup"><span data-stu-id="d4362-154">String</span></span> |<span data-ttu-id="d4362-155">通常為 source 物件的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="d4362-155">Usually name of the attribute from the source object.</span></span> |
| <span data-ttu-id="d4362-156">**inputFormat**</span><span class="sxs-lookup"><span data-stu-id="d4362-156">**inputFormat**</span></span> |<span data-ttu-id="d4362-157">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-157">Required</span></span> |<span data-ttu-id="d4362-158">String</span><span class="sxs-lookup"><span data-stu-id="d4362-158">String</span></span> |<span data-ttu-id="d4362-159">source 值的預期格式。</span><span class="sxs-lookup"><span data-stu-id="d4362-159">Expected format of the source value.</span></span> <span data-ttu-id="d4362-160">如需支援的格式，請參閱 [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d4362-160">For supported formats, see [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx).</span></span> |
| <span data-ttu-id="d4362-161">**outputFormat**</span><span class="sxs-lookup"><span data-stu-id="d4362-161">**outputFormat**</span></span> |<span data-ttu-id="d4362-162">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-162">Required</span></span> |<span data-ttu-id="d4362-163">String</span><span class="sxs-lookup"><span data-stu-id="d4362-163">String</span></span> |<span data-ttu-id="d4362-164">輸出日期的格式。</span><span class="sxs-lookup"><span data-stu-id="d4362-164">Format of the output date.</span></span> |

- - -
### <a name="join"></a><span data-ttu-id="d4362-165">Join</span><span class="sxs-lookup"><span data-stu-id="d4362-165">Join</span></span>
<span data-ttu-id="d4362-166">**函式：**</span><span class="sxs-lookup"><span data-stu-id="d4362-166">**Function:**</span></span><br> <span data-ttu-id="d4362-167">Join(separator, source1, source2, …)</span><span class="sxs-lookup"><span data-stu-id="d4362-167">Join(separator, source1, source2, …)</span></span>

<span data-ttu-id="d4362-168">**說明：**</span><span class="sxs-lookup"><span data-stu-id="d4362-168">**Description:**</span></span><br> <span data-ttu-id="d4362-169">Join() 類似 Append()，不過前者可以將多個 **source** 字串值合併成單一字串，且每個值會以 **separator** 字串分隔。</span><span class="sxs-lookup"><span data-stu-id="d4362-169">Join() is similar to Append(), except that it can combine multiple **source** string values into a single string, and each value will be separated by a **separator** string.</span></span>

<span data-ttu-id="d4362-170">如果其中一個 source 值是多重值屬性，則該屬性中的每個值會結合在一起，並以分隔符號值分隔。</span><span class="sxs-lookup"><span data-stu-id="d4362-170">If one of the source values is a multi-value attribute, then every value in that attribute will be joined together, separated the separator value.</span></span>

<span data-ttu-id="d4362-171">**參數：**</span><span class="sxs-lookup"><span data-stu-id="d4362-171">**Parameters:**</span></span><br> 

| <span data-ttu-id="d4362-172">名稱</span><span class="sxs-lookup"><span data-stu-id="d4362-172">Name</span></span> | <span data-ttu-id="d4362-173">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="d4362-173">Required/ Repeating</span></span> | <span data-ttu-id="d4362-174">型別</span><span class="sxs-lookup"><span data-stu-id="d4362-174">Type</span></span> | <span data-ttu-id="d4362-175">注意事項</span><span class="sxs-lookup"><span data-stu-id="d4362-175">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4362-176">**separator**</span><span class="sxs-lookup"><span data-stu-id="d4362-176">**separator**</span></span> |<span data-ttu-id="d4362-177">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-177">Required</span></span> |<span data-ttu-id="d4362-178">String</span><span class="sxs-lookup"><span data-stu-id="d4362-178">String</span></span> |<span data-ttu-id="d4362-179">用來分隔串連成一個字串的 source 值的字串。</span><span class="sxs-lookup"><span data-stu-id="d4362-179">String used to separate source values when they are concatenated into one string.</span></span> <span data-ttu-id="d4362-180">如果不需要分隔符號，可以是 ""。</span><span class="sxs-lookup"><span data-stu-id="d4362-180">Can be "" if no separator is required.</span></span> |
| <span data-ttu-id="d4362-181">**source1  …</span><span class="sxs-lookup"><span data-stu-id="d4362-181">**source1  …</span></span> <span data-ttu-id="d4362-182">sourceN **</span><span class="sxs-lookup"><span data-stu-id="d4362-182">sourceN **</span></span> |<span data-ttu-id="d4362-183">必要，變動次數</span><span class="sxs-lookup"><span data-stu-id="d4362-183">Required, variable-number of times</span></span> |<span data-ttu-id="d4362-184">String</span><span class="sxs-lookup"><span data-stu-id="d4362-184">String</span></span> |<span data-ttu-id="d4362-185">要聯結在一起的字串值。</span><span class="sxs-lookup"><span data-stu-id="d4362-185">String values to be joined together.</span></span> |

- - -
### <a name="mid"></a><span data-ttu-id="d4362-186">Mid</span><span class="sxs-lookup"><span data-stu-id="d4362-186">Mid</span></span>
<span data-ttu-id="d4362-187">**函式：**</span><span class="sxs-lookup"><span data-stu-id="d4362-187">**Function:**</span></span><br> <span data-ttu-id="d4362-188">Mid(source, start, length)</span><span class="sxs-lookup"><span data-stu-id="d4362-188">Mid(source, start, length)</span></span>

<span data-ttu-id="d4362-189">**說明：**</span><span class="sxs-lookup"><span data-stu-id="d4362-189">**Description:**</span></span><br> <span data-ttu-id="d4362-190">傳回 source 值的子字串。</span><span class="sxs-lookup"><span data-stu-id="d4362-190">Returns a substring of the source value.</span></span> <span data-ttu-id="d4362-191">子字串是只包含 source 字串某些字元的字串。</span><span class="sxs-lookup"><span data-stu-id="d4362-191">A substring is a string that contains only some of the characters from the source string.</span></span>

<span data-ttu-id="d4362-192">**參數：**</span><span class="sxs-lookup"><span data-stu-id="d4362-192">**Parameters:**</span></span><br> 

| <span data-ttu-id="d4362-193">名稱</span><span class="sxs-lookup"><span data-stu-id="d4362-193">Name</span></span> | <span data-ttu-id="d4362-194">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="d4362-194">Required/ Repeating</span></span> | <span data-ttu-id="d4362-195">型別</span><span class="sxs-lookup"><span data-stu-id="d4362-195">Type</span></span> | <span data-ttu-id="d4362-196">注意事項</span><span class="sxs-lookup"><span data-stu-id="d4362-196">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4362-197">**source**</span><span class="sxs-lookup"><span data-stu-id="d4362-197">**source**</span></span> |<span data-ttu-id="d4362-198">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-198">Required</span></span> |<span data-ttu-id="d4362-199">String</span><span class="sxs-lookup"><span data-stu-id="d4362-199">String</span></span> |<span data-ttu-id="d4362-200">通常為屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="d4362-200">Usually name of the attribute.</span></span> |
| <span data-ttu-id="d4362-201">**start**</span><span class="sxs-lookup"><span data-stu-id="d4362-201">**start**</span></span> |<span data-ttu-id="d4362-202">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-202">Required</span></span> |<span data-ttu-id="d4362-203">integer</span><span class="sxs-lookup"><span data-stu-id="d4362-203">integer</span></span> |<span data-ttu-id="d4362-204">子字串在 **source** 字串中起始位置的索引。</span><span class="sxs-lookup"><span data-stu-id="d4362-204">Index in the **source** string where substring should start.</span></span> <span data-ttu-id="d4362-205">字串第一個字元的索引為 1，第二個字元的索引為 2，依此類推。</span><span class="sxs-lookup"><span data-stu-id="d4362-205">First character in the string will have index of 1, second character will have index 2, and so on.</span></span> |
| <span data-ttu-id="d4362-206">**length**</span><span class="sxs-lookup"><span data-stu-id="d4362-206">**length**</span></span> |<span data-ttu-id="d4362-207">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-207">Required</span></span> |<span data-ttu-id="d4362-208">integer</span><span class="sxs-lookup"><span data-stu-id="d4362-208">integer</span></span> |<span data-ttu-id="d4362-209">子字串的長度。</span><span class="sxs-lookup"><span data-stu-id="d4362-209">Length of the substring.</span></span> <span data-ttu-id="d4362-210">如果長度超出 **source** 字串結尾，函式會傳回從 **start** 索引一直到 **source** 字串結尾的子字串。</span><span class="sxs-lookup"><span data-stu-id="d4362-210">If length ends outside the **source** string, function will return substring from **start** index till end of **source** string.</span></span> |

- - -
### <a name="not"></a><span data-ttu-id="d4362-211">否</span><span class="sxs-lookup"><span data-stu-id="d4362-211">Not</span></span>
<span data-ttu-id="d4362-212">**函式：**</span><span class="sxs-lookup"><span data-stu-id="d4362-212">**Function:**</span></span><br> <span data-ttu-id="d4362-213">Not(source)</span><span class="sxs-lookup"><span data-stu-id="d4362-213">Not(source)</span></span>

<span data-ttu-id="d4362-214">**說明：**</span><span class="sxs-lookup"><span data-stu-id="d4362-214">**Description:**</span></span><br> <span data-ttu-id="d4362-215">翻轉 **source** 的布林值。</span><span class="sxs-lookup"><span data-stu-id="d4362-215">Flips the boolean value of the **source**.</span></span> <span data-ttu-id="d4362-216">如果 **source** 值為 "*True*"，則傳回 "*False*"。</span><span class="sxs-lookup"><span data-stu-id="d4362-216">If **source** value is "*True*", returns "*False*".</span></span> <span data-ttu-id="d4362-217">反之則傳回 "*True*"。</span><span class="sxs-lookup"><span data-stu-id="d4362-217">Otherwise, returns "*True*".</span></span>

<span data-ttu-id="d4362-218">**參數：**</span><span class="sxs-lookup"><span data-stu-id="d4362-218">**Parameters:**</span></span><br> 

| <span data-ttu-id="d4362-219">名稱</span><span class="sxs-lookup"><span data-stu-id="d4362-219">Name</span></span> | <span data-ttu-id="d4362-220">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="d4362-220">Required/ Repeating</span></span> | <span data-ttu-id="d4362-221">型別</span><span class="sxs-lookup"><span data-stu-id="d4362-221">Type</span></span> | <span data-ttu-id="d4362-222">注意事項</span><span class="sxs-lookup"><span data-stu-id="d4362-222">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4362-223">**source**</span><span class="sxs-lookup"><span data-stu-id="d4362-223">**source**</span></span> |<span data-ttu-id="d4362-224">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-224">Required</span></span> |<span data-ttu-id="d4362-225">Boolean String</span><span class="sxs-lookup"><span data-stu-id="d4362-225">Boolean String</span></span> |<span data-ttu-id="d4362-226">預期的 **source** 值為 "True" 或 "False"。</span><span class="sxs-lookup"><span data-stu-id="d4362-226">Expected **source** values are "True" or "False"..</span></span> |

- - -
### <a name="replace"></a><span data-ttu-id="d4362-227">將</span><span class="sxs-lookup"><span data-stu-id="d4362-227">Replace</span></span>
<span data-ttu-id="d4362-228">**函式：**</span><span class="sxs-lookup"><span data-stu-id="d4362-228">**Function:**</span></span><br> <span data-ttu-id="d4362-229">ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)</span><span class="sxs-lookup"><span data-stu-id="d4362-229">ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)</span></span>

<span data-ttu-id="d4362-230">**說明：**</span><span class="sxs-lookup"><span data-stu-id="d4362-230">**Description:**</span></span><br>
<span data-ttu-id="d4362-231">取代字串內的值。</span><span class="sxs-lookup"><span data-stu-id="d4362-231">Replaces values within a string.</span></span> <span data-ttu-id="d4362-232">根據提供的參數而以不同的方式運作：</span><span class="sxs-lookup"><span data-stu-id="d4362-232">It works differently depending on the parameters provided:</span></span>

* <span data-ttu-id="d4362-233">提供 **oldValue** 和 **replacementValue** 時：</span><span class="sxs-lookup"><span data-stu-id="d4362-233">When **oldValue** and **replacementValue** are provided:</span></span>
  
  * <span data-ttu-id="d4362-234">以 replacementValue 取代 source 中所有的 oldValue 項目</span><span class="sxs-lookup"><span data-stu-id="d4362-234">Replaces all occurrences of oldValue in the source  with replacementValue</span></span>
* <span data-ttu-id="d4362-235">提供 **oldValue** 和 **template** 時：</span><span class="sxs-lookup"><span data-stu-id="d4362-235">When **oldValue** and **template** are provided:</span></span>
  
  * <span data-ttu-id="d4362-236">以 **source** 值取代 **template** 中所有的 **oldValue** 項目</span><span class="sxs-lookup"><span data-stu-id="d4362-236">Replaces all occurrences of the **oldValue** in the **template** with the **source** value</span></span>
* <span data-ttu-id="d4362-237">提供 **oldValueRegexPattern**、**oldValueRegexGroupName**、**replacementValue** 時：</span><span class="sxs-lookup"><span data-stu-id="d4362-237">When **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementValue** are provided:</span></span>
  
  * <span data-ttu-id="d4362-238">以 replacementValue 取代 source 字串中符合 oldValueRegexPattern 的所有值</span><span class="sxs-lookup"><span data-stu-id="d4362-238">Replaces all values matching oldValueRegexPattern in the source string with replacementValue</span></span>
* <span data-ttu-id="d4362-239">提供 **oldValueRegexPattern**、**oldValueRegexGroupName**、**replacementPropertyName** 時：</span><span class="sxs-lookup"><span data-stu-id="d4362-239">When **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementPropertyName** are provided:</span></span>
  
  * <span data-ttu-id="d4362-240">如果 **source** 有值，則傳回 **source**</span><span class="sxs-lookup"><span data-stu-id="d4362-240">If **source** has value, **source** is returned</span></span>
  * <span data-ttu-id="d4362-241">如果 **source** 沒有值，則使用 **oldValueRegexPattern** 和 **oldValueRegexGroupName** 從有 **replacementPropertyName** 的屬性擷取取代值。</span><span class="sxs-lookup"><span data-stu-id="d4362-241">If **source** has no value, uses **oldValueRegexPattern** and **oldValueRegexGroupName** to extract replacement value from the property with **replacementPropertyName**.</span></span> <span data-ttu-id="d4362-242">結果會傳回取代值</span><span class="sxs-lookup"><span data-stu-id="d4362-242">Replacement value is returned as the result</span></span>

<span data-ttu-id="d4362-243">**參數：**</span><span class="sxs-lookup"><span data-stu-id="d4362-243">**Parameters:**</span></span><br> 

| <span data-ttu-id="d4362-244">名稱</span><span class="sxs-lookup"><span data-stu-id="d4362-244">Name</span></span> | <span data-ttu-id="d4362-245">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="d4362-245">Required/ Repeating</span></span> | <span data-ttu-id="d4362-246">型別</span><span class="sxs-lookup"><span data-stu-id="d4362-246">Type</span></span> | <span data-ttu-id="d4362-247">注意事項</span><span class="sxs-lookup"><span data-stu-id="d4362-247">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4362-248">**source**</span><span class="sxs-lookup"><span data-stu-id="d4362-248">**source**</span></span> |<span data-ttu-id="d4362-249">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-249">Required</span></span> |<span data-ttu-id="d4362-250">String</span><span class="sxs-lookup"><span data-stu-id="d4362-250">String</span></span> |<span data-ttu-id="d4362-251">通常為 source 物件的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="d4362-251">Usually name of the attribute from the source object.</span></span> |
| <span data-ttu-id="d4362-252">**oldValue**</span><span class="sxs-lookup"><span data-stu-id="d4362-252">**oldValue**</span></span> |<span data-ttu-id="d4362-253">選用</span><span class="sxs-lookup"><span data-stu-id="d4362-253">Optional</span></span> |<span data-ttu-id="d4362-254">String</span><span class="sxs-lookup"><span data-stu-id="d4362-254">String</span></span> |<span data-ttu-id="d4362-255">在 **source** 或 **template** 中要被取代的值。</span><span class="sxs-lookup"><span data-stu-id="d4362-255">Value to be replaced in **source** or **template**.</span></span> |
| <span data-ttu-id="d4362-256">**regexPattern**</span><span class="sxs-lookup"><span data-stu-id="d4362-256">**regexPattern**</span></span> |<span data-ttu-id="d4362-257">選用</span><span class="sxs-lookup"><span data-stu-id="d4362-257">Optional</span></span> |<span data-ttu-id="d4362-258">String</span><span class="sxs-lookup"><span data-stu-id="d4362-258">String</span></span> |<span data-ttu-id="d4362-259">在 **source**中要被取代的值的規則運算式模式。</span><span class="sxs-lookup"><span data-stu-id="d4362-259">Regex pattern for the value to be replaced in **source**.</span></span> <span data-ttu-id="d4362-260">或者，如果使用了 replacementPropertyName，要從取代屬性擷取值的模式。</span><span class="sxs-lookup"><span data-stu-id="d4362-260">Or, when replacementPropertyName is used, pattern to extract value from replacement property.</span></span> |
| <span data-ttu-id="d4362-261">**regexGroupName**</span><span class="sxs-lookup"><span data-stu-id="d4362-261">**regexGroupName**</span></span> |<span data-ttu-id="d4362-262">選用</span><span class="sxs-lookup"><span data-stu-id="d4362-262">Optional</span></span> |<span data-ttu-id="d4362-263">String</span><span class="sxs-lookup"><span data-stu-id="d4362-263">String</span></span> |<span data-ttu-id="d4362-264">**regexPattern**內的群組名稱。</span><span class="sxs-lookup"><span data-stu-id="d4362-264">Name of the group inside **regexPattern**.</span></span> <span data-ttu-id="d4362-265">只有當使用了 replacementPropertyName 時，我們才會從取代屬性擷取此群組的值做為 replacementValue。</span><span class="sxs-lookup"><span data-stu-id="d4362-265">Only when  replacementPropertyName is used, we will extract value of this group as replacementValue from replacement property.</span></span> |
| <span data-ttu-id="d4362-266">**replacementValue**</span><span class="sxs-lookup"><span data-stu-id="d4362-266">**replacementValue**</span></span> |<span data-ttu-id="d4362-267">選用</span><span class="sxs-lookup"><span data-stu-id="d4362-267">Optional</span></span> |<span data-ttu-id="d4362-268">String</span><span class="sxs-lookup"><span data-stu-id="d4362-268">String</span></span> |<span data-ttu-id="d4362-269">要取代舊值的新值。</span><span class="sxs-lookup"><span data-stu-id="d4362-269">New value to replace old one with.</span></span> |
| <span data-ttu-id="d4362-270">**replacementAttributeName**</span><span class="sxs-lookup"><span data-stu-id="d4362-270">**replacementAttributeName**</span></span> |<span data-ttu-id="d4362-271">選用</span><span class="sxs-lookup"><span data-stu-id="d4362-271">Optional</span></span> |<span data-ttu-id="d4362-272">String</span><span class="sxs-lookup"><span data-stu-id="d4362-272">String</span></span> |<span data-ttu-id="d4362-273">當 source 沒有任何值時，要用於取代值的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="d4362-273">Name of the attribute to be used for replacement value, when source has no value.</span></span> |
| <span data-ttu-id="d4362-274">**template**</span><span class="sxs-lookup"><span data-stu-id="d4362-274">**template**</span></span> |<span data-ttu-id="d4362-275">選用</span><span class="sxs-lookup"><span data-stu-id="d4362-275">Optional</span></span> |<span data-ttu-id="d4362-276">String</span><span class="sxs-lookup"><span data-stu-id="d4362-276">String</span></span> |<span data-ttu-id="d4362-277">提供 **template** 值時，我們會尋找 template 內的 **oldValue** 並以 source 值取代。</span><span class="sxs-lookup"><span data-stu-id="d4362-277">When **template** value is provided, we will look for **oldValue** inside the template and replace it with source value.</span></span> |

- - -
### <a name="stripspaces"></a><span data-ttu-id="d4362-278">StripSpaces</span><span class="sxs-lookup"><span data-stu-id="d4362-278">StripSpaces</span></span>
<span data-ttu-id="d4362-279">**函式：**</span><span class="sxs-lookup"><span data-stu-id="d4362-279">**Function:**</span></span><br> <span data-ttu-id="d4362-280">StripSpaces(source)</span><span class="sxs-lookup"><span data-stu-id="d4362-280">StripSpaces(source)</span></span>

<span data-ttu-id="d4362-281">**說明：**</span><span class="sxs-lookup"><span data-stu-id="d4362-281">**Description:**</span></span><br> <span data-ttu-id="d4362-282">移除 source 字串中的所有空格 (" ") 字元。</span><span class="sxs-lookup"><span data-stu-id="d4362-282">Removes all space (" ") characters from the source string.</span></span>

<span data-ttu-id="d4362-283">**參數：**</span><span class="sxs-lookup"><span data-stu-id="d4362-283">**Parameters:**</span></span><br> 

| <span data-ttu-id="d4362-284">名稱</span><span class="sxs-lookup"><span data-stu-id="d4362-284">Name</span></span> | <span data-ttu-id="d4362-285">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="d4362-285">Required/ Repeating</span></span> | <span data-ttu-id="d4362-286">型別</span><span class="sxs-lookup"><span data-stu-id="d4362-286">Type</span></span> | <span data-ttu-id="d4362-287">注意事項</span><span class="sxs-lookup"><span data-stu-id="d4362-287">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4362-288">**source**</span><span class="sxs-lookup"><span data-stu-id="d4362-288">**source**</span></span> |<span data-ttu-id="d4362-289">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-289">Required</span></span> |<span data-ttu-id="d4362-290">String</span><span class="sxs-lookup"><span data-stu-id="d4362-290">String</span></span> |<span data-ttu-id="d4362-291">**source** 值。</span><span class="sxs-lookup"><span data-stu-id="d4362-291">**source** value to update.</span></span> |

- - -
### <a name="switch"></a><span data-ttu-id="d4362-292">Switch</span><span class="sxs-lookup"><span data-stu-id="d4362-292">Switch</span></span>
<span data-ttu-id="d4362-293">**函式：**</span><span class="sxs-lookup"><span data-stu-id="d4362-293">**Function:**</span></span><br> <span data-ttu-id="d4362-294">Switch(source, defaultValue, key1, value1, key2, value2, …)</span><span class="sxs-lookup"><span data-stu-id="d4362-294">Switch(source, defaultValue, key1, value1, key2, value2, …)</span></span>

<span data-ttu-id="d4362-295">**說明：**</span><span class="sxs-lookup"><span data-stu-id="d4362-295">**Description:**</span></span><br> <span data-ttu-id="d4362-296">當 **source** 值符合某個 **key** 時，傳回該 **key** 的 **value**。</span><span class="sxs-lookup"><span data-stu-id="d4362-296">When **source** value matches a **key**, returns **value** for that **key**.</span></span> <span data-ttu-id="d4362-297">如果 **source** 值不符合任何 key，則傳回 **defaultValue**。</span><span class="sxs-lookup"><span data-stu-id="d4362-297">If **source** value doesn't match any keys, returns **defaultValue**.</span></span>  <span data-ttu-id="d4362-298">**key** 和 **value** 參數必須永遠成對出現。</span><span class="sxs-lookup"><span data-stu-id="d4362-298">**Key** and **value** parameters must always come in pairs.</span></span> <span data-ttu-id="d4362-299">函式必須要有偶數數目的參數。</span><span class="sxs-lookup"><span data-stu-id="d4362-299">The function always expects an even number of parameters.</span></span>

<span data-ttu-id="d4362-300">**參數：**</span><span class="sxs-lookup"><span data-stu-id="d4362-300">**Parameters:**</span></span><br> 

| <span data-ttu-id="d4362-301">名稱</span><span class="sxs-lookup"><span data-stu-id="d4362-301">Name</span></span> | <span data-ttu-id="d4362-302">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="d4362-302">Required/ Repeating</span></span> | <span data-ttu-id="d4362-303">型別</span><span class="sxs-lookup"><span data-stu-id="d4362-303">Type</span></span> | <span data-ttu-id="d4362-304">注意事項</span><span class="sxs-lookup"><span data-stu-id="d4362-304">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4362-305">**source**</span><span class="sxs-lookup"><span data-stu-id="d4362-305">**source**</span></span> |<span data-ttu-id="d4362-306">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-306">Required</span></span> |<span data-ttu-id="d4362-307">String</span><span class="sxs-lookup"><span data-stu-id="d4362-307">String</span></span> |<span data-ttu-id="d4362-308">**Source** 值。</span><span class="sxs-lookup"><span data-stu-id="d4362-308">**Source** value to update.</span></span> |
| <span data-ttu-id="d4362-309">**defaultValue**</span><span class="sxs-lookup"><span data-stu-id="d4362-309">**defaultValue**</span></span> |<span data-ttu-id="d4362-310">選用</span><span class="sxs-lookup"><span data-stu-id="d4362-310">Optional</span></span> |<span data-ttu-id="d4362-311">String</span><span class="sxs-lookup"><span data-stu-id="d4362-311">String</span></span> |<span data-ttu-id="d4362-312">當 source 不符合任何 key 時要使用的預設值。</span><span class="sxs-lookup"><span data-stu-id="d4362-312">Default value to be used when source doesn't match any keys.</span></span> <span data-ttu-id="d4362-313">可以是空字串 ("")。</span><span class="sxs-lookup"><span data-stu-id="d4362-313">Can be empty string ("").</span></span> |
| <span data-ttu-id="d4362-314">**key**</span><span class="sxs-lookup"><span data-stu-id="d4362-314">**key**</span></span> |<span data-ttu-id="d4362-315">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-315">Required</span></span> |<span data-ttu-id="d4362-316">String</span><span class="sxs-lookup"><span data-stu-id="d4362-316">String</span></span> |<span data-ttu-id="d4362-317">要與 **source** 值比較的 **key**。</span><span class="sxs-lookup"><span data-stu-id="d4362-317">**Key** to compare **source** value with.</span></span> |
| <span data-ttu-id="d4362-318">**value**</span><span class="sxs-lookup"><span data-stu-id="d4362-318">**value**</span></span> |<span data-ttu-id="d4362-319">必要</span><span class="sxs-lookup"><span data-stu-id="d4362-319">Required</span></span> |<span data-ttu-id="d4362-320">String</span><span class="sxs-lookup"><span data-stu-id="d4362-320">String</span></span> |<span data-ttu-id="d4362-321">符合 key 的 **source** 的取代值。</span><span class="sxs-lookup"><span data-stu-id="d4362-321">Replacement value for the **source** matching the key.</span></span> |

## <a name="examples"></a><span data-ttu-id="d4362-322">範例</span><span class="sxs-lookup"><span data-stu-id="d4362-322">Examples</span></span>
### <a name="strip-known-domain-name"></a><span data-ttu-id="d4362-323">刪去已知的網域名稱</span><span class="sxs-lookup"><span data-stu-id="d4362-323">Strip known domain name</span></span>
<span data-ttu-id="d4362-324">您必須從使用者的電子郵件刪去已知的網域名稱，得到使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d4362-324">You need to strip a known domain name from a user’s email to obtain a user name.</span></span> <br>
<span data-ttu-id="d4362-325">例如，如果網域是 "contoso.com"，您可以使用下列運算式：</span><span class="sxs-lookup"><span data-stu-id="d4362-325">For example, if the domain is "contoso.com", then you could use the following expression:</span></span>

<span data-ttu-id="d4362-326">**運算式：**</span><span class="sxs-lookup"><span data-stu-id="d4362-326">**Expression:**</span></span> <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

<span data-ttu-id="d4362-327">**範例輸入/輸出：**</span><span class="sxs-lookup"><span data-stu-id="d4362-327">**Sample input / output:**</span></span> <br>

* <span data-ttu-id="d4362-328">**輸入** (mail)："john.doe@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="d4362-328">**INPUT** (mail): "john.doe@contoso.com"</span></span>
* <span data-ttu-id="d4362-329">**輸出**："john.doe"</span><span class="sxs-lookup"><span data-stu-id="d4362-329">**OUTPUT**:  "john.doe"</span></span>

### <a name="append-constant-suffix-to-user-name"></a><span data-ttu-id="d4362-330">附加常數尾碼到使用者名稱</span><span class="sxs-lookup"><span data-stu-id="d4362-330">Append constant suffix to user name</span></span>
<span data-ttu-id="d4362-331">如果您使用 Salesforce 沙箱，您可能需要附加額外的尾碼到您所有的使用者名稱，才能進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="d4362-331">If you are using a Salesforce Sandbox, you might need to append an additional suffix to all your user names before synchronizing them.</span></span>

<span data-ttu-id="d4362-332">**運算式：**</span><span class="sxs-lookup"><span data-stu-id="d4362-332">**Expression:**</span></span> <br>
`Append([userPrincipalName], ".test"))`

<span data-ttu-id="d4362-333">**範例輸入/輸出：**</span><span class="sxs-lookup"><span data-stu-id="d4362-333">**Sample input/output:**</span></span> <br>

* <span data-ttu-id="d4362-334">**輸入**：(userPrincipalName)："John.Doe@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="d4362-334">**INPUT**: (userPrincipalName): "John.Doe@contoso.com"</span></span>
* <span data-ttu-id="d4362-335">**輸出**："John.Doe@contoso.com.test"</span><span class="sxs-lookup"><span data-stu-id="d4362-335">**OUTPUT**:  "John.Doe@contoso.com.test"</span></span>

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a><span data-ttu-id="d4362-336">串連部分名字和姓氏產生使用者別名</span><span class="sxs-lookup"><span data-stu-id="d4362-336">Generate user alias by concatenating parts of first and last name</span></span>
<span data-ttu-id="d4362-337">您必須取出使用者名字的前 3 個字母和使用者姓氏的前 5 個字母來產生使用者別名。</span><span class="sxs-lookup"><span data-stu-id="d4362-337">You need to generate a user alias by taking first 3 letters of user's first name and first 5 letters of user's last name.</span></span>

<span data-ttu-id="d4362-338">**運算式：**</span><span class="sxs-lookup"><span data-stu-id="d4362-338">**Expression:**</span></span> <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

<span data-ttu-id="d4362-339">**範例輸入/輸出：**</span><span class="sxs-lookup"><span data-stu-id="d4362-339">**Sample input/output:**</span></span> <br>

* <span data-ttu-id="d4362-340">**輸入** (givenName)："John"</span><span class="sxs-lookup"><span data-stu-id="d4362-340">**INPUT** (givenName): "John"</span></span>
* <span data-ttu-id="d4362-341">**輸入** (surname)："Doe"</span><span class="sxs-lookup"><span data-stu-id="d4362-341">**INPUT** (surname): "Doe"</span></span>
* <span data-ttu-id="d4362-342">**輸出**："JohDoe"</span><span class="sxs-lookup"><span data-stu-id="d4362-342">**OUTPUT**:  "JohDoe"</span></span>

### <a name="output-date-as-a-string-in-a-certain-format"></a><span data-ttu-id="d4362-343">以特定格式將日期輸出為字串</span><span class="sxs-lookup"><span data-stu-id="d4362-343">Output date as a string in a certain format</span></span>
<span data-ttu-id="d4362-344">您想要以特定格式傳送日期到 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4362-344">You want to send dates to a SaaS application in a certain format.</span></span> <br>
<span data-ttu-id="d4362-345">例如，您要格式化 ServiceNow 的日期。</span><span class="sxs-lookup"><span data-stu-id="d4362-345">For example, you want to format dates for ServiceNow.</span></span>

<span data-ttu-id="d4362-346">**運算式：**</span><span class="sxs-lookup"><span data-stu-id="d4362-346">**Expression:**</span></span> <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

<span data-ttu-id="d4362-347">**範例輸入/輸出：**</span><span class="sxs-lookup"><span data-stu-id="d4362-347">**Sample input/output:**</span></span>

* <span data-ttu-id="d4362-348">**輸入** (extensionAttribute1)："20150123105347.1Z"</span><span class="sxs-lookup"><span data-stu-id="d4362-348">**INPUT** (extensionAttribute1): "20150123105347.1Z"</span></span>
* <span data-ttu-id="d4362-349">**輸出**："2015-01-23"</span><span class="sxs-lookup"><span data-stu-id="d4362-349">**OUTPUT**:  "2015-01-23"</span></span>

### <a name="replace-a-value-based-on-predefined-set-of-options"></a><span data-ttu-id="d4362-350">根據預先定義的一組選項取代值</span><span class="sxs-lookup"><span data-stu-id="d4362-350">Replace a value based on predefined set of options</span></span>
<span data-ttu-id="d4362-351">您必須根據儲存在 Azure AD 中的狀態碼定義使用者的時區。</span><span class="sxs-lookup"><span data-stu-id="d4362-351">You need to define the time zone of the user based on the state code stored in Azure AD.</span></span> <br>
<span data-ttu-id="d4362-352">如果狀態碼不符合任何預先定義的選項，則使用 "Australia/Sydney" 的預設值。</span><span class="sxs-lookup"><span data-stu-id="d4362-352">If the state code doesn't match any of the predefined options, use default value of "Australia/Sydney".</span></span>

<span data-ttu-id="d4362-353">**運算式：**</span><span class="sxs-lookup"><span data-stu-id="d4362-353">**Expression:**</span></span> <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

<span data-ttu-id="d4362-354">**範例輸入/輸出：**</span><span class="sxs-lookup"><span data-stu-id="d4362-354">**Sample input/output:**</span></span>

* <span data-ttu-id="d4362-355">**輸入** (state)："QLD"</span><span class="sxs-lookup"><span data-stu-id="d4362-355">**INPUT** (state): "QLD"</span></span>
* <span data-ttu-id="d4362-356">**輸出**："Australia/Brisbane"</span><span class="sxs-lookup"><span data-stu-id="d4362-356">**OUTPUT**: "Australia/Brisbane"</span></span>

## <a name="related-articles"></a><span data-ttu-id="d4362-357">相關文章</span><span class="sxs-lookup"><span data-stu-id="d4362-357">Related Articles</span></span>
* [<span data-ttu-id="d4362-358">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="d4362-358">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="d4362-359">自動化 SaaS 應用程式使用者佈建/解除佈建</span><span class="sxs-lookup"><span data-stu-id="d4362-359">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="d4362-360">自訂使用者佈建的屬性對應</span><span class="sxs-lookup"><span data-stu-id="d4362-360">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="d4362-361">適用於使用者佈建的範圍篩選器</span><span class="sxs-lookup"><span data-stu-id="d4362-361">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="d4362-362">使用 SCIM 以啟用從 Azure Active Directory 到應用程式的使用者和群組自動佈建</span><span class="sxs-lookup"><span data-stu-id="d4362-362">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="d4362-363">帳戶佈建通知</span><span class="sxs-lookup"><span data-stu-id="d4362-363">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="d4362-364">如何整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d4362-364">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)


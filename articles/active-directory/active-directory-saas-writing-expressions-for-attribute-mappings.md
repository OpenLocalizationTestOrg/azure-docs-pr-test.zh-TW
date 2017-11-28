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
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a><span data-ttu-id="eded9-103">在 Azure Active Directory 中撰寫屬性對應的運算式</span><span class="sxs-lookup"><span data-stu-id="eded9-103">Writing Expressions for Attribute Mappings in Azure Active Directory</span></span>
<span data-ttu-id="eded9-104">當您設定佈建 tooa SaaS 應用程式時，其中一種您可以指定的屬性對應的 hello 類型是為運算式對應。</span><span class="sxs-lookup"><span data-stu-id="eded9-104">When you configure provisioning tooa SaaS application, one of hello types of attribute mappings that you can specify is an expression mapping.</span></span> <span data-ttu-id="eded9-105">這些項目，您必須撰寫類似指令碼運算式，可讓您 tootransform 使用者資料成 hello SaaS 應用程式可以接受的格式。</span><span class="sxs-lookup"><span data-stu-id="eded9-105">For these, you must write a script-like expression that allows you tootransform your users’ data into formats that are more acceptable for hello SaaS application.</span></span>

## <a name="syntax-overview"></a><span data-ttu-id="eded9-106">語法概觀</span><span class="sxs-lookup"><span data-stu-id="eded9-106">Syntax Overview</span></span>
<span data-ttu-id="eded9-107">hello 進行屬性對應的運算式語法是讓人聯想到 Visual Basic for Applications (VBA) 函數。</span><span class="sxs-lookup"><span data-stu-id="eded9-107">hello syntax for Expressions for Attribute Mappings is reminiscent of Visual Basic for Applications (VBA) functions.</span></span>

* <span data-ttu-id="eded9-108">hello 整個運算式必須定義以函數名稱，後面接著括號括住的引數所組成：</span><span class="sxs-lookup"><span data-stu-id="eded9-108">hello entire expression must be defined in terms of functions, which consist of a name followed by arguments in parentheses:</span></span> <br><span data-ttu-id="eded9-109">
  *FunctionName(<<argument 1>>,<<argument N>>)*</span><span class="sxs-lookup"><span data-stu-id="eded9-109">
*FunctionName(<<argument 1>>,<<argument N>>)*</span></span>
* <span data-ttu-id="eded9-110">您可以在函式內互相巢狀函式。</span><span class="sxs-lookup"><span data-stu-id="eded9-110">You may nest functions within each other.</span></span> <span data-ttu-id="eded9-111">例如：</span><span class="sxs-lookup"><span data-stu-id="eded9-111">For example:</span></span> <br> <span data-ttu-id="eded9-112">*FunctionOne(FunctionTwo(<<argument1>>))*</span><span class="sxs-lookup"><span data-stu-id="eded9-112">*FunctionOne(FunctionTwo(<<argument1>>))*</span></span>
* <span data-ttu-id="eded9-113">您可以將三種不同類型的引數傳入函式：</span><span class="sxs-lookup"><span data-stu-id="eded9-113">You can pass three different types of arguments into functions:</span></span>
  
  1. <span data-ttu-id="eded9-114">屬性，必須以方括弧括住。</span><span class="sxs-lookup"><span data-stu-id="eded9-114">Attributes, which must be enclosed in square square brackets.</span></span> <span data-ttu-id="eded9-115">例如：[attributeName]</span><span class="sxs-lookup"><span data-stu-id="eded9-115">For example: [attributeName]</span></span>
  2. <span data-ttu-id="eded9-116">字串常數，必須以雙引號括住。</span><span class="sxs-lookup"><span data-stu-id="eded9-116">String constants, which must be enclosed in double quotes.</span></span> <span data-ttu-id="eded9-117">例如："United States"</span><span class="sxs-lookup"><span data-stu-id="eded9-117">For example: "United States"</span></span>
  3. <span data-ttu-id="eded9-118">其他函式。</span><span class="sxs-lookup"><span data-stu-id="eded9-118">Other Functions.</span></span> <span data-ttu-id="eded9-119">例如：FunctionOne(<<argument1>>, FunctionTwo(<<argument2>>))</span><span class="sxs-lookup"><span data-stu-id="eded9-119">For example: FunctionOne(<<argument1>>, FunctionTwo(<<argument2>>))</span></span>
* <span data-ttu-id="eded9-120">字串常數，如果您需要反斜線 (\) 或引號 （"） 在 hello 字串中，則必須逸出 hello 反斜線 (\) 符號。</span><span class="sxs-lookup"><span data-stu-id="eded9-120">For string constants, if you need a backslash ( \ ) or quotation mark ( " ) in hello string, it must be escaped with hello backslash ( \ ) symbol.</span></span> <span data-ttu-id="eded9-121">例如："公司名稱：\"Contoso\""</span><span class="sxs-lookup"><span data-stu-id="eded9-121">For example: "Company name: \"Contoso\""</span></span>

## <a name="list-of-functions"></a><span data-ttu-id="eded9-122">函式的清單</span><span class="sxs-lookup"><span data-stu-id="eded9-122">List of Functions</span></span>
<span data-ttu-id="eded9-123">[Append](#append) &nbsp;&nbsp;&nbsp;&nbsp; [FormatDateTime](#formatdatetime) &nbsp;&nbsp;&nbsp;&nbsp; [Join](#join) &nbsp;&nbsp;&nbsp;&nbsp; [Mid](#mid) &nbsp;&nbsp;&nbsp;&nbsp; [Not](#not) &nbsp;&nbsp;&nbsp;&nbsp; [將](#replace) &nbsp;&nbsp;&nbsp;&nbsp; [StripSpaces](#stripspaces) &nbsp;&nbsp;&nbsp;&nbsp; [Switch](#switch)</span><span class="sxs-lookup"><span data-stu-id="eded9-123">[Append](#append) &nbsp;&nbsp;&nbsp;&nbsp; [FormatDateTime](#formatdatetime) &nbsp;&nbsp;&nbsp;&nbsp; [Join](#join) &nbsp;&nbsp;&nbsp;&nbsp; [Mid](#mid) &nbsp;&nbsp;&nbsp;&nbsp; [Not](#not) &nbsp;&nbsp;&nbsp;&nbsp; [Replace](#replace) &nbsp;&nbsp;&nbsp;&nbsp; [StripSpaces](#stripspaces) &nbsp;&nbsp;&nbsp;&nbsp; [Switch](#switch)</span></span>

- - -
### <a name="append"></a><span data-ttu-id="eded9-124">Append</span><span class="sxs-lookup"><span data-stu-id="eded9-124">Append</span></span>
<span data-ttu-id="eded9-125">**函式：**</span><span class="sxs-lookup"><span data-stu-id="eded9-125">**Function:**</span></span><br> <span data-ttu-id="eded9-126">Append(source, suffix)</span><span class="sxs-lookup"><span data-stu-id="eded9-126">Append(source, suffix)</span></span>

<span data-ttu-id="eded9-127">**說明：**</span><span class="sxs-lookup"><span data-stu-id="eded9-127">**Description:**</span></span><br> <span data-ttu-id="eded9-128">接受來源字串值，並且附加 hello 尾碼 toohello 結尾。</span><span class="sxs-lookup"><span data-stu-id="eded9-128">Takes a source string value and appends hello suffix toohello end of it.</span></span>

<span data-ttu-id="eded9-129">**參數：**</span><span class="sxs-lookup"><span data-stu-id="eded9-129">**Parameters:**</span></span><br> 

| <span data-ttu-id="eded9-130">名稱</span><span class="sxs-lookup"><span data-stu-id="eded9-130">Name</span></span> | <span data-ttu-id="eded9-131">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="eded9-131">Required/ Repeating</span></span> | <span data-ttu-id="eded9-132">型別</span><span class="sxs-lookup"><span data-stu-id="eded9-132">Type</span></span> | <span data-ttu-id="eded9-133">注意事項</span><span class="sxs-lookup"><span data-stu-id="eded9-133">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eded9-134">**source**</span><span class="sxs-lookup"><span data-stu-id="eded9-134">**source**</span></span> |<span data-ttu-id="eded9-135">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-135">Required</span></span> |<span data-ttu-id="eded9-136">String</span><span class="sxs-lookup"><span data-stu-id="eded9-136">String</span></span> |<span data-ttu-id="eded9-137">通常從 hello 來源物件的 hello 屬性名稱</span><span class="sxs-lookup"><span data-stu-id="eded9-137">Usually name of hello attribute from hello source object</span></span> |
| <span data-ttu-id="eded9-138">**suffix**</span><span class="sxs-lookup"><span data-stu-id="eded9-138">**suffix**</span></span> |<span data-ttu-id="eded9-139">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-139">Required</span></span> |<span data-ttu-id="eded9-140">String</span><span class="sxs-lookup"><span data-stu-id="eded9-140">String</span></span> |<span data-ttu-id="eded9-141">hello 想 tooappend toohello 結尾 hello 來源值的字串。</span><span class="sxs-lookup"><span data-stu-id="eded9-141">hello string that you want tooappend toohello end of hello source value.</span></span> |

- - -
### <a name="formatdatetime"></a><span data-ttu-id="eded9-142">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="eded9-142">FormatDateTime</span></span>
<span data-ttu-id="eded9-143">**函式：**</span><span class="sxs-lookup"><span data-stu-id="eded9-143">**Function:**</span></span><br> <span data-ttu-id="eded9-144"> FormatDateTime(source, inputFormat, outputFormat)</span><span class="sxs-lookup"><span data-stu-id="eded9-144">FormatDateTime(source, inputFormat, outputFormat)</span></span>

<span data-ttu-id="eded9-145">**說明：**</span><span class="sxs-lookup"><span data-stu-id="eded9-145">**Description:**</span></span><br> <span data-ttu-id="eded9-146">從一種格式取出日期字串，並將它轉換成不同的格式。</span><span class="sxs-lookup"><span data-stu-id="eded9-146">Takes a date string from one format and converts it into a different format.</span></span>

<span data-ttu-id="eded9-147">**參數：**</span><span class="sxs-lookup"><span data-stu-id="eded9-147">**Parameters:**</span></span><br> 

| <span data-ttu-id="eded9-148">名稱</span><span class="sxs-lookup"><span data-stu-id="eded9-148">Name</span></span> | <span data-ttu-id="eded9-149">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="eded9-149">Required/ Repeating</span></span> | <span data-ttu-id="eded9-150">型別</span><span class="sxs-lookup"><span data-stu-id="eded9-150">Type</span></span> | <span data-ttu-id="eded9-151">注意事項</span><span class="sxs-lookup"><span data-stu-id="eded9-151">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eded9-152">**source**</span><span class="sxs-lookup"><span data-stu-id="eded9-152">**source**</span></span> |<span data-ttu-id="eded9-153">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-153">Required</span></span> |<span data-ttu-id="eded9-154">String</span><span class="sxs-lookup"><span data-stu-id="eded9-154">String</span></span> |<span data-ttu-id="eded9-155">通常 hello hello 來源物件屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="eded9-155">Usually name of hello attribute from hello source object.</span></span> |
| <span data-ttu-id="eded9-156">**inputFormat**</span><span class="sxs-lookup"><span data-stu-id="eded9-156">**inputFormat**</span></span> |<span data-ttu-id="eded9-157">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-157">Required</span></span> |<span data-ttu-id="eded9-158">String</span><span class="sxs-lookup"><span data-stu-id="eded9-158">String</span></span> |<span data-ttu-id="eded9-159">Hello 來源值的預期的格式。</span><span class="sxs-lookup"><span data-stu-id="eded9-159">Expected format of hello source value.</span></span> <span data-ttu-id="eded9-160">如需支援的格式，請參閱 [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="eded9-160">For supported formats, see [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx).</span></span> |
| <span data-ttu-id="eded9-161">**outputFormat**</span><span class="sxs-lookup"><span data-stu-id="eded9-161">**outputFormat**</span></span> |<span data-ttu-id="eded9-162">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-162">Required</span></span> |<span data-ttu-id="eded9-163">String</span><span class="sxs-lookup"><span data-stu-id="eded9-163">String</span></span> |<span data-ttu-id="eded9-164">Hello 輸出日期的格式。</span><span class="sxs-lookup"><span data-stu-id="eded9-164">Format of hello output date.</span></span> |

- - -
### <a name="join"></a><span data-ttu-id="eded9-165">Join</span><span class="sxs-lookup"><span data-stu-id="eded9-165">Join</span></span>
<span data-ttu-id="eded9-166">**函式：**</span><span class="sxs-lookup"><span data-stu-id="eded9-166">**Function:**</span></span><br> <span data-ttu-id="eded9-167">Join(separator, source1, source2, …)</span><span class="sxs-lookup"><span data-stu-id="eded9-167">Join(separator, source1, source2, …)</span></span>

<span data-ttu-id="eded9-168">**說明：**</span><span class="sxs-lookup"><span data-stu-id="eded9-168">**Description:**</span></span><br> <span data-ttu-id="eded9-169">Join （） 是類似的 tooAppend()，不同之處在於它結合多個**來源**成單一字串，值的字串和每個值會分開**分隔符號**字串。</span><span class="sxs-lookup"><span data-stu-id="eded9-169">Join() is similar tooAppend(), except that it can combine multiple **source** string values into a single string, and each value will be separated by a **separator** string.</span></span>

<span data-ttu-id="eded9-170">如果 hello 來源值的其中一個是多重值屬性，則該屬性中的每個值會聯結在一起，分隔 hello 分隔符號值。</span><span class="sxs-lookup"><span data-stu-id="eded9-170">If one of hello source values is a multi-value attribute, then every value in that attribute will be joined together, separated hello separator value.</span></span>

<span data-ttu-id="eded9-171">**參數：**</span><span class="sxs-lookup"><span data-stu-id="eded9-171">**Parameters:**</span></span><br> 

| <span data-ttu-id="eded9-172">名稱</span><span class="sxs-lookup"><span data-stu-id="eded9-172">Name</span></span> | <span data-ttu-id="eded9-173">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="eded9-173">Required/ Repeating</span></span> | <span data-ttu-id="eded9-174">型別</span><span class="sxs-lookup"><span data-stu-id="eded9-174">Type</span></span> | <span data-ttu-id="eded9-175">注意事項</span><span class="sxs-lookup"><span data-stu-id="eded9-175">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eded9-176">**separator**</span><span class="sxs-lookup"><span data-stu-id="eded9-176">**separator**</span></span> |<span data-ttu-id="eded9-177">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-177">Required</span></span> |<span data-ttu-id="eded9-178">String</span><span class="sxs-lookup"><span data-stu-id="eded9-178">String</span></span> |<span data-ttu-id="eded9-179">它們會串連成一個字串時，字串會使用 tooseparate 來源值。</span><span class="sxs-lookup"><span data-stu-id="eded9-179">String used tooseparate source values when they are concatenated into one string.</span></span> <span data-ttu-id="eded9-180">如果不需要分隔符號，可以是 ""。</span><span class="sxs-lookup"><span data-stu-id="eded9-180">Can be "" if no separator is required.</span></span> |
| <span data-ttu-id="eded9-181">**source1  …</span><span class="sxs-lookup"><span data-stu-id="eded9-181">**source1  …</span></span> <span data-ttu-id="eded9-182">sourceN **</span><span class="sxs-lookup"><span data-stu-id="eded9-182">sourceN **</span></span> |<span data-ttu-id="eded9-183">必要，變動次數</span><span class="sxs-lookup"><span data-stu-id="eded9-183">Required, variable-number of times</span></span> |<span data-ttu-id="eded9-184">String</span><span class="sxs-lookup"><span data-stu-id="eded9-184">String</span></span> |<span data-ttu-id="eded9-185">字串值 toobe 聯結在一起。</span><span class="sxs-lookup"><span data-stu-id="eded9-185">String values toobe joined together.</span></span> |

- - -
### <a name="mid"></a><span data-ttu-id="eded9-186">Mid</span><span class="sxs-lookup"><span data-stu-id="eded9-186">Mid</span></span>
<span data-ttu-id="eded9-187">**函式：**</span><span class="sxs-lookup"><span data-stu-id="eded9-187">**Function:**</span></span><br> <span data-ttu-id="eded9-188">Mid(source, start, length)</span><span class="sxs-lookup"><span data-stu-id="eded9-188">Mid(source, start, length)</span></span>

<span data-ttu-id="eded9-189">**說明：**</span><span class="sxs-lookup"><span data-stu-id="eded9-189">**Description:**</span></span><br> <span data-ttu-id="eded9-190">傳回子字串 hello 來源值。</span><span class="sxs-lookup"><span data-stu-id="eded9-190">Returns a substring of hello source value.</span></span> <span data-ttu-id="eded9-191">子字串會包含只對某些 hello 來源字串 hello 字元的字串。</span><span class="sxs-lookup"><span data-stu-id="eded9-191">A substring is a string that contains only some of hello characters from hello source string.</span></span>

<span data-ttu-id="eded9-192">**參數：**</span><span class="sxs-lookup"><span data-stu-id="eded9-192">**Parameters:**</span></span><br> 

| <span data-ttu-id="eded9-193">名稱</span><span class="sxs-lookup"><span data-stu-id="eded9-193">Name</span></span> | <span data-ttu-id="eded9-194">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="eded9-194">Required/ Repeating</span></span> | <span data-ttu-id="eded9-195">型別</span><span class="sxs-lookup"><span data-stu-id="eded9-195">Type</span></span> | <span data-ttu-id="eded9-196">注意事項</span><span class="sxs-lookup"><span data-stu-id="eded9-196">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eded9-197">**source**</span><span class="sxs-lookup"><span data-stu-id="eded9-197">**source**</span></span> |<span data-ttu-id="eded9-198">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-198">Required</span></span> |<span data-ttu-id="eded9-199">String</span><span class="sxs-lookup"><span data-stu-id="eded9-199">String</span></span> |<span data-ttu-id="eded9-200">通常 hello 屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="eded9-200">Usually name of hello attribute.</span></span> |
| <span data-ttu-id="eded9-201">**start**</span><span class="sxs-lookup"><span data-stu-id="eded9-201">**start**</span></span> |<span data-ttu-id="eded9-202">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-202">Required</span></span> |<span data-ttu-id="eded9-203">integer</span><span class="sxs-lookup"><span data-stu-id="eded9-203">integer</span></span> |<span data-ttu-id="eded9-204">索引中 hello**來源**應該在此處開始的子字串的字串。</span><span class="sxs-lookup"><span data-stu-id="eded9-204">Index in hello **source** string where substring should start.</span></span> <span data-ttu-id="eded9-205">Hello 字串中的第一個字元必須索引為 1，第二個字元將會有索引 2，依此類推。</span><span class="sxs-lookup"><span data-stu-id="eded9-205">First character in hello string will have index of 1, second character will have index 2, and so on.</span></span> |
| <span data-ttu-id="eded9-206">**length**</span><span class="sxs-lookup"><span data-stu-id="eded9-206">**length**</span></span> |<span data-ttu-id="eded9-207">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-207">Required</span></span> |<span data-ttu-id="eded9-208">integer</span><span class="sxs-lookup"><span data-stu-id="eded9-208">integer</span></span> |<span data-ttu-id="eded9-209">Hello 子字串的長度。</span><span class="sxs-lookup"><span data-stu-id="eded9-209">Length of hello substring.</span></span> <span data-ttu-id="eded9-210">若長度結尾處之外 hello**來源**字串函數會傳回子字串從**啟動**索引到結尾**來源**字串。</span><span class="sxs-lookup"><span data-stu-id="eded9-210">If length ends outside hello **source** string, function will return substring from **start** index till end of **source** string.</span></span> |

- - -
### <a name="not"></a><span data-ttu-id="eded9-211">否</span><span class="sxs-lookup"><span data-stu-id="eded9-211">Not</span></span>
<span data-ttu-id="eded9-212">**函式：**</span><span class="sxs-lookup"><span data-stu-id="eded9-212">**Function:**</span></span><br> <span data-ttu-id="eded9-213">Not(source)</span><span class="sxs-lookup"><span data-stu-id="eded9-213">Not(source)</span></span>

<span data-ttu-id="eded9-214">**說明：**</span><span class="sxs-lookup"><span data-stu-id="eded9-214">**Description:**</span></span><br> <span data-ttu-id="eded9-215">翻轉 hello 布林值為 hello**來源**。</span><span class="sxs-lookup"><span data-stu-id="eded9-215">Flips hello boolean value of hello **source**.</span></span> <span data-ttu-id="eded9-216">如果 **source** 值為 "*True*"，則傳回 "*False*"。</span><span class="sxs-lookup"><span data-stu-id="eded9-216">If **source** value is "*True*", returns "*False*".</span></span> <span data-ttu-id="eded9-217">反之則傳回 "*True*"。</span><span class="sxs-lookup"><span data-stu-id="eded9-217">Otherwise, returns "*True*".</span></span>

<span data-ttu-id="eded9-218">**參數：**</span><span class="sxs-lookup"><span data-stu-id="eded9-218">**Parameters:**</span></span><br> 

| <span data-ttu-id="eded9-219">名稱</span><span class="sxs-lookup"><span data-stu-id="eded9-219">Name</span></span> | <span data-ttu-id="eded9-220">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="eded9-220">Required/ Repeating</span></span> | <span data-ttu-id="eded9-221">型別</span><span class="sxs-lookup"><span data-stu-id="eded9-221">Type</span></span> | <span data-ttu-id="eded9-222">注意事項</span><span class="sxs-lookup"><span data-stu-id="eded9-222">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eded9-223">**source**</span><span class="sxs-lookup"><span data-stu-id="eded9-223">**source**</span></span> |<span data-ttu-id="eded9-224">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-224">Required</span></span> |<span data-ttu-id="eded9-225">Boolean String</span><span class="sxs-lookup"><span data-stu-id="eded9-225">Boolean String</span></span> |<span data-ttu-id="eded9-226">預期的 **source** 值為 "True" 或 "False"。</span><span class="sxs-lookup"><span data-stu-id="eded9-226">Expected **source** values are "True" or "False"..</span></span> |

- - -
### <a name="replace"></a><span data-ttu-id="eded9-227">將</span><span class="sxs-lookup"><span data-stu-id="eded9-227">Replace</span></span>
<span data-ttu-id="eded9-228">**函式：**</span><span class="sxs-lookup"><span data-stu-id="eded9-228">**Function:**</span></span><br> <span data-ttu-id="eded9-229">ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)</span><span class="sxs-lookup"><span data-stu-id="eded9-229">ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)</span></span>

<span data-ttu-id="eded9-230">**說明：**</span><span class="sxs-lookup"><span data-stu-id="eded9-230">**Description:**</span></span><br>
<span data-ttu-id="eded9-231">取代字串內的值。</span><span class="sxs-lookup"><span data-stu-id="eded9-231">Replaces values within a string.</span></span> <span data-ttu-id="eded9-232">此函數的作用視提供的 hello 參數而定：</span><span class="sxs-lookup"><span data-stu-id="eded9-232">It works differently depending on hello parameters provided:</span></span>

* <span data-ttu-id="eded9-233">提供 **oldValue** 和 **replacementValue** 時：</span><span class="sxs-lookup"><span data-stu-id="eded9-233">When **oldValue** and **replacementValue** are provided:</span></span>
  
  * <span data-ttu-id="eded9-234">OldValue hello 來源中的所有項目取代 replacementValue</span><span class="sxs-lookup"><span data-stu-id="eded9-234">Replaces all occurrences of oldValue in hello source  with replacementValue</span></span>
* <span data-ttu-id="eded9-235">提供 **oldValue** 和 **template** 時：</span><span class="sxs-lookup"><span data-stu-id="eded9-235">When **oldValue** and **template** are provided:</span></span>
  
  * <span data-ttu-id="eded9-236">會取代所有出現的 hello **oldValue**在 hello**範本**以 hello**來源**值</span><span class="sxs-lookup"><span data-stu-id="eded9-236">Replaces all occurrences of hello **oldValue** in hello **template** with hello **source** value</span></span>
* <span data-ttu-id="eded9-237">提供 **oldValueRegexPattern**、**oldValueRegexGroupName**、**replacementValue** 時：</span><span class="sxs-lookup"><span data-stu-id="eded9-237">When **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementValue** are provided:</span></span>
  
  * <span data-ttu-id="eded9-238">取代相符的 oldValueRegexPattern replacementValue 與 hello 來源字串中的所有值</span><span class="sxs-lookup"><span data-stu-id="eded9-238">Replaces all values matching oldValueRegexPattern in hello source string with replacementValue</span></span>
* <span data-ttu-id="eded9-239">提供 **oldValueRegexPattern**、**oldValueRegexGroupName**、**replacementPropertyName** 時：</span><span class="sxs-lookup"><span data-stu-id="eded9-239">When **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementPropertyName** are provided:</span></span>
  
  * <span data-ttu-id="eded9-240">如果 **source** 有值，則傳回 **source**</span><span class="sxs-lookup"><span data-stu-id="eded9-240">If **source** has value, **source** is returned</span></span>
  * <span data-ttu-id="eded9-241">如果**來源**沒有值，會使用**oldValueRegexPattern**和**oldValueRegexGroupName** tooextract 取代值，從與 hello 屬性**replacementPropertyName**。</span><span class="sxs-lookup"><span data-stu-id="eded9-241">If **source** has no value, uses **oldValueRegexPattern** and **oldValueRegexGroupName** tooextract replacement value from hello property with **replacementPropertyName**.</span></span> <span data-ttu-id="eded9-242">Hello 結果為傳回取代值</span><span class="sxs-lookup"><span data-stu-id="eded9-242">Replacement value is returned as hello result</span></span>

<span data-ttu-id="eded9-243">**參數：**</span><span class="sxs-lookup"><span data-stu-id="eded9-243">**Parameters:**</span></span><br> 

| <span data-ttu-id="eded9-244">名稱</span><span class="sxs-lookup"><span data-stu-id="eded9-244">Name</span></span> | <span data-ttu-id="eded9-245">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="eded9-245">Required/ Repeating</span></span> | <span data-ttu-id="eded9-246">型別</span><span class="sxs-lookup"><span data-stu-id="eded9-246">Type</span></span> | <span data-ttu-id="eded9-247">注意事項</span><span class="sxs-lookup"><span data-stu-id="eded9-247">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eded9-248">**source**</span><span class="sxs-lookup"><span data-stu-id="eded9-248">**source**</span></span> |<span data-ttu-id="eded9-249">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-249">Required</span></span> |<span data-ttu-id="eded9-250">String</span><span class="sxs-lookup"><span data-stu-id="eded9-250">String</span></span> |<span data-ttu-id="eded9-251">通常 hello hello 來源物件屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="eded9-251">Usually name of hello attribute from hello source object.</span></span> |
| <span data-ttu-id="eded9-252">**oldValue**</span><span class="sxs-lookup"><span data-stu-id="eded9-252">**oldValue**</span></span> |<span data-ttu-id="eded9-253">選用</span><span class="sxs-lookup"><span data-stu-id="eded9-253">Optional</span></span> |<span data-ttu-id="eded9-254">String</span><span class="sxs-lookup"><span data-stu-id="eded9-254">String</span></span> |<span data-ttu-id="eded9-255">值取代 toobe**來源**或**範本**。</span><span class="sxs-lookup"><span data-stu-id="eded9-255">Value toobe replaced in **source** or **template**.</span></span> |
| <span data-ttu-id="eded9-256">**regexPattern**</span><span class="sxs-lookup"><span data-stu-id="eded9-256">**regexPattern**</span></span> |<span data-ttu-id="eded9-257">選用</span><span class="sxs-lookup"><span data-stu-id="eded9-257">Optional</span></span> |<span data-ttu-id="eded9-258">String</span><span class="sxs-lookup"><span data-stu-id="eded9-258">String</span></span> |<span data-ttu-id="eded9-259">Regex 模式中被取代的 hello 值 toobe**來源**。</span><span class="sxs-lookup"><span data-stu-id="eded9-259">Regex pattern for hello value toobe replaced in **source**.</span></span> <span data-ttu-id="eded9-260">或者，使用 replacementPropertyName 時，模式 tooextract 從取代內容的值。</span><span class="sxs-lookup"><span data-stu-id="eded9-260">Or, when replacementPropertyName is used, pattern tooextract value from replacement property.</span></span> |
| <span data-ttu-id="eded9-261">**regexGroupName**</span><span class="sxs-lookup"><span data-stu-id="eded9-261">**regexGroupName**</span></span> |<span data-ttu-id="eded9-262">選用</span><span class="sxs-lookup"><span data-stu-id="eded9-262">Optional</span></span> |<span data-ttu-id="eded9-263">String</span><span class="sxs-lookup"><span data-stu-id="eded9-263">String</span></span> |<span data-ttu-id="eded9-264">Hello 群組內的名稱**regexpattern 中**。</span><span class="sxs-lookup"><span data-stu-id="eded9-264">Name of hello group inside **regexPattern**.</span></span> <span data-ttu-id="eded9-265">只有當使用了 replacementPropertyName 時，我們才會從取代屬性擷取此群組的值做為 replacementValue。</span><span class="sxs-lookup"><span data-stu-id="eded9-265">Only when  replacementPropertyName is used, we will extract value of this group as replacementValue from replacement property.</span></span> |
| <span data-ttu-id="eded9-266">**replacementValue**</span><span class="sxs-lookup"><span data-stu-id="eded9-266">**replacementValue**</span></span> |<span data-ttu-id="eded9-267">選用</span><span class="sxs-lookup"><span data-stu-id="eded9-267">Optional</span></span> |<span data-ttu-id="eded9-268">String</span><span class="sxs-lookup"><span data-stu-id="eded9-268">String</span></span> |<span data-ttu-id="eded9-269">新值 tooreplace 舊專案使用。</span><span class="sxs-lookup"><span data-stu-id="eded9-269">New value tooreplace old one with.</span></span> |
| <span data-ttu-id="eded9-270">**replacementAttributeName**</span><span class="sxs-lookup"><span data-stu-id="eded9-270">**replacementAttributeName**</span></span> |<span data-ttu-id="eded9-271">選用</span><span class="sxs-lookup"><span data-stu-id="eded9-271">Optional</span></span> |<span data-ttu-id="eded9-272">String</span><span class="sxs-lookup"><span data-stu-id="eded9-272">String</span></span> |<span data-ttu-id="eded9-273">Hello 屬性 toobe 用於當來源沒有任何值的取代值的名稱。</span><span class="sxs-lookup"><span data-stu-id="eded9-273">Name of hello attribute toobe used for replacement value, when source has no value.</span></span> |
| <span data-ttu-id="eded9-274">**template**</span><span class="sxs-lookup"><span data-stu-id="eded9-274">**template**</span></span> |<span data-ttu-id="eded9-275">選用</span><span class="sxs-lookup"><span data-stu-id="eded9-275">Optional</span></span> |<span data-ttu-id="eded9-276">String</span><span class="sxs-lookup"><span data-stu-id="eded9-276">String</span></span> |<span data-ttu-id="eded9-277">當**範本**提供值，則會尋找**oldValue**內部 hello 範本，並取代為原始值。</span><span class="sxs-lookup"><span data-stu-id="eded9-277">When **template** value is provided, we will look for **oldValue** inside hello template and replace it with source value.</span></span> |

- - -
### <a name="stripspaces"></a><span data-ttu-id="eded9-278">StripSpaces</span><span class="sxs-lookup"><span data-stu-id="eded9-278">StripSpaces</span></span>
<span data-ttu-id="eded9-279">**函式：**</span><span class="sxs-lookup"><span data-stu-id="eded9-279">**Function:**</span></span><br> <span data-ttu-id="eded9-280">StripSpaces(source)</span><span class="sxs-lookup"><span data-stu-id="eded9-280">StripSpaces(source)</span></span>

<span data-ttu-id="eded9-281">**說明：**</span><span class="sxs-lookup"><span data-stu-id="eded9-281">**Description:**</span></span><br> <span data-ttu-id="eded9-282">移除開頭空格 ("") 字元 hello 從來源字串。</span><span class="sxs-lookup"><span data-stu-id="eded9-282">Removes all space (" ") characters from hello source string.</span></span>

<span data-ttu-id="eded9-283">**參數：**</span><span class="sxs-lookup"><span data-stu-id="eded9-283">**Parameters:**</span></span><br> 

| <span data-ttu-id="eded9-284">名稱</span><span class="sxs-lookup"><span data-stu-id="eded9-284">Name</span></span> | <span data-ttu-id="eded9-285">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="eded9-285">Required/ Repeating</span></span> | <span data-ttu-id="eded9-286">型別</span><span class="sxs-lookup"><span data-stu-id="eded9-286">Type</span></span> | <span data-ttu-id="eded9-287">注意事項</span><span class="sxs-lookup"><span data-stu-id="eded9-287">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eded9-288">**source**</span><span class="sxs-lookup"><span data-stu-id="eded9-288">**source**</span></span> |<span data-ttu-id="eded9-289">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-289">Required</span></span> |<span data-ttu-id="eded9-290">String</span><span class="sxs-lookup"><span data-stu-id="eded9-290">String</span></span> |<span data-ttu-id="eded9-291">**來源**值 tooupdate。</span><span class="sxs-lookup"><span data-stu-id="eded9-291">**source** value tooupdate.</span></span> |

- - -
### <a name="switch"></a><span data-ttu-id="eded9-292">Switch</span><span class="sxs-lookup"><span data-stu-id="eded9-292">Switch</span></span>
<span data-ttu-id="eded9-293">**函式：**</span><span class="sxs-lookup"><span data-stu-id="eded9-293">**Function:**</span></span><br> <span data-ttu-id="eded9-294">Switch(source, defaultValue, key1, value1, key2, value2, …)</span><span class="sxs-lookup"><span data-stu-id="eded9-294">Switch(source, defaultValue, key1, value1, key2, value2, …)</span></span>

<span data-ttu-id="eded9-295">**說明：**</span><span class="sxs-lookup"><span data-stu-id="eded9-295">**Description:**</span></span><br> <span data-ttu-id="eded9-296">當 **source** 值符合某個 **key** 時，傳回該 **key** 的 **value**。</span><span class="sxs-lookup"><span data-stu-id="eded9-296">When **source** value matches a **key**, returns **value** for that **key**.</span></span> <span data-ttu-id="eded9-297">如果 **source** 值不符合任何 key，則傳回 **defaultValue**。</span><span class="sxs-lookup"><span data-stu-id="eded9-297">If **source** value doesn't match any keys, returns **defaultValue**.</span></span>  <span data-ttu-id="eded9-298">**key** 和 **value** 參數必須永遠成對出現。</span><span class="sxs-lookup"><span data-stu-id="eded9-298">**Key** and **value** parameters must always come in pairs.</span></span> <span data-ttu-id="eded9-299">hello 函式一律預期出現雙數的參數。</span><span class="sxs-lookup"><span data-stu-id="eded9-299">hello function always expects an even number of parameters.</span></span>

<span data-ttu-id="eded9-300">**參數：**</span><span class="sxs-lookup"><span data-stu-id="eded9-300">**Parameters:**</span></span><br> 

| <span data-ttu-id="eded9-301">名稱</span><span class="sxs-lookup"><span data-stu-id="eded9-301">Name</span></span> | <span data-ttu-id="eded9-302">必要 / 重複</span><span class="sxs-lookup"><span data-stu-id="eded9-302">Required/ Repeating</span></span> | <span data-ttu-id="eded9-303">型別</span><span class="sxs-lookup"><span data-stu-id="eded9-303">Type</span></span> | <span data-ttu-id="eded9-304">注意事項</span><span class="sxs-lookup"><span data-stu-id="eded9-304">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eded9-305">**source**</span><span class="sxs-lookup"><span data-stu-id="eded9-305">**source**</span></span> |<span data-ttu-id="eded9-306">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-306">Required</span></span> |<span data-ttu-id="eded9-307">String</span><span class="sxs-lookup"><span data-stu-id="eded9-307">String</span></span> |<span data-ttu-id="eded9-308">**來源**值 tooupdate。</span><span class="sxs-lookup"><span data-stu-id="eded9-308">**Source** value tooupdate.</span></span> |
| <span data-ttu-id="eded9-309">**defaultValue**</span><span class="sxs-lookup"><span data-stu-id="eded9-309">**defaultValue**</span></span> |<span data-ttu-id="eded9-310">選用</span><span class="sxs-lookup"><span data-stu-id="eded9-310">Optional</span></span> |<span data-ttu-id="eded9-311">String</span><span class="sxs-lookup"><span data-stu-id="eded9-311">String</span></span> |<span data-ttu-id="eded9-312">預設值 toobe 來源不符合任何 key 時使用。</span><span class="sxs-lookup"><span data-stu-id="eded9-312">Default value toobe used when source doesn't match any keys.</span></span> <span data-ttu-id="eded9-313">可以是空字串 ("")。</span><span class="sxs-lookup"><span data-stu-id="eded9-313">Can be empty string ("").</span></span> |
| <span data-ttu-id="eded9-314">**key**</span><span class="sxs-lookup"><span data-stu-id="eded9-314">**key**</span></span> |<span data-ttu-id="eded9-315">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-315">Required</span></span> |<span data-ttu-id="eded9-316">String</span><span class="sxs-lookup"><span data-stu-id="eded9-316">String</span></span> |<span data-ttu-id="eded9-317">**索引鍵**toocompare**來源**具有值。</span><span class="sxs-lookup"><span data-stu-id="eded9-317">**Key** toocompare **source** value with.</span></span> |
| <span data-ttu-id="eded9-318">**value**</span><span class="sxs-lookup"><span data-stu-id="eded9-318">**value**</span></span> |<span data-ttu-id="eded9-319">必要</span><span class="sxs-lookup"><span data-stu-id="eded9-319">Required</span></span> |<span data-ttu-id="eded9-320">String</span><span class="sxs-lookup"><span data-stu-id="eded9-320">String</span></span> |<span data-ttu-id="eded9-321">取代值 hello**來源**hello 相符的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="eded9-321">Replacement value for hello **source** matching hello key.</span></span> |

## <a name="examples"></a><span data-ttu-id="eded9-322">範例</span><span class="sxs-lookup"><span data-stu-id="eded9-322">Examples</span></span>
### <a name="strip-known-domain-name"></a><span data-ttu-id="eded9-323">刪去已知的網域名稱</span><span class="sxs-lookup"><span data-stu-id="eded9-323">Strip known domain name</span></span>
<span data-ttu-id="eded9-324">您需要 toostrip 從使用者的電子郵件 tooobtain 使用者名稱的已知的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="eded9-324">You need toostrip a known domain name from a user’s email tooobtain a user name.</span></span> <br>
<span data-ttu-id="eded9-325">例如，如果"contoso.com"hello 網域，您可以使用下列運算式 hello:</span><span class="sxs-lookup"><span data-stu-id="eded9-325">For example, if hello domain is "contoso.com", then you could use hello following expression:</span></span>

<span data-ttu-id="eded9-326">**運算式：**</span><span class="sxs-lookup"><span data-stu-id="eded9-326">**Expression:**</span></span> <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

<span data-ttu-id="eded9-327">**範例輸入/輸出：**</span><span class="sxs-lookup"><span data-stu-id="eded9-327">**Sample input / output:**</span></span> <br>

* <span data-ttu-id="eded9-328">**輸入** (mail)："john.doe@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="eded9-328">**INPUT** (mail): "john.doe@contoso.com"</span></span>
* <span data-ttu-id="eded9-329">**輸出**："john.doe"</span><span class="sxs-lookup"><span data-stu-id="eded9-329">**OUTPUT**:  "john.doe"</span></span>

### <a name="append-constant-suffix-toouser-name"></a><span data-ttu-id="eded9-330">附加常數後置詞 toouser 名稱</span><span class="sxs-lookup"><span data-stu-id="eded9-330">Append constant suffix toouser name</span></span>
<span data-ttu-id="eded9-331">如果您使用 Salesforce 沙箱，您可能需要其他尾碼 tooall tooappend 您的使用者名稱才能同步處理它們。</span><span class="sxs-lookup"><span data-stu-id="eded9-331">If you are using a Salesforce Sandbox, you might need tooappend an additional suffix tooall your user names before synchronizing them.</span></span>

<span data-ttu-id="eded9-332">**運算式：**</span><span class="sxs-lookup"><span data-stu-id="eded9-332">**Expression:**</span></span> <br>
`Append([userPrincipalName], ".test"))`

<span data-ttu-id="eded9-333">**範例輸入/輸出：**</span><span class="sxs-lookup"><span data-stu-id="eded9-333">**Sample input/output:**</span></span> <br>

* <span data-ttu-id="eded9-334">**輸入**：(userPrincipalName)："John.Doe@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="eded9-334">**INPUT**: (userPrincipalName): "John.Doe@contoso.com"</span></span>
* <span data-ttu-id="eded9-335">**輸出**："John.Doe@contoso.com.test"</span><span class="sxs-lookup"><span data-stu-id="eded9-335">**OUTPUT**:  "John.Doe@contoso.com.test"</span></span>

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a><span data-ttu-id="eded9-336">串連部分名字和姓氏產生使用者別名</span><span class="sxs-lookup"><span data-stu-id="eded9-336">Generate user alias by concatenating parts of first and last name</span></span>
<span data-ttu-id="eded9-337">您必須利用使用者名字的前 3 個字母和使用者的姓氏的前 5 個字母的 toogenerate 使用者別名。</span><span class="sxs-lookup"><span data-stu-id="eded9-337">You need toogenerate a user alias by taking first 3 letters of user's first name and first 5 letters of user's last name.</span></span>

<span data-ttu-id="eded9-338">**運算式：**</span><span class="sxs-lookup"><span data-stu-id="eded9-338">**Expression:**</span></span> <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

<span data-ttu-id="eded9-339">**範例輸入/輸出：**</span><span class="sxs-lookup"><span data-stu-id="eded9-339">**Sample input/output:**</span></span> <br>

* <span data-ttu-id="eded9-340">**輸入** (givenName)："John"</span><span class="sxs-lookup"><span data-stu-id="eded9-340">**INPUT** (givenName): "John"</span></span>
* <span data-ttu-id="eded9-341">**輸入** (surname)："Doe"</span><span class="sxs-lookup"><span data-stu-id="eded9-341">**INPUT** (surname): "Doe"</span></span>
* <span data-ttu-id="eded9-342">**輸出**："JohDoe"</span><span class="sxs-lookup"><span data-stu-id="eded9-342">**OUTPUT**:  "JohDoe"</span></span>

### <a name="output-date-as-a-string-in-a-certain-format"></a><span data-ttu-id="eded9-343">以特定格式將日期輸出為字串</span><span class="sxs-lookup"><span data-stu-id="eded9-343">Output date as a string in a certain format</span></span>
<span data-ttu-id="eded9-344">您想 toosend 日期 tooa SaaS 應用程式的特定格式。</span><span class="sxs-lookup"><span data-stu-id="eded9-344">You want toosend dates tooa SaaS application in a certain format.</span></span> <br>
<span data-ttu-id="eded9-345">例如，您會想 tooformat 日期 servicenow。</span><span class="sxs-lookup"><span data-stu-id="eded9-345">For example, you want tooformat dates for ServiceNow.</span></span>

<span data-ttu-id="eded9-346">**運算式：**</span><span class="sxs-lookup"><span data-stu-id="eded9-346">**Expression:**</span></span> <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

<span data-ttu-id="eded9-347">**範例輸入/輸出：**</span><span class="sxs-lookup"><span data-stu-id="eded9-347">**Sample input/output:**</span></span>

* <span data-ttu-id="eded9-348">**輸入** (extensionAttribute1)："20150123105347.1Z"</span><span class="sxs-lookup"><span data-stu-id="eded9-348">**INPUT** (extensionAttribute1): "20150123105347.1Z"</span></span>
* <span data-ttu-id="eded9-349">**輸出**："2015-01-23"</span><span class="sxs-lookup"><span data-stu-id="eded9-349">**OUTPUT**:  "2015-01-23"</span></span>

### <a name="replace-a-value-based-on-predefined-set-of-options"></a><span data-ttu-id="eded9-350">根據預先定義的一組選項取代值</span><span class="sxs-lookup"><span data-stu-id="eded9-350">Replace a value based on predefined set of options</span></span>
<span data-ttu-id="eded9-351">您需要 toodefine hello 的時區時間 hello 使用者儲存在 Azure AD 中的 hello 狀態碼為基礎。</span><span class="sxs-lookup"><span data-stu-id="eded9-351">You need toodefine hello time zone of hello user based on hello state code stored in Azure AD.</span></span> <br>
<span data-ttu-id="eded9-352">如果 hello 狀態碼不符合任何預先定義的 hello 選項，使用預設值是"Australia/Sydney"。</span><span class="sxs-lookup"><span data-stu-id="eded9-352">If hello state code doesn't match any of hello predefined options, use default value of "Australia/Sydney".</span></span>

<span data-ttu-id="eded9-353">**運算式：**</span><span class="sxs-lookup"><span data-stu-id="eded9-353">**Expression:**</span></span> <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

<span data-ttu-id="eded9-354">**範例輸入/輸出：**</span><span class="sxs-lookup"><span data-stu-id="eded9-354">**Sample input/output:**</span></span>

* <span data-ttu-id="eded9-355">**輸入** (state)："QLD"</span><span class="sxs-lookup"><span data-stu-id="eded9-355">**INPUT** (state): "QLD"</span></span>
* <span data-ttu-id="eded9-356">**輸出**："Australia/Brisbane"</span><span class="sxs-lookup"><span data-stu-id="eded9-356">**OUTPUT**: "Australia/Brisbane"</span></span>

## <a name="related-articles"></a><span data-ttu-id="eded9-357">相關文章</span><span class="sxs-lookup"><span data-stu-id="eded9-357">Related Articles</span></span>
* [<span data-ttu-id="eded9-358">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="eded9-358">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="eded9-359">自動化使用者佈建/取消佈建 tooSaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="eded9-359">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="eded9-360">自訂使用者佈建的屬性對應</span><span class="sxs-lookup"><span data-stu-id="eded9-360">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="eded9-361">適用於使用者佈建的範圍篩選器</span><span class="sxs-lookup"><span data-stu-id="eded9-361">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="eded9-362">使用 SCIM tooenable 自動佈建的 Azure Active Directory tooapplications 來自使用者和群組</span><span class="sxs-lookup"><span data-stu-id="eded9-362">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="eded9-363">帳戶佈建通知</span><span class="sxs-lookup"><span data-stu-id="eded9-363">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="eded9-364">如何教學課程清單 tooIntegrate SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="eded9-364">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)


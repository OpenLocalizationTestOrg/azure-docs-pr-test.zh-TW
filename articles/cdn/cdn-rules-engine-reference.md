---
title: "Azure CDN 規則引擎參考 | Microsoft Docs"
description: "Azure CDN 規則引擎比對條件和功能的參考文件。"
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: c10145661a8c575381493c9aaa901c3ef92c2e81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cdn-rules-engine"></a><span data-ttu-id="53305-103">Azure CDN 規則引擎</span><span class="sxs-lookup"><span data-stu-id="53305-103">Azure CDN rules engine</span></span>
<span data-ttu-id="53305-104">本主題會針對 Azure 內容傳遞網路 (CDN) [規則引擎](cdn-rules-engine.md)列出可用比對條件和功能的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="53305-104">This topic lists detailed descriptions of the available match conditions and features for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="53305-105">HTTP 規則引擎是設計為特定類型要求如何由 CDN 處理的最終授權。</span><span class="sxs-lookup"><span data-stu-id="53305-105">The HTTP Rules Engine is designed to be the final authority on how specific types of requests are processed by the CDN.</span></span>

<span data-ttu-id="53305-106">**常見用途**：</span><span class="sxs-lookup"><span data-stu-id="53305-106">**Common uses**:</span></span>

- <span data-ttu-id="53305-107">覆寫或定義自訂快取原則。</span><span class="sxs-lookup"><span data-stu-id="53305-107">Override or define a custom cache policy.</span></span>
- <span data-ttu-id="53305-108">保護或拒絕機密內容的要求。</span><span class="sxs-lookup"><span data-stu-id="53305-108">Secure or deny requests for sensitive content.</span></span>
- <span data-ttu-id="53305-109">將要求重新導向。</span><span class="sxs-lookup"><span data-stu-id="53305-109">Redirect requests.</span></span>
- <span data-ttu-id="53305-110">儲存自訂記錄檔資料。</span><span class="sxs-lookup"><span data-stu-id="53305-110">Store custom log data.</span></span>

## <a name="terminology"></a><span data-ttu-id="53305-111">術語</span><span class="sxs-lookup"><span data-stu-id="53305-111">Terminology</span></span>
<span data-ttu-id="53305-112">規則是透過使用[**條件運算式**](cdn-rules-engine-reference-conditional-expressions.md)、[**比對**](cdn-rules-engine-reference-match-conditions.md)和[**功能**](cdn-rules-engine-reference-features.md)定義。</span><span class="sxs-lookup"><span data-stu-id="53305-112">A rule is defined through the use of [**conditional expressions**](cdn-rules-engine-reference-conditional-expressions.md), [**matches**](cdn-rules-engine-reference-match-conditions.md), and [**features**](cdn-rules-engine-reference-features.md).</span></span> <span data-ttu-id="53305-113">這些元素會在下圖中反白顯示。</span><span class="sxs-lookup"><span data-stu-id="53305-113">These elements are highlighted in the following illustration.</span></span>

 ![CDN 相符條件](./media/cdn-rules-engine-reference/cdn-rules-engine-terminology.png)

## <a name="syntax"></a><span data-ttu-id="53305-115">語法</span><span class="sxs-lookup"><span data-stu-id="53305-115">Syntax</span></span>

<span data-ttu-id="53305-116">處理特殊字元的方式會根據比對條件或功能如何處理文字值而異。</span><span class="sxs-lookup"><span data-stu-id="53305-116">The manner in which special characters will be treated varies according to how a match condition or feature handles text values.</span></span> <span data-ttu-id="53305-117">比對條件或功能可能會以下列其中一種方式解譯文字︰</span><span class="sxs-lookup"><span data-stu-id="53305-117">A match condition or feature may interpret text in one of the following ways:</span></span>

1. [<span data-ttu-id="53305-118">**常值**</span><span class="sxs-lookup"><span data-stu-id="53305-118">**Literal Values**</span></span>](#literal-values) 
2. [<span data-ttu-id="53305-119">**萬用字元值**</span><span class="sxs-lookup"><span data-stu-id="53305-119">**Wildcard Values**</span></span>](#wildcard-values)
3. [<span data-ttu-id="53305-120">**規則運算式**</span><span class="sxs-lookup"><span data-stu-id="53305-120">**Regular Expressions**</span></span>](#regular-expressions)

### <a name="literal-values"></a><span data-ttu-id="53305-121">常值</span><span class="sxs-lookup"><span data-stu-id="53305-121">Literal Values</span></span>
<span data-ttu-id="53305-122">解譯為常值的文字會將所有特殊字元 (除了 % 符號之外)，視為必須符合值的一部分。</span><span class="sxs-lookup"><span data-stu-id="53305-122">Text that is interpreted as a literal value will treat all special characters, with the exception of the % symbol, as a part of the value that must be matched.</span></span> <span data-ttu-id="53305-123">換句話說，常值比對條件設定為 `\'*'\`，只會在找到確切值時 (亦即，`\'*'\`) 獲得滿足。</span><span class="sxs-lookup"><span data-stu-id="53305-123">In other words, a literal match condition set to `\'*'\` will only be satisfied when that exact value (i.e., `\'*'\`) is found.</span></span>
 
<span data-ttu-id="53305-124">百分比符號是用來表示 URL 編碼 (例如 `%20`)。</span><span class="sxs-lookup"><span data-stu-id="53305-124">A percentage symbol is used to indicate URL encoding (e.g., `%20`).</span></span>

### <a name="wildcard-values"></a><span data-ttu-id="53305-125">萬用字元值</span><span class="sxs-lookup"><span data-stu-id="53305-125">Wildcard Values</span></span>
<span data-ttu-id="53305-126">解譯為萬用字元值的文字會將額外意義指派給特殊字元。</span><span class="sxs-lookup"><span data-stu-id="53305-126">Text that is interpreted as a wildcard value will assign additional meaning to special characters.</span></span> <span data-ttu-id="53305-127">下表描述如何解譯下列字元集。</span><span class="sxs-lookup"><span data-stu-id="53305-127">The following table describes how the following set of characters will be interpreted.</span></span>

<span data-ttu-id="53305-128">Character</span><span class="sxs-lookup"><span data-stu-id="53305-128">Character</span></span> | <span data-ttu-id="53305-129">說明</span><span class="sxs-lookup"><span data-stu-id="53305-129">Description</span></span>
----------|------------
\ | <span data-ttu-id="53305-130">反斜線是用來逸出此資料表中指定的任何字元。</span><span class="sxs-lookup"><span data-stu-id="53305-130">A backslash is used to escape any of the characters specified in this table.</span></span> <span data-ttu-id="53305-131">必須在逸出特殊字元之前指定反斜線。</span><span class="sxs-lookup"><span data-stu-id="53305-131">A backslash must be specified directly before the special character that should be escaped.</span></span><br/><span data-ttu-id="53305-132">例如，下列語法逸出星號︰`\*`</span><span class="sxs-lookup"><span data-stu-id="53305-132">For example, the following syntax escapes an asterisk: `\*`</span></span>
% | <span data-ttu-id="53305-133">百分比符號是用來表示 URL 編碼 (例如 `%20`)。</span><span class="sxs-lookup"><span data-stu-id="53305-133">A percentage symbol is used to indicate URL encoding (e.g., `%20`).</span></span>
* | <span data-ttu-id="53305-134">星號為萬用字元，表示一或多個字元。</span><span class="sxs-lookup"><span data-stu-id="53305-134">An asterisk is a wildcard that represents one or more characters.</span></span>
<span data-ttu-id="53305-135">空白字元</span><span class="sxs-lookup"><span data-stu-id="53305-135">Space</span></span> | <span data-ttu-id="53305-136">空白字元，表示比對條件可能藉由指定值或模式獲得滿足。</span><span class="sxs-lookup"><span data-stu-id="53305-136">A space character indicates that a match condition may be satisfied by either of the specified values or patterns.</span></span>
<span data-ttu-id="53305-137">'value'</span><span class="sxs-lookup"><span data-stu-id="53305-137">'value'</span></span> | <span data-ttu-id="53305-138">單引號不具有特殊意義。</span><span class="sxs-lookup"><span data-stu-id="53305-138">A single quote does not have special meaning.</span></span> <span data-ttu-id="53305-139">不過，單引號組是用來表示值應視為常值。</span><span class="sxs-lookup"><span data-stu-id="53305-139">However, a set of single quotes is used to indicate that a value should be treated as a literal value.</span></span> <span data-ttu-id="53305-140">使用方式如下：</span><span class="sxs-lookup"><span data-stu-id="53305-140">It can be used in the following ways:</span></span><br><br/><span data-ttu-id="53305-141">- 它可讓比對條件在指定值符合比較值的任何部分時獲得滿足。</span><span class="sxs-lookup"><span data-stu-id="53305-141">- It allows a match condition to be satisfied whenever the specified value matches any portion of the comparison value.</span></span>  <span data-ttu-id="53305-142">例如，`'ma'` 會比對下列任何字串︰</span><span class="sxs-lookup"><span data-stu-id="53305-142">For example, `'ma'` would match any of the following strings:</span></span> <br/><br/><span data-ttu-id="53305-143">/business/**ma**rathon/asset.htm</span><span class="sxs-lookup"><span data-stu-id="53305-143">/business/**ma**rathon/asset.htm</span></span><br/><span data-ttu-id="53305-144">**ma**p.gif</span><span class="sxs-lookup"><span data-stu-id="53305-144">**ma**p.gif</span></span><br/><span data-ttu-id="53305-145">/business/template.**ma**p</span><span class="sxs-lookup"><span data-stu-id="53305-145">/business/template.**ma**p</span></span><br /><br /><span data-ttu-id="53305-146">- 它可讓特殊字元指定為常值字元。</span><span class="sxs-lookup"><span data-stu-id="53305-146">- It allows a special character to be specified as a literal character.</span></span> <span data-ttu-id="53305-147">例如，您可以指定常值空白字元，方法是在單引號組內括住空白字元 (亦即，`' '` 或 `'sample value'`)。</span><span class="sxs-lookup"><span data-stu-id="53305-147">For example, you may specify a literal space character by enclosing a space character within a set of single quotes (i.e., `' '` or `'sample value'`).</span></span><br/><span data-ttu-id="53305-148">- 它可以指定空白值。</span><span class="sxs-lookup"><span data-stu-id="53305-148">- It allows a blank value to be specified.</span></span> <span data-ttu-id="53305-149">藉由指定單引號組來指定空白值 (亦即，'')。</span><span class="sxs-lookup"><span data-stu-id="53305-149">Specify a blank value by specifying a set of single quotes (i.e., '').</span></span><br /><br/><span data-ttu-id="53305-150">**重要事項：**</span><span class="sxs-lookup"><span data-stu-id="53305-150">**Important:**</span></span><br/><span data-ttu-id="53305-151">- 如果指定值不包含萬用字元，則它會自動被視為常值。</span><span class="sxs-lookup"><span data-stu-id="53305-151">- If the specified value does not contain a wildcard, then it will automatically be considered a literal value.</span></span> <span data-ttu-id="53305-152">這表示不需要指定單引號組。</span><span class="sxs-lookup"><span data-stu-id="53305-152">This means that it is not necessary to specify a set of single quotes.</span></span><br/><span data-ttu-id="53305-153">- 如果反斜線不會逸出此資料表中的另一個字元，則它將會在於單引號組內指定時被忽略。</span><span class="sxs-lookup"><span data-stu-id="53305-153">- If a backslash does not escape another character in this table, then it will be ignored when specified within a set of single quotes.</span></span><br/><span data-ttu-id="53305-154">- 另一種將特殊字元指定為常值字元的方式是使用反斜線逸出它 (亦即，`\`)。</span><span class="sxs-lookup"><span data-stu-id="53305-154">- Another way to specify a special character as a literal character is to escape it using a backslash (i.e., `\`).</span></span>

### <a name="regular-expressions"></a><span data-ttu-id="53305-155">規則運算式</span><span class="sxs-lookup"><span data-stu-id="53305-155">Regular Expressions</span></span>

<span data-ttu-id="53305-156">規則運算式會定義要在文字值中搜尋的模式。</span><span class="sxs-lookup"><span data-stu-id="53305-156">Regular expressions define a pattern that will be searched for within a text value.</span></span> <span data-ttu-id="53305-157">規則運算式標記法會將特定意義定義為各種符號。</span><span class="sxs-lookup"><span data-stu-id="53305-157">Regular expression notation defines specific meanings to a variety of symbols.</span></span> <span data-ttu-id="53305-158">下表指出支援規則運算式的比對條件和功能如何處理特殊字元。</span><span class="sxs-lookup"><span data-stu-id="53305-158">The following table indicates how special characters are treated by match conditions and features that support regular expressions.</span></span>

<span data-ttu-id="53305-159">特殊字元</span><span class="sxs-lookup"><span data-stu-id="53305-159">Special Character</span></span> | <span data-ttu-id="53305-160">說明</span><span class="sxs-lookup"><span data-stu-id="53305-160">Description</span></span>
------------------|------------
\ | <span data-ttu-id="53305-161">反斜線會逸出它後面接續的字元。</span><span class="sxs-lookup"><span data-stu-id="53305-161">A backslash escapes the character the follows it.</span></span> <span data-ttu-id="53305-162">這會導致該字元被視為常值，而非採用它的規則運算式的意義。</span><span class="sxs-lookup"><span data-stu-id="53305-162">This causes that character to be treated as a literal value instead of taking on its regular expression meaning.</span></span> <span data-ttu-id="53305-163">例如，下列語法逸出星號︰`\*`</span><span class="sxs-lookup"><span data-stu-id="53305-163">For example, the following syntax escapes an asterisk: `\*`</span></span>
% | <span data-ttu-id="53305-164">百分比符號的意義取決於其使用方式。</span><span class="sxs-lookup"><span data-stu-id="53305-164">The meaning of a percentage symbol depends on its usage.</span></span><br/><br/> <span data-ttu-id="53305-165">`%{HTTPVariable}`︰這個語法會識別 HTTP 變數。</span><span class="sxs-lookup"><span data-stu-id="53305-165">`%{HTTPVariable}`: This syntax identifies an HTTP variable.</span></span><br/><span data-ttu-id="53305-166">`%{HTTPVariable%Pattern}`︰這個語法會使用百分比符號來識別 HTTP 變數，並做為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="53305-166">`%{HTTPVariable%Pattern}`: This syntax uses a percentage symbol to identify an HTTP variable and as a delimiter.</span></span><br /><span data-ttu-id="53305-167">`\%`︰逸出百分比符號可以讓它可用來做為常值，或表示 URL 編碼 (例如 `\%20`)。</span><span class="sxs-lookup"><span data-stu-id="53305-167">`\%`: Escaping a percentage symbol allows it to be used as a literal value or to indicate URL encoding (e.g., `\%20`).</span></span>
* | <span data-ttu-id="53305-168">星號可讓前置字元比對零或多次。</span><span class="sxs-lookup"><span data-stu-id="53305-168">An asterisk allows the preceding character to be matched zero or more times.</span></span> 
<span data-ttu-id="53305-169">空白字元</span><span class="sxs-lookup"><span data-stu-id="53305-169">Space</span></span> | <span data-ttu-id="53305-170">空白字元通常會被視為常值字元。</span><span class="sxs-lookup"><span data-stu-id="53305-170">A space character is typically treated as a literal character.</span></span> 
<span data-ttu-id="53305-171">'value'</span><span class="sxs-lookup"><span data-stu-id="53305-171">'value'</span></span> | <span data-ttu-id="53305-172">單引號會被視為常值字元。</span><span class="sxs-lookup"><span data-stu-id="53305-172">Single quotes are treated as literal characters.</span></span> <span data-ttu-id="53305-173">單引號組不具有特殊意義。</span><span class="sxs-lookup"><span data-stu-id="53305-173">A set of single quotes does not have special meaning.</span></span>


## <a name="next-steps"></a><span data-ttu-id="53305-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53305-174">Next steps</span></span>
* [<span data-ttu-id="53305-175">規則引擎比對條件</span><span class="sxs-lookup"><span data-stu-id="53305-175">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="53305-176">規則引擎條件運算式</span><span class="sxs-lookup"><span data-stu-id="53305-176">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="53305-177">規則引擎功能</span><span class="sxs-lookup"><span data-stu-id="53305-177">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="53305-178">使用規則引擎覆寫預設的 HTTP 行為</span><span class="sxs-lookup"><span data-stu-id="53305-178">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
* [<span data-ttu-id="53305-179">Azure CDN 概觀</span><span class="sxs-lookup"><span data-stu-id="53305-179">Azure CDN Overview</span></span>](cdn-overview.md)

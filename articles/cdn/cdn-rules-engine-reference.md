---
title: "aaaAzure CDN 規則引擎參考 |Microsoft 文件"
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
ms.openlocfilehash: 4159715d15fc792afb49dcd2a30752fabcd94a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine"></a><span data-ttu-id="696b7-103">Azure CDN 規則引擎</span><span class="sxs-lookup"><span data-stu-id="696b7-103">Azure CDN rules engine</span></span>
<span data-ttu-id="696b7-104">本主題列出的詳細的描述 hello 可比對條件和功能的 Azure 內容傳遞網路 (CDN)[規則引擎](cdn-rules-engine.md)。</span><span class="sxs-lookup"><span data-stu-id="696b7-104">This topic lists detailed descriptions of hello available match conditions and features for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="696b7-105">hello HTTP 規則引擎已設計的 toobe hello 最終授權單位上如何特定類型的要求處理 hello CDN。</span><span class="sxs-lookup"><span data-stu-id="696b7-105">hello HTTP Rules Engine is designed toobe hello final authority on how specific types of requests are processed by hello CDN.</span></span>

<span data-ttu-id="696b7-106">**常見用途**：</span><span class="sxs-lookup"><span data-stu-id="696b7-106">**Common uses**:</span></span>

- <span data-ttu-id="696b7-107">覆寫或定義自訂快取原則。</span><span class="sxs-lookup"><span data-stu-id="696b7-107">Override or define a custom cache policy.</span></span>
- <span data-ttu-id="696b7-108">保護或拒絕機密內容的要求。</span><span class="sxs-lookup"><span data-stu-id="696b7-108">Secure or deny requests for sensitive content.</span></span>
- <span data-ttu-id="696b7-109">將要求重新導向。</span><span class="sxs-lookup"><span data-stu-id="696b7-109">Redirect requests.</span></span>
- <span data-ttu-id="696b7-110">儲存自訂記錄檔資料。</span><span class="sxs-lookup"><span data-stu-id="696b7-110">Store custom log data.</span></span>

## <a name="terminology"></a><span data-ttu-id="696b7-111">術語</span><span class="sxs-lookup"><span data-stu-id="696b7-111">Terminology</span></span>
<span data-ttu-id="696b7-112">藉由使用 hello 定義規則[**條件運算式**](cdn-rules-engine-reference-conditional-expressions.md)， [**符合**](cdn-rules-engine-reference-match-conditions.md)，和[ **功能**](cdn-rules-engine-reference-features.md)。</span><span class="sxs-lookup"><span data-stu-id="696b7-112">A rule is defined through hello use of [**conditional expressions**](cdn-rules-engine-reference-conditional-expressions.md), [**matches**](cdn-rules-engine-reference-match-conditions.md), and [**features**](cdn-rules-engine-reference-features.md).</span></span> <span data-ttu-id="696b7-113">這些項目會在 hello 遵循圖中反白顯示。</span><span class="sxs-lookup"><span data-stu-id="696b7-113">These elements are highlighted in hello following illustration.</span></span>

 ![CDN 相符條件](./media/cdn-rules-engine-reference/cdn-rules-engine-terminology.png)

## <a name="syntax"></a><span data-ttu-id="696b7-115">語法</span><span class="sxs-lookup"><span data-stu-id="696b7-115">Syntax</span></span>

<span data-ttu-id="696b7-116">相應 toohow 相符或功能的控制代碼的文字值，會將用來處理特殊字元的 hello 方式各不相同。</span><span class="sxs-lookup"><span data-stu-id="696b7-116">hello manner in which special characters will be treated varies according toohow a match condition or feature handles text values.</span></span> <span data-ttu-id="696b7-117">比對條件或功能，可能會將解譯其中一種下列方法的 hello 文字：</span><span class="sxs-lookup"><span data-stu-id="696b7-117">A match condition or feature may interpret text in one of hello following ways:</span></span>

1. [<span data-ttu-id="696b7-118">**常值**</span><span class="sxs-lookup"><span data-stu-id="696b7-118">**Literal Values**</span></span>](#literal-values) 
2. [<span data-ttu-id="696b7-119">**萬用字元值**</span><span class="sxs-lookup"><span data-stu-id="696b7-119">**Wildcard Values**</span></span>](#wildcard-values)
3. [<span data-ttu-id="696b7-120">**規則運算式**</span><span class="sxs-lookup"><span data-stu-id="696b7-120">**Regular Expressions**</span></span>](#regular-expressions)

### <a name="literal-values"></a><span data-ttu-id="696b7-121">常值</span><span class="sxs-lookup"><span data-stu-id="696b7-121">Literal Values</span></span>
<span data-ttu-id="696b7-122">解譯為常值的文字會將所有的特殊字元，與 hello 例外狀況的 hello %符號，視為 hello 值必須符合的一部分。</span><span class="sxs-lookup"><span data-stu-id="696b7-122">Text that is interpreted as a literal value will treat all special characters, with hello exception of hello % symbol, as a part of hello value that must be matched.</span></span> <span data-ttu-id="696b7-123">換句話說，常值符合條件設定得`\'*'\`只而得以滿足時，確切的值 (亦即， `\'*'\`) 找到。</span><span class="sxs-lookup"><span data-stu-id="696b7-123">In other words, a literal match condition set too`\'*'\` will only be satisfied when that exact value (i.e., `\'*'\`) is found.</span></span>
 
<span data-ttu-id="696b7-124">百分比符號是使用的 tooindicate URL 編碼方式 (例如`%20`)。</span><span class="sxs-lookup"><span data-stu-id="696b7-124">A percentage symbol is used tooindicate URL encoding (e.g., `%20`).</span></span>

### <a name="wildcard-values"></a><span data-ttu-id="696b7-125">萬用字元值</span><span class="sxs-lookup"><span data-stu-id="696b7-125">Wildcard Values</span></span>
<span data-ttu-id="696b7-126">文字會解譯為萬用字元值，將會指派額外的意義 toospecial 字元。</span><span class="sxs-lookup"><span data-stu-id="696b7-126">Text that is interpreted as a wildcard value will assign additional meaning toospecial characters.</span></span> <span data-ttu-id="696b7-127">hello 下表描述 hello 遵循一組字元解譯的方式。</span><span class="sxs-lookup"><span data-stu-id="696b7-127">hello following table describes how hello following set of characters will be interpreted.</span></span>

<span data-ttu-id="696b7-128">Character</span><span class="sxs-lookup"><span data-stu-id="696b7-128">Character</span></span> | <span data-ttu-id="696b7-129">說明</span><span class="sxs-lookup"><span data-stu-id="696b7-129">Description</span></span>
----------|------------
\ | <span data-ttu-id="696b7-130">使用的 tooescape hello 字元指定此資料表中的反斜線。</span><span class="sxs-lookup"><span data-stu-id="696b7-130">A backslash is used tooescape any of hello characters specified in this table.</span></span> <span data-ttu-id="696b7-131">Hello 應該逸出的特殊字元必須先指定直接反斜線。</span><span class="sxs-lookup"><span data-stu-id="696b7-131">A backslash must be specified directly before hello special character that should be escaped.</span></span><br/><span data-ttu-id="696b7-132">例如，請使用下列語法的 hello 逸出星號：`\*`</span><span class="sxs-lookup"><span data-stu-id="696b7-132">For example, hello following syntax escapes an asterisk: `\*`</span></span>
% | <span data-ttu-id="696b7-133">百分比符號是使用的 tooindicate URL 編碼方式 (例如`%20`)。</span><span class="sxs-lookup"><span data-stu-id="696b7-133">A percentage symbol is used tooindicate URL encoding (e.g., `%20`).</span></span>
* | <span data-ttu-id="696b7-134">星號為萬用字元，表示一或多個字元。</span><span class="sxs-lookup"><span data-stu-id="696b7-134">An asterisk is a wildcard that represents one or more characters.</span></span>
<span data-ttu-id="696b7-135">空白字元</span><span class="sxs-lookup"><span data-stu-id="696b7-135">Space</span></span> | <span data-ttu-id="696b7-136">空格字元，表示可能會透過其中一種指定 hello 中滿足比對條件值或模式。</span><span class="sxs-lookup"><span data-stu-id="696b7-136">A space character indicates that a match condition may be satisfied by either of hello specified values or patterns.</span></span>
<span data-ttu-id="696b7-137">'value'</span><span class="sxs-lookup"><span data-stu-id="696b7-137">'value'</span></span> | <span data-ttu-id="696b7-138">單引號不具有特殊意義。</span><span class="sxs-lookup"><span data-stu-id="696b7-138">A single quote does not have special meaning.</span></span> <span data-ttu-id="696b7-139">不過，會使用一組單引號 tooindicate 值應該被視為常值。</span><span class="sxs-lookup"><span data-stu-id="696b7-139">However, a set of single quotes is used tooindicate that a value should be treated as a literal value.</span></span> <span data-ttu-id="696b7-140">它可以用於下列方式 hello:</span><span class="sxs-lookup"><span data-stu-id="696b7-140">It can be used in hello following ways:</span></span><br><br/><span data-ttu-id="696b7-141">-它可讓比對條件 toobe 滿足只要 hello 指定的值符合 hello 比較值的任何部分。</span><span class="sxs-lookup"><span data-stu-id="696b7-141">- It allows a match condition toobe satisfied whenever hello specified value matches any portion of hello comparison value.</span></span>  <span data-ttu-id="696b7-142">例如，`'ma'`會符合任何 hello 下列字串：</span><span class="sxs-lookup"><span data-stu-id="696b7-142">For example, `'ma'` would match any of hello following strings:</span></span> <br/><br/><span data-ttu-id="696b7-143">/business/**ma**rathon/asset.htm</span><span class="sxs-lookup"><span data-stu-id="696b7-143">/business/**ma**rathon/asset.htm</span></span><br/><span data-ttu-id="696b7-144">**ma**p.gif</span><span class="sxs-lookup"><span data-stu-id="696b7-144">**ma**p.gif</span></span><br/><span data-ttu-id="696b7-145">/business/template.**ma**p</span><span class="sxs-lookup"><span data-stu-id="696b7-145">/business/template.**ma**p</span></span><br /><br /><span data-ttu-id="696b7-146">-它可讓特殊字元 toobe 指定為常值字元。</span><span class="sxs-lookup"><span data-stu-id="696b7-146">- It allows a special character toobe specified as a literal character.</span></span> <span data-ttu-id="696b7-147">例如，您可以指定常值空白字元，方法是在單引號組內括住空白字元 (亦即，`' '` 或 `'sample value'`)。</span><span class="sxs-lookup"><span data-stu-id="696b7-147">For example, you may specify a literal space character by enclosing a space character within a set of single quotes (i.e., `' '` or `'sample value'`).</span></span><br/><span data-ttu-id="696b7-148">-它可讓指定空白值 toobe。</span><span class="sxs-lookup"><span data-stu-id="696b7-148">- It allows a blank value toobe specified.</span></span> <span data-ttu-id="696b7-149">藉由指定單引號組來指定空白值 (亦即，'')。</span><span class="sxs-lookup"><span data-stu-id="696b7-149">Specify a blank value by specifying a set of single quotes (i.e., '').</span></span><br /><br/><span data-ttu-id="696b7-150">**重要事項：**</span><span class="sxs-lookup"><span data-stu-id="696b7-150">**Important:**</span></span><br/><span data-ttu-id="696b7-151">-如果 hello 指定值不包含萬用字元，然後它會自動被視為常值。</span><span class="sxs-lookup"><span data-stu-id="696b7-151">- If hello specified value does not contain a wildcard, then it will automatically be considered a literal value.</span></span> <span data-ttu-id="696b7-152">這表示它不是必要的 toospecify 方以單引號包住一組。</span><span class="sxs-lookup"><span data-stu-id="696b7-152">This means that it is not necessary toospecify a set of single quotes.</span></span><br/><span data-ttu-id="696b7-153">- 如果反斜線不會逸出此資料表中的另一個字元，則它將會在於單引號組內指定時被忽略。</span><span class="sxs-lookup"><span data-stu-id="696b7-153">- If a backslash does not escape another character in this table, then it will be ignored when specified within a set of single quotes.</span></span><br/><span data-ttu-id="696b7-154">為另一個方式 toospecify 做常值字元的特殊字元是 tooescape 使用反斜線 (亦即， `\`)。</span><span class="sxs-lookup"><span data-stu-id="696b7-154">- Another way toospecify a special character as a literal character is tooescape it using a backslash (i.e., `\`).</span></span>

### <a name="regular-expressions"></a><span data-ttu-id="696b7-155">規則運算式</span><span class="sxs-lookup"><span data-stu-id="696b7-155">Regular Expressions</span></span>

<span data-ttu-id="696b7-156">規則運算式會定義要在文字值中搜尋的模式。</span><span class="sxs-lookup"><span data-stu-id="696b7-156">Regular expressions define a pattern that will be searched for within a text value.</span></span> <span data-ttu-id="696b7-157">規則運算式標記法定義特定的意義 tooa 各種不同的符號。</span><span class="sxs-lookup"><span data-stu-id="696b7-157">Regular expression notation defines specific meanings tooa variety of symbols.</span></span> <span data-ttu-id="696b7-158">hello 下表指出如何特殊字元都會被比對條件和支援規則運算式的功能。</span><span class="sxs-lookup"><span data-stu-id="696b7-158">hello following table indicates how special characters are treated by match conditions and features that support regular expressions.</span></span>

<span data-ttu-id="696b7-159">特殊字元</span><span class="sxs-lookup"><span data-stu-id="696b7-159">Special Character</span></span> | <span data-ttu-id="696b7-160">說明</span><span class="sxs-lookup"><span data-stu-id="696b7-160">Description</span></span>
------------------|------------
\ | <span data-ttu-id="696b7-161">反斜線逸出 hello 字元 hello 在它後面。</span><span class="sxs-lookup"><span data-stu-id="696b7-161">A backslash escapes hello character hello follows it.</span></span> <span data-ttu-id="696b7-162">這會導致視為常值的值，而不會採取其規則運算式的意義上該字元 toobe。</span><span class="sxs-lookup"><span data-stu-id="696b7-162">This causes that character toobe treated as a literal value instead of taking on its regular expression meaning.</span></span> <span data-ttu-id="696b7-163">例如，請使用下列語法的 hello 逸出星號：`\*`</span><span class="sxs-lookup"><span data-stu-id="696b7-163">For example, hello following syntax escapes an asterisk: `\*`</span></span>
% | <span data-ttu-id="696b7-164">百分比符號的 hello 意義取決於其使用情形。</span><span class="sxs-lookup"><span data-stu-id="696b7-164">hello meaning of a percentage symbol depends on its usage.</span></span><br/><br/> <span data-ttu-id="696b7-165">`%{HTTPVariable}`︰這個語法會識別 HTTP 變數。</span><span class="sxs-lookup"><span data-stu-id="696b7-165">`%{HTTPVariable}`: This syntax identifies an HTTP variable.</span></span><br/><span data-ttu-id="696b7-166">`%{HTTPVariable%Pattern}`： 這個語法會使用百分比符號 tooidentify HTTP 變數以及做為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="696b7-166">`%{HTTPVariable%Pattern}`: This syntax uses a percentage symbol tooidentify an HTTP variable and as a delimiter.</span></span><br /><span data-ttu-id="696b7-167">`\%`： 逸出的百分比符號可讓它 toobe 做為常值或 tooindicate URL 編碼 (例如`\%20`)。</span><span class="sxs-lookup"><span data-stu-id="696b7-167">`\%`: Escaping a percentage symbol allows it toobe used as a literal value or tooindicate URL encoding (e.g., `\%20`).</span></span>
* | <span data-ttu-id="696b7-168">星號允許 hello 前置字元 toobe 比對零或多次。</span><span class="sxs-lookup"><span data-stu-id="696b7-168">An asterisk allows hello preceding character toobe matched zero or more times.</span></span> 
<span data-ttu-id="696b7-169">空白字元</span><span class="sxs-lookup"><span data-stu-id="696b7-169">Space</span></span> | <span data-ttu-id="696b7-170">空白字元通常會被視為常值字元。</span><span class="sxs-lookup"><span data-stu-id="696b7-170">A space character is typically treated as a literal character.</span></span> 
<span data-ttu-id="696b7-171">'value'</span><span class="sxs-lookup"><span data-stu-id="696b7-171">'value'</span></span> | <span data-ttu-id="696b7-172">單引號會被視為常值字元。</span><span class="sxs-lookup"><span data-stu-id="696b7-172">Single quotes are treated as literal characters.</span></span> <span data-ttu-id="696b7-173">單引號組不具有特殊意義。</span><span class="sxs-lookup"><span data-stu-id="696b7-173">A set of single quotes does not have special meaning.</span></span>


## <a name="next-steps"></a><span data-ttu-id="696b7-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="696b7-174">Next steps</span></span>
* [<span data-ttu-id="696b7-175">規則引擎比對條件</span><span class="sxs-lookup"><span data-stu-id="696b7-175">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="696b7-176">規則引擎條件運算式</span><span class="sxs-lookup"><span data-stu-id="696b7-176">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="696b7-177">規則引擎功能</span><span class="sxs-lookup"><span data-stu-id="696b7-177">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="696b7-178">覆寫使用 hello 規則引擎的預設 HTTP 行為</span><span class="sxs-lookup"><span data-stu-id="696b7-178">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* [<span data-ttu-id="696b7-179">Azure CDN 概觀</span><span class="sxs-lookup"><span data-stu-id="696b7-179">Azure CDN Overview</span></span>](cdn-overview.md)

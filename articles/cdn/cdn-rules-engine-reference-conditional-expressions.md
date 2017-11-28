---
title: "aaaAzure CDN 規則引擎的條件運算式 |Microsoft 文件"
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
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="c6576-103">Azure CDN 規則引擎條件運算式</span><span class="sxs-lookup"><span data-stu-id="c6576-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="c6576-104">本主題列出的詳細的描述 hello 條件運算式的 Azure 內容傳遞網路 (CDN)[規則引擎](cdn-rules-engine.md)。</span><span class="sxs-lookup"><span data-stu-id="c6576-104">This topic lists detailed descriptions of hello Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="c6576-105">規則 hello 第一個部分是 hello 條件運算式。</span><span class="sxs-lookup"><span data-stu-id="c6576-105">hello first part of a rule is hello Conditional Expression.</span></span>

<span data-ttu-id="c6576-106">條件運算式</span><span class="sxs-lookup"><span data-stu-id="c6576-106">Conditional Expression</span></span> | <span data-ttu-id="c6576-107">說明</span><span class="sxs-lookup"><span data-stu-id="c6576-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="c6576-108">IF</span><span class="sxs-lookup"><span data-stu-id="c6576-108">IF</span></span> | <span data-ttu-id="c6576-109">如果運算式永遠是 hello 規則中的第一個陳述式的一部分。</span><span class="sxs-lookup"><span data-stu-id="c6576-109">An IF expression is always a part of hello first statement in a rule.</span></span> <span data-ttu-id="c6576-110">像所有其他條件運算式一樣，此 IF 陳述式必須與符合項目相關聯。</span><span class="sxs-lookup"><span data-stu-id="c6576-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="c6576-111">如果不定義了任何額外的條件運算式，這個比對會決定一組功能可能會套用的 tooa 要求之前，必須符合的 hello 準則。</span><span class="sxs-lookup"><span data-stu-id="c6576-111">If no additional conditional expressions are defined, then this match determines hello criterion that must be met before a set of features may be applied tooa request.</span></span>
<span data-ttu-id="c6576-112">AND IF</span><span class="sxs-lookup"><span data-stu-id="c6576-112">AND IF</span></span> | <span data-ttu-id="c6576-113">表示運算式只能加入下列類型的條件運算式： 如果，表示 hello 之後。</span><span class="sxs-lookup"><span data-stu-id="c6576-113">An AND IF expression may only be added after hello following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="c6576-114">就表示另一個 hello 初始 IF 陳述式必須符合的條件。</span><span class="sxs-lookup"><span data-stu-id="c6576-114">It indicates that there is another condition that must be met for hello initial IF statement.</span></span>
<span data-ttu-id="c6576-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="c6576-115">ELSE IF</span></span>| <span data-ttu-id="c6576-116">ELSE IF 運算式指定的替代進行一組功能特定 toothis ELSE 的 IF 陳述式之前必須符合的條件。</span><span class="sxs-lookup"><span data-stu-id="c6576-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific toothis ELSE IF statement takes place.</span></span> <span data-ttu-id="c6576-117">hello 存在 ELSE 的 IF 陳述式表示 hello hello 前一個陳述式結尾。</span><span class="sxs-lookup"><span data-stu-id="c6576-117">hello presence of an ELSE IF statement indicates hello end of hello previous statement.</span></span> <span data-ttu-id="c6576-118">可能會放在 ELSE 的 IF 陳述式之後的 hello 只有條件式運算式是另一個 ELSE IF 陳述式。</span><span class="sxs-lookup"><span data-stu-id="c6576-118">hello only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="c6576-119">這表示 ELSE 的 IF 陳述式只可以使用的 toospecify 單一具有 toobe 符合其他條件。</span><span class="sxs-lookup"><span data-stu-id="c6576-119">This means that an ELSE IF statement may only be used toospecify a single additional condition that has toobe met.</span></span>

<span data-ttu-id="c6576-120">**範例**：![CDN 相符條件](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="c6576-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="c6576-121">後續的規則可能會覆寫先前規則所指定的 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="c6576-121">A subsequent rule may override hello actions specified by a previous rule.</span></span> <span data-ttu-id="c6576-122">範例︰全面涵蓋規則會保護所有透過以權杖為基礎的驗證要求。</span><span class="sxs-lookup"><span data-stu-id="c6576-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="c6576-123">另一個規則可能會建立它的下方 toomake 某些類型的要求的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c6576-123">Another rule may be created directly below it toomake an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="c6576-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6576-124">Next steps</span></span>
* [<span data-ttu-id="c6576-125">Azure CDN 概觀</span><span class="sxs-lookup"><span data-stu-id="c6576-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="c6576-126">規則引擎參考</span><span class="sxs-lookup"><span data-stu-id="c6576-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="c6576-127">規則引擎比對條件</span><span class="sxs-lookup"><span data-stu-id="c6576-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="c6576-128">規則引擎功能</span><span class="sxs-lookup"><span data-stu-id="c6576-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="c6576-129">覆寫使用 hello 規則引擎的預設 HTTP 行為</span><span class="sxs-lookup"><span data-stu-id="c6576-129">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)

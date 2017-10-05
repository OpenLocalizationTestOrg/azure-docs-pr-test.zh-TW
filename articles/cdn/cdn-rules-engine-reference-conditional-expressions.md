---
title: "Azure CDN 規則引擎條件運算式 | Microsoft Docs"
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
ms.openlocfilehash: 57e56c38e003cb83dcf44f455c4451d159db8a59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="54ec0-103">Azure CDN 規則引擎條件運算式</span><span class="sxs-lookup"><span data-stu-id="54ec0-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="54ec0-104">本主題會針對 Azure 內容傳遞網路 (CDN) [規則引擎](cdn-rules-engine.md)的條件運算式列出詳細說明。</span><span class="sxs-lookup"><span data-stu-id="54ec0-104">This topic lists detailed descriptions of the Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="54ec0-105">規則的第一個部分是條件運算式。</span><span class="sxs-lookup"><span data-stu-id="54ec0-105">The first part of a rule is the Conditional Expression.</span></span>

<span data-ttu-id="54ec0-106">條件運算式</span><span class="sxs-lookup"><span data-stu-id="54ec0-106">Conditional Expression</span></span> | <span data-ttu-id="54ec0-107">說明</span><span class="sxs-lookup"><span data-stu-id="54ec0-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="54ec0-108">IF</span><span class="sxs-lookup"><span data-stu-id="54ec0-108">IF</span></span> | <span data-ttu-id="54ec0-109">IF 運算式永遠是規則中第一個陳述式的一部分。</span><span class="sxs-lookup"><span data-stu-id="54ec0-109">An IF expression is always a part of the first statement in a rule.</span></span> <span data-ttu-id="54ec0-110">像所有其他條件運算式一樣，此 IF 陳述式必須與符合項目相關聯。</span><span class="sxs-lookup"><span data-stu-id="54ec0-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="54ec0-111">如果未定義其他條件運算式，則此相符項目會決定在將一組功能套用至要求之前必須符合的準則。</span><span class="sxs-lookup"><span data-stu-id="54ec0-111">If no additional conditional expressions are defined, then this match determines the criterion that must be met before a set of features may be applied to a request.</span></span>
<span data-ttu-id="54ec0-112">AND IF</span><span class="sxs-lookup"><span data-stu-id="54ec0-112">AND IF</span></span> | <span data-ttu-id="54ec0-113">AND IF 運算式只能在下列類型的條件運算式之後新增︰IF、AND IF。</span><span class="sxs-lookup"><span data-stu-id="54ec0-113">An AND IF expression may only be added after the following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="54ec0-114">它表示針對初始 IF 陳述式有必須符合的另一個條件。</span><span class="sxs-lookup"><span data-stu-id="54ec0-114">It indicates that there is another condition that must be met for the initial IF statement.</span></span>
<span data-ttu-id="54ec0-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="54ec0-115">ELSE IF</span></span>| <span data-ttu-id="54ec0-116">ELSE IF 運算式會指定其他條件，必須在此 ELSE IF 陳述式特定的一組功能發生之前符合。</span><span class="sxs-lookup"><span data-stu-id="54ec0-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific to this ELSE IF statement takes place.</span></span> <span data-ttu-id="54ec0-117">有 ELSE IF 陳述式表示前一個陳述式的結尾。</span><span class="sxs-lookup"><span data-stu-id="54ec0-117">The presence of an ELSE IF statement indicates the end of the previous statement.</span></span> <span data-ttu-id="54ec0-118">可以放在 ELSE IF 陳述式之後的條件運算式是另一個 ELSE IF 陳述式。</span><span class="sxs-lookup"><span data-stu-id="54ec0-118">The only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="54ec0-119">這表示 ELSE IF 陳述式只能用來指定必須符合的單一其他條件。</span><span class="sxs-lookup"><span data-stu-id="54ec0-119">This means that an ELSE IF statement may only be used to specify a single additional condition that has to be met.</span></span>

<span data-ttu-id="54ec0-120">**範例**：![CDN 相符條件](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="54ec0-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="54ec0-121">後一項規則可能會覆寫前一項規則所指定的動作。</span><span class="sxs-lookup"><span data-stu-id="54ec0-121">A subsequent rule may override the actions specified by a previous rule.</span></span> <span data-ttu-id="54ec0-122">範例︰全面涵蓋規則會保護所有透過以權杖為基礎的驗證要求。</span><span class="sxs-lookup"><span data-stu-id="54ec0-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="54ec0-123">可以直接在它底下建立另一個規則，對特定類型的要求產生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="54ec0-123">Another rule may be created directly below it to make an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="54ec0-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54ec0-124">Next steps</span></span>
* [<span data-ttu-id="54ec0-125">Azure CDN 概觀</span><span class="sxs-lookup"><span data-stu-id="54ec0-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="54ec0-126">規則引擎參考</span><span class="sxs-lookup"><span data-stu-id="54ec0-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="54ec0-127">規則引擎比對條件</span><span class="sxs-lookup"><span data-stu-id="54ec0-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="54ec0-128">規則引擎功能</span><span class="sxs-lookup"><span data-stu-id="54ec0-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="54ec0-129">使用規則引擎覆寫預設的 HTTP 行為</span><span class="sxs-lookup"><span data-stu-id="54ec0-129">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)

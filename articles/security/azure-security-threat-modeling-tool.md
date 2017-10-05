---
title: "Microsoft 威脅模型化工具 - Azure | Microsoft Docs"
description: "Microsoft 威脅模型化工具的主頁面，內含開始使用工具的資訊，包括威脅模型化程序"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 6e26b0af2a16a872c8e02b736e24019b47ed5780
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="7d580-103">Microsoft 威脅模型化工具</span><span class="sxs-lookup"><span data-stu-id="7d580-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="7d580-104">威脅模型化工具是 Microsoft 安全性開發生命週期 (SDL) 的核心元素。</span><span class="sxs-lookup"><span data-stu-id="7d580-104">The Threat Modeling Tool is a core element of the Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="7d580-105">它可讓軟體架構設計人員及早識別和降低潛在安全性問題的風險，以在問題相對簡單且符合成本效益時加以解決。</span><span class="sxs-lookup"><span data-stu-id="7d580-105">It allows software architects to identify and mitigate potential security issues early, when they are relatively easy and cost-effective to resolve.</span></span> <span data-ttu-id="7d580-106">因此，可大幅降低總開發成本。</span><span class="sxs-lookup"><span data-stu-id="7d580-106">As a result, it greatly reduces the total cost of development.</span></span> <span data-ttu-id="7d580-107">此外，我們在設計此工具時已考慮到非安全性專家的問題，因此可讓所有開發人員更加方便地建立威脅模型，為他們提供清楚說明如何建立和分析威脅模型的指導方針。</span><span class="sxs-lookup"><span data-stu-id="7d580-107">Also, we designed the tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="7d580-108">此工具可讓任何人：</span><span class="sxs-lookup"><span data-stu-id="7d580-108">The tool enables anyone to:</span></span>

* <span data-ttu-id="7d580-109">溝通有關其系統的安全性設計</span><span class="sxs-lookup"><span data-stu-id="7d580-109">Communicate about the security design of their systems</span></span>
* <span data-ttu-id="7d580-110">使用已證實的方法分析這些設計中的潛在安全性問題</span><span class="sxs-lookup"><span data-stu-id="7d580-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="7d580-111">建議和管理安全性問題的風險降低措施</span><span class="sxs-lookup"><span data-stu-id="7d580-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="7d580-112">以下列舉部分工具功能和創新︰</span><span class="sxs-lookup"><span data-stu-id="7d580-112">Here are some tooling capabilities and innovations, just to name a few:</span></span>

* <span data-ttu-id="7d580-113">**自動化︰**繪製模型的指引和意見反應</span><span class="sxs-lookup"><span data-stu-id="7d580-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="7d580-114">**每個元素的 STRIDE：**引導式的威脅與降低風險分析</span><span class="sxs-lookup"><span data-stu-id="7d580-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="7d580-115">**報告︰**驗證階段的安全性活動和測試</span><span class="sxs-lookup"><span data-stu-id="7d580-115">**Reporting:** Security activities and testing in the verification phase</span></span>
* <span data-ttu-id="7d580-116">**獨特的方法︰**可讓使用者更加看懂和了解威脅</span><span class="sxs-lookup"><span data-stu-id="7d580-116">**Unique Methodology:** Enables users to better visualize and understand threats</span></span>
* <span data-ttu-id="7d580-117">**專為開發人員所設計並聚焦於軟體上︰**許多方法都聚焦在資產或攻擊者上。</span><span class="sxs-lookup"><span data-stu-id="7d580-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="7d580-118">我們則聚焦在軟體上。</span><span class="sxs-lookup"><span data-stu-id="7d580-118">We are centered on software.</span></span> <span data-ttu-id="7d580-119">我們以所有軟體開發人員和架構設計人員都熟悉的活動為基礎來建置 -- 例如繪製其軟體架構的圖片</span><span class="sxs-lookup"><span data-stu-id="7d580-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="7d580-120">**聚焦在設計分析︰**「威脅模型化」一詞指的可能是需求或設計分析技巧。</span><span class="sxs-lookup"><span data-stu-id="7d580-120">**Focused on Design Analysis:** The term "threat modeling" can refer to either a requirements or a design analysis technique.</span></span> <span data-ttu-id="7d580-121">有時指的是這兩個情況的複雜混合。</span><span class="sxs-lookup"><span data-stu-id="7d580-121">Sometimes, it refers to a complex blend of the two.</span></span> <span data-ttu-id="7d580-122">Microsoft SDL 威脅模型化方法是聚焦在設計分析技巧</span><span class="sxs-lookup"><span data-stu-id="7d580-122">The Microsoft SDL approach to threat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d580-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d580-123">Next steps</span></span>

<span data-ttu-id="7d580-124">下表包含重要的連結，可以協助您開始使用威脅模型化工具：</span><span class="sxs-lookup"><span data-stu-id="7d580-124">The table below contains important links to get you started with the Threat Modeling Tool:</span></span>

| <span data-ttu-id="7d580-125">步驟</span><span class="sxs-lookup"><span data-stu-id="7d580-125">Step</span></span>  | <span data-ttu-id="7d580-126">說明</span><span class="sxs-lookup"><span data-stu-id="7d580-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="7d580-127">**1**</span><span class="sxs-lookup"><span data-stu-id="7d580-127">**1**</span></span> | [<span data-ttu-id="7d580-128">下載威脅模型化工具</span><span class="sxs-lookup"><span data-stu-id="7d580-128">Download the Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="7d580-129">**2**</span><span class="sxs-lookup"><span data-stu-id="7d580-129">**2**</span></span> | [<span data-ttu-id="7d580-130">參閱使用者入門指南</span><span class="sxs-lookup"><span data-stu-id="7d580-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="7d580-131">**3**</span><span class="sxs-lookup"><span data-stu-id="7d580-131">**3**</span></span> | [<span data-ttu-id="7d580-132">熟悉功能</span><span class="sxs-lookup"><span data-stu-id="7d580-132">Get familiar with the features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="7d580-133">**4**</span><span class="sxs-lookup"><span data-stu-id="7d580-133">**4**</span></span> | [<span data-ttu-id="7d580-134">深入了解產生的威脅類別</span><span class="sxs-lookup"><span data-stu-id="7d580-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="7d580-135">**5**</span><span class="sxs-lookup"><span data-stu-id="7d580-135">**5**</span></span> | [<span data-ttu-id="7d580-136">尋找對產生之威脅的風險降低</span><span class="sxs-lookup"><span data-stu-id="7d580-136">Find mitigations to generated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="7d580-137">資源</span><span class="sxs-lookup"><span data-stu-id="7d580-137">Resources</span></span>

<span data-ttu-id="7d580-138">以下是一些與現今威脅模型化仍然相關的較舊文章：</span><span class="sxs-lookup"><span data-stu-id="7d580-138">Here are a few older articles still relevant to threat modeling today:</span></span>

* [<span data-ttu-id="7d580-139">有關威脅模型化重要性的文章</span><span class="sxs-lookup"><span data-stu-id="7d580-139">Article on the Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="7d580-140">Trustworthy Computing 所發佈的訓練</span><span class="sxs-lookup"><span data-stu-id="7d580-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="7d580-141">查看某些威脅模型化工具專家做了些什麼︰</span><span class="sxs-lookup"><span data-stu-id="7d580-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="7d580-142">Threats Manager</span><span class="sxs-lookup"><span data-stu-id="7d580-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="7d580-143">Simone Curzi 安全性部落格</span><span class="sxs-lookup"><span data-stu-id="7d580-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)
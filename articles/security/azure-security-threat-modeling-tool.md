---
title: "aaaMicrosoft 威脅模型化工具-Azure |Microsoft 文件"
description: "hello Microsoft 威脅模型化工具，其中包含有關入門 hello 工具，包括 hello 威脅模型程序的主頁面"
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
ms.openlocfilehash: 923225a30c592ffdb1d254000451cfaac54a0e68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="4189e-103">Microsoft 威脅模型化工具</span><span class="sxs-lookup"><span data-stu-id="4189e-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="4189e-104">hello 威脅模型化工具是 Microsoft 安全性開發週期 (SDL) hello 的核心項目。</span><span class="sxs-lookup"><span data-stu-id="4189e-104">hello Threat Modeling Tool is a core element of hello Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="4189e-105">它可讓軟體架構設計人員 tooidentify 和時，它們相當容易、 更符合成本效益 tooresolve 早期減輕潛在的安全性問題。</span><span class="sxs-lookup"><span data-stu-id="4189e-105">It allows software architects tooidentify and mitigate potential security issues early, when they are relatively easy and cost-effective tooresolve.</span></span> <span data-ttu-id="4189e-106">如此一來，它可大幅減少開發 hello 總成本。</span><span class="sxs-lookup"><span data-stu-id="4189e-106">As a result, it greatly reduces hello total cost of development.</span></span> <span data-ttu-id="4189e-107">此外，我們會與非安全性專家納入考量，方便威脅分析模型的所有開發人員藉由提供清楚的指引，建立和分析威脅模型設計 hello 工具。</span><span class="sxs-lookup"><span data-stu-id="4189e-107">Also, we designed hello tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="4189e-108">hello 工具可讓任何人：</span><span class="sxs-lookup"><span data-stu-id="4189e-108">hello tool enables anyone to:</span></span>

* <span data-ttu-id="4189e-109">溝通有關其系統的 hello 安全性設計</span><span class="sxs-lookup"><span data-stu-id="4189e-109">Communicate about hello security design of their systems</span></span>
* <span data-ttu-id="4189e-110">使用已證實的方法分析這些設計中的潛在安全性問題</span><span class="sxs-lookup"><span data-stu-id="4189e-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="4189e-111">建議和管理安全性問題的風險降低措施</span><span class="sxs-lookup"><span data-stu-id="4189e-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="4189e-112">以下是一些工具功能和創新的做法，只是 tooname 幾個：</span><span class="sxs-lookup"><span data-stu-id="4189e-112">Here are some tooling capabilities and innovations, just tooname a few:</span></span>

* <span data-ttu-id="4189e-113">**自動化︰**繪製模型的指引和意見反應</span><span class="sxs-lookup"><span data-stu-id="4189e-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="4189e-114">**每個元素的 STRIDE：**引導式的威脅與降低風險分析</span><span class="sxs-lookup"><span data-stu-id="4189e-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="4189e-115">**報告：**安全性活動與 hello 確認階段中的測試</span><span class="sxs-lookup"><span data-stu-id="4189e-115">**Reporting:** Security activities and testing in hello verification phase</span></span>
* <span data-ttu-id="4189e-116">**唯一的方法：**可讓使用者 toobetter 視覺化並了解威脅</span><span class="sxs-lookup"><span data-stu-id="4189e-116">**Unique Methodology:** Enables users toobetter visualize and understand threats</span></span>
* <span data-ttu-id="4189e-117">**專為開發人員所設計並聚焦於軟體上︰**許多方法都聚焦在資產或攻擊者上。</span><span class="sxs-lookup"><span data-stu-id="4189e-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="4189e-118">我們則聚焦在軟體上。</span><span class="sxs-lookup"><span data-stu-id="4189e-118">We are centered on software.</span></span> <span data-ttu-id="4189e-119">我們以所有軟體開發人員和架構設計人員都熟悉的活動為基礎來建置 -- 例如繪製其軟體架構的圖片</span><span class="sxs-lookup"><span data-stu-id="4189e-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="4189e-120">**將焦點放在設計分析：** hello 詞彙 「 威脅模型 」 可以參考 tooeither 需求或設計的分析技術。</span><span class="sxs-lookup"><span data-stu-id="4189e-120">**Focused on Design Analysis:** hello term "threat modeling" can refer tooeither a requirements or a design analysis technique.</span></span> <span data-ttu-id="4189e-121">某些情況下，它是指 tooa 的 hello 兩個複雜的 blend。</span><span class="sxs-lookup"><span data-stu-id="4189e-121">Sometimes, it refers tooa complex blend of hello two.</span></span> <span data-ttu-id="4189e-122">hello Microsoft SDL 方法 toothreat 模型是已取得焦點的設計的分析技術</span><span class="sxs-lookup"><span data-stu-id="4189e-122">hello Microsoft SDL approach toothreat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="4189e-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4189e-123">Next steps</span></span>

<span data-ttu-id="4189e-124">hello 表包含重要連結 tooget 您一開始 hello 威脅模型化工具：</span><span class="sxs-lookup"><span data-stu-id="4189e-124">hello table below contains important links tooget you started with hello Threat Modeling Tool:</span></span>

| <span data-ttu-id="4189e-125">步驟</span><span class="sxs-lookup"><span data-stu-id="4189e-125">Step</span></span>  | <span data-ttu-id="4189e-126">說明</span><span class="sxs-lookup"><span data-stu-id="4189e-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="4189e-127">**1**</span><span class="sxs-lookup"><span data-stu-id="4189e-127">**1**</span></span> | [<span data-ttu-id="4189e-128">下載 hello 威脅模型化工具</span><span class="sxs-lookup"><span data-stu-id="4189e-128">Download hello Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="4189e-129">**2**</span><span class="sxs-lookup"><span data-stu-id="4189e-129">**2**</span></span> | [<span data-ttu-id="4189e-130">參閱使用者入門指南</span><span class="sxs-lookup"><span data-stu-id="4189e-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="4189e-131">**3**</span><span class="sxs-lookup"><span data-stu-id="4189e-131">**3**</span></span> | [<span data-ttu-id="4189e-132">讓您熟悉 hello 功能</span><span class="sxs-lookup"><span data-stu-id="4189e-132">Get familiar with hello features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="4189e-133">**4**</span><span class="sxs-lookup"><span data-stu-id="4189e-133">**4**</span></span> | [<span data-ttu-id="4189e-134">深入了解產生的威脅類別</span><span class="sxs-lookup"><span data-stu-id="4189e-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="4189e-135">**5**</span><span class="sxs-lookup"><span data-stu-id="4189e-135">**5**</span></span> | [<span data-ttu-id="4189e-136">尋找 toogenerated 威脅防護</span><span class="sxs-lookup"><span data-stu-id="4189e-136">Find mitigations toogenerated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="4189e-137">資源</span><span class="sxs-lookup"><span data-stu-id="4189e-137">Resources</span></span>

<span data-ttu-id="4189e-138">以下是幾個較舊的發行項仍與 toothreat 模型今天：</span><span class="sxs-lookup"><span data-stu-id="4189e-138">Here are a few older articles still relevant toothreat modeling today:</span></span>

* [<span data-ttu-id="4189e-139">發行項上 hello 重要性的威脅模型</span><span class="sxs-lookup"><span data-stu-id="4189e-139">Article on hello Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="4189e-140">Trustworthy Computing 所發佈的訓練</span><span class="sxs-lookup"><span data-stu-id="4189e-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="4189e-141">查看某些威脅模型化工具專家做了些什麼︰</span><span class="sxs-lookup"><span data-stu-id="4189e-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="4189e-142">Threats Manager</span><span class="sxs-lookup"><span data-stu-id="4189e-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="4189e-143">Simone Curzi 安全性部落格</span><span class="sxs-lookup"><span data-stu-id="4189e-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)
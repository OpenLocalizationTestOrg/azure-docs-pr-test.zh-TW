---
title: "Azure 安全性最佳作法與模式 | Microsoft Docs"
description: "本文提供有關 Azure 安全性最佳作法和模式，以及策劃好的不同 Azure 資源安全性最佳作法清單的簡介。"
services: azure-security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1cbbf8dc-ea94-4a7e-8fa0-c2cb198956c5
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: terrylan
ms.openlocfilehash: 1cc0d2d1e9a62ff8531f963413ff573713d508ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-best-practices-and-patterns"></a><span data-ttu-id="0da2d-103">Azure 安全性最佳作法與模式</span><span class="sxs-lookup"><span data-stu-id="0da2d-103">Azure security best practices and patterns</span></span>
<span data-ttu-id="0da2d-104">我們目前有下列的 Azure 安全性最佳作法和模式文章。</span><span class="sxs-lookup"><span data-stu-id="0da2d-104">We currently have the following Azure security best practices and patterns articles.</span></span> <span data-ttu-id="0da2d-105">請務必定期瀏覽此網站，以查看日益增加的 Azure 安全性最佳作法和模式的清單是否有更新︰</span><span class="sxs-lookup"><span data-stu-id="0da2d-105">Make sure to visit this site periodically to see updates to our growing list of Azure security best practices and patterns:</span></span>  

* [<span data-ttu-id="0da2d-106">Azure 網路安全性最佳作法</span><span class="sxs-lookup"><span data-stu-id="0da2d-106">Azure network security best practices</span></span>](azure-security-network-security-best-practices.md)
* [<span data-ttu-id="0da2d-107">Azure 資料安全性和加密最佳作法</span><span class="sxs-lookup"><span data-stu-id="0da2d-107">Azure data security and encryption best practices</span></span>](azure-security-data-encryption-best-practices.md)
* [<span data-ttu-id="0da2d-108">身分識別管理和存取控制安全性最佳作法</span><span class="sxs-lookup"><span data-stu-id="0da2d-108">Identity management and access control security best practices</span></span>](azure-security-identity-management-best-practices.md)
* [<span data-ttu-id="0da2d-109">物聯網安全性最佳做法</span><span class="sxs-lookup"><span data-stu-id="0da2d-109">Internet of Things security best practices</span></span>](azure-security-iot-best-practices.md)
* <span data-ttu-id="0da2d-110">[Azure IaaS 安全性最佳做法] (azure-security-iaas.md)</span><span class="sxs-lookup"><span data-stu-id="0da2d-110">[Azure IaaS Security Best Practices] (azure-security-iaas.md)</span></span>
* [<span data-ttu-id="0da2d-111">Azure 界限安全性最佳作法</span><span class="sxs-lookup"><span data-stu-id="0da2d-111">Azure boundary security best practices</span></span>](../best-practices-network-security.md)
* [<span data-ttu-id="0da2d-112">在 Azure 中實作安全的混合式網路架構</span><span class="sxs-lookup"><span data-stu-id="0da2d-112">Implementing a secure hybrid network architecture in Azure</span></span>](../guidance/guidance-iaas-ra-secure-vnet-hybrid.md)
* <span data-ttu-id="0da2d-113">[Azure PaaS 最佳作法] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span><span class="sxs-lookup"><span data-stu-id="0da2d-113">[Azure PaaS Best Practices] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span></span>

<span data-ttu-id="0da2d-114">Azure 提供安全的平台，您可以在其中建立您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="0da2d-114">Azure provides a secure platform on which you can build your solutions.</span></span> <span data-ttu-id="0da2d-115">我們也提供服務和技術，可讓您的解決方案在 Azure 上更安全。</span><span class="sxs-lookup"><span data-stu-id="0da2d-115">We also provide services and technologies to make your solutions on Azure more secure.</span></span> <span data-ttu-id="0da2d-116">由於有許多選項可供使用，因此對 Microsoft 針對改善安全性所建議作為最佳做法與模式的內容，許多人都表示感興趣。</span><span class="sxs-lookup"><span data-stu-id="0da2d-116">Because of the many options available to you, many of you have voiced an interest in what Microsoft recommends as best practices and patterns for improving security.</span></span>

<span data-ttu-id="0da2d-117">我們了解您的興趣所在，因此我們建立了一組文件，當中說明在適當的背景環境下您可以執行以改善 Azure 部署安全性的動作。</span><span class="sxs-lookup"><span data-stu-id="0da2d-117">We understand your interest and have created a collection of documents that describe things you can do, given the right context, to improve the security of Azure deployments.</span></span>

<span data-ttu-id="0da2d-118">在這些最佳做法和模式的文章中，我們針對特定的主題討論了一組最佳做法和實用模式。</span><span class="sxs-lookup"><span data-stu-id="0da2d-118">In these best practices and patterns articles, we discuss a collection of best practices and useful patterns for specific topics.</span></span> <span data-ttu-id="0da2d-119">這些最佳作法和模式衍生自我們這些技術的經驗和客戶的經驗。</span><span class="sxs-lookup"><span data-stu-id="0da2d-119">These best practices and patterns are derived from our experiences with these technologies and the experiences of customers like yourself.</span></span>

<span data-ttu-id="0da2d-120">對於每個最佳作法，我們會說明︰</span><span class="sxs-lookup"><span data-stu-id="0da2d-120">For each best practice we strive to explain:</span></span>

* <span data-ttu-id="0da2d-121">最佳作法是什麼</span><span class="sxs-lookup"><span data-stu-id="0da2d-121">What the best practice is</span></span>
* <span data-ttu-id="0da2d-122">您為何想要啟用該最佳作法</span><span class="sxs-lookup"><span data-stu-id="0da2d-122">Why you want to enable that best practice</span></span>
* <span data-ttu-id="0da2d-123">如果無法啟用最佳作法，結果可能為何</span><span class="sxs-lookup"><span data-stu-id="0da2d-123">What might be the result if you fail to enable the best practice</span></span>
* <span data-ttu-id="0da2d-124">最佳作法的可能替代方案</span><span class="sxs-lookup"><span data-stu-id="0da2d-124">Possible alternatives to the best practice</span></span>
* <span data-ttu-id="0da2d-125">如何學習啟用最佳作法</span><span class="sxs-lookup"><span data-stu-id="0da2d-125">How you can learn to enable the best practice</span></span>

<span data-ttu-id="0da2d-126">我們希望在 Azure 安全性架構和最佳作法中納入更多文章。</span><span class="sxs-lookup"><span data-stu-id="0da2d-126">We look forward to including many more articles on Azure security architecture and best practices.</span></span> <span data-ttu-id="0da2d-127">如果您有希望我們納入的主題，請在本頁面底部的討論區中讓我們知道。</span><span class="sxs-lookup"><span data-stu-id="0da2d-127">If there are topics that you'd like us to include, let us know in the discussion area at the bottom of this page.</span></span>

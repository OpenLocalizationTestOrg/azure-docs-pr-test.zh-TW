---
title: "aaaAzure 安全性最佳作法和模式 |Microsoft 文件"
description: "hello 文章提供有關 Azure 安全性的最佳作法和模式和不同的 Azure 資源的安全性最佳作法的策劃的清單的簡介。"
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
ms.openlocfilehash: eaaa9457faa1d5906275eb1fd8988d4d4aad101a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-best-practices-and-patterns"></a><span data-ttu-id="a1741-103">Azure 安全性最佳作法與模式</span><span class="sxs-lookup"><span data-stu-id="a1741-103">Azure security best practices and patterns</span></span>
<span data-ttu-id="a1741-104">我們目前已有下列 Azure 的安全性最佳作法和模式的發行項的 hello。</span><span class="sxs-lookup"><span data-stu-id="a1741-104">We currently have hello following Azure security best practices and patterns articles.</span></span> <span data-ttu-id="a1741-105">此站台，請確定 toovisit toosee 會定期更新 Azure 的安全性最佳作法和模式的 tooour 不斷增長清單：</span><span class="sxs-lookup"><span data-stu-id="a1741-105">Make sure toovisit this site periodically toosee updates tooour growing list of Azure security best practices and patterns:</span></span>  

* [<span data-ttu-id="a1741-106">Azure 網路安全性最佳作法</span><span class="sxs-lookup"><span data-stu-id="a1741-106">Azure network security best practices</span></span>](azure-security-network-security-best-practices.md)
* [<span data-ttu-id="a1741-107">Azure 資料安全性和加密最佳作法</span><span class="sxs-lookup"><span data-stu-id="a1741-107">Azure data security and encryption best practices</span></span>](azure-security-data-encryption-best-practices.md)
* [<span data-ttu-id="a1741-108">身分識別管理和存取控制安全性最佳作法</span><span class="sxs-lookup"><span data-stu-id="a1741-108">Identity management and access control security best practices</span></span>](azure-security-identity-management-best-practices.md)
* [<span data-ttu-id="a1741-109">物聯網安全性最佳做法</span><span class="sxs-lookup"><span data-stu-id="a1741-109">Internet of Things security best practices</span></span>](azure-security-iot-best-practices.md)
* <span data-ttu-id="a1741-110">[Azure IaaS 安全性最佳做法] (azure-security-iaas.md)</span><span class="sxs-lookup"><span data-stu-id="a1741-110">[Azure IaaS Security Best Practices] (azure-security-iaas.md)</span></span>
* [<span data-ttu-id="a1741-111">Azure 界限安全性最佳作法</span><span class="sxs-lookup"><span data-stu-id="a1741-111">Azure boundary security best practices</span></span>](../best-practices-network-security.md)
* [<span data-ttu-id="a1741-112">在 Azure 中實作安全的混合式網路架構</span><span class="sxs-lookup"><span data-stu-id="a1741-112">Implementing a secure hybrid network architecture in Azure</span></span>](../guidance/guidance-iaas-ra-secure-vnet-hybrid.md)
* <span data-ttu-id="a1741-113">[Azure PaaS 最佳作法] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span><span class="sxs-lookup"><span data-stu-id="a1741-113">[Azure PaaS Best Practices] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span></span>

<span data-ttu-id="a1741-114">Azure 提供安全的平台，您可以在其中建立您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="a1741-114">Azure provides a secure platform on which you can build your solutions.</span></span> <span data-ttu-id="a1741-115">我們也提供服務和技術 toomake 方案更安全的 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="a1741-115">We also provide services and technologies toomake your solutions on Azure more secure.</span></span> <span data-ttu-id="a1741-116">因為 hello 許多選項可用 tooyou，許多具有有聲什麼 Microsoft 建議最佳作法與改善安全性模式有興趣。</span><span class="sxs-lookup"><span data-stu-id="a1741-116">Because of hello many options available tooyou, many of you have voiced an interest in what Microsoft recommends as best practices and patterns for improving security.</span></span>

<span data-ttu-id="a1741-117">我們了解您感興趣，而且已建立的文件，描述您可以執行，給定的 hello 右內容，tooimprove hello 安全性的 Azure 部署的項目集合。</span><span class="sxs-lookup"><span data-stu-id="a1741-117">We understand your interest and have created a collection of documents that describe things you can do, given hello right context, tooimprove hello security of Azure deployments.</span></span>

<span data-ttu-id="a1741-118">在這些最佳做法和模式的文章中，我們針對特定的主題討論了一組最佳做法和實用模式。</span><span class="sxs-lookup"><span data-stu-id="a1741-118">In these best practices and patterns articles, we discuss a collection of best practices and useful patterns for specific topics.</span></span> <span data-ttu-id="a1741-119">這些最佳作法和模式衍生自我們的經驗與這些技術和 hello 經驗的客戶想自己。</span><span class="sxs-lookup"><span data-stu-id="a1741-119">These best practices and patterns are derived from our experiences with these technologies and hello experiences of customers like yourself.</span></span>

<span data-ttu-id="a1741-120">針對每個最佳做法，我們會盡力 tooexplain:</span><span class="sxs-lookup"><span data-stu-id="a1741-120">For each best practice we strive tooexplain:</span></span>

* <span data-ttu-id="a1741-121">哪些 hello 最佳作法是</span><span class="sxs-lookup"><span data-stu-id="a1741-121">What hello best practice is</span></span>
* <span data-ttu-id="a1741-122">為什麼要 tooenable 該最佳作法</span><span class="sxs-lookup"><span data-stu-id="a1741-122">Why you want tooenable that best practice</span></span>
* <span data-ttu-id="a1741-123">如果您無法 tooenable hello 最佳作法，可能 hello 結果</span><span class="sxs-lookup"><span data-stu-id="a1741-123">What might be hello result if you fail tooenable hello best practice</span></span>
* <span data-ttu-id="a1741-124">可能的替代方式 toohello 最佳作法</span><span class="sxs-lookup"><span data-stu-id="a1741-124">Possible alternatives toohello best practice</span></span>
* <span data-ttu-id="a1741-125">如何了解 tooenable hello 最佳作法</span><span class="sxs-lookup"><span data-stu-id="a1741-125">How you can learn tooenable hello best practice</span></span>

<span data-ttu-id="a1741-126">我們期待 tooincluding 許多 Azure 安全性的架構和最佳作法的詳細文章。</span><span class="sxs-lookup"><span data-stu-id="a1741-126">We look forward tooincluding many more articles on Azure security architecture and best practices.</span></span> <span data-ttu-id="a1741-127">如果您想要我們主題 tooinclude，讓我們知道在 hello 此頁面底部的 hello 討論區中。</span><span class="sxs-lookup"><span data-stu-id="a1741-127">If there are topics that you'd like us tooinclude, let us know in hello discussion area at hello bottom of this page.</span></span>

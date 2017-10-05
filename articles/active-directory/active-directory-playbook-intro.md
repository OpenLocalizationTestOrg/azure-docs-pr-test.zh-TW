---
title: "Azure Active Directory PoC 腳本簡介 | Microsoft Docs"
description: "探索並快速實作身分識別和存取管理案例"
services: active-directory
keywords: "azure active directory, 腳本, 概念證明, PoC"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 567f3373594bc53435e8c0bd0a3445dd318af1cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="51769-104">Azure Active Directory 概念證明腳本：簡介</span><span class="sxs-lookup"><span data-stu-id="51769-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="51769-105">這篇文章提供在概念證明 (PoC) 中探索不同 Azure AD 功能的指導方針。</span><span class="sxs-lookup"><span data-stu-id="51769-105">This article provides guidelines to explore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="51769-106">本文件的目標對象是身分識別架構設計人員、IT 專業人員和系統整合者</span><span class="sxs-lookup"><span data-stu-id="51769-106">The intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-to-use-this-playbook"></a><span data-ttu-id="51769-107">如何使用這個腳本</span><span class="sxs-lookup"><span data-stu-id="51769-107">How to use this Playbook</span></span>

1. <span data-ttu-id="51769-108">使用[佈景主題](active-directory-playbook-ingredients.md#theme)區段，然後根據您的需求選取感興趣的區域。</span><span class="sxs-lookup"><span data-stu-id="51769-108">Use the [Theme](active-directory-playbook-ingredients.md#theme) section and pick the area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="51769-109">藉由選取與您的商務目標一致的案例，來設定 PoC 的範圍。</span><span class="sxs-lookup"><span data-stu-id="51769-109">Scope the PoC by choosing the scenarios that align with your business goals.</span></span> <span data-ttu-id="51769-110">愈短愈好。</span><span class="sxs-lookup"><span data-stu-id="51769-110">The shorter the better.</span></span> <span data-ttu-id="51769-111">我們建議這麼做是因為越簡潔越能將價值傳達給專案關係人，同時將實現作業的複雜度降至最低。</span><span class="sxs-lookup"><span data-stu-id="51769-111">We recommend doing it as short and concise as possible to convey the value to the stakeholders while minimizing the complexity to realize it.</span></span>  
3. <span data-ttu-id="51769-112">使用[實作](active-directory-playbook-implementation.md)區段以了解案例，以及它們對於您的環境有什麼意義。</span><span class="sxs-lookup"><span data-stu-id="51769-112">Use the [Implementation](active-directory-playbook-implementation.md) section to understand the scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="51769-113">在每個案例中，我們會說明如何設定 (所謂的[建置組塊](active-directory-playbook-building-blocks.md))，以及如何瀏覽案例。</span><span class="sxs-lookup"><span data-stu-id="51769-113">In each scenario, we describe how to set it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how to navigate the scenarios.</span></span> 
4. <span data-ttu-id="51769-114">每個建置區塊均會說明所需的必要條件，以及完成的大約時間。</span><span class="sxs-lookup"><span data-stu-id="51769-114">Each building block explains the pre-requisites needed, as well as an approximate time to complete.</span></span> <span data-ttu-id="51769-115">這可以在計劃程序期間協助您。</span><span class="sxs-lookup"><span data-stu-id="51769-115">This can help you during the planning process.</span></span> 
5. <span data-ttu-id="51769-116">根據上述的 1-3，定義要在其中執行的[環境](active-directory-playbook-ingredients.md#environment)。</span><span class="sxs-lookup"><span data-stu-id="51769-116">Based on 1-3 Above, define the [Environment](active-directory-playbook-ingredients.md#environment) in which to execute.</span></span> <span data-ttu-id="51769-117">我們鼓勵尋求生產環境，為使用者取得良好的經驗。</span><span class="sxs-lookup"><span data-stu-id="51769-117">We encourage to strive for a production environment to get a good feel of the experience for your users.</span></span> 
6. <span data-ttu-id="51769-118">當需求有衝突的時候，請使用這個實用的取捨矩陣</span><span class="sxs-lookup"><span data-stu-id="51769-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="51769-119">以佈景主題為主的顯示值</span><span class="sxs-lookup"><span data-stu-id="51769-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="51769-120">準備、設定及執行案例的流暢度</span><span class="sxs-lookup"><span data-stu-id="51769-120">Smoothness to prepare, to set up, and to execute the scenarios</span></span> 
   * <span data-ttu-id="51769-121">執行目標案例的最少時間</span><span class="sxs-lookup"><span data-stu-id="51769-121">Minimal time to execute the target scenarios</span></span> 
   * <span data-ttu-id="51769-122">在您的限制之內儘可能接近生產</span><span class="sxs-lookup"><span data-stu-id="51769-122">As close to production as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="51769-123">在本文中，您會看到一些特定第三方應用程式和產品，以便作為範例。</span><span class="sxs-lookup"><span data-stu-id="51769-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="51769-124">Azure AD 支援我們的[應用程式庫](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps)中數千個應用程式，您可以根據需求和環境加以使用。</span><span class="sxs-lookup"><span data-stu-id="51769-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]
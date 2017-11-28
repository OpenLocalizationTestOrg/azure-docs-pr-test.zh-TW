---
title: "aaaAzure Active Directory PoC 腳本簡介 |Microsoft 文件"
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
ms.openlocfilehash: 655524e9692de46e831fc68e1636e6c20d41958f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="fcc20-104">Azure Active Directory 概念證明腳本：簡介</span><span class="sxs-lookup"><span data-stu-id="fcc20-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="fcc20-105">本文章提供概念證明 (PoC) 中的 tooexplore 不同的 Azure AD 功能的指導方針。</span><span class="sxs-lookup"><span data-stu-id="fcc20-105">This article provides guidelines tooexplore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="fcc20-106">hello 適合此文件的適用對象是識別架構設計人員、 IT 專業人員和系統整合者</span><span class="sxs-lookup"><span data-stu-id="fcc20-106">hello intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-toouse-this-playbook"></a><span data-ttu-id="fcc20-107">如何 toouse 這個腳本</span><span class="sxs-lookup"><span data-stu-id="fcc20-107">How toouse this Playbook</span></span>

1. <span data-ttu-id="fcc20-108">使用 hello[佈景主題](active-directory-playbook-ingredients.md#theme)區段，然後挑選您的需求為基礎的感興趣的 hello box-decoration-break。</span><span class="sxs-lookup"><span data-stu-id="fcc20-108">Use hello [Theme](active-directory-playbook-ingredients.md#theme) section and pick hello area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="fcc20-109">範圍 hello PoC 選擇符合商務目標的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="fcc20-109">Scope hello PoC by choosing hello scenarios that align with your business goals.</span></span> <span data-ttu-id="fcc20-110">hello 短 hello 更好。</span><span class="sxs-lookup"><span data-stu-id="fcc20-110">hello shorter hello better.</span></span> <span data-ttu-id="fcc20-111">我們建議您這麼做為短和精簡做為可能 tooconvey hello 值降至最低 toohello 專案關係人 hello 複雜性 toorealize 它。</span><span class="sxs-lookup"><span data-stu-id="fcc20-111">We recommend doing it as short and concise as possible tooconvey hello value toohello stakeholders while minimizing hello complexity toorealize it.</span></span>  
3. <span data-ttu-id="fcc20-112">使用 hello[實作](active-directory-playbook-implementation.md)區段 toounderstand hello 情節，以及其代表意義為您的環境。</span><span class="sxs-lookup"><span data-stu-id="fcc20-112">Use hello [Implementation](active-directory-playbook-implementation.md) section toounderstand hello scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="fcc20-113">在每個案例中，我們說明如何 tooset 它 (我們所謂[建置組塊](active-directory-playbook-building-blocks.md))，及如何 toonavigate hello 案例。</span><span class="sxs-lookup"><span data-stu-id="fcc20-113">In each scenario, we describe how tooset it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how toonavigate hello scenarios.</span></span> 
4. <span data-ttu-id="fcc20-114">每個建置組塊說明 hello 必要元件所需，以及大約時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="fcc20-114">Each building block explains hello pre-requisites needed, as well as an approximate time toocomplete.</span></span> <span data-ttu-id="fcc20-115">這可協助您規劃程序的 hello 期間。</span><span class="sxs-lookup"><span data-stu-id="fcc20-115">This can help you during hello planning process.</span></span> 
5. <span data-ttu-id="fcc20-116">根據上述的 1-3，定義 hello[環境](active-directory-playbook-ingredients.md#environment)哪些 tooexecute 中。</span><span class="sxs-lookup"><span data-stu-id="fcc20-116">Based on 1-3 Above, define hello [Environment](active-directory-playbook-ingredients.md#environment) in which tooexecute.</span></span> <span data-ttu-id="fcc20-117">我們建議實際執行環境 tooget hello 使用者體驗很好風格的 toostrive。</span><span class="sxs-lookup"><span data-stu-id="fcc20-117">We encourage toostrive for a production environment tooget a good feel of hello experience for your users.</span></span> 
6. <span data-ttu-id="fcc20-118">當需求有衝突的時候，請使用這個實用的取捨矩陣</span><span class="sxs-lookup"><span data-stu-id="fcc20-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="fcc20-119">以佈景主題為主的顯示值</span><span class="sxs-lookup"><span data-stu-id="fcc20-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="fcc20-120">平滑度 tooprepare、 tooset 和 tooexecute hello 案例</span><span class="sxs-lookup"><span data-stu-id="fcc20-120">Smoothness tooprepare, tooset up, and tooexecute hello scenarios</span></span> 
   * <span data-ttu-id="fcc20-121">最短時間 tooexecute hello 目標情況</span><span class="sxs-lookup"><span data-stu-id="fcc20-121">Minimal time tooexecute hello target scenarios</span></span> 
   * <span data-ttu-id="fcc20-122">做為您的條件約束中關閉 tooproduction</span><span class="sxs-lookup"><span data-stu-id="fcc20-122">As close tooproduction as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="fcc20-123">在本文中，您會看到一些特定第三方應用程式和產品，以便作為範例。</span><span class="sxs-lookup"><span data-stu-id="fcc20-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="fcc20-124">Azure AD 支援我們的[應用程式庫](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps)中數千個應用程式，您可以根據需求和環境加以使用。</span><span class="sxs-lookup"><span data-stu-id="fcc20-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]
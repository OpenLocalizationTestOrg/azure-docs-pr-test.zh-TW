---
title: "Azure API 管理開發人員入口網站範本 | Microsoft Docs"
description: "了解如何使用「Azure API 管理」中的一組範本來自訂開發人員入口網站頁面的內容。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 5189f3d8-2a4c-4dc8-ab19-11c7df0114d4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dc3f32a3cff2e66a798bd8f6c19c6b56a47643ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-developer-portal-templates"></a><span data-ttu-id="a8789-103">Azure API 管理開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="a8789-103">Azure API Management Developer Portal Templates</span></span>
<span data-ttu-id="a8789-104">「Azure API 管理」可讓您使用一組可設定開發人員入口網站頁面內容的範本，來自訂那些頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="a8789-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="a8789-105">使用這些範本時，您可以運用 [DotLiquid](http://dotliquidmarkup.org/) 語法和您選擇的編輯器 (例如 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers))，以及一組提供的當地語系化[字串資源](api-management-template-resources.md#strings)、[字符資源](api-management-template-resources.md#glyphs)和[頁面控制項](api-management-page-controls.md)，依照您的想法自由靈活地設定頁面內容。</span><span class="sxs-lookup"><span data-stu-id="a8789-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="a8789-106">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="a8789-106">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  



  
##  <span data-ttu-id="a8789-107"><a name="DeveloperPortalTemplates"></a> 開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="a8789-107"><a name="DeveloperPortalTemplates"></a> Developer portal templates</span></span>  
  
-   [<span data-ttu-id="a8789-108">API</span><span class="sxs-lookup"><span data-stu-id="a8789-108">APIs</span></span>](api-management-api-templates.md)  
    -   [<span data-ttu-id="a8789-109">API 清單</span><span class="sxs-lookup"><span data-stu-id="a8789-109">API list</span></span>](api-management-api-templates.md#APIList)  
    -   [<span data-ttu-id="a8789-110">作業</span><span class="sxs-lookup"><span data-stu-id="a8789-110">Operation</span></span>](api-management-api-templates.md#Product)  
    -   [<span data-ttu-id="a8789-111">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="a8789-111">Code samples</span></span>](api-management-api-templates.md#CodeSamples)  
        -   [<span data-ttu-id="a8789-112">Curl</span><span class="sxs-lookup"><span data-stu-id="a8789-112">Curl</span></span>](api-management-api-templates.md#Curl)  
        -   [<span data-ttu-id="a8789-113">C#</span><span class="sxs-lookup"><span data-stu-id="a8789-113">C#</span></span>](api-management-api-templates.md#CSharp)  
        -   [<span data-ttu-id="a8789-114">Java</span><span class="sxs-lookup"><span data-stu-id="a8789-114">Java</span></span>](api-management-api-templates.md#Stub)  
        -   [<span data-ttu-id="a8789-115">JavaScript</span><span class="sxs-lookup"><span data-stu-id="a8789-115">JavaScript</span></span>](api-management-api-templates.md#JavaScript)  
        -   [<span data-ttu-id="a8789-116">Objective C</span><span class="sxs-lookup"><span data-stu-id="a8789-116">Objective C</span></span>](api-management-api-templates.md#ObjectiveC)  
        -   [<span data-ttu-id="a8789-117">PHP</span><span class="sxs-lookup"><span data-stu-id="a8789-117">PHP</span></span>](api-management-api-templates.md#PHP)  
        -   [<span data-ttu-id="a8789-118">Python</span><span class="sxs-lookup"><span data-stu-id="a8789-118">Python</span></span>](api-management-api-templates.md#Python)  
        -   [<span data-ttu-id="a8789-119">Ruby</span><span class="sxs-lookup"><span data-stu-id="a8789-119">Ruby</span></span>](api-management-api-templates.md#Ruby)  
-   [<span data-ttu-id="a8789-120">產品</span><span class="sxs-lookup"><span data-stu-id="a8789-120">Products</span></span>](api-management-product-templates.md)  
    -   [<span data-ttu-id="a8789-121">產品清單</span><span class="sxs-lookup"><span data-stu-id="a8789-121">Product list</span></span>](api-management-product-templates.md#ProductList)  
    -   [<span data-ttu-id="a8789-122">產品</span><span class="sxs-lookup"><span data-stu-id="a8789-122">Product</span></span>](api-management-product-templates.md#Product)  
-   [<span data-ttu-id="a8789-123">應用程式</span><span class="sxs-lookup"><span data-stu-id="a8789-123">Applications</span></span>](api-management-application-templates.md)  
    -   [<span data-ttu-id="a8789-124">應用程式清單</span><span class="sxs-lookup"><span data-stu-id="a8789-124">Application list</span></span>](api-management-application-templates.md#ProductList)  
    -   [<span data-ttu-id="a8789-125">應用程式</span><span class="sxs-lookup"><span data-stu-id="a8789-125">Application</span></span>](api-management-application-templates.md#Application)  
-   [<span data-ttu-id="a8789-126">問題</span><span class="sxs-lookup"><span data-stu-id="a8789-126">Issues</span></span>](api-management-issue-templates.md)  
    -   [<span data-ttu-id="a8789-127">問題清單</span><span class="sxs-lookup"><span data-stu-id="a8789-127">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
-   [<span data-ttu-id="a8789-128">使用者設定檔</span><span class="sxs-lookup"><span data-stu-id="a8789-128">User Profile</span></span>](api-management-user-profile-templates.md)  
    -   [<span data-ttu-id="a8789-129">設定檔</span><span class="sxs-lookup"><span data-stu-id="a8789-129">Profile</span></span>](api-management-user-profile-templates.md#Profile)  
    -   [<span data-ttu-id="a8789-130">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a8789-130">Subscriptions</span></span>](api-management-user-profile-templates.md#Subscriptions)  
    -   [<span data-ttu-id="a8789-131">應用程式</span><span class="sxs-lookup"><span data-stu-id="a8789-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
    -   [<span data-ttu-id="a8789-132">更新帳戶資訊</span><span class="sxs-lookup"><span data-stu-id="a8789-132">Update account info</span></span>](api-management-user-profile-templates.md#UpdateAccountInfo)  
-   [<span data-ttu-id="a8789-133">頁面</span><span class="sxs-lookup"><span data-stu-id="a8789-133">Pages</span></span>](api-management-page-templates.md)  
    -   [<span data-ttu-id="a8789-134">登入</span><span class="sxs-lookup"><span data-stu-id="a8789-134">Sign in</span></span>](api-management-page-templates.md#SignIn)  
    -   [<span data-ttu-id="a8789-135">註冊</span><span class="sxs-lookup"><span data-stu-id="a8789-135">Sign up</span></span>](api-management-page-templates.md#SignUp)  
    -   [<span data-ttu-id="a8789-136">找不到頁面</span><span class="sxs-lookup"><span data-stu-id="a8789-136">Page not found</span></span>](api-management-page-templates.md#PageNotFound)


## <a name="next-steps"></a><span data-ttu-id="a8789-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a8789-137">Next steps</span></span>  
-   [<span data-ttu-id="a8789-138">範本參考</span><span class="sxs-lookup"><span data-stu-id="a8789-138">Template reference</span></span>](api-management-developer-portal-templates-reference.md)  
-   [<span data-ttu-id="a8789-139">資料模型參考</span><span class="sxs-lookup"><span data-stu-id="a8789-139">Data model reference</span></span>](api-management-template-data-model-reference.md)  
-   [<span data-ttu-id="a8789-140">頁面控制項</span><span class="sxs-lookup"><span data-stu-id="a8789-140">Page controls</span></span>](api-management-page-controls.md)  
-   [<span data-ttu-id="a8789-141">範本資源</span><span class="sxs-lookup"><span data-stu-id="a8789-141">Template resources</span></span>](api-management-template-resources.md)
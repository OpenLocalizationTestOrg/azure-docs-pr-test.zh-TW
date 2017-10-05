---
title: "Azure API 管理的頁面控制項 | Microsoft Docs"
description: "了解在 Azure API 管理的開發人員入口網站範本中可使用的頁面控制項。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1ce0657aebe34d093ae94281de208c929067742a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="0218f-103">Azure API 管理的頁面控制項</span><span class="sxs-lookup"><span data-stu-id="0218f-103">Azure API Management page controls</span></span>
<span data-ttu-id="0218f-104">Azure API 管理提供下列可在開發人員入口網站範本中使用的控制項。</span><span class="sxs-lookup"><span data-stu-id="0218f-104">Azure API Management provides the following controls for use in the developer portal templates.</span></span>  
  
 <span data-ttu-id="0218f-105">若要使用控制項，請將它放在開發人員入口網站範本中所要的位置。</span><span class="sxs-lookup"><span data-stu-id="0218f-105">To use a control, place it in the desired location in the developer portal template.</span></span> <span data-ttu-id="0218f-106">某些控制項 (例如 [app-actions](#app-actions) 控制項) 具有參數，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="0218f-106">Some controls, such as the [app-actions](#app-actions) control, have parameters, as shown in the following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="0218f-107">參數的值會以範本資料模型組件的形式來傳入。</span><span class="sxs-lookup"><span data-stu-id="0218f-107">The values for the parameters are passed in as part of the data model for the template.</span></span> <span data-ttu-id="0218f-108">大部分情況下，您只要在針對每個控制項所提供的範例中貼上，即可讓其正確運作。</span><span class="sxs-lookup"><span data-stu-id="0218f-108">In most cases, you can simply paste in the provided example for each control for it to work correctly.</span></span> <span data-ttu-id="0218f-109">如需參數值的詳細資訊，請參閱控制項可能使用所在之各個範本的資料模型區段。</span><span class="sxs-lookup"><span data-stu-id="0218f-109">For more information on the parameter values, you can see the data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="0218f-110">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。</span><span class="sxs-lookup"><span data-stu-id="0218f-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="0218f-111">開發人員入口網站範本頁面控制項</span><span class="sxs-lookup"><span data-stu-id="0218f-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="0218f-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="0218f-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="0218f-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="0218f-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="0218f-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="0218f-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="0218f-115">提供者</span><span class="sxs-lookup"><span data-stu-id="0218f-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="0218f-116">search-control</span><span class="sxs-lookup"><span data-stu-id="0218f-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="0218f-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="0218f-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="0218f-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="0218f-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="0218f-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="0218f-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="0218f-120"><a name="app-actions"></a>app-actions</span><span class="sxs-lookup"><span data-stu-id="0218f-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="0218f-121">`app-actions` 控制項會提供使用者介面，以便與開發人員入口網站中 [使用者設定檔] 頁面上的應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="0218f-121">The `app-actions` control provides a user interface for interacting with applications on the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="0218f-122">![app&#45;actions 控制項](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions 控制項")</span><span class="sxs-lookup"><span data-stu-id="0218f-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="0218f-123">使用量</span><span class="sxs-lookup"><span data-stu-id="0218f-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="0218f-124">參數</span><span class="sxs-lookup"><span data-stu-id="0218f-124">Parameters</span></span>  
  
|<span data-ttu-id="0218f-125">參數</span><span class="sxs-lookup"><span data-stu-id="0218f-125">Parameter</span></span>|<span data-ttu-id="0218f-126">說明</span><span class="sxs-lookup"><span data-stu-id="0218f-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="0218f-127">appId</span><span class="sxs-lookup"><span data-stu-id="0218f-127">appId</span></span>|<span data-ttu-id="0218f-128">應用程式的識別碼。</span><span class="sxs-lookup"><span data-stu-id="0218f-128">The id of the application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="0218f-129">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="0218f-129">Developer portal templates</span></span>  
 <span data-ttu-id="0218f-130">`app-actions` 控制項可用於下列開發人員入口網站範本。</span><span class="sxs-lookup"><span data-stu-id="0218f-130">The `app-actions` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="0218f-131">應用程式</span><span class="sxs-lookup"><span data-stu-id="0218f-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="0218f-132"><a name="basic-signin"></a>basic-signin</span><span class="sxs-lookup"><span data-stu-id="0218f-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="0218f-133">`basic-signin` 控制項會提供用來在開發人員入口網站的登入頁面中收集使用者登入資訊的控制項。</span><span class="sxs-lookup"><span data-stu-id="0218f-133">The `basic-signin` control provides a control for collecting user sign in information in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="0218f-134">![basic&#45;signin 控制項](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin 控制項")</span><span class="sxs-lookup"><span data-stu-id="0218f-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="0218f-135">使用量</span><span class="sxs-lookup"><span data-stu-id="0218f-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="0218f-136">參數</span><span class="sxs-lookup"><span data-stu-id="0218f-136">Parameters</span></span>  
 <span data-ttu-id="0218f-137">無。</span><span class="sxs-lookup"><span data-stu-id="0218f-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="0218f-138">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="0218f-138">Developer portal templates</span></span>  
 <span data-ttu-id="0218f-139">`basic-signin` 控制項可用於下列開發人員入口網站範本。</span><span class="sxs-lookup"><span data-stu-id="0218f-139">The `basic-signin` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="0218f-140">登入</span><span class="sxs-lookup"><span data-stu-id="0218f-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="0218f-141"><a name="paging-control"></a>paging-control</span><span class="sxs-lookup"><span data-stu-id="0218f-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="0218f-142">`paging-control` 會在顯示項目清單的開發人員入口網站頁面上提供分頁功能。</span><span class="sxs-lookup"><span data-stu-id="0218f-142">The `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="0218f-143">![分頁控制項](./media/api-management-page-controls/APIM-paging-control.png "APIM 分頁控制項")</span><span class="sxs-lookup"><span data-stu-id="0218f-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="0218f-144">使用量</span><span class="sxs-lookup"><span data-stu-id="0218f-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="0218f-145">參數</span><span class="sxs-lookup"><span data-stu-id="0218f-145">Parameters</span></span>  
 <span data-ttu-id="0218f-146">無。</span><span class="sxs-lookup"><span data-stu-id="0218f-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="0218f-147">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="0218f-147">Developer portal templates</span></span>  
 <span data-ttu-id="0218f-148">`paging-control` 控制項可用於下列開發人員入口網站範本。</span><span class="sxs-lookup"><span data-stu-id="0218f-148">The `paging-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="0218f-149">API 清單</span><span class="sxs-lookup"><span data-stu-id="0218f-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="0218f-150">問題清單</span><span class="sxs-lookup"><span data-stu-id="0218f-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="0218f-151">產品清單</span><span class="sxs-lookup"><span data-stu-id="0218f-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="0218f-152"><a name="providers"></a>providers</span><span class="sxs-lookup"><span data-stu-id="0218f-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="0218f-153">`providers` 控制項會提供用來在開發人員入口網站的登入頁面中選取驗證提供者的控制項。</span><span class="sxs-lookup"><span data-stu-id="0218f-153">The `providers` control provides a control for selection of authentication providers in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="0218f-154">![提供者控制項](./media/api-management-page-controls/APIM-providers-control.png "APIM 提供者控制項")</span><span class="sxs-lookup"><span data-stu-id="0218f-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="0218f-155">使用量</span><span class="sxs-lookup"><span data-stu-id="0218f-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="0218f-156">參數</span><span class="sxs-lookup"><span data-stu-id="0218f-156">Parameters</span></span>  
 <span data-ttu-id="0218f-157">無。</span><span class="sxs-lookup"><span data-stu-id="0218f-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="0218f-158">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="0218f-158">Developer portal templates</span></span>  
 <span data-ttu-id="0218f-159">`providers` 控制項可用於下列開發人員入口網站範本。</span><span class="sxs-lookup"><span data-stu-id="0218f-159">The `providers` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="0218f-160">登入</span><span class="sxs-lookup"><span data-stu-id="0218f-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="0218f-161"><a name="search-control"></a>search-control</span><span class="sxs-lookup"><span data-stu-id="0218f-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="0218f-162">`search-control` 會在顯示項目清單的開發人員入口網站頁面上提供搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="0218f-162">The `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="0218f-163">![搜尋控制項](./media/api-management-page-controls/APIM-search-control.png "APIM 搜尋控制項")</span><span class="sxs-lookup"><span data-stu-id="0218f-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="0218f-164">使用量</span><span class="sxs-lookup"><span data-stu-id="0218f-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="0218f-165">參數</span><span class="sxs-lookup"><span data-stu-id="0218f-165">Parameters</span></span>  
 <span data-ttu-id="0218f-166">無。</span><span class="sxs-lookup"><span data-stu-id="0218f-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="0218f-167">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="0218f-167">Developer portal templates</span></span>  
 <span data-ttu-id="0218f-168">`search-control` 控制項可用於下列開發人員入口網站範本。</span><span class="sxs-lookup"><span data-stu-id="0218f-168">The `search-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="0218f-169">API 清單</span><span class="sxs-lookup"><span data-stu-id="0218f-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="0218f-170">產品清單</span><span class="sxs-lookup"><span data-stu-id="0218f-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="0218f-171"><a name="sign-up"></a>sign-up</span><span class="sxs-lookup"><span data-stu-id="0218f-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="0218f-172">`sign-up` 控制項會提供用來在開發人員入口網站的註冊頁面中收集使用者設定檔資訊的控制項。</span><span class="sxs-lookup"><span data-stu-id="0218f-172">The `sign-up` control provides a control for collecting user profile information in the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="0218f-173">![註冊控制項](./media/api-management-page-controls/APIM-sign-up-control.png "APIM 註冊控制項")</span><span class="sxs-lookup"><span data-stu-id="0218f-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="0218f-174">使用量</span><span class="sxs-lookup"><span data-stu-id="0218f-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="0218f-175">參數</span><span class="sxs-lookup"><span data-stu-id="0218f-175">Parameters</span></span>  
 <span data-ttu-id="0218f-176">無。</span><span class="sxs-lookup"><span data-stu-id="0218f-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="0218f-177">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="0218f-177">Developer portal templates</span></span>  
 <span data-ttu-id="0218f-178">`sign-up` 控制項可用於下列開發人員入口網站範本。</span><span class="sxs-lookup"><span data-stu-id="0218f-178">The `sign-up` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="0218f-179">註冊</span><span class="sxs-lookup"><span data-stu-id="0218f-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="0218f-180"><a name="subscribe-button"></a>subscribe-button</span><span class="sxs-lookup"><span data-stu-id="0218f-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="0218f-181">`subscribe-button` 會提供用來為使用者訂閱產品的控制項。</span><span class="sxs-lookup"><span data-stu-id="0218f-181">The `subscribe-button` provides a control for subscribing a user to a product.</span></span>  
  
 <span data-ttu-id="0218f-182">![subscribe&#45;button 控制項](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button 控制項")</span><span class="sxs-lookup"><span data-stu-id="0218f-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="0218f-183">使用量</span><span class="sxs-lookup"><span data-stu-id="0218f-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="0218f-184">參數</span><span class="sxs-lookup"><span data-stu-id="0218f-184">Parameters</span></span>  
 <span data-ttu-id="0218f-185">無。</span><span class="sxs-lookup"><span data-stu-id="0218f-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="0218f-186">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="0218f-186">Developer portal templates</span></span>  
 <span data-ttu-id="0218f-187">`subscribe-button` 控制項可用於下列開發人員入口網站範本。</span><span class="sxs-lookup"><span data-stu-id="0218f-187">The `subscribe-button` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="0218f-188">產品</span><span class="sxs-lookup"><span data-stu-id="0218f-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="0218f-189"><a name="subscription-cancel"></a>subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="0218f-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="0218f-190">`subscription-cancel` 控制項會提供可在開發人員入口網站的 [使用者設定檔] 頁面中取消產品訂閱的控制項。</span><span class="sxs-lookup"><span data-stu-id="0218f-190">The `subscription-cancel` control provides a control for cancelling a subscription to a product in the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="0218f-191">![subscription&#45;cancel 控制項](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel 控制項")</span><span class="sxs-lookup"><span data-stu-id="0218f-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="0218f-192">使用量</span><span class="sxs-lookup"><span data-stu-id="0218f-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="0218f-193">參數</span><span class="sxs-lookup"><span data-stu-id="0218f-193">Parameters</span></span>  
  
|<span data-ttu-id="0218f-194">參數</span><span class="sxs-lookup"><span data-stu-id="0218f-194">Parameter</span></span>|<span data-ttu-id="0218f-195">說明</span><span class="sxs-lookup"><span data-stu-id="0218f-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="0218f-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="0218f-196">subscriptionId</span></span>|<span data-ttu-id="0218f-197">要取消之訂用帳戶的識別碼。</span><span class="sxs-lookup"><span data-stu-id="0218f-197">The id of the subscription to cancel.</span></span>|  
|<span data-ttu-id="0218f-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="0218f-198">cancelUrl</span></span>|<span data-ttu-id="0218f-199">訂用帳戶取消 URL。</span><span class="sxs-lookup"><span data-stu-id="0218f-199">The subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="0218f-200">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="0218f-200">Developer portal templates</span></span>  
 <span data-ttu-id="0218f-201">`subscription-cancel` 控制項可用於下列開發人員入口網站範本。</span><span class="sxs-lookup"><span data-stu-id="0218f-201">The `subscription-cancel` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="0218f-202">產品</span><span class="sxs-lookup"><span data-stu-id="0218f-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="0218f-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0218f-203">Next steps</span></span>
<span data-ttu-id="0218f-204">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="0218f-204">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
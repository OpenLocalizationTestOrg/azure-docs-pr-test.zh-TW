---
title: "aaaAzure API 管理頁面控制項 |Microsoft 文件"
description: "深入了解適用於在 Azure API 管理開發人員入口網站範本中所使用的 hello 頁面控制項。"
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
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="5e2b8-103">Azure API 管理的頁面控制項</span><span class="sxs-lookup"><span data-stu-id="5e2b8-103">Azure API Management page controls</span></span>
<span data-ttu-id="5e2b8-104">Azure API 管理提供 hello hello 開發人員入口網站範本中所使用的控制項。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-104">Azure API Management provides hello following controls for use in hello developer portal templates.</span></span>  
  
 <span data-ttu-id="5e2b8-105">toouse 控制項，將它放在預期的 hello 位置 hello 開發人員入口網站範本中。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-105">toouse a control, place it in hello desired location in hello developer portal template.</span></span> <span data-ttu-id="5e2b8-106">某些控制項，例如 hello[應用程式動作](#app-actions)控制項，具有參數，hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-106">Some controls, such as hello [app-actions](#app-actions) control, have parameters, as shown in hello following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="5e2b8-107">hello hello 參數值傳入 hello 範本的 hello 資料模型的一部分。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-107">hello values for hello parameters are passed in as part of hello data model for hello template.</span></span> <span data-ttu-id="5e2b8-108">在大部分情況下，您可以只要貼在 hello 範例的每個控制項為它提供 toowork 正確。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-108">In most cases, you can simply paste in hello provided example for each control for it toowork correctly.</span></span> <span data-ttu-id="5e2b8-109">如需有關 hello 參數值的詳細資訊，您可以看到每個範本可能可使用之控制項的 hello 資料模型區段。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-109">For more information on hello parameter values, you can see hello data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="5e2b8-110">如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="5e2b8-111">開發人員入口網站範本頁面控制項</span><span class="sxs-lookup"><span data-stu-id="5e2b8-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="5e2b8-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="5e2b8-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="5e2b8-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="5e2b8-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="5e2b8-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="5e2b8-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="5e2b8-115">提供者</span><span class="sxs-lookup"><span data-stu-id="5e2b8-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="5e2b8-116">search-control</span><span class="sxs-lookup"><span data-stu-id="5e2b8-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="5e2b8-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="5e2b8-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="5e2b8-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="5e2b8-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="5e2b8-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="5e2b8-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="5e2b8-120"><a name="app-actions"></a>app-actions</span><span class="sxs-lookup"><span data-stu-id="5e2b8-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="5e2b8-121">hello`app-actions`控制項可提供使用者介面與 hello 開發人員入口網站中的 hello 使用者設定檔頁面上的應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-121">hello `app-actions` control provides a user interface for interacting with applications on hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5e2b8-122">![app&#45;actions 控制項](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions 控制項")</span><span class="sxs-lookup"><span data-stu-id="5e2b8-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="5e2b8-123">使用量</span><span class="sxs-lookup"><span data-stu-id="5e2b8-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="5e2b8-124">參數</span><span class="sxs-lookup"><span data-stu-id="5e2b8-124">Parameters</span></span>  
  
|<span data-ttu-id="5e2b8-125">參數</span><span class="sxs-lookup"><span data-stu-id="5e2b8-125">Parameter</span></span>|<span data-ttu-id="5e2b8-126">說明</span><span class="sxs-lookup"><span data-stu-id="5e2b8-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="5e2b8-127">appId</span><span class="sxs-lookup"><span data-stu-id="5e2b8-127">appId</span></span>|<span data-ttu-id="5e2b8-128">hello hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-128">hello id of hello application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="5e2b8-129">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="5e2b8-129">Developer portal templates</span></span>  
 <span data-ttu-id="5e2b8-130">hello `app-actions` hello 遵循開發人員入口網站的範本可用來控制。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-130">hello `app-actions` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="5e2b8-131">應用程式</span><span class="sxs-lookup"><span data-stu-id="5e2b8-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="5e2b8-132"><a name="basic-signin"></a>basic-signin</span><span class="sxs-lookup"><span data-stu-id="5e2b8-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="5e2b8-133">hello`basic-signin`控制項提供的控制項，如收集的使用者登入資訊在 hello 登入 hello 開發人員入口網站中的頁面。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-133">hello `basic-signin` control provides a control for collecting user sign in information in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5e2b8-134">![basic&#45;signin 控制項](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin 控制項")</span><span class="sxs-lookup"><span data-stu-id="5e2b8-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="5e2b8-135">使用量</span><span class="sxs-lookup"><span data-stu-id="5e2b8-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="5e2b8-136">參數</span><span class="sxs-lookup"><span data-stu-id="5e2b8-136">Parameters</span></span>  
 <span data-ttu-id="5e2b8-137">無。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="5e2b8-138">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="5e2b8-138">Developer portal templates</span></span>  
 <span data-ttu-id="5e2b8-139">hello `basic-signin` hello 遵循開發人員入口網站的範本可用來控制。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-139">hello `basic-signin` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="5e2b8-140">登入</span><span class="sxs-lookup"><span data-stu-id="5e2b8-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="5e2b8-141"><a name="paging-control"></a>paging-control</span><span class="sxs-lookup"><span data-stu-id="5e2b8-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="5e2b8-142">hello`paging-control`提供開發人員入口網站頁面顯示項目清單的分頁功能。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-142">hello `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="5e2b8-143">![分頁控制項](./media/api-management-page-controls/APIM-paging-control.png "APIM 分頁控制項")</span><span class="sxs-lookup"><span data-stu-id="5e2b8-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="5e2b8-144">使用量</span><span class="sxs-lookup"><span data-stu-id="5e2b8-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="5e2b8-145">參數</span><span class="sxs-lookup"><span data-stu-id="5e2b8-145">Parameters</span></span>  
 <span data-ttu-id="5e2b8-146">無。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="5e2b8-147">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="5e2b8-147">Developer portal templates</span></span>  
 <span data-ttu-id="5e2b8-148">hello `paging-control` hello 遵循開發人員入口網站的範本可用來控制。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-148">hello `paging-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="5e2b8-149">API 清單</span><span class="sxs-lookup"><span data-stu-id="5e2b8-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="5e2b8-150">問題清單</span><span class="sxs-lookup"><span data-stu-id="5e2b8-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="5e2b8-151">產品清單</span><span class="sxs-lookup"><span data-stu-id="5e2b8-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="5e2b8-152"><a name="providers"></a>providers</span><span class="sxs-lookup"><span data-stu-id="5e2b8-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="5e2b8-153">hello`providers`控制項提供的驗證提供者在 hello 登入 hello 開發人員入口網站中的頁面中選取的控制項。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-153">hello `providers` control provides a control for selection of authentication providers in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5e2b8-154">![提供者控制項](./media/api-management-page-controls/APIM-providers-control.png "APIM 提供者控制項")</span><span class="sxs-lookup"><span data-stu-id="5e2b8-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="5e2b8-155">使用量</span><span class="sxs-lookup"><span data-stu-id="5e2b8-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="5e2b8-156">參數</span><span class="sxs-lookup"><span data-stu-id="5e2b8-156">Parameters</span></span>  
 <span data-ttu-id="5e2b8-157">無。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="5e2b8-158">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="5e2b8-158">Developer portal templates</span></span>  
 <span data-ttu-id="5e2b8-159">hello `providers` hello 遵循開發人員入口網站的範本可用來控制。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-159">hello `providers` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="5e2b8-160">登入</span><span class="sxs-lookup"><span data-stu-id="5e2b8-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="5e2b8-161"><a name="search-control"></a>search-control</span><span class="sxs-lookup"><span data-stu-id="5e2b8-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="5e2b8-162">hello`search-control`提供開發人員入口網站頁面顯示項目清單的搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-162">hello `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="5e2b8-163">![搜尋控制項](./media/api-management-page-controls/APIM-search-control.png "APIM 搜尋控制項")</span><span class="sxs-lookup"><span data-stu-id="5e2b8-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="5e2b8-164">使用量</span><span class="sxs-lookup"><span data-stu-id="5e2b8-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="5e2b8-165">參數</span><span class="sxs-lookup"><span data-stu-id="5e2b8-165">Parameters</span></span>  
 <span data-ttu-id="5e2b8-166">無。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="5e2b8-167">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="5e2b8-167">Developer portal templates</span></span>  
 <span data-ttu-id="5e2b8-168">hello `search-control` hello 遵循開發人員入口網站的範本可用來控制。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-168">hello `search-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="5e2b8-169">API 清單</span><span class="sxs-lookup"><span data-stu-id="5e2b8-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="5e2b8-170">產品清單</span><span class="sxs-lookup"><span data-stu-id="5e2b8-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="5e2b8-171"><a name="sign-up"></a>sign-up</span><span class="sxs-lookup"><span data-stu-id="5e2b8-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="5e2b8-172">hello`sign-up`控制項提供控制項，以收集 hello 註冊 頁面中 hello 開發人員入口網站中的使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-172">hello `sign-up` control provides a control for collecting user profile information in hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5e2b8-173">![註冊控制項](./media/api-management-page-controls/APIM-sign-up-control.png "APIM 註冊控制項")</span><span class="sxs-lookup"><span data-stu-id="5e2b8-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="5e2b8-174">使用量</span><span class="sxs-lookup"><span data-stu-id="5e2b8-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="5e2b8-175">參數</span><span class="sxs-lookup"><span data-stu-id="5e2b8-175">Parameters</span></span>  
 <span data-ttu-id="5e2b8-176">無。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="5e2b8-177">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="5e2b8-177">Developer portal templates</span></span>  
 <span data-ttu-id="5e2b8-178">hello `sign-up` hello 遵循開發人員入口網站的範本可用來控制。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-178">hello `sign-up` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="5e2b8-179">註冊</span><span class="sxs-lookup"><span data-stu-id="5e2b8-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="5e2b8-180"><a name="subscribe-button"></a>subscribe-button</span><span class="sxs-lookup"><span data-stu-id="5e2b8-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="5e2b8-181">hello`subscribe-button`訂閱使用者 tooa 產品提供的控制項。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-181">hello `subscribe-button` provides a control for subscribing a user tooa product.</span></span>  
  
 <span data-ttu-id="5e2b8-182">![subscribe&#45;button 控制項](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button 控制項")</span><span class="sxs-lookup"><span data-stu-id="5e2b8-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="5e2b8-183">使用量</span><span class="sxs-lookup"><span data-stu-id="5e2b8-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="5e2b8-184">參數</span><span class="sxs-lookup"><span data-stu-id="5e2b8-184">Parameters</span></span>  
 <span data-ttu-id="5e2b8-185">無。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="5e2b8-186">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="5e2b8-186">Developer portal templates</span></span>  
 <span data-ttu-id="5e2b8-187">hello `subscribe-button` hello 遵循開發人員入口網站的範本可用來控制。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-187">hello `subscribe-button` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="5e2b8-188">產品</span><span class="sxs-lookup"><span data-stu-id="5e2b8-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="5e2b8-189"><a name="subscription-cancel"></a>subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="5e2b8-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="5e2b8-190">hello`subscription-cancel`控制項取消訂閱 tooa 產品 hello 開發人員入口網站中的 hello 使用者設定檔頁面中提供的控制項。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-190">hello `subscription-cancel` control provides a control for cancelling a subscription tooa product in hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5e2b8-191">![subscription&#45;cancel 控制項](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel 控制項")</span><span class="sxs-lookup"><span data-stu-id="5e2b8-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="5e2b8-192">使用量</span><span class="sxs-lookup"><span data-stu-id="5e2b8-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="5e2b8-193">參數</span><span class="sxs-lookup"><span data-stu-id="5e2b8-193">Parameters</span></span>  
  
|<span data-ttu-id="5e2b8-194">參數</span><span class="sxs-lookup"><span data-stu-id="5e2b8-194">Parameter</span></span>|<span data-ttu-id="5e2b8-195">說明</span><span class="sxs-lookup"><span data-stu-id="5e2b8-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="5e2b8-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="5e2b8-196">subscriptionId</span></span>|<span data-ttu-id="5e2b8-197">hello 訂用帳戶 toocancel hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-197">hello id of hello subscription toocancel.</span></span>|  
|<span data-ttu-id="5e2b8-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="5e2b8-198">cancelUrl</span></span>|<span data-ttu-id="5e2b8-199">hello 訂用帳戶取消 URL。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-199">hello subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="5e2b8-200">開發人員入口網站範本</span><span class="sxs-lookup"><span data-stu-id="5e2b8-200">Developer portal templates</span></span>  
 <span data-ttu-id="5e2b8-201">hello `subscription-cancel` hello 遵循開發人員入口網站的範本可用來控制。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-201">hello `subscription-cancel` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="5e2b8-202">產品</span><span class="sxs-lookup"><span data-stu-id="5e2b8-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="5e2b8-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e2b8-203">Next steps</span></span>
<span data-ttu-id="5e2b8-204">如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="5e2b8-204">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>

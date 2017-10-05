---
title: "在 Azure API 管理中管理您的第一個 API | Microsoft Docs"
description: "了解如何建立 API、加入作業，以及開始使用 API 管理。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 6e76d1ee08f804637999ef2ebf5d25becf6a0408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="1ee6e-103">在 Azure API 管理中管理您的第一個 API</span><span class="sxs-lookup"><span data-stu-id="1ee6e-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="1ee6e-104"><a name="overview"> </a>概觀</span><span class="sxs-lookup"><span data-stu-id="1ee6e-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="1ee6e-105">本指南示範如何快速開始使用 Azure API 管理，以及進行您的第一個 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-105">This guide shows you how to quickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="1ee6e-106"><a name="concepts"> </a>什麼是 Azure API 管理？</span><span class="sxs-lookup"><span data-stu-id="1ee6e-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="1ee6e-107">您可以使用 Azure API 管理來取得任何後端，並根據該後端來啟用完善的 API 方案。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-107">You can use Azure API Management to take any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="1ee6e-108">常見案例包括：</span><span class="sxs-lookup"><span data-stu-id="1ee6e-108">Common scenarios include:</span></span>

* <span data-ttu-id="1ee6e-109">**保護行動基礎結構** 。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="1ee6e-110">**促成 ISV 合作夥伴生態系統** 。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through the developer portal and building an API facade to decouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="1ee6e-111">**執行內部 API 方案** 。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-111">**Running an internal API program** by offering a centralized location for the organization to communicate about the availability and latest changes to APIs, gating access based on organizational accounts, all based on a secured channel between the API gateway and the backend.</span></span>

<span data-ttu-id="1ee6e-112">系統是由下列元件所組成：</span><span class="sxs-lookup"><span data-stu-id="1ee6e-112">The system is made up of the following components:</span></span>

* <span data-ttu-id="1ee6e-113">**API 閘道** 是可執行以下作業的端點：</span><span class="sxs-lookup"><span data-stu-id="1ee6e-113">The **API gateway** is the endpoint that:</span></span>
  
  * <span data-ttu-id="1ee6e-114">接受 API 呼叫，並將這些呼叫路由傳送到您的後端。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-114">Accepts API calls and routes them to your backends.</span></span>
  * <span data-ttu-id="1ee6e-115">驗證 API 金鑰、JWT 權杖、憑證和其他認證。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="1ee6e-116">強制採用使用量配額和頻率限制。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="1ee6e-117">即時轉換您的 API 且不需修改程式碼。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-117">Transforms your API on the fly without code modifications.</span></span>
  * <span data-ttu-id="1ee6e-118">快取設定的後端回應。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="1ee6e-119">記錄呼叫中繼資料以供分析使用。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="1ee6e-120">**發行者入口網站** 是您設定 API 方案的管理介面。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-120">The **publisher portal** is the administrative interface where you set up your API program.</span></span> <span data-ttu-id="1ee6e-121">使用方式：</span><span class="sxs-lookup"><span data-stu-id="1ee6e-121">Use it to:</span></span>
  
  * <span data-ttu-id="1ee6e-122">定義或匯入 API 結構描述。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-122">Define or import API schema.</span></span>
  * <span data-ttu-id="1ee6e-123">將 API 封裝至產品。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-123">Package APIs into products.</span></span>
  * <span data-ttu-id="1ee6e-124">設定原則，例如 API 的配額或轉換。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-124">Set up policies like quotas or transformations on the APIs.</span></span>
  * <span data-ttu-id="1ee6e-125">從分析中取得見解。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="1ee6e-126">管理使用者。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-126">Manage users.</span></span>
* <span data-ttu-id="1ee6e-127">**開發人員入口網站** 是供開發人員執行以下作業的主要網站空間：</span><span class="sxs-lookup"><span data-stu-id="1ee6e-127">The **developer portal** serves as the main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="1ee6e-128">閱讀 API 文件。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-128">Read API documentation.</span></span>
  * <span data-ttu-id="1ee6e-129">透過互動式主控台試用 API。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-129">Try out an API via the interactive console.</span></span>
  * <span data-ttu-id="1ee6e-130">建立帳戶，並訂閱以取得 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-130">Create an account and subscribe to get API keys.</span></span>
  * <span data-ttu-id="1ee6e-131">存取他們的使用量分析資料。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="1ee6e-132"><a name="create-service-instance"> </a>建立 API 管理執行個體</span><span class="sxs-lookup"><span data-stu-id="1ee6e-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="1ee6e-133">若要完成此教學課程，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-133">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="1ee6e-134">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="1ee6e-135">如需詳細資訊，請參閱 [Azure 免費試用][Azure Free Trial]。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="1ee6e-136">使用 API 管理的第一個步驟是建立服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-136">The first step in working with API Management is to create a service instance.</span></span> <span data-ttu-id="1ee6e-137">登入 [Azure 入口網站][Azure Portal]，然後按一下 [新增]、[Web + 行動]、[API 管理]。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-137">Sign in to the [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![API Management new instance][api-management-create-instance-menu]

<span data-ttu-id="1ee6e-139">針對 [名稱]，指定要用於服務 URL 的唯一子網域名稱。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-139">For **Name**, specify a unique sub-domain name to use for the service URL.</span></span>

<span data-ttu-id="1ee6e-140">針對您的服務執行個體，選擇需要的 [訂用帳戶]、[資源群組] 和 [位置]。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-140">Choose the desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="1ee6e-141">輸入 **Contoso Ltd.**</span><span class="sxs-lookup"><span data-stu-id="1ee6e-141">Enter **Contoso Ltd.**</span></span> <span data-ttu-id="1ee6e-142">做為 [組織名稱]，然後在 [管理員電子郵件] 欄位中輸入您的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-142">for the **Organization Name**, and enter your email address in the **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="1ee6e-143">此電子郵件地址將用於自 API 管理系統傳送通知。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-143">This email address is used for notifications from the API Management system.</span></span> <span data-ttu-id="1ee6e-144">如需詳細資訊，請參閱[如何在 Azure API 管理中設定通知和電子郵件範本][How to configure notifications and email templates in Azure API Management]。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-144">For more information, see [How to configure notifications and email templates in Azure API Management][How to configure notifications and email templates in Azure API Management].</span></span>
> 
> 

![New API Management service][api-management-create-instance-step1]

<span data-ttu-id="1ee6e-146">API 管理服務執行個體共有三種層次：開發人員、標準和高階。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-146">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="1ee6e-147">開發人員階層可用來針對不注重高可用性的 API 程式進行開發、測試及試驗。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-147">The Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="1ee6e-148">在「標準」和「高階」層次中，您可以調整保留的單位計數以處理更多流量。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-148">In the Standard and Premium tiers, you can scale your reserved unit count to handle more traffic.</span></span> <span data-ttu-id="1ee6e-149">「標準」和「高階」層次可為您的 API 管理服務提供最高的處理能力和效能。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-149">The Standard and Premium tiers provide your API Management service with the most processing power and performance.</span></span> <span data-ttu-id="1ee6e-150">您可以使用任何階層來完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-150">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="1ee6e-151">如需關於 API 管理層次的詳細資訊，請參閱 [API 管理價格][API Management pricing]。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-151">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="1ee6e-152">按一下 [建立] 以開始佈建您的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-152">Click **Create** to start provisioning your service instance.</span></span>

![New API Management service][api-management-instance-created]

<span data-ttu-id="1ee6e-154">建立服務執行個體之後，下一步是建立或匯入 API。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-154">Once the service instance is created, the next step is to create or import an API.</span></span>

## <span data-ttu-id="1ee6e-155"><a name="create-api"> </a>匯入 API</span><span class="sxs-lookup"><span data-stu-id="1ee6e-155"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="1ee6e-156">API 包含可自用戶端應用程式叫用的一組作業。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-156">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="1ee6e-157">API 作業會代理到現有的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-157">API operations are proxied to existing web services.</span></span>

<span data-ttu-id="1ee6e-158">您可以手動建立 API (並可加入作業)，或是匯入這兩者。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-158">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="1ee6e-159">在本教學課程中，我們將針對由 Microsoft 所提供且裝載在 Azure 上的範例計算機 Web 服務來匯入 API。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-159">In this tutorial, we will import the API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="1ee6e-160">如需建立 API 和手動新增作業的指引，請參閱[如何建立 API](api-management-howto-create-apis.md) 和[如何將作業新增至 API](api-management-howto-add-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-160">For guidance on creating an API and manually adding operations, see [How to create APIs](api-management-howto-create-apis.md) and [How to add operations to an API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="1ee6e-161">API 是從發佈者入口網站進行設定。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-161">APIs are configured from the publisher portal.</span></span> <span data-ttu-id="1ee6e-162">若要觸達它，請從服務工具列按一下 [發佈者入口網站]。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-162">To reach it, click **Publisher portal** from the service toolbar.</span></span>

![發行者入口網站][api-management-management-console]

<span data-ttu-id="1ee6e-164">若要匯入計算機 API，請從左邊的 [API 管理] 功能表中按一下 [API]，然後按一下 [匯入 API]。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-164">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![匯入 API 按鈕][api-management-import-api]

<span data-ttu-id="1ee6e-166">執行下列步驟來設定計算機 API：</span><span class="sxs-lookup"><span data-stu-id="1ee6e-166">Perform the following steps to configure the calculator API:</span></span>

1. <span data-ttu-id="1ee6e-167">按一下 [從 URL]，在 [規格文件 URL] 文字方塊中輸入 **http://calcapi.cloudapp.net/calcapi.json**，然後按一下 [Swagger] 選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-167">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into the **Specification document URL** text box, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="1ee6e-168">在 [Web API URL 尾碼] 文字方塊中，輸入 **calc**。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-168">Type **calc** into the **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="1ee6e-169">按一下 [產品 (選擇性)] 方塊，然後選擇 [入門]。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-169">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="1ee6e-170">按一下 [ **儲存** ] 匯入 API。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-170">Click **Save** to import the API.</span></span>

![Add new API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="1ee6e-172">**API 管理**目前支援匯入 1.2 和 2.0 版本的 Swagger 文件。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-172">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="1ee6e-173">即使 [Swagger 2.0 規格](http://swagger.io/specification)表示 `host`、`basePath` 和 `schemes` 是選擇性的屬性，請確定您的 Swagger 2.0 文件**必須**包含這些屬性，否則無法匯入。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-173">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="1ee6e-174">匯入 API 之後，API 的摘要頁面隨即會顯示在發行者入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-174">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

![API summary][api-management-imported-api-summary]

<span data-ttu-id="1ee6e-176">API 區段有一些索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-176">The API section has several tabs.</span></span> <span data-ttu-id="1ee6e-177">[摘要]  索引標籤會顯示 API 的基本度量和相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-177">The **Summary** tab displays basic metrics and information about the API.</span></span> <span data-ttu-id="1ee6e-178">[設定](api-management-howto-create-apis.md#configure-api-settings) 索引標籤可用來檢視和編輯 API 的組態。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-178">The [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used to view and edit the configuration for an API.</span></span> <span data-ttu-id="1ee6e-179">[作業](api-management-howto-add-operations.md) 索引標籤可用來管理 API 的作業。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-179">The [Operations](api-management-howto-add-operations.md) tab is used to manage the API's operations.</span></span> <span data-ttu-id="1ee6e-180">[安全性] 索引標籤可用來將後端伺服器的閘道驗證設定為使用基本驗證或[相互憑證驗證](api-management-howto-mutual-certificates.md)，以及用來設定[使用 OAuth 2.0 的使用者授權](api-management-howto-oauth2.md)。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-180">The **Security** tab can be used to configure gateway authentication for the backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and to configure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="1ee6e-181">[問題]  索引標籤是用來檢視使用您 API 的開發人員所報告的問題。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-181">The **Issues** tab is used to view issues reported by the developers who are using your APIs.</span></span> <span data-ttu-id="1ee6e-182">[產品]  索引標籤是用來設定包含此 API 的產品。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-182">The **Products** tab is used to configure the products that contain this API.</span></span>

<span data-ttu-id="1ee6e-183">依預設，每個 API 管理執行個體會隨附兩個範例產品：</span><span class="sxs-lookup"><span data-stu-id="1ee6e-183">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="1ee6e-184">**入門**</span><span class="sxs-lookup"><span data-stu-id="1ee6e-184">**Starter**</span></span>
* <span data-ttu-id="1ee6e-185">**無限制**</span><span class="sxs-lookup"><span data-stu-id="1ee6e-185">**Unlimited**</span></span>

<span data-ttu-id="1ee6e-186">在本教學課程中，Basic Calculator API 已在匯入 API 時加入至「入門」產品。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-186">In this tutorial, the Basic Calculator API was added to the Starter product when the API was imported.</span></span>

<span data-ttu-id="1ee6e-187">若要呼叫 API，開發人員必須先訂閱能夠讓他們存取 API 的產品。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-187">In order to make calls to an API, developers must first subscribe to a product that gives them access to it.</span></span> <span data-ttu-id="1ee6e-188">開發人員可以在開發人員入口網站中訂閱產品，或者管理員也可以在發行者入口網站中為開發人員訂閱產品。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-188">Developers can subscribe to products in the developer portal, or administrators can subscribe developers to products in the publisher portal.</span></span> <span data-ttu-id="1ee6e-189">由於您在先前的教學課程步驟中建立了 API 管理執行個體，因此您是管理員，且已根據預設訂閱了所有產品。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-189">You are an administrator since you created the API Management instance in the previous steps in the tutorial, so you are already subscribed to every product by default.</span></span>

## <span data-ttu-id="1ee6e-190"><a name="call-operation"> </a>從開發人員入口網站呼叫作業</span><span class="sxs-lookup"><span data-stu-id="1ee6e-190"><a name="call-operation"> </a>Call an operation from the developer portal</span></span>
<span data-ttu-id="1ee6e-191">您可以從開發人員入口網站直接呼叫作業，以便檢視和測試 API 的操作。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-191">Operations can be called directly from the developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="1ee6e-192">在本教學課程步驟中，您將會呼叫 Basic Calculator API 的 **Add two integers** 作業。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-192">In this tutorial step, you will call the Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="1ee6e-193">從發行者入口網站右上角的功能表中，按一下 [ **開發人員入口網站** ]。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-193">Click **Developer portal** from the menu at the top right of the publisher portal.</span></span>

![開發人員入口網站][api-management-developer-portal-menu]

<span data-ttu-id="1ee6e-195">按一下頂端功能表中的 [API]，然後按一下 [Basic Calculator] 來查看可用作業。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-195">Click **APIs** from the top menu, and then click **Basic Calculator** to see the available operations.</span></span>

![開發人員入口網站][api-management-developer-portal-calc-api]

<span data-ttu-id="1ee6e-197">請記下和 API 及作業一起匯入的範例說明與參數，為要使用此作業的開發人員提供文件。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-197">Note the sample descriptions and parameters that were imported along with the API and operations, providing documentation for the developers that will use this operation.</span></span> <span data-ttu-id="1ee6e-198">手動加入作業時，也可以加入這些說明。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-198">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="1ee6e-199">若要呼叫 **Add two integers** 作業，請按一下 [試試看]。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-199">To call the **Add two integers** operation, click **Try it**.</span></span>

![試試看][api-management-developer-portal-calc-api-console]

<span data-ttu-id="1ee6e-201">您可以輸入部分參數值或保留預設值，然後按一下 [傳送] 。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-201">You can enter some values for the parameters or keep the defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="1ee6e-203">叫用作業之後，開發人員入口網站會顯示 [回應狀態]、[回應標頭]，以及任何的 [回應內容]。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-203">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![Response][api-management-invoke-get-response]

## <span data-ttu-id="1ee6e-205"><a name="view-analytics"> </a>檢視分析</span><span class="sxs-lookup"><span data-stu-id="1ee6e-205"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="1ee6e-206">若要檢視 Basic Calculator 的分析，可從開發人員入口網站右上角的功能表中選取 [管理]  ，以切換回發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-206">To view analytics for Basic Calculator, switch back to the publisher portal by selecting **Manage** from the menu at the top right of the developer portal.</span></span>

![管理][api-management-manage-menu]

<span data-ttu-id="1ee6e-208">發行者入口網站的預設檢視為 **儀表板**，其中提供您 API 管理執行個體的概觀。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-208">The default view for the publisher portal is the **Dashboard**, which provides an overview of your API Management instance.</span></span>

![儀表板][api-management-dashboard]

<span data-ttu-id="1ee6e-210">將滑鼠游標移到 **Basic Calculator** 的圖表上，以查看指定時段中 API 使用量的特定度量。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-210">Hover the mouse over the chart for **Basic Calculator** to see the specific metrics for the usage of the API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="1ee6e-211">如果您在圖表上看不見任何線條，請切換回開發人員入口網站，並對 API 進行一些呼叫，等候片刻，然後返回儀表板。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-211">If you don't see any lines on your chart, switch back to the developer portal and make some calls into the API, wait a few moments, and then come back to the dashboard.</span></span>
> 
> 

<span data-ttu-id="1ee6e-212">按一下 [檢視詳細資料]  來檢視 API 的摘要頁面，包括已顯示度量的較大版本。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-212">Click **View Details** to view the summary page for the API, including a larger version of the displayed metrics.</span></span>

![Analytics][api-management-mouse-over]

![摘要][api-management-api-summary-metrics]

<span data-ttu-id="1ee6e-215">如需詳細度量和報告，請從左側的 [API 管理] 功能表按一下 [分析]。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-215">For detailed metrics and reports, click **Analytics** from the **API Management** menu on the left.</span></span>

![Overview][api-management-analytics-overview]

<span data-ttu-id="1ee6e-217">[分析]  區段具有下列四個索引標籤：</span><span class="sxs-lookup"><span data-stu-id="1ee6e-217">The **Analytics** section has the following four tabs:</span></span>

* <span data-ttu-id="1ee6e-218"> 提供整體的使用量和健康情況度量，以及名列前茅的開發人員、產品、API 和作業等相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-218">**At a glance** provides overall usage and health metrics, as well as the top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="1ee6e-219"> 提供 API 呼叫和頻寬的深入檢視，包括地理區域的呈現。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-219">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="1ee6e-220">**Health** 著重在狀態碼、快取成功率、回應時間，以及 API 與服務回應時間。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-220">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="1ee6e-221">**Activity** 提供的報告依開發人員、產品、API 和作業向下鑽研特定活動。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-221">**Activity** provides reports that drill down on the specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="1ee6e-222"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ee6e-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="1ee6e-223">了解 [以頻率限制保護您的 API](api-management-howto-product-with-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="1ee6e-223">Learn how to [Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add the new API to a product]: #add-api-to-product
[Subscribe to the product that contains the API]: #subscribe
[Call an operation from the Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How to manage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How to configure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png

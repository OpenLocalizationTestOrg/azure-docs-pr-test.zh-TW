---
title: "aaaManage 您在 Azure API 管理中的第一個 API |Microsoft 文件"
description: "了解如何 toocreate 應用程式開發介面，加入作業，並開始使用 API 管理。"
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
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="33930-103">在 Azure API 管理中管理您的第一個 API</span><span class="sxs-lookup"><span data-stu-id="33930-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="33930-104"><a name="overview"> </a>概觀</span><span class="sxs-lookup"><span data-stu-id="33930-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="33930-105">本指南也說明如何開始使用 Azure API 管理中的 tooquickly，並進行第一次的 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="33930-105">This guide shows you how tooquickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="33930-106"><a name="concepts"> </a>什麼是 Azure API 管理？</span><span class="sxs-lookup"><span data-stu-id="33930-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="33930-107">您可以使用 Azure API 管理 tootake 任何後端，並啟動它為基礎的完整功能 API 程式。</span><span class="sxs-lookup"><span data-stu-id="33930-107">You can use Azure API Management tootake any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="33930-108">常見案例包括：</span><span class="sxs-lookup"><span data-stu-id="33930-108">Common scenarios include:</span></span>

* <span data-ttu-id="33930-109">**保護行動基礎結構** 。</span><span class="sxs-lookup"><span data-stu-id="33930-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="33930-110">**啟用 ISV 合作夥伴生態系統**藉由提供快速的夥伴上架 hello 開發人員透過入口網站和建立從內部實作應用程式開發介面外觀 toodecouple 不敞開夥伴耗用量。</span><span class="sxs-lookup"><span data-stu-id="33930-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through hello developer portal and building an API facade toodecouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="33930-111">**執行內部的 API 程式**藉由提供集中式的位置，如 hello 組織 toocommunicate hello 可用性和最新相關變更 tooAPIs，控制組織的帳戶為基礎的存取為基礎之間的安全通道hello API 閘道和 hello 後端。</span><span class="sxs-lookup"><span data-stu-id="33930-111">**Running an internal API program** by offering a centralized location for hello organization toocommunicate about hello availability and latest changes tooAPIs, gating access based on organizational accounts, all based on a secured channel between hello API gateway and hello backend.</span></span>

<span data-ttu-id="33930-112">hello 系統是由下列元件的 hello 所組成：</span><span class="sxs-lookup"><span data-stu-id="33930-112">hello system is made up of hello following components:</span></span>

* <span data-ttu-id="33930-113">hello **API 閘道**hello 端點的：</span><span class="sxs-lookup"><span data-stu-id="33930-113">hello **API gateway** is hello endpoint that:</span></span>
  
  * <span data-ttu-id="33930-114">接受應用程式開發介面呼叫，並將其傳送 tooyour 後端。</span><span class="sxs-lookup"><span data-stu-id="33930-114">Accepts API calls and routes them tooyour backends.</span></span>
  * <span data-ttu-id="33930-115">驗證 API 金鑰、JWT 權杖、憑證和其他認證。</span><span class="sxs-lookup"><span data-stu-id="33930-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="33930-116">強制採用使用量配額和頻率限制。</span><span class="sxs-lookup"><span data-stu-id="33930-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="33930-117">會將您的 API，而不需修改程式碼的 hello 立即轉換。</span><span class="sxs-lookup"><span data-stu-id="33930-117">Transforms your API on hello fly without code modifications.</span></span>
  * <span data-ttu-id="33930-118">快取設定的後端回應。</span><span class="sxs-lookup"><span data-stu-id="33930-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="33930-119">記錄呼叫中繼資料以供分析使用。</span><span class="sxs-lookup"><span data-stu-id="33930-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="33930-120">hello**發行者入口網站**hello 系統管理介面設定您應用程式開發介面的程式。</span><span class="sxs-lookup"><span data-stu-id="33930-120">hello **publisher portal** is hello administrative interface where you set up your API program.</span></span> <span data-ttu-id="33930-121">使用方式：</span><span class="sxs-lookup"><span data-stu-id="33930-121">Use it to:</span></span>
  
  * <span data-ttu-id="33930-122">定義或匯入 API 結構描述。</span><span class="sxs-lookup"><span data-stu-id="33930-122">Define or import API schema.</span></span>
  * <span data-ttu-id="33930-123">將 API 封裝至產品。</span><span class="sxs-lookup"><span data-stu-id="33930-123">Package APIs into products.</span></span>
  * <span data-ttu-id="33930-124">設定原則，例如配額或 hello 應用程式開發介面上的轉換。</span><span class="sxs-lookup"><span data-stu-id="33930-124">Set up policies like quotas or transformations on hello APIs.</span></span>
  * <span data-ttu-id="33930-125">從分析中取得見解。</span><span class="sxs-lookup"><span data-stu-id="33930-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="33930-126">管理使用者。</span><span class="sxs-lookup"><span data-stu-id="33930-126">Manage users.</span></span>
* <span data-ttu-id="33930-127">hello**開發人員入口網站**做 hello 主要 web 存在為開發人員而言，它們可以在其中：</span><span class="sxs-lookup"><span data-stu-id="33930-127">hello **developer portal** serves as hello main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="33930-128">閱讀 API 文件。</span><span class="sxs-lookup"><span data-stu-id="33930-128">Read API documentation.</span></span>
  * <span data-ttu-id="33930-129">嘗試透過 hello 互動式主控台應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="33930-129">Try out an API via hello interactive console.</span></span>
  * <span data-ttu-id="33930-130">建立帳戶和訂閱 tooget API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="33930-130">Create an account and subscribe tooget API keys.</span></span>
  * <span data-ttu-id="33930-131">存取他們的使用量分析資料。</span><span class="sxs-lookup"><span data-stu-id="33930-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="33930-132"><a name="create-service-instance"> </a>建立 API 管理執行個體</span><span class="sxs-lookup"><span data-stu-id="33930-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="33930-133">toocomplete 本教學課程中，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="33930-133">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="33930-134">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="33930-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="33930-135">如需詳細資訊，請參閱 [Azure 免費試用][Azure Free Trial]。</span><span class="sxs-lookup"><span data-stu-id="33930-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="33930-136">使用 API 管理中的 hello 第一個步驟是 toocreate 服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="33930-136">hello first step in working with API Management is toocreate a service instance.</span></span> <span data-ttu-id="33930-137">登入 toohello [Azure 入口網站][ Azure Portal]按一下**新增**， **Web + 行動**， **API 管理**。</span><span class="sxs-lookup"><span data-stu-id="33930-137">Sign in toohello [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![API Management new instance][api-management-create-instance-menu]

<span data-ttu-id="33930-139">如**名稱**，指定唯一的子網域名稱 toouse hello 服務 url。</span><span class="sxs-lookup"><span data-stu-id="33930-139">For **Name**, specify a unique sub-domain name toouse for hello service URL.</span></span>

<span data-ttu-id="33930-140">選擇所需的 hello**訂用帳戶**，**資源群組**和**位置**服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="33930-140">Choose hello desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="33930-141">輸入**Contoso Ltd.** hello**組織名稱**，並輸入您的電子郵件地址中 hello**系統管理員電子郵件**欄位。</span><span class="sxs-lookup"><span data-stu-id="33930-141">Enter **Contoso Ltd.** for hello **Organization Name**, and enter your email address in hello **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="33930-142">此電子郵件地址用於從 hello API 管理系統的通知。</span><span class="sxs-lookup"><span data-stu-id="33930-142">This email address is used for notifications from hello API Management system.</span></span> <span data-ttu-id="33930-143">如需詳細資訊，請參閱[如何 tooconfigure 通知和電子郵件範本，在 Azure API 管理][How tooconfigure notifications and email templates in Azure API Management]。</span><span class="sxs-lookup"><span data-stu-id="33930-143">For more information, see [How tooconfigure notifications and email templates in Azure API Management][How tooconfigure notifications and email templates in Azure API Management].</span></span>
> 
> 

![New API Management service][api-management-create-instance-step1]

<span data-ttu-id="33930-145">API 管理服務執行個體共有三種層次：開發人員、標準和高階。</span><span class="sxs-lookup"><span data-stu-id="33930-145">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="33930-146">hello 開發人員層適用於開發、 測試及試驗 API 方案，高可用性不是問題。</span><span class="sxs-lookup"><span data-stu-id="33930-146">hello Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="33930-147">在 hello Standard 和 Premium 層，您可以調整您的保留的單元計數 toohandle 更多流量。</span><span class="sxs-lookup"><span data-stu-id="33930-147">In hello Standard and Premium tiers, you can scale your reserved unit count toohandle more traffic.</span></span> <span data-ttu-id="33930-148">hello Standard 和 Premium 層提供 API 管理服務以 hello 大部分處理能力和效能。</span><span class="sxs-lookup"><span data-stu-id="33930-148">hello Standard and Premium tiers provide your API Management service with hello most processing power and performance.</span></span> <span data-ttu-id="33930-149">您可以使用任何階層來完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="33930-149">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="33930-150">如需關於 API 管理層次的詳細資訊，請參閱 [API 管理價格][API Management pricing]。</span><span class="sxs-lookup"><span data-stu-id="33930-150">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="33930-151">按一下**建立**toostart 佈建您的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="33930-151">Click **Create** toostart provisioning your service instance.</span></span>

![New API Management service][api-management-instance-created]

<span data-ttu-id="33930-153">一旦建立 hello 服務執行個體，hello 下一個步驟是 toocreate，或匯入應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="33930-153">Once hello service instance is created, hello next step is toocreate or import an API.</span></span>

## <span data-ttu-id="33930-154"><a name="create-api"> </a>匯入 API</span><span class="sxs-lookup"><span data-stu-id="33930-154"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="33930-155">API 包含可自用戶端應用程式叫用的一組作業。</span><span class="sxs-lookup"><span data-stu-id="33930-155">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="33930-156">應用程式開發介面作業會代理 tooexisting web 服務。</span><span class="sxs-lookup"><span data-stu-id="33930-156">API operations are proxied tooexisting web services.</span></span>

<span data-ttu-id="33930-157">您可以手動建立 API (並可加入作業)，或是匯入這兩者。</span><span class="sxs-lookup"><span data-stu-id="33930-157">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="33930-158">在本教學課程中，我們將匯入範例計算機 web 服務由 Microsoft 提供，裝載於 Azure 的 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="33930-158">In this tutorial, we will import hello API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="33930-159">如需建立應用程式開發介面和手動加入作業的指示，請參閱[如何 toocreate Api](api-management-howto-create-apis.md)和[如何 tooadd 作業 tooan API](api-management-howto-add-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="33930-159">For guidance on creating an API and manually adding operations, see [How toocreate APIs](api-management-howto-create-apis.md) and [How tooadd operations tooan API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="33930-160">應用程式開發介面會在 hello 發行者入口網站設定。</span><span class="sxs-lookup"><span data-stu-id="33930-160">APIs are configured from hello publisher portal.</span></span> <span data-ttu-id="33930-161">tooreach，按一下 **發行者入口網站**從 hello 服務工具列。</span><span class="sxs-lookup"><span data-stu-id="33930-161">tooreach it, click **Publisher portal** from hello service toolbar.</span></span>

![發行者入口網站][api-management-management-console]

<span data-ttu-id="33930-163">tooimport hello 計算機 API 中，按一下**Api**從 hello **API 管理**hello 左、，然後按一下功能表**匯入 API**。</span><span class="sxs-lookup"><span data-stu-id="33930-163">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![匯入 API 按鈕][api-management-import-api]

<span data-ttu-id="33930-165">執行下列步驟 tooconfigure hello [小算盤] 應用程式開發介面的 hello:</span><span class="sxs-lookup"><span data-stu-id="33930-165">Perform hello following steps tooconfigure hello calculator API:</span></span>

1. <span data-ttu-id="33930-166">按一下**From URL**，輸入**http://calcapi.cloudapp.net/calcapi.json**到 hello**規格文件 URL**文字方塊，然後按一下 hello **Swagger**選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="33930-166">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into hello **Specification document URL** text box, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="33930-167">型別**calc**到 hello **Web API URL 尾碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="33930-167">Type **calc** into hello **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="33930-168">按一下 hello**產品 （選擇性）**方塊，然後選擇**入門**。</span><span class="sxs-lookup"><span data-stu-id="33930-168">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="33930-169">按一下**儲存**tooimport hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="33930-169">Click **Save** tooimport hello API.</span></span>

![Add new API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="33930-171">**API 管理**目前支援匯入 1.2 和 2.0 版本的 Swagger 文件。</span><span class="sxs-lookup"><span data-stu-id="33930-171">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="33930-172">即使 [Swagger 2.0 規格](http://swagger.io/specification)表示 `host`、`basePath` 和 `schemes` 是選擇性的屬性，請確定您的 Swagger 2.0 文件**必須**包含這些屬性，否則無法匯入。</span><span class="sxs-lookup"><span data-stu-id="33930-172">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="33930-173">一旦匯入 hello API 時，hello hello api 摘要頁面會顯示 hello 發行者入口網站中。</span><span class="sxs-lookup"><span data-stu-id="33930-173">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![API summary][api-management-imported-api-summary]

<span data-ttu-id="33930-175">hello 應用程式開發介面 > 一節中有數個索引標籤。</span><span class="sxs-lookup"><span data-stu-id="33930-175">hello API section has several tabs.</span></span> <span data-ttu-id="33930-176">hello**摘要**索引標籤會顯示有關 hello API 基本度量和資訊。</span><span class="sxs-lookup"><span data-stu-id="33930-176">hello **Summary** tab displays basic metrics and information about hello API.</span></span> <span data-ttu-id="33930-177">hello[設定](api-management-howto-create-apis.md#configure-api-settings) 索引標籤是應用程式開發介面的使用的 tooview 和編輯 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="33930-177">hello [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used tooview and edit hello configuration for an API.</span></span> <span data-ttu-id="33930-178">hello[作業](api-management-howto-add-operations.md) 索引標籤是使用的 toomanage hello API 的作業。</span><span class="sxs-lookup"><span data-stu-id="33930-178">hello [Operations](api-management-howto-add-operations.md) tab is used toomanage hello API's operations.</span></span> <span data-ttu-id="33930-179">hello**安全性** 索引標籤可以 hello 後端伺服器的使用的 tooconfigure 閘道驗證使用基本驗證或[相互憑證驗證](api-management-howto-mutual-certificates.md)，和 tooconfigure [使用 OAuth 2.0 的使用者授權](api-management-howto-oauth2.md)。</span><span class="sxs-lookup"><span data-stu-id="33930-179">hello **Security** tab can be used tooconfigure gateway authentication for hello backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and tooconfigure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="33930-180">hello**問題** 索引標籤是使用的 tooview hello 開發人員使用您 Api 所報告的問題。</span><span class="sxs-lookup"><span data-stu-id="33930-180">hello **Issues** tab is used tooview issues reported by hello developers who are using your APIs.</span></span> <span data-ttu-id="33930-181">hello**產品** 索引標籤會包含此應用程式開發介面使用的 tooconfigure hello 產品。</span><span class="sxs-lookup"><span data-stu-id="33930-181">hello **Products** tab is used tooconfigure hello products that contain this API.</span></span>

<span data-ttu-id="33930-182">依預設，每個 API 管理執行個體會隨附兩個範例產品：</span><span class="sxs-lookup"><span data-stu-id="33930-182">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="33930-183">**入門**</span><span class="sxs-lookup"><span data-stu-id="33930-183">**Starter**</span></span>
* <span data-ttu-id="33930-184">**無限制**</span><span class="sxs-lookup"><span data-stu-id="33930-184">**Unlimited**</span></span>

<span data-ttu-id="33930-185">在本教學課程中，當 hello 應用程式開發介面已匯入 hello 基本計算機 API 時，已加入 toohello Starter 產品。</span><span class="sxs-lookup"><span data-stu-id="33930-185">In this tutorial, hello Basic Calculator API was added toohello Starter product when hello API was imported.</span></span>

<span data-ttu-id="33930-186">在訂單 toomake 呼叫 tooan API 中，開發人員必須先訂閱，他們存取 tooit tooa 產品。</span><span class="sxs-lookup"><span data-stu-id="33930-186">In order toomake calls tooan API, developers must first subscribe tooa product that gives them access tooit.</span></span> <span data-ttu-id="33930-187">開發人員可以訂閱 tooproducts 在 hello 開發人員入口網站或系統管理員可以訂閱 hello 發行者入口網站中的開發人員 tooproducts。</span><span class="sxs-lookup"><span data-stu-id="33930-187">Developers can subscribe tooproducts in hello developer portal, or administrators can subscribe developers tooproducts in hello publisher portal.</span></span> <span data-ttu-id="33930-188">由於您已建立 hello API 管理執行個體 hello 中先前的步驟在 hello 教學課程中，讓您已訂閱的 tooevery 產品，根據預設，您是系統管理員。</span><span class="sxs-lookup"><span data-stu-id="33930-188">You are an administrator since you created hello API Management instance in hello previous steps in hello tutorial, so you are already subscribed tooevery product by default.</span></span>

## <span data-ttu-id="33930-189"><a name="call-operation"></a>從 hello 開發人員入口網站呼叫作業</span><span class="sxs-lookup"><span data-stu-id="33930-189"><a name="call-operation"> </a>Call an operation from hello developer portal</span></span>
<span data-ttu-id="33930-190">作業可以直接從 hello 開發人員入口網站，可提供便利的方式 tooview 呼叫，並測試應用程式開發介面的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="33930-190">Operations can be called directly from hello developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="33930-191">在此教學課程步驟中，您會呼叫 hello 基本計算機 API**加入兩個整數**作業。</span><span class="sxs-lookup"><span data-stu-id="33930-191">In this tutorial step, you will call hello Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="33930-192">按一下**開發人員入口網站**功能表在 hello hello hello 發行者入口網站的右上方。</span><span class="sxs-lookup"><span data-stu-id="33930-192">Click **Developer portal** from hello menu at hello top right of hello publisher portal.</span></span>

![開發人員入口網站][api-management-developer-portal-menu]

<span data-ttu-id="33930-194">按一下**Api**從 hello 最上層功能表，然後再按一下**基本計算機**toosee hello 可用的作業。</span><span class="sxs-lookup"><span data-stu-id="33930-194">Click **APIs** from hello top menu, and then click **Basic Calculator** toosee hello available operations.</span></span>

![開發人員入口網站][api-management-developer-portal-calc-api]

<span data-ttu-id="33930-196">請注意 hello 範例描述和匯入以及 hello 應用程式開發介面和作業，提供文件以 hello 開發人員會使用這項作業的參數。</span><span class="sxs-lookup"><span data-stu-id="33930-196">Note hello sample descriptions and parameters that were imported along with hello API and operations, providing documentation for hello developers that will use this operation.</span></span> <span data-ttu-id="33930-197">手動加入作業時，也可以加入這些說明。</span><span class="sxs-lookup"><span data-stu-id="33930-197">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="33930-198">toocall hello**加入兩個整數**作業中，按一下 **試試**。</span><span class="sxs-lookup"><span data-stu-id="33930-198">toocall hello **Add two integers** operation, click **Try it**.</span></span>

![試試看][api-management-developer-portal-calc-api-console]

<span data-ttu-id="33930-200">您可以輸入 hello 參數的某些值或保留 hello 的預設值，然後按一下**傳送**。</span><span class="sxs-lookup"><span data-stu-id="33930-200">You can enter some values for hello parameters or keep hello defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="33930-202">叫用作業之後，hello 開發人員入口網站會顯示 hello**回應狀態**，hello**回應標頭**，和任何**回應內容**。</span><span class="sxs-lookup"><span data-stu-id="33930-202">After an operation is invoked, hello developer portal displays hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![Response][api-management-invoke-get-response]

## <span data-ttu-id="33930-204"><a name="view-analytics"> </a>檢視分析</span><span class="sxs-lookup"><span data-stu-id="33930-204"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="33930-205">基本計算機，藉由選取的參數後 toohello 發行者入口網站的 tooview 分析**管理**功能表在 hello hello hello 開發人員入口網站的右上方。</span><span class="sxs-lookup"><span data-stu-id="33930-205">tooview analytics for Basic Calculator, switch back toohello publisher portal by selecting **Manage** from hello menu at hello top right of hello developer portal.</span></span>

![管理][api-management-manage-menu]

<span data-ttu-id="33930-207">hello hello 發行者入口網站的預設檢視為 hello**儀表板**，這樣會提供您的 API 管理執行個體的概觀。</span><span class="sxs-lookup"><span data-stu-id="33930-207">hello default view for hello publisher portal is hello **Dashboard**, which provides an overview of your API Management instance.</span></span>

![儀表板][api-management-dashboard]

<span data-ttu-id="33930-209">Hello 停留 hello 圖表**基本計算機**toosee hello 特定的衡量標準 hello hello 應用程式開發介面的指定的時段內使用。</span><span class="sxs-lookup"><span data-stu-id="33930-209">Hover hello mouse over hello chart for **Basic Calculator** toosee hello specific metrics for hello usage of hello API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="33930-210">如果您沒有看到任何線條在圖表上，切換後 toohello 開發人員入口網站和某些 hello API 呼叫、 稍待片刻，並再回來 toohello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="33930-210">If you don't see any lines on your chart, switch back toohello developer portal and make some calls into hello API, wait a few moments, and then come back toohello dashboard.</span></span>
> 
> 

<span data-ttu-id="33930-211">按一下**檢視詳細資料**hello 應用程式開發介面，包括放大顯示 hello 度量的 tooview hello 摘要頁面。</span><span class="sxs-lookup"><span data-stu-id="33930-211">Click **View Details** tooview hello summary page for hello API, including a larger version of hello displayed metrics.</span></span>

![Analytics][api-management-mouse-over]

![摘要][api-management-api-summary-metrics]

<span data-ttu-id="33930-214">對於詳細的計量和報表，按一下 **分析**從 hello **API 管理**hello 左邊功能表上的。</span><span class="sxs-lookup"><span data-stu-id="33930-214">For detailed metrics and reports, click **Analytics** from hello **API Management** menu on hello left.</span></span>

![概觀][api-management-analytics-overview]

<span data-ttu-id="33930-216">hello**分析**區段具有下列四個索引標籤的 hello:</span><span class="sxs-lookup"><span data-stu-id="33930-216">hello **Analytics** section has hello following four tabs:</span></span>

* <span data-ttu-id="33930-217">**一眼**提供整體使用量和健全狀況度量，以及 hello 最上層的開發人員、 最上層的產品、 最上層應用程式開發介面和最上層的作業。</span><span class="sxs-lookup"><span data-stu-id="33930-217">**At a glance** provides overall usage and health metrics, as well as hello top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="33930-218"> 提供 API 呼叫和頻寬的深入檢視，包括地理區域的呈現。</span><span class="sxs-lookup"><span data-stu-id="33930-218">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="33930-219">**Health** 著重在狀態碼、快取成功率、回應時間，以及 API 與服務回應時間。</span><span class="sxs-lookup"><span data-stu-id="33930-219">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="33930-220">**活動**提供 hello 的開發人員、 產品、 API 和作業的特定活動的向下鑽研報表。</span><span class="sxs-lookup"><span data-stu-id="33930-220">**Activity** provides reports that drill down on hello specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="33930-221"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="33930-221"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="33930-222">了解如何太[保護您的 API 與速率限制](api-management-howto-product-with-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="33930-222">Learn how too[Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
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

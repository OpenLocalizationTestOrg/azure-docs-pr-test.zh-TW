---
title: "如何在 Azure API 管理中建立 API"
description: "了解如何在 Azure API 管理中建立和設定 API。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ab08256fbc3caca05bf23a12016ad2acf4fc7412
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-apis-in-azure-api-management"></a><span data-ttu-id="5ae80-103">如何在 Azure API 管理中建立 API</span><span class="sxs-lookup"><span data-stu-id="5ae80-103">How to create APIs in Azure API Management</span></span>
<span data-ttu-id="5ae80-104">API 管理中的 API 代表可供用戶端應用程式叫用的一組作業。</span><span class="sxs-lookup"><span data-stu-id="5ae80-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="5ae80-105">新的 API 是在發行者入口網站中建立，然後新增所需的作業。</span><span class="sxs-lookup"><span data-stu-id="5ae80-105">New APIs are created in the publisher portal, and then the desired operations are added.</span></span> <span data-ttu-id="5ae80-106">加入操作之後，API 就可加入至產品，接著就可發佈。</span><span class="sxs-lookup"><span data-stu-id="5ae80-106">Once the operations are added, the API is added to a product and can be published.</span></span> <span data-ttu-id="5ae80-107">API 發佈之後，就可供開發人員訂閱和使用。</span><span class="sxs-lookup"><span data-stu-id="5ae80-107">Once an API is published, it can be subscribed to and used by developers.</span></span>

<span data-ttu-id="5ae80-108">本指南示範過程中的第一個步驟：如何在 API 管理中建立和設定新 API。</span><span class="sxs-lookup"><span data-stu-id="5ae80-108">This guide shows the first step in the process: how to create and configure a new API in API Management.</span></span> <span data-ttu-id="5ae80-109">如需有關新增作業和發佈產品的詳細資訊，請參閱[如何將作業新增至 API][How to add operations to an API] 和[如何建立和發佈產品][How to create and publish a product]。</span><span class="sxs-lookup"><span data-stu-id="5ae80-109">For more information on adding operations and publishing a product, see [How to add operations to an API][How to add operations to an API] and [How to create and publish a product][How to create and publish a product].</span></span>

## <span data-ttu-id="5ae80-110"><a name="create-new-api"> </a>建立新的 API</span><span class="sxs-lookup"><span data-stu-id="5ae80-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="5ae80-111">API 是在發行者入口網站中建立和設定。</span><span class="sxs-lookup"><span data-stu-id="5ae80-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="5ae80-112">若要存取發行者入口網站，請在您「API 管理」服務的「Azure 入口網站」中按一下 [發行者入口網站]。</span><span class="sxs-lookup"><span data-stu-id="5ae80-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![發行者入口網站][api-management-management-console]

> <span data-ttu-id="5ae80-114">如果您尚未建立 API 管理服務執行個體，請參閱[開始使用 Azure API 管理][Get started with Azure API Management]教學課程中的[建立 API 管理服務執行個體][Create an API Management service instance]。</span><span class="sxs-lookup"><span data-stu-id="5ae80-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="5ae80-115">從左側 [API 管理] 功能表按一下 [API]，然後按一下 [新增 API]。</span><span class="sxs-lookup"><span data-stu-id="5ae80-115">Click **APIs** from the **API Management** menu on the left, and then click **add API**.</span></span>

![Create API][api-management-create-api]

<span data-ttu-id="5ae80-117">使用 [Add new API]  視窗來設定新的 API。</span><span class="sxs-lookup"><span data-stu-id="5ae80-117">Use the **Add new API** window to configure the new API.</span></span>

![Add new API][api-management-add-new-api]

<span data-ttu-id="5ae80-119">以下欄位可用來設定新 API。</span><span class="sxs-lookup"><span data-stu-id="5ae80-119">The following fields are used to configure the new API.</span></span>

* <span data-ttu-id="5ae80-120"> 提供 API 的獨特描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="5ae80-120">**Web API name** provides a unique and descriptive name for the API.</span></span> <span data-ttu-id="5ae80-121">它會顯示在開發人員和發行者入口網站中。</span><span class="sxs-lookup"><span data-stu-id="5ae80-121">It is displayed in the developer and publisher portals.</span></span>
* <span data-ttu-id="5ae80-122"> 會參考實作 API 的 HTTP 服務。</span><span class="sxs-lookup"><span data-stu-id="5ae80-122">**Web service URL** references the HTTP service implementing the API.</span></span> <span data-ttu-id="5ae80-123">API 管理則將要求轉送至此位址。</span><span class="sxs-lookup"><span data-stu-id="5ae80-123">API management forwards requests to this address.</span></span>
* <span data-ttu-id="5ae80-124"> 會附加到 API 管理服務的基礎 URL。</span><span class="sxs-lookup"><span data-stu-id="5ae80-124">**Web API URL suffix** is appended to the base URL for the API management service.</span></span> <span data-ttu-id="5ae80-125">基礎 URL 是 API 管理服務主控的所有 API 所共有。</span><span class="sxs-lookup"><span data-stu-id="5ae80-125">The base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="5ae80-126">API 管理依尾碼來區分 API，因此，特定發行者的每一個 API 必須有唯一的尾碼。</span><span class="sxs-lookup"><span data-stu-id="5ae80-126">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="5ae80-127">**Web API URL 配置**  決定可使用哪些通訊協定來存取 API。</span><span class="sxs-lookup"><span data-stu-id="5ae80-127">**Web API URL scheme** determines which protocols can be used to access the API.</span></span> <span data-ttu-id="5ae80-128">預設會指定 HTTPs。</span><span class="sxs-lookup"><span data-stu-id="5ae80-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="5ae80-129">若要選擇性地將此新 API 加入產品，請按一下 [產品 (選擇性)]  下拉式清單，並選擇產品。</span><span class="sxs-lookup"><span data-stu-id="5ae80-129">To optionally add this new API to a product, click the **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="5ae80-130">可以重複此步驟多次來將 API 加入多個產品。</span><span class="sxs-lookup"><span data-stu-id="5ae80-130">This step can be repeated multiple times to add the API to multiple products.</span></span>

<span data-ttu-id="5ae80-131">設定需要的值之後，請按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5ae80-131">Once the desired values are configured, click **Save**.</span></span> <span data-ttu-id="5ae80-132">建立新 API 之後，API 的摘要頁面隨即會顯示在發行者入口網站中。</span><span class="sxs-lookup"><span data-stu-id="5ae80-132">Once the new API is created, the summary page for the API is displayed in the publisher portal.</span></span>

![API summary][api-management-api-summary]

## <span data-ttu-id="5ae80-134"><a name="configure-api-settings"> </a>設定 API 設定</span><span class="sxs-lookup"><span data-stu-id="5ae80-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="5ae80-135">您可以使用 [設定] 索引標籤來驗證和編輯 API 的組態。</span><span class="sxs-lookup"><span data-stu-id="5ae80-135">You can use the **Settings** tab to verify and edit the configuration for an API.</span></span> <span data-ttu-id="5ae80-136">[Web API 名稱]、[Web 服務 URL] 和 [Web API URL 尾碼] 最初是在建立 API 時設定，可在這裡修改。</span><span class="sxs-lookup"><span data-stu-id="5ae80-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when the API is created and can be modified here.</span></span> <span data-ttu-id="5ae80-137">[說明] 提供選擇性說明，而 [Web API URL 配置] 決定可使用哪些通訊協定來存取 API。</span><span class="sxs-lookup"><span data-stu-id="5ae80-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used to access the API.</span></span>

![API settings][api-management-api-settings]

<span data-ttu-id="5ae80-139">若要針對實作 API 的後端服務設定 [閘道驗證]，請選取 [安全性]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5ae80-139">To configure gateway authentication for the backend service implementing the API, select the **Security** tab.</span></span> <span data-ttu-id="5ae80-140">[使用認證] 下拉式清單可用來設定 [HTTP 基本] 或 [用戶端憑證] 驗證。</span><span class="sxs-lookup"><span data-stu-id="5ae80-140">The **With credentials** drop-down can be used to configure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="5ae80-141">若要使用 HTTP Basic 驗證，只需要輸入所需的認證。</span><span class="sxs-lookup"><span data-stu-id="5ae80-141">To use HTTP basic authentication, simply enter the desired credentials.</span></span> <span data-ttu-id="5ae80-142">如需使用用戶端憑證驗證的詳細資訊，請參閱 [如何在 Azure API 管理中使用用戶端憑證驗證來保護後端服務][How to secure back-end services using client certificate authentication in Azure API Management]。</span><span class="sxs-lookup"><span data-stu-id="5ae80-142">For information on using client certificate authentication, see [How to secure back-end services using client certificate authentication in Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="5ae80-143">[安全性] 索引標籤也可用來使用 OAuth 2.0 設定 [使用者授權]。</span><span class="sxs-lookup"><span data-stu-id="5ae80-143">The **Security** tab can also be used to configure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="5ae80-144">如需詳細資訊，請參閱 [如何在 Azure API 管理中使用 OAuth 2.0 授權開發人員帳戶][How to authorize developer accounts using OAuth 2.0 in Azure API Management]。</span><span class="sxs-lookup"><span data-stu-id="5ae80-144">For more information, see [How to authorize developer accounts using OAuth 2.0 in Azure API Management][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Basic authentication settings][api-management-api-settings-credentials]

<span data-ttu-id="5ae80-146">按一下 [儲存]  ，儲存您對 API 設定所做的任何變更。</span><span class="sxs-lookup"><span data-stu-id="5ae80-146">Click **Save** to save any changes you make to the API settings.</span></span>

## <span data-ttu-id="5ae80-147"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ae80-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="5ae80-148">建立 API 並完成設定之後，接下來是將操作加入至 API、將 API 加入至產品，以及發佈它供開發人員使用。</span><span class="sxs-lookup"><span data-stu-id="5ae80-148">Once an API is created and the settings configured, the next steps are to add the operations to the API, add the API to a product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="5ae80-149">如需詳細資訊，請參閱下列文章。</span><span class="sxs-lookup"><span data-stu-id="5ae80-149">For more information, see the following articles.</span></span>

* <span data-ttu-id="5ae80-150">[如何將作業加入至 API][How to add operations to an API]</span><span class="sxs-lookup"><span data-stu-id="5ae80-150">[How to add operations to an API][How to add operations to an API]</span></span>
* <span data-ttu-id="5ae80-151">[如何建立和發佈產品][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="5ae80-151">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How to secure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How to authorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md

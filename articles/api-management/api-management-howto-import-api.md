---
title: "將 API 匯入至 Azure API 管理 | Microsoft Docs"
description: "了解如何將 API 及其操作匯入至 Azure API 管理。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c851b88fc1067e65044266d07775717c028e75d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-the-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="f4cf9-103">如何在 Azure API 管理中連同操作一起匯入 API 的定義</span><span class="sxs-lookup"><span data-stu-id="f4cf9-103">How to import the definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="f4cf9-104">在 API 管理中，可手動建立新的 API 並新增作業，或在一個步驟中連同作業一起匯入 API。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-104">In API Management, new APIs can be created and the operations added manually, or the API can be imported along with the operations in one step.</span></span>

<span data-ttu-id="f4cf9-105">您可以使用下列格式來匯入 API 及其操作。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-105">APIs and their operations can be imported using the following formats.</span></span>

* <span data-ttu-id="f4cf9-106">WADL</span><span class="sxs-lookup"><span data-stu-id="f4cf9-106">WADL</span></span>
* <span data-ttu-id="f4cf9-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="f4cf9-107">Swagger</span></span>

<span data-ttu-id="f4cf9-108">本指南示範如何在一個步驟中建立新的 API 並匯入其操作。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="f4cf9-109">如需有關手動建立 API 和新增作業的資訊，請參閱[如何建立 API][How to create APIs] 和[如何將作業新增至 API][How to add operations to an API]。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-109">For information on manually creating an API and adding operations, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span></span>

## <span data-ttu-id="f4cf9-110"><a name="import-api"> </a>匯入 API</span><span class="sxs-lookup"><span data-stu-id="f4cf9-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="f4cf9-111">API 是在發行者入口網站中建立和設定。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="f4cf9-112">若要存取發行者入口網站，請在您「API 管理」服務的「Azure 入口網站」中按一下 [發行者入口網站]。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="f4cf9-113">如果您尚未建立 API 管理服務執行個體，請參閱[開始使用 Azure API 管理][Get started with Azure API Management]教學課程中的[建立 API 管理服務執行個體][Create an API Management service instance]。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![發行者入口網站][api-management-management-console]

<span data-ttu-id="f4cf9-115">從左邊的 [API 管理] 功能表中按一下 [API]，然後按一下 [匯入 API]。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-115">Click **APIs** from the **API Management** menu on the left, and then click **import API**.</span></span>

![Import API][api-management-import-apis]

<span data-ttu-id="f4cf9-117">[匯入 API]  視窗有三個索引標籤，分別對應至三種提供 API 規格的方式。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-117">The **Import API** window has three tabs that correspond to the three ways to provide the API specification.</span></span>

* <span data-ttu-id="f4cf9-118"> 可讓您將 API 規格貼到指定的文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-118">**From clipboard** allows you to paste the API specification into the designated text box.</span></span>
* <span data-ttu-id="f4cf9-119"> 可讓您瀏覽並選取含有 API 規格的檔案。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-119">**From file** allows you to browse to and select the file that contains the API specification.</span></span>
* <span data-ttu-id="f4cf9-120"> 可讓您提供指向 API 規格的 URL。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-120">**From URL** allows you to supply the URL to the specification for the API.</span></span>

![Import API format][api-management-import-api-clipboard]

<span data-ttu-id="f4cf9-122">提供 API 規格之後，請使用右邊的選項按鈕來指出規格格式。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-122">After providing the API specification, use the radio buttons on the right to indicate the specification format.</span></span> <span data-ttu-id="f4cf9-123">支援下列格式。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-123">The following formats are supported.</span></span>

* <span data-ttu-id="f4cf9-124">WADL</span><span class="sxs-lookup"><span data-stu-id="f4cf9-124">WADL</span></span>
* <span data-ttu-id="f4cf9-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="f4cf9-125">Swagger</span></span>

<span data-ttu-id="f4cf9-126">接下來，輸入 [Web API URL 尾碼] 。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="f4cf9-127">這會附加至 API 管理服務的基礎 URL 後面。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-127">This is appended to the base URL for your API management service.</span></span> <span data-ttu-id="f4cf9-128">基礎 URL 是 API 管理服務的每一個執行個體上主控的所有 API 所共有。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-128">The base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="f4cf9-129">API 管理依尾碼來區分 API，因此，特定 API 管理服務執行個體中的每一個 API 必須有唯一的尾碼。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-129">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="f4cf9-130">輸入所有的值之後，按一下 [ **儲存** ]，以建立 API 和相關聯的操作。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-130">Once all values are entered, click **Save** to create the API and the associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="f4cf9-131">如需以 Swagger 格式匯入基本計算機 API 的教學課程，請參閱 [在 Azure API 管理中管理您的第一個 API](api-management-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="f4cf9-132"><a name="export-api"> </a> 匯出 API</span><span class="sxs-lookup"><span data-stu-id="f4cf9-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="f4cf9-133">除了匯入新的 API 之外，您還可以從發行者入口網站匯出 API 的定義。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-133">In addition to importing new APIs, you can export the definitions of your APIs from the publisher portal.</span></span> <span data-ttu-id="f4cf9-134">若要這樣做，請從 **API** 的 [摘要] 索引標籤中按一下 [匯出 API]。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-134">To do so, click **Export API** from the **Summary tab** of your **API**.</span></span>

![Export API][api-management-export-api]

<span data-ttu-id="f4cf9-136">您可以使用 WADL 或 Swagger 來匯出 API。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="f4cf9-137">選取所需的格式，按一下 [儲存] ，並選擇用來儲存檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-137">Select the desired format, click **Save**, and choose the location in which to save the file.</span></span>

![Export API format][api-management-export-api-format]

## <span data-ttu-id="f4cf9-139"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4cf9-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="f4cf9-140">建立 API 並匯入操作之後，您就可以檢閱和設定其他任何設定、將 API 加入至產品，以及發佈它供開發人員使用。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-140">Once an API is created and the operations imported, you can review and configure any additional settings, add the API to a Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="f4cf9-141">如需詳細資訊，請參閱下列指南。</span><span class="sxs-lookup"><span data-stu-id="f4cf9-141">For more information, see the following guides.</span></span>

* <span data-ttu-id="f4cf9-142">[如何設定 API 設定][How to configure API settings]</span><span class="sxs-lookup"><span data-stu-id="f4cf9-142">[How to configure API settings][How to configure API settings]</span></span>
* <span data-ttu-id="f4cf9-143">[如何建立和發佈產品][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="f4cf9-143">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create APIs]: api-management-howto-create-apis.md
[How to configure API settings]: api-management-howto-create-apis.md#configure-api-settings

---
title: "Azure API 管理的應用程式開發介面 aaaImport |Microsoft 文件"
description: "深入了解如何 tooimport API 和 Azure API 管理其作業。"
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
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="11e22-103">如何 tooimport hello Azure API 管理中的作業的應用程式開發介面的定義</span><span class="sxs-lookup"><span data-stu-id="11e22-103">How tooimport hello definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="11e22-104">在 API 管理中，可以建立新的 Api，並手動新增的 hello 作業或 hello API 可以匯入以及 hello 作業在一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="11e22-104">In API Management, new APIs can be created and hello operations added manually, or hello API can be imported along with hello operations in one step.</span></span>

<span data-ttu-id="11e22-105">應用程式開發介面和其作業可以使用匯入下列格式的 hello。</span><span class="sxs-lookup"><span data-stu-id="11e22-105">APIs and their operations can be imported using hello following formats.</span></span>

* <span data-ttu-id="11e22-106">WADL</span><span class="sxs-lookup"><span data-stu-id="11e22-106">WADL</span></span>
* <span data-ttu-id="11e22-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="11e22-107">Swagger</span></span>

<span data-ttu-id="11e22-108">本指南示範如何在一個步驟中建立新的 API 並匯入其操作。</span><span class="sxs-lookup"><span data-stu-id="11e22-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="11e22-109">如需手動建立應用程式開發介面，並將作業加入資訊，請參閱[如何 toocreate Api] [ How toocreate APIs]和[如何 tooadd 作業 tooan API] [ How tooadd operations tooan API].</span><span class="sxs-lookup"><span data-stu-id="11e22-109">For information on manually creating an API and adding operations, see [How toocreate APIs][How toocreate APIs] and [How tooadd operations tooan API][How tooadd operations tooan API].</span></span>

## <span data-ttu-id="11e22-110"><a name="import-api"> </a>匯入 API</span><span class="sxs-lookup"><span data-stu-id="11e22-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="11e22-111">建立並設定在 hello 發行者入口網站應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="11e22-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="11e22-112">tooaccess hello 發行者入口網站中，按一下**發行者入口網站**API 管理服務的 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="11e22-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="11e22-113">如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。</span><span class="sxs-lookup"><span data-stu-id="11e22-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![發行者入口網站][api-management-management-console]

<span data-ttu-id="11e22-115">按一下**Api**從 hello **API 管理**hello 左、，然後按一下功能表**匯入 API**。</span><span class="sxs-lookup"><span data-stu-id="11e22-115">Click **APIs** from hello **API Management** menu on hello left, and then click **import API**.</span></span>

![Import API][api-management-import-apis]

<span data-ttu-id="11e22-117">hello**匯入 API**視窗有對應 toohello 三種方式 tooprovide hello API 規格的三個索引標籤。</span><span class="sxs-lookup"><span data-stu-id="11e22-117">hello **Import API** window has three tabs that correspond toohello three ways tooprovide hello API specification.</span></span>

* <span data-ttu-id="11e22-118">**從剪貼簿**可讓您在 hello 指定的文字方塊的 toopaste hello API 規格。</span><span class="sxs-lookup"><span data-stu-id="11e22-118">**From clipboard** allows you toopaste hello API specification into hello designated text box.</span></span>
* <span data-ttu-id="11e22-119">**從檔案**可讓您包含 hello API 規格的 toobrowse tooand 選取 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="11e22-119">**From file** allows you toobrowse tooand select hello file that contains hello API specification.</span></span>
* <span data-ttu-id="11e22-120">**從 URL** toosupply hello URL toohello 規格 hello API 可讓您。</span><span class="sxs-lookup"><span data-stu-id="11e22-120">**From URL** allows you toosupply hello URL toohello specification for hello API.</span></span>

![Import API format][api-management-import-api-clipboard]

<span data-ttu-id="11e22-122">提供 hello API 規格之後, 使用 hello 圓鈕 hello 右 tooindicate hello 規格格式。</span><span class="sxs-lookup"><span data-stu-id="11e22-122">After providing hello API specification, use hello radio buttons on hello right tooindicate hello specification format.</span></span> <span data-ttu-id="11e22-123">支援下列格式的 hello。</span><span class="sxs-lookup"><span data-stu-id="11e22-123">hello following formats are supported.</span></span>

* <span data-ttu-id="11e22-124">WADL</span><span class="sxs-lookup"><span data-stu-id="11e22-124">WADL</span></span>
* <span data-ttu-id="11e22-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="11e22-125">Swagger</span></span>

<span data-ttu-id="11e22-126">接下來，輸入 [Web API URL 尾碼] 。</span><span class="sxs-lookup"><span data-stu-id="11e22-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="11e22-127">這是您的 API 管理服務的附加的 toohello 基底 URL。</span><span class="sxs-lookup"><span data-stu-id="11e22-127">This is appended toohello base URL for your API management service.</span></span> <span data-ttu-id="11e22-128">hello 基底 URL 是很常見的 API 管理服務的每個執行個體上裝載的所有 Api。</span><span class="sxs-lookup"><span data-stu-id="11e22-128">hello base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="11e22-129">API 管理它們的後置字元來區分應用程式開發介面，因此 hello 後置字元必須是唯一的特定 API 管理服務執行個體中的每一種 API。</span><span class="sxs-lookup"><span data-stu-id="11e22-129">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="11e22-130">輸入所有的值，當按一下**儲存**toocreate hello API 和 hello 相關聯的作業。</span><span class="sxs-lookup"><span data-stu-id="11e22-130">Once all values are entered, click **Save** toocreate hello API and hello associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="11e22-131">如需以 Swagger 格式匯入基本計算機 API 的教學課程，請參閱 [在 Azure API 管理中管理您的第一個 API](api-management-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="11e22-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="11e22-132"><a name="export-api"> </a> 匯出 API</span><span class="sxs-lookup"><span data-stu-id="11e22-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="11e22-133">加法 tooimporting 中新的 Api，您可以從 hello 發行者入口網站匯出您的應用程式開發介面的 hello 定義。</span><span class="sxs-lookup"><span data-stu-id="11e22-133">In addition tooimporting new APIs, you can export hello definitions of your APIs from hello publisher portal.</span></span> <span data-ttu-id="11e22-134">toodo，請按一下**匯出應用程式開發介面**從 hello**摘要 索引標籤**的您**API**。</span><span class="sxs-lookup"><span data-stu-id="11e22-134">toodo so, click **Export API** from hello **Summary tab** of your **API**.</span></span>

![Export API][api-management-export-api]

<span data-ttu-id="11e22-136">您可以使用 WADL 或 Swagger 來匯出 API。</span><span class="sxs-lookup"><span data-stu-id="11e22-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="11e22-137">選取 hello 所要的格式，請按一下**儲存**，並選擇哪些 toosave hello 檔案中的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="11e22-137">Select hello desired format, click **Save**, and choose hello location in which toosave hello file.</span></span>

![Export API format][api-management-export-api-format]

## <span data-ttu-id="11e22-139"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="11e22-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="11e22-140">一旦建立應用程式開發介面，並匯入的 hello 作業，您可以檢閱並設定任何其他設定，hello API tooa 產品，加上發佈，讓開發人員使用。</span><span class="sxs-lookup"><span data-stu-id="11e22-140">Once an API is created and hello operations imported, you can review and configure any additional settings, add hello API tooa Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="11e22-141">如需詳細資訊，請參閱下列指南中的 hello。</span><span class="sxs-lookup"><span data-stu-id="11e22-141">For more information, see hello following guides.</span></span>

* <span data-ttu-id="11e22-142">[如何設定 tooconfigure 應用程式開發介面][How tooconfigure API settings]</span><span class="sxs-lookup"><span data-stu-id="11e22-142">[How tooconfigure API settings][How tooconfigure API settings]</span></span>
* <span data-ttu-id="11e22-143">[如何 toocreate 及發佈產品][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="11e22-143">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings

---
title: "在 Azure API 管理 API 匯入的限制和已知問題 | Microsoft Docs"
description: "有關使用 Open API、WSDL 或 WADL 格式匯入 Azure API 管理的已知問題和限制的詳細資料。"
services: api-management
documentationcenter: 
author: mattfarm
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: ac799d66b5038c207413086b0fa71239ff2a332f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="2d587-103">API 匯入的限制和已知問題</span><span class="sxs-lookup"><span data-stu-id="2d587-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="2d587-104">關於本清單</span><span class="sxs-lookup"><span data-stu-id="2d587-104">About this list</span></span>
<span data-ttu-id="2d587-105">儘管我們盡力確保將 API 匯入 Azure API 管理的過程是順暢、沒問題的，偶爾還是要強制加上成功匯入之前需要加以改正的限制或身分識別問題。</span><span class="sxs-lookup"><span data-stu-id="2d587-105">While every effort is made to ensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need to be rectified before you can successfully import.</span></span> <span data-ttu-id="2d587-106">這篇文章說明這些項目，依 API 的匯入格式整理說明。</span><span class="sxs-lookup"><span data-stu-id="2d587-106">This article documents these, organised by the import format of the API.</span></span>

## <span data-ttu-id="2d587-107"><a name="open-api"> </a>Open API/Swagger</span><span class="sxs-lookup"><span data-stu-id="2d587-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="2d587-108">一般情況下，如果您匯入 Open API 文件時收到錯誤，請務必確認您的文件 - 可使用新 Azure 入口網站中的設計工具 ([設計] - [前端] - [Open API 規格編輯器])，或使用第 3 方工具 (例如 <a href="http://www.swagger.io">Swagger 編輯器</a>)。</span><span class="sxs-lookup"><span data-stu-id="2d587-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using the designer in the new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="2d587-109">**主機名稱** - 我們需要主機名稱屬性。</span><span class="sxs-lookup"><span data-stu-id="2d587-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="2d587-110">**基本路徑** - 我們需要基本路徑屬性。</span><span class="sxs-lookup"><span data-stu-id="2d587-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="2d587-111">**配置** - 我們需要配置陣列。</span><span class="sxs-lookup"><span data-stu-id="2d587-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="2d587-112"><a name="wsdl"> </a>WSDL</span><span class="sxs-lookup"><span data-stu-id="2d587-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="2d587-113">WSDL 檔案是用來產生 SOAP 傳遞的 API，或做為「SOAP 至 REST」API 的後端。</span><span class="sxs-lookup"><span data-stu-id="2d587-113">WSDL files are used to generate SOAP Pass-through APIs, or serve as the backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="2d587-114">**WSDL:Import** - 我們目前不支援使用這個屬性的 API。</span><span class="sxs-lookup"><span data-stu-id="2d587-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="2d587-115">客戶應該將匯入的項目合併成一份文件。</span><span class="sxs-lookup"><span data-stu-id="2d587-115">Customers should merge the imported elements into one document.</span></span>
* <span data-ttu-id="2d587-116">**具有多個部分的訊息** - 目前不支援。</span><span class="sxs-lookup"><span data-stu-id="2d587-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="2d587-117">**WCF wsHttpBinding** 使用 Windows Communication Foundation 建立的 SOAP 服務應該使用 basicHttpBinding - 不支援 wsHttpBinding。</span><span class="sxs-lookup"><span data-stu-id="2d587-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="2d587-118">**MTOM** - 使用 MTOM 的服務「可能」<em></em>可以運作。</span><span class="sxs-lookup"><span data-stu-id="2d587-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="2d587-119">目前不提供官方支援。</span><span class="sxs-lookup"><span data-stu-id="2d587-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="2d587-120">不支援以遞迴方式定義的**遞迴**類型 (例如，參考自己的陣列)。</span><span class="sxs-lookup"><span data-stu-id="2d587-120">**Recursion** types that are defined recursively (e.g. refer to an array of themselves) are not supported.</span></span>

## <span data-ttu-id="2d587-121"><a name="wadl"> </a>WADL</span><span class="sxs-lookup"><span data-stu-id="2d587-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="2d587-122">目前沒有任何已知的 WADL 匯入問題。</span><span class="sxs-lookup"><span data-stu-id="2d587-122">There are no known WADL import issues currently.</span></span>


[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md

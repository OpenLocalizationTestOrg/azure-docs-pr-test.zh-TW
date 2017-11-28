---
title: "匯入 aaaRestrictions 和 Azure API 管理 API 中的已知的問題 |Microsoft 文件"
description: "已知的問題與已匯入至 Azure API 管理使用 hello 開啟應用程式開發介面、 WSDL 或 WADL 格式的限制的詳細資料。"
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
ms.openlocfilehash: 0bed5ace47de6ccbfbecba25ea6b69c5329de089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="e9fc8-103">API 匯入的限制和已知問題</span><span class="sxs-lookup"><span data-stu-id="e9fc8-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="e9fc8-104">關於本清單</span><span class="sxs-lookup"><span data-stu-id="e9fc8-104">About this list</span></span>
<span data-ttu-id="e9fc8-105">雖然盡量 tooensure 所匯入 Azure API 管理您的應用程式開發介面的緊密性，且沒問題的越好，我們不要偶爾會強制限制或識別會需要 toobe 可以成功匯入之前修正的問題。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-105">While every effort is made tooensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need toobe rectified before you can successfully import.</span></span> <span data-ttu-id="e9fc8-106">本文記載這些 organised hello 匯入格式的 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-106">This article documents these, organised by hello import format of hello API.</span></span>

## <span data-ttu-id="e9fc8-107"><a name="open-api"> </a>Open API/Swagger</span><span class="sxs-lookup"><span data-stu-id="e9fc8-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="e9fc8-108">一般情況下，如果您收到錯誤匯入文件開啟的 API，請確認您已驗證-使用 hello 設計工具中的 hello 新版 Azure 入口網站 （設計-Front End-開啟應用程式開發介面規格編輯器），或第 3 與合作對象工具例如<a href="http://www.swagger.io">Swagger 編輯器</a>。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using hello designer in hello new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="e9fc8-109">**主機名稱** - 我們需要主機名稱屬性。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="e9fc8-110">**基本路徑** - 我們需要基本路徑屬性。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="e9fc8-111">**配置** - 我們需要配置陣列。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="e9fc8-112"><a name="wsdl"> </a>WSDL</span><span class="sxs-lookup"><span data-stu-id="e9fc8-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="e9fc8-113">WSDL 檔案使用的 toogenerate SOAP 傳遞 Api，或做為 hello SOAP-REST API 的後端。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-113">WSDL files are used toogenerate SOAP Pass-through APIs, or serve as hello backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="e9fc8-114">**WSDL:Import** - 我們目前不支援使用這個屬性的 API。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="e9fc8-115">客戶應該匯入的 hello 元素合併成一份文件中。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-115">Customers should merge hello imported elements into one document.</span></span>
* <span data-ttu-id="e9fc8-116">**具有多個部分的訊息** - 目前不支援。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="e9fc8-117">**WCF wsHttpBinding** 使用 Windows Communication Foundation 建立的 SOAP 服務應該使用 basicHttpBinding - 不支援 wsHttpBinding。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="e9fc8-118">**MTOM** - 使用 MTOM 的服務「可能」<em></em>可以運作。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="e9fc8-119">目前不提供官方支援。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="e9fc8-120">**遞迴**類型定義以遞迴方式 （例如，請參閱 tooan 陣列本身） 不支援。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-120">**Recursion** types that are defined recursively (e.g. refer tooan array of themselves) are not supported.</span></span>

## <span data-ttu-id="e9fc8-121"><a name="wadl"> </a>WADL</span><span class="sxs-lookup"><span data-stu-id="e9fc8-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="e9fc8-122">目前沒有任何已知的 WADL 匯入問題。</span><span class="sxs-lookup"><span data-stu-id="e9fc8-122">There are no known WADL import issues currently.</span></span>


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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md

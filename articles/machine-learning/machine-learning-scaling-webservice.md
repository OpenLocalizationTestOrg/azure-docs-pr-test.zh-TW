---
title: "如何提高 Azure Machine Learning Web 服務的並行 | Microsoft Docs"
description: "了解如何藉由新增其他端點來提高 Azure Machine Learning Web 服務的並行。"
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "azure 機器學習服務, web 服務, 作業化, 調整, 端點, 並行要求"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: 013354515d841003c912ac0338690dd975a79ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="26bad-104">藉由新增其他端點來調整 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="26bad-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="26bad-105">此主題描述適用於**傳統** Machine Learning Web 服務的技巧。</span><span class="sxs-lookup"><span data-stu-id="26bad-105">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="26bad-106">根據預設，系統將每個發佈的 Web 服務設定為支援 20 個並行要求，而且最多可達 200 個並行要求。</span><span class="sxs-lookup"><span data-stu-id="26bad-106">By default, each published Web service is configured to support 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="26bad-107">雖然 Azure 傳統入口網站提供設定此值的方法，但是 Azure Machine Learning 會自動最佳化此設定，為您的 Web 服務提供最佳的效能，並忽略入口網站的值。</span><span class="sxs-lookup"><span data-stu-id="26bad-107">While the Azure classic portal provides a way to set this value, Azure Machine Learning automatically optimizes the setting to provide the best performance for your web service and the portal value is ignored.</span></span> 

<span data-ttu-id="26bad-108">如果您打算以超過「並行呼叫數上限」值 200 可支援的負載來呼叫 API，則應該在相同的 Web 服務上建立多個端點。</span><span class="sxs-lookup"><span data-stu-id="26bad-108">If you plan to call the API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on the same Web service.</span></span> <span data-ttu-id="26bad-109">然後，您就可以將負載隨機分配給所有端點。</span><span class="sxs-lookup"><span data-stu-id="26bad-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="26bad-110">調整 Web 服務一件常見的工作。</span><span class="sxs-lookup"><span data-stu-id="26bad-110">The scaling of a Web service is a common task.</span></span> <span data-ttu-id="26bad-111">一些調整理由包括為了支援超過 200 個並行要求、透過多個端點提高可用性，或為 Web 服務提供個別的端點。</span><span class="sxs-lookup"><span data-stu-id="26bad-111">Some reasons to scale are to support more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for the web service.</span></span> <span data-ttu-id="26bad-112">您可以透過 [Azure 傳統入口網站](https://manage.windowsazure.com/)[Machine Learning Web 服務](https://services.azureml.net/)新增更多端點來為同一個 Web 服務擴大規模。</span><span class="sxs-lookup"><span data-stu-id="26bad-112">You can increase the scale by adding additional endpoints for the same Web service through [Azure classic portal](https://manage.windowsazure.com/) or the [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="26bad-113">如需有關新增端點的詳細資訊，請參閱[建立端點](machine-learning-create-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="26bad-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="26bad-114">請記住，如果您未以對應的高比例來呼叫 API，則使用較大的並行處理計數可能有害。</span><span class="sxs-lookup"><span data-stu-id="26bad-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling the API with a correspondingly high rate.</span></span> <span data-ttu-id="26bad-115">如果您將相對低的負載放在為高負載設定的 API，可能會看見延遲有零星的逾時及 (或) 突增情況。</span><span class="sxs-lookup"><span data-stu-id="26bad-115">You might see sporadic timeouts and/or spikes in the latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="26bad-116">通常在需要低度延遲的情況下，才會使用同步 API。</span><span class="sxs-lookup"><span data-stu-id="26bad-116">The synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="26bad-117">這裡所說的延遲意味著 API 完成一個要求所花費的時間，而未計入任何網路延遲的時間。</span><span class="sxs-lookup"><span data-stu-id="26bad-117">Latency here implies the time it takes for the API to complete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="26bad-118">假設您有一個會延遲 50 毫秒的 API。</span><span class="sxs-lookup"><span data-stu-id="26bad-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="26bad-119">其節流層級為 [高] 且 [最大同時呼叫數目] 為 20，您必須每秒呼叫這個 API 20 * 1000 / 50 = 400 次，才能完全耗盡可用的容量。</span><span class="sxs-lookup"><span data-stu-id="26bad-119">To fully consume the available capacity with throttle level High and Max Concurrent Calls = 20, you need to call this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="26bad-120">再進一步延伸，假設會延遲 50 毫秒，則「並行呼叫數上限」200 可讓您每秒呼叫 API 4000 次。</span><span class="sxs-lookup"><span data-stu-id="26bad-120">Extending this further, a Max Concurrent Calls of 200 allows you to call the API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png

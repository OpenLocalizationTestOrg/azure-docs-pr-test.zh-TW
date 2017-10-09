---
title: "在 Azure Machine Learning web 服務的 aaaHow tooincrease 並行 |Microsoft 文件"
description: "了解 tooincrease 並行的 Azure Machine Learning web 服務藉由新增其他端點的方式。"
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
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="e56d9-104">藉由新增其他端點來調整 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="e56d9-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="e56d9-105">本主題說明的技巧適用 tooa**傳統**機器學習 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e56d9-105">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="e56d9-106">根據預設，每個已發行的 Web 服務是設定的 toosupport 20 的並行要求，而且可以高達 200 的並行要求。</span><span class="sxs-lookup"><span data-stu-id="e56d9-106">By default, each published Web service is configured toosupport 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="e56d9-107">雖然 hello Azure 傳統入口網站提供此值的方式 tooset，Azure Machine Learning 自動 hello 設定 tooprovide hello 最佳效能最佳化您的 web 服務和 hello 入口網站的值會被忽略。</span><span class="sxs-lookup"><span data-stu-id="e56d9-107">While hello Azure classic portal provides a way tooset this value, Azure Machine Learning automatically optimizes hello setting tooprovide hello best performance for your web service and hello portal value is ignored.</span></span> 

<span data-ttu-id="e56d9-108">如果您計劃與更高的負載超過 200 的同時呼叫數目上限值將會支援 toocall hello API，您應該建立多個端點上 hello 相同的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e56d9-108">If you plan toocall hello API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on hello same Web service.</span></span> <span data-ttu-id="e56d9-109">然後，您就可以將負載隨機分配給所有端點。</span><span class="sxs-lookup"><span data-stu-id="e56d9-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="e56d9-110">hello 調整的 Web 服務是常見的工作。</span><span class="sxs-lookup"><span data-stu-id="e56d9-110">hello scaling of a Web service is a common task.</span></span> <span data-ttu-id="e56d9-111">某些原因 tooscale toosupport 多個並行要求數目 200、 提高可用性，透過多個端點，或為 hello web 服務提供單獨的端點。</span><span class="sxs-lookup"><span data-stu-id="e56d9-111">Some reasons tooscale are toosupport more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for hello web service.</span></span> <span data-ttu-id="e56d9-112">您可以透過加入其他端點 hello 提高 hello 小數位數相同的 Web 服務，透過[Azure 傳統入口網站](https://manage.windowsazure.com/)或 hello [Azure Machine Learning Web 服務](https://services.azureml.net/)入口網站。</span><span class="sxs-lookup"><span data-stu-id="e56d9-112">You can increase hello scale by adding additional endpoints for hello same Web service through [Azure classic portal](https://manage.windowsazure.com/) or hello [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="e56d9-113">如需有關新增端點的詳細資訊，請參閱[建立端點](machine-learning-create-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="e56d9-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="e56d9-114">請記住，使用高並行計數可能會危害，如果您不呼叫 hello API 跟著率。</span><span class="sxs-lookup"><span data-stu-id="e56d9-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling hello API with a correspondingly high rate.</span></span> <span data-ttu-id="e56d9-115">您可能會看到偶發的逾時和/或尖峰 hello 延遲時間相對較低負載放在應用程式開發介面，設定為高負載。</span><span class="sxs-lookup"><span data-stu-id="e56d9-115">You might see sporadic timeouts and/or spikes in hello latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="e56d9-116">hello 通常會使用同步的應用程式開發介面在所需的低延遲的情況。</span><span class="sxs-lookup"><span data-stu-id="e56d9-116">hello synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="e56d9-117">這裡的延遲表示 hello 時間 hello API toocomplete 一個要求，並不會考量任何網路延遲。</span><span class="sxs-lookup"><span data-stu-id="e56d9-117">Latency here implies hello time it takes for hello API toocomplete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="e56d9-118">假設您有一個會延遲 50 毫秒的 API。</span><span class="sxs-lookup"><span data-stu-id="e56d9-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="e56d9-119">toofully 取用 hello 與節流層級高的可用容量，以及同時呼叫數目上限 = 20，20 * 1000 這個 API 需要 toocall / 每秒逾 50 = 400。</span><span class="sxs-lookup"><span data-stu-id="e56d9-119">toofully consume hello available capacity with throttle level High and Max Concurrent Calls = 20, you need toocall this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="e56d9-120">同時呼叫數目上限為 200 的進一步擴充，可讓您 toocall hello API 4000 時間每秒，假設 50 毫秒延遲。</span><span class="sxs-lookup"><span data-stu-id="e56d9-120">Extending this further, a Max Concurrent Calls of 200 allows you toocall hello API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png

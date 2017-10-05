---
title: "步驟 6：存取 Machine Learning Web 服務 | Microsoft Docs"
description: "開發預測解決方案的逐步解說步驟 6：存取使用中的 Azure Machine Learning Web 服務。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d309f6c4749a80c81859b693a2bd5927e8fe0e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-6-access-the-azure-machine-learning-web-service"></a><span data-ttu-id="208ec-103">逐步解說步驟 6：存取 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="208ec-103">Walkthrough Step 6: Access the Azure Machine Learning web service</span></span>

<span data-ttu-id="208ec-104">這是 [在 Azure Machine Learning 中為信用風險評估開發預測性分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="208ec-104">This is the last step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="208ec-105">建立機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="208ec-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="208ec-106">上傳現有資料</span><span class="sxs-lookup"><span data-stu-id="208ec-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="208ec-107">建立新實驗</span><span class="sxs-lookup"><span data-stu-id="208ec-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="208ec-108">訓練及評估模型</span><span class="sxs-lookup"><span data-stu-id="208ec-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="208ec-109">部署 Web 服務</span><span class="sxs-lookup"><span data-stu-id="208ec-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="208ec-110">**存取 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="208ec-110">**Access the Web service**</span></span>

- - -
<span data-ttu-id="208ec-111">在此逐步解說先前的步驟中，我們已經部署一個使用我們的信用風險預測模型的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="208ec-111">In the previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="208ec-112">現在使用者能夠將資料傳送至服務並接收結果。</span><span class="sxs-lookup"><span data-stu-id="208ec-112">Now users are able to send data to it and receive results.</span></span> 

<span data-ttu-id="208ec-113">此 Web 服務是可使用 REST API，透過下列其中一種方式接收和傳回資料的 Azure Web 服務：</span><span class="sxs-lookup"><span data-stu-id="208ec-113">The Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="208ec-114">**要求/回應** - 使用者以 HTTP 通訊協定，將一或多列的信用資料傳送給服務，然後服務回應一或多組結果。</span><span class="sxs-lookup"><span data-stu-id="208ec-114">**Request/Response** - The user sends one or more rows of credit data to the service by using an HTTP protocol, and the service responds with one or more sets of results.</span></span>
* <span data-ttu-id="208ec-115">**批次執行** - 使用者在 Azure Blob 中儲存一或多列信用資料，然後將 Blob 位置傳送給服務。</span><span class="sxs-lookup"><span data-stu-id="208ec-115">**Batch Execution** - The user stores one or more rows of credit data in an Azure blob and then sends the blob location to the service.</span></span> <span data-ttu-id="208ec-116">服務會給輸入 Blob 中的所有資料列評分，將結果儲存在另一個 Blob 中，再傳回該容器的 URL。</span><span class="sxs-lookup"><span data-stu-id="208ec-116">The service scores all the rows of data in the input blob, stores the results in another blob, and returns the URL of that container.</span></span>  

<span data-ttu-id="208ec-117">存取傳統 Web 服務最簡單快速的方式，是透過 [Azure ML 要求-回應服務 Web 應用程式 (英文)](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) 或 [Azure ML 批次執行服務 Web 應用程式範本 (英文)](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)。</span><span class="sxs-lookup"><span data-stu-id="208ec-117">The quickest and easiest way to access a Classic web service is through the [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="208ec-118">這些 Web 應用程式範本可以建立自訂的 Web 應用程式，該應用程式知道您的 Web 服務輸入資料和將傳回的內容。</span><span class="sxs-lookup"><span data-stu-id="208ec-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="208ec-119">您所需要做的就是提供 Web 服務和資料的存取權限，範本會執行其餘部分。</span><span class="sxs-lookup"><span data-stu-id="208ec-119">All you need to do is provide access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="208ec-120">如需使用 Web 應用程式範本的詳細資訊，請參閱[使用 Azure Machine Learning Web 服務與 Web 應用程式範本](machine-learning-consume-web-service-with-web-app-template.md)。</span><span class="sxs-lookup"><span data-stu-id="208ec-120">For more information on using the web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="208ec-121">您也可以使用以 R、C# 和 Python 程式語言為您提供的起始程式碼來開發自訂應用程式以存取 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="208ec-121">You can also develop a custom application to access the web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="208ec-122">您可以在[如何使用 Azure Machine Learning Web 服務](machine-learning-consume-web-services.md)中找到完整詳細資料。</span><span class="sxs-lookup"><span data-stu-id="208ec-122">You can find complete details in [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>


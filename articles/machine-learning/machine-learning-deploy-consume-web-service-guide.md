---
title: "Azure Machine Learning Web 服務：部署和取用 | Microsoft Docs"
description: "部署和使用 Web 服務的資源。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 18edabe267ec06c08074d7a7a6d71435cedc8489
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="e88c0-103">Azure Machine Learning Web 服務：部署和取用</span><span class="sxs-lookup"><span data-stu-id="e88c0-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="e88c0-104">您可以使用 Azure Machine Learning 來部署機器學習服務的工作流程和模型做為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e88c0-104">You can use Azure Machine Learning to deploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="e88c0-105">然後便可以透過網際網路利用這些 Web 服務從應用程式呼叫機器學習服務模型，進行即時預測或批次模式的預測。</span><span class="sxs-lookup"><span data-stu-id="e88c0-105">These web services can then be used to call the machine-learning models from applications over the Internet to do predictions in real time or in batch mode.</span></span> <span data-ttu-id="e88c0-106">由於 Web 服務為 RESTful，您可以從各種程式設計語言與平台 (如 .NET 與 Java) 和應用程式 (如 Excel) 呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="e88c0-106">Because the web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="e88c0-107">下列章節提供可協助您快速開始的逐步解說、程式碼及文件的連結。</span><span class="sxs-lookup"><span data-stu-id="e88c0-107">The next sections provide links to walkthroughs, code, and documentation to help get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="e88c0-108">部署 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e88c0-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="e88c0-109">使用 Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="e88c0-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="e88c0-110">Machine Learning Studio 和 Microsoft Azure Machine Learning Web 服務入口網站可協助您部署和管理 Web 服務，而不需要撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="e88c0-110">Machine Learning Studio and the Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="e88c0-111">下列連結提供有關如何部署新的 Web 服務的一般資訊︰</span><span class="sxs-lookup"><span data-stu-id="e88c0-111">The following links provide general Information about how to deploy a new web service:</span></span>

* <span data-ttu-id="e88c0-112">如需如何部署以 Azure Resource Manager 為基礎的新 Web 服務的概觀，請參閱 [部署新的 Web 服務](machine-learning-webservice-deploy-a-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="e88c0-112">For an overview about how to deploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="e88c0-113">如需如何部署 Web 服務的逐步解說，請參閱 [部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="e88c0-113">For a walkthrough about how to deploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="e88c0-114">如需如何建立和部署 Web 服務的完整逐步解說，請參閱 [逐步解說步驟 1︰建立 Machine Learning 工作區](machine-learning-walkthrough-1-create-ml-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="e88c0-114">For a full walkthrough about how to create and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="e88c0-115">如需部署 Web 服務的特定範例，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="e88c0-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="e88c0-116">逐步解說步驟 5：部署 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="e88c0-116">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="e88c0-117">如何將 Web 服務部署到多個區域</span><span class="sxs-lookup"><span data-stu-id="e88c0-117">How to deploy a web service to multiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="e88c0-118">使用 Web 服務資源提供者 API (Azure Resource Manager API)</span><span class="sxs-lookup"><span data-stu-id="e88c0-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="e88c0-119">用於 Web 服務的 Azure Machine Learning 資源提供者，可利用 REST API 呼叫來部署和管理 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e88c0-119">The Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="e88c0-120">如需詳細資訊，請參閱 [Machine Learning Web 服務 (REST)](/rest/api/machinelearning/index) 參考資料。</span><span class="sxs-lookup"><span data-stu-id="e88c0-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="e88c0-121">使用 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e88c0-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="e88c0-122">用於 Web 服務的 Azure Machine Learning 資源提供者，可利用 PowerShell Cmdlet 來部署和管理 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e88c0-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="e88c0-123">若要使用 Cmdlet，您必須先在 PowerShell 環境中，使用 [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) Cmdlet 登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e88c0-123">To use the cmdlets, you must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="e88c0-124">如果您不熟悉如何呼叫以 Resource Manager 為基礎的 PowerShell 命令，請參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account)。</span><span class="sxs-lookup"><span data-stu-id="e88c0-124">If you are unfamiliar with how to call PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="e88c0-125">若要匯出預測實驗，請使用這個 [範例程式碼](https://github.com/ritwik20/AzureML-WebServices)。</span><span class="sxs-lookup"><span data-stu-id="e88c0-125">To export your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="e88c0-126">由程式碼建立 .exe 檔案之後，您可以輸入︰</span><span class="sxs-lookup"><span data-stu-id="e88c0-126">After you create the .exe file from the code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="e88c0-127">執行應用程式會建立 Web 服務的 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="e88c0-127">Running the application creates a web service JSON template.</span></span> <span data-ttu-id="e88c0-128">若要使用此範本部署 Web 服務，必須新增下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="e88c0-128">To use the template to deploy a web service, you must add the following information:</span></span>

* <span data-ttu-id="e88c0-129">儲存體帳戶名稱和金鑰</span><span class="sxs-lookup"><span data-stu-id="e88c0-129">Storage account name and key</span></span>

    <span data-ttu-id="e88c0-130">您可以從 [Azure 入口網站](https://portal.azure.com/)或 [Azure 傳統入口網站](http://manage.windowsazure.com/)取得儲存體帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="e88c0-130">You can get the storage account name and key from either the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="e88c0-131">承諾用量方案識別碼</span><span class="sxs-lookup"><span data-stu-id="e88c0-131">Commitment plan ID</span></span>

    <span data-ttu-id="e88c0-132">您可以從 [Azure Machine Learning Web 服務](https://services.azureml.net) 入口網站登入，按一下方案名稱取得方案識別碼。</span><span class="sxs-lookup"><span data-stu-id="e88c0-132">You can get the plan ID from the [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="e88c0-133">將它們新增至 JSON 範本做為 *Properties* 節點的子系，與 *MachineLearningWorkspace* 節點位於相同層級。</span><span class="sxs-lookup"><span data-stu-id="e88c0-133">Add them to the JSON template as children of the *Properties* node at the same level as the *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="e88c0-134">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="e88c0-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="e88c0-135">如需更詳細的資訊，請參閱下列文章和範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="e88c0-135">See the following articles and sample code for additional details:</span></span>

* <span data-ttu-id="e88c0-136">[Azure Machine Learning Cmdlet](https://msdn.microsoft.com/library/azure/mt767952.aspx) 參考資料。</span><span class="sxs-lookup"><span data-stu-id="e88c0-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="e88c0-137">GitHub 上的範例 [逐步解說](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt)</span><span class="sxs-lookup"><span data-stu-id="e88c0-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-the-web-services"></a><span data-ttu-id="e88c0-138">取用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e88c0-138">Consume the web services</span></span>
### <a name="from-the-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="e88c0-139">從 Azure Machine Learning Web Services UI (測試)</span><span class="sxs-lookup"><span data-stu-id="e88c0-139">From the Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="e88c0-140">您可以從 Azure Machine Learning Web Services 入口網站測試您的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e88c0-140">You can test your web service from the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="e88c0-141">這包括測試要求-回應服務 (RRS) 和批次執行服務 (BES) 介面。</span><span class="sxs-lookup"><span data-stu-id="e88c0-141">This includes testing the Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="e88c0-142">部署新的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e88c0-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="e88c0-143">部署 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="e88c0-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="e88c0-144">逐步解說步驟 5：部署 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="e88c0-144">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="e88c0-145">從 Excel</span><span class="sxs-lookup"><span data-stu-id="e88c0-145">From Excel</span></span>
<span data-ttu-id="e88c0-146">您可以下載可取用 Web 服務的 Excel 範本︰</span><span class="sxs-lookup"><span data-stu-id="e88c0-146">You can download an Excel template that consumes the web service:</span></span>

* [<span data-ttu-id="e88c0-147">從 Excel 使用 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="e88c0-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="e88c0-148">適用於 Azure Machine Learning Web 服務的 Excel 增益集</span><span class="sxs-lookup"><span data-stu-id="e88c0-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="e88c0-149">從以 REST 為基礎的用戶端</span><span class="sxs-lookup"><span data-stu-id="e88c0-149">From a REST-based client</span></span>
<span data-ttu-id="e88c0-150">Azure Machine Learning Web 服務是 RESTful API。</span><span class="sxs-lookup"><span data-stu-id="e88c0-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="e88c0-151">您可以從 .NET、Python、R、Java 等各種平台使用這些 API。在 [Microsoft Azure Machine Learning Web 服務入口網站](https://services.azureml.net)上，您的 Web 服務的 [取用] 頁面有提供範例程式碼，可協助您開始使用。</span><span class="sxs-lookup"><span data-stu-id="e88c0-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. The **Consume** page for your web service on the [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="e88c0-152">如需詳細資訊，請參閱 [如何取用 Azure Machine Learning Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="e88c0-152">For more information, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

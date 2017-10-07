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
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="abefc-103">Azure Machine Learning Web 服務：部署和取用</span><span class="sxs-lookup"><span data-stu-id="abefc-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="abefc-104">您可以使用 Azure 機器學習 toodeploy 機器學習服務工作流程與模型做為 web 服務。</span><span class="sxs-lookup"><span data-stu-id="abefc-104">You can use Azure Machine Learning toodeploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="abefc-105">這些 web 服務接著可以使用的 toocall hello 機器學習模型，從應用程式透過 hello 網際網路 toodo 預測即時或批次模式。</span><span class="sxs-lookup"><span data-stu-id="abefc-105">These web services can then be used toocall hello machine-learning models from applications over hello Internet toodo predictions in real time or in batch mode.</span></span> <span data-ttu-id="abefc-106">因為 hello web 服務是 RESTful，您可以從各種程式設計語言與平台，例如.NET 和 Java，並從應用程式，例如 Excel 加以呼叫。</span><span class="sxs-lookup"><span data-stu-id="abefc-106">Because hello web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="abefc-107">hello 下一個區段提供連結 toowalkthroughs、 程式碼，以及文件 toohelp 協助您開始。</span><span class="sxs-lookup"><span data-stu-id="abefc-107">hello next sections provide links toowalkthroughs, code, and documentation toohelp get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="abefc-108">部署 Web 服務</span><span class="sxs-lookup"><span data-stu-id="abefc-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="abefc-109">使用 Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="abefc-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="abefc-110">Machine Learning Studio 和 hello Microsoft Azure 機器學習 Web 服務入口網站可協助您部署和管理 web 服務，而不需要撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="abefc-110">Machine Learning Studio and hello Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="abefc-111">hello 下列連結提供有關的一般資訊 toodeploy 新的 web 服務：</span><span class="sxs-lookup"><span data-stu-id="abefc-111">hello following links provide general Information about how toodeploy a new web service:</span></span>

* <span data-ttu-id="abefc-112">如需有關如何 toodeploy 新的 web 服務為基礎的 Azure 資源管理員中，請參閱概觀[部署新的 web 服務](machine-learning-webservice-deploy-a-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="abefc-112">For an overview about how toodeploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="abefc-113">如需逐步解說如何 toodeploy web 服務，請參閱[部署 Azure Machine Learning web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="abefc-113">For a walkthrough about how toodeploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="abefc-114">如需完整的逐步解說有關 toocreate 和部署 web 服務，請參閱[逐步解說步驟 1： 建立機器學習服務工作區](machine-learning-walkthrough-1-create-ml-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="abefc-114">For a full walkthrough about how toocreate and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="abefc-115">如需部署 Web 服務的特定範例，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="abefc-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="abefc-116">逐步解說步驟 5： 部署的 hello Azure Machine Learning web 服務</span><span class="sxs-lookup"><span data-stu-id="abefc-116">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="abefc-117">如何 toodeploy web 服務 toomultiple 區域</span><span class="sxs-lookup"><span data-stu-id="abefc-117">How toodeploy a web service toomultiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="abefc-118">使用 Web 服務資源提供者 API (Azure Resource Manager API)</span><span class="sxs-lookup"><span data-stu-id="abefc-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="abefc-119">web 服務的 hello Azure 機器學習資源提供者可讓部署及管理的 web 服務使用 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="abefc-119">hello Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="abefc-120">如需詳細資訊，請參閱 [Machine Learning Web 服務 (REST)](/rest/api/machinelearning/index) 參考資料。</span><span class="sxs-lookup"><span data-stu-id="abefc-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="abefc-121">使用 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="abefc-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="abefc-122">用於 Web 服務的 Azure Machine Learning 資源提供者，可利用 PowerShell Cmdlet 來部署和管理 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="abefc-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="abefc-123">toouse hello cmdlet，您必須先登入 tooyour 從 hello PowerShell 環境中的 Azure 帳戶使用 hello[新增 AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="abefc-123">toouse hello cmdlets, you must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="abefc-124">如果您不熟悉如何 toocall PowerShell 命令的採用資源管理員，請參閱[使用 Azure PowerShell 的 Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account)。</span><span class="sxs-lookup"><span data-stu-id="abefc-124">If you are unfamiliar with how toocall PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="abefc-125">tooexport 您預測進行實驗，請使用[此範例程式碼](https://github.com/ritwik20/AzureML-WebServices)。</span><span class="sxs-lookup"><span data-stu-id="abefc-125">tooexport your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="abefc-126">從 hello 程式碼建立 hello.exe 檔案之後，您可以輸入：</span><span class="sxs-lookup"><span data-stu-id="abefc-126">After you create hello .exe file from hello code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="abefc-127">執行 hello 應用程式建立 web 服務的 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="abefc-127">Running hello application creates a web service JSON template.</span></span> <span data-ttu-id="abefc-128">toouse hello 範本 toodeploy web 服務，您必須新增 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="abefc-128">toouse hello template toodeploy a web service, you must add hello following information:</span></span>

* <span data-ttu-id="abefc-129">儲存體帳戶名稱和金鑰</span><span class="sxs-lookup"><span data-stu-id="abefc-129">Storage account name and key</span></span>

    <span data-ttu-id="abefc-130">您可以從任一 hello 取得 hello 儲存體帳戶名稱和金鑰[Azure 入口網站](https://portal.azure.com/)或 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="abefc-130">You can get hello storage account name and key from either hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="abefc-131">承諾用量方案識別碼</span><span class="sxs-lookup"><span data-stu-id="abefc-131">Commitment plan ID</span></span>

    <span data-ttu-id="abefc-132">您可以從 hello 取得 hello 計劃 ID [Azure 機器學習 Web 服務](https://services.azureml.net)入口網站登入，然後按一下方案名稱。</span><span class="sxs-lookup"><span data-stu-id="abefc-132">You can get hello plan ID from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="abefc-133">將活動當做子系的 hello 加入 toohello JSON 範本*屬性*hello 節點相同層級為 hello *MachineLearningWorkspace*節點。</span><span class="sxs-lookup"><span data-stu-id="abefc-133">Add them toohello JSON template as children of hello *Properties* node at hello same level as hello *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="abefc-134">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="abefc-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="abefc-135">請參閱下列文章 hello 和範例程式碼的其他詳細資料：</span><span class="sxs-lookup"><span data-stu-id="abefc-135">See hello following articles and sample code for additional details:</span></span>

* <span data-ttu-id="abefc-136">[Azure Machine Learning Cmdlet](https://msdn.microsoft.com/library/azure/mt767952.aspx) 參考資料。</span><span class="sxs-lookup"><span data-stu-id="abefc-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="abefc-137">GitHub 上的範例 [逐步解說](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt)</span><span class="sxs-lookup"><span data-stu-id="abefc-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-hello-web-services"></a><span data-ttu-id="abefc-138">使用 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="abefc-138">Consume hello web services</span></span>
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="abefc-139">從 hello Azure 機器學習 Web 服務使用者介面 （測試）</span><span class="sxs-lookup"><span data-stu-id="abefc-139">From hello Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="abefc-140">您可以測試您的 web 服務從 hello Azure 機器學習 Web 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="abefc-140">You can test your web service from hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="abefc-141">這包括測試 hello 要求-回應服務 (RR)，批次執行服務 (BES) 介面。</span><span class="sxs-lookup"><span data-stu-id="abefc-141">This includes testing hello Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="abefc-142">部署新的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="abefc-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="abefc-143">部署 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="abefc-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="abefc-144">逐步解說步驟 5： 部署的 hello Azure Machine Learning web 服務</span><span class="sxs-lookup"><span data-stu-id="abefc-144">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="abefc-145">從 Excel</span><span class="sxs-lookup"><span data-stu-id="abefc-145">From Excel</span></span>
<span data-ttu-id="abefc-146">您可以下載使用 hello web 服務的 Excel 範本：</span><span class="sxs-lookup"><span data-stu-id="abefc-146">You can download an Excel template that consumes hello web service:</span></span>

* [<span data-ttu-id="abefc-147">從 Excel 使用 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="abefc-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="abefc-148">適用於 Azure Machine Learning Web 服務的 Excel 增益集</span><span class="sxs-lookup"><span data-stu-id="abefc-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="abefc-149">從以 REST 為基礎的用戶端</span><span class="sxs-lookup"><span data-stu-id="abefc-149">From a REST-based client</span></span>
<span data-ttu-id="abefc-150">Azure Machine Learning Web 服務是 RESTful API。</span><span class="sxs-lookup"><span data-stu-id="abefc-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="abefc-151">您可以使用這些 Api，從各種平台，例如.NET、 Python、 R、 Java、 等 hello**取用**頁面為您的 web 服務上 hello [Microsoft Azure 機器學習 Web 服務入口網站](https://services.azureml.net)具有範例程式碼，可協助您開始使用。</span><span class="sxs-lookup"><span data-stu-id="abefc-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. hello **Consume** page for your web service on hello [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="abefc-152">如需詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="abefc-152">For more information, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

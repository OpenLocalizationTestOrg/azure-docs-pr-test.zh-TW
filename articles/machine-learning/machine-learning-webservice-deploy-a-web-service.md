---
title: "在 Azure Machine Learning 中部署新的 Web 服務 | Microsoft Docs"
description: "部署以 ARM 為基礎 Web 服務的的工作流程"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: TRUE
ms.openlocfilehash: 1415709f9da2bb2cce859af9feb0ec15c1fa5801
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="6b66e-103">部署新的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="6b66e-103">Deploy a new web service</span></span>
<span data-ttu-id="6b66e-104">Microsoft Azure Machine Learning 現在提供的 Web 服務是以 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 為基礎，允許新的計費方案選項以及將您的 Web 服務部署到多個區域。</span><span class="sxs-lookup"><span data-stu-id="6b66e-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service to multiple regions.</span></span>

<span data-ttu-id="6b66e-105">使用 Microsoft Azure Machine Learning Web Services 部署 Web 服務的一般工作流程為︰</span><span class="sxs-lookup"><span data-stu-id="6b66e-105">The general workflow to deploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="6b66e-106">建立預測性實驗</span><span class="sxs-lookup"><span data-stu-id="6b66e-106">Create a predictive experiment</span></span>
* <span data-ttu-id="6b66e-107">進行部署</span><span class="sxs-lookup"><span data-stu-id="6b66e-107">deploy it</span></span>
* <span data-ttu-id="6b66e-108">設定其名稱</span><span class="sxs-lookup"><span data-stu-id="6b66e-108">configure its name</span></span>
* <span data-ttu-id="6b66e-109">計費方案</span><span class="sxs-lookup"><span data-stu-id="6b66e-109">billing plan</span></span>
* <span data-ttu-id="6b66e-110">進行測試</span><span class="sxs-lookup"><span data-stu-id="6b66e-110">test it</span></span>
* <span data-ttu-id="6b66e-111">加以取用。</span><span class="sxs-lookup"><span data-stu-id="6b66e-111">consume it.</span></span>

<span data-ttu-id="6b66e-112">下圖說明此工作流程。</span><span class="sxs-lookup"><span data-stu-id="6b66e-112">The following graphic illustrates the workflow.</span></span>

![Web 服務部署工作流程][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="6b66e-114">從 Studio 部署 Web 服務</span><span class="sxs-lookup"><span data-stu-id="6b66e-114">Deploy web service from Studio</span></span>
<span data-ttu-id="6b66e-115">將實驗部署為新的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="6b66e-115">To deploy an experiment as a new web service.</span></span> <span data-ttu-id="6b66e-116">登入 Machine Learning Studio，並建立新的預測性 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="6b66e-116">Sign into the Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="6b66e-117">**注意**︰如果您已將實驗部署為傳統 Web 服務，您就無法將它部署為新的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="6b66e-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="6b66e-118">按一下實驗畫布底端的 [執行]，然後按一下 [部署 Web 服務] 和 [部署 Web 服務 [新式]]。</span><span class="sxs-lookup"><span data-stu-id="6b66e-118">Click **Run** at the bottom of the experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="6b66e-119">機器學習 Web 服務管理員的部署頁面將會開啟。</span><span class="sxs-lookup"><span data-stu-id="6b66e-119">The deployment page of the Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="6b66e-120">機器學習 Web 服務管理員部署實驗頁面</span><span class="sxs-lookup"><span data-stu-id="6b66e-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="6b66e-121">在 [部署實驗] 頁面上，輸入 Web 服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="6b66e-121">On the Deploy Experiment page, enter a name for the web service.</span></span>
<span data-ttu-id="6b66e-122">選取定價方案。</span><span class="sxs-lookup"><span data-stu-id="6b66e-122">Select a pricing plan.</span></span> <span data-ttu-id="6b66e-123">如果您有現有的定價方案，可以進行選取，否則您必須為服務建立新的定價方案。</span><span class="sxs-lookup"><span data-stu-id="6b66e-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for the service.</span></span> 

1. <span data-ttu-id="6b66e-124">在 [價格方案] 下拉式清單中，選取現有的方案或選取 [選取新的方案] 選項。</span><span class="sxs-lookup"><span data-stu-id="6b66e-124">In the **Price Plan** drop down, select an existing plan or select the **Select new plan** option.</span></span>
2. <span data-ttu-id="6b66e-125">在 [方案名稱] 中，輸入將識別您帳單上方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="6b66e-125">In **Plan Name**, type a name that will identify the plan on your bill.</span></span>
3. <span data-ttu-id="6b66e-126">選取其中一個 [每月方案層] 。</span><span class="sxs-lookup"><span data-stu-id="6b66e-126">Select one of the **Monthly Plan Tiers**.</span></span> <span data-ttu-id="6b66e-127">請注意，方案層預設為您預設區域的方案，您的 Web 服務會部署到該區域。</span><span class="sxs-lookup"><span data-stu-id="6b66e-127">Note that the plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

<span data-ttu-id="6b66e-128">按一下 [部署]  ，Web 服務的 [快速入門] 頁面就會開啟。</span><span class="sxs-lookup"><span data-stu-id="6b66e-128">Click **Deploy** and the Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="6b66e-129">快速入門頁面</span><span class="sxs-lookup"><span data-stu-id="6b66e-129">Quickstart page</span></span>
<span data-ttu-id="6b66e-130">Web 服務的 [快速入門] 頁面提供您存取建立新的 Web 服務之後最常執行的工作及其指引。</span><span class="sxs-lookup"><span data-stu-id="6b66e-130">The web service Quickstart page gives you access and guidance on the most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="6b66e-131">從這裡您可以輕鬆地存取 [測試] 頁面和 [取用] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6b66e-131">From here you can easily access both the **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="6b66e-132">測試您的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="6b66e-132">Testing your web service</span></span>
<span data-ttu-id="6b66e-133">從 [快速入門] 頁面中，按一下常見工作下的 [測試 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="6b66e-133">From the Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="6b66e-134">以要求-回應服務 (RRS) 測試 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="6b66e-134">To test the web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="6b66e-135">按一下功能表列上的 [測試]  。</span><span class="sxs-lookup"><span data-stu-id="6b66e-135">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="6b66e-136">按一下 [要求-回應] 。</span><span class="sxs-lookup"><span data-stu-id="6b66e-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="6b66e-137">為實驗的輸入資料行輸入適當的值。</span><span class="sxs-lookup"><span data-stu-id="6b66e-137">Enter appropriate values for the input columns of your experiment.</span></span>
* <span data-ttu-id="6b66e-138">按一下 [測試要求-回應] 。</span><span class="sxs-lookup"><span data-stu-id="6b66e-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="6b66e-139">您的結果將會顯示在頁面的右手邊。</span><span class="sxs-lookup"><span data-stu-id="6b66e-139">You results will display on the right hand side of the page.</span></span>

<span data-ttu-id="6b66e-140">若要測試批次執行服務 (BES) Web 服務，您要使用 CSV 檔案︰</span><span class="sxs-lookup"><span data-stu-id="6b66e-140">To test a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="6b66e-141">按一下功能表列上的 [測試]  。</span><span class="sxs-lookup"><span data-stu-id="6b66e-141">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="6b66e-142">按一下 [批次] 。</span><span class="sxs-lookup"><span data-stu-id="6b66e-142">Click **Batch**.</span></span>
* <span data-ttu-id="6b66e-143">在您的輸入下，按一下 [瀏覽] 並導覽至您的範例資料檔案。</span><span class="sxs-lookup"><span data-stu-id="6b66e-143">Under your input, click Browse and navigate to your sample data file.</span></span>
* <span data-ttu-id="6b66e-144">按一下 [ **測試**]。</span><span class="sxs-lookup"><span data-stu-id="6b66e-144">Click **Test**.</span></span>

<span data-ttu-id="6b66e-145">測試的狀態會顯示在 [測試批次作業] 下。</span><span class="sxs-lookup"><span data-stu-id="6b66e-145">The status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="6b66e-146">取用您的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="6b66e-146">Consuming your Web Service</span></span>
<span data-ttu-id="6b66e-147">部署為 Web 服務時，Azure Machine Learning 實驗所提供的 REST API，可供各種裝置和平台使用。</span><span class="sxs-lookup"><span data-stu-id="6b66e-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="6b66e-148">這是因為簡單的 REST API 可接受並回應 JSON 格式化的訊息。</span><span class="sxs-lookup"><span data-stu-id="6b66e-148">This is because the simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="6b66e-149">Azure Machine Learning 入口網站提供的程式碼可用來呼叫 R、C# 和 Python 的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="6b66e-149">The Azure Machine Learning portal provides code that can be used to call the web service in R, C#, and Python.</span></span>

<span data-ttu-id="6b66e-150">您可以在 [取用中] 頁面上找到︰</span><span class="sxs-lookup"><span data-stu-id="6b66e-150">On the Consuming page you can find:</span></span>

* <span data-ttu-id="6b66e-151">應用程式中取用中 Web 服務的 API 金鑰和 URI。</span><span class="sxs-lookup"><span data-stu-id="6b66e-151">The API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="6b66e-152">Excel 和 Web 應用程式範本，以開始啟動您的耗用程序。</span><span class="sxs-lookup"><span data-stu-id="6b66e-152">Excel and web app templates to kick start your consumption process.</span></span>
* <span data-ttu-id="6b66e-153">以 C#、Python 和 R 撰寫，讓您開始的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="6b66e-153">Sample code in C#, python, and R to get you started.</span></span>

<span data-ttu-id="6b66e-154">有關使用 Web 服務的詳細資訊，請參閱[如何使用 Azure Machine Learning Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="6b66e-154">For more information on consuming web services, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b66e-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b66e-155">Next Steps</span></span>
<span data-ttu-id="6b66e-156">如需有關如何取用 Web 服務的詳細資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="6b66e-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="6b66e-157">如何使用 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="6b66e-157">How to consume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="6b66e-158">Azure Machine Learning Web 服務：部署和取用</span><span class="sxs-lookup"><span data-stu-id="6b66e-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->

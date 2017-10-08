---
title: "新的 web 服務，Azure Machine Learning 中 aaaDeploying |Microsoft 文件"
description: "hello 工作流程的部署是 ARM 型 web 服務"
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
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="3d84e-103">部署新的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="3d84e-103">Deploy a new web service</span></span>
<span data-ttu-id="3d84e-104">Microsoft Azure Machine learning 現在提供 web 服務為基礎的[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)允許新的計費計劃選項，或部署您的 web 服務 toomultiple 區域。</span><span class="sxs-lookup"><span data-stu-id="3d84e-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service toomultiple regions.</span></span>

<span data-ttu-id="3d84e-105">hello 一般工作流程 toodeploy 使用 Microsoft Azure 機器學習 Web 服務的 web 服務是：</span><span class="sxs-lookup"><span data-stu-id="3d84e-105">hello general workflow toodeploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="3d84e-106">建立預測性實驗</span><span class="sxs-lookup"><span data-stu-id="3d84e-106">Create a predictive experiment</span></span>
* <span data-ttu-id="3d84e-107">進行部署</span><span class="sxs-lookup"><span data-stu-id="3d84e-107">deploy it</span></span>
* <span data-ttu-id="3d84e-108">設定其名稱</span><span class="sxs-lookup"><span data-stu-id="3d84e-108">configure its name</span></span>
* <span data-ttu-id="3d84e-109">計費方案</span><span class="sxs-lookup"><span data-stu-id="3d84e-109">billing plan</span></span>
* <span data-ttu-id="3d84e-110">進行測試</span><span class="sxs-lookup"><span data-stu-id="3d84e-110">test it</span></span>
* <span data-ttu-id="3d84e-111">加以取用。</span><span class="sxs-lookup"><span data-stu-id="3d84e-111">consume it.</span></span>

<span data-ttu-id="3d84e-112">hello 下列圖形說明 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="3d84e-112">hello following graphic illustrates hello workflow.</span></span>

![Web 服務部署工作流程][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="3d84e-114">從 Studio 部署 Web 服務</span><span class="sxs-lookup"><span data-stu-id="3d84e-114">Deploy web service from Studio</span></span>
<span data-ttu-id="3d84e-115">toodeploy 做為新的 web 服務實驗中。</span><span class="sxs-lookup"><span data-stu-id="3d84e-115">toodeploy an experiment as a new web service.</span></span> <span data-ttu-id="3d84e-116">登入 hello Machine Learning Studio 並建立新的預測 web 服務。</span><span class="sxs-lookup"><span data-stu-id="3d84e-116">Sign into hello Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="3d84e-117">**注意**︰如果您已將實驗部署為傳統 Web 服務，您就無法將它部署為新的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="3d84e-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="3d84e-118">按一下**執行**底部 hello hello 試驗畫布，然後按一下**部署 Web 服務**和**部署 Web 服務 [New]**。</span><span class="sxs-lookup"><span data-stu-id="3d84e-118">Click **Run** at hello bottom of hello experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="3d84e-119">hello 部署的 hello Machine Learning Web 服務管理員 頁面將會開啟。</span><span class="sxs-lookup"><span data-stu-id="3d84e-119">hello deployment page of hello Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="3d84e-120">機器學習 Web 服務管理員部署實驗頁面</span><span class="sxs-lookup"><span data-stu-id="3d84e-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="3d84e-121">在 hello 部署實驗 頁面上，輸入 hello web 服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="3d84e-121">On hello Deploy Experiment page, enter a name for hello web service.</span></span>
<span data-ttu-id="3d84e-122">選取定價方案。</span><span class="sxs-lookup"><span data-stu-id="3d84e-122">Select a pricing plan.</span></span> <span data-ttu-id="3d84e-123">如果您有現有的定價方案，您可以選取它，否則您必須建立新的價格計劃 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="3d84e-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for hello service.</span></span> 

1. <span data-ttu-id="3d84e-124">在 hello**價格計劃**下拉式清單中，選取現有的方案或選取 hello**選取新的計畫**選項。</span><span class="sxs-lookup"><span data-stu-id="3d84e-124">In hello **Price Plan** drop down, select an existing plan or select hello **Select new plan** option.</span></span>
2. <span data-ttu-id="3d84e-125">在**計劃名稱**，輸入會識別在帳單上的 hello 計劃的名稱。</span><span class="sxs-lookup"><span data-stu-id="3d84e-125">In **Plan Name**, type a name that will identify hello plan on your bill.</span></span>
3. <span data-ttu-id="3d84e-126">選取其中一個 hello**每月的計劃層**。</span><span class="sxs-lookup"><span data-stu-id="3d84e-126">Select one of hello **Monthly Plan Tiers**.</span></span> <span data-ttu-id="3d84e-127">請注意，hello 計劃層預設 toohello 預設區域計劃您的 web 服務是部署的 toothat 區域。</span><span class="sxs-lookup"><span data-stu-id="3d84e-127">Note that hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

<span data-ttu-id="3d84e-128">按一下**部署**和您的 web 服務的 hello 快速入門頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="3d84e-128">Click **Deploy** and hello Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="3d84e-129">快速入門頁面</span><span class="sxs-lookup"><span data-stu-id="3d84e-129">Quickstart page</span></span>
<span data-ttu-id="3d84e-130">hello web 服務快速入門 頁面提供您存取和指引 hello 最常見的工作，您將建立新的 web 服務之後執行。</span><span class="sxs-lookup"><span data-stu-id="3d84e-130">hello web service Quickstart page gives you access and guidance on hello most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="3d84e-131">從這裡您可以輕鬆地存取這兩個 hello**測試**頁面和**取用**頁面。</span><span class="sxs-lookup"><span data-stu-id="3d84e-131">From here you can easily access both hello **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="3d84e-132">測試您的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="3d84e-132">Testing your web service</span></span>
<span data-ttu-id="3d84e-133">從 hello 快速入門 頁面上，按一下測試 web 服務在一般工作。</span><span class="sxs-lookup"><span data-stu-id="3d84e-133">From hello Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="3d84e-134">tootest hello web 服務做為要求-回應服務 (RR):</span><span class="sxs-lookup"><span data-stu-id="3d84e-134">tootest hello web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="3d84e-135">按一下**測試**hello 功能表列上。</span><span class="sxs-lookup"><span data-stu-id="3d84e-135">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="3d84e-136">按一下 [要求-回應] 。</span><span class="sxs-lookup"><span data-stu-id="3d84e-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="3d84e-137">Hello 實驗的輸入資料行中輸入適當的值。</span><span class="sxs-lookup"><span data-stu-id="3d84e-137">Enter appropriate values for hello input columns of your experiment.</span></span>
* <span data-ttu-id="3d84e-138">按一下 [測試要求-回應] 。</span><span class="sxs-lookup"><span data-stu-id="3d84e-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="3d84e-139">您的結果會顯示 hello 右手邊的 hello 頁面上。</span><span class="sxs-lookup"><span data-stu-id="3d84e-139">You results will display on hello right hand side of hello page.</span></span>

<span data-ttu-id="3d84e-140">tootest 批次執行服務 (BES) web 服務，您將使用 CSV 檔案：</span><span class="sxs-lookup"><span data-stu-id="3d84e-140">tootest a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="3d84e-141">按一下**測試**hello 功能表列上。</span><span class="sxs-lookup"><span data-stu-id="3d84e-141">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="3d84e-142">按一下 [批次] 。</span><span class="sxs-lookup"><span data-stu-id="3d84e-142">Click **Batch**.</span></span>
* <span data-ttu-id="3d84e-143">在您的輸入，按一下 瀏覽並瀏覽 tooyour 範例資料檔。</span><span class="sxs-lookup"><span data-stu-id="3d84e-143">Under your input, click Browse and navigate tooyour sample data file.</span></span>
* <span data-ttu-id="3d84e-144">按一下 [ **測試**]。</span><span class="sxs-lookup"><span data-stu-id="3d84e-144">Click **Test**.</span></span>

<span data-ttu-id="3d84e-145">您的測試 hello 狀態會顯示下**測試批次作業**。</span><span class="sxs-lookup"><span data-stu-id="3d84e-145">hello status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="3d84e-146">取用您的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="3d84e-146">Consuming your Web Service</span></span>
<span data-ttu-id="3d84e-147">部署為 Web 服務時，Azure Machine Learning 實驗所提供的 REST API，可供各種裝置和平台使用。</span><span class="sxs-lookup"><span data-stu-id="3d84e-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="3d84e-148">這是因為 hello 簡單的 REST API 接受和回應使用 JSON 格式的訊息。</span><span class="sxs-lookup"><span data-stu-id="3d84e-148">This is because hello simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="3d84e-149">hello Azure Machine Learning 入口網站提供的程式碼可以用在 R、 C# 和 Python toocall hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="3d84e-149">hello Azure Machine Learning portal provides code that can be used toocall hello web service in R, C#, and Python.</span></span>

<span data-ttu-id="3d84e-150">您可以在 hello Consuming 頁面上找到：</span><span class="sxs-lookup"><span data-stu-id="3d84e-150">On hello Consuming page you can find:</span></span>

* <span data-ttu-id="3d84e-151">hello API 金鑰，URI 的使用中應用程式 web 服務。</span><span class="sxs-lookup"><span data-stu-id="3d84e-151">hello API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="3d84e-152">Excel 和 web 應用程式範本 tookick 開始耗用量程序。</span><span class="sxs-lookup"><span data-stu-id="3d84e-152">Excel and web app templates tookick start your consumption process.</span></span>
* <span data-ttu-id="3d84e-153">您開始在 C#、 python 和 R tooget 的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="3d84e-153">Sample code in C#, python, and R tooget you started.</span></span>

<span data-ttu-id="3d84e-154">如需有關如何使用 web 服務的詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="3d84e-154">For more information on consuming web services, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d84e-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d84e-155">Next Steps</span></span>
<span data-ttu-id="3d84e-156">如需有關如何取用 Web 服務的詳細資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="3d84e-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="3d84e-157">如何 tooconsume Azure 機器學習 Web 服務</span><span class="sxs-lookup"><span data-stu-id="3d84e-157">How tooconsume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="3d84e-158">Azure Machine Learning Web 服務：部署和取用</span><span class="sxs-lookup"><span data-stu-id="3d84e-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->

---
title: "aaaRetrain 機器學習模型 |Microsoft 文件"
description: "了解 tooretrain 模型和更新 hello Web 服務 toouse hello 新定型的模型在 Azure Machine Learning 中。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="c34ff-103">重新定型機器學習服務模型</span><span class="sxs-lookup"><span data-stu-id="c34ff-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="c34ff-104">Hello 實施的機器學習模型，在 Azure 機器學習程序的一部分，您的模型定型並儲存。</span><span class="sxs-lookup"><span data-stu-id="c34ff-104">As part of hello process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="c34ff-105">您接著使用它 toocreate predicative 的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c34ff-105">You then use it toocreate a predicative Web service.</span></span> <span data-ttu-id="c34ff-106">在 web sites、 儀表板和行動裝置應用程式可以使用 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c34ff-106">hello Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="c34ff-107">您使用 Machine Learning 建立的模型通常不是靜態。</span><span class="sxs-lookup"><span data-stu-id="c34ff-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="c34ff-108">當新的資料可用時，或 hello hello API 取用者擁有自己資料 hello 模型必須 toobe 重新定型。</span><span class="sxs-lookup"><span data-stu-id="c34ff-108">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span> 

<span data-ttu-id="c34ff-109">重新定型可能經常會發生。</span><span class="sxs-lookup"><span data-stu-id="c34ff-109">Retraining may occur frequently.</span></span> <span data-ttu-id="c34ff-110">利用 hello 以程式設計方式重新訓練應用程式開發介面的功能，您可以透過程式設計方式重新訓練 hello hello 重新訓練應用程式開發介面和 update hello Web 服務使用 hello 定型新模型的模型。</span><span class="sxs-lookup"><span data-stu-id="c34ff-110">With hello Programmatic Retraining API feature, you can programmatically retrain hello model using hello Retraining APIs and update hello Web service with hello newly trained model.</span></span> 

<span data-ttu-id="c34ff-111">本文件描述 hello 定型程序，並顯示如何 toouse hello 重新訓練應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="c34ff-111">This document describes hello retraining process, and shows you how toouse hello Retraining APIs.</span></span>

## <a name="why-retrain-defining-hello-problem"></a><span data-ttu-id="c34ff-112">為什麼重新訓練： 定義 hello 問題</span><span class="sxs-lookup"><span data-stu-id="c34ff-112">Why retrain: defining hello problem</span></span>
<span data-ttu-id="c34ff-113">Hello 機器學習，定型程序的一部分，模型是來定型資料集。</span><span class="sxs-lookup"><span data-stu-id="c34ff-113">As part of hello machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="c34ff-114">您使用 Machine Learning 建立的模型通常不是靜態。</span><span class="sxs-lookup"><span data-stu-id="c34ff-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="c34ff-115">當新的資料可用時，或 hello hello API 取用者擁有自己資料 hello 模型必須 toobe 重新定型。</span><span class="sxs-lookup"><span data-stu-id="c34ff-115">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span>

<span data-ttu-id="c34ff-116">在這些情況下，以程式設計方式的應用程式開發介面提供便利的方式 tooallow 您或使用 hello 您應用程式開發介面 toocreate 的用戶端，可以一次或規則為基礎，進行重新培訓 hello 模型使用自己的資料取用者。</span><span class="sxs-lookup"><span data-stu-id="c34ff-116">In these scenarios, a programmatic API provides a convenient way tooallow you or hello consumer of your APIs toocreate a client that can, on a one-time or regular basis, retrain hello model using their own data.</span></span> <span data-ttu-id="c34ff-117">它們可以評估 hello 結果重新訓練，並更新 hello Web 服務 API toouse hello 定型新模型。</span><span class="sxs-lookup"><span data-stu-id="c34ff-117">They can then evaluate hello results of retraining, and update hello Web service API toouse hello newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="c34ff-118">如果您有現有的定型實驗和新的 Web 服務，您可能想 toocheck 出重新定型現有的預測 Web 服務，而不是 hello 之後 > 一節中所述的下列 hello 逐步解說。</span><span class="sxs-lookup"><span data-stu-id="c34ff-118">If you have an existing Training Experiment and New Web service, you may want toocheck out Retrain an existing Predictive Web service instead of following hello walkthrough mentioned in hello following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="c34ff-119">端對端工作流程</span><span class="sxs-lookup"><span data-stu-id="c34ff-119">End-to-end workflow</span></span>
<span data-ttu-id="c34ff-120">hello 程序牽涉到下列元件的 hello: 定型實驗和預測實驗發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c34ff-120">hello process involves hello following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="c34ff-121">tooenable 重新訓練的定型的模型，hello 定型實驗必須發佈為 Web 服務的 hello 輸出定型的模型。</span><span class="sxs-lookup"><span data-stu-id="c34ff-121">tooenable retraining of a trained model, hello Training Experiment must be published as a Web service with hello output of a trained model.</span></span> <span data-ttu-id="c34ff-122">這可讓應用程式開發介面存取 toohello 模型定型。</span><span class="sxs-lookup"><span data-stu-id="c34ff-122">This enables API access toohello model for retraining.</span></span> 

<span data-ttu-id="c34ff-123">hello 步驟適用於 tooboth 新增與傳統 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="c34ff-123">hello following steps apply tooboth New and Classic Web services:</span></span>

<span data-ttu-id="c34ff-124">建立 hello 初始預測 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="c34ff-124">Create hello initial Predictive Web service:</span></span>

* <span data-ttu-id="c34ff-125">建立訓練實驗</span><span class="sxs-lookup"><span data-stu-id="c34ff-125">Create a training experiment</span></span>
* <span data-ttu-id="c34ff-126">建立預測性 Web 實驗</span><span class="sxs-lookup"><span data-stu-id="c34ff-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="c34ff-127">部署預測性 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c34ff-127">Deploy a predictive web service</span></span>

<span data-ttu-id="c34ff-128">進行重新培訓 hello Web 服務：</span><span class="sxs-lookup"><span data-stu-id="c34ff-128">Retrain hello Web service:</span></span>

* <span data-ttu-id="c34ff-129">更新定型實驗 tooallow 重新定型</span><span class="sxs-lookup"><span data-stu-id="c34ff-129">Update training experiment tooallow for retraining</span></span>
* <span data-ttu-id="c34ff-130">部署重新訓練 web 服務的 hello</span><span class="sxs-lookup"><span data-stu-id="c34ff-130">Deploy hello retraining web service</span></span>
* <span data-ttu-id="c34ff-131">使用 hello 批次執行服務的程式碼 tooretrain hello 模型</span><span class="sxs-lookup"><span data-stu-id="c34ff-131">Use hello Batch Execution Service code tooretrain hello model</span></span>

<span data-ttu-id="c34ff-132">Hello 先前步驟的逐步解說，請參閱[重新訓練機器學習模型以程式設計方式](machine-learning-retrain-models-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="c34ff-132">For a walkthrough of hello preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="c34ff-133">toodeploy 新的 web 服務，您必須擁有足夠的權限 hello 訂用帳戶 toowhich 您部署 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="c34ff-133">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="c34ff-134">如需詳細資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="c34ff-134">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="c34ff-135">如果您部署了傳統 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="c34ff-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="c34ff-136">建立新的端點上 hello 預測 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c34ff-136">Create a new Endpoint on hello Predictive Web service</span></span>
* <span data-ttu-id="c34ff-137">取得 hello 修補程式 URL 和程式碼</span><span class="sxs-lookup"><span data-stu-id="c34ff-137">Get hello PATCH URL and code</span></span>
* <span data-ttu-id="c34ff-138">使用 hello 修補程式的 URL toopoint hello hello 新端點重新定型模型</span><span class="sxs-lookup"><span data-stu-id="c34ff-138">Use hello PATCH URL toopoint hello new Endpoint at hello retrained model</span></span> 

<span data-ttu-id="c34ff-139">Hello 先前步驟的逐步解說，請參閱[傳統 Web 服務進行重新培訓](machine-learning-retrain-a-classic-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="c34ff-139">For a walkthrough of hello preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="c34ff-140">如果您執行重新訓練傳統 Web 服務發生問題，請參閱[疑難排解在 Azure 機器學習傳統 Web 服務的定型 hello](machine-learning-troubleshooting-retraining-models.md)。</span><span class="sxs-lookup"><span data-stu-id="c34ff-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting hello retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="c34ff-141">如果您部署了新式 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="c34ff-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="c34ff-142">登入 tooyour Azure 資源管理員帳戶</span><span class="sxs-lookup"><span data-stu-id="c34ff-142">Sign in tooyour Azure Resource Manager account</span></span>
* <span data-ttu-id="c34ff-143">取得 hello Web 服務定義</span><span class="sxs-lookup"><span data-stu-id="c34ff-143">Get hello Web service definition</span></span>
* <span data-ttu-id="c34ff-144">匯出為 JSON 的 hello Web 服務定義</span><span class="sxs-lookup"><span data-stu-id="c34ff-144">Export hello Web Service Definition as JSON</span></span>
* <span data-ttu-id="c34ff-145">更新 hello 參考 toohello `ilearner` hello JSON 中的 blob</span><span class="sxs-lookup"><span data-stu-id="c34ff-145">Update hello reference toohello `ilearner` blob in hello JSON</span></span>
* <span data-ttu-id="c34ff-146">Hello JSON 匯入 Web 服務定義</span><span class="sxs-lookup"><span data-stu-id="c34ff-146">Import hello JSON into a Web Service Definition</span></span>
* <span data-ttu-id="c34ff-147">使用新的 Web 服務定義更新 hello Web 服務</span><span class="sxs-lookup"><span data-stu-id="c34ff-147">Update hello Web service with new Web Service Definition</span></span>

<span data-ttu-id="c34ff-148">Hello 先前步驟的逐步解說，請參閱[重新定型新的 Web 服務使用 hello 機器學習服務管理 PowerShell 指令程式](machine-learning-retrain-new-web-service-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="c34ff-148">For a walkthrough of hello preceding steps, see [Retrain a New Web service using hello Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="c34ff-149">設定重新訓練傳統 Web 服務的 hello 程序牽涉到 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c34ff-149">hello process for setting up retraining for a Classic Web service involves hello following steps:</span></span>

![重新定型程序概觀][1]

<span data-ttu-id="c34ff-151">設定定型新的 Web 服務的 hello 程序包含下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c34ff-151">hello process for setting up retraining for a New Web service involves hello following steps:</span></span>

![重新定型程序概觀][7]

## <a name="other-resources"></a><span data-ttu-id="c34ff-153">其他資源</span><span class="sxs-lookup"><span data-stu-id="c34ff-153">Other Resources</span></span>
* [<span data-ttu-id="c34ff-154">使用 Azure Data Factory 重新定型和更新 Azure Machine Learning 模型</span><span class="sxs-lookup"><span data-stu-id="c34ff-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="c34ff-155">使用 PowerShell，從一個實驗中建立許多機器學習服務模型和 Web 服務端點</span><span class="sxs-lookup"><span data-stu-id="c34ff-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="c34ff-156">hello [AML 定型模型使用 Api](https://www.youtube.com/watch?v=wwjglA8xllg)段影片會示範如何 tooretrain 機器學習模型中建立 Azure Machine Learning 使用 hello 重新訓練應用程式開發介面和 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="c34ff-156">hello [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how tooretrain Machine Learning models created in Azure Machine Learning using hello Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png


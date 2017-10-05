---
title: "重新訓練機器學習模型 | Microsoft Docs"
description: "了解如何在 Azure Machine Learning 中重新定型模型，以及使用新定型的模型來更新 Web 服務。"
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
ms.openlocfilehash: f86c2bc41dd7ff0bc31454a56b84d136dc7d026c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="02c53-103">重新定型機器學習服務模型</span><span class="sxs-lookup"><span data-stu-id="02c53-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="02c53-104">在 Azure Machine Learning 中進行機器學習服務模型的實作程序時，需要定型並儲存您的模型。</span><span class="sxs-lookup"><span data-stu-id="02c53-104">As part of the process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="02c53-105">接著，使用它來建立預測性 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="02c53-105">You then use it to create a predicative Web service.</span></span> <span data-ttu-id="02c53-106">接著才能在網站、儀表板及行動應用程式取用 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="02c53-106">The Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="02c53-107">您使用 Machine Learning 建立的模型通常不是靜態。</span><span class="sxs-lookup"><span data-stu-id="02c53-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="02c53-108">因為當有新資料或 API 取用者有自己的資料時，模型就必須重新定型。</span><span class="sxs-lookup"><span data-stu-id="02c53-108">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span> 

<span data-ttu-id="02c53-109">重新定型可能經常會發生。</span><span class="sxs-lookup"><span data-stu-id="02c53-109">Retraining may occur frequently.</span></span> <span data-ttu-id="02c53-110">有了程式設計重新定型 API 功能後，您能夠使用重新定型 API 以程式設計方式重新定型模型，並使用新定型的模型來更新 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="02c53-110">With the Programmatic Retraining API feature, you can programmatically retrain the model using the Retraining APIs and update the Web service with the newly trained model.</span></span> 

<span data-ttu-id="02c53-111">本文說明重新定型程序，並示範如何使用重新定型 API。</span><span class="sxs-lookup"><span data-stu-id="02c53-111">This document describes the retraining process, and shows you how to use the Retraining APIs.</span></span>

## <a name="why-retrain-defining-the-problem"></a><span data-ttu-id="02c53-112">為何要重新定型：定義問題</span><span class="sxs-lookup"><span data-stu-id="02c53-112">Why retrain: defining the problem</span></span>
<span data-ttu-id="02c53-113">進行 Machine Learning 定型程序時，會使用一組資料來將模型定型。</span><span class="sxs-lookup"><span data-stu-id="02c53-113">As part of the machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="02c53-114">您使用 Machine Learning 建立的模型通常不是靜態。</span><span class="sxs-lookup"><span data-stu-id="02c53-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="02c53-115">因為當有新資料或 API 取用者有自己的資料時，模型就必須重新定型。</span><span class="sxs-lookup"><span data-stu-id="02c53-115">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span>

<span data-ttu-id="02c53-116">在這些情況下，程式設計 API 可方便您或 API 取用者建立能夠單次或定期使用自己的資料重新定型模型的用戶端。</span><span class="sxs-lookup"><span data-stu-id="02c53-116">In these scenarios, a programmatic API provides a convenient way to allow you or the consumer of your APIs to create a client that can, on a one-time or regular basis, retrain the model using their own data.</span></span> <span data-ttu-id="02c53-117">接著可以評估重新定型的結果，然後更新 Web 服務 API 以使用新定型的模型。</span><span class="sxs-lookup"><span data-stu-id="02c53-117">They can then evaluate the results of retraining, and update the Web service API to use the newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="02c53-118">如果您現在已有訓練實驗和新式 Web 服務，建議您查看＜重新定型現有預測性 Web 服務＞而不是遵循下一節中所述的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="02c53-118">If you have an existing Training Experiment and New Web service, you may want to check out Retrain an existing Predictive Web service instead of following the walkthrough mentioned in the following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="02c53-119">端對端工作流程</span><span class="sxs-lookup"><span data-stu-id="02c53-119">End-to-end workflow</span></span>
<span data-ttu-id="02c53-120">此程序包含下列部分：訓練實驗以及以 Web 服務形式發佈的預測性實驗。</span><span class="sxs-lookup"><span data-stu-id="02c53-120">The process involves the following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="02c53-121">若要啟用已定型模型的重新定型功能，必須利用定型模型的輸出將訓練實驗發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="02c53-121">To enable retraining of a trained model, the Training Experiment must be published as a Web service with the output of a trained model.</span></span> <span data-ttu-id="02c53-122">這樣做可讓 API 存取模型進行重新定型。</span><span class="sxs-lookup"><span data-stu-id="02c53-122">This enables API access to the model for retraining.</span></span> 

<span data-ttu-id="02c53-123">下列步驟適用於新式和傳統 Web 服務︰</span><span class="sxs-lookup"><span data-stu-id="02c53-123">The following steps apply to both New and Classic Web services:</span></span>

<span data-ttu-id="02c53-124">建立初始的預測性 Web 服務︰</span><span class="sxs-lookup"><span data-stu-id="02c53-124">Create the initial Predictive Web service:</span></span>

* <span data-ttu-id="02c53-125">建立訓練實驗</span><span class="sxs-lookup"><span data-stu-id="02c53-125">Create a training experiment</span></span>
* <span data-ttu-id="02c53-126">建立預測性 Web 實驗</span><span class="sxs-lookup"><span data-stu-id="02c53-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="02c53-127">部署預測性 Web 服務</span><span class="sxs-lookup"><span data-stu-id="02c53-127">Deploy a predictive web service</span></span>

<span data-ttu-id="02c53-128">重新定型 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="02c53-128">Retrain the Web service:</span></span>

* <span data-ttu-id="02c53-129">更新訓練實驗以便能重新定型</span><span class="sxs-lookup"><span data-stu-id="02c53-129">Update training experiment to allow for retraining</span></span>
* <span data-ttu-id="02c53-130">部署重新訓練的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="02c53-130">Deploy the retraining web service</span></span>
* <span data-ttu-id="02c53-131">使用批次執行服務程式碼重新定型模型</span><span class="sxs-lookup"><span data-stu-id="02c53-131">Use the Batch Execution Service code to retrain the model</span></span>

<span data-ttu-id="02c53-132">如需上述步驟的逐步解說，請參閱[以程式設計方式重新定型機器學習服務模型](machine-learning-retrain-models-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="02c53-132">For a walkthrough of the preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="02c53-133">若要部署新的 Web 服務，您必須在要部署 Web 服務的訂用帳戶中具備足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="02c53-133">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="02c53-134">如需詳細資訊，請參閱[使用 Azure Machine Learning Web 服務入口網站管理 Web 服務](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="02c53-134">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="02c53-135">如果您部署了傳統 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="02c53-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="02c53-136">在預測性 Web 服務上建立新端點</span><span class="sxs-lookup"><span data-stu-id="02c53-136">Create a new Endpoint on the Predictive Web service</span></span>
* <span data-ttu-id="02c53-137">取得 PATCH URL 和程式碼</span><span class="sxs-lookup"><span data-stu-id="02c53-137">Get the PATCH URL and code</span></span>
* <span data-ttu-id="02c53-138">使用 PATCH URL 以指出位於重新定型模型中的新端點</span><span class="sxs-lookup"><span data-stu-id="02c53-138">Use the PATCH URL to point the new Endpoint at the retrained model</span></span> 

<span data-ttu-id="02c53-139">如需上述步驟的逐步解說，請參閱[重新定型傳統 Web 服務](machine-learning-retrain-a-classic-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="02c53-139">For a walkthrough of the preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="02c53-140">如果您在重新定型傳統 Web 服務時遇到麻煩，請參閱[針對 Azure Machine Learning 傳統 Web 服務的重新訓練進行疑難排解](machine-learning-troubleshooting-retraining-models.md)。</span><span class="sxs-lookup"><span data-stu-id="02c53-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting the retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="02c53-141">如果您部署了新式 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="02c53-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="02c53-142">登入您的 Azure Resource Manager 帳戶</span><span class="sxs-lookup"><span data-stu-id="02c53-142">Sign in to your Azure Resource Manager account</span></span>
* <span data-ttu-id="02c53-143">取得 Web 服務定義</span><span class="sxs-lookup"><span data-stu-id="02c53-143">Get the Web service definition</span></span>
* <span data-ttu-id="02c53-144">將 Web 服務定義匯出為 JSON</span><span class="sxs-lookup"><span data-stu-id="02c53-144">Export the Web Service Definition as JSON</span></span>
* <span data-ttu-id="02c53-145">在 JSON 中更新 `ilearner` Blob 的參考</span><span class="sxs-lookup"><span data-stu-id="02c53-145">Update the reference to the `ilearner` blob in the JSON</span></span>
* <span data-ttu-id="02c53-146">將 JSON 匯入至 Web 服務定義</span><span class="sxs-lookup"><span data-stu-id="02c53-146">Import the JSON into a Web Service Definition</span></span>
* <span data-ttu-id="02c53-147">使用新的 Web 服務定義更新 Web 服務</span><span class="sxs-lookup"><span data-stu-id="02c53-147">Update the Web service with new Web Service Definition</span></span>

<span data-ttu-id="02c53-148">如需上述步驟的逐步解說，請參閱[使用 Machine Learning Management PowerShell Cmdlet 重新定型新的 Web 服務](machine-learning-retrain-new-web-service-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="02c53-148">For a walkthrough of the preceding steps, see [Retrain a New Web service using the Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="02c53-149">傳統 Web 服務設定重新定型的程序包含下列步驟：</span><span class="sxs-lookup"><span data-stu-id="02c53-149">The process for setting up retraining for a Classic Web service involves the following steps:</span></span>

![重新定型程序概觀][1]

<span data-ttu-id="02c53-151">新式 Web 服務設定重新定型的程序包含下列步驟：</span><span class="sxs-lookup"><span data-stu-id="02c53-151">The process for setting up retraining for a New Web service involves the following steps:</span></span>

![重新定型程序概觀][7]

## <a name="other-resources"></a><span data-ttu-id="02c53-153">其他資源</span><span class="sxs-lookup"><span data-stu-id="02c53-153">Other Resources</span></span>
* [<span data-ttu-id="02c53-154">使用 Azure Data Factory 重新定型和更新 Azure Machine Learning 模型</span><span class="sxs-lookup"><span data-stu-id="02c53-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="02c53-155">使用 PowerShell，從一個實驗中建立許多機器學習服務模型和 Web 服務端點</span><span class="sxs-lookup"><span data-stu-id="02c53-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="02c53-156">[使用 API 的 AML 重新定型模型](https://www.youtube.com/watch?v=wwjglA8xllg)影片會示範如何使用重新定型 API 和 PowerShell，將 Azure Machine Learning 中所建立的機器學習服務模型重新定型。</span><span class="sxs-lookup"><span data-stu-id="02c53-156">The [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how to retrain Machine Learning models created in Azure Machine Learning using the Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png


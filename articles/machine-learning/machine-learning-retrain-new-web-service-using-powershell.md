---
title: "使用 PowerShell 重新訓練新的 Azure Machine Learning Web 服務 | Microsoft Docs"
description: "了解如何使用 Machine Learning Management PowerShell Cmdlet 在 Azure Machine Learning 中以程式設計方式重新訓練模型，以及使用新訓練的模型來更新 Web 服務。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 804dd59e62f38ee1878045d93211ee18e0d5bfce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-the-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="8a389-103">使用 Machine Learning Management PowerShell Cmdlet 重新訓練以 Resource Manager 為基礎的新 Web 服務</span><span class="sxs-lookup"><span data-stu-id="8a389-103">Retrain a New Resource Manager based web service using the Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="8a389-104">當您重新訓練新的 Web 服務時，可以更新預測性 Web 服務定義以參考新的訓練模型。</span><span class="sxs-lookup"><span data-stu-id="8a389-104">When you retrain a New web service, you update the predictive web service definition to reference the new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="8a389-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="8a389-105">Prerequisites</span></span>
<span data-ttu-id="8a389-106">您必須設定訓練實驗與預測性實驗，如[以程式設計方式重新定型機器學習服務模型](machine-learning-retrain-models-programmatically.md)中所示。</span><span class="sxs-lookup"><span data-stu-id="8a389-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8a389-107">預測性實驗必須部署為 Azure Resource Manager (新) 型 Machine Learning Web 服務。</span><span class="sxs-lookup"><span data-stu-id="8a389-107">The predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="8a389-108">若要部署新的 Web 服務，您必須在要部署 Web 服務的訂用帳戶中具備足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="8a389-108">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="8a389-109">如需詳細資訊，請參閱[使用 Azure Machine Learning Web 服務入口網站管理 Web 服務](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="8a389-109">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="8a389-110">如需關於部署 Web 服務的其他資訊，請參閱[部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="8a389-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="8a389-111">此程序要求您已安裝 Azure Machine Learning Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8a389-111">This process requires that you have installed the Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="8a389-112">如需安裝 Machine Learning cmdlet 的資訊，請參閱 MSDN 上的 [Azure Machine Learning Cmdlet](https://msdn.microsoft.com/library/azure/mt767952.aspx) 參考。</span><span class="sxs-lookup"><span data-stu-id="8a389-112">For information installing the Machine Learning cmdlets, see the [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="8a389-113">已從重新定型輸出中複製下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="8a389-113">Copied the following information from the retraining output:</span></span>

* <span data-ttu-id="8a389-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="8a389-114">BaseLocation</span></span>
* <span data-ttu-id="8a389-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="8a389-115">RelativeLocation</span></span>

<span data-ttu-id="8a389-116">您採取的步驟如下︰</span><span class="sxs-lookup"><span data-stu-id="8a389-116">The steps you take are:</span></span>

1. <span data-ttu-id="8a389-117">登入您的 Azure Resource Manager 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8a389-117">Sign in to your Azure Resource Manager account.</span></span>
2. <span data-ttu-id="8a389-118">取得 Web 服務定義</span><span class="sxs-lookup"><span data-stu-id="8a389-118">Get the web service definition</span></span>
3. <span data-ttu-id="8a389-119">將 Web 服務定義匯出為 JSON</span><span class="sxs-lookup"><span data-stu-id="8a389-119">Export the Web Service Definition as JSON</span></span>
4. <span data-ttu-id="8a389-120">在 JSON 中將參考更新為 ilearner blob。</span><span class="sxs-lookup"><span data-stu-id="8a389-120">Update the reference to the ilearner blob in the JSON.</span></span>
5. <span data-ttu-id="8a389-121">將 JSON 匯入至 Web 服務定義</span><span class="sxs-lookup"><span data-stu-id="8a389-121">Import the JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="8a389-122">使用新的 Web 服務定義更新 Web 服務</span><span class="sxs-lookup"><span data-stu-id="8a389-122">Update the web service with new Web Service Definition</span></span>

## <a name="sign-in-to-your-azure-resource-manager-account"></a><span data-ttu-id="8a389-123">登入您的 Azure Resource Manager 帳戶</span><span class="sxs-lookup"><span data-stu-id="8a389-123">Sign in to your Azure Resource Manager account</span></span>
<span data-ttu-id="8a389-124">您必須先在 PowerShell 環境中，使用 [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) Cmdlet 登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8a389-124">You must first sign in to your Azure account from within the PowerShell environment using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition"></a><span data-ttu-id="8a389-125">取得 Web 服務定義</span><span class="sxs-lookup"><span data-stu-id="8a389-125">Get the Web Service Definition</span></span>
<span data-ttu-id="8a389-126">接下來，呼叫 [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) Cmdlet 取得 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="8a389-126">Next, get the Web Service by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="8a389-127">Web 服務定義是 Web 服務訓練模型的內部表示法，且不可直接修改。</span><span class="sxs-lookup"><span data-stu-id="8a389-127">The Web Service Definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="8a389-128">請確定您要擷取的是預測性實驗 (而非訓練實驗) 的 Web 服務定義。</span><span class="sxs-lookup"><span data-stu-id="8a389-128">Make sure that you are retrieving the Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="8a389-129">若要判斷現有 Web 服務的資源群組名稱，執行不含任何參數的 Get-AzureRmMlWebService cmdlet 來顯示您訂用帳戶中的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="8a389-129">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="8a389-130">找出 Web 服務，再查看其 Web 服務識別碼。</span><span class="sxs-lookup"><span data-stu-id="8a389-130">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="8a389-131">資源群組的名稱是識別碼中的第四個元素，緊接在 resourceGroups  元素之後。</span><span class="sxs-lookup"><span data-stu-id="8a389-131">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="8a389-132">在下列範例中，資源群組名稱是 Default-MachineLearning-SouthCentralUS。</span><span class="sxs-lookup"><span data-stu-id="8a389-132">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="8a389-133">或者，若要判斷現有 Web 服務的資源群組名稱，登入 Microsoft Azure Machine Learning Web 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="8a389-133">Alternatively, to determine the resource group name of an existing web service, log on to the Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="8a389-134">選取 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="8a389-134">Select the web service.</span></span> <span data-ttu-id="8a389-135">資源群組名稱是 Web 服務 URL 的第五個元素，緊接在 resourceGroups  元素之後。</span><span class="sxs-lookup"><span data-stu-id="8a389-135">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="8a389-136">在下列範例中，資源群組名稱是 Default-MachineLearning-SouthCentralUS。</span><span class="sxs-lookup"><span data-stu-id="8a389-136">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-as-json"></a><span data-ttu-id="8a389-137">將 Web 服務定義匯出為 JSON</span><span class="sxs-lookup"><span data-stu-id="8a389-137">Export the Web Service Definition as JSON</span></span>
<span data-ttu-id="8a389-138">若要將定義修改為定型模型以使用新定型的模型，您必須先使用 [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet 將其匯出為 JSON 格式檔案。</span><span class="sxs-lookup"><span data-stu-id="8a389-138">To modify the definition to the trained model to use the newly Trained Model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob-in-the-json"></a><span data-ttu-id="8a389-139">在 JSON 中將參考更新為 ilearner blob。</span><span class="sxs-lookup"><span data-stu-id="8a389-139">Update the reference to the ilearner blob in the JSON.</span></span>
<span data-ttu-id="8a389-140">在資產中，找出 [定型模型]，使用 ilearner blob 的 URI 更新 locationInfo 節點中的 uri 值。</span><span class="sxs-lookup"><span data-stu-id="8a389-140">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="8a389-141">URI 的產生方式為結合來自 BES 重新定型呼叫輸出的 BaseLocation 和 RelativeLocation。</span><span class="sxs-lookup"><span data-stu-id="8a389-141">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span> <span data-ttu-id="8a389-142">這會更新路徑以參考新定型的模型。</span><span class="sxs-lookup"><span data-stu-id="8a389-142">This updates the path to reference the new trained model.</span></span>

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-the-json-into-a-web-service-definition"></a><span data-ttu-id="8a389-143">將 JSON 匯入至 Web 服務定義</span><span class="sxs-lookup"><span data-stu-id="8a389-143">Import the JSON into a Web Service Definition</span></span>
<span data-ttu-id="8a389-144">您必須使用 [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) Cmdlet 將修改過的 JSON 檔案轉換回可用來更新 Web 服務定義的 Web 服務定義。</span><span class="sxs-lookup"><span data-stu-id="8a389-144">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition that you can use to update the Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service-with-new-web-service-definition"></a><span data-ttu-id="8a389-145">使用新的 Web 服務定義更新 Web 服務</span><span class="sxs-lookup"><span data-stu-id="8a389-145">Update the web service with new Web Service Definition</span></span>
<span data-ttu-id="8a389-146">最後，使用 [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) Cmdlet 來更新 Web 服務定義。</span><span class="sxs-lookup"><span data-stu-id="8a389-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="8a389-147">摘要</span><span class="sxs-lookup"><span data-stu-id="8a389-147">Summary</span></span>
<span data-ttu-id="8a389-148">您可以使用 Machine Learning PowerShell Management Cmdlet 來更新預測性 Web 服務的定型模型，運用於如下案例︰</span><span class="sxs-lookup"><span data-stu-id="8a389-148">Using the Machine Learning PowerShell management cmdlets, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="8a389-149">定期以新的資料重新定型模型。</span><span class="sxs-lookup"><span data-stu-id="8a389-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="8a389-150">散發模型給客戶，目的是要讓他們使用自己的資料重新定型模型。</span><span class="sxs-lookup"><span data-stu-id="8a389-150">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>


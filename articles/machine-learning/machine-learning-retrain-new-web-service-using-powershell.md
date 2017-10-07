---
title: "新的 Azure Machine Learning web 服務使用 PowerShell aaaRetrain |Microsoft 文件"
description: "了解 tooprogrammatically 重新定型模型和更新 hello web 服務 toouse hello 新定型的模型使用 hello 機器學習服務管理 PowerShell 指令程式的 Azure Machine Learning 中。"
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
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="a733c-103">進行重新培訓新的資源管理員基礎 web 服務使用 hello 機器學習服務管理 PowerShell 指令程式</span><span class="sxs-lookup"><span data-stu-id="a733c-103">Retrain a New Resource Manager based web service using hello Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="a733c-104">當您重新訓練新的 web 服務時，您會更新 hello 預測 web 服務定義 tooreference hello 新定型的模型。</span><span class="sxs-lookup"><span data-stu-id="a733c-104">When you retrain a New web service, you update hello predictive web service definition tooreference hello new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="a733c-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="a733c-105">Prerequisites</span></span>
<span data-ttu-id="a733c-106">您必須設定訓練實驗與預測性實驗，如[以程式設計方式重新定型機器學習服務模型](machine-learning-retrain-models-programmatically.md)中所示。</span><span class="sxs-lookup"><span data-stu-id="a733c-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a733c-107">hello 預測實驗必須部署為 Azure 資源管理員 （新） 基礎機器學習 web 服務。</span><span class="sxs-lookup"><span data-stu-id="a733c-107">hello predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="a733c-108">toodeploy 新的 web 服務，您必須擁有足夠的權限 hello 訂用帳戶 toowhich 您部署 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="a733c-108">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="a733c-109">如需詳細資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="a733c-109">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="a733c-110">如需關於部署 Web 服務的其他資訊，請參閱[部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="a733c-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="a733c-111">此程序需要您已安裝 hello Azure 機器學習指令程式。</span><span class="sxs-lookup"><span data-stu-id="a733c-111">This process requires that you have installed hello Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="a733c-112">安裝 hello 機器學習服務 cmdlet 的詳細資訊，請參閱 hello [Azure 機器學習指令程式](https://msdn.microsoft.com/library/azure/mt767952.aspx)MSDN 上的參考。</span><span class="sxs-lookup"><span data-stu-id="a733c-112">For information installing hello Machine Learning cmdlets, see hello [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="a733c-113">複製的 hello hello 重新訓練輸出中的下列資訊：</span><span class="sxs-lookup"><span data-stu-id="a733c-113">Copied hello following information from hello retraining output:</span></span>

* <span data-ttu-id="a733c-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="a733c-114">BaseLocation</span></span>
* <span data-ttu-id="a733c-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="a733c-115">RelativeLocation</span></span>

<span data-ttu-id="a733c-116">hello 您採取的步驟如下：</span><span class="sxs-lookup"><span data-stu-id="a733c-116">hello steps you take are:</span></span>

1. <span data-ttu-id="a733c-117">登入 tooyour Azure 資源管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="a733c-117">Sign in tooyour Azure Resource Manager account.</span></span>
2. <span data-ttu-id="a733c-118">取得 hello web 服務定義</span><span class="sxs-lookup"><span data-stu-id="a733c-118">Get hello web service definition</span></span>
3. <span data-ttu-id="a733c-119">匯出為 JSON 的 hello Web 服務定義</span><span class="sxs-lookup"><span data-stu-id="a733c-119">Export hello Web Service Definition as JSON</span></span>
4. <span data-ttu-id="a733c-120">更新 hello JSON 中的 hello 參考 toohello ilearner 做為 blob。</span><span class="sxs-lookup"><span data-stu-id="a733c-120">Update hello reference toohello ilearner blob in hello JSON.</span></span>
5. <span data-ttu-id="a733c-121">Hello JSON 匯入 Web 服務定義</span><span class="sxs-lookup"><span data-stu-id="a733c-121">Import hello JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="a733c-122">使用新的 Web 服務定義更新 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="a733c-122">Update hello web service with new Web Service Definition</span></span>

## <a name="sign-in-tooyour-azure-resource-manager-account"></a><span data-ttu-id="a733c-123">登入 tooyour Azure 資源管理員帳戶</span><span class="sxs-lookup"><span data-stu-id="a733c-123">Sign in tooyour Azure Resource Manager account</span></span>
<span data-ttu-id="a733c-124">您必須先登入從使用 hello hello PowerShell 環境中的 Azure 帳戶 tooyour[新增 AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a733c-124">You must first sign in tooyour Azure account from within hello PowerShell environment using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition"></a><span data-ttu-id="a733c-125">取得 Web 服務定義 hello</span><span class="sxs-lookup"><span data-stu-id="a733c-125">Get hello Web Service Definition</span></span>
<span data-ttu-id="a733c-126">接下來，取得 hello Web 服務所呼叫的 hello [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a733c-126">Next, get hello Web Service by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="a733c-127">hello Web 服務定義是 hello 定型模型的 hello web 服務的內部表示法，並不是直接修改。</span><span class="sxs-lookup"><span data-stu-id="a733c-127">hello Web Service Definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="a733c-128">請確定您會預測實驗和未定型實驗擷取 hello Web 服務定義。</span><span class="sxs-lookup"><span data-stu-id="a733c-128">Make sure that you are retrieving hello Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="a733c-129">toodetermine hello 資源群組名稱的現有 web 服務，在您訂用帳戶中執行不含任何參數 toodisplay hello web 服務的 hello Get AzureRmMlWebService cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a733c-129">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="a733c-130">找出 hello web 服務，然後查看 [其 web 服務識別碼。</span><span class="sxs-lookup"><span data-stu-id="a733c-130">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="a733c-131">hello hello 資源群組名稱是 hello 識別碼 hello 第四個元素後方 hello *resourceGroups*項目。</span><span class="sxs-lookup"><span data-stu-id="a733c-131">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="a733c-132">在下列範例的 hello，hello 資源群組名稱會是預設-MachineLearning-SouthCentralUS。</span><span class="sxs-lookup"><span data-stu-id="a733c-132">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="a733c-133">或者，toodetermine hello 資源群組名稱的現有 web 服務，toohello Microsoft Azure 機器學習 Web 服務入口網站上的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a733c-133">Alternatively, toodetermine hello resource group name of an existing web service, log on toohello Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="a733c-134">選取 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="a733c-134">Select hello web service.</span></span> <span data-ttu-id="a733c-135">hello 資源群組名稱是 hello hello web 服務，URL hello 第五個項目後方 hello *resourceGroups*項目。</span><span class="sxs-lookup"><span data-stu-id="a733c-135">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="a733c-136">在下列範例的 hello，hello 資源群組名稱會是預設-MachineLearning-SouthCentralUS。</span><span class="sxs-lookup"><span data-stu-id="a733c-136">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a><span data-ttu-id="a733c-137">匯出為 JSON 的 hello Web 服務定義</span><span class="sxs-lookup"><span data-stu-id="a733c-137">Export hello Web Service Definition as JSON</span></span>
<span data-ttu-id="a733c-138">toomodify hello 定義 toohello 定型模型 toouse 新 hello 定型的模型，您必須先使用 hello[匯出 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport 它 tooa JSON 格式的檔案。</span><span class="sxs-lookup"><span data-stu-id="a733c-138">toomodify hello definition toohello trained model toouse hello newly Trained Model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a><span data-ttu-id="a733c-139">更新 hello JSON 中的 hello 參考 toohello ilearner 做為 blob。</span><span class="sxs-lookup"><span data-stu-id="a733c-139">Update hello reference toohello ilearner blob in hello JSON.</span></span>
<span data-ttu-id="a733c-140">在 [hello 資產，找出 hello [定型的模型]，更新 hello *uri* hello 中的值*locationInfo*節點以 hello hello ilearner 做為 blob 的 URI。</span><span class="sxs-lookup"><span data-stu-id="a733c-140">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="a733c-141">hello URI 由產生結合 hello *BaseLocation*和 hello *RelativeLocation* hello BES 訓練呼叫 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="a733c-141">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span> <span data-ttu-id="a733c-142">這會更新 hello 路徑 tooreference hello 新定型的模型。</span><span class="sxs-lookup"><span data-stu-id="a733c-142">This updates hello path tooreference hello new trained model.</span></span>

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

## <a name="import-hello-json-into-a-web-service-definition"></a><span data-ttu-id="a733c-143">Hello JSON 匯入 Web 服務定義</span><span class="sxs-lookup"><span data-stu-id="a733c-143">Import hello JSON into a Web Service Definition</span></span>
<span data-ttu-id="a733c-144">您必須使用 hello[匯入 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello 修改成 Web 服務定義，您可以使用 tooupdate hello Web 服務定義 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="a733c-144">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition that you can use tooupdate hello Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a><span data-ttu-id="a733c-145">使用新的 Web 服務定義更新 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="a733c-145">Update hello web service with new Web Service Definition</span></span>
<span data-ttu-id="a733c-146">最後，您使用[更新 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web 服務定義。</span><span class="sxs-lookup"><span data-stu-id="a733c-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="a733c-147">摘要</span><span class="sxs-lookup"><span data-stu-id="a733c-147">Summary</span></span>
<span data-ttu-id="a733c-148">您可以使用 hello 機器學習 PowerShell 管理 cmdlet，來更新 hello 定型的模型的預測的 Web 服務，啟用這類的案例：</span><span class="sxs-lookup"><span data-stu-id="a733c-148">Using hello Machine Learning PowerShell management cmdlets, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="a733c-149">定期以新的資料重新定型模型。</span><span class="sxs-lookup"><span data-stu-id="a733c-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="a733c-150">Hello 目標是讓它們重新訓練 hello 模型使用自己的資料模型 toocustomers 的散發。</span><span class="sxs-lookup"><span data-stu-id="a733c-150">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>


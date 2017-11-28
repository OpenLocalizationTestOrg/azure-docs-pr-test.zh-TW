---
title: "aaaCreate 多個模型，從一個實驗 |Microsoft 文件"
description: "使用 PowerShell toocreate 多個機器學習模型和 web 服務端點以 hello 相同的演算法，但不同的訓練資料集。"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="a0408-103">使用 PowerShell，從一個實驗中建立許多機器學習服務模型和 Web 服務端點</span><span class="sxs-lookup"><span data-stu-id="a0408-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="a0408-104">以下是常見的機器學習問題： 您擁有 hello 的許多模型想 toocreate 同一個訓練工作流程並使用 hello 相同的演算法，但有不同的訓練資料集做為輸入。</span><span class="sxs-lookup"><span data-stu-id="a0408-104">Here's a common machine learning problem: You want toocreate many models that have hello same training workflow and use hello same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="a0408-105">本文章將示範如何 toodo 這在 Azure Machine Learning Studio 使用只要單一的實驗中的小數位數。</span><span class="sxs-lookup"><span data-stu-id="a0408-105">This article shows you how toodo this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="a0408-106">例如，假設您擁有一家全球性自行車出租加盟商。</span><span class="sxs-lookup"><span data-stu-id="a0408-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="a0408-107">您想的 toobuild 迴歸模型 toopredict hello 以租用方式佔用指定根據歷程記錄資料。</span><span class="sxs-lookup"><span data-stu-id="a0408-107">You want toobuild a regression model toopredict hello rental demand based on historic data.</span></span> <span data-ttu-id="a0408-108">您有 1000 以租用方式佔用位置 hello 世界各地，而您已收集到的每個位置，其中包含重要功能，例如日期、 時間、 天氣和是特定 tooeach 位置的流量的資料集。</span><span class="sxs-lookup"><span data-stu-id="a0408-108">You have 1,000 rental locations across hello world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific tooeach location.</span></span>

<span data-ttu-id="a0408-109">您可以先培訓模型一次使用 hello 的所有資料集的合併的版本，跨所有位置。</span><span class="sxs-lookup"><span data-stu-id="a0408-109">You could train your model once using a merged version of all hello datasets across all locations.</span></span> <span data-ttu-id="a0408-110">但是因為您的位置中每個唯一的環境，較好的做法是 tootrain 迴歸模型使用的每個位置分別 hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="a0408-110">But because each of your locations has a unique environment, a better approach would be tootrain your regression model separately using hello dataset for each location.</span></span> <span data-ttu-id="a0408-111">這樣一來，每個已定型的模型無法納入帳戶 hello 不同的存放區大小、 磁碟區、 geography、 母體擴展、 bike 易記流量的環境中，*等*。</span><span class="sxs-lookup"><span data-stu-id="a0408-111">That way, each trained model could take into account hello different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="a0408-112">可能 hello 最好的方法，但您不想將定型實驗 toocreate 1000 Azure Machine Learning 中的與每一個代表唯一的位置。</span><span class="sxs-lookup"><span data-stu-id="a0408-112">That may be hello best approach, but you don't want toocreate 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="a0408-113">除了非常龐大的工作，也是看起來非常沒有效率，因為每個實驗會擁有所有 hello 除了 hello 定型資料集相同的元件。</span><span class="sxs-lookup"><span data-stu-id="a0408-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all hello same components except for hello training dataset.</span></span>

<span data-ttu-id="a0408-114">幸運的是，我們可以完成這項作業使用 hello[重新訓練應用程式開發介面的 Azure Machine Learning](machine-learning-retrain-models-programmatically.md)和自動化 hello 工作[Azure 機器學習 PowerShell](machine-learning-powershell-module.md)。</span><span class="sxs-lookup"><span data-stu-id="a0408-114">Fortunately, we can accomplish this by using hello [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating hello task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a0408-115">toomake 更快速執行我們的範例，我們會減少 hello 1,000 too10 的位置數目。</span><span class="sxs-lookup"><span data-stu-id="a0408-115">toomake our sample run faster, we'll reduce hello number of locations from 1,000 too10.</span></span> <span data-ttu-id="a0408-116">但 hello 相同的原則和程序適用於 too1，000 的位置。</span><span class="sxs-lookup"><span data-stu-id="a0408-116">But hello same principles and procedures apply too1,000 locations.</span></span> <span data-ttu-id="a0408-117">hello 唯一的差別是如果您想 1000 個資料集 tootrain 您可能想 toothink 執行下列 PowerShell 指令碼，以平行方式 hello。</span><span class="sxs-lookup"><span data-stu-id="a0408-117">hello only difference is that if you want tootrain from 1,000 datasets you probably want toothink of running hello following PowerShell scripts in parallel.</span></span> <span data-ttu-id="a0408-118">如何 toodo 超出 hello 範圍的本文中，但您可以找到的範例 PowerShell 多執行緒處理 hello 網際網路上。</span><span class="sxs-lookup"><span data-stu-id="a0408-118">How toodo that is beyond hello scope of this article, but you can find examples of PowerShell multi-threading on hello Internet.</span></span>  
> 
> 

## <a name="set-up-hello-training-experiment"></a><span data-ttu-id="a0408-119">設定 hello 定型實驗</span><span class="sxs-lookup"><span data-stu-id="a0408-119">Set up hello training experiment</span></span>
<span data-ttu-id="a0408-120">我們會 toouse 範例[定型實驗](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1)，我們已經建立了在 hello [Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="a0408-120">We're going toouse an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="a0408-121">在 [Azure Machine Learning Studio](https://studio.azureml.net) 工作區開啟此實驗。</span><span class="sxs-lookup"><span data-stu-id="a0408-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="a0408-122">在此範例中以及 order toofollow，您可能想 toouse 標準的工作區，而不是免費的工作區。</span><span class="sxs-lookup"><span data-stu-id="a0408-122">In order toofollow along with this example, you may want toouse a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="a0408-123">我們將針對每個客戶的總計的 10 個端點-建立一個端點，以及將需要標準的工作區因為免費工作區是有限的 too3 端點。</span><span class="sxs-lookup"><span data-stu-id="a0408-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited too3 endpoints.</span></span> <span data-ttu-id="a0408-124">如果您只需要免費工作區，只需修改 hello tooallow 只有 3 位置底下的指令碼。</span><span class="sxs-lookup"><span data-stu-id="a0408-124">If you only have a free workspace, just modify hello scripts below tooallow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="a0408-125">hello 實驗使用**匯入資料**模組 tooimport hello 定型資料集*customer001.csv*從 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a0408-125">hello experiment uses an **Import Data** module tooimport hello training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="a0408-126">假設我們收集從所有自行車以租用方式佔用位置的定型資料集，而且它們儲存在相同檔案名稱，從 blob 儲存體位置的 hello *rentalloc001.csv*太*rentalloc10.csv*.</span><span class="sxs-lookup"><span data-stu-id="a0408-126">Let's assume we have collected training datasets from all bike rental locations and stored them in hello same blob storage location with file names ranging from *rentalloc001.csv* too*rentalloc10.csv*.</span></span>

![image](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="a0408-128">請注意， **Web 服務輸出**加入模組 toohello**定型模型**模組。</span><span class="sxs-lookup"><span data-stu-id="a0408-128">Note that a **Web Service Output** module has been added toohello **Train Model** module.</span></span>
<span data-ttu-id="a0408-129">此實驗為 web 服務部署時，該輸出相關聯的 hello 端點會傳回 hello 定型的模型 hello.ilearner 檔案格式。</span><span class="sxs-lookup"><span data-stu-id="a0408-129">When this experiment is deployed as a web service, hello endpoint associated with that output will return hello trained model in hello format of a .ilearner file.</span></span>

<span data-ttu-id="a0408-130">也請注意，我們設定 web 服務參數 hello url 該 hello**匯入資料**模組使用。</span><span class="sxs-lookup"><span data-stu-id="a0408-130">Also note that we set up a web service parameter for hello URL that hello **Import Data** module uses.</span></span> <span data-ttu-id="a0408-131">這可讓我們 toouse hello 參數 toospecify 個別訓練資料集 tootrain hello 模型的每個位置。</span><span class="sxs-lookup"><span data-stu-id="a0408-131">This allows us toouse hello parameter toospecify individual training datasets tootrain hello model for each location.</span></span>
<span data-ttu-id="a0408-132">我們無法完成，例如 SQL 查詢中使用 web 服務參數 tooget 」 資料，從 SQL Azure 資料庫，或只使用其他方法**Web 服務輸出**中資料集 toohello 模組 toopass web 服務。</span><span class="sxs-lookup"><span data-stu-id="a0408-132">There are other ways we could have done this, such as using a SQL query with a web service parameter tooget data from a SQL Azure database, or simply using a  **Web Service Input** module toopass in a dataset toohello web service.</span></span>

![image](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="a0408-134">現在，我們先執行此使用 hello 預設值的定型實驗*rental001.csv*為 hello 定型資料集。</span><span class="sxs-lookup"><span data-stu-id="a0408-134">Now, let's run this training experiment using hello default value *rental001.csv* as hello training dataset.</span></span> <span data-ttu-id="a0408-135">如果檢視的 hello hello 輸出**評估**模組 (按一下 hello 輸出，然後選取**視覺化**)，您可以看到我們取得的不錯效能*AUC* = 0.91。</span><span class="sxs-lookup"><span data-stu-id="a0408-135">If you view hello output of hello **Evaluate** module (click hello output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="a0408-136">此時，我們準備 toodeploy 超出本訓練實驗的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="a0408-136">At this point, we're ready toodeploy a web service out of this training experiment.</span></span>

## <a name="deploy-hello-training-and-scoring-web-services"></a><span data-ttu-id="a0408-137">部署 hello 定型和計分 web 服務</span><span class="sxs-lookup"><span data-stu-id="a0408-137">Deploy hello training and scoring web services</span></span>
<span data-ttu-id="a0408-138">toodeploy hello 定型 web 服務，按一下 hello**設定 Web 服務**hello 實驗畫布下方的按鈕，然後選取**部署 Web 服務**。</span><span class="sxs-lookup"><span data-stu-id="a0408-138">toodeploy hello training web service, click hello **Set Up Web Service** button below hello experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="a0408-139">將此 Web 服務命名為「自行車出租訓練」。</span><span class="sxs-lookup"><span data-stu-id="a0408-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="a0408-140">現在我們需要 toodeploy hello 計分的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="a0408-140">Now we need toodeploy hello scoring web service.</span></span>
<span data-ttu-id="a0408-141">toodo，我們可以按一下**設定 Web 服務**下方 hello 畫布，然後選取**預測 Web 服務**。</span><span class="sxs-lookup"><span data-stu-id="a0408-141">toodo this, we can click **Set Up Web Service** below hello canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="a0408-142">這會建立評分實驗。</span><span class="sxs-lookup"><span data-stu-id="a0408-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="a0408-143">我們需要 toomake 一些細微的調整 toomake 運作為 web 服務，例如移除 hello 標籤資料行 」 cnt"hello 從輸入資料，以及預測值的限制 hello 輸出 tooonly hello 執行個體識別碼和 hello 對應。</span><span class="sxs-lookup"><span data-stu-id="a0408-143">We'll need toomake a few minor adjustments toomake it work as a web service, such as removing hello label column "cnt" from hello input data and limiting hello output tooonly hello instance id and hello corresponding predicted value.</span></span>

<span data-ttu-id="a0408-144">toosave 自行運作，您可以只是開啟 hello[預測實驗](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1)hello 已準備的組件庫中。</span><span class="sxs-lookup"><span data-stu-id="a0408-144">toosave yourself that work, you can simply open hello [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in hello Gallery that's already been prepared.</span></span>

<span data-ttu-id="a0408-145">toodeploy hello web 服務，執行 hello 預測實驗中，然後按一下 hello**部署 Web 服務**hello 畫布下方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a0408-145">toodeploy hello web service, run hello predictive experiment, then click hello **Deploy Web Service** button below hello canvas.</span></span> <span data-ttu-id="a0408-146">計分"Bike 以租用方式佔用計分 」 web 服務的名稱 hello"。</span><span class="sxs-lookup"><span data-stu-id="a0408-146">Name hello scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="a0408-147">使用 PowerShell 建立 10 個相同的 Web 服務端點</span><span class="sxs-lookup"><span data-stu-id="a0408-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="a0408-148">此 Web 服務隨附一個預設端點。</span><span class="sxs-lookup"><span data-stu-id="a0408-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="a0408-149">但目前尚未有興趣 hello 預設端點，因為無法更新。</span><span class="sxs-lookup"><span data-stu-id="a0408-149">But we're not as interested in hello default endpoint since it can't be updated.</span></span> <span data-ttu-id="a0408-150">我們需要 toodo 是 toocreate 10 其他端點，一個用於每個位置。</span><span class="sxs-lookup"><span data-stu-id="a0408-150">What we need toodo is toocreate 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="a0408-151">我們將利用 PowerShell 來完成這件事。</span><span class="sxs-lookup"><span data-stu-id="a0408-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="a0408-152">首先，設定我們的 PowerShell 環境：</span><span class="sxs-lookup"><span data-stu-id="a0408-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="a0408-153">然後，執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a0408-153">Then, run hello following PowerShell command:</span></span>

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="a0408-154">現在我們建立了 10 個端點，而且它們都包含相同定型的模型定型的 hello *customer001.csv*。</span><span class="sxs-lookup"><span data-stu-id="a0408-154">Now we've created 10 endpoints and they all contain hello same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="a0408-155">您可以在 hello Azure 管理入口網站中檢視它們。</span><span class="sxs-lookup"><span data-stu-id="a0408-155">You can view them in hello Azure Management Portal.</span></span>

![image](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a><span data-ttu-id="a0408-157">更新 hello 端點 toouse 不同的訓練資料集使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0408-157">Update hello endpoints toouse separate training datasets using PowerShell</span></span>
<span data-ttu-id="a0408-158">hello 下一個步驟是 tooupdate hello 端點，其中包含每個客戶個別資料唯一定型的模型。</span><span class="sxs-lookup"><span data-stu-id="a0408-158">hello next step is tooupdate hello endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="a0408-159">但首先我們必須 tooproduce 這些模型從 hello**自行車以租用方式佔用訓練**web 服務。</span><span class="sxs-lookup"><span data-stu-id="a0408-159">But first we need tooproduce these models from hello **Bike Rental Training** web service.</span></span> <span data-ttu-id="a0408-160">讓我們繼續後 toohello**自行車以租用方式佔用訓練**web 服務。</span><span class="sxs-lookup"><span data-stu-id="a0408-160">Let's go back toohello **Bike Rental Training** web service.</span></span> <span data-ttu-id="a0408-161">我們需要 toocall 其 BES 10 次具有端點順序 tooproduce 10 不同模型中的 10 個不同的訓練資料集。</span><span class="sxs-lookup"><span data-stu-id="a0408-161">We need toocall its BES endpoint 10 times with 10 different training datasets in order tooproduce 10 different models.</span></span> <span data-ttu-id="a0408-162">我們將使用 hello **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo 這。</span><span class="sxs-lookup"><span data-stu-id="a0408-162">We'll use hello **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo this.</span></span>

<span data-ttu-id="a0408-163">您也需要 tooprovide 認證到 blob 儲存體帳戶`$configContent`，也就是在 hello 欄位`AccountName`，`AccountKey`和`RelativeLocation`。</span><span class="sxs-lookup"><span data-stu-id="a0408-163">You will also need tooprovide credentials for your blob storage account into `$configContent`, namely, at hello fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="a0408-164">hello`AccountName`可以是您帳戶的名稱，其中 hello 中所見**傳統 Azure 管理入口網站**(*儲存體* 索引標籤)。</span><span class="sxs-lookup"><span data-stu-id="a0408-164">hello `AccountName` can be one of your account names, as seen in hello **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="a0408-165">一旦您按一下 儲存體帳戶，其`AccountKey`即可找到按 hello**管理存取金鑰**按鈕 hello 下和複製 hello*主要存取金鑰*。</span><span class="sxs-lookup"><span data-stu-id="a0408-165">Once you click on a storage account, its `AccountKey` can be found by pressing hello **Manage Access Keys** button at hello bottom and copying hello *Primary Access Key*.</span></span> <span data-ttu-id="a0408-166">hello`RelativeLocation`為 hello 路徑的相對 tooyour 儲存要儲存新的模型。</span><span class="sxs-lookup"><span data-stu-id="a0408-166">hello `RelativeLocation` is hello path relative tooyour storage where a new model will be stored.</span></span> <span data-ttu-id="a0408-167">比方說，hello 路徑`hai/retrain/bike_rental/`hello 名為點 tooa 容器下的指令碼中`hai`，和`/retrain/bike_rental/`子資料夾。</span><span class="sxs-lookup"><span data-stu-id="a0408-167">For instance, hello path `hai/retrain/bike_rental/` in hello script below points tooa container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="a0408-168">目前，您無法建立子資料夾，透過 hello 入口網站 UI，但有[數個 Azure 儲存體總管](../storage/common/storage-explorers.md)可讓您 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="a0408-168">Currently, you cannot create subfolders through hello portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you toodo so.</span></span> <span data-ttu-id="a0408-169">建議您新的容器中建立您的儲存體 toostore hello 新定型的模型 （.ilearner 檔案），如下所示： 您的儲存體頁面上，按一下 hello**新增**hello 底部的按鈕並將其命名`retrain`。</span><span class="sxs-lookup"><span data-stu-id="a0408-169">It is recommended that you create a new container in your storage toostore hello new trained models (.ilearner files) as follows: from your storage page, click on hello **Add** button at hello bottom and name it `retrain`.</span></span> <span data-ttu-id="a0408-170">在 [摘要] hello 必要的變更 toohello 下列指令碼太相關`AccountName`，`AccountKey`和`RelativeLocation`(:`"retrain/model' + $seq + '.ilearner"`)。</span><span class="sxs-lookup"><span data-stu-id="a0408-170">In summary, hello necassary changes toohello script below pertain too`AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> <span data-ttu-id="a0408-171">hello BES 端點是 hello 才支援這項作業模式。</span><span class="sxs-lookup"><span data-stu-id="a0408-171">hello BES endpoint is hello only supported mode for this operation.</span></span> <span data-ttu-id="a0408-172">RRS 無法用於產生訓練的模型。</span><span class="sxs-lookup"><span data-stu-id="a0408-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="a0408-173">您可以看到以上版本，而不是建構 10 個不同 BES 工作組態 json 檔案，我們以動態方式改為建立 hello 設定字串，並摘要它 toohello *jobConfigString* hello 參數**InvokeAmlWebServceBESEndpoint** cmdlet，因為沒有真的不需要 tookeep 複本磁碟上。</span><span class="sxs-lookup"><span data-stu-id="a0408-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create hello config string instead and feed it toohello *jobConfigString* parameter of hello **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need tookeep a copy on disk.</span></span>

<span data-ttu-id="a0408-174">如果一切順利，一段時間之後應該會看到 10 個.ilearner 檔案，從*model001.ilearner*太*model010.ilearner*，Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="a0408-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* too*model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="a0408-175">現在我們準備 tooupdate 我們 10 計分 web 服務端點的搭配這些模型使用 hello**修補程式 AmlWebServiceEndpoint** PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a0408-175">Now we're ready tooupdate our 10 scoring web service endpoints with these models using hello **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="a0408-176">請記住，一次，我們只修補 hello 我們以程式設計的方式稍早建立的非預設端點。</span><span class="sxs-lookup"><span data-stu-id="a0408-176">Remember again that we can only patch hello non-default endpoints we programmatically created earlier.</span></span>

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="a0408-177">這應該會非常快速地執行。</span><span class="sxs-lookup"><span data-stu-id="a0408-177">This should run fairly quickly.</span></span> <span data-ttu-id="a0408-178">Hello 執行完成時，我們將已成功建立 10 個預測的 web 服務端點，每一個都會包含唯一定型 hello 資料集特定 tooa 以租用方式佔用位置中，全部從單一定型實驗定型的模型。</span><span class="sxs-lookup"><span data-stu-id="a0408-178">When hello execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on hello dataset specific tooa rental location, all from a single training experiment.</span></span> <span data-ttu-id="a0408-179">tooverify，您可以嘗試呼叫使用 hello 這些端點**InvokeAmlWebServiceRRSEndpoint** cmdlet，讓他們能夠 hello 與相同輸入資料，以及您應該預期 toosee 不同的預測結果，因為 hello 模型使用不同的定型集來定型。</span><span class="sxs-lookup"><span data-stu-id="a0408-179">tooverify this, you can try calling these endpoints using hello **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with hello same input data, and you should expect toosee different prediction results since hello models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="a0408-180">完整 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="a0408-180">Full PowerShell script</span></span>
<span data-ttu-id="a0408-181">以下是 hello hello 完整來源的程式碼清單：</span><span class="sxs-lookup"><span data-stu-id="a0408-181">Here's hello listing of hello full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

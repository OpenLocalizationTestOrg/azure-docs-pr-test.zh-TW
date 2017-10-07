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
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a>使用 PowerShell，從一個實驗中建立許多機器學習服務模型和 Web 服務端點
以下是常見的機器學習問題： 您擁有 hello 的許多模型想 toocreate 同一個訓練工作流程並使用 hello 相同的演算法，但有不同的訓練資料集做為輸入。 本文章將示範如何 toodo 這在 Azure Machine Learning Studio 使用只要單一的實驗中的小數位數。

例如，假設您擁有一家全球性自行車出租加盟商。 您想的 toobuild 迴歸模型 toopredict hello 以租用方式佔用指定根據歷程記錄資料。 您有 1000 以租用方式佔用位置 hello 世界各地，而您已收集到的每個位置，其中包含重要功能，例如日期、 時間、 天氣和是特定 tooeach 位置的流量的資料集。

您可以先培訓模型一次使用 hello 的所有資料集的合併的版本，跨所有位置。 但是因為您的位置中每個唯一的環境，較好的做法是 tootrain 迴歸模型使用的每個位置分別 hello 資料集。 這樣一來，每個已定型的模型無法納入帳戶 hello 不同的存放區大小、 磁碟區、 geography、 母體擴展、 bike 易記流量的環境中，*等*。

可能 hello 最好的方法，但您不想將定型實驗 toocreate 1000 Azure Machine Learning 中的與每一個代表唯一的位置。 除了非常龐大的工作，也是看起來非常沒有效率，因為每個實驗會擁有所有 hello 除了 hello 定型資料集相同的元件。

幸運的是，我們可以完成這項作業使用 hello[重新訓練應用程式開發介面的 Azure Machine Learning](machine-learning-retrain-models-programmatically.md)和自動化 hello 工作[Azure 機器學習 PowerShell](machine-learning-powershell-module.md)。

> [!NOTE]
> toomake 更快速執行我們的範例，我們會減少 hello 1,000 too10 的位置數目。 但 hello 相同的原則和程序適用於 too1，000 的位置。 hello 唯一的差別是如果您想 1000 個資料集 tootrain 您可能想 toothink 執行下列 PowerShell 指令碼，以平行方式 hello。 如何 toodo 超出 hello 範圍的本文中，但您可以找到的範例 PowerShell 多執行緒處理 hello 網際網路上。  
> 
> 

## <a name="set-up-hello-training-experiment"></a>設定 hello 定型實驗
我們會 toouse 範例[定型實驗](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1)，我們已經建立了在 hello [Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。 在 [Azure Machine Learning Studio](https://studio.azureml.net) 工作區開啟此實驗。

> [!NOTE]
> 在此範例中以及 order toofollow，您可能想 toouse 標準的工作區，而不是免費的工作區。 我們將針對每個客戶的總計的 10 個端點-建立一個端點，以及將需要標準的工作區因為免費工作區是有限的 too3 端點。 如果您只需要免費工作區，只需修改 hello tooallow 只有 3 位置底下的指令碼。
> 
> 

hello 實驗使用**匯入資料**模組 tooimport hello 定型資料集*customer001.csv*從 Azure 儲存體帳戶。 假設我們收集從所有自行車以租用方式佔用位置的定型資料集，而且它們儲存在相同檔案名稱，從 blob 儲存體位置的 hello *rentalloc001.csv*太*rentalloc10.csv*.

![image](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

請注意， **Web 服務輸出**加入模組 toohello**定型模型**模組。
此實驗為 web 服務部署時，該輸出相關聯的 hello 端點會傳回 hello 定型的模型 hello.ilearner 檔案格式。

也請注意，我們設定 web 服務參數 hello url 該 hello**匯入資料**模組使用。 這可讓我們 toouse hello 參數 toospecify 個別訓練資料集 tootrain hello 模型的每個位置。
我們無法完成，例如 SQL 查詢中使用 web 服務參數 tooget 」 資料，從 SQL Azure 資料庫，或只使用其他方法**Web 服務輸出**中資料集 toohello 模組 toopass web 服務。

![image](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

現在，我們先執行此使用 hello 預設值的定型實驗*rental001.csv*為 hello 定型資料集。 如果檢視的 hello hello 輸出**評估**模組 (按一下 hello 輸出，然後選取**視覺化**)，您可以看到我們取得的不錯效能*AUC* = 0.91。 此時，我們準備 toodeploy 超出本訓練實驗的 web 服務。

## <a name="deploy-hello-training-and-scoring-web-services"></a>部署 hello 定型和計分 web 服務
toodeploy hello 定型 web 服務，按一下 hello**設定 Web 服務**hello 實驗畫布下方的按鈕，然後選取**部署 Web 服務**。 將此 Web 服務命名為「自行車出租訓練」。

現在我們需要 toodeploy hello 計分的 web 服務。
toodo，我們可以按一下**設定 Web 服務**下方 hello 畫布，然後選取**預測 Web 服務**。 這會建立評分實驗。
我們需要 toomake 一些細微的調整 toomake 運作為 web 服務，例如移除 hello 標籤資料行 」 cnt"hello 從輸入資料，以及預測值的限制 hello 輸出 tooonly hello 執行個體識別碼和 hello 對應。

toosave 自行運作，您可以只是開啟 hello[預測實驗](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1)hello 已準備的組件庫中。

toodeploy hello web 服務，執行 hello 預測實驗中，然後按一下 hello**部署 Web 服務**hello 畫布下方的按鈕。 計分"Bike 以租用方式佔用計分 」 web 服務的名稱 hello"。

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a>使用 PowerShell 建立 10 個相同的 Web 服務端點
此 Web 服務隨附一個預設端點。 但目前尚未有興趣 hello 預設端點，因為無法更新。 我們需要 toodo 是 toocreate 10 其他端點，一個用於每個位置。 我們將利用 PowerShell 來完成這件事。

首先，設定我們的 PowerShell 環境：

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

然後，執行下列 PowerShell 命令的 hello:

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

現在我們建立了 10 個端點，而且它們都包含相同定型的模型定型的 hello *customer001.csv*。 您可以在 hello Azure 管理入口網站中檢視它們。

![image](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a>更新 hello 端點 toouse 不同的訓練資料集使用 PowerShell
hello 下一個步驟是 tooupdate hello 端點，其中包含每個客戶個別資料唯一定型的模型。 但首先我們必須 tooproduce 這些模型從 hello**自行車以租用方式佔用訓練**web 服務。 讓我們繼續後 toohello**自行車以租用方式佔用訓練**web 服務。 我們需要 toocall 其 BES 10 次具有端點順序 tooproduce 10 不同模型中的 10 個不同的訓練資料集。 我們將使用 hello **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo 這。

您也需要 tooprovide 認證到 blob 儲存體帳戶`$configContent`，也就是在 hello 欄位`AccountName`，`AccountKey`和`RelativeLocation`。 hello`AccountName`可以是您帳戶的名稱，其中 hello 中所見**傳統 Azure 管理入口網站**(*儲存體* 索引標籤)。 一旦您按一下 儲存體帳戶，其`AccountKey`即可找到按 hello**管理存取金鑰**按鈕 hello 下和複製 hello*主要存取金鑰*。 hello`RelativeLocation`為 hello 路徑的相對 tooyour 儲存要儲存新的模型。 比方說，hello 路徑`hai/retrain/bike_rental/`hello 名為點 tooa 容器下的指令碼中`hai`，和`/retrain/bike_rental/`子資料夾。 目前，您無法建立子資料夾，透過 hello 入口網站 UI，但有[數個 Azure 儲存體總管](../storage/common/storage-explorers.md)可讓您 toodo 因此。 建議您新的容器中建立您的儲存體 toostore hello 新定型的模型 （.ilearner 檔案），如下所示： 您的儲存體頁面上，按一下 hello**新增**hello 底部的按鈕並將其命名`retrain`。 在 [摘要] hello 必要的變更 toohello 下列指令碼太相關`AccountName`，`AccountKey`和`RelativeLocation`(:`"retrain/model' + $seq + '.ilearner"`)。

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
> hello BES 端點是 hello 才支援這項作業模式。 RRS 無法用於產生訓練的模型。
> 
> 

您可以看到以上版本，而不是建構 10 個不同 BES 工作組態 json 檔案，我們以動態方式改為建立 hello 設定字串，並摘要它 toohello *jobConfigString* hello 參數**InvokeAmlWebServceBESEndpoint** cmdlet，因為沒有真的不需要 tookeep 複本磁碟上。

如果一切順利，一段時間之後應該會看到 10 個.ilearner 檔案，從*model001.ilearner*太*model010.ilearner*，Azure 儲存體帳戶中。 現在我們準備 tooupdate 我們 10 計分 web 服務端點的搭配這些模型使用 hello**修補程式 AmlWebServiceEndpoint** PowerShell cmdlet。 請記住，一次，我們只修補 hello 我們以程式設計的方式稍早建立的非預設端點。

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

這應該會非常快速地執行。 Hello 執行完成時，我們將已成功建立 10 個預測的 web 服務端點，每一個都會包含唯一定型 hello 資料集特定 tooa 以租用方式佔用位置中，全部從單一定型實驗定型的模型。 tooverify，您可以嘗試呼叫使用 hello 這些端點**InvokeAmlWebServiceRRSEndpoint** cmdlet，讓他們能夠 hello 與相同輸入資料，以及您應該預期 toosee 不同的預測結果，因為 hello 模型使用不同的定型集來定型。

## <a name="full-powershell-script"></a>完整 PowerShell 指令碼
以下是 hello hello 完整來源的程式碼清單：

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

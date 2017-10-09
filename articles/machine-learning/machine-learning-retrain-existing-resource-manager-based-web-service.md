---
title: "aaaRetrain 預測的現有 web 服務 |Microsoft 文件"
description: "了解 tooretrain 模型和更新 hello web 服務 toouse hello 新定型的模型在 Azure Machine Learning 中。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a>重新定型現有的預測 Web 服務
本文件說明 hello 重新訓練 hello 遵照案例的程序：

* 您有訓練實驗和預測實驗，您已部署為實際運作的 Web 服務。
* 您有新的資料，您希望您預測的 web 服務 toouse tooperform 其計分。

> [!NOTE] 
> toodeploy 新的 web 服務，您必須擁有足夠的權限 hello 訂用帳戶 toowhich 您部署 hello web 服務。 如需詳細資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。 

從您現有的 web 服務和實驗，您需要 toofollow 下列步驟：

1. 更新 hello 模型。
   1. 修改您的 web 服務輸入及輸出的定型實驗 tooallow。
   2. 訓練的 web 服務來部署 hello 定型實驗。
   3. 使用 hello 定型實驗的批次執行服務 (BES) tooretrain hello 模型。
2. 使用 hello Azure 機器學習 PowerShell cmdlet tooupdate hello 預測實驗。
   1. 登入 tooyour Azure 資源管理員帳戶。
   2. 收到 hello web 服務定義。
   3. 將 hello web 服務定義匯出為 JSON。
   4. 更新 hello JSON 中的 hello 參考 toohello ilearner 做為 blob。
   5. Hello JSON 匯入 web 服務定義。
   6. 使用新的 web 服務定義來更新 hello web 服務。

## <a name="deploy-hello-training-experiment"></a>部署 hello 定型實驗
toodeploy hello 訓練試驗訓練的 web 服務，您必須新增 web 服務輸入及輸出 toohello 模型。 藉由連接*Web 服務輸出*模組 toohello 實驗的*[定型模型][ train-model]* 模組，啟用 hello 定型實驗tooproduce 新定型的模型，您可以使用預測實驗中。 如果您有*評估模型*模組，您也可以附加 web 服務輸出 tooget hello 評估的結果做為輸出。

tooupdate 定型實驗：

1. 連接*Web 服務輸入*模組 tooyour 資料輸入 (例如，*清除遺漏資料*模組)。 您通常會想 tooensure 中處理您的輸入的資料相同的 hello 與原始定型資料的方式。
2. 連接*Web 服務輸出*模組 toohello 輸出您*定型模型*模組。
3. 如果您有*評估模型*模組，而且您想要將 toooutput hello 評估結果，連接*Web 服務輸出*模組 toohello 輸出您*評估模型*模組。

執行您的實驗。

接下來，您必須部署 hello 定型實驗做會產生定型的模型和模型的評估結果為 web 服務。  

在 hello hello 實驗畫布底部，按一下 **設定 Web 服務**，然後選取**部署 Web 服務 [New]**。 hello Azure 機器學習 Web 服務入口網站開啟 toohello**部署 Web 服務**頁面。 輸入您的 Web 服務名稱，選擇付款方案，然後按一下部署 。 您只能使用 hello 批次執行方法來建立定型的模型。

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a>使用 BES 進行重新培訓 hello 模型使用新的資料
此範例中，我們會使用重新訓練應用程式的 C# toocreate hello。 您也可以使用 Python 或 R 的範例程式碼 tooaccomplish 這項工作。

重新訓練應用程式開發介面 toocall hello:

1. 在 Visual Studio 中建立 C# 主控台應用程式：[新增] > [專案] > [Visual C#] > [Windows 傳統桌面] > [主控台應用程式 (.NET Framework)]。
2. 登入 toohello 機器學習 Web 服務入口網站。
3. 按一下您正在使用的 hello web 服務。
4. 按一下 [取用] 。
5. 在 hello 底部 hello**取用** 頁面的 hello**範例程式碼**區段中，按一下**批次**。
6. 複製 hello C# 程式碼範例的批次執行，並將它貼到 hello Program.cs 檔案。 請確定該 hello 命名空間會保持不變。

新增 hello NuGet 封裝 Microsoft.AspNet.WebApi.Client，hello 註解中所指定。 tooadd hello 參考 tooMicrosoft.WindowsAzure.Storage.dll，您可能必須先 tooinstall hello [Azure 儲存體服務的用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage)。

hello 下列螢幕擷取畫面顯示 hello**取用**hello Azure 機器學習 Web 服務入口網站頁面中的。

![取用頁面][1]

### <a name="update-hello-apikey-declaration"></a>更新 hello apikey 宣告
找出 hello **apikey**宣告：

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

在 hello**基本耗用量資訊**區段 hello**取用**頁面上，找出 hello 主索引鍵並將它複製 toohello **apikey**宣告。

### <a name="update-hello-azure-storage-information"></a>更新 hello Azure 儲存體資訊
hello BES 範例程式碼會將檔案從本機磁碟機 (例如，"C:\temp\CensusIpnput.csv 」) tooAzure 儲存體上傳、 加以處理，並將 hello 結果後 tooAzure 儲存體。  

tooupdate hello Azure 儲存體資訊，您必須擷取 hello hello Azure 傳統入口網站，從儲存體帳戶的名稱、 金鑰和容器資訊，然後執行實驗之後, 更新 hello correspondi hello 所產生的儲存體帳戶工作流程應該類似 toohello 下列：

![執行後產生的工作流程][4]ng hello 程式碼中的值。

1. 登入 toohello Azure 傳統入口網站。
2. 在 hello 左側瀏覽資料行中，按一下 **儲存體**。
3. 從儲存體帳戶的 hello 清單中選取一個 toostore hello 重新定型模型。
4. 在 hello hello 頁面底部，按一下**管理存取金鑰**。
5. 複製並儲存 hello**主要存取金鑰**和 hello 關閉對話方塊。
6. 在 hello hello 頁面頂端，按一下**容器**。
7. 選取現有的容器，或建立一個新並儲存 hello 名稱。

找出 hello *StorageAccountName*， *StorageAccountKey*，和*StorageContainerName*宣告和更新您儲存從 hello 傳統入口網站的 hello 值.

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

您也必須確定該 hello 輸入的檔可在您指定在 hello 程式碼中的 hello 位置。

### <a name="specify-hello-output-location"></a>指定 hello 輸出位置
當您在 hello 要求裝載中指定 hello 輸出位置時，hello hello 檔案中指定的副檔名*RelativeLocation*必須指定為`ilearner`。 請參閱下列範例中的 hello:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

hello 以下是範例的輸出重新訓練：![重新訓練輸出][6]

## <a name="evaluate-hello-retraining-results"></a>評估 hello 定型的結果
當您執行 hello 應用程式時，hello 輸出會包括 hello URL 和必要 tooaccess hello 評估結果的共用的存取簽章 token。

您可以看到 hello 重新定型模型的 hello 效能結果，藉由結合 hello *BaseLocation*， *RelativeLocation*，和*SasBlobToken* hello 輸出結果如*output2* （如 hello 上述重新訓練輸出影像所示） 並貼入 hello 瀏覽器網址列中的 hello 完整 URL。  

請檢查 hello 結果 toodetermine 是否 hello 新定型的模型執行現有的指引也足夠 tooreplace hello。

複製 hello *BaseLocation*， *RelativeLocation*，和*SasBlobToken* hello 輸出結果。

## <a name="retrain-hello-web-service"></a>進行重新培訓 hello web 服務
當您重新訓練新的 web 服務時，您會更新 hello 預測 web 服務定義 tooreference hello 新定型的模型。 hello web 服務定義是 hello 定型模型的 hello web 服務的內部表示法，而且不是直接修改。 請確定您會預測實驗和未定型實驗擷取 hello web 服務定義。

## <a name="sign-in-tooazure-resource-manager"></a>登入 tooAzure 資源管理員
您必須先登入 tooyour 從 hello PowerShell 環境中的 Azure 帳戶，使用 hello[新增 AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet。

## <a name="get-hello-web-service-definition-object"></a>取得 hello Web 服務定義物件
接下來，呼叫 hello 取得 hello Web 服務定義物件[Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet。

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello 資源群組名稱的現有 web 服務，在您訂用帳戶中執行不含任何參數 toodisplay hello web 服務的 hello Get AzureRmMlWebService cmdlet。 找出 hello web 服務，然後查看 其 web 服務識別碼。 hello hello 資源群組名稱是 hello 識別碼 hello 第四個元素後方 hello *resourceGroups*項目。 在下列範例的 hello，hello 資源群組名稱會是預設-MachineLearning-SouthCentralUS。

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

或者，toodetermine hello 資源群組名稱的現有 web 服務，請登入 toohello Azure 機器學習 Web 服務入口網站。 選取 hello web 服務。 hello 資源群組名稱是 hello hello web 服務，URL hello 第五個項目後方 hello *resourceGroups*項目。 在下列範例的 hello，hello 資源群組名稱會是預設-MachineLearning-SouthCentralUS。

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a>匯出為 JSON 的 hello Web 服務定義物件
hello 定型的模型 toouse hello toomodify hello 定義新定型模型，您必須先使用 hello[匯出 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport 它 tooa JSON 格式的檔案。

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a>更新 hello 參考 toohello ilearner 做為 blob
在 [hello 資產，找出 hello [定型的模型]，更新 hello *uri* hello 中的值*locationInfo*節點以 hello hello ilearner 做為 blob 的 URI。 hello URI 由產生結合 hello *BaseLocation*和 hello *RelativeLocation* hello BES 訓練呼叫 hello 輸出。

     "asset3": {
        "name": "Retrain Sample [trained model]",
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

## <a name="import-hello-json-into-a-web-service-definition-object"></a>Hello JSON 匯入 Web 服務定義物件
您必須使用 hello[匯入 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello 修改回您可以使用 tooupdate hello predicative 實驗的 Web 服務定義物件的 JSON 檔案。

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a>更新 hello web 服務
最後，使用 hello[更新 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello 預測實驗。

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

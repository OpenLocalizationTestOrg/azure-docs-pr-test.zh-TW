---
title: "aaaRetrain 傳統 web 服務 |Microsoft 文件"
description: "了解 tooprogrammatically 訓練模型和更新 hello web 服務 toouse hello 新定型的模型在 Azure Machine Learning 中的結果。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a>重新訓練傳統 Web 服務
評分端點的 hello 預設 hello 預測您部署的 Web 服務。 預設端點會保留與 hello 的同步處理原始定型和計分實驗，並因此 hello hello 預設端點已定型的模型無法取代。 tooretrain hello web 服務，您必須加入新的端點 toohello web 服務。 

## <a name="prerequisites"></a>必要條件
您必須已設定訓練實驗與預測性實驗，如[以程式設計方式重新訓練機器學習服務模型](machine-learning-retrain-models-programmatically.md)中所示。 

> [!IMPORTANT]
> hello 預測實驗必須部署為傳統機器學習 web 服務。 
> 
> 

如需關於部署 Web 服務的其他資訊，請參閱[部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。

## <a name="add-a-new-endpoint"></a>新增端點
hello 預測您部署的 Web 服務包含預設的計分會保留與 hello 原始定型和計分實驗定型的模型的同步處理的端點。 tooupdate 您 web 服務 toowith 新定型的模型，您必須建立新的計分端點。 

toocreate 新計分端點，則在 hello 可以隨 hello 定型模型的預測 Web 服務：

> [!NOTE]
> 請確定您要加入 hello 端點 toohello 預測的 Web 服務，hello 訓練 Web 服務。 如果您正確部署定型和預測性 Web 服務，您應該會看到列出兩個不同的 Web 服務。 hello 預測 Web 服務應該以"[預測 exp 表示。] 結束。
> 
> 

有三種方式，您可以在其中加入新的結束點 tooa web 服務：

1. 以程式設計方式
2. 使用 hello Microsoft Azure Web 服務的入口網站
3. 使用 hello Azure 傳統入口網站

### <a name="programmatically-add-an-endpoint"></a>以程式設計方式新增端點
您可以加入使用 hello 範例程式碼中提供的計分端點[github 儲存機制](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs)。

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a>使用 hello Microsoft Azure Web 服務入口網站 tooadd 端點
1. 在機器學習 Studio 中，在 hello 左側瀏覽資料行中，按一下 Web 服務。
2. 在 hello hello web 服務儀表板底部，按一下 **管理端點預覽**。
3. 按一下 [新增] 。
4. 輸入的名稱和描述 hello 新端點。 選取 hello 記錄層級，以及是否啟用範例資料。 如需有關記錄的詳細資訊，請參閱 [為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a>使用 Azure 傳統入口網站 tooadd 端點 hello
1. 登入 toohello[傳統 Azure 入口網站](https://manage.windowsazure.com)。
2. 在 hello 左窗格中，按一下  **Machine Learning**。
3. 在 名稱 下，按一下您的工作區，然後按一下Web 服務 。
4. 在 [名稱] 下，按一下 [普查模型 [predictive exp.]] 。
5. 在 hello hello 頁面底部，按一下**加入端點**。 如需有關新增端點的詳細資訊，請參閱 [建立端點](machine-learning-create-endpoint.md)。 

## <a name="update-hello-added-endpoints-trained-model"></a>更新 hello 加入端點的定型的模型
toocomplete hello 訓練程序，您必須更新 hello hello 您加入的新端點的定型的模型。

* 如果您加入 hello 使用 hello 傳統 Azure 入口網站的新端點，您可以按一下 hello 入口網站中的 hello 新端點的名稱，然後 hello **UpdateResource**連結 tooget hello URL，您需要 tooupdate hello 端點的模型。
* 如果您加入 hello 端點使用 hello 範例程式碼，這包括由 hello hello 說明 URL 位置*HelpLocationURL* hello 輸出中的值。

tooretrieve hello 路徑 URL:

1. 複製並貼入您的瀏覽器中的 hello URL。
2. 按一下 hello 更新資源連結。
3. 將複製 hello 後的 hello PATCH 要求的 URL。 例如：
   
     修補程式 URL：https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2

您現在可以使用 hello 定型的模型 tooupdate hello 計分您先前建立的端點。

下列範例程式碼的 hello 為您示範如何 toouse hello *BaseLocation*， *RelativeLocation*， *SasBlobToken*，和修補程式的 URL tooupdate hello 端點。

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

hello *apiKey*和 hello*端點 Url* hello 呼叫可以取得從端點儀表板。

hello 值 hello*名稱*中的參數*資源*應該符合 hello hello 資源名稱儲存已定型的模型在 hello 預測實驗中。 tooget hello 資源名稱：

1. 登入 toohello[傳統 Azure 入口網站](https://manage.windowsazure.com)。
2. 在 hello 左窗格中，按一下  **Machine Learning**。
3. 在 名稱 下，按一下您的工作區，然後按一下Web 服務 。
4. 在 [名稱] 下，按一下 [普查模型 [predictive exp.]] 。
5. 按一下 hello 您加入新的端點。
6. 在 hello 端點儀表板上按一下**更新資源**。
7. 您可以在 hello hello web 服務的更新資源應用程式開發介面文件頁面上，找到 hello**資源名稱**下**可更新資源**。

如果您的 SAS 權杖到期之前更新 hello 端點完成，您必須執行 GET 與 hello Id> tooobtain 新的權杖。

Hello 程式碼已成功執行時，應該啟動 hello 新端點，在大約 30 秒內使用 hello 重新定型模型。

## <a name="summary"></a>摘要
使用 hello 重新訓練應用程式開發介面，您可以更新 hello 定型的模型的預測的 Web 服務，例如啟用案例：

* 定期以新的資料重新定型模型。
* Hello 目標是讓它們重新訓練 hello 模型使用自己的資料模型 toocustomers 的散發。

## <a name="next-steps"></a>後續步驟
[疑難排解在 Azure Machine Learning 傳統的 web 服務的定型 hello](machine-learning-troubleshooting-retraining-models.md)


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
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a>進行重新培訓新的資源管理員基礎 web 服務使用 hello 機器學習服務管理 PowerShell 指令程式
當您重新訓練新的 web 服務時，您會更新 hello 預測 web 服務定義 tooreference hello 新定型的模型。  

## <a name="prerequisites"></a>必要條件
您必須設定訓練實驗與預測性實驗，如[以程式設計方式重新定型機器學習服務模型](machine-learning-retrain-models-programmatically.md)中所示。 

> [!IMPORTANT]
> hello 預測實驗必須部署為 Azure 資源管理員 （新） 基礎機器學習 web 服務。 toodeploy 新的 web 服務，您必須擁有足夠的權限 hello 訂用帳戶 toowhich 您部署 hello web 服務。 如需詳細資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。 

如需關於部署 Web 服務的其他資訊，請參閱[部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。

此程序需要您已安裝 hello Azure 機器學習指令程式。 安裝 hello 機器學習服務 cmdlet 的詳細資訊，請參閱 hello [Azure 機器學習指令程式](https://msdn.microsoft.com/library/azure/mt767952.aspx)MSDN 上的參考。

複製的 hello hello 重新訓練輸出中的下列資訊：

* BaseLocation
* RelativeLocation

hello 您採取的步驟如下：

1. 登入 tooyour Azure 資源管理員帳戶。
2. 取得 hello web 服務定義
3. 匯出為 JSON 的 hello Web 服務定義
4. 更新 hello JSON 中的 hello 參考 toohello ilearner 做為 blob。
5. Hello JSON 匯入 Web 服務定義
6. 使用新的 Web 服務定義更新 hello web 服務

## <a name="sign-in-tooyour-azure-resource-manager-account"></a>登入 tooyour Azure 資源管理員帳戶
您必須先登入從使用 hello hello PowerShell 環境中的 Azure 帳戶 tooyour[新增 AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet。

## <a name="get-hello-web-service-definition"></a>取得 Web 服務定義 hello
接下來，取得 hello Web 服務所呼叫的 hello [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet。 hello Web 服務定義是 hello 定型模型的 hello web 服務的內部表示法，並不是直接修改。 請確定您會預測實驗和未定型實驗擷取 hello Web 服務定義。

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello 資源群組名稱的現有 web 服務，在您訂用帳戶中執行不含任何參數 toodisplay hello web 服務的 hello Get AzureRmMlWebService cmdlet。 找出 hello web 服務，然後查看 [其 web 服務識別碼。 hello hello 資源群組名稱是 hello 識別碼 hello 第四個元素後方 hello *resourceGroups*項目。 在下列範例的 hello，hello 資源群組名稱會是預設-MachineLearning-SouthCentralUS。

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

或者，toodetermine hello 資源群組名稱的現有 web 服務，toohello Microsoft Azure 機器學習 Web 服務入口網站上的記錄檔。 選取 hello web 服務。 hello 資源群組名稱是 hello hello web 服務，URL hello 第五個項目後方 hello *resourceGroups*項目。 在下列範例的 hello，hello 資源群組名稱會是預設-MachineLearning-SouthCentralUS。

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a>匯出為 JSON 的 hello Web 服務定義
toomodify hello 定義 toohello 定型模型 toouse 新 hello 定型的模型，您必須先使用 hello[匯出 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport 它 tooa JSON 格式的檔案。

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a>更新 hello JSON 中的 hello 參考 toohello ilearner 做為 blob。
在 [hello 資產，找出 hello [定型的模型]，更新 hello *uri* hello 中的值*locationInfo*節點以 hello hello ilearner 做為 blob 的 URI。 hello URI 由產生結合 hello *BaseLocation*和 hello *RelativeLocation* hello BES 訓練呼叫 hello 輸出。 這會更新 hello 路徑 tooreference hello 新定型的模型。

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

## <a name="import-hello-json-into-a-web-service-definition"></a>Hello JSON 匯入 Web 服務定義
您必須使用 hello[匯入 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello 修改成 Web 服務定義，您可以使用 tooupdate hello Web 服務定義 JSON 檔案。

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a>使用新的 Web 服務定義更新 hello web 服務
最後，您使用[更新 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web 服務定義。

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a>摘要
您可以使用 hello 機器學習 PowerShell 管理 cmdlet，來更新 hello 定型的模型的預測的 Web 服務，啟用這類的案例：

* 定期以新的資料重新定型模型。
* Hello 目標是讓它們重新訓練 hello 模型使用自己的資料模型 toocustomers 的散發。


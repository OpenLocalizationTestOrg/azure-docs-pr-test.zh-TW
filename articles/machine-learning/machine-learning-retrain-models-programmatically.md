---
title: "aaaRetrain 機器學習模型以程式設計的方式 |Microsoft 文件"
description: "了解 tooprogrammatically 訓練模型和更新 hello web 服務 toouse hello 新定型的模型在 Azure Machine Learning 中的結果。"
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a>以程式設計方式重新定型機器學習服務模型
在本逐步解說中，您將學習如何 tooprogrammatically 重新定型使用 C# 和機器學習批次執行服務的 hello Azure Machine Learning Web 服務。

一旦您已重新定型 hello 模型，hello 遵循逐步解說顯示如何 tooupdate hello 模型在預測 web 服務：

* 如果您部署的 hello 機器學習 Web 服務入口網站中的傳統 web 服務，請參閱[傳統 web 服務進行重新培訓](machine-learning-retrain-a-classic-web-service.md)。 
* 如果您部署新的 web 服務，請參閱[重新定型新的 web 服務使用 hello 機器學習服務管理 cmdlet](machine-learning-retrain-new-web-service-using-powershell.md)。

如需 hello 定型程序的概觀，請參閱[機器學習模型進行重新培訓](machine-learning-retrain-machine-learning-model.md)。

如果您想 toostart 與現有新的 Azure 資源管理員會根據 web 服務，請參閱[重新定型現有預測 web 服務](machine-learning-retrain-existing-resource-manager-based-web-service.md)。

## <a name="create-a-training-experiment"></a>建立訓練實驗
針對此範例中，您將使用 「 範例 5： 定型、 測試評估二元分類的： 成人資料集 」 從 hello Microsoft Azure Machine Learning 的範例。 

toocreate hello 實驗：

1. 登入 tooMicrosoft Azure Machine Learning Studio。 
2. 在 hello 底部 hello 儀表板的右下角，按一下 **新增**。
3. 從 hello Microsoft 範例中，選取 範例 5。
4. toorename hello 實驗中的，在 hello 頂端 hello 實驗畫布範圍，請選取 hello 實驗名稱 」 範例 5： 定型、 測試評估二元分類的： 成人資料集 」。
5. 輸入「普查模型」。
6. 在 hello hello 實驗畫布底部，按一下 **執行**。
7. 按一下 [設定 Web 服務]，然後選取 [重新訓練 Web 服務]。 

hello 下列範例示範 hello 初始實驗。
   
   ![初始實驗。][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a>建立預測性實驗並發佈為 Web 服務
接下來，您要建立預測性實驗。

1. 在 hello hello 實驗畫布底部，按一下 **設定 Web 服務**選取**預測 Web 服務**。 這樣會將 hello 模型儲存為定型的模型，並將 web 服務輸入和輸出模組。 
2. 按一下 **[執行]**。 
3. Hello 實驗執行完成之後，請按一下**部署 Web 服務 [傳統]**或**部署 Web 服務 [New]**。

> [!NOTE] 
> toodeploy 新的 web 服務，您必須擁有足夠的權限 hello 訂用帳戶 toowhich 您部署 hello web 服務。 如需詳細資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a>部署為定型 web 服務的 hello 定型實驗
tooretrain hello 定型的模型，您必須部署您建立為 Retraining web 服務的 hello 定型實驗。 此 web 服務需要*Web 服務輸出*模組連接 toohello *[定型模型][ train-model]* 模組、 新 toobe 無法 tooproduce定型的模型。

1. tooreturn toohello 定型實驗中，按一下 hello 左窗格中的 hello 實驗圖示，然後按一下 hello 實驗名為 「 人口普查 」 模型。  
2. 在 hello 搜尋實驗項目搜尋方塊中，輸入 web 服務。 
3. 拖曳*Web 服務輸出*模組 hello 到實驗畫布，並連接其輸出 toohello*清除遺漏資料*模組。  這可確保您訓練的資料會處理相同的 hello 與原始定型資料的方式。
4. 拖放兩*web 服務輸出*模組 hello 到實驗畫布。 Hello hello 輸出連接*定型模型*模組 tooone 和 hello 輸出 hello*評估模型*模組 toohello 其他。 hello web 服務輸出**定型模型**為我們提供 hello 新定型的模型。 hello 輸出太附加**評估模型**傳回該模組的輸出，也就是 hello 效能結果。
5. 按一下 **[執行]**。 

接下來您必須部署 hello 定型實驗做會產生定型的模型和模型的評估結果為 web 服務。 tooaccomplish 您下一步的動作集，這是取決於您使用與傳統 web 服務或新的 web 服務。  

**傳統 Web 服務**

在 hello hello 實驗畫布底部，按一下 **設定 Web 服務**選取**部署 Web 服務 [傳統]**。 Web 服務的 hello**儀表板**hello API 金鑰與 hello API 說明頁面會顯示批次執行。 Hello 批次執行方法可用來建立定型模型。

**新式 Web 服務**

在 hello hello 實驗畫布底部，按一下 **設定 Web 服務**選取**部署 Web 服務 [New]**。 hello Web 服務 Azure 機器學習 Web 服務入口網站開啟 toohello 部署 web 服務頁面。 輸入您 Web 服務的名稱，選擇付款方案，然後按一下 [部署]。 Hello 批次執行方法可以用來建立定型的模型

在任一情況下，實驗具有已完成的執行之後 hello 產生工作流程看起來應該如下：

![執行後產生的工作流程。][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a>訓練 hello 模型結果與新的資料使用 BES
例如，您使用重新訓練應用程式的 C# toocreate hello。 您也可以使用 hello Python 或 R 範例程式碼 tooaccomplish 這項工作。

toocall hello 重新訓練應用程式開發介面：

1. 在 Visual Studio 中建立 C# 主控台應用程式：[新增] > [專案] > [Visual C#] > [Windows 傳統桌面] > [主控台應用程式 (.NET Framework)]。
2. 登入 toohello Machine Learning Web 服務入口網站。
3. 如果您使用傳統 Web 服務，按一下 [傳統 Web 服務]。
   1. 按一下您要使用的 hello web 服務。
   2. 按一下 hello 預設端點。
   3. 按一下 [取用] 。
   4. 在 hello 底部 hello**取用** 頁面的 hello**範例程式碼**區段中，按一下**批次**。
   5. 繼續此程序的 toostep 5。
4. 如果您是使用新式 Web 服務，請按一下 [Web 服務]。
   1. 按一下您要使用的 hello web 服務。
   2. 按一下 [取用] 。
   3. 在 hello 底部 hello 取用的頁面上，於 hello**範例程式碼**區段中，按一下**批次**。
5. 複製 hello C# 程式碼範例的批次執行，並將它貼到 hello Program.cs 檔案中，確定 hello 命名空間會保持不變。

新增 hello Nuget 封裝 Microsoft.AspNet.WebApi.Client hello 註解中所指定。 tooadd hello 參考 tooMicrosoft.WindowsAzure.Storage.dll，您需要 tooinstall hello 用戶端程式庫的 Microsoft Azure 儲存體服務。 如需詳細資訊，請參閱 [Windows 儲存體服務](https://www.nuget.org/packages/WindowsAzure.Storage)。

### <a name="update-hello-apikey-declaration"></a>更新 hello apikey 宣告
找出 hello **apikey**宣告。

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

在 hello**基本耗用量資訊**區段 hello**取用**頁面上，找出 hello 主索引鍵並將它複製 toohello **apikey**宣告。

### <a name="update-hello-azure-storage-information"></a>更新 hello Azure 儲存體資訊
hello BES 範例程式碼會將檔案從本機磁碟機 （例如"C:\temp\CensusIpnput.csv 」） tooAzure 儲存體上傳、 加以處理，並將 hello 結果後 tooAzure 儲存體。  

tooaccomplish 這個工作中，您必須擷取 hello 儲存體帳戶名稱、 金鑰和容器資訊從 hello 傳統 Azure 入口網站和對應值 hello 程式碼中的 hello 更新儲存體帳戶。 

1. 登入 toohello 傳統 Azure 入口網站。
2. 在 hello 左側瀏覽資料行中，按一下 **儲存體**。
3. 從儲存體帳戶的 hello 清單中選取一個 toostore hello 重新定型模型。
4. 在 hello hello 頁面底部，按一下**管理存取金鑰**。
5. 複製並儲存 hello**主要存取金鑰**和 hello 關閉對話方塊。 
6. 在 hello hello 頁面頂端，按一下**容器**。
7. 選取現有的容器或建立一個新並儲存 hello 名稱。

找出 hello *StorageAccountName*， *StorageAccountKey*，和*StorageContainerName*宣告和更新您從儲存的 hello 值 hello Azure 入口網站。

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

您也必須確定您指定在 hello 程式碼中的 hello 位置位於可用 hello 輸入的檔。 

### <a name="specify-hello-output-location"></a>指定 hello 輸出位置
當指定 hello 輸出位置中的 hello 要求內容，hello hello 檔案中指定的副檔名*RelativeLocation*必須指定為 ilearner。 

請參閱下列範例中的 hello:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> hello 名稱的輸出位置，可能不同於在本逐步解說是根據您加入 hello web 服務輸出模組中的 hello 順序 hello。 因為您設定具有兩個輸出此定型實驗，hello 結果會包含儲存體位置的這兩種資訊。  
> 
> 

![重新定型輸出][6]

圖 4：重新定型輸出。

## <a name="evaluate-hello-retraining-results"></a>評估 hello 定型的結果
當您執行 hello 應用程式時，hello 輸出包含 hello URL 和 SAS 權杖的必要 tooaccess hello 評估結果。

您可以看到 hello 重新定型模型的 hello 效能結果，藉由結合 hello *BaseLocation*， *RelativeLocation*，和*SasBlobToken* hello 輸出結果如*output2* （如 hello 上述重新訓練輸出影像所示） 並貼上 hello 瀏覽器網址列中的 hello 完整 URL。  

請檢查 hello 結果 toodetermine 是否 hello 新定型的模型執行現有的指引也足夠 tooreplace hello。

複製 hello *BaseLocation*， *RelativeLocation*，和*SasBlobToken*從 hello 輸出結果中，您會使用在 hello 定型程序期間。

## <a name="next-steps"></a>後續步驟
如果您部署 hello 預測 web 服務，依序按一下**部署 Web 服務 [傳統]**，請參閱[傳統 web 服務進行重新培訓](machine-learning-retrain-a-classic-web-service.md)。

如果您部署 hello 預測 web 服務，依序按一下**部署 Web 服務 [New]**，請參閱[重新定型新的 web 服務使用 hello 機器學習服務管理 cmdlet](machine-learning-retrain-new-web-service-using-powershell.md)。

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

---
title: "Azure Machine Learning 中的 aaaALM |Microsoft 文件"
description: "在 Azure Machine Learning Studio 中套用應用程式生命週期管理最佳作法"
keywords: "ALM、AML、Azure ML、應用程式生命週期管理、版本控制"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1be6577d-f2c7-425b-b6b9-d5038e52b395
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: haining
ms.openlocfilehash: 99470ff72fea7ab59d9d44f3fded7b9dd49a38c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-lifecycle-management-in-azure-machine-learning-studio"></a>Azure Machine Learning Studio 中的應用程式生命週期管理
Azure Machine Learning Studio 是開發的是實際運作 hello Azure 雲端平台機器學習實驗的工具。 就像 hello Visual Studio IDE 和可擴充的雲端服務合併到單一平台。 您可以併入標準的應用程式生命週期管理 (ALM) 作法，從版本控制各種資產 tooautomated 執行和部署，Azure Machine Learning Studio。 本文將探討一些 hello 選項和方法。

## <a name="versioning-experiment"></a>版本控制實驗
有兩個建議的方式 tooversion 將實驗。 您可以依賴內建的執行歷程記錄，或匯出以 JavaScript Object Notation (JSON) 格式的 hello 實驗和外部進行管理。 每種方法都有其優缺點。

### <a name="experiment-snapshots-using-run-history"></a>使用執行歷程記錄的實驗快照
Hello 執行模型中的 hello Azure Machine Learning Studio 學習實驗中，每次您按一下 hello**執行**按鈕在 hello 實驗編輯器中的 hello 實驗的不可變的快照集已送出的 toohello 作業排程器。 您可以檢視快照集的這份清單，依序按一下 hello**執行歷程記錄**hello hello 實驗編輯器檢視中的命令列上的按鈕。

![執行歷程記錄按鈕](media/machine-learning-version-control/runhistory.png)

您可以在 hello 時間 hello 實驗 hello 實驗 hello 名稱，即可鎖定模式中的開啟 hello 快照集已送出的 toorun 然後 hello 快照。 請注意，只有 hello hello 清單中，它代表 hello 目前實驗，第一個項目處於可編輯狀態。 也請注意，每個快照也可以有各種狀態，包括「已完成 (部分執行)」、「失敗」、「失敗 (部分執行)」或「草稿」。

![執行歷程記錄清單](media/machine-learning-version-control/runhistorylist.png)

它已開啟之後，您可以將 hello 快照實驗儲存為新的實驗，然後再修改它。 如果您的實驗快照包含資產，例如已定型的模型、 轉換或資料集有更新版本，hello 快照會在 hello 快照時保留 hello 參考 toohello 原始版本。 如果您儲存 hello 鎖定快照集做為新的實驗中，Azure Machine Learning Studio 偵測到較新版本的這些資產，hello 存在且 hello 新實驗中會自動更新。

如果您刪除 hello 實驗時，會刪除所有快照集的這項實驗。

### <a name="exportimport-experiment-in-json-format"></a>以 JSON 格式匯出/匯入實驗
hello 執行歷程記錄快照集保留 hello 實驗不可變版 Azure Machine Learning Studio 中，每次它時送出的 toorun。 您可以也儲存 hello 實驗的本機副本和簽入 tooyour 最愛的原始檔控制系統，例如 Team Foundation Server，並在稍後重新建立實驗從該本機檔案。 您可以使用 hello [Azure 機器學習 PowerShell](http://aka.ms/amlps)指令程式[*匯出 AmlExperimentGraph* ](https://github.com/hning86/azuremlps#export-amlexperimentgraph)和[ *匯入 AmlExperimentGraph* ](https://github.com/hning86/azuremlps#import-amlexperimentgraph) tooaccomplish 的。

hello JSON 檔案是 hello 的文字表示法進行實驗圖形，其中可能包含參考 tooassets hello 工作區，例如資料集或已定型的模型中。 它並未包含 hello 資產的序列化的版本。 如果您嘗試 tooimport hello JSON 文件回 hello 工作區中，參考的 hello 資產必須已經存在與 hello 相同資產 hello 實驗中所參考的識別碼。 否則就無法 tooaccess 匯入的 hello 實驗。

## <a name="versioning-trained-model"></a>定型模型版本控制
定型的模型，Azure Machine Learning 中序列化成已知為.iLearner 檔案格式，並儲存在 hello 與 hello 區相關聯的 Azure Blob 儲存體帳戶。 其中一種方式 tooget hello.iLearner 檔案的複本是透過 hello 重新訓練應用程式開發介面。 [這篇文章](machine-learning-retrain-models-programmatically.md)說明 hello 重新訓練應用程式開發介面的運作方式。 hello 高階步驟：

1. 設定您的訓練實驗。
2. 新增 web 服務輸出連接埠 toohello 定型模型 」 模組或產生 hello 定型的模型，例如微調模型 Hyperparameter 或建立 R 模型的 hello 模組。
3. 執行訓練實驗，然後將它部署為模型訓練 Web 服務。
4. 呼叫 hello BES 端點 hello 訓練 web 服務，並指定 hello.iLearner 所需的檔案名稱和 Blob 儲存體帳戶位置會儲存。
5. 蒐集所產生的 hello.iLearner 檔案後 hello BES 呼叫完成。

另一個方式 tooretrieve hello.iLearner 檔案是透過 hello PowerShell commandlet [*下載 AmlExperimentNodeOutput*](https://github.com/hning86/azuremlps#download-amlexperimentnodeoutput)。 這可能是更容易，如果您只想的 tooget hello.iLearner 一份檔案的情況下 hello 需要 tooretrain hello 模型以程式設計的方式。

Hello.iLearner 檔案包含 hello 定型的模型之後，您可以再運用版本控制策略。 hello 策略可以為套用前/後置依照命名慣例，而只留下 hello.iLearner 檔案在 Blob 儲存體，或複製/匯入至版本控制系統一樣簡單。

hello 儲存的.iLearner 檔案然後可以用於計分透過已部署的 web 服務。

## <a name="versioning-web-service"></a>控制 Web 服務版本
您可以從 Azure Machine Learning 實驗部署兩種類型的 Web 服務。 hello 傳統 web 服務會緊密結合 hello 實驗以及 hello 工作區。 hello 新的 web 服務會使用 hello Azure Resource Manager 架構，並不會再搭配 hello 原始實驗或 hello 工作區。

### <a name="classic-web-service"></a>傳統 Web 服務
tooversion 傳統 web 服務，您可以利用 hello web 服務端點建構。 以下是典型的流程︰

1. 在預測性實驗中部署新的傳統 Web 服務，其中包含預設端點。
2. 您建立新的端點，名為 ep2 上公開 hello 最新版 hello 實驗/定型模型。
3. 返回並更新預測性實驗和定型模型。
4. 您重新部署 hello 預測實驗，然後將更新 hello 預設端點。 但這並不會更改 ep2。
5. 您會建立名為 ep3，公開 hello 新版 hello 實驗和定型的模型的其他端點。
6. 返回 toostep 3 視。

經過一段時間，您可能需要建立多個端點在 hello 相同 web 服務。 每個端點會表示 hello 實驗包含 hello 時間點版本的 hello 定型模型的時間點副本。 然後，您可以使用的外部邏輯 toodetermine 哪些端點 toocall，也就是說，有效地選取 hello 的版本來定型模型 hello 計分的執行。

您可以同時建立許多相同的 web 服務端點，並再修補不同版本的 hello.iLearner 檔案 toohello 端點 tooachieve 類似的效果。 [這篇文章](machine-learning-create-models-and-endpoints-with-powershell.md)詳細說明如何 tooaccomplish 的。

### <a name="new-web-service"></a>新的 Web 服務
如果您建立新的 Azure 資源管理員為基礎的 web 服務時，已無法再使用 hello 端點建構。 相反地，產生 web 服務定義 (WSD) 檔案，以 JSON 格式，從您預測的實驗使用 hello[匯出 AmlWebServiceDefinitionFromExperiment](https://github.com/hning86/azuremlps#export-amlwebservicedefinitionfromexperiment) PowerShell 指令程式，或使用 hello [*匯出 AzureRmMlWebservice* ](https://msdn.microsoft.com/library/azure/mt767935.aspx)從已部署的資源管理員 web 服務的 PowerShell 指令程式。

您有匯出的 hello 之後 WSD 檔案和版本控制，您也可以部署為新的 web 服務 hello WSD，在不同的 Azure 區域中不同的網頁服務計劃中。 請確定您提供 hello 適當的儲存體帳戶設定，以及 hello 新增 web 服務的計畫識別碼。 toopatch 不同.iLearner 檔案中的，您可以修改 hello WSD 檔案並更新 hello 位置參考 hello 定型模型，然後將其部署為新的 web 服務。

## <a name="automate-experiment-execution-and-deployment"></a>自動進行實驗執行和部署
ALM 的重要層面是 toobe 無法 tooautomate hello 執行和的 hello 應用程式的部署程序。 在 Azure Machine Learning 中，您可以完成這項作業使用 hello [PowerShell 模組](http://aka.ms/amlps)。 以下是範例的端對端的步驟相關 tooa 標準 ALM 自動化執行/部署程序使用 hello [Azure Machine Learning Studio PowerShell 模組](http://aka.ms/amlps)。 每個步驟是連結的 tooone 或多個 PowerShell 指令程式，您可以使用 tooaccomplish 步驟。

1. [上傳資料集](https://github.com/hning86/azuremlps#upload-amldataset)。
2. 將定型實驗複製到從 hello 工作區[工作區](https://github.com/hning86/azuremlps#copy-amlexperiment)或從[圖庫](https://github.com/hning86/azuremlps#copy-amlexperimentfromgallery)，或[匯入](https://github.com/hning86/azuremlps#import-amlexperimentgraph)[匯出](https://github.com/hning86/azuremlps#export-amlexperimentgraph)從實驗本機磁碟。
3. [更新的資料集 hello](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) hello 定型實驗中。
4. [執行 hello 定型實驗](https://github.com/hning86/azuremlps#start-amlexperiment)。
5. [升級 hello 定型的模型](https://github.com/hning86/azuremlps#promote-amltrainedmodel)。
6. [複製預測實驗](https://github.com/hning86/azuremlps#copy-amlexperiment)hello 工作區。
7. [更新 hello 定型的模型](https://github.com/hning86/azuremlps#update-amlexperimentuserasset)hello 預測實驗中。
8. [執行 hello 預測實驗](https://github.com/hning86/azuremlps#start-amlexperiment)。
9. [部署 web 服務](https://github.com/hning86/azuremlps#new-amlwebservice)從 hello 預測實驗。
10. 測試 hello web 服務[RR](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint)或[BES](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint)端點。

## <a name="next-steps"></a>後續步驟
* 下載 hello [Azure Machine Learning Studio PowerShell](http://aka.ms/amlps)模組並開始 tooautomate 您 ALM 的工作。
* 了解如何太[建立和管理大量的 ML 模型使用剛才單一實驗](machine-learning-create-models-and-endpoints-with-powershell.md)透過 PowerShell 和重新訓練應用程式開發介面。
* 深入了解如何[部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。

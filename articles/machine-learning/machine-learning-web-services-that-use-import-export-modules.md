---
title: "Azure Machine Learning web 服務中的資料匯入/匯出 aaaUsing |Microsoft 文件"
description: "了解如何 toouse hello 資料匯入及匯出資料的模組 toosend 以及從 web 服務接收資料。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a>部署使用資料匯入和資料匯出模組的 Azure ML Web 服務

當您建立預測性實驗時，通常會新增 Web 服務輸入和輸出。 當您部署的 hello 實驗時，取用者可以傳送和接收 hello web 服務透過 hello 輸入和輸出的資料。 對於某些應用程式，取用者的資料可能可以從資料摘要獲得，或者資料已經位於外部資料來源 (例如 Azure Blob 儲存體)。 在這些情況下，應用程式就不需要使用 Web 服務的輸入和輸出讀取和寫入資料。 相反地，他們可以使用 hello 資料來源使用資料匯入模組的 hello 批次執行服務 (BES) tooread 資料並寫入 hello 計分結果使用匯出資料模組 tooa 不同的資料位置。

hello 資料匯入和匯出資料模組，可以讀取和寫入 toovarious 資料提供位置，例如透過 HTTP、 Hive 查詢、 Azure SQL database、 Azure 資料表儲存體、 Azure Blob 儲存體，資料摘要的 Web URL 或在內部部署 SQL 資料庫。

本主題使用 hello 」 範例 5： 定型、 測試評估二元分類的： 成人資料集 」 範例，並假設 hello 資料集已載入名為 censusdata Azure SQL 資料表。

## <a name="create-hello-training-experiment"></a>建立 hello 定型實驗
當您開啟 hello 」 範例 5： 定型、 測試評估二元分類的： 成人資料集 」 範例它使用 hello 範例成人人口普查收入二元分類的資料集。 和 hello 畫布中的 hello 實驗看起來類似 toohello 下列映像：

![Hello 實驗初始組態。](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

tooread hello hello Azure SQL 資料表資料：

1. 刪除 hello 資料集的模組。
2. 在 hello 元件搜尋方塊中，輸入 匯入。
3. 從 hello 結果清單中，加入*匯入資料*模組 toohello 實驗畫布。
4. Hello 輸出連接*匯入資料*模組 hello 輸入的 hello*清除遺漏資料*模組。
5. 在 屬性 窗格中，選取  **Azure SQL Database**在 hello**資料來源**下拉式清單。
6. 在 hello**資料庫伺服器名稱**，**資料庫名稱**，**使用者名稱**，和**密碼**欄位中，輸入 hello 適當資訊您的資料庫。
7. 在 hello 資料庫查詢欄位中，輸入下列查詢的 hello。
   
     select [age],
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     from dbo.censusdata;
8. 在 hello hello 實驗畫布底部，按一下 **執行**。

## <a name="create-hello-predictive-experiment"></a>建立 hello 預測實驗
接下來您將設定 hello 預測的實驗，您用來部署您的 web 服務。

1. 在 hello hello 實驗畫布底部，按一下 **設定 Web 服務**選取**預測 Web 服務 [建議]**。
2. 移除 hello *Web 服務輸出*和*Web 服務輸出模組*從 hello 預測實驗。 
3. 在 hello 元件搜尋方塊中，輸入匯出。
4. 從 hello 結果清單中，加入*匯出資料*模組 toohello 實驗畫布。
5. Hello 輸出連接*計分模型*模組 hello 輸入的 hello*匯出資料*模組。 
6. 在 屬性 窗格中，選取  **Azure SQL Database** hello 資料目的地的下拉式清單中。
7. 在 hello**資料庫伺服器名稱**，**資料庫名稱**，**伺服器使用者帳戶名稱**，和**伺服器使用者帳戶密碼**欄位中，輸入hello 適當資料庫的資訊。
8. 在 hello**以逗號分隔的清單儲存的資料行 toobe**欄位中，輸入計分標籤。
9. 在 [hello**資料的資料表名稱] 欄位**，輸入 dbo。ScoredLabels。 如果 hello 資料表不存在，則會建立執行 hello 實驗或呼叫 hello web 服務時。
10. 在 hello**以逗號分隔的 datatable 資料行清單**欄位中，輸入 ScoredLabels。

當您撰寫應用程式呼叫 hello 最終的 web 服務時，您可能想 toospecify 不同的輸入的查詢或目的地資料表在執行階段。 tooconfigure 這些輸入和輸出，請使用 hello Web 服務參數功能 tooset hello*匯入資料*模組*資料來源*屬性和 hello*匯出資料*模式資料目的地屬性。  如需有關 Web 服務參數的詳細資訊，請參閱 hello [AzureML Web 服務參數項目](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/)hello Cortana 智慧和機器學習部落格上。

hello 匯入查詢 hello 目的地資料表的 tooconfigure hello Web 服務參數：

1. Hello hello 屬性 窗格中*匯入資料*模組中，按一下 hello hello 圖示右上角的 hello**資料庫查詢**欄位，然後選取**設定為 web 服務參數**。
2. Hello hello 屬性 窗格中*匯出資料*模組中，按一下 hello hello 圖示右上角的 hello**資料表名稱**欄位，然後選取**設定為 web 服務參數**。
3. 在 hello 底部 hello*匯出資料*模組屬性] 窗格中 hello **Web 服務參數**區段中，按一下 [查詢資料庫並將它重新命名查詢。
4. 按一下 [資料表名稱] 並將它重新命名為**資料表**。

當您完成之後時，您的經驗看起來應該類似 toohello 下列映像：

![實驗的最終外觀。](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

現在您可以為 web 服務部署 hello 實驗。

## <a name="deploy-hello-web-service"></a>部署 hello web 服務
您可以部署 tooeither 傳統 」 或 「 新增 web 服務。

### <a name="deploy-a-classic-web-service"></a>部署傳統 Web 服務
toodeploy 為傳統的 Web 服務，並建立應用程式 tooconsume 它：

1. 在 hello hello 實驗畫布底部，按一下 [執行]。
2. Hello 執行完成後，按一下**部署 Web 服務**選取**部署 Web 服務 [傳統]**。
3. 在 hello web 服務儀表板，找到您的 API 金鑰。 複製並儲存它 toouse 更新版本。
4. 在 hello**預設端點**資料表中，按一下 hello**批次執行**連結 tooopen hello API 說明頁面。
5. 在 Visual Studio 中建立 C# 主控台應用程式：[新增] > [專案] > [Visual C#] > [Windows 傳統桌面] > [主控台應用程式 (.NET Framework)]。
6. 在 hello API 說明頁面，尋找 hello**範例程式碼**在 hello hello 頁面底部的區段。
7. 複製並貼入 hello C# 範例程式碼 Program.cs 檔案中，然後移除所有參考 toohello blob 儲存體。
8. 更新 hello hello 值*apiKey*變數使用稍早儲存的 hello API 金鑰。
9. 找出 hello 要求宣告和更新 hello 的 Web 服務參數值會傳遞 toohello*匯入資料*和*匯出資料*模組。 在此情況下，您會使用 hello 原始查詢，但定義新的資料表名稱。
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. 執行 hello 應用程式。 

Hello 執行完成時，新的資料表會加入包含 hello 計分結果 toohello 資料庫。

### <a name="deploy-a-new-web-service"></a>部署新的 Web 服務

> [!NOTE] 
> toodeploy 新的 web 服務，您必須擁有足夠的權限 hello 訂用帳戶 toowhich 您部署 hello web 服務。 如需詳細資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。 

toodeploy 做為新的 Web 服務，並建立應用程式 tooconsume 它：

1. 在 hello hello 實驗畫布底部，按一下 **執行**。
2. Hello 執行完成後，按一下**部署 Web 服務**選取**部署 Web 服務 [New]**。
3. Hello 部署實驗頁面上，輸入您的 web 服務的名稱並選取定價方案，然後按一下**部署**。
4. 在 hello**快速入門**頁面上，按一下**取用**。
5. 在 hello**範例程式碼**區段中，按一下**批次**。
6. 在 Visual Studio 中建立 C# 主控台應用程式：[新增] > [專案] > [Visual C#] > [Windows 傳統桌面] > [主控台應用程式 (.NET Framework)]。
7. 複製並貼入您 Program.cs 檔案中的 hello C# 範例程式碼。
8. 更新 hello hello 值*apiKey*變數以 hello**主索引鍵**位於 hello**基本耗用量資訊**> 一節。
9. 找出 hello *scoreRequest*宣告和更新的 Web 服務參數傳遞 toohello hello 值*匯入資料*和*匯出資料*模組。 在此情況下，您會使用 hello 原始查詢，但定義新的資料表名稱。
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. 執行 hello 應用程式。 


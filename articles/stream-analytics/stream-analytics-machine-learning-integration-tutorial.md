---
title: "aaaAzure 資料流分析和機器學習的整合 |Microsoft 文件"
description: "如何 toouse 使用者定義函數和機器學習中資料流分析工作"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a>使用 Azure 串流分析和 Azure Machine Learning 執行情感分析
本文說明如何 tooquickly 設定整合 Azure Machine Learning 的簡單 Azure Stream Analytics 工作。 您使用的機器學習情緒分析模型與 hello Cortana 智慧組件庫 tooanalyze 資料流處理的文字資料，並判斷即時 hello 人氣分數。 使用 hello Cortana 智慧套件，可讓您完成這項工作，而不需擔心 hello 複雜的建置情緒分析模型。

您可以套用您從這類的發行項 tooscenarios 了解：

* 分析串流 Twitter 資料的即時情感。
* 分析客戶與支援人員對談的記錄。
* 評估論壇、部落格和影片的註解。 
* 許多其他即時、預測評分的案例。

在真實世界案例中，您會取得 hello 資料直接從 Twitter 資料流。 toosimplify hello 教學課程中，我們已寫入它，如此 hello 串流分析工作取得推文從 Azure Blob 儲存體中的 CSV 檔案。 您可以建立您自己的 CSV 檔案，或 hello 下列影像所示，您可以使用範例 CSV 檔案：

![CSV 檔案的範例推文](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

您所建立的 hello 串流分析工作套用 hello 情緒分析模型做為使用者定義函數 (UDF) 的 hello 範例文字資料的 hello blob 存放區。 hello 輸出 （hello 情緒分析中的 hello 結果） 都會寫入 toohello 不同的 CSV 檔案中的同一個 blob 存放區。 

hello 下圖示範這項設定。 請注意，如需更真實的案例，可將 Blob 儲存體更換為 Azure 事件中樞輸入內的串流 Twitter 資料。 此外，您可以建置[Microsoft Power BI](https://powerbi.microsoft.com/)即時的視覺效果的 hello 彙總的人氣。    

![串流分析機器學習服務整合概觀](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a>必要條件
開始之前，請確定您擁有 hello 下列：

* 有效的 Azure 訂用帳戶。
* 內附資料的 CSV 檔。 您可以下載從稍早所示的 hello 檔案[GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv)，或者您可以建立您自己的檔案。 本文中，我們假設您使用從 GitHub hello 檔案。

在高層級，在本文中示範 toocomplete hello 工作您不要 hello 遵循：

1. 建立 Azure 儲存體帳戶和 blob 儲存體容器，並上傳 CSV 格式的輸入的檔案 toohello 容器。
3. 從 hello Cortana 智慧組件庫 tooyour Azure Machine Learning 工作區加入情緒分析模型並將部署此模型為 hello Machine Learning 工作區中的 web 服務。
5. 建立順序 toodetermine 人氣中的函式會呼叫此 web 服務的 hello 文字輸入資料流分析工作。
6. 啟動 hello 資料流分析工作，並檢查 hello 輸出。

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a>建立儲存體容器及上傳 hello CSV 輸入的檔
此步驟中，您可以使用任何 CSV 檔案，例如其中一個可從 GitHub hello。

1. 在 hello Azure 入口網站，按一下 **新增** &gt; **儲存體** &gt; **儲存體帳戶**。

   ![建立新的儲存體帳戶](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. 提供的名稱 (`samldemo` hello 範例中)。 hello 名稱可以使用小寫字母和數字，而且它必須是唯一整個 Azure。 

3. 指定現有的資源群組，並指定位置。 我們建議您針對位置，建立在此教學課程使用的所有都 hello 資源都 hello 相同位置。

    ![提供儲存體帳戶詳細資料](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. 在 hello Azure 入口網站，選取 hello 儲存體帳戶。 在 hello 儲存體帳戶刀鋒視窗中，按一下 **容器**，然後按一下  **+&nbsp;容器**toocreate blob 儲存體。

    ![建立 Blob 容器](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. 提供 hello 容器的名稱 (`azuresamldemoblob` hello 範例中)，並確認**存取類型**設定得**Blob**。 完成後，按一下 [ **確定**]。

    ![指定 Blob 容器詳細資料](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. 在 hello**容器**刀鋒視窗中，選取 hello 新的容器，這會開啟該容器的 hello 刀鋒視窗。

7. 按一下 [上傳] 。

    ![容器的 [上傳] 按鈕](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. 在 hello**上傳 blob**刀鋒視窗中，指定您想 toouse，本教學課程中的 hello CSV 檔案。 如**Blob 類型**，選取**區塊 blob**和 set hello 區塊大小 too4 MB，足以讓本教學課程。

    ![上傳 Blob 檔案](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. 按一下 hello**上傳**在 hello hello 刀鋒視窗底部的按鈕。

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a>從 hello Cortana 智慧組件庫加入 hello 情緒分析模型

Hello 範例資料是 blob，您可以啟用 Cortana 智慧組件庫中的 hello 情緒分析模型。

1. 移 toohello[預測情緒分析模型](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1)hello Cortana 智慧組件庫中的頁面。  

2. 按一下 [在 Studio 中開啟]。  
   
   ![串流分析機器學習服務, 開啟 Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. 登入 toogo toohello 工作區。 選取位置。

4. 按一下**執行**hello hello 頁底端。 hello 程序會執行，其約一分鐘。

   ![在 Machine Learning Studio 中執行實驗](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. Hello 程序已順利執行之後，請選取**部署 Web 服務**hello hello 頁底端。

   ![在 Machine Learning Studio 中將實驗部署為 Web 服務](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. hello 情緒分析模型是準備 toouse 的 toovalidate 按一下 hello**測試** 按鈕。 提供文字輸入，例如「我喜歡 Microsoft」。 

   ![在 Machine Learning Studio 中測試實驗](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    如果 hello 測試正常運作，您會看到結果類似 toohello，下列範例：

   ![Machine Learning Studio 中的測試結果](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. 在 hello**應用程式**資料行中，按一下 hello **Excel 2010 或舊版的活頁簿**連結 toodownload Excel 活頁簿。 hello 活頁簿包含 hello API 金鑰和 hello URL，您需要稍後 tooset 向上 hello 資料流分析工作。

    ![串流分析機器學習服務, 快速概覽](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a>建立 hello 機器學習模型會使用資料流分析工作

您現在可以建立從 blob 儲存體中的 hello CSV 檔案中讀取 hello 範例推文資料流分析工作。 

### <a name="create-hello-job"></a>建立 hello 作業

1. 移 toohello [Azure 入口網站](https://portal.azure.com)。  

2. 按一下 [新增] > [物聯網] > [串流分析工作]。 

   ![Azure 入口網站的路徑，以取得 tooa 新的資料流分析工作](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. 名稱 hello 工作`azure-sa-ml-demo`、 指定訂用帳戶、 指定現有的資源群組或建立一個新和選取 hello hello 作業的位置。

   ![指定新串流分析工作的設定](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a>設定 hello 作業輸入
hello 作業從您上傳先前 tooblob 儲存體的 hello CSV 檔案取得其輸入。

1. Hello 工作建立之後下, 之後**作業拓撲**在 hello 作業刀鋒視窗中，按一下 hello**輸入**方塊。  
   
   ![在串流分析工作刀鋒視窗中的 [輸入] 方塊](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. 在 hello**輸入**刀鋒視窗中，按一下  **+ 加**。

   ![[新增] 按鈕，新增輸入的 toohello 資料流分析工作](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. 填寫 hello**新輸入**刀鋒視窗包含下列值：

    * **輸入的別名**： 使用 hello 名稱`datainput`。
    * **來源類型**：選取 [資料流]。
    * **來源**：選取 [Blob 儲存體]。
    * **匯入選項**：選取 [從目前的訂用帳戶使用 Blob 儲存體]。 
    * **儲存體帳戶**。 選取您稍早建立的 hello 儲存體帳戶。
    * **容器**。 選取 hello 您稍早建立的容器 (`azuresamldemoblob`)。
    * **事件序列化格式**。 選取 [CSV]。

    ![新工作輸入的設定](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. 按一下 [建立] 。

### <a name="configure-hello-job-output"></a>設定 hello 作業輸出
相同 blob 儲存體它取得在此對話方塊輸入 hello 作業傳送結果 toohello。 

1. 在下**作業拓撲**在 hello 作業刀鋒視窗中，按一下 hello**輸出**方塊。  
  
   ![建立串流分析作業的新輸出](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. 在 hello**輸出**刀鋒視窗中，按一下**+ 加**，並將輸出結果與 hello 別名`datamloutput`。 

3. 對於 [接收器]，選取 [Blob 儲存體]。 然後在 hello hello 其餘部分的填滿輸出使用的設定 hello 相同的值與您用於輸入 hello blob 儲存體：

    * **儲存體帳戶**。 選取您稍早建立的 hello 儲存體帳戶。
    * **容器**。 選取 hello 您稍早建立的容器 (`azuresamldemoblob`)。
    * **事件序列化格式**。 選取 [CSV]。

   ![新工作輸出的設定](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. 按一下 [建立] 。   


### <a name="add-hello-machine-learning-function"></a>新增 hello 機器學習服務函數 
先前您發行的機器學習模型 tooa web 服務。 在我們的案例中，當執行 hello 資料流分析作業時，會傳送每個範例推文情緒分析 hello 輸入的 toohello web 服務。 hello 機器學習 web 服務傳回的人氣 (`positive`， `neutral`，或`negative`) 與 hello 推文中的正面的機率。 

在本節中的 hello 教學課程，您可以定義 hello 資料流分析作業中的函式。 hello 函式可以是叫用的 toosend 推文 toohello web 服務，並回到 hello 回應。 

1. 請確定您擁有 hello web 服務 URL 和 API 金鑰您稍早在 hello Excel 活頁簿中下載。

2. 傳回 toohello 作業概觀刀鋒視窗。

3. 在 設定 下，選取 函數，然後按一下+ 新增。

   ![新增函式 toohello 資料流分析工作](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. 輸入`sentiment`為 hello 函式別名，並填寫 hello 其餘 hello 刀鋒視窗中使用這些值：

    * **函數類型**：選取 [Azure ML]。
    * **匯入選項**：選取 [從不同的訂用帳戶匯入]。 這可讓您有機會 tooenter hello URL 和金鑰。
    * **URL**: hello web 服務 URL 中的貼。
    * **索引鍵**: hello API 機碼中的貼。
  
    ![新增機器學習服務函數 toohello 資料流分析工作設定](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. 按一下 [建立] 。

### <a name="create-a-query-tootransform-hello-data"></a>建立查詢 tootransform hello 資料

資料流分析會使用宣告式、 以 SQL 為基礎的查詢 tooexamine hello 輸入，並加以處理。 在本節中，您可以建立從輸入讀取每個推文，然後再叫用 hello 機器學習服務函數 tooperform 情緒分析的查詢。 hello 查詢接著會傳送 hello 結果 toohello 輸出，您會定義 （blob 儲存）。

1. 傳回 toohello 作業概觀刀鋒視窗。

2.  在下**作業拓撲**，按一下 hello**查詢**方塊。

    ![建立串流分析工作的查詢](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. 輸入下列查詢的 hello:

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    hello 查詢叫用您稍早建立的 hello 函式 (`sentiment`) 順序 tooperform 情緒分析 」 在 hello 輸入中的每個推文中。 

4. 按一下**儲存**toosave hello 查詢。


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a>啟動 hello 資料流分析工作，並檢查 hello 輸出

您現在可以啟動 hello 資料流分析工作。

### <a name="start-hello-job"></a>啟動 hello 工作
1. 傳回 toohello 作業概觀刀鋒視窗。

2. 按一下**啟動**在 hello hello 刀鋒視窗最上方。

    ![建立串流分析工作的查詢](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. 在 hello**開始工作**，選取**自訂**，然後選取一天前 toowhen 您上傳 CSV 檔案 tooblob 存放裝置 hello。 完成後，按一下 [啟動]。  


### <a name="check-hello-output"></a>核取 hello 輸出
1. 讓的 hello 工作執行直到您看到 hello 中的活動的幾分鐘**監視**方塊。 

2. 如果您通常使用 blob 儲存體 tooexamine hello 內容的工具，請使用該工具 tooexamine hello`azuresamldemoblob`容器。 或者，不要 hello hello Azure 入口網站中所述步驟：

    1. 在 hello 入口網站中，尋找 hello`samldemo`儲存體帳戶，而且 hello 帳戶內找出 hello`azuresamldemoblob`容器。 您看到 hello 容器中的兩個檔案： hello 檔案，其中包含 hello 範例推文和 hello 資料流分析工作所產生的 CSV 檔案。
    2. 產生的 hello 檔案上按一下滑鼠右鍵，然後選取**下載**。 

   ![從 Blob 儲存體下載 CSV 工作輸出](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. 開啟 hello 產生 CSV 檔案。 您會看到類似下列範例中的 hello:  
   
   ![串流分析機器學習服務, CSV 檢視](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a>檢視計量
您也能檢視與 Azure Machine Learning 函數相關的度量。 hello 下列函式相關的度量資訊會顯示在 hello**監視**方塊 hello 作業刀鋒視窗中：

* **函式要求**指出傳送要求 tooa 機器學習 web 服務的 hello 數目。  
* **函式事件**指出 hello hello 要求中的事件數目。 根據預設，每個要求 tooa 機器學習 web 服務包含 too1，000 事件。  


## <a name="next-steps"></a>後續步驟

* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [整合 REST API 與 Machine Learning](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)




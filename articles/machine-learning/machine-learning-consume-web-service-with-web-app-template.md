---
title: "aaaConsume 機器學習 web 服務的 web 應用程式範本 |Microsoft 文件"
description: "在 Azure Marketplace tooconsume 在預測 web 服務，Azure Machine Learning 中使用的 web 應用程式範本。"
keywords: "Web 服務、operationalization、REST API、機器學習服務"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a>使用 Azure Machine Learning Web 服務與 Web 應用程式範本

一次您已開發預測模型並將它部署為 Azure web 服務使用 Machine Learning Studio 中，或使用 R 或 Python 之類的工具，您可以存取 hello 實際運作的模型，使用 REST API。

有數種方式 tooconsume hello REST API 及存取 hello web 服務。 例如，您可以撰寫應用程式，在 C# 中，R，或使用 hello Python 部署 hello web 服務時，為您產生的程式碼範例 (用於 hello[機器學習 Web 服務網站](https://services.azureml.net/quickstart)或 hello web 服務儀表板中Machine Learning Studio)。 您可以使用 hello 範例 Microsoft Excel 活頁簿為您建立在 hello 或相同的時間。

但 hello web 服務是透過 hello hello 中提供的 Web 應用程式範本的最快速且輕鬆的方式 tooaccess [Azure Web 應用程式 Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/)。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a>hello Azure 機器學習 Web 應用程式範本
hello hello Azure Marketplace 中提供的 web 應用程式範本可以建立自訂的 web 應用程式知道您的 web 服務輸入的資料和預期的結果。 您只需要 toodo 是提供 hello web 應用程式存取 tooyour web 服務和資料，並 hello 範本沒有 hello rest。

兩個範本可供使用：

* [Azure ML 要求回應服務 Web 應用程式範本](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [Azure ML 批次執行服務 Web 應用程式範本](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

每個範本會建立範例 ASP.NET 應用程式，您的 web 服務，使用 hello API URI 和金鑰，並將其部署為網站 tooAzure。 hello 要求-回應服務 (RR) 範本會建立 web 應用程式，可讓您 toosend 資料 toohello web 服務 tooget 單一結果的單一資料列。 hello 批次執行服務 (BES) 範本會建立 web 應用程式，可讓您 toosend 多個資料列的資料 tooget 多個結果。

任何程式碼是必要的 toouse 這些範本。 您只需要提供 hello API 金鑰和 URI，並 hello 範本建置 hello 的應用程式。

tooget hello API 金鑰和 web 服務的要求 URI:

1. 在 hello[服務入口網站](https://services.azureml.net/quickstart)，新的 web 服務，按一下  **Web 服務**hello 頂端。 或者，按一下 [傳統 Web 服務] \(對於傳統 Web 服務)。
2. 按一下您想 tooaccess hello web 服務。
3. 傳統 web 服務中，按一下您想要 tooaccess hello 端點。
4. 按一下**取用**hello 頂端。
5. 複製 hello**主要**或**次要金鑰**並將其儲存。
6. 如果您要建立要求-回應服務 (RR) 範本，將複製 hello**要求-回應**URI 並將其儲存。 如果您要建立批次執行服務 (BES) 範本，將複製 hello**批次要求**URI 並將其儲存。


## <a name="how-toouse-hello-request-response-service-rrs-template"></a>如何 toouse hello 要求-回應服務 (RR) 範本
依照這些步驟 toouse hello RR web 應用程式範本，hello 下列圖表所示。

![處理序 toouse RR 網站範本][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. 移 toohello [Azure 入口網站](https://portal.azure.com)，**登入**，按一下 **新增**、 搜尋和選取**Azure ML 要求-回應服務 Web 應用程式**，然後按一下**建立**。 
   
   * 為您的 Web 應用程式提供唯一名稱。 hello hello web 應用程式的 URL 是此名稱，後面接著`.azurewebsites.net.`，例如`http://carprediction.azurewebsites.net.`
   * 選取 hello Azure 訂用帳戶和服務執行您的 web 服務。
   * 按一下 [建立] 。
     
     ![建立 Web 應用程式][image5]

4. 當 Azure 完成部署 hello web 應用程式時，按一下 hello **URL**在 hello 在 Azure 中，web 應用程式設定 頁面，或在網頁瀏覽器中輸入 hello。 例如， `http://carprediction.azurewebsites.net.`
5. 當 hello web 應用程式第一次執行它會要求您提供 hello **API Post URL**和**API 金鑰**。
   輸入您稍早儲存的 hello 值 (**要求 URI**和**API 金鑰**分別)。
     
     按一下 [提交] 。
     
     ![輸入貼文 URI 和 API 金鑰][image6]

6. hello web 應用程式會顯示其**Web 應用程式組態**hello 目前的 web 服務設定 頁面。 這裡您可以進行變更 toohello hello web 應用程式所使用的設定。
   
   > [!NOTE]
   > 變更此處 hello 設定只會變更此 web 應用程式它們。 它不會變更您的 web 服務的 hello 預設設定。 例如，如果您變更 hello**描述**這裡不會變更顯示 hello web 服務儀表板 Machine Learning Studio 中的 hello 描述。
   > 
   > 
   
    當您完成時，按一下**儲存變更**，然後按一下**移 tooHome 頁面**。

7. 從 hello 首頁上，您可以輸入值 toosend tooyour web 服務。 按一下**送出**當您完成時，並將傳回 hello 的結果。

如果您想 tooreturn toohello**組態**頁面上，移 toohello `setting.aspx` hello web 應用程式頁面。 例如：`http://carprediction.azurewebsites.net/setting.aspx.`會提示的 tooenter hello API 金鑰一次-您需要 tooaccess hello 頁面，以及更新 hello 設定。

您可以停止、 重新啟動，或刪除 hello hello 像任何其他 web 應用程式的 Azure 入口網站中的 web 應用程式。 只要執行您可以瀏覽 toohello 家用 web 位址，並輸入新值。

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a>如何 toouse hello 批次執行服務 (BES) 範本
您可以使用 hello BES hello 相同方式為 hello RR 範本，除非建立該 hello web 應用程式中的 web 應用程式範本可讓您 toosubmit 多個資料列和接收多個結果。

批次執行 web 服務的 hello 輸入的值可能來自 Azure 儲存體或本機檔案。hello 結果會儲存在 Azure 儲存體容器。
因此，您將需要 Azure 儲存體容器 toohold hello hello web 應用程式，所傳回的結果，您可能需要 tooget 您輸入的資料準備。

![處理 toouse BES 網站範本][image2]

1. 後續 hello 相同程序 toocreate hello BES 太 web 應用程式與 hello RR 範本時，除了 go[Azure ML 批次執行服務 Web 應用程式範本](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)tooopen hello BES Azure Marketplace 範本，然後按一下**建立 Web 應用程式**.

2. 您想要儲存，hello 結果 toospecify hello web 應用程式首頁上輸入 hello 目的地容器的資訊。 也指定 hello web 應用程式可以從何處取得 hello 輸入的值，在本機檔案或 Azure 儲存體容器。
   按一下 [提交] 。
   
    ![儲存體資訊][image7]

hello web 應用程式將會顯示作業狀態的頁面。
Hello 作業完成時將提供您在 Azure blob 儲存體中的 hello 結果 hello 位置。 您也可以下載 hello 結果 tooa 本機檔案的 hello 選項。

## <a name="for-more-information"></a>取得詳細資訊
深入了解 toolearn...

* 使用 Machine Learning Studio 建立機器學習服務實驗，請參閱 [在 Azure Machine Learning Studio 中建立您的第一個實驗](machine-learning-create-experiment.md)
* 如何 toodeploy 機器學習實驗為 web 服務，請參閱[部署 Azure 機器學習 web 服務](machine-learning-publish-a-machine-learning-web-service.md)
* 其他方式 tooaccess web 服務之後，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png

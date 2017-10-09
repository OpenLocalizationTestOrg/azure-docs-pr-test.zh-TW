---
title: "aaaConnect tooa Machine Learning Web 服務 |Microsoft 文件"
description: "使用 C# 或 Python，連線 tooan Azure 機器學習 Web 服務使用的授權金鑰。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a>連接 tooan Azure Machine Learning Web 服務
hello Azure Machine Learning 開發人員經驗是 Web 服務 API toomake 預測從即時或批次模式的輸入資料。 您使用 Azure Machine Learning Studio toocreate 預測，並部署 Azure 機器學習 Web 服務。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

有關如何 toolearn toocreate 及部署機器學習 Web 服務使用 Machine Learning Studio:

* 如需如何 toocreate 實驗在機器學習 Studio 中，請參閱教學課程[建立第一個實驗](machine-learning-create-experiment.md)。
* 如需詳細資訊，如何 toodeploy Web 服務，請參閱[部署機器學習 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。
* 如需機器學習一般情況下，請瀏覽 hello[機器學習服務文件中心](https://azure.microsoft.com/documentation/services/machine-learning/)。

## <a name="azure-machine-learning-web-service"></a>Azure Machine Learning Web 服務
Hello Azure 機器學習 Web 服務，與外部應用程式與即時的機器學習服務工作流程計分模型進行通訊。 在機器學習 Web 服務呼叫傳回預測結果 tooan 外部應用程式。 toomake 在機器學習 Web 服務呼叫，您將部署預測時，會建立 API 金鑰。 hello 機器學習 Web 服務根據其餘部分，web 程式設計專案常用的架構選項。

Azure Machine Learning 有兩種類型的服務：

* 要求-回應服務 (RR)-低延遲、 高擴充性服務 toohello 無狀態模型建立和部署的 hello Machine Learning Studio 提供的介面。
* 批次執行服務 (BES) – 這是一種非同步的服務，為一批資料記錄進行計分。

如需 Machine Learning Web 服務的詳細資訊，請參閱[部署 Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。

## <a name="get-an-azure-machine-learning-authorization-key"></a>取得 Azure Machine Learning 授權金鑰
當您部署您的經驗時，會產生 API 金鑰 hello Web 服務。 您可以從數個位置擷取 hello 索引鍵。

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a>從 hello Microsoft Azure 機器學習 Web 服務入口網站
登入 toohello [Microsoft Azure 機器學習 Web 服務](https://services.azureml.net)入口網站。

新的機器學習 Web 服務的 tooretrieve hello API 金鑰：

1. 在 hello Azure 機器學習 Web 服務入口網站中，按一下  **Web 服務**hello 上方的功能表。
2. 按一下您想要的 tooretrieve hello 金鑰 hello Web 服務。
3. 在 hello 上方功能表中，按一下 **取用**。
4. 複製並儲存 hello**主索引鍵**。

傳統的機器學習 Web 服務的 tooretrieve hello API 金鑰：

1. 在 hello Azure 機器學習 Web 服務入口網站中，按一下 **傳統 Web 服務**hello 上方的功能表。
2. 按一下您要使用的 hello Web 服務。
3. 按一下您想要的 tooretrieve hello 金鑰 hello 端點。
4. 在 hello 上方功能表中，按一下 **取用**。
5. 複製並儲存 hello**主索引鍵**。

### <a name="classic-web-service"></a>傳統 Web 服務
 您也可以擷取從 Machine Learning Studio 或 hello Azure 傳統入口網站的傳統 Web 服務的索引鍵。

#### <a name="machine-learning-studio"></a>Machine Learning Studio
1. 在機器學習 Studio 中，按一下  **WEB 服務**hello 左側。
2. 按一下某個 Web 服務。 hello **API 金鑰**位於 hello**儀表板** 索引標籤。

#### <a name="azure-classic-portal"></a>Azure 傳統入口網站
1. 按一下**MACHINE LEARNING** hello 左側。
2. 按一下您的 Web 服務所在的 hello 工作區。
3. 按一下 [Web 服務] 。
4. 按一下某個 Web 服務。
5. 按一下某個端點。 hello 「 API 金鑰 」 已關閉在 hello 右下方。

## <a id="connect"></a>Tooa 機器學習 Web 服務連接
您可以連接 tooa 使用任何支援 HTTP 要求和回應的程式設計語言的機器學習 Web 服務。 您可以從機器學習 Web 服務說明頁面檢視 C#、Python 和 R 的範例。

**機器學習服務 API 說明**當您部署 Web 服務時，會建立機器學習服務 API 說明。 請參閱 [Azure 機器學習逐步解說 - 部署 Web 服務](machine-learning-walkthrough-5-publish-web-service.md)。
hello 機器學習 API 說明包含預測 Web 服務的相關詳細資料。

1. 按一下您要使用的 hello Web 服務。
2. 按一下您想要的 tooview hello API 說明頁面的 hello 端點。
3. 在 hello 上方功能表中，按一下 **取用**。
4. 按一下**API 說明頁面**hello 要求-回應] 或 [批次執行端點之下。

**tooview 機器學習 API 說明新的 Web 服務**

在 hello Azure 機器學習 Web 服務入口網站：

1. 按一下**WEB 服務**hello 上方功能表上。
2. 按一下您想要的 tooretrieve hello 金鑰 hello Web 服務。

按一下**取用**tooget hello hello 要求 Reposonse 與 C#、 R 和 Python 中的批次執行服務和範例程式碼的 Uri。

按一下**Swagger API** tooget Swagger 根據文件 hello 應用程式開發介面呼叫 hello 從提供的 Uri。

### <a name="c-sample"></a>C# 範例
tooconnect tooa 機器學習 Web 服務，使用**HttpClient**傳遞 ScoreData。 ScoreData 包含 FeatureVector，代表 hello ScoreData n 維向量的數字的功能。 您 API 金鑰與驗證 toohello 機器學習服務。

tooconnect tooa 機器學習 Web 服務，hello **Microsoft.AspNet.WebApi.Client**必須安裝 NuGet 套件。

**在 Visual Studio 中安裝 Microsoft.AspNet.WebApi.Client NuGet**

1. 發行 hello 下載 UCI 資料集： 成人 2 類別的資料集 Web 服務。
2. 按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。
3. 選擇 [ **Install-package Microsoft.AspNet.WebApi.Client**]。

**toorun hello 程式碼範例**

1. 發行 」 範例 1： 下載 UCI 資料集： 成人 2 類別的資料集 」 實驗、 hello 機器學習範例集合的一部分。
2. 指派 apiKey 與 hello 索引鍵，從 Web 服務。 請參閱前述的 **取得 Azure Machine Learning 授權金鑰** 。
3. 指派 serviceUri 以 hello 要求的 URI。

### <a name="python-sample"></a>Python 範例
tooconnect tooa 機器學習 Web 服務，使用 hello **urllib2**傳遞 ScoreData 程式庫。 ScoreData 包含 FeatureVector，代表 hello ScoreData n 維向量的數字的功能。 您 API 金鑰與驗證 toohello 機器學習服務。

**toorun hello 程式碼範例**

1. 部署 」 範例 1： 下載 UCI 資料集： 成人 2 類別的資料集 」 實驗、 hello 機器學習範例集合的一部分。
2. 指派 apiKey 與 hello 索引鍵，從 Web 服務。 請參閱 hello**取得 Azure Machine Learning 授權金鑰**hello 開頭附近的這篇文章的一節。
3. 指派 serviceUri 以 hello 要求的 URI。


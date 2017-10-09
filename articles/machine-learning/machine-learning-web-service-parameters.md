---
title: "Azure 機器學習 Web 服務參數 aaaUse |Microsoft 文件"
description: "存取 hello web 服務時，如何 toouse Azure 機器學習 Web 服務參數 toomodify hello 您模型的行為。"
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a>使用 Azure Machine Learning Web 服務參數
藉由發行包含可設定參數模組的試驗，來建立 Azure Machine Learning Web 服務。 在某些情況下，您可能想 toochange hello 模組行為 hello web 服務執行時。 *Web 服務參數*toodo 可讓您這項工作。 

常見的範例設定 hello[匯入資料][ reader]模組，因此 hello 的 hello 使用者發行 web 服務存取 hello web 服務時，可以指定不同的資料來源。 設定 hello 或者[匯出資料][ writer]模組，讓您可以指定不同的目的地。 一些其他範例，包括變更 hello 位元數目做 hello[特徵雜湊][ feature-hashing] hello 功能所需的模組或 hello 數[篩選器為基礎特徵選取] [ filter-based-feature-selection]模組。 

您可以設定 Web 服務參數，並使其與實驗中的一個或多個模組參數產生關聯，而且您可以指定它們是必要還是選用參數。 撥打電話 hello web 服務時的 hello web 服務的 hello 使用者然後可以對這些參數提供值。 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a>如何 tooset 並使用 Web 服務參數
您可以按一下 hello 圖示下一個 toohello 參數為模組，然後選取 「 設定做為 web 服務參數 」 定義 Web 服務參數。 這會建立新的 Web 服務參數，並將它連接 toothat 模組參數。 然後，當存取 hello web 服務時，hello 使用者可以指定 hello Web 服務參數的值，套用的 toohello 模組參數。

一旦您定義 Web 服務參數，就是可用 tooany hello 實驗中的其他模組參數。 如果您定義一個模組的參數與關聯的 Web 服務參數，您可以使用該相同的 Web 服務參數，任何其他模組，只要 hello 參數必須要有相同的值類型的 hello 即可。 比方說，如果數字的值為 hello Web 服務參數，然後它可以只用於模組參數所預期的數值。 當 hello 使用者設定 hello Web 服務參數的值時，它將會套用相關聯的 tooall 模組參數。

您可以決定是否 tooprovide 預設值為 hello Web 服務參數。 如果您執行動作，然後 hello 參數是選擇性的 hello hello web 服務的使用者。 如果您沒有提供預設值，然後 hello 使用者時需要的 tooenter 值 hello web 服務存取。

hello hello web 服務的 API 文件包含 hello web 服務使用者的有關如何 toospecify hello Web 服務參數以程式設計方式存取 hello web 服務時。

> [!NOTE]
> hello API 文件中提供傳統 web 服務透過 hello **API 說明頁面**hello web 服務中的連結**儀表板**Machine Learning Studio 中。 hello API 文件中提供新的 web 服務透過 hello [Azure 機器學習 Web 服務](https://services.azureml.net/Quickstart)入口網站上 hello**取用**和**Swagger API**頁面您web 服務。
> 
> 

## <a name="example"></a>範例
例如，假設我們有實驗[匯出資料][ writer]傳送資訊 tooAzure blob 儲存體的模組。 我們會定義名為"Blob 路徑 」 的 Web 服務參數，可讓 hello web 服務使用者 toochange hello 路徑 toohello blob 儲存體存取 hello 服務時。

1. 在機器學習 Studio 中，按一下 hello[匯出資料][ writer]模組 tooselect 它。 其屬性會顯示在 hello 屬性窗格 toohello hello 實驗畫布的權限。
2. 指定 hello 儲存類型：
   
   * 在 **[請指定資料目的地]**底下，選取 [Azure Blob 儲存體]。
   * 在 **[請指定驗證類型]**底下，選取 [帳戶]。
   * 輸入 hello hello Azure blob 儲存體帳戶資訊。 
     <p />
3.按一下向右的 hello hello 圖示 toohello**路徑 tooblob 開頭容器參數**。 它看起來像這樣：
   
   ![Web 服務參數圖示][icon]
   
   選取 [設為 Web 服務參數]。
   
   項目會加入下**Web 服務參數**在 hello 開頭 hello 名稱"路徑 tooblob 容器"hello 屬性 窗格的底部。 這是 hello Web 服務參數，現在已與此相關聯[匯出資料][ writer]模組參數。
4. toorename hello Web 服務參數、 按一下 hello 名稱，輸入 「 Blob 路徑 」，然後按 hello **Enter**索引鍵。 
5. tooprovide hello Web 服務參數，預設值按一下 hello 圖示 toohello 方 hello 名稱、 選取 「 提供預設值 」、 輸入的值 (例如，"container1/output1.csv")，然後按 hello **Enter**索引鍵。
   
   ![Web 服務參數][parameter]
6. 按一下 **[執行]**。 
7. 按一下**部署 Web 服務**選取**部署 Web 服務 [傳統]**或**部署 Web 服務 [New]** toodeploy hello web 服務。

> [!NOTE] 
> toodeploy 新的 web 服務，您必須擁有足夠的權限 hello 訂用帳戶 toowhich 您部署 hello web 服務。 如需詳細資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。 

hello web 服務的 hello 使用者現在可以指定新的目的地 hello[匯出資料][ writer]模組存取 hello web 服務時。

## <a name="more-information"></a>詳細資訊
如需更詳細的範例，請參閱 hello [Web 服務參數](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx)hello 中的項目[機器學習部落格](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx)。

如需有關存取機器學習 web 服務的詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/


---
title: "aaaCommon hello 機器學習建議 API 中的作業 |Microsoft 文件"
description: "Azure ML Recommendation 範例應用程式"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 0220bc17-3315-47d7-84a3-ef490263a343
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: da16767134a1386617e1184e4a4850f1f346e972
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a>建議 API 範例應用程式逐步解說
> [!NOTE]
> 您應該開始使用 hello 建議 API 認知服務，而不此版本。 hello 建議認知服務將會取代此服務，並將那里開發所有 hello 新功能。 它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。
> 深入了解[移轉 toohello 新認知的服務](http://aka.ms/recomigrate)
> 
> 

## <a name="purpose"></a>目的
本文件說明的 hello hello 使用量透過的 Azure 機器學習建議 API[範例應用程式](https://code.msdn.microsoft.com/Recommendations-144df403)。

此應用程式不屬於預期的 tooinclude 完整功能，也不會使用所有 hello 應用程式開發介面。 當您第一次想 tooplay 以 hello Machine Learning 建議服務時，它會示範一些常見的作業 tooperform。 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-toomachine-learning-recommendation-service"></a>簡介 tooMachine 學習建議服務
當您建置 hello 下列資料為基礎的建議模型時，會啟用建議透過 hello Machine Learning 建議服務：

* 您想要的 toorecommend，也就是為類別目錄的 hello 項目儲存機制
* 代表 hello 的項目，每個使用者或工作階段 （這可以取得一段時間，透過資料擷取，不 hello 範例應用程式的一部分） 的使用方式資料

建立建議模型之後，您可以使用它 toopredict 項目，使用者可能感興趣，根據 tooa 組項目 （或單一項目） hello 使用者選取。

tooenable hello 前述案例中，執行中的 hello 下列 hello Machine Learning 建議服務：

* 建立模型： 這是保留 hello 資料 （目錄和使用方式） 和 hello 預測模型的邏輯容器。 每個模型的容器會透過建立時配置的唯一識別碼來識別。 此識別碼稱為 hello 模型識別碼，和大部分的 hello 應用程式開發介面使用它。 
* 上傳 toocatalog： 建立模型容器時，您可以將關聯 tooit 類別目錄。

**請注意**： 建立模型及上傳 tooa 目錄通常就會執行一次 hello 模型的生命週期。

* 上傳使用方式： 這會將使用量資料 toohello 模型容器。
* 建立建議模型： 您擁有足夠的資料之後，您可以建立 hello 推薦模型。 這項作業會使用最上層機器學習演算法 toocreate hello 推薦模型。 每個組建都與唯一識別碼相關聯。 您需要 tookeep 此識別碼的記錄，因為它為某些應用程式開發介面的 hello 功能所需。
* 建立處理序監視器 hello： 建議模型建置是非同步作業，它可以和花幾分鐘 tooseveral 小時，視 hello （類別目錄和使用方式） 的資料數量而定 hello 組建參數。 因此，您需要 toomonitor hello 組建。 建議模型只有在與其相關聯的建置成功完成時才會建立。
* (選擇性) 選擇使用中建議模型建置：只有在模型容器中已建置一個以上的建議模型時，才需要執行此步驟。 指出 hello 作用中的建議模型沒有任何要求 tooget 建議是由 hello 系統 toohello 預設作用中建置自動重新導向。 

**注意**：作用中的建議模型可在實際執行環境中使用，而且它是針對實際執行環境工作負載所建置。 這不同於非作用中建議的模型，其仍會維持在類似測試的環境中 (有時稱為「預備」)。

* 取得建議：具備建議模型之後，您可以針對您選取的單一項目或項目清單觸發建議。 

您通常會在特定期間叫用「取得建議」。 在這段時間，您可以重新導向使用方式資料 toohello Machine Learning 建議系統，這會將此資料 toohello 指定之模型的容器。 當您有足夠的使用方式資料時，您可以建立新的建議模型，其中包含 hello 其他使用量資料。 

## <a name="prerequisites"></a>必要條件
* Visual Studio 2013 或更新版本
* 網際網路存取 
* 訂用帳戶 toohello 建議應用程式開發介面 (https://datamarket.azure.com/dataset/amla/recommendations)。

## <a name="azure-machine-learning-sample-app-solution"></a>Azure Machine Learning 範例 App 方案
此方案包含 hello 來源程式碼、 範例使用方式、 類別目錄檔案和指示詞 toodownload hello 封裝所需的編譯。

## <a name="hello-apis-used"></a>hello 使用的應用程式開發介面
hello 應用程式會使用機器學習建議功能，透過可用的應用程式開發介面的子集。 hello hello 應用程式將示範下列 Api:

* 建立模型： 建立邏輯容器 toohold 資料和建議的模型。 由名稱、 識別模型，而且您無法建立多個模型以 hello 相同的名稱。
* 類別目錄檔案上傳： 使用 tooupload 目錄資料。
* 使用檔案上傳： 使用 tooupload 使用方式資料。
* 觸發建置： 使用 toocreate 推薦模型。
* 監視組建執行： 使用推薦模型建置 toomonitor hello 狀態。
* 選擇建議的內建的模型： 預設會使用 tooindicate 的建議模型 toouse 特定模型的容器。 您有一個以上的建議模型，而且您想的 tooactivate 非作用中建置為 hello 作用中的建議模型時，才需要此步驟。
* 取得建議： 使用 tooretrieve 建議項目，根據 tooa 給定的單一項目或一組項目。 

Hello 應用程式開發介面的完整說明，請參閱 hello Microsoft Azure Marketplace 文件。 

**附註**：一個模型經過一段時間 (非同時) 可以有數個組建。 每個組建建立 hello 與相同或更新類別目錄和其他使用量資料。

## <a name="common-pitfalls"></a>常見陷阱
* 您的使用者名稱和您 Microsoft Azure Marketplace 主要帳戶金鑰 toorun hello 範例應用程式，您會需要 tooprovide。
* Hello 範例應用程式執行連續將會失敗。 hello 應用程式流程包括建立、 上傳、 建立 hello 監視器和從預先定義的模型，取得建議因此，它將無法在連續執行如果您不要變更 hello 引動過程之間的模型名稱。
* Recommendations 可能不會傳回任何資料。 hello 範例應用程式會使用非常小的目錄和使用方式檔案。 因此，從 hello 類別目錄的某些項目會有任何建議的項目。

## <a name="disclaimer"></a>免責聲明
hello 範例應用程式不會在實際執行環境中執行的預定的 toobe。 hello 目錄中提供的 hello 資料太小，而且它將不會提供有意義的推薦模型。 提供示範 hello 資料。 


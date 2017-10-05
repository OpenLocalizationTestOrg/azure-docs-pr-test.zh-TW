---
title: "Machine Learning Recommendations API 中的常見作業 | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 8d8efa93e820f4a745ed93c0f4d13b2438dfa1eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a>建議 API 範例應用程式逐步解說
> [!NOTE]
> 您應該開始使用 Recommendations API 的 Cognitive Service，而不是此版本。 Recommendations 的 Cognitive Service 將會取代這個服務，而所有的新特徵都會在其中進行開發。 它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。
> 深入了解 [移轉到新的 Cognitive Service](http://aka.ms/recomigrate)
> 
> 

## <a name="purpose"></a>目的
本文件透過 [範例應用程式](https://code.msdn.microsoft.com/Recommendations-144df403)說明一些 Azure Machine Learning Recommendations API 的使用方式。

此應用程式並非預期要包含完整的功能，也不會使用所有的 API。 它會示範一些常見的作業，以在您第一次想要試試機器學習服務建議服務時執行。 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-to-machine-learning-recommendation-service"></a>機器學習服務建議服務簡介
當您根據下列資料建立建議模型時，會啟用透過機器學習服務建議服務的 Recommendations：

* 您想要建議的項目的儲存機制，也就是類別目錄
* 代表每一個使用者或工作階段之項目使用的資料 (這可以經由資料擷取取得，不屬於範例應用程式的一部份)

建置建議模型之後，可以使用它來根據使用者選取的一組項目 (或單一項目)，預測使用者可能會有興趣的項目。

若要啟用先前的案例，請在機器學習服務建議服務中執行下列動作：

* 建立模型：這是邏輯容器，會保留資料 (目錄和使用方式) 與預測模型。 每個模型的容器會透過建立時配置的唯一識別碼來識別。 這個識別碼稱為模型識別碼，並且大部分的 API 都會使用它。 
* 上傳至目錄：建立模型容器之後，您即可讓該容器與目錄產生關聯

**附註**：建立模型和上傳至目錄通常會在模型生命週期中執行一次。

* 上傳使用狀況資料：這會將使用狀況資料加入至模型容器。
* 建置建議的模型：您有足夠的資料之後，您可以建置建議模型。 這項作業將使用最高層機器學習演算法來建立建議模型。 每個組建都與唯一識別碼相關聯。 您要保留這個識別碼的記錄，因為它是某些 API 的功能所需。
* 監控建置程序：建議模型建置是一項非同步作業，視資料量 (目錄和使用) 和建置參數而定，所需的時間從數分鐘到數小時。 因此，您必須監視組建。 建議模型只有在與其相關聯的建置成功完成時才會建立。
* (選擇性) 選擇使用中建議模型建置：只有在模型容器中已建置一個以上的建議模型時，才需要執行此步驟。 若未指出使用中建議模型，系統會將任何取得建議的要求自動重新導向至預設的使用中組建。 

**注意**：作用中的建議模型可在實際執行環境中使用，而且它是針對實際執行環境工作負載所建置。 這不同於非作用中建議的模型，其仍會維持在類似測試的環境中 (有時稱為「預備」)。

* 取得建議：具備建議模型之後，您可以針對您選取的單一項目或項目清單觸發建議。 

您通常會在特定期間叫用「取得建議」。 在該段時間，您可以將使用量資料重新導向至機器學習服務建議系統，它會將此資料加入至指定的模型容器。 當您有足夠的使用量資料時，您可以建立新的建議模型，其中包含額外的使用量資料。 

## <a name="prerequisites"></a>必要條件
* Visual Studio 2013 或更新版本
* 網際網路存取 
* Recommendations API 的訂用帳戶 (https://datamarket.azure.com/dataset/amla/recommendations)。

## <a name="azure-machine-learning-sample-app-solution"></a>Azure Machine Learning 範例 App 方案
這個方案包含原始程式碼、範例使用、目錄檔案及指示詞，以下載編譯所需的套件。

## <a name="the-apis-used"></a>使用的 API
應用程式會透過可用 API 的子集使用機器學習服務建議功能。 應用程式中會示範下列 API：

* 建立模型：建立邏輯容器以保存資料和建議模型。 模型是以名稱識別，而您無法建立同名的模型超過一次。
* 上傳目錄檔案：用來上傳目錄資料。
* 上傳使用檔案：用來上傳使用資料。
* 觸發建置：用來建立建議模型。
* 監視組建執行：用來監視建議模型組建的狀態
* 選擇建議的建置模型：用來指出特定模型容器預設要使用的建議模型。 只有在您有一個以上的建議模型，而且想要啟動非使用中組建作為使用中建議時，才需要執行此步驟。
* 取得建議：用來根據指定的單一項目或一組項目擷取建議項目。 

如需 API 的完整描述，請參閱 Microsoft Azure Marketplace 文件。 

**附註**：一個模型經過一段時間 (非同時) 可以有數個組建。 每個組建會使用相同或更新的目錄和其他使用量資料建立。

## <a name="common-pitfalls"></a>常見陷阱
* 您必須提供您的使用者名稱和您的 Microsoft Azure Marketplace 主要帳戶金鑰來執行範例 App。
* 連續執行範例應用程式將會失敗。 應用程式流程可能包括從預先定義之模型建立、上傳、建置監視器及取得建議，因此如果您未在引動之間變更模型名稱，它就無法連續執行。
* Recommendations 可能不會傳回任何資料。 範例應用程式會使用非常小的目錄和使用方式檔案。 因此，類別目錄中的某些項目將不會有任何建議的項目。

## <a name="disclaimer"></a>免責聲明
範例應用程式並非預期在實際執行環境中執行。 目錄中提供的資料太小，而且它將不會提供有意義的建議模型。 提供資料基於示範目的。 


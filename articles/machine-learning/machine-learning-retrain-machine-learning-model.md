---
title: "aaaRetrain 機器學習模型 |Microsoft 文件"
description: "了解 tooretrain 模型和更新 hello Web 服務 toouse hello 新定型的模型在 Azure Machine Learning 中。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a>重新定型機器學習服務模型
Hello 實施的機器學習模型，在 Azure 機器學習程序的一部分，您的模型定型並儲存。 您接著使用它 toocreate predicative 的 Web 服務。 在 web sites、 儀表板和行動裝置應用程式可以使用 hello Web 服務。 

您使用 Machine Learning 建立的模型通常不是靜態。 當新的資料可用時，或 hello hello API 取用者擁有自己資料 hello 模型必須 toobe 重新定型。 

重新定型可能經常會發生。 利用 hello 以程式設計方式重新訓練應用程式開發介面的功能，您可以透過程式設計方式重新訓練 hello hello 重新訓練應用程式開發介面和 update hello Web 服務使用 hello 定型新模型的模型。 

本文件描述 hello 定型程序，並顯示如何 toouse hello 重新訓練應用程式開發介面。

## <a name="why-retrain-defining-hello-problem"></a>為什麼重新訓練： 定義 hello 問題
Hello 機器學習，定型程序的一部分，模型是來定型資料集。 您使用 Machine Learning 建立的模型通常不是靜態。 當新的資料可用時，或 hello hello API 取用者擁有自己資料 hello 模型必須 toobe 重新定型。

在這些情況下，以程式設計方式的應用程式開發介面提供便利的方式 tooallow 您或使用 hello 您應用程式開發介面 toocreate 的用戶端，可以一次或規則為基礎，進行重新培訓 hello 模型使用自己的資料取用者。 它們可以評估 hello 結果重新訓練，並更新 hello Web 服務 API toouse hello 定型新模型。

> [!NOTE]
> 如果您有現有的定型實驗和新的 Web 服務，您可能想 toocheck 出重新定型現有的預測 Web 服務，而不是 hello 之後 > 一節中所述的下列 hello 逐步解說。
> 
> 

## <a name="end-to-end-workflow"></a>端對端工作流程
hello 程序牽涉到下列元件的 hello: 定型實驗和預測實驗發佈為 Web 服務。 tooenable 重新訓練的定型的模型，hello 定型實驗必須發佈為 Web 服務的 hello 輸出定型的模型。 這可讓應用程式開發介面存取 toohello 模型定型。 

hello 步驟適用於 tooboth 新增與傳統 Web 服務：

建立 hello 初始預測 Web 服務：

* 建立訓練實驗
* 建立預測性 Web 實驗
* 部署預測性 Web 服務

進行重新培訓 hello Web 服務：

* 更新定型實驗 tooallow 重新定型
* 部署重新訓練 web 服務的 hello
* 使用 hello 批次執行服務的程式碼 tooretrain hello 模型

Hello 先前步驟的逐步解說，請參閱[重新訓練機器學習模型以程式設計方式](machine-learning-retrain-models-programmatically.md)。

> [!NOTE] 
> toodeploy 新的 web 服務，您必須擁有足夠的權限 hello 訂用帳戶 toowhich 您部署 hello web 服務。 如需詳細資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。 

如果您部署了傳統 Web 服務：

* 建立新的端點上 hello 預測 Web 服務
* 取得 hello 修補程式 URL 和程式碼
* 使用 hello 修補程式的 URL toopoint hello hello 新端點重新定型模型 

Hello 先前步驟的逐步解說，請參閱[傳統 Web 服務進行重新培訓](machine-learning-retrain-a-classic-web-service.md)。

如果您執行重新訓練傳統 Web 服務發生問題，請參閱[疑難排解在 Azure 機器學習傳統 Web 服務的定型 hello](machine-learning-troubleshooting-retraining-models.md)。

如果您部署了新式 Web 服務：

* 登入 tooyour Azure 資源管理員帳戶
* 取得 hello Web 服務定義
* 匯出為 JSON 的 hello Web 服務定義
* 更新 hello 參考 toohello `ilearner` hello JSON 中的 blob
* Hello JSON 匯入 Web 服務定義
* 使用新的 Web 服務定義更新 hello Web 服務

Hello 先前步驟的逐步解說，請參閱[重新定型新的 Web 服務使用 hello 機器學習服務管理 PowerShell 指令程式](machine-learning-retrain-new-web-service-using-powershell.md)。

設定重新訓練傳統 Web 服務的 hello 程序牽涉到 hello 下列步驟：

![重新定型程序概觀][1]

設定定型新的 Web 服務的 hello 程序包含下列步驟的 hello:

![重新定型程序概觀][7]

## <a name="other-resources"></a>其他資源
* [使用 Azure Data Factory 重新定型和更新 Azure Machine Learning 模型](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [使用 PowerShell，從一個實驗中建立許多機器學習服務模型和 Web 服務端點](machine-learning-create-models-and-endpoints-with-powershell.md)
* hello [AML 定型模型使用 Api](https://www.youtube.com/watch?v=wwjglA8xllg)段影片會示範如何 tooretrain 機器學習模型中建立 Azure Machine Learning 使用 hello 重新訓練應用程式開發介面和 PowerShell。

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png


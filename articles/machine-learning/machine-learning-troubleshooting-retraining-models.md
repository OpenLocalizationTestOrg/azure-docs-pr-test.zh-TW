---
title: "aaaTroubleshoot 重新訓練 Azure 機器學習傳統 web 服務 |Microsoft 文件"
description: "識別並更正時都重新 hello 模型訓練 Azure 機器學習 Web 服務的一般問題時發生。"
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a>疑難排解在 Azure 機器學習傳統 Web 服務的定型 hello
## <a name="retraining-overview"></a>重新訓練概觀
當您將預測性實驗部署為評分 Web 服務時，它會是靜態模型。 當新的資料可用時，或 hello hello API 取用者擁有自己的資料，hello 模型需要 toobe 重新定型。 

Hello 重新訓練傳統 Web 服務的程序的完整逐步解說，請參閱[重新訓練機器學習模型以程式設計方式](machine-learning-retrain-models-programmatically.md)。

## <a name="retraining-process"></a>重新訓練程序
當您需要 tooretrain hello Web 服務時，您必須新增某些其他的片段：

* Web 服務，從 hello 訓練試驗部署。 必須要有 hello 實驗**Web 服務輸出**模組附加的 hello toohello 輸出**定型模型**模組。  
  
    ![附加 hello web 服務輸出 toohello 定型模型。][image1]
* 新的端點加入 tooyour 計分 Web 服務。  您可以透過程式設計方式加入 hello 端點使用 hello hello 中參考的範例程式碼進行重新培訓機器學習模型以程式設計方式主題或透過 hello Azure 傳統入口網站。

然後，您可以使用 hello 範例 C# 程式碼從 hello 訓練 Web 服務的 API 說明頁面 tooretrain 模型。 評估 hello 結果並感到滿意它們之後，您會更新計分 hello 您加入的新端點的 web 服務的 hello 定型的模型。

與所有 hello 元件之後，您必須採取 tooretrain hello 模型 hello 主要步驟如下：

1. 呼叫 hello 訓練 Web 服務： hello 呼叫 toohello 批次執行服務 (BES)，不 hello 要求回應服務 (RR)。 您可以在 hello API 說明頁面 toomake hello 呼叫使用 hello 範例 C# 程式碼。 
2. 尋找 hello 的 hello 值*BaseLocation*， *RelativeLocation*，和*SasBlobToken*： 從您呼叫 toohello 訓練 Web hello 輸出中傳回這些值服務。 
   ![顯示 hello 輸出的 hello 重新訓練範例與 hello BaseLocation、 RelativeLocation 和 SasBlobToken 的值。][image6]
3. 更新 hello 加入從 hello 新計分 hello 與 web 服務端點來定型模型： 使用 hello 範例程式碼，提供在 hello 重新訓練機器學習模型以程式設計方式更新 hello 新端點加入新計分模型以 hello toohellohello 訓練 Web 服務從定型的模型。

## <a name="common-obstacles"></a>常見障礙
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a>如果您擁有 hello 更正修補程式的 URL，請核取 toosee
hello 修補程式的 URL，您正在使用必須 hello 與相關聯的 hello 評分端點您新增 toohello 計分 Web 服務。 有數種方式 tooobtain hello 修補程式的 URL:

**選項 1︰程式設計方式**

tooget hello 更正修補程式的 URL:

1. 執行 hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs)範例程式碼。
2. 從 AddEndpoint hello 輸出，找出 hello *HelpLocation*值並複製 hello URL。
   
   ![HelpLocation hello hello addEndpoint 範例輸出中。][image2]
3. Hello URL 貼入瀏覽器 toonavigate tooa 頁面提供 hello Web 服務的說明連結。
4. 按一下 hello**更新資源**連結 tooopen hello 修補程式說明頁面。

**選項 2： 使用 hello Azure 傳統入口網站**

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 開啟 hello 機器學習服務索引標籤。![機器學習服務索引標籤。][image4]
3. 依序按一下工作區名稱和 [Web 服務] 。
4. 按一下 hello 計分您正在使用的 Web 服務。 （如果您未修改 hello hello web 服務的預設名稱，它會結束 [計分 Exp。] 中。）
5. 按一下 [新增端點]。
6. 加入 hello 端點之後，按一下 hello 端點名稱。 然後按一下 **更新資源**tooopen hello 修補說明頁面。

> [!NOTE]
> 如果您已加入而不是 hello 預測 Web 服務的 hello 端點 toohello 訓練 Web 服務，您會收到下列錯誤，當您按一下 hello hello**更新資源**連結： 抱歉，但不是支援這項功能或在此內容中使用。 此 Web 服務有沒有可更新的資源。 我們深感抱歉造成您的不便 hello，努力改善此工作流程。
> 
> 

![新端點的儀表板。][image3]

hello 修補程式說明頁面包含 hello 修補程式的 URL，您必須使用，並提供範例程式碼，您可以使用 toocall 它。

![修補 URL。][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a>請檢查您要更新 hello 正確的計分端點 toosee
* 無法修補 hello 訓練 Web 服務： hello 修補作業必須 hello 計分 Web 服務上執行。
* 無法修補 hello Web 服務上的預設端點： hello 修補作業必須 hello 新計分您加入的 Web 服務端點上執行。

您可以確認哪一個 Web 服務的 hello 端點是在造訪 hello Azure 傳統入口網站。 

> [!NOTE]
> 請確定您要加入 hello 端點 toohello 預測的 Web 服務，hello 訓練 Web 服務。 如果您正確部署定型和預測性 Web 服務，您應該會看到列出兩個不同的 Web 服務。 hello 預測 Web 服務應該以"[預測 exp 表示。] 結束。
> 
> 

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 開啟 hello 機器學習服務索引標籤。![Machine Learning 工作區 UI。][image4]
3. 選取您的工作區。
4. 按一下 [Web 服務] 。
5. 選取您的預測性 Web 服務。
6. 確認新的端點已加入 toohello Web 服務。

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a>檢查您的 web 服務是的 tooensure 處於 hello 正確的地區中的 hello 工作區
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 選取機器學習 hello 功能表。
   ![Machine Learning 區域 UI。][image4]
3. 確認您的工作區的 hello 位置。

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png

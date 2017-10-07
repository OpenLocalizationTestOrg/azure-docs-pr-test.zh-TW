---
title: "aaa(deprecated) 比例測試-Azure 中，差異 |Microsoft 文件"
description: "(已過時) 比例差異測試"
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a>(已過時) 比例差異測試

> [!NOTE]
> 淘汰 hello Microsoft DataMarket 和這個 API 已被取代。 
> 
> 您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。 如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。

兩個比例有統計上的差異嗎？ 假設使用者需要 toocompare 兩個影片 toodetermine 必須有一部電影的明顯更高比例 '喜歡' 當比較 toohello 其他。 使用大型的範例中，可能是 hello 比例 0.50 和 0.51 統計上明顯的差異。 使用一小部分的範例中，有可能無法足夠資料 toodetermine 如果這些比例實際不同。 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

這[web 服務](https://datamarket.azure.com/dataset/aml_labs/prop_test)進行兩個根據使用者輸入 hello 次數和試用 hello 2 比較群組的 hello 總數的比例 hello 差異檢定。 在一個可能的情況下，此 web 服務呼叫從影片比較應用程式，告知 hello 使用者是否 hello 影片的其中一個 '喜歡' 頻率遠高於其他 hello 根據電影分級中。

> 使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。 但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。 只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。 接著可以發行的 toohello Azure Marketplace 和跨使用者和裝置 hello world hello 作者 hello web 服務的任何基礎結構設定與 hello web 服務。
> 
> 

## <a name="consumption-of-web-service"></a>使用 Web 服務
這項服務可接受 4 個引數，並執行比例的假設測試。

hello 輸入引數為：

* Successes1 - 樣本 1 中的成功事件數目。
* Successes2 - 樣本 2 中的成功事件數目。
* Total1 - 樣本 1 的大小。
* Total2 - 樣本 2 的大小。

hello 服務的 hello 輸出是 hello 假設 hello 結果 hello chi-square 統計資料，df，p 值，以及測試，並在範例 1/2 和信賴區間界限內的比例。

> 這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。 
> 
> 

有多種方式來使用 hello 服務，以自動化方式 (範例應用程式是[這裡](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx))。

### <a name="starting-c-code-for-web-service-consumption"></a>啟動 Web 服務使用的 C# 程式碼：
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a>建立 Web 服務
> 這項 Web 服務是使用 Azure Machine Learning 所建立。 如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。 以下是 hello 實驗中的 hello 模組的每個建立 hello web 服務和範例程式碼的 hello 實驗的螢幕擷取畫面。
> 
> 

Azure Machine Learning 中已建立具有兩個[執行 R 指令碼][execute-r-script]模組的新空白實驗。 Hello 第一個模組中 hello 資料結構描述定義，但 hello 第二個模組使用 R tooperform hello 假設測試中的 hello prop.test 命令進行 2 的比例。 

### <a name="experiment-flow"></a>實驗流程：
![實驗流程][2]

#### <a name="module-1"></a>模組 1：
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a>模組 2：
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a>限制
這是一個非常簡單的測試範例，可測試 2 個比例中的差異。 可以從上述的 hello 範例程式碼看出，實作沒有錯誤攔截和 hello 服務承擔所有的 hello 變數是連續。

## <a name="faq"></a>常見問題集
常見問題集 hello web 服務或發行 toohello Azure Marketplace 的耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


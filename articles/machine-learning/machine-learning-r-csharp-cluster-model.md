---
title: "aaa(deprecated) 叢集模型-Azure |Microsoft 文件"
description: "(已過時) 叢集模型"
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a>(已過時) 叢集模型

> [!NOTE]
> 淘汰 hello Microsoft DataMarket 和這個 API 已被取代。 
> 
> 您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。 如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。

我們可以預測的順序 tooreduce hello 電量關閉風險的信用卡簽發者的信用額度 cardholders 行為的群組？ 我們如何可以定義群組的特質特性的員工順序 tooimprove 其工作的效能？ 如何可以醫生分類病人分組根據其疾病 hello 特性？ 基本上，叢集分析可以回答所有這些問題。   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

叢集分析會根據變數的組合，將一組觀察分成兩個或多個互斥的未知群組。 hello 叢集分析的目的是 toodiscover 系統的組織成群組的觀察值，通常是人員或它們的特性，其中 hello 群組的成員共用屬性在一般。 這[服務](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model)使用 hello K-means 方法，一個常用的群集技巧，toocluster 任意資料分組。 此 web 服務會接受 hello 資料並 hello 數目 k 叢集做為輸入，並產生其中的每個觀察值所屬的 hello k 群組 toowhich 預測。 

> 使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。 但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。 只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。 接著可以發行的 toohello Azure Marketplace 和跨使用者和裝置 hello world hello 作者 hello web 服務的任何基礎結構設定與 hello web 服務。  
> 
> 

## <a name="consumption-of-web-service"></a>使用 Web 服務
此 web 服務會將 hello 資料分組的每個資料列的 k 群組和輸出 hello 群組指派一組。 hello web 服務預期 hello 終端使用者 tooinput 資料做為字串，其中會以逗號 （，） 分隔的資料列和資料行以分號 （;） 分隔。 hello web 服務中，必須要有 1 個資料列一次。 範例資料集看起來可能像這樣：

![範例資料][1]

假設此資料 hello 使用者希望 tooseparate 3 互斥分組。 hello 輸入的資料集上方 hello hello 下列資料： 值 ="10 5; 2,18; 1; 6,7; 5; 5,22; 3; 4,12，則為 2; 1,10; 3; 4";k ="3"。 hello 輸出是 hello 資料列的每個 hello 預測的群組成員資格。

> 這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。 
> 
> 

有多種方式來使用 hello 服務，以自動化方式 (範例應用程式是[這裡](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx))。

### <a name="starting-c-code-for-web-service-consumption"></a>啟動 Web 服務使用的 C# 程式碼：
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
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

在 Azure Machine Learning 中，新的空白實驗建立的來源和兩個[執行 R 指令碼][ execute-r-script]模組提取到 hello 工作區。 建立 hello 資料結構描述使用簡單[執行 R 指令碼][execute-r-script]。 然後，hello 資料結構描述已連結的 toohello 叢集模型 > 一節，以重新建立[執行 R 指令碼][execute-r-script]。 在 hello[執行 R 指令碼][ execute-r-script]用於 hello 群集模型，hello web 服務然後會利用 hello"的 k-means"函式，也就是預先建置到 hello[執行 R 指令碼][ execute-r-script] Azure 機器學習服務。    

![實驗流程][3]

#### <a name="module-1"></a>模組 1：
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a>模組 2：
    # Map 1-based optional input ports toovariables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a>限制
這是一個非常簡單的群集 Web 服務範例。 可以從上述的 hello 範例程式碼看出，實作沒有錯誤攔截和 hello 服務承擔一切都是連續的變數 （沒有類別功能允許），當做 hello 服務只有輸入數字值時的這個 web 的 hello 建立 hello服務。 此外，hello 服務目前會處理有限的資料大小，因為 toohello 要求/回應性質 hello web 服務呼叫和 hello hello 模型的事實所適合每次呼叫 hello web 服務。 

## <a name="faq"></a>常見問題集
常見問題集 hello web 服務或發行 toohello Azure Marketplace 的耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


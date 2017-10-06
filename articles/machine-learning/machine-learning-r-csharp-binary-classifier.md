---
title: "aaa(deprecated) 二元分類器-Azure |Microsoft 文件"
description: "(已過時) 二元分類器"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a>(已過時) 二元分類器

> [!NOTE]
> 淘汰 hello Microsoft DataMarket 和這個 API 已被取代。 
> 
> 您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。 如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。

假設您擁有的資料集，並希望 toopredict hello 獨立變數所根據的二進位相依變數。 「羅吉斯迴歸」是適用於此類預測的普遍統計技術。 這裡 hello 相依變數是二進位或二分，而 p hello 與否 hello 特性感興趣的機率。 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

簡單的案例可能是其中研究人員正嘗試 toopredict 潛在學生是否可能 tooaccept 根據的資訊 （GPA 高中、 家庭收入、 內建的狀態，性別） 許可提供 tooa 大學。 hello 預測的結果都接受 hello 許可提供 hello 潛在學生 hello 可能性。 這[web 服務](https://datamarket.azure.com/dataset/aml_labs/log_regression)最適合 hello 羅吉斯迴歸模型 toohello 資料和輸出 hello hello 觀察 hello 資料中的每個機率值 (y)。  

> 使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。 但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。 只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。 接著可以發行的 toohello Azure Marketplace 和跨使用者和裝置 hello world hello 作者 hello web 服務的任何基礎結構設定與 hello web 服務。  
> 
> 

## <a name="consumption-of-web-service"></a>使用 Web 服務
此 web 服務可提供 hello 預測所有 hello 觀察 hello 獨立變數所都根據的 hello 相依變數的值。 hello web 服務預期 hello 終端使用者 tooinput 資料做為字串，其中資料列會以逗號 （，） 分隔，並以分號 （;） 分隔資料行。 hello web 服務需要 1 個資料列一次，並預期 hello 第一個資料行 toobe hello 相依變數。 範例資料集看起來可能像這樣：

![範例資料][1]

沒有相依變數的觀察應輸入 “NA” 做為 y。 hello 資料輸入資料集上方 hello 會 hello 遵循字串:"1; 5; 2,1; 1; 6，0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2，則為 1，NA; 3; 4"。 hello 輸出 hello hello 資料列的每個預測的值根據 hello 獨立變數。 

> 這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。 
> 
> 

有多種方式來使用 hello 服務，以自動化方式 (範例應用程式是[這裡](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx))。

### <a name="starting-c-code-for-web-service-consumption"></a>啟動 Web 服務使用的 C# 程式碼：
    public class Input
    {
           public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
        byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
        return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
        var input = new Input() { value = TextBox1.Text };
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

在 Azure Machine Learning 中，新的空白實驗建立的來源和兩個[執行 R 指令碼][ execute-r-script]模組提取到 hello 工作區。 這項 Web 服務使用基礎 R 指令碼來執行 Azure Machine Learning 實驗。 有 2 組件 toothis 試驗： 結構描述定義，以及定型模型 + 計分。 hello 第一個模組定義 hello 預期結構 hello 輸入資料集，其中 hello 第一個變數是 hello 相依變數，而其餘的 hello 變數無關。 hello 第二個模組非常適合 hello 輸入資料的一般羅吉斯迴歸模型。    

![實驗流程][2]

#### <a name="module-1"></a>模組 1：
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a>模組 2：
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a>限制
這是一個非常簡單的二元分類 Web 服務範例。 可以從上述的 hello 範例程式碼看出，實作沒有錯誤攔截和 hello 服務承擔一切都是連續的二進位檔/變數 （沒有類別功能允許），當做 hello 服務只有輸入數字值時的 hello 建立 helloweb 服務。 此外，hello 服務目前會處理有限的資料大小，因為 toohello 要求/回應性質 hello web 服務呼叫和 hello hello 模型的事實所適合每次呼叫 hello web 服務。 

## <a name="faq"></a>常見問題集
常見問題集 hello web 服務或發行 toohello Azure Marketplace 的耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


---
title: "hello Linux Data Science 虛擬機器上的 aaaData 科學 |Microsoft 文件"
description: "影響 tooperform 幾個常見的資料科學工作以 hello Linux 資料科學 VM。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a>在 hello Linux Data Science 虛擬機器上的資料科學
本逐步解說會示範如何 tooperform 幾個常見的資料科學工作以 hello Linux 資料科學 VM。 hello Linux 資料科學虛擬機器 (DSVM) 是預先安裝工具常用於資料分析和機器學習的集合，在 Azure 上的虛擬機器映像。 hello 索引鍵的軟體元件會分在 hello [Linux Data Science 虛擬機器的佈建 hello](machine-learning-data-science-linux-dsvm-intro.md)主題。 hello VM 映像可讓您輕鬆 tooget 開始執行以分鐘為單位的資料科學，而不需要 tooinstall 並個別設定每個 hello 工具。 您可以輕鬆地向上延展 hello VM，如有需要和它在不使用時停止。 因此，這項資源既有彈性，又符合成本效益。

hello 本逐步解說中所示範的資料科學工作步驟 hello 述 hello[資料科學的小組流程](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)。 這個程序提供系統化的方法 toodata 科學中，可讓資料科學家 tooeffectively 共同作業在 hello 生命週期的建置智慧型應用程式的小組。 hello 資料科學程序也提供可供遵循個人資料科學反覆的架構。

我們分析 hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase)本逐步解說中的資料集。 這是一組電子郵件標示為垃圾郵件或 ham （亦即它們不垃圾郵件），而且也包含 hello 內容 hello 電子郵件的一些統計資料。 包含的 hello 統計資料中會討論 hello 接下來但有一個區段。

## <a name="prerequisites"></a>必要條件
您可以使用 Linux Data Science 虛擬機器之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 如果您還沒有訂用帳戶，請參閱 [立即建立免費的 Azure 帳戶](https://azure.microsoft.com/free/)。
* [**Linux 資料科學 VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm)。 如需此 VM 佈建資訊，請參閱[Linux Data Science 虛擬機器的佈建 hello](machine-learning-data-science-linux-dsvm-intro.md)。
* [X2Go](http://wiki.x2go.org/doku.php) 已安裝在電腦上並已開啟 XFCE 工作階段。 如需安裝和設定 **X2Go 用戶端**的相關資訊，請參閱[安裝和設定 X2Go 用戶端](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client)。 
* **AzureML 帳戶**。 如果您還沒有一個申請新一 hello [AzureML 首頁](https://studio.azureml.net/)。 沒有可用的使用量層 toohelp 您立即開始。

## <a name="download-hello-spambase-dataset"></a>下載 hello spambase 資料集
hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase)資料集是一組較小包含只 4601 範例的資料。 這是 hello 的方便大小 toouse 示範的某些 hello 的主要功能，因為它資料科學 VM 保留 hello 資源需求適度時。

> [!NOTE]
> 本逐步解說建立在 D2 v2 大小的 Linux 資料科學虛擬機器上。 此大小 DSVM 是能夠處理這個逐步解說中的 hello 程序。
>
>

如果您需要更多儲存空間，您可以建立額外的磁碟，並將它們附加 tooyour VM。 這些磁碟使用永續性的 Azure 儲存體，因此其資料時，會保留甚至 hello 伺服器重新佈建到期 tooresizing 或已關閉。 tooadd 磁碟並將它附加 tooyour VM，請依照中的 hello 指示[新增磁碟 tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 這些步驟使用 hello 的 hello DSVM 上已安裝的 Azure 命令列介面 (Azure CLI)。 因此可以完全從 hello VM 本身完成這些程序。 另一個選項 tooincrease 儲存體是 toouse [Azure 檔案](../storage/files/storage-how-to-use-files-linux.md)。

toodownload hello 資料中，開啟終端機視窗，然後執行此命令：

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

hello 下載的檔案沒有標頭資料列，因此讓我們來建立另一個檔案沒有標頭。 Hello 適當的標頭以執行此命令 toocreate 檔案：

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

再進行串連 hello 以及 hello 命令的兩個檔案：

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

hello 資料集上每個電子郵件，有幾種類型的統計資料：

* 資料行要***word\_頻率\_WORD***表示比對的文字在 hello 電子郵件中的 hello 百分比*WORD*。 例如，如果*word\_頻率\_進行*是 1，則在 hello 電子郵件中的所有文字的 1%已*進行*。
* 資料行要***char\_頻率\_CHAR***指出 hello 電子郵件中的所有字元所 hello 百分比*CHAR*。
* ***資本\_執行\_長度\_最長***hello 大寫的字母順序的最長的長度。
* ***資本\_執行\_長度\_平均***是 hello 大寫的字母的所有序列的平均時間長度。
* ***資本\_執行\_長度\_總***是大寫的字母的所有序列 hello 總長度。
* ***垃圾郵件***表示 hello 電子郵件是否被視為垃圾郵件 (1 = 垃圾郵件，0 = 不垃圾郵件)。

## <a name="explore-hello-dataset-with-microsoft-r-open"></a>瀏覽 Microsoft R open hello 資料集
讓我們來檢查 hello 資料並執行以 r hello 資料科學 VM 隨附一些基本的機器學習[Microsoft R Open](https://mran.revolutionanalytics.com/open/)預先安裝。 hello 多執行緒的數學程式庫在這個版本的 R 提供較佳的效能比單一執行緒的各種版本。 Microsoft R Open 也提供重現使用 hello CRAN 封裝儲存機制的快照集。

tooget 副本 hello 程式碼範例使用在這個逐步解說中，複製 hello **Azure-Machine-學習的資料-科學**使用 git，也就預先安裝 hello VM 上的儲存機制。 從 hello git 命令列執行：

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

開啟 終端機視窗，並與 hello R 互動式主控台啟動新的 R 工作階段。

> [!NOTE]
> 您也可以使用 RStudio hello 下列程序。 tooinstall RStudio、 執行此命令在終端機：`./Desktop/DSVM\ tools/installRStudio.sh`
>
>

tooimport hello 資料和設定 hello 環境中，執行：

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

toosee 每個資料行的相關摘要統計資料：

    summary(data)

針對不同的 hello 資料檢視：

    str(data)

這會顯示 hello 每個變數的型別，並先 hello hello 資料集中的幾個值。

hello*垃圾郵件*讀取資料行做為整數，但實際上類別變數 （或係數）。 tooset 其型別：

    data$spam <- as.factor(data$spam)

toodo 一些探勘分析，使用 hello [ggplot2](http://ggplot2.org/)封裝，hello VM 上已安裝的的熱門圖形文件庫。 請注意，從 hello 摘要資料顯示更早版本，我們 hello 頻率 hello 驚嘆號字元有摘要統計資料。 讓我們以下列命令的 hello 繪製這些的頻率：

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

因為 hello 零列會扭曲 hello 繪圖，讓我們來刪除它：

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

在 1 上面有看起來很有意思的不尋常密度。 讓我們只看該資料︰

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

然後按照垃圾郵件和非垃圾郵件進行分割：

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

這些範例應可讓您的 hello toomake 類似繪圖其他資料行 tooexplore hello 它們所包含的資料。

## <a name="train-and-test-an-ml-model"></a>訓練和測試 ML 模型
現在讓我們來定型數個機器學習模型 hello 集中 tooclassify hello 電子郵件做為包含跨越或 ham。 在本節中，我們會訓練決策樹模型和隨機樹系模型，然後測試其預測的精確度。

> [!NOTE]
> hello 資料科學 VM 上已安裝在 hello 下列程式碼中使用的 hello rpart （遞迴資料分割和迴歸樹） 封裝。
>
>

首先，我們將 hello 資料集分割成定型和測試集：

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

然後再建立決策樹 tooclassify hello 電子郵件。

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

以下是 hello 結果：

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

toodetermine 以及它對 hello 訓練設定，請使用下列程式碼的 hello:

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

它對 hello 測試集的 toodetermine 程度：

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

讓我們同時嘗試隨機樹系模型。 隨機樹系訓練的決策樹，並輸出是從所有 hello 個別的決策樹的 hello 分類 hello 模式的類別。 它們提供的功能更強大的機器學習方法，如它們更正 hello 普遍的傾向的決策樹模型 toooverfit 定型資料集。

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a>部署模型 tooAzure ML
[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) 是一種雲端服務，可讓您輕鬆 toobuild 及部署模型的預測分析。 AzureML hello nice 功能之一是其任何 R 函式做為 web 服務的能力 toopublish。 hello AzureML R 封裝會在建立部署簡單 toodo 直接從我們的 R 工作階段 hello DSVM。

toodeploy hello 決策樹狀結構的程式碼 hello 前一節，您需要 toosign tooAzure Machine Learning Studio 中。 您需要工作區識別碼和授權權杖 toosign 中。 toofind 這些值和它們的初始化 hello AzureML 變數：

選取**設定**hello 左側功能表上。 記下您的**工作區識別碼**。 ![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)

選取**授權權杖**從 hello 負擔功能表和附註您**主要授權權杖**。![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)

負載 hello **AzureML**封裝，然後在 hello DSVM 上的 R 工作階段中將以您的語彙基元和工作區識別碼 hello 變數的值：

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


讓我們來簡化此示範更容易 tooimplement hello 模型 toomake。 挑選 hello hello 決策樹狀結構最接近 toohello 根目錄中的三個變數，並建置使用只是那些三個變數的新樹狀結構：

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

我們需要使用 hello 功能做為輸入的預測函式，並傳回 hello 預測的值：

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

發行使用 hello hello predictSpam 函式 tooAzureML **publishWebService**函式：

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

此函數會採用 hello **predictSpam**函式中，會建立名為 web 服務**spamWebService**與定義輸入和輸出，並傳回 hello 新端點的相關資訊。

檢視詳細資料的 hello 發佈 web 服務，包括其應用程式開發介面端點和存取金鑰與 hello 命令：

    spamWebService[[2]]

tootry 它在 hello hello 測試集中的前 10 個資料列：

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a>使用其他可用工具
hello 其餘各節說明如何 toouse 部分 hello 工具安裝在 hello Linux 資料科學 VM。以下是工具所討論的 hello 清單：

* XGBoost
* Python
* Jupyterhub
* Rattle
* PostgreSQL 和 Squirrel SQL
* SQL Server 資料倉儲

## <a name="xgboost"></a>XGBoost
[XGBoost](https://xgboost.readthedocs.org/en/latest/) 工具可提供快速且正確的推進式決策樹實作。

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

XGBoost 也可以從 Python 或命令列進行呼叫。

## <a name="python"></a>Python
程式開發中使用 Python，hello Anaconda Python 分佈 2.7 和 3.5 已安裝在 hello DSVM。

> [!NOTE]
> hello Anaconda 發佈包含[Condas](http://conda.pydata.org/docs/index.html)，也可以使用的 toocreate 有不同的版本及/或在其中安裝封裝的 python 是自訂的環境。
>
>

讓我們在某些 hello spambase 資料集的讀取和分類 hello 電子郵件中，搭配支援向量機器 scikit-了解：

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toomake 預測：

    clf.predict(X.ix[0:20, :])

tooshow 如何 toopublish AzureML 端點，讓我們來建立簡單的模型 hello 三個變數為我們所做的我們先前發行 hello R 模型。

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toopublish hello 模型 tooAzureML:

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> 此操作只適用於 Python 2.7，3.5 版則尚未支援。 請使用 **/anaconda/bin/python2.7**來執行。
>
>

## <a name="jupyterhub"></a>Jupyterhub
在 hello hello Anaconda 發佈 DSVM 隨附 Jupyter 筆記本、 跨平台環境 tooshare Python、 R 或 Julia 的程式碼和分析。 hello Jupyter 筆記本是透過 JupyterHub 存取。 您可以在 ***https://\<VM DNS 名稱或 IP 位址\>:8000/*** 使用本機 Linux 使用者名稱和密碼來登入。 JupyterHub 的所有組態檔可在 **eg /etc/ jupyterhub**目錄中找到。

Hello VM 上已安裝數個範例筆記本：

* 請參閱 hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb)範例 Python 筆記本。
* 如需 [R](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) 的 Notebook 範例，請參閱 **IntroTutorialinR** 。
* 請參閱 hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb)如需其他範例**Python**筆記型電腦。

> [!NOTE]
> hello Julia 語言也會提供 hello hello Linux 資料科學 VM 上的命令列。
>
>

## <a name="rattle"></a>Rattle
[祕](https://cran.r-project.org/web/packages/rattle/index.html)(輕鬆 hello R 分析工具 tooLearn) 是用於資料採礦圖形的 R 工具。 它有直覺式的介面，可讓您輕鬆 tooload、 探索和轉換資料和建立及評估模型。  hello 文章[祕： R 的資料採礦 GUI](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf)提供逐步解說，示範它的功能。

安裝並啟動祕以 hello 下列命令：

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> Hello DSVM 上不需要安裝。 但祕可能會提示您 tooinstall 其他封裝在載入時。
>
>

Rattle 使用索引標籤式介面。 大部分的 hello 索引標籤對應中 hello toosteps[資料科學程序](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)： 如載入資料，或瀏覽它。 從透過 hello 索引標籤的左 tooright 傳送 hello 資料科學程序。 但 hello 最後一個索引標籤包含執行祕 hello R 命令的記錄。

tooload 及設定 hello 資料集：

* tooload hello 檔案、 選取 hello**資料**索引標籤，然後
* 選擇 hello 選取器接下來太**Filename**選擇**spambaseHeaders.data**。
* tooload hello 檔案。 選取**Execute** hello 頂端列的按鈕。 您應該會看到每個資料行，包括其識別的資料類型，其是否為輸入，為目標，或其他類型的變數及 hello 唯一值數目的摘要。
* 祕正確地識別 hello**垃圾郵件**hello 目標資料行。 選取 hello 垃圾郵件 欄中，然後設定 hello**目標資料型別**太**Categoric**。

tooexplore hello 資料：

* 選取 hello**瀏覽** 索引標籤。
* 按一下**摘要**，然後**Execute**，toosee 某些 hello 變數型別資訊和一些摘要統計資料。
* tooview 其他類型的每個變數的相關統計資料選取其他選項，例如**描述**或**基本概念**。

hello**瀏覽** 索引標籤也可讓您有許多繪製的 toogenerate。 tooplot 長條圖的 hello 資料：

* 選取 [分佈] 。
* 為 **word_freq_remove** 和 **word_freq_you** 勾選 [長條圖]。
* 選取 [執行] 。 您應該會看到這兩個密度繪製在單一圖表視窗中，會清除這個 hello 文字的 「 您 」 更經常出現在電子郵件比 「 移除 」。

hello 相互關聯的繪圖也是有趣的。 其中一個 toocreate:

* 選擇**相互關聯**為 hello**類型**，然後
* 選取 [執行] 。
* Rattle 會警告您，它建議的上限為 40 個變數。 選取**是**tooview hello 繪圖。

有一些有趣的相互關聯的: 「 技術 」 強大關聯太"HP 」 和 「 實驗室 」，例如。 此外，強烈相互關聯太"650"，因為 hello 區域的程式碼的 hello 資料集的捐血人 650。

hello 瀏覽視窗中可用 hello hello 字與字之間的關聯性的數字值。 很有趣 toonote，例如，「 技術 」 與 「 貴用戶 」 負面相互關聯和"money"。

祕可以轉換 hello 資料集 toohandle 一些常見的問題。 比方說，它可讓您 toorescale 功能、 推算遺漏值、 處理極端值，並移除變數或資料遺失的觀察值。 Rattle 也可以識別觀察值和 (或) 變數之間的關聯規則。 這些索引標籤不在此入門逐步解說的討論範圍內。

Rattle 也可以執行叢集分析。 讓我們來排除某些功能 toomake hello 輸出更容易 tooread。 在 hello**資料**索引標籤上，選擇**忽略**下一步 tooeach 的 hello 變數，但這十個項目：

* word_freq_hp
* word_freq_technology
* word_freq_george
* word_freq_remove
* word_freq_your
* word_freq_dollar
* word_freq_money
* capital_run_length_longest
* word_freq_business
* spam

然後返回 toohello**叢集**索引標籤上，選擇**KMeans**，並設定 hello*群集數目*too4。 然後**執行**。 hello 結果會顯示 hello [輸出] 視窗中。 有一個叢集具有高頻率的「george」和「hp」，因此可能是合法的商業電子郵件。

toobuild 簡單的決策樹的機器學習模型：

* 選取 hello**模型**索引標籤上，
* 選擇**樹狀**為 hello**類型**。
* 選取**Execute** toodisplay hello 樹狀目錄中的 hello 文字格式輸出視窗。
* 選取 hello**繪製**按鈕 tooview 圖形化版本。 這看起來非常類似 toohello 樹狀目錄中我們取得之前使用*rpart*。

Hello nice 祕功能之一是其能力 toorun 數個機器學習方法，並快速地對其進行評估。 以下是 hello 程序：

* 選擇**所有**hello**類型**。
* 選取 [執行] 。
* 完成之後，您可以按一下任何單一**類型**、 like **SVM**，並檢視 hello 結果。
* 您也可以比較 hello 模型上設定使用 hello hello 驗證 hello 效能**評估** 索引標籤。例如，hello**錯誤矩陣**選取範圍會顯示 hello 混淆矩陣、 整體的錯誤和每個模型的平均的類別錯誤 hello 驗證組。
* 您也可以繪製 ROC 曲線、執行敏感度分析和進行其他類型的模型評估。

一旦您完成建立模型時，選取 hello**記錄**tooview hello R 程式碼在您的工作階段期間執行的祕索引標籤上。 您可以選取 hello**匯出**按鈕 toosave 它。

> [!NOTE]
> 最新版 Rattle 中有一個錯誤。 toomodify hello 指令碼，或使用 toorepeat 您步驟之後，您必須插入 # 字元前面的 * 匯出此記錄檔 … * hello 文字 hello 記錄檔中。
>
>

## <a name="postgresql--squirrel-sql"></a>PostgreSQL 和 Squirrel SQL
hello DSVM 隨附 PostgreSQL 安裝。 PostgreSQL 是複雜的開放原始碼關聯式資料庫。 此區段會顯示如何 tooload 我們 PostgreSQL 到垃圾資料集，然後進行查詢。

您可以載入 hello 資料之前，您必須從 hello localhost tooallow 密碼驗證。 在命令提示字元中︰

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

Hello 底部 hello 設定檔會詳細說明 hello 允許連線的幾行：

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

變更而不是 ident，hello [IPv4 本機連線] 列 toouse md5，因此我們可以使用登入使用者名稱和密碼：

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

然後重新啟動 hello postgres 服務：

    sudo systemctl restart postgresql

PostgreSQL，作為 hello postgres 內建使用者，執行下列命令提示字元中的 hello interactive 終端機 toolaunch psql:

    sudo -u postgres psql

建立新的使用者帳戶，請使用如 hello 您目前的登入，Linux 帳戶 hello 相同的使用者名稱和指定的密碼：

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

然後您的使用者身分登入 toopsql:

    psql

和 hello 資料匯入至新的資料庫：

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

現在，讓我們來瀏覽 hello 資料並執行一些查詢使用**松鼠 SQL**，可讓您與 JDBC 驅動程式透過資料庫互動的圖形工具。

tooget 啟動中，從 hello 應用程式 功能表啟動松鼠 SQL。 tooset 向上 hello 驅動程式：

* 依序選取 [Windows] 和 [檢視驅動程式]。
* 以滑鼠右鍵按一下 [PostgreSQL]，然後選取 [修改驅動程式]。
* 依序選取 [額外類別路徑] 和 [新增]。
* 輸入***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** hello**檔案名稱**和
* 選取 [開啟] 。
* 選擇 [列出驅動程式]，接著在 [類別名稱] 中選取 [org.postgresql.Driver]，然後選取 [確定]。

tooset hello 連接 toohello 本機伺服器上：

* 依序選取 [Windows] 和 [檢視別名]。
* 選擇 hello  **+** 按鈕 toomake 新的別名。
* 命名*垃圾郵件資料庫*，選擇**PostgreSQL**在 hello**驅動程式**下拉式清單。
* 設定 hello URL 太*jdbc:postgresql://localhost/spam*。
* 輸入您的*使用者名稱*和*密碼*。
* 按一下 [確定] 。
* tooopen hello**連接**視窗中，按兩下 hello***垃圾郵件資料庫***別名。
* 選取 [ **連接**]。

toorun 某些查詢：

* 選取 hello **SQL**  索引標籤。
* 輸入一個簡單的查詢，例如`SELECT * from data;`hello 查詢在 hello hello SQL 索引標籤頂端 文字方塊中。
* 按**Ctrl-enter** toorun 它。 根據預設松鼠 SQL 傳回 hello 前 100 個資料列從您的查詢。

有許多您可以執行 tooexplore 這項資料的多個查詢。 例如，如何執行 hello hello word 的頻率*進行*垃圾郵件和火腿之間有差異？

    SELECT avg(word_freq_make), spam from data group by spam;

什麼是經常包含的 hello 特性的電子郵件或者*3d*嗎？

    SELECT * from data order by word_freq_3d desc;

大部分的電子郵件，具有高次數*3d*會很明顯在極垃圾郵件，因此可能很實用的功能，來建立預測模型 tooclassify hello 電子郵件。

如果您想 tooperform 機器學習 PostgreSQL 資料庫中所儲存的資料，請考慮使用[MADlib](http://madlib.incubator.apache.org/)。

## <a name="sql-server-data-warehouse"></a>SQL Server 資料倉儲
Azure SQL 資料倉儲是一種雲端架構、相應放大的資料庫，可處理大量的關聯式與非關聯式資料。 如需詳細資訊，請參閱 [什麼是 Azure SQL 資料倉儲？](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)

tooconnect toohello 資料倉儲，並建立 hello 資料表，請從命令提示字元的 hello 執行的下列命令：

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

然後在 hello sqlcmd 提示字元：

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

使用 bcp 複製資料︰

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> hello hello 下載的檔案中的行尾結束符號視窗樣式，但 bcp 需要 UNIX 樣式，因此我們需要 tootell bcp，使用 hello-r 旗標。
>
>

並使用 sqlcmd 進行查詢︰

    select top 10 spam, char_freq_dollar from spam;
    GO

您也可以使用 Squirrel SQL 進行查詢。 遵循 PostgreSQL，使用 hello Microsoft MSSQL Server JDBC 驅動程式，可以在中找到類似的步驟***/usr/share/java/jdbcdrivers/sqljdbc42.jar***。

## <a name="next-steps"></a>後續步驟
如需這些主題會逐步引導您完成組成 hello 資料科學程序，在 Azure 中的 hello 工作的概觀，請參閱[資料科學的小組流程](http://aka.ms/datascienceprocess)。

如需其他端對端逐步解說示範如何針對特定案例的 hello 小組資料科學程序中的 hello 步驟的說明，請參閱[小組資料科學程序的逐步解說](data-science-process-walkthroughs.md)。 hello 逐步解說也說明如何 toocombine 雲端和內部部署工具和服務至工作流程或管線 toocreate 智慧型應用程式。

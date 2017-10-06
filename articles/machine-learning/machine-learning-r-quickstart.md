---
title: "機器學習的 R 語言 aaaQuickstart 教學課程 |Microsoft 文件"
description: "使用此 R 程式設計教學課程 tooget 啟動快速地使用 Azure Machine Learning Studio toocreate 預測的方案中的 hello R 語言。"
keywords: "快速入門,r 語言,r 程式設計語言,r 程式設計教學課程"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a>Azure Machine Learning 的 hello R 程式設計語言的快速入門教學課程

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a>簡介
本快速入門教學課程可協助您快速開始使用 hello R 程式設計語言擴充 Azure 機器學習。 請遵循此 R 程式設計教學課程 toocreate、 測試及執行 Azure Machine Learning 中的 R 程式碼。 當您完成教學課程，您將使用 Azure Machine Learning 中的 hello R 語言來建立預測的完整解決方案。  

Microsoft Azure Machine Learning 包含許多功能強大的機器學習和資料操作模組。 hello 功能強大的 R 語言被描述為 hello 通用語言分析。 幸好，擴充 Azure Machine Learning 中的分析和資料操作，使用。這種組合提供 hello 延展性及容易部署的 Azure Machine Learning 的 hello 彈性和更深層的分析是。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a>預測和 hello 資料集
預測是一個獲得廣泛採用且相當實用的分析方法。 常見用法預測銷售量的季節性的項目，決定最佳的存貨層級，toopredicting macroeconomic 變數範圍的內。 進行預測時通常是搭配時間序列模型。

時間序列資料是在其中 hello 值有時間索引的資料。 hello 時間索引可以是規則，例如每月或每隔一分鐘，或異常。 時間序列模型會根據時間序列資料。 hello R 程式設計語言包含彈性架構，時間序列資料的大量分析。

在本快速入門指南中，我們將使用加州乳製品產量和訂價資料。 此資料包括每月的數個日常用品 hello 生產和牛奶 fat、 基準商用 hello 價格的相關資訊。

使用 R 指令碼，以及此篇文章中的 hello 資料可以是[這裡下載][download]。 此資料已原本合成 hello 大學的威斯康辛 http://future.aae.wisc.edu/tab/production.html 在提供的資訊。

### <a name="organization"></a>組織
由於您學習如何 toocreate，測試並執行 hello Azure Machine Learning 環境中分析和資料操作 R 程式碼，我們會介紹幾個步驟。  

* 首先，我們將探討 hello hello Azure Machine Learning Studio 環境中使用 hello R 語言的基本概念。
* 然後我們會進行 toodiscussing 資料、 R 程式碼和 hello Azure Machine Learning 環境中的圖形 I/O 的各個層面。
* 然後將藉由建立針對資料清理和轉換程式碼建構 hello 我們的預測解決方案的第一個部分。
* 我們的資料準備，我們將會執行數個 hello 變數，在我們的資料集之間的 hello 相互關聯的分析。
* 最後，我們將針對牛奶產量建立季節性的時間序列預測模型。

## <a id="mlstudio"></a>與 Machine Learning Studio 中的 R 語言互動
本節會帶領您完成與 hello Machine Learning Studio 環境中的 hello R 程式設計語言互動的一些基本概念。 hello R 語言提供功能強大的工具 toocreate 自訂分析和資料操作模組 hello Azure Machine Learning 環境中。

我將使用 RStudio toodevelop、 測試和偵錯的 R 程式碼小的標尺上。 此程式碼是然後剪下和貼上到[執行 R 指令碼][ execute-r-script] Machine Learning Studio 準備 toorun 中的模組。  

### <a name="hello-execute-r-script-module"></a>hello 執行 R 指令碼模組
Machine Learning Studio 中，在 R 指令碼執行內 hello[執行 R 指令碼][ execute-r-script]模組。 舉例來說，hello[執行 R 指令碼][ execute-r-script] Machine Learning Studio 中的模組以圖 1 所示。

 ![R 程式設計語言： 選取 Machine Learning Studio 中的 hello 執行 R 指令碼模組][1]

*圖 1。顯示選取的 hello 執行 R 指令碼模組 hello Machine Learning Studio 環境。*

參照 tooFigure 1，讓我們看看一些使用 hello hello Machine Learning Studio 環境的 hello 關鍵部分[執行 R 指令碼][ execute-r-script]模組。

* hello 實驗中的 hello 模組會顯示 hello 中間窗格內。
* 包含視窗 tooview hello hello 右邊窗格上半部，並編輯您的 R 指令碼。  
* hello 的右窗格的下半部顯示 hello 的某些屬性[執行 R 指令碼][execute-r-script]。 按一下此窗格的 hello 適當點，您可以檢視 hello 錯誤和輸出記錄檔。

我們將當然，討論 hello[執行 R 指令碼][ execute-r-script]更詳細地在 hello 這份文件其餘部分。

使用複雜的 R 函式時，建議您在 RStudio 中進行編輯、測試及偵錯。 與進行任何軟體開發相同，請以累加方式擴充您的程式碼，並在小型的簡單測試案例上進行測試。 然後剪下並貼到 hello R 指令碼視窗中的 hello 的函式[執行 R 指令碼][ execute-r-script]模組。 這種方法可讓您 tooharness hello RStudio 整合式的開發環境 (IDE) 和 hello Azure Machine Learning 的電源。  

#### <a name="execute-r-code"></a>執行 R 程式碼
任何 R 中的程式碼 hello[執行 R 指令碼][ execute-r-script]當您按一下 hello 以執行 hello 實驗，就會執行模組**執行**] 按鈕。 核取記號完成執行之後，會出現在 hello[執行 R 指令碼][ execute-r-script]圖示。

#### <a name="defensive-r-coding-for-azure-machine-learning"></a>Azure Machine Learning 的防禦型 R 編碼
如果您正在使用 Azure Machine Learning 為 Web 服務開發 R 程式碼，您應該明確地規劃程式碼將如何處理非預期的資料輸入和例外狀況。 toomaintain 求清楚明瞭，並未包含許多 hello 方式檢查或例外狀況處理中的大部分 hello 程式碼範例所示。 不過，隨著我們繼續進行，我將會提供您幾個使用 R 例外狀況處理功能的函式範例。  

如果您需要更完整的處理方式的 R 例外狀況處理時，建議您閱讀 hello hello 活頁簿中所列的 Wickham 所適用的章節[附錄 B-進一步閱讀](#appendixb)。

#### <a name="debug-and-test-r-in-machine-learning-studio"></a>在 Machine Learning Studio 中進行 R 程式碼偵錯和測試
tooreiterate，建議您測試和偵錯小型 RStudio 在標尺上的 R 程式碼。 不過，一些情況下，您必須在 hello 的 R 程式碼問題 tootrack[執行 R 指令碼][ execute-r-script]本身。 此外，它是很好的作法 toocheck 在 Machine Learning Studio。

主要的 output.log 找到 hello 執行 R 程式碼並且在 hello Azure Machine Learning 平台上的輸出。 有些其他資訊會顯示在 error.log 中。  

如果發生錯誤 Machine Learning Studio 中執行 R 程式碼時，您的第一個採取的動作應該在 error.log toolook。 這個檔案可以包含有用的錯誤訊息 toohelp 您了解並修正錯誤訊息。 tooview error.log，請按一下 [**檢視錯誤記錄檔**上 hello**屬性] 窗格**hello[執行 R 指令碼][ execute-r-script]包含 hello 錯誤。

例如，執行下列 R 程式碼中的使用未定義變數 y 中的 hello[執行 R 指令碼][ execute-r-script]模組：

    x <- 1.0
    z <- x + y

此程式碼無法 tooexecute，導致錯誤狀況。 按一下**檢視錯誤記錄檔**上 hello**屬性 窗格**產生 hello 顯示圖 2 所示。

  ![錯誤訊息快顯][2]

*圖 2.錯誤訊息快顯。*

它看起來我們需要 toolook output.log toosee hello R 錯誤訊息中。 按一下 hello[執行 R 指令碼][ execute-r-script] ，然後按一下hello**檢視 output.log** hello 上的項目**屬性] 窗格**toohello 權限。 新的瀏覽器視窗隨即開啟，並看 hello 下列。

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

這則錯誤訊息包含意外狀況，並清楚地識別 hello 問題。

tooinspect hello R 中的任何物件值，您可以列印這些值 toohello output.log 檔案。 hello 規則檢查物件的值基本上為 hello 相同如同互動式的 R 工作階段。 例如，如果您的一行輸入變數的名稱，hello 物件 hello 值會列印的 toohello output.log 檔案。  

#### <a name="packages-in-machine-learning-studio"></a>Machine Learning Studio 中的封裝
Azure Machine Learning 附有超過 350 個預先安裝的 R 語言封裝。 您可以使用下列程式碼中 hello hello[執行 R 指令碼][ execute-r-script]模組 tooretrieve hello 一份預先安裝套件。

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

如果您不要在 hello 時刻，以了解 hello 這段程式碼的最後一行，閱讀。 在這份文件其餘部分 hello 廣泛我們將討論在 hello Azure Machine Learning 環境中使用 R。

### <a name="introduction-toorstudio"></a>簡介 tooRStudio
RStudio 是廣泛使用的 IDE，如。我將使用 RStudio 編輯、 測試和偵錯的一些本快速入門指南中使用的 hello R 程式碼。 R 程式碼測試並準備好後，您只需剪下，並從 hello RStudio 編輯器貼入 Machine Learning Studio[執行 R 指令碼][ execute-r-script]模組。  

如果您沒有在桌面的電腦上安裝的 hello R 程式設計語言，建議您請立刻。 開放原始碼 R 語言的免費下載位於 hello 完整 R 封存網路 (CRAN) 在[http://www.r-project.org/](http://www.r-project.org/)。 有提供適用於 Windows、MacOS 及 Linux/UNIX 的下載項目。 選擇附近的鏡像，並依照 hello 下載指示進行。 此外，CRAN 也包含大量實用的分析和資料操作封裝。

如果您是新 tooRStudio，您應該下載並安裝 hello 桌面版本。 您可以找到 RStudio Windows、 Mac OS 和 Linux/UNIX 會在下載 http://www.rstudio.com/products/RStudio/ hello。 請依照 hello tooinstall RStudio 提供您桌面的電腦上的指示。  

教學課程簡介 tooRStudio 位於 https://support.rstudio.com/hc/sections/200107586-Using-RStudio。

我在[附錄 A][appendixa] 中提供了一些使用 RStudio 的其他相關資訊。  

## <a id="scriptmodule"></a>取得資料移轉入和 hello 執行 R 指令碼模組
本節中，我們將討論如何您將資料傳入及傳出 hello[執行 R 指令碼][ execute-r-script]模組。 我們將復 toohandle 各種資料型別讀取方式 hello 進出[執行 R 指令碼][ execute-r-script]模組。

本節 hello 完整程式碼是您之前下載的 hello zip 檔案中。

### <a name="load-and-check-data-in-machine-learning-studio"></a>在 Machine Learning Studio 中載入和檢查資料
#### <a id="loading"></a>載入 hello 資料集
我們一開始會載入 hello **csdairydata.csv** Azure Machine Learning Studio 檔案。

* 啟動 Azure Machine Learning Studio 環境。
* 按一下**+ 新增**hello 在較低的螢幕，然後選取左**資料集**。
* 選取**從本機檔案**，然後**瀏覽**tooselect hello 檔案。
* 請確定您已選取**一般 CSV 檔案具有標頭 (.csv)** hello hello 資料集的類型。
* 按一下 hello 核取記號。
* 已上傳 hello 資料集之後，您應該看到 hello 新的資料集即可 hello**資料集** 索引標籤。  

#### <a name="create-an-experiment"></a>建立實驗
現在我們有一些資料 Machine Learning Studio 中，我們需要 toocreate 實驗 toodo hello 分析。  

* 按一下**+ 新增**在 hello 左下並選取**實驗**，然後**空白實驗**。
* 您可以藉由選取，命名您的經驗，並修改 hello**上建立的實驗...** hello hello 頁頂端的標題。 例如，變更太**CA 香蕉分析**。
* Hello hello 實驗頁面的左側展開**儲存的資料集**，然後**我的資料集**。 您應該會看見 hello **cadairydata.csv**您先前上傳。
* 拖放 hello **csdairydata.csv 資料集**到 hello 實驗。
* 在 hello**搜尋實驗項目**hello 頂端 hello 左窗格中，型別上的方塊[執行 R 指令碼][execute-r-script]。 您會看到顯示 hello 搜尋清單中的 hello 模組。
* 拖放 hello[執行 R 指令碼][ execute-r-script]到您棧板上的模組。  
* Hello hello 輸出連接**csdairydata.csv 資料集**toohello 最左邊的輸入 (**Dataset1**) 的 hello[執行 R 指令碼][execute-r-script]。
* **別忘了 [儲存] tooclick ！**  

此時，您的實驗應該會看起來像圖 3。

![hello CA 香蕉分析試驗資料集和執行 R 指令碼模組][3]

*圖 3。hello CA 香蕉分析試驗資料集和執行 R 指令碼模組。*

#### <a name="check-on-hello-data"></a>檢查 hello 資料
讓我們看看我們已載入至我們實驗 hello 資料。 在 hello 實驗中，按一下 hello hello 輸出**cadairydata.csv 資料集**選取**視覺化**。 您應該會看到類似圖 4 的內容。  

![Hello cadairydata.csv 資料集的摘要][4]

*圖 4：Hello cadairydata.csv 資料集的摘要。*

在這個檢視中，我們會看到許多有用的資訊。 我們可以看到 hello 該資料集的前幾個資料列。 如果我們選取資料行，hello 統計資料 區段會顯示 hello 資料行的詳細資訊。 例如，hello 功能類型的資料列顯示我們哪些 Azure Machine Learning Studio 指派 toohello 資料行的資料型別。 擁有快速的看起來像這樣是很好的例行性檢查，我們開始 toodo 任何嚴重的工作之前。

### <a name="first-r-script"></a>第一個 R 指令碼
讓我們來建立簡單的第一個 R 指令碼 tooexperiment 與 Azure Machine Learning Studio 中。 已建立並測試下列指令碼中 RStudio hello。  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

現在我需要 tootransfer 此指令碼 tooAzure Machine Learning Studio。 我可以只利用剪下並貼上。 不過，在此案例中，我將透過 Zip 檔案轉移我的 R 指令碼。

### <a name="data-input-toohello-execute-r-script-module"></a>資料輸入的 toohello 執行 R 指令碼模組
讓我們看一下 hello 輸入 toohello[執行 R 指令碼][ execute-r-script]模組。 在此範例中我們將 hello 加州日常的資料讀入 hello[執行 R 指令碼][ execute-r-script]模組。  

有三個可能的輸入 hello[執行 R 指令碼][ execute-r-script]模組。 視您的應用方式而定，您可以使用這當中的任何一個或所有輸入。 它也是非常合理 toouse R 指令碼完全接受任何輸入。  

讓我們看看每個這些輸入，從左 tooright。 您可以藉由將游標放在 hello 輸入上方及閱讀 hello 工具提示中看到每個 hello 輸入 hello 名稱。  

#### <a name="script-bundle"></a>指令碼組合
hello 指令碼組合輸入可讓您將 zip 檔案 toopass hello 內容[執行 R 指令碼][ execute-r-script]模組。 您可以使用其中一個 hello 遵循 hello zip 檔案的命令 tooread hello 內容到您的 R 程式碼。

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> Azure Machine Learning 會處理 hello zip 檔案，就好像它們是在 hello src / 目錄，因此您需要的 tooprefix 您的檔案名稱具有這個目錄名稱。 例如，如果 hello zip 包含 hello 檔案`yourfile.R`和`yourData.rdata`hello 在根目錄中的 hello zip，您會解決這些問題，做為`src/yourfile.R`和`src/yourData.rdata`時使用`source`和`load`。
> 
> 

我們已經討論過載入中的資料集[載入 hello 資料集](#loading)。 一旦您建立並測試顯示 hello 前一節中的 hello R 指令碼，不要 hello 遵循：

1. 儲存成 hello R 指令碼。R 的檔案。 我將我的指令碼檔案稱為 "simpleplot.R"。 以下是 hello 內容。
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. 建立一個 Zip 檔案，然後將您的指令碼複製到此 Zip 檔案。 在 Windows 中，您可以在 hello 檔案上按一下滑鼠右鍵並選取**傳送給**，然後**壓縮的資料夾**。 這會建立新的 zip 檔案包含 hello"simpleplot。R"檔案。
3. 新增檔案 toohello**資料集**在 Machine Learning Studio 中，指定與 hello 類型**zip**。 您現在應該會在您資料集中看到 hello zip 檔案。
4. 拖放 hello zip 檔案從**資料集**到 hello **ML Studio 畫布**。
5. Hello hello 輸出連接**zip 資料**圖示 toohello**指令碼組合**輸入的 hello[執行 R 指令碼][ execute-r-script]模組。
6. 型別 hello `source()` hello 到 hello 程式碼視窗您 zip 檔案名稱的函式[執行 R 指令碼][ execute-r-script]模組。 在我的案例中，我鍵入了 `source("src/simpleplot.R")`。  
7. 確定按一下 [ **儲存**]。

完成這些步驟之後，hello[執行 R 指令碼][ execute-r-script]模組會執行 hello R 指令碼 hello zip 檔案中執行 hello 實驗時。 此時，您的實驗應該會看起來像圖 5。

![使用已壓縮之 R 指令碼的實驗][6]

*圖 5.使用已壓縮之 R 指令碼的實驗。*

#### <a name="dataset1"></a>資料集1
您可以使用的 hello Dataset1 輸入傳遞矩形資料 tooyour R 程式碼的資料表。 在我們的簡單的指令碼 hello`maml.mapInputPort(1)`函式會從連接埠 1 讀取 hello 資料。 這項資料接著會指派 tooa 資料框架變數名稱在程式碼中。 在簡單的指令碼 hello 第一行程式碼會執行 hello 分派。

    cadairydata <- maml.mapInputPort(1)

Hello 上按一下來執行實驗**執行** 按鈕。 Hello 執行完成時，按一下 hello[執行 R 指令碼][ execute-r-script]模組，然後按一下**檢視輸出記錄檔**hello 屬性] 窗格。 新的頁面應該會出現在瀏覽器中顯示 hello hello output.log 檔案內容。 當您向下捲動時您應該會看到類似下列 hello。

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

遠 hello 關閉頁面是 hello 的資料行，看起來像 hello 以下更詳細的資訊。

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

這些結果是大部分如預期般，使用 228 觀察和 9 hello 資料框架中的資料行。 我們可以看到 hello 資料行名稱、 hello R 資料類型以及每個資料行的範例。

> [!NOTE]
> 這個相同的列印的輸出會很方便提供 hello R 裝置 hello 輸出[執行 R 指令碼][ execute-r-script]模組。 我們將討論的 hello hello 輸出[執行 R 指令碼][ execute-r-script] hello 下一節中的模組。  
> 
> 

#### <a name="dataset2"></a>資料集2
hello hello Dataset2 輸入行為是相同的 Dataset1 toothat。 您可以使用此輸入將第二個矩形資料表傳遞給您的 R 程式碼。 hello 函式`maml.mapInputPort(2)`，hello 引數 2，是使用的 toopass 這項資料。  

### <a name="execute-r-script-outputs"></a>執行 R 指令碼輸出
#### <a name="output-a-dataframe"></a>輸出資料框架
您也可以使用 hello 為矩形資料表透過 hello 結果 Dataset1 連接埠輸出的 R 資料框架的 hello 內容`maml.mapOutputPort()`函式。 在簡單的 R 指令碼會執行由 hello 行下。

    maml.mapOutputPort('cadairydata')

之後執行 hello 實驗中，按一下 hello 結果 Dataset1 輸出連接埠，然後按一下**視覺化**。 您應該會看到類似圖 6 的內容。

![hello 視覺效果的 hello hello 加州日常資料輸出][7]

*圖 6。hello hello 加州日常資料輸出的 hello 視覺效果。*

完全依照我們所預期，此輸出看起來相同 toohello 輸入。  

### <a name="r-device-output"></a>R 裝置輸出
hello 裝置 hello 輸出[執行 R 指令碼][ execute-r-script]模組包含訊息和圖形輸出。 從 R 這兩個標準輸出和標準錯誤訊息會傳送 toohello R 裝置輸出連接埠。  

tooview hello R 裝置輸出，按一下 hello 連接埠，然後在**視覺化**。 我們看到 hello 標準輸出和圖 7 中的 hello R 指令碼從標準錯誤。

![標準輸出和標準錯誤從 hello R 裝置連接埠][8]

*圖 7.標準輸出和標準誤差從 hello R 裝置連接埠。*

我們向下捲動，請參閱我們的 R 指令碼，圖 8 中的 hello 圖形輸出。  

![從 hello R 裝置連接埠圖形輸出][9]

*圖 8.來自 hello R 裝置連接埠的輸出圖形。*  

## <a id="filtering"></a>資料篩選和轉換
本節中，我們將會執行一些基本的資料篩選和 hello 加州日常資料轉換作業。 本節結尾 hello 我們會具有適合用來建立分析模型的格式資料。  

更具體來說，在本節中，我們將會執行數個常見的資料清除和轉換工作：類型轉換、依據資料框架進行篩選、新增新的計算資料行，以及值轉換。 這個背景應可協助您處理 hello 許多實際問題中發生的變化。

hello 完整的 R 程式碼對此區段可前往您剛才下載的 hello zip 檔案中。

### <a name="type-transformations"></a>類型轉換
現在，我們可以讀入 hello 中的 hello R 程式碼中的 hello 加州日常資料[執行 R 指令碼][ execute-r-script]模組中，我們需要 tooensure hello 資料行中的 hello 資料有適合的 hello 類型與格式。  

R 是動態類型的語言，這表示資料型別會從所需的一個 tooanother 強制。 在 R 中的 hello 不可部分完成的資料類型包括數值、 邏輯和字元。 hello 因素型別是使用的 toocompactly 存放區中的類別資料。 您可以在 hello 參考中找到更多有關資料型別的[附錄 B-進一步閱讀](#appendixb)。

表格式資料到 R 從外部來源讀取時，永遠是個不錯的主意 toocheck hello 產生 hello 資料行中的型別。 您可能想要字元類型的資料行，但在許多情況下這會顯示為因素類型，反之亦然。 在其他情況下，則是會以字元資料代表您認為應該是數值的資料行，例如 '1.23' 而非浮點數形式的 1.23。  

幸運的是，它是一個型別 tooanother 輕鬆 tooconvert，只要對應可能。 例如，您無法將 'Nevada' 轉換成數值，但您可以將它轉換 tooa 因素 （類別變數）。 另舉一例，您可以將數值 1 轉換成字元 '1' 或因素。  

針對任何這些轉換 hello 語法很簡單： `as.datatype()`。 這些類型轉換函式 hello 如下。

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

查看 hello 我們輸入 hello 前一節中的 hello 資料行資料類型： 所有資料行都是數字，除了 hello 資料行標示為 'Month'，也就是型別字元的類型。 讓我們來轉換這個 tooa 因素，並測試 hello 結果。  

我已刪除 hello 列建立 hello scatterplot 矩陣並加入轉換 hello 'Month' 資料行 tooa 因素一條線。 在我的實驗中我將只剪下並 hello R 程式碼貼入程式碼視窗中 hello hello[執行 R 指令碼][ execute-r-script]模組。 您也可以更新 hello zip 檔案，並將它上傳 tooAzure Machine Learning Studio 中，但這需要一些步驟。  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

讓我們來執行這個程式碼，並查看 hello hello R 指令碼的輸出記錄檔。 圖 9 顯示 hello hello 記錄檔中的相關資料。

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*圖 9.Hello 與因數變數的資料框架的摘要。*

現在應顯示月份的 hello 型別 '**具有 14 個層級的因素**'。 因為 hello 年只 12 個月，這會是問題。 您也可以檢查 hello 類型的 toosee 中**視覺化**hello 結果資料集中的連接埠是 '**類別**'。

hello 問題為該 hello 'Month' 資料行未有系統地編碼。 在某些情況下，某個月份稱為 April ，在其他情況下則會縮寫成 Apr。我們可以修剪 hello 字串 too3 字元來解決這個問題。 hello 一行程式碼現在看起來像下列 hello:

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

重新執行 hello 實驗，並檢視 hello 輸出記錄檔。 hello 預期的結果會顯示在圖 10。  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*圖 10.Hello 與因素層級的正確數目的資料框架的摘要。*

我們因數變數現在具有所需的 hello 12 個層級。

### <a name="basic-data-frame-filtering"></a>基本資料框架篩選
R 資料框架支援強大的篩選功能。 藉由在資料列或資料行使用邏輯篩選，可將資料集再細分成子集。 在許多情況下，將會需要複雜的篩選條件。 參考中的 hello[附錄 B-進一步閱讀](#appendixb)包含廣泛的篩選資料框架的範例。  

有一些篩選是我們應該在資料集上執行的。 如果您看一下 hello hello cadairydata 資料框架中的資料行，您會看到兩個不必要的資料行。 hello 第一個資料行只會保存資料列數字，不是很有用。 hello 第二個資料行，Year.Month，包含重複的資訊。 我們可以使用下列 R 程式碼的 hello，輕鬆地排除這些資料行。

> [!NOTE]
> 從現在在本節中，我將只顯示您的 hello 我 hello 中加入額外的程式碼[執行 R 指令碼][ execute-r-script]模組。 將每一個新行**之前**hello`str()`函式。 我使用這個函式 tooverify 我結果 Azure Machine Learning Studio 中。
> 
> 

加入下列行 toomy R 程式碼中 hello hello[執行 R 指令碼][ execute-r-script]模組。

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

在您實驗中執行此程式碼並查看 hello 輸出記錄檔中的 hello 結果。 這些結果如圖 11 所示。

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*圖 11.Hello 與移除的兩個資料行的資料框架的摘要。*

好消息！ 我們取得 hello 預期結果。

### <a name="add-a-new-column"></a>加入新的資料行
toocreate 時間序列模型會很方便 toohave 資料行包含 hello hello hello 時間序列的開頭之後的月份。 我們將會建立新資料行 'Month.Count'。

toohelp 組織 hello 程式碼，我們將建立簡單我們第一個函式， `num.month()`。 然後，我們會套用此函式 toocreate hello 資料框架中的新資料行。 hello 新的程式碼如下所示。

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

現在，執行更新的 hello 實驗並使用 hello 輸出記錄檔 tooview hello 結果。 這些結果如圖 12 所示。

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*圖 12.Hello 與 hello 額外的資料行的資料框架的摘要。*

看來一切運作正常。 我們在我們的資料框架中有 hello hello 預期的值與新資料行。

### <a name="value-transformations"></a>值轉換
這一節我們將的部分我們的資料框架的 hello 欄中的 hello 值上執行一些簡單的轉換。 hello R 語言支援幾乎任意值轉換。 參考中的 hello[附錄 B-進一步閱讀](#appendixb)包含廣泛的範例。

如果您看一下您應該會看到我們資料框架的 hello 摘要中的 hello 值是奇數這裡。 加州生產的冰淇淋比牛奶多？ 否，當然不是，這樣會造成沒有意義，悲傷成為這個事實可能 toosome 我們冰淇淋能。 hello 單位都不同。 hello 價格是以我們磅，單位 1 M 的冰淇淋美國磅 1000 的單位我們加侖，而且小屋 cheese 為 1,000 美國磅單位的牛奶。 假設冰淇淋充分權衡約 6.5 磅每加侖，我們可以輕鬆地執行 hello 乘法 tooconvert，因此它們都放在相同單位的 1,000 磅，這些值。

針對我們的預測模型，我們使用乘法模型來進行此資料的趨勢和季節性調整。 記錄轉換，可讓我們 toouse 線性模型，以簡化此程序。 我們可以套用在 hello 相同函式套用 hello 乘數的位置中的 hello 記錄轉換。

在下列程式碼的 hello，定義新的函式， `log.transform()`，並將它套用 toohello 包含 hello 數值的資料列。 hello R`Map()`函式是使用的 tooapply hello`log.transform()`函式 toohello 選取 hello 資料框架的資料行。 `Map()`太類似`apply()`，但允許多個引數 toohello 函式清單。 請注意，有一份提供第二個引數 toohello hello`log.transform()`函式。 hello`na.omit()`函式當做位元的清除 tooensure 我們沒有遺失或未定義的值在 hello 資料框架。

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

沒有在 hello 相當多的位元發生`log.transform()`函式。 大部分的這段程式碼會檢查 hello 引數的潛在問題，或處理的例外狀況，仍可能會發生在 hello 計算期間。 只需幾行，此程式碼的實際 hello 計算。

hello 防禦程式設計 hello 目標是 tooprevent hello 失敗會阻礙無法繼續處理的單一函式。 執行很久的分析如果突然失敗，可能會讓使用者深感挫折。 這種情況下，預設傳回值必須選擇，將會限制的 tooavoid 損害 toodownstream 處理。 訊息也是有錯誤哪裡發生的產生的 tooalert 使用者。

如果您不使用的 toodefensive 程式設計，在 R 中，所有這段程式碼看起來可能有點非常龐大。 我將引導您完成 hello 主要步驟：

1. 定義包含四個訊息的向量。 這些訊息是部分 hello 可能的錯誤和例外狀況，可能會發生這段程式碼使用的 toocommunicate 資訊。
2. 我會針對每個案例傳回一個 NA 值。 有許多其他可能會有較少副作用的可能性。 我無法傳回向量的零或原始輸入的向量 hello，例如。
3. Hello 引數 toohello 函式上執行的檢查。 在每個案例中，如果偵測到錯誤時，會傳回預設值的訊息所產生和 hello`warning()`函式。 我使用`warning()`而不是`stop()`為 hello 後者將會終止執行，完全什麼我試著 tooavoid。 請注意，我是以程序性風格撰寫此程式碼，因此在此情況下，函式型方法看似既複雜又難以理解。
4. hello 記錄計算會包裝在`tryCatch()`，讓例外狀況並不會造成突然中止 tooprocessing。 如果沒有 `tryCatch()` ，R 函式所引發的大多數錯誤都會導致產生停止訊號，而此訊號所執行的就是停止。

執行此 R 程式碼在您實驗中，並查看 hello 列印 hello output.log 檔案的輸出。 您現在會看見 hello 轉換值的 hello hello 的四個資料行記錄，如圖 13 所示。

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*圖 13.摘要的 hello 轉換 hello 資料框架中的值。*

我們會看到已轉換 hello 值。 現在，牛奶產量大幅超過所有其他乳製品產量，還記得我們現在看的是對數刻度。

此時會清除我們的資料，而我們已經準備好進行一些建立模型工作。 查看 hello 視覺效果的輸出結果集的 hello 摘要我們[執行 R 指令碼][ execute-r-script]模組，就會看見 hello 'Month' 資料行是 '類別' 具有 12 個唯一值，一次，就像我們.

## <a id="timeseries"></a>時間序列物件和相互關聯分析
這一節中，我們將探索幾個基本的 R 時間序列物件及分析 hello 相互關聯之間有些 hello 變數。 我們的目標是 toooutput 資料框架包含 hello 成對的相互關聯資訊在數個延遲。

hello 完整的 R 程式碼對此區段是您之前下載的 hello zip 檔案中。

### <a name="time-series-objects-in-r"></a>R 中的時間序列物件
如已經提過的，時間序列是一系列依時間編制索引的資料值。 R 時間序列物件是使用的 toocreate，而且管理 hello 時間索引。 有數個優點 toousing 時間數列物件。 時間序列物件讓您從 hello 管理 hello 時間序列索引值 hello 物件中封裝的詳細資料。 此外，時間序列物件允許您 toouse hello 許多時間數列方法來繪製，等模型列印。

hello POSIXct 時間數列類別通常用於和相當簡單。 這個時間數列類別測量從 hello hello epoch，自 1970 年 1 月 1 日開始的時間。 在此範例中，我們將使用 POSIXct 時間序列物件。 其他廣泛使用的 R 時間序列物件類別包括 zoo 和 xts (可延伸時間序列)。
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a>時間序列物件範例
讓我們開始進行我們的範例。 請將**新的**[執行 R 指令碼][execute-r-script]模組拖放到您的實驗中。 連接現有 hello hello 結果 Dataset1 輸出連接埠[執行 R 指令碼][ execute-r-script]模組 toohello Dataset1 輸入 hello 新連接埠[執行 R 指令碼][execute-r-script]模組。

我在 hello 第一個範例中，當我們透過 hello 範例中，在一些重點，我將會顯示進度只 hello 累加的 R 程式碼在每個步驟的其他行。  

#### <a name="reading-hello-dataframe"></a>讀取 hello 資料框架
第一個步驟中，我們在資料框架中讀取，並確定我們取得 hello 預期結果。 hello 下列程式碼應該執行 hello 作業。

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

現在，執行 hello 實驗。 新執行 R 指令碼圖形 hello hello 記錄看起來應該像圖 14。

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

 *14.Hello hello 執行 R 指令碼模組中的資料框架的摘要。*

此資料是 hello 預期型別和格式。 請注意，型別因素 hello 'Month' 資料行是 hello 是預期的層級數目。

#### <a name="creating-a-time-series-object"></a>建立時間序列物件
我們需要 tooadd 時間序列物件 tooour 資料框架。 Hello 目前程式碼取代 hello 下列程式碼，這會將 POSIXct 類別的新資料行中。

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

現在，檢查 hello 記錄檔。 這應該會看起來像圖 15。

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

 *15.Hello 與時間序列物件的資料框架的摘要。*

我們可以看到從 hello 摘要類別 POSIXct 事實上是該 hello 新資料行。

### <a name="exploring-and-transforming-hello-data"></a>瀏覽及 hello 資料轉換
讓我們來探索一些 hello 這個 dataset 中的變數。 Scatterplot 矩陣是很好的方式 tooproduce 快速瀏覽。 我正在取代 hello `str()` hello 先前 R 的程式碼以行下的 hello 函式。

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

請執行此程式碼，然後看看結果如何。 hello R 裝置連接埠在產生的 hello 圖看起來應該像圖 16。

![所選變數的散佈圖矩陣][17]

*圖 16.所選變數的散佈圖矩陣。*

一些奇怪的結構中沒有 hello 關聯性之間這些變數。 也許這就會發生與 hello 資料中的趨勢和 hello 事實，我們不標準化 hello 變數。

### <a name="correlation-analysis"></a>相互關聯分析
我們需要 tooboth tooperform 相互關聯分析解除趨勢，並設立標準 hello 變數。 我們可以只使用 hello R`scale()`函式，以同時中心和縮放變數。 此函式可能也執行得更快。 不過，我想 tooshow 您的防禦程式設計範例

hello`ts.detrend()`如下所示的函式會執行這兩種作業。 hello 下列兩行程式碼取消趨勢 hello 資料，然後標準化 hello 值。

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

沒有在 hello 相當多的位元發生`ts.detrend()`函式。 大部分的這段程式碼會檢查 hello 引數的潛在問題，或處理的例外狀況，仍可能會發生在 hello 計算期間。 只需幾行，此程式碼的實際 hello 計算。

我們已經在[值轉換](#valuetransformations)中討論過防禦型程式設計的範例。 兩個計算區塊皆包裝在 `tryCatch()` 中。 對於某些錯誤它意義 tooreturn hello 原始輸入的向量，而在其他情況下，傳回零的向量。  

請注意，用來取消趨勢 hello 線性迴歸時間數列迴歸。 hello 預測量變數是時間序列物件。  

一次`ts.detrend()`定義我們會套用它 toohello 變數，在我們的資料框架中有用。 我們必須強制轉型所建立的 hello 產生清單`lapply()`toodata 資料框架使用`as.data.frame()`。 因為防禦層面`ts.detrend()`，失敗 tooprocess 其中 hello 變數並不會妨礙修正 hello 處理其他人。  

hello 最後一行程式碼會建立成對 scatterplot。 執行 hello R 程式碼之後, 的 hello scatterplot 的 hello 結果會顯示在圖 17。

![已去除趨勢並已標準化之時間序列的成對散佈圖][18]

*圖 17.已去除趨勢並已標準化之時間序列的成對散佈圖。*

您可以比較這些結果 toothose，16 圖所示。 以 hello 趨勢移除與 hello 變數標準化，我們看到少很多 hello 這些變數之間的關聯性中的結構。

hello 程式碼 toocompute hello 相互關聯當做 R ccf 物件如下所示。

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

執行此程式碼會產生 hello 記錄圖 18 所示。

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

*圖 18.Ccf 的清單物件從 hello 成對的相互關聯分析。*

每段延隔時間都有一個相互關聯值。 這些相互關聯值的 「 無 」 夠大 toobe 顯著。 因此，可以推斷出我們可以獨立建立每個變數的模型。

### <a name="output-a-dataframe"></a>輸出資料框架
我們有一份 R ccf 物件為計算 hello 成對的相互關聯。 因為 hello 結果資料集輸出連接埠真正需要的資料框架，這會有問題的位元。 此外，hello ccf 物件是本身的清單，我們想要只 hello 值 hello 這個清單中，在 hello hello 相互關聯的第一個項目中各種延遲。

hello hello ccf 物件清單，也就是本身的清單中的下列程式碼擷取 hello 延隔時間值。

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

hello 第一行程式碼會有點困難，並說明可協助您了解它。 我們有 hello 下列出內部工作 hello:

1. hello '**[[**'hello 引數的運算子'**1**' 選取 hello 向量的相互關聯性在 hello 像是從 hello hello ccf 物件清單的第一個項目。
2. hello`do.call()`函式適用於 hello`rbind()`透過 hello 清單元件的 hello 函式會傳回`lapply()`。
3. hello`data.frame()`函式會強制使所產生的 hello 結果`do.call()`tooa 資料框架。

請注意，hello 列名稱資料行中的 hello 資料框架。 這樣會保留 hello 列名稱時，它們的 hello 輸出[執行 R 指令碼][execute-r-script]。

執行 hello 程式碼會產生 hello 圖 19 所示的輸出時我**視覺化**hello 在 hello 結果資料集連接埠的輸出。 如預期般 hello 列名稱位於 hello 第一個資料行中。

![從 hello 相互關聯分析的結果輸出][20]

*圖 19.輸出來源 hello 相互關聯分析的結果。*

## <a id="seasonalforecasting"></a>時間序列範例：季節性預測
我們的資料現在是適用於分析，表單中，我們判定有沒有 hello 變數之間的重要相互關聯。 讓我們繼續來建立時間序列預測模型。 使用此模型會預測加州牛奶生產環境適用於 hello 12 個月的 2013年。

我們的預測模型將會有兩個元件，亦即趨勢元件和季節性元件。 hello 完成預測是 hello 的這兩個元件的產品。 這種模型稱為乘法模型。 hello 的替代方式是加總的模型。 我們已經有套用感興趣，使得這項分析容易處理的記錄檔轉換 toohello 變數。

hello 完整的 R 程式碼對此區段是您之前下載的 hello zip 檔案中。

### <a name="creating-hello-dataframe-for-analysis"></a>建立 hello 進行分析的資料框架
啟動新增**新**[執行 R 指令碼][ execute-r-script]模組 tooyour 實驗。 連接 hello**結果資料集**hello 現有輸出[執行 R 指令碼][ execute-r-script]模組 toohello **Dataset1** hello 新模組的輸入。 hello 結果看起來應該像圖 20。

![hello 試驗 hello 加入新執行 R 指令碼模組][21]

*圖 20。hello 試驗 hello 加入新執行 R 指令碼模組。*

與 hello 相互關聯分析我們剛完成時，我們需要 tooadd POSIXct 時間序列物件的資料行。 下列程式碼的 hello 會這樣做只。

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

執行這個程式碼，並查看 hello 記錄檔。 hello 結果看起來應該像圖 21。

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*圖 21.Hello 資料框架的摘要。*

與這個結果中，我們會準備 toostart 我們的分析。

### <a name="create-a-training-dataset"></a>建立訓練資料集
使用建構的 hello 資料框架中，我們需要 toocreate 定型資料集。 這項資料將會包含所有的 hello 觀察 hello 過去 12 的 hello 2013 年，但這是我們的測試資料集。 hello 下列子集 hello 資料框架的程式碼，並建立 hello 日常的生產環境和價格變數的繪圖。 然後建立繪圖 hello 的生產環境和價格的四個變數。 是使用的 toodefine 圖，某些加強匿名函式，然後逐一查看的 hello hello 清單與其他兩個引數`Map()`。 如果您正在想著可以在這裡使用 for 迴圈，的確沒錯。 但是，由於 R 是函式型語言，因此我示範給您的是函式型方法。

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

執行 hello 程式碼會產生的 hello hello R 裝置輸出所示圖 22 繪製數列的時間序列。 請注意該 hello 時間軸中的日期，nice hello 時間數列繪製方法的優點的單位。

![加州乳製品產量和價格資料的第一個時間序列圖](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![加州乳製品產量和價格資料的第二個時間序列圖](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![加州乳製品產量和價格資料的第三個時間序列圖](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![加州乳製品產量和價格資料的第四個時間序列圖](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

*圖 22.加州乳製品產量和價格資料的時間序列圖。*

### <a name="a-trend-model"></a>趨勢模型
一旦建立時間序列物件，但有查看 hello 資料，讓我們開始 tooconstruct hello 加州牛奶實際執行資料的趨勢模型。 我們可以使用時間序列迴歸來進行這項操作。 不過，它是清除來自 hello 繪圖，我們將會需要個以上的斜率和截距 tooaccurately 模型 hello 觀察到 hello 定型資料中的趨勢。

我會提供 hello 小規模的 hello 資料，來建置 RStudio 趨勢的 hello 模型，然後剪下並貼入 Azure Machine Learning 中的 hello 產生模型。 RStudio 針對這種互動式分析提供了互動式環境。

做為第一次嘗試，我會嘗試與向上 too3 的次方多項式迴歸。 這些種類的模型實際蘊藏過度配適的危險。 因此，它會是最佳 tooavoid 高序位條款。 hello`I()`函式會禁止 hello 內容的解譯 （解譯 hello 內容 「 依照原狀 」） 並可讓您在迴歸方程式的 toowrite 逐字解譯函式。

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

這會產生下列 hello。

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

從 P 值 (Pr (> | t |)) 在此輸出中，我們可以看到該 hello 平方的詞彙可能不重要。 我將使用 hello`update()`函式的 toomodify 此模型所卸除 hello 平方詞彙。

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

這會產生下列 hello。

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

這樣看起來較好。 所有 hello 詞彙皆屬於顯著。 不過，hello 2e-16 個值是預設值，而且不應該太嚴重採用。  

例行性進行測試，讓我們進行 hello 加州日常的實際執行資料的時間序列的圖以顯示 hello 趨勢曲線。 加入下列程式碼在 hello Azure Machine Learning 中的 hello[執行 R 指令碼][ execute-r-script]模型 (不 RStudio) toocreate hello 模型，然後進行繪圖。 hello 結果是以圖 23 所示。

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![顯示趨勢模型的加州牛奶產量資料](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

*圖 23.顯示趨勢模型的加州牛奶產量資料。*

您似乎 hello 趨勢模型也相當適合 hello 資料。 此外，那里似乎未 toobe 辨識項的過度配度，例如在 hello 模型曲線 wiggles 奇數。  

### <a name="seasonal-model"></a>季節性模型
使用趨勢模型中時，我們需要 toopush 上，而且包含 hello 季節性效應。 我們將使用 hello hello 年度月份 hello 線性模型 toocapture hello 月的作用中的虛擬變數。 請注意，當您引入因數變數到模型，hello 截距必須計算。 如果您不這樣做，hello 公式是過度指定 R 將卸除其中一個 hello 預期因素，但保留 hello 截距項。

由於我們有令人滿意的趨勢模型，我們就可以使用 hello`update()`函式 tooadd hello 新條款 toohello 現有模型。 hello 更新公式中的 hello-1 會卸除 hello 截距項。 延續中 RStudio hello 時間：

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

這會產生下列 hello。

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

我們看到該 hello 模型不會再有截距項並具有 12 個重要的月份因素。 這就是我們要 toosee。

讓我們進行另一個時間序列繪製 hello 加州日常的實際執行資料 toosee hello 季節性模型使用的程度。 加入下列程式碼在 hello Azure Machine Learning 中的 hello[執行 R 指令碼][ execute-r-script] toocreate hello 模型，然後進行繪圖。

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

Azure Machine Learning 中執行此程式碼會產生 hello 盒狀圖 24 所示。

![模型包含季節性效果的加州牛奶產量](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

*圖 24.模型包含季節性效果的加州牛奶產量。*

hello 調整的 toohello 資料顯示在圖 24 為而不是令人滿意。 Hello 趨勢及 hello 季節性效果 （每月的變化） 的外觀合理。

在我們的模型上的另一個檢查，讓我們看一下 hello 剩餘數。 hello 下列程式碼計算 hello 從我們的兩個模型的預測的值、 計算 hello 殘 hello 季節性的模型，並再繪製這些殘 hello 訓練資料。

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

顯示 hello 剩餘盒狀圖 25。

![剩餘數的 hello 季節性 hello 定型資料模型](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

*圖 25.剩餘的 hello 定型資料的 hello 季節性模型數。*

這些殘差看起來相當合理。 沒有特定結構，除了 hello 2008 2009年經歷，我們的模型並不考慮 hello 效果特別好。

hello 盒狀圖 25 所示適用於在 hello 殘中偵測到任何時間相依模式。 hello 的計算並繪製用 hello 剩餘數的明確方式置於 hello 繪圖區上的時間順序的 hello 剩餘數。 如果在 hello 相反地，我必須繪製`milk.lm$residuals`，hello 繪圖不已經按照時間順序。

您也可以使用`plot.lm()`tooproduce 一系列診斷繪圖。

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

此程式碼會產生一系列診斷圖，如圖 26 所示。

![診斷繪圖 hello 季節性模型中的第一個](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![第二個診斷繪圖 hello 季節性模型](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![第三個診斷繪圖 hello 季節性模型](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![第四個的 hello 季節性模型診斷的繪圖](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

*圖 26.診斷繪製 hello 季節性的模型。*

有幾個高影響力點中這些的繪圖，但不是識別 toocause 相當大的問題。 此外，我們可以看到從 hello 一般 Q Q 繪圖 hello 殘會關閉 toonormally 分散，線性模型是很重要的假設。

### <a name="forecasting-and-model-evaluation"></a>預測和模型評估
沒有一個多個項目 toodo toocomplete 我們的範例。 我們需要 toocompute 預測，並針對 hello 實際資料測量 hello 錯誤。 我們預測將會 hello 12 個月的 2013年。 我們可以計算此預測的 toohello 實際資料不是我們的定型資料集的一部分的錯誤量值。 此外，我們可以比較效能 hello 18 歲定型資料 toohello 12 個月的測試資料。  

可用的幾個度量的時間序列模型 toomeasure hello 效能。 在我們的案例中，我們將使用 hello 均方根 (RMS) 錯誤。 hello 下列函數會計算兩個數列間的 hello RMS 錯誤。  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

如同 hello`log.transform()`函式中我們討論 hello"的值轉換 」 一節，有很多錯誤檢查和例外狀況復原程式碼，在這個函式。 採用 hello 原則是 hello 相同。 hello 工作都是在兩個地方包裝在`tryCatch()`。 首先，hello 時間序列都是 exponentiated，因為我們已使用的 hello 值 hello 記錄檔。 第二，計算 hello 實際 RMS 錯誤。  

配備函式 toomeasure hello RMS 錯誤，我們會建置並輸出包含 hello RMS 錯誤的資料框架。 我們將包括 hello 趨勢單獨針對模型詞彙和 hello 完整模型以季節性的因素。 hello 下列程式碼沒有 hello 作業使用兩個 hello 我們建構線性模型。

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

執行此程式碼會產生 hello 輸出顯示在圖 27 hello 結果資料集輸出連接埠。

![RMS 錯誤 hello 模型的比較][26]

*圖 27.RMS 錯誤 hello 模型的比較。*

從這些結果中，我們看到，加入 hello 季節性因素 toohello 模型可減少 hello RMS 錯誤明顯。 不太令 hello 定型資料的 hello RMS 錯誤元小於 hello 預測。

## <a id="appendixa"></a>附錄 a： 指南 tooRStudio
RStudio 已經很完善記載，因此本附錄中，我會提供一些連結 toohello hello RStudio 文件 tooget 您啟動主要區段。

1. 建立專案
   
   您可以使用 RStudio，以專案方式組織和管理您的 R 程式碼。 使用專案的 hello 文件可以位於 https://support.rstudio.com/hc/articles/200526207-Using-Projects。
   
   建議您遵循這些指示，並在此文件中建立 hello R 程式碼範例的專案。  
2. 編輯和執行 R 程式碼
   
   RStudio 提供一個可編輯和執行 R 程式碼的整合式環境。 您可以在下列網址找到相關文件：https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code。
3. Debugging
   
   RStudio 包含強大的偵錯功能。 下列網址提供這些功能的相關文件：https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio。
   
   hello 中斷點疑難排解功能會記載於 https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting。

## <a id="appendixb"></a>附錄 B：進階閱讀
此 R 程式設計教學課程涵蓋 hello 基本概念的需要 toouse hello 與 Azure Machine Learning Studio 的 R 語言。 如果您不熟悉 R，CRAN 有提供兩本簡介：

* 為初學者所設計的 Emmanuel Paradis R 是很好的起點 toostart http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf 在。  
* 由 W N 簡介導覽 Venables et.  所著的《An Introduction to R》 提供略為深入的探討，網址為 http://cran.r-project.org/doc/manuals/R-intro.html。

有許多 R 的相關書籍可以協助您輕鬆上手。 以下是一些我認為實用的書籍：

* 封面 R 程式設計的 hello: 教學課程的統計軟體設計諾曼 Matloff 是絕佳的簡介 tooprogramming  
* R Cookbook Paul Teetor 所提供的問題和解決方案方法 toousing。  
* Robert Kabacoff 所著的《R in Action》是另一本實用的簡介書籍。 hello 附屬快速 R 網站是在 http://www.statmethods.net/ 實用的資源。
* 由 Patrick Burns R 煉獄是出乎意料幽默的書籍數目 r hello 活頁簿中的程式設計時可能遇到的複雜且困難主題處理是可免費從 http://www.burns-stat.com/documents/books/the-r-inferno/。
* 如果您想在 R 中的進階主題深入探討，看看 hello 進階 R Hadley Wickham 由活頁簿。 可以免費在 http://adv-r.had.co.nz/ 上這本書的 hello 線上版本。

時間序列的 R 封裝的目錄可以在 hello CRAN 工作檢視時間序列分析： http://cran.r-project.org/web/views/TimeSeries.html。 如需特定的時間序列物件的封裝，您應該參閱 toohello 文件，該套件。

hello 活頁簿與 R Paul Cowpertwait 和 Andrew Metcalfe 簡介時間序列提供時間序列分析簡介 toousing R。 許多理論文本皆有提供 R 範例。

一些絕佳的網際網路資源：

* DataCamp: DataCamp 教導 R hello 舒適度視訊課程與程式碼撰寫練習在瀏覽器中。 有 hello 最新的 R 技巧和封裝上的互動式教學課程。 在 https://www.datacamp.com/courses/introduction-to-r 拍攝 hello 可用互動式 R 教學課程
* 有關從 Programiz 開始使用 R 的指南：https://www.programiz.com/r-programming
* Clarkson 大學 Kelly Black 提供的快速 R 教學課程：http://www.cyclismo.org/tutorial/R/
* http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html 列出 60 個以上的 R 資源

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

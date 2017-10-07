---
title: "aaaExecute Python 機器學習指令碼 |Microsoft 文件"
description: "概述 Azure Machine Learning 中對於 Python 指令碼目前支援基礎之下的設計原則，以及基本使用案例、功能及限制。"
keywords: "python 機器學習服務,pandas,python pandas,python 指令碼, 執行 python 指令碼"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ee9eb764-0d3e-4104-a797-19fc29345d39
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bradsev
ms.openlocfilehash: 8d23aaa972a46cb1a07ea0f18cc1e24933fe3e6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a>在 Azure Machine Learning Studio 中執行 Python 機器學習服務指令碼

本主題描述基礎 hello Azure Machine Learning 中的 Python 指令碼目前支援的 hello 設計原則。 也說明了 hello 所提供的主要功能，包括：

- 執行基本的使用方式案例
- 為 Web 服務中的實驗評分
- 支援匯入現有的程式碼
- 匯出視覺效果
- 執行受監督的功能選取
- 了解部分限制

[Python](https://www.python.org/)是不可或缺的工具中的許多資料科學家 hello 工具箱子。 其中包含：

* 優雅簡潔的語法， 
* 跨平台支援， 
* 大量功能強大的程式庫集合，以及 
* 臻致完善的開發工具。 

Python 是在工作流程的所有階段中使用 (通常使用於機器學習模型化)：

- 資料內嵌和處理 
- 功能建構
- 模型訓練 
- 模型驗證
- 部署的 hello 模型

Azure Machine Learning Studio 支援將 Python 指令碼內嵌至機器學習實驗的各個部分，並且順暢地將其發佈為 Microsoft Azure 上的 Web 服務。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a>在 Machine Learning 中設計 Python 指令碼的原則

Azure Machine Learning Studio 中的 hello 主要介面 tooPython 是透過 hello[執行 Python 指令碼][ execute-python-script]圖 1 所示的模組。

![image1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![image2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

圖 1. hello**執行 Python 指令碼**模組。

hello[執行 Python 指令碼][ execute-python-script] Azure ML Studio 中的模組接受向上 toothree 輸入，並產生向上 tootwo 輸出 （hello 之後 > 一節中討論），其 R 的類比，像是 hello [執行 R 指令碼][ execute-r-script]模組。 hello 執行 Python 程式碼 toobe 是 hello 參數中輸入特殊命名為進入點函式，呼叫`azureml_main`。 以下是 hello 原則使用 tooimplement 本單元的重要設計：

1. *必須是 Python 使用者慣用的。* 大多數 Python 使用者將其程式碼視為模組中的函式。 因此，將大量的可執行陳述式放在最上層的模組相當罕見。 如此一來，hello 指令碼 方塊也會採用特殊命名的 Python 函式做為相對於 toojust 陳述式的序列。 hello hello 函式中公開的物件是標準的 Python 程式庫類型例如[熊](http://pandas.pydata.org/)資料框架和[NumPy](http://www.numpy.org/)陣列。
2. *必須在本機和雲端執行之間具有高畫質。* hello 後端使用 tooexecute hello Python 程式碼根據[Anaconda](https://store.continuum.io/cshop/anaconda/)、 廣泛使用跨平台科學 Python 的散發。 它隨附關閉 too200 的 hello 最常見的 Python 封裝。 因此，資料科學家可在其本機 Azure Machine Learning 相容的 Anaconda 環境中，對程式碼進行偵錯與限定。 然後使用現有的開發環境，例如[IPython](http://ipython.org/)筆記型電腦或[Python Tools for Visual Studio](http://aka.ms/ptvs)，toorun 做為 Azure ML 實驗的一部分。 hello`azureml_main`進入點是香草 Python 函式，因此 * * * Azure ML 專屬的程式碼不可以用來撰寫或 hello 安裝 SDK。
3. *必須可以順暢地與其他 Azure Machine Learning 模組組合。* hello[執行 Python 指令碼][ execute-python-script]模組接受，做為輸入及輸出，標準 Azure Machine Learning 資料集。 hello 基礎架構明確而有效率地橋接器 hello Azure ML 和 Python 執行階段。 因此，Python 可以用於與現有 Azure ML 工作流程接合，包括呼叫 R 和 SQLite 的那些工作流程。 因此，資料科學家可以撰寫執行下列工作的工作流程：
   * 使用 Python 和 Pandas 進行資料前處理和清除
   * 摘要 hello 資料 tooa SQL 轉換，聯結多個資料集 tooform 功能
   * 使用 Azure Machine Learning 中的 hello 演算法定型模型 
   * 評估並使用 r 的 hello 結果進行後置處理


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a>ML 中 Python 指令碼的基本使用案例

在本節中，我們的問卷的部分 hello 基本用法的 hello[執行 Python 指令碼][ execute-python-script]模組。 輸入 toohello Python 模組會公開為熊資料框架。 hello 函式必須傳回單一熊資料框架內 Python 封裝[順序](https://docs.python.org/2/c-api/sequence.html)例如 tuple、 清單或 NumPy 陣列。 hello 第一個輸出連接埠 hello 模組然後就會傳回 hello 這個序列的第一個項目。 此配置顯示在「圖 2」中。

![image3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

圖 2. 輸入連接埠 tooparameters 和傳回值 toooutput 連接埠的對應。

詳細的 hello 輸入連接埠如何取得對應的 hello tooparameters 語意`azureml_main`函式 資料表 1 所示：

![image1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

表 1. 輸入連接埠 toofunction 參數的對應。

輸入連接埠與函式參數之間的 hello 對應是位置性：

- hello 第一個連接輸入連接埠是對應的 toohello hello 函式的第一個參數。 
- hello 第二個輸入 （如果連接） 是對應的 toohello hello 函式的第二個參數。

請參閱*資料分析的 Python* (O'Reilly 2012) 由西部 McKinney 如需詳細資訊和如何它可以是使用的 toomanipulate 資料有效地和 Python 熊上。 


## <a name="translation-of-input-and-output-types"></a>輸入和輸出類型的轉譯 
在 Azure ML 的輸入資料集是轉換的 toodata 框架熊中。 輸出資料框架會轉換後 tooAzure ML 資料集。 請執行下列轉換 hello:

1. 字串和數值資料行轉換成-為資料集內的遺漏值，而 已轉換的 too'NA' 熊中的值。 hello 相同轉換發生在 hello 回溯 （熊 NA 值是在 Azure ML 轉換的 toomissing 值）。
2. Azure ML 不支援 Pandas 中的索引向量。 Hello Python 函式中的所有輸入的資料框架一律有 0 toohello 資料列數目減 1 的 64 位元數字索引。 
3. Azure ML 資料集無法具有重複的資料行名稱或非字串的資料行名稱。 如果輸出資料框架中包含非數值資料行，hello 架構會呼叫`str`hello 資料行名稱。 同樣地，任何重複的資料行名稱都是自動 mangled 的 tooinsure hello 名稱是唯一的。 hello 尾碼 (2) 新增 toohello 第一個重複項目、 (3) toohello 第二個重複項目，依此類推。


## <a name="operationalizing-python-scripts"></a>運作 Python 指令碼

當評分實驗中使用的任何[執行 Python 指令碼][execute-python-script]模組發佈為 Web 服務時，系統會呼叫這些模組。 例如，圖 3 顯示包含 hello 程式碼 tooevaluate 單一 Python 運算式計分實驗。 

![image4](./media/machine-learning-execute-python-scripts/figure3a.png)

![image5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

圖 3. 用以評估 Python 運算式的 Web 服務。

從此實驗建立的 Web 服務：

- 會將 Python 運算式作為輸入 (字串)
- 將它傳送 toohello Python 解譯器 
- 傳回表格，內含 hello 運算式和 hello 評估結果。


## <a name="importing-existing-python-script-modules"></a>匯入現有的 Python 指令碼模組

常見使用案例的許多資料科學家是 tooincorporate 現有 Python 指令碼 Azure ML 實驗。 而不是要求所有的程式碼即將串連並貼到單一指令碼 方塊，hello[執行 Python 指令碼][ execute-python-script]模組接受包含在 hello 第三個輸入連接埠的 Python 模組 zip 檔案。 hello 檔案會解壓縮 hello 執行架構，在執行階段和 hello 內容加入 toohello hello Python 解譯器程式庫路徑。 hello`azureml_main`函式可以再直接匯入這些模組的進入點。

例如，請考慮 hello 檔案 Hello.py 包含簡單的"Hello，World"函式。

![image6](./media/machine-learning-execute-python-scripts/figure4.png)

圖 4. Hello.py 檔案中的使用者定義函式。

接下來，我們會建立包含 Hello.py 的 Hello.zip 檔案：

![image7](./media/machine-learning-execute-python-scripts/figure5.png)

圖 5. 包含使用者定義 Python 程式碼的 Zip 檔案。

做為資料集 hello zip 檔案上傳至 Azure Machine Learning Studio。 然後建立並執行的實驗使用 hello Hello.zip 檔案中的 hello Python 程式碼，方法是將它附加 toohello 第三個輸入連接埠的 hello**執行 Python 指令碼**模組，如本圖所示。

![image8](./media/machine-learning-execute-python-scripts/figure6a.png)

![image9](./media/machine-learning-execute-python-scripts/figure6b.png)

圖 6. 範例實驗，具有上傳為 zip 檔案的使用者定義 Python 程式碼。

hello 模組輸出會顯示該 hello zip 檔已解除封裝及該 hello 函式`print_hello`已執行。
 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)

圖 7. Hello 內的使用中的使用者定義函數[執行 Python 指令碼][ execute-python-script]模組。


## <a name="working-with-visualizations"></a>使用視覺效果

建立 hello 瀏覽器上使用 MatplotLib 可以視覺化的繪圖可以傳回 hello[執行 Python 指令碼][execute-python-script]。 但是 hello 繪圖不自動重新導向的 tooimages 如時使用。因此 hello 使用者必須明確儲存任何繪圖 tooPNG 檔案有 toobe 傳回後 tooAzure 機器學習。 

MatplotLib toogenerate 映像，您必須完成下列程序的 hello:

* 切換 hello 後端 」 彙總 」 從 hello 太預設 Qt 為基礎的轉譯器 
* 建立新的圖表物件 
* 取得 hello 座標軸，並產生到它所有的繪圖 
* 儲存 hello 圖 tooa PNG 檔案 

此程序是以 hello 遵循建立散佈圖矩陣中熊使用 hello scatter_matrix 函式的圖 8 所示。

![image1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

圖 8. 程式碼的 toosave MatplotLib 圖 tooimages。

圖 9 顯示的實驗使用先前所示 tooreturn 繪製從 hello 第二個輸出連接埠傳送的 hello 指令碼。

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

圖 9. 視覺化從 Python 程式碼產生的繪圖。

可能的 tooreturn 多個圖表將其儲存到不同的映像、 hello Azure 機器學習服務執行階段拾取所有映像並將它們串連視覺效果。


## <a name="advanced-examples"></a>進階範例

安裝 Azure Machine Learning 中的 hello Anaconda 環境包含常見的封裝，例如 NumPy、 SciPy 和 Scikits-learn。 這些套件可以有效地用於機器學習管線中的各種資料處理工作。 例如，hello 下列實驗和指令碼說明 hello 用途中 Scikits-learn toocompute 功能重要性分數的集團學習模組資料集。 hello 分數可以是使用的 tooperform 監督式特徵選取之前饋送至另一個 ML 模型。

以下是 hello Python 用函式 toocompute hello 重要性分數和根據 hello 分數的順序 hello 功能：

![image11](./media/machine-learning-execute-python-scripts/figure8.png)

圖 10. 函式 toorank 功能分數。
 hello 下列實驗計算，然後在 Azure Machine Learning 中的 hello"Pima 印度洋糖尿病"資料集中傳回 hello 重要性分數的功能：

![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)    

圖 11. 實驗 toorank hello Pima 印度洋糖尿病資料集中的功能。

## <a name="limitations"></a>限制
hello[執行 Python 指令碼][ execute-python-script]目前有下列限制的 hello:

1. *沙箱化執行。* hello Python 執行階段目前沙箱化，如此一來，不允許存取 toohello 網路或 toohello 本機檔案系統中以持續方式。 儲存在本機的所有檔案會隔離，並 hello 模組完成之後刪除。 hello Python 程式碼無法執行該 hello 機器上的大部分目錄的存取，目前的目錄和子目錄 hello 例外狀況正在 hello。
2. *缺少精細的開發和偵錯支援。* hello Python 模組目前不支援 intellisense 和偵錯等 IDE 功能。 此外，如果 hello 模組在執行階段，hello 完整 Python 堆疊追蹤會提供。 但是，它必須在 hello hello 模組的輸出記錄檔中的檢視。 目前建議您開發及偵錯這類 IPython 的環境中的 Python 指令碼，然後匯入 hello 模組的 hello 程式碼。
3. *單一資料框架輸出。* hello Python 進入點是只允許的 tooreturn 單一資料框架，做為輸出。 它不是目前 tooreturn 任意 Python 物件，例如定型的模型直接回 toohello Azure 機器學習服務執行階段。 像[執行 R 指令碼][execute-r-script]，其具有 hello 很可能在許多情況下 toopickle 物件至位元組陣列，然後再回頭執行資料框架內，相同的限制。
4. *無法 toocustomize Python 安裝*。 目前，hello 只有方式 tooadd 自訂 Python 模組是透過 hello zip 檔案機制稍早所述。 對於小模組可行，但是對於大模組 (特別是具有原生 DLL 的模組) 和大量模組而言則顯得繁瑣。 

## <a name="conclusions"></a>結論
hello[執行 Python 指令碼][ execute-python-script]模組可讓資料科學家 tooincorporate 現有 Python 程式碼在 Azure 機器學習和 tooseamlessly 的雲端裝載的機器學習工作流程實施它們做為 web 服務的一部分。 hello Python 指令碼模組可與 Azure Machine Learning 中的其他模組自然互通。 hello 模組可以用於許多工作，從 資料瀏覽 toopre 處理及擷取特徵，然後 tooevaluation 和 hello 結果的後續處理。 用於執行 hello 後端執行階段為基礎 Anaconda，經過完整測試也廣泛使用的 Python 發佈。 這個後端可簡化您的現有程式碼資產 tooon 面板到 hello 的雲端。

我們預期 tooprovide 額外的功能 toohello[執行 Python 指令碼][ execute-python-script]模組例如 hello 能力 tootrain 實施模型以 Python 和 tooadd 更佳的 hello 支援開發和偵錯在 Azure Machine Learning Studio 中的程式碼。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 hello [Python 開發人員中心](https://azure.microsoft.com/develop/python/)。

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

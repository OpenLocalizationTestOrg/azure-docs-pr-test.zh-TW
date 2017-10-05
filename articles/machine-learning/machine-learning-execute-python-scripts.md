---
title: "執行 Python 機器學習服務指令碼 | Microsoft Docs"
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
ms.openlocfilehash: e8d6377bc939e6711a96e521b5f574fc8d060929
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a><span data-ttu-id="80003-104">在 Azure Machine Learning Studio 中執行 Python 機器學習服務指令碼</span><span class="sxs-lookup"><span data-stu-id="80003-104">Execute Python machine learning scripts in Azure Machine Learning Studio</span></span>

<span data-ttu-id="80003-105">本主題說明 Azure Machine Learning 中對於 Python 指令碼目前支援基礎之下的設計原則。</span><span class="sxs-lookup"><span data-stu-id="80003-105">This topic describes the design principles underlying the current support for Python scripts in Azure Machine Learning.</span></span> <span data-ttu-id="80003-106">也說明了所提供的主要功能，包括：</span><span class="sxs-lookup"><span data-stu-id="80003-106">The main capabilities provided are also outlined, including:</span></span>

- <span data-ttu-id="80003-107">執行基本的使用方式案例</span><span class="sxs-lookup"><span data-stu-id="80003-107">execute basic usage scenarios</span></span>
- <span data-ttu-id="80003-108">為 Web 服務中的實驗評分</span><span class="sxs-lookup"><span data-stu-id="80003-108">score an experiment in a web service</span></span>
- <span data-ttu-id="80003-109">支援匯入現有的程式碼</span><span class="sxs-lookup"><span data-stu-id="80003-109">support for importing existing code</span></span>
- <span data-ttu-id="80003-110">匯出視覺效果</span><span class="sxs-lookup"><span data-stu-id="80003-110">export visualizations</span></span>
- <span data-ttu-id="80003-111">執行受監督的功能選取</span><span class="sxs-lookup"><span data-stu-id="80003-111">perform supervised feature selection</span></span>
- <span data-ttu-id="80003-112">了解部分限制</span><span class="sxs-lookup"><span data-stu-id="80003-112">understand some limitations</span></span>

<span data-ttu-id="80003-113">[Python](https://www.python.org/) 是許多資料科學家工具櫃中不可或缺的工具。</span><span class="sxs-lookup"><span data-stu-id="80003-113">[Python](https://www.python.org/) is an indispensable tool in the tool chest of many data scientists.</span></span> <span data-ttu-id="80003-114">其中包含：</span><span class="sxs-lookup"><span data-stu-id="80003-114">It has:</span></span>

* <span data-ttu-id="80003-115">優雅簡潔的語法，</span><span class="sxs-lookup"><span data-stu-id="80003-115">an elegant and concise syntax,</span></span> 
* <span data-ttu-id="80003-116">跨平台支援，</span><span class="sxs-lookup"><span data-stu-id="80003-116">cross-platform support,</span></span> 
* <span data-ttu-id="80003-117">大量功能強大的程式庫集合，以及</span><span class="sxs-lookup"><span data-stu-id="80003-117">a vast collection of powerful libraries, and</span></span> 
* <span data-ttu-id="80003-118">臻致完善的開發工具。</span><span class="sxs-lookup"><span data-stu-id="80003-118">mature development tools.</span></span> 

<span data-ttu-id="80003-119">Python 是在工作流程的所有階段中使用 (通常使用於機器學習模型化)：</span><span class="sxs-lookup"><span data-stu-id="80003-119">Python is being used in all phases of a workflow typically used in machine learning modeling:</span></span>

- <span data-ttu-id="80003-120">資料內嵌和處理</span><span class="sxs-lookup"><span data-stu-id="80003-120">data ingest and processing</span></span> 
- <span data-ttu-id="80003-121">功能建構</span><span class="sxs-lookup"><span data-stu-id="80003-121">feature construction</span></span>
- <span data-ttu-id="80003-122">模型訓練</span><span class="sxs-lookup"><span data-stu-id="80003-122">model training</span></span> 
- <span data-ttu-id="80003-123">模型驗證</span><span class="sxs-lookup"><span data-stu-id="80003-123">model validation</span></span>
- <span data-ttu-id="80003-124">模型部署</span><span class="sxs-lookup"><span data-stu-id="80003-124">deployment of the models</span></span>

<span data-ttu-id="80003-125">Azure Machine Learning Studio 支援將 Python 指令碼內嵌至機器學習實驗的各個部分，並且順暢地將其發佈為 Microsoft Azure 上的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="80003-125">Azure Machine Learning Studio supports embedding Python scripts into various parts of a machine learning experiment and also seamlessly publishing them as web services on Microsoft Azure.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a><span data-ttu-id="80003-126">在 Machine Learning 中設計 Python 指令碼的原則</span><span class="sxs-lookup"><span data-stu-id="80003-126">Design principles of Python scripts in Machine Learning</span></span>

<span data-ttu-id="80003-127">在 Azure Machine Learning Studio 中，存取 Python 的主要介面是透過圖 1 所示的[執行 Python 指令碼][execute-python-script]模組。</span><span class="sxs-lookup"><span data-stu-id="80003-127">The primary interface to Python in Azure Machine Learning Studio is via the [Execute Python Script][execute-python-script] module shown in Figure 1.</span></span>

![image1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![image2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

<span data-ttu-id="80003-130">圖 1.</span><span class="sxs-lookup"><span data-stu-id="80003-130">Figure 1.</span></span> <span data-ttu-id="80003-131">**執行 Python 指令碼** 模組。</span><span class="sxs-lookup"><span data-stu-id="80003-131">The **Execute Python Script** module.</span></span>

<span data-ttu-id="80003-132">Azure ML Studio 中的[執行 Python 指令碼][execute-python-script]模組最多接受三個輸入，而且最多產生兩個輸出 (於下一節中討論)，就像其同類的 R 一樣：[執行 R 指令碼][execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="80003-132">The [Execute Python Script][execute-python-script] module in Azure ML Studio accepts up to three inputs and produces up to two outputs (discussed in the following section), like its R analogue, the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="80003-133">要執行的 Python 程式碼會輸入至稱為 `azureml_main` 之特殊命名進入點函式的參數方塊。</span><span class="sxs-lookup"><span data-stu-id="80003-133">The Python code to be executed is entered into the parameter box as a specially named entry-point function called `azureml_main`.</span></span> <span data-ttu-id="80003-134">以下是用來實作此模組的關鍵設計原則：</span><span class="sxs-lookup"><span data-stu-id="80003-134">Here are the key design principles used to implement this module:</span></span>

1. <span data-ttu-id="80003-135">*必須是 Python 使用者慣用的。*</span><span class="sxs-lookup"><span data-stu-id="80003-135">*Must be idiomatic for Python users.*</span></span> <span data-ttu-id="80003-136">大多數 Python 使用者將其程式碼視為模組中的函式。</span><span class="sxs-lookup"><span data-stu-id="80003-136">Most Python users factor their code as functions inside modules.</span></span> <span data-ttu-id="80003-137">因此，將大量的可執行陳述式放在最上層的模組相當罕見。</span><span class="sxs-lookup"><span data-stu-id="80003-137">So putting a lot of executable statements in a top-level module is relatively rare.</span></span> <span data-ttu-id="80003-138">因此，指令碼方塊也會採用特殊命名的 Python 函數，而不是採用一系列的陳述式。</span><span class="sxs-lookup"><span data-stu-id="80003-138">As a result, the script box also takes a specially named Python function as opposed to just a sequence of statements.</span></span> <span data-ttu-id="80003-139">在函式中公開的物件是標準 Python 程式庫類型 (例如 [Pandas](http://pandas.pydata.org/)資料框架和 [NumPy](http://www.numpy.org/) 陣列)。</span><span class="sxs-lookup"><span data-stu-id="80003-139">The objects exposed in the function are standard Python library types such as [Pandas](http://pandas.pydata.org/) data frames and [NumPy](http://www.numpy.org/) arrays.</span></span>
2. <span data-ttu-id="80003-140">*必須在本機和雲端執行之間具有高畫質。*</span><span class="sxs-lookup"><span data-stu-id="80003-140">*Must have high-fidelity between local and cloud executions.*</span></span> <span data-ttu-id="80003-141">用來執行 Python 程式碼的後端是以 [Anaconda](https://store.continuum.io/cshop/anaconda/) (廣為使用的跨平台科學 Python 發行版本) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="80003-141">The backend used to execute the Python code is based on [Anaconda](https://store.continuum.io/cshop/anaconda/), a widely used cross-platform scientific Python distribution.</span></span> <span data-ttu-id="80003-142">它隨附將近 200 個最常見的 Python 套件。</span><span class="sxs-lookup"><span data-stu-id="80003-142">It comes with close to 200 of the most common Python packages.</span></span> <span data-ttu-id="80003-143">因此，資料科學家可在其本機 Azure Machine Learning 相容的 Anaconda 環境中，對程式碼進行偵錯與限定。</span><span class="sxs-lookup"><span data-stu-id="80003-143">Therefore, data scientists can debug and qualify their code on their local Azure Machine Learning-compatible Anaconda environment.</span></span> <span data-ttu-id="80003-144">然後使用現有的開發環境 (例如 [IPython](http://ipython.org/) 筆記本或[適用於 Visual Studio 的 Python 工具](http://aka.ms/ptvs)) 來執行它，以作為 Azure ML 實驗的一部分執行。</span><span class="sxs-lookup"><span data-stu-id="80003-144">Then use an existing development environment, such as [IPython](http://ipython.org/) notebook or [Python Tools for Visual Studio](http://aka.ms/ptvs), to run it as part of an Azure ML experiment.</span></span> <span data-ttu-id="80003-145">此外，`azureml_main` 進入點是原始 Python 函式，因此****不需要 Azure ML 特定程式碼或安裝 SDK 即可編寫。</span><span class="sxs-lookup"><span data-stu-id="80003-145">The `azureml_main` entry point is a vanilla Python function and so ****can be authored without Azure ML-specific code or the SDK installed.</span></span>
3. <span data-ttu-id="80003-146">*必須可以順暢地與其他 Azure Machine Learning 模組組合。*</span><span class="sxs-lookup"><span data-stu-id="80003-146">*Must be seamlessly composable with other Azure Machine Learning modules.*</span></span> <span data-ttu-id="80003-147">[執行 Python 指令碼][execute-python-script]模組接受標準 Azure Machine Learning 資料集作為輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="80003-147">The [Execute Python Script][execute-python-script] module accepts, as inputs and outputs, standard Azure Machine Learning datasets.</span></span> <span data-ttu-id="80003-148">底層架構明確而有效率地橋接了 Azure ML 和 Python 執行階段。</span><span class="sxs-lookup"><span data-stu-id="80003-148">The underlying framework transparently and efficiently bridges the Azure ML and Python runtimes.</span></span> <span data-ttu-id="80003-149">因此，Python 可以用於與現有 Azure ML 工作流程接合，包括呼叫 R 和 SQLite 的那些工作流程。</span><span class="sxs-lookup"><span data-stu-id="80003-149">So Python can be used in conjunction with existing Azure ML workflows, including those that call into R and SQLite.</span></span> <span data-ttu-id="80003-150">因此，資料科學家可以撰寫執行下列工作的工作流程：</span><span class="sxs-lookup"><span data-stu-id="80003-150">A  result, data scientist could compose workflows that:</span></span>
   * <span data-ttu-id="80003-151">使用 Python 和 Pandas 進行資料前處理和清除</span><span class="sxs-lookup"><span data-stu-id="80003-151">use Python and Pandas for data pre-processing and cleaning</span></span>
   * <span data-ttu-id="80003-152">將資料饋送至 SQL 轉換、聯結多個資料集以形成功能</span><span class="sxs-lookup"><span data-stu-id="80003-152">feed the data to a SQL transformation, joining multiple datasets to form features</span></span>
   * <span data-ttu-id="80003-153">使用 Azure Machine Learning 中的演算法來訓練模型</span><span class="sxs-lookup"><span data-stu-id="80003-153">train models using the algorithms in Azure Machine Learning</span></span> 
   * <span data-ttu-id="80003-154">使用 R 評估和後處理結果。</span><span class="sxs-lookup"><span data-stu-id="80003-154">evaluate and post-process the results using R.</span></span>


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a><span data-ttu-id="80003-155">ML 中 Python 指令碼的基本使用案例</span><span class="sxs-lookup"><span data-stu-id="80003-155">Basic usage scenarios in ML for Python scripts</span></span>

<span data-ttu-id="80003-156">在本節中，我們調查[執行 Python 指令碼][execute-python-script]模組的一些基本用法。</span><span class="sxs-lookup"><span data-stu-id="80003-156">In this section, we survey some of the basic uses of the [Execute Python Script][execute-python-script] module.</span></span> <span data-ttu-id="80003-157">對 Python 模組的任何輸入都會公開為 Pandas 資料框架。</span><span class="sxs-lookup"><span data-stu-id="80003-157">Inputs to the Python module are exposed as Pandas data frames.</span></span> <span data-ttu-id="80003-158">函式必須傳回在 Python [序列](https://docs.python.org/2/c-api/sequence.html) (例如 tuple、清單或 NumPy 陣列) 內封裝的單一 Pandas 資料框架。</span><span class="sxs-lookup"><span data-stu-id="80003-158">The function must return a single Pandas data frame packaged inside of a Python [sequence](https://docs.python.org/2/c-api/sequence.html) such as a tuple, list, or NumPy array.</span></span> <span data-ttu-id="80003-159">然後會在模組的第一個輸出連接埠中傳回此序列的第一個元素。</span><span class="sxs-lookup"><span data-stu-id="80003-159">The first element of this sequence is then returned in the first output port of the module.</span></span> <span data-ttu-id="80003-160">此配置顯示在「圖 2」中。</span><span class="sxs-lookup"><span data-stu-id="80003-160">This scheme is shown in Figure 2.</span></span>

![image3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

<span data-ttu-id="80003-162">圖 2.</span><span class="sxs-lookup"><span data-stu-id="80003-162">Figure 2.</span></span> <span data-ttu-id="80003-163">將輸入連接埠對應至參數，並且將值傳回至輸出連接埠。</span><span class="sxs-lookup"><span data-stu-id="80003-163">Mapping of input ports to parameters and return value to output port.</span></span>

<span data-ttu-id="80003-164">輸入連接埠如何對應至 `azureml_main` 函數的參數的更詳細語意如「表 1」所示：</span><span class="sxs-lookup"><span data-stu-id="80003-164">More detailed semantics of how the input ports get mapped to parameters of the `azureml_main` function are shown in Table 1:</span></span>

![image1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

<span data-ttu-id="80003-166">表 1.</span><span class="sxs-lookup"><span data-stu-id="80003-166">Table 1.</span></span> <span data-ttu-id="80003-167">將輸入連接埠對應至函數參數。</span><span class="sxs-lookup"><span data-stu-id="80003-167">Mapping of input ports to function parameters.</span></span>

<span data-ttu-id="80003-168">輸入連接埠和函式參數之間的對應是有位置關係的：</span><span class="sxs-lookup"><span data-stu-id="80003-168">The mapping between input ports and function parameters is positional:</span></span>

- <span data-ttu-id="80003-169">第一個連接的輸入連接埠會對應至函式的第一個參數。</span><span class="sxs-lookup"><span data-stu-id="80003-169">The first connected input port is mapped to the first parameter of the function.</span></span> 
- <span data-ttu-id="80003-170">第二個輸入連接埠 (如果連接) 會對應至函式的第二個參數。</span><span class="sxs-lookup"><span data-stu-id="80003-170">The second input (if connected) is mapped to the second parameter of the function.</span></span>

<span data-ttu-id="80003-171">如需 Python Pandas 以及如何以有效且有效率的方式使用它來處理資料的詳細資訊，請參閱 W. McKinney 所撰寫的 *Python for Data Analysis* (O'Reilly, 2012)。</span><span class="sxs-lookup"><span data-stu-id="80003-171">See *Python for Data Analysis* (O'Reilly, 2012) by W. McKinney for more information on Python Pandas and on how it can be used to manipulate data effectively and efficiently.</span></span> 


## <a name="translation-of-input-and-output-types"></a><span data-ttu-id="80003-172">輸入和輸出類型的轉譯</span><span class="sxs-lookup"><span data-stu-id="80003-172">Translation of input and output types</span></span> 
<span data-ttu-id="80003-173">Azure ML 中的輸入資料集會轉換為 Pandas 中的資料框架。</span><span class="sxs-lookup"><span data-stu-id="80003-173">Input datasets in Azure ML are converted to data frames in Pandas.</span></span> <span data-ttu-id="80003-174">輸出資料框架會轉換回 Azure ML 資料集。</span><span class="sxs-lookup"><span data-stu-id="80003-174">Output data frames are converted back to Azure ML datasets.</span></span> <span data-ttu-id="80003-175">會執行下列轉換：</span><span class="sxs-lookup"><span data-stu-id="80003-175">The following conversions are performed:</span></span>

1. <span data-ttu-id="80003-176">字串和數值資料行會如現狀轉換，資料集中的遺漏值則會在 Pandas 中轉換為 ‘NA’ 值。</span><span class="sxs-lookup"><span data-stu-id="80003-176">String and numeric columns are converted as-is and missing values in a dataset are converted to ‘NA’ values in Pandas.</span></span> <span data-ttu-id="80003-177">會在反向發生相同轉換 (Pandas 中的 NA 值會轉換為 Azure ML 中的遺漏值)。</span><span class="sxs-lookup"><span data-stu-id="80003-177">The same conversion happens on the way back (NA values in Pandas are converted to missing values in Azure ML).</span></span>
2. <span data-ttu-id="80003-178">Azure ML 不支援 Pandas 中的索引向量。</span><span class="sxs-lookup"><span data-stu-id="80003-178">Index vectors in Pandas are not supported in Azure ML.</span></span> <span data-ttu-id="80003-179">Python 函式中所有的輸入資料框架一律具有 64 位元的數值索引，範圍從 0 到資料列數目減 1。</span><span class="sxs-lookup"><span data-stu-id="80003-179">All input data frames in the Python function always have a 64-bit numerical index from 0 to the number of rows minus 1.</span></span> 
3. <span data-ttu-id="80003-180">Azure ML 資料集無法具有重複的資料行名稱或非字串的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="80003-180">Azure ML datasets cannot have duplicate column names and column names that are not strings.</span></span> <span data-ttu-id="80003-181">如果輸出資料框架包含非數值資料行，則架構會在資料行名稱上呼叫 `str` 。</span><span class="sxs-lookup"><span data-stu-id="80003-181">If an output data frame contains non-numeric columns, the framework calls `str` on the column names.</span></span> <span data-ttu-id="80003-182">同樣地，任何重複的資料行名稱會自動錯位，以確保名稱是唯一的。</span><span class="sxs-lookup"><span data-stu-id="80003-182">Likewise, any duplicate column names are automatically mangled to insure the names are unique.</span></span> <span data-ttu-id="80003-183">尾碼 (2) 會新增至第一個重複項目，尾碼 (3) 新增至第二個重複項目等等。</span><span class="sxs-lookup"><span data-stu-id="80003-183">The suffix (2) is added to the first duplicate, (3) to the second duplicate, and so on.</span></span>


## <a name="operationalizing-python-scripts"></a><span data-ttu-id="80003-184">運作 Python 指令碼</span><span class="sxs-lookup"><span data-stu-id="80003-184">Operationalizing Python scripts</span></span>

<span data-ttu-id="80003-185">當評分實驗中使用的任何[執行 Python 指令碼][execute-python-script]模組發佈為 Web 服務時，系統會呼叫這些模組。</span><span class="sxs-lookup"><span data-stu-id="80003-185">Any [Execute Python Script][execute-python-script] modules used in a scoring experiment are called when published as a web service.</span></span> <span data-ttu-id="80003-186">例如，「圖 3」顯示計分實驗，其中包含用以評估單一 Python 運算式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="80003-186">For example, Figure 3 shows a scoring experiment that contains the code to evaluate a single Python expression.</span></span> 

![image4](./media/machine-learning-execute-python-scripts/figure3a.png)

![image5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

<span data-ttu-id="80003-189">圖 3.</span><span class="sxs-lookup"><span data-stu-id="80003-189">Figure 3.</span></span> <span data-ttu-id="80003-190">用以評估 Python 運算式的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="80003-190">Web service for evaluating a Python expression.</span></span>

<span data-ttu-id="80003-191">從此實驗建立的 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="80003-191">A web service created from this experiment:</span></span>

- <span data-ttu-id="80003-192">會將 Python 運算式作為輸入 (字串)</span><span class="sxs-lookup"><span data-stu-id="80003-192">takes as input a Python expression (as a string)</span></span>
- <span data-ttu-id="80003-193">會將它傳送給 Python 解譯器</span><span class="sxs-lookup"><span data-stu-id="80003-193">sends it to the Python interpreter</span></span> 
- <span data-ttu-id="80003-194">會傳回包含運算式以及評估結果的表格。</span><span class="sxs-lookup"><span data-stu-id="80003-194">returns a table containing both the expression and the evaluated result.</span></span>


## <a name="importing-existing-python-script-modules"></a><span data-ttu-id="80003-195">匯入現有的 Python 指令碼模組</span><span class="sxs-lookup"><span data-stu-id="80003-195">Importing existing Python script modules</span></span>

<span data-ttu-id="80003-196">對於許多資料科學家，常見的使用案例是將現有 Python 指令碼併入 Azure ML 實驗。</span><span class="sxs-lookup"><span data-stu-id="80003-196">A common use-case for many data scientists is to incorporate existing Python scripts into Azure ML experiments.</span></span> <span data-ttu-id="80003-197">[執行 Python 指令碼][execute-python-script]模組不需要將所有程式碼串連並貼到單一指令碼方塊中，而是在第三個輸入連接埠接受包含 Python 模組的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="80003-197">Instead of requiring that all code be concatenated and pasted into a single script box, the [Execute Python Script][execute-python-script] module accepts a zip file that contains Python modules at the third input port.</span></span> <span data-ttu-id="80003-198">該檔案會由執行架構在執行階段解壓縮，且內容會新增至 Python 解譯器的程式庫路徑。</span><span class="sxs-lookup"><span data-stu-id="80003-198">The file is unzipped by the execution framework at runtime and the contents are added to the library path of the Python interpreter.</span></span> <span data-ttu-id="80003-199">然後 `azureml_main` 進入點函式可以直接匯入這些模組。</span><span class="sxs-lookup"><span data-stu-id="80003-199">The `azureml_main` entry point function can then import these modules directly.</span></span>

<span data-ttu-id="80003-200">作為範例，請考量包含簡單 “Hello, World” 函式的 Hello.py 檔案。</span><span class="sxs-lookup"><span data-stu-id="80003-200">As an example, consider the file Hello.py containing a simple “Hello, World” function.</span></span>

![image6](./media/machine-learning-execute-python-scripts/figure4.png)

<span data-ttu-id="80003-202">圖 4.</span><span class="sxs-lookup"><span data-stu-id="80003-202">Figure 4.</span></span> <span data-ttu-id="80003-203">Hello.py 檔案中的使用者定義函式。</span><span class="sxs-lookup"><span data-stu-id="80003-203">User-defined function in Hello.py file.</span></span>

<span data-ttu-id="80003-204">接下來，我們會建立包含 Hello.py 的 Hello.zip 檔案：</span><span class="sxs-lookup"><span data-stu-id="80003-204">Next, we create a file Hello.zip that contains Hello.py:</span></span>

![image7](./media/machine-learning-execute-python-scripts/figure5.png)

<span data-ttu-id="80003-206">圖 5.</span><span class="sxs-lookup"><span data-stu-id="80003-206">Figure 5.</span></span> <span data-ttu-id="80003-207">包含使用者定義 Python 程式碼的 Zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="80003-207">Zip file containing user-defined Python code.</span></span>

<span data-ttu-id="80003-208">將此 zip 檔案上傳至 Azure Machine Learning Studio 作為資料集。</span><span class="sxs-lookup"><span data-stu-id="80003-208">Upload the zip file as a dataset into Azure Machine Learning Studio.</span></span> <span data-ttu-id="80003-209">然後，建立並執行使用 Hello.zip 檔案中之 Python 程式碼的實驗，方法是將它附加到**執行 Python 指令碼**模組的第三個輸入連接埠，如此圖所示。</span><span class="sxs-lookup"><span data-stu-id="80003-209">Then create and run an experiment that uses the Python code in the Hello.zip file by attaching it to the third input port of the **Execute Python Script** module, as shown in this figure.</span></span>

![image8](./media/machine-learning-execute-python-scripts/figure6a.png)

![image9](./media/machine-learning-execute-python-scripts/figure6b.png)

<span data-ttu-id="80003-212">圖 6.</span><span class="sxs-lookup"><span data-stu-id="80003-212">Figure 6.</span></span> <span data-ttu-id="80003-213">範例實驗，具有上傳為 zip 檔案的使用者定義 Python 程式碼。</span><span class="sxs-lookup"><span data-stu-id="80003-213">Sample experiment with user-defined Python code uploaded as a zip file.</span></span>

<span data-ttu-id="80003-214">模組輸出顯示 zip 檔案已解除封裝，且函式 `print_hello` 已執行。</span><span class="sxs-lookup"><span data-stu-id="80003-214">The module output shows that the zip file has been unpackaged and that the function `print_hello` has been run.</span></span>
<span data-ttu-id="80003-215"> 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)</span><span class="sxs-lookup"><span data-stu-id="80003-215"> 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)</span></span>

<span data-ttu-id="80003-216">圖 7.</span><span class="sxs-lookup"><span data-stu-id="80003-216">Figure 7.</span></span> <span data-ttu-id="80003-217">[執行 Python 指令碼][execute-python-script]模組內正在使用的使用者定義函式。</span><span class="sxs-lookup"><span data-stu-id="80003-217">User-defined function in use inside the [Execute Python Script][execute-python-script] module.</span></span>


## <a name="working-with-visualizations"></a><span data-ttu-id="80003-218">使用視覺效果</span><span class="sxs-lookup"><span data-stu-id="80003-218">Working with visualizations</span></span>

<span data-ttu-id="80003-219">[執行 Python 指令碼][execute-python-script]可以傳回以 MatplotLib 建立而可呈現在瀏覽器的繪圖。</span><span class="sxs-lookup"><span data-stu-id="80003-219">Plots created using MatplotLib that can be visualized on the browser can be returned by the [Execute Python Script][execute-python-script].</span></span> <span data-ttu-id="80003-220">但是繪圖不會在使用 R 時自動重新導向至映像。因此使用者必須明確地將任何繪圖儲存為 PNG 檔案，才能傳回至 Azure Machine Learning。</span><span class="sxs-lookup"><span data-stu-id="80003-220">But the plots are not automatically redirected to images as they are when using R. So the user must explicitly save any plots to PNG files if they are to be returned back to Azure Machine Learning.</span></span> 

<span data-ttu-id="80003-221">若要從 MatplotLib 產生影像，您必須完成下列程序：</span><span class="sxs-lookup"><span data-stu-id="80003-221">To generate images from MatplotLib, you must complete the following procedure:</span></span>

* <span data-ttu-id="80003-222">將後端從預設 Qt 型轉譯器切換為 “AGG”</span><span class="sxs-lookup"><span data-stu-id="80003-222">switch the backend to “AGG” from the default Qt-based renderer</span></span> 
* <span data-ttu-id="80003-223">建立新的圖表物件</span><span class="sxs-lookup"><span data-stu-id="80003-223">create a new figure object</span></span> 
* <span data-ttu-id="80003-224">取得軸並且對其產生所有繪圖</span><span class="sxs-lookup"><span data-stu-id="80003-224">get the axis and generate all plots into it</span></span> 
* <span data-ttu-id="80003-225">將圖表儲存為 PNG 檔案</span><span class="sxs-lookup"><span data-stu-id="80003-225">save the figure to a PNG file</span></span> 

<span data-ttu-id="80003-226">以下的圖 8 會說明此程序，其使用 Pandas 中的 scatter_matrix 函式來建立散佈圖矩陣。</span><span class="sxs-lookup"><span data-stu-id="80003-226">This process is illustrated in the following Figure 8 that creates a scatter plot matrix using the scatter_matrix function in Pandas.</span></span>

![image1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

<span data-ttu-id="80003-228">圖 8.</span><span class="sxs-lookup"><span data-stu-id="80003-228">Figure 8.</span></span> <span data-ttu-id="80003-229">將 MatplotLib 圖表儲存為影像的程式碼。</span><span class="sxs-lookup"><span data-stu-id="80003-229">Code to save MatplotLib figures to images.</span></span>

<span data-ttu-id="80003-230">圖 9 顯示的實驗會使用先前顯示的指令碼，透過第二個輸出連接埠傳回繪圖。</span><span class="sxs-lookup"><span data-stu-id="80003-230">Figure 9 shows an experiment that uses the script shown previously to return plots via the second output port.</span></span>

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

<span data-ttu-id="80003-233">圖 9.</span><span class="sxs-lookup"><span data-stu-id="80003-233">Figure 9.</span></span> <span data-ttu-id="80003-234">視覺化從 Python 程式碼產生的繪圖。</span><span class="sxs-lookup"><span data-stu-id="80003-234">Visualizing plots generated from Python code.</span></span>

<span data-ttu-id="80003-235">可藉由將多個圖表儲存為不同的影像以傳回它們，Azure Machine Learning 執行階段會挑選所有影像並加以串連，以產生視覺效果。</span><span class="sxs-lookup"><span data-stu-id="80003-235">It is possible to return multiple figures by saving them into different images, the Azure Machine Learning runtime picks up all images and concatenates them for visualization.</span></span>


## <a name="advanced-examples"></a><span data-ttu-id="80003-236">進階範例</span><span class="sxs-lookup"><span data-stu-id="80003-236">Advanced examples</span></span>

<span data-ttu-id="80003-237">安裝在 Azure Machine Learning 中的 Anaconda 環境包含常見的套件，例如 NumPy、SciPy 和 Scikits-learn。</span><span class="sxs-lookup"><span data-stu-id="80003-237">The Anaconda environment installed in Azure Machine Learning contains common packages such as NumPy, SciPy, and Scikits-Learn.</span></span> <span data-ttu-id="80003-238">這些套件可以有效地用於機器學習管線中的各種資料處理工作。</span><span class="sxs-lookup"><span data-stu-id="80003-238">These packages can be effectively used for various data processing tasks in a machine learning pipeline.</span></span> <span data-ttu-id="80003-239">作為範例，下列實驗和指令碼說明在 Scikits-Learn 中使用集成學習器以計算資料集的功能重要性分數。</span><span class="sxs-lookup"><span data-stu-id="80003-239">As an example, the following experiment and script illustrate the use of ensemble learners in Scikits-Learn to compute feature importance scores for a dataset.</span></span> <span data-ttu-id="80003-240">然後，可以使用該分數先執行受監督的功能選取，再饋送至其他 ML 模型。</span><span class="sxs-lookup"><span data-stu-id="80003-240">The scores can be used to perform supervised feature selection before being fed into another ML model.</span></span>

<span data-ttu-id="80003-241">以下 Python 函式是用於根據分數計算重要性分數及將功能排序：</span><span class="sxs-lookup"><span data-stu-id="80003-241">Here is the Python function used to compute the importance scores and order the features based on the scores:</span></span>

![image11](./media/machine-learning-execute-python-scripts/figure8.png)

<span data-ttu-id="80003-243">圖 10.</span><span class="sxs-lookup"><span data-stu-id="80003-243">Figure 10.</span></span> <span data-ttu-id="80003-244">用於依分數將功能排名的函式。</span><span class="sxs-lookup"><span data-stu-id="80003-244">Function to rank features by scores.</span></span>
<span data-ttu-id="80003-245"> 然後下列實驗會在 Azure Machine Learning 中的 “Pima Indian Diabetes” 資料集計算及傳回功能的重要性分數：</span><span class="sxs-lookup"><span data-stu-id="80003-245">  The following experiment then computes and returns the importance scores of features in the “Pima Indian Diabetes” dataset in Azure Machine Learning:</span></span>

<span data-ttu-id="80003-246">![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)</span><span class="sxs-lookup"><span data-stu-id="80003-246">![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)</span></span>    

<span data-ttu-id="80003-247">圖 11.</span><span class="sxs-lookup"><span data-stu-id="80003-247">Figure 11.</span></span> <span data-ttu-id="80003-248">實驗，在 Pima Indian Diabetes 資料集中排名功能。</span><span class="sxs-lookup"><span data-stu-id="80003-248">Experiment to rank features in the Pima Indian Diabetes dataset.</span></span>

## <a name="limitations"></a><span data-ttu-id="80003-249">限制</span><span class="sxs-lookup"><span data-stu-id="80003-249">Limitations</span></span>
<span data-ttu-id="80003-250">[執行 Python 指令碼][execute-python-script]目前具有下列限制：</span><span class="sxs-lookup"><span data-stu-id="80003-250">The [Execute Python Script][execute-python-script] currently has the following limitations:</span></span>

1. <span data-ttu-id="80003-251">*沙箱化執行。*</span><span class="sxs-lookup"><span data-stu-id="80003-251">*Sandboxed execution.*</span></span> <span data-ttu-id="80003-252">Python 執行階段目前已沙箱化，因此，不允許以永續方式存取網路或本機檔案系統。</span><span class="sxs-lookup"><span data-stu-id="80003-252">The Python runtime is currently sandboxed and, as a result, does not allow access to the network or to the local file system in a persistent manner.</span></span> <span data-ttu-id="80003-253">所有本機儲存的文件都會被隔離，並且在模組結束時加以刪除。</span><span class="sxs-lookup"><span data-stu-id="80003-253">All files saved locally are isolated and deleted once the module finishes.</span></span> <span data-ttu-id="80003-254">Python 程式碼無法在其執行的機器上存取大部分的目錄，但目前的目錄及其子目錄例外。</span><span class="sxs-lookup"><span data-stu-id="80003-254">The Python code cannot access most directories on the machine it runs on, the exception being the current directory and its subdirectories.</span></span>
2. <span data-ttu-id="80003-255">*缺少精細的開發和偵錯支援。*</span><span class="sxs-lookup"><span data-stu-id="80003-255">*Lack of sophisticated development and debugging support.*</span></span> <span data-ttu-id="80003-256">Python 模組目前不支援 IDE 功能，例如 intellisense 和偵錯。</span><span class="sxs-lookup"><span data-stu-id="80003-256">The Python module currently does not support IDE features such as intellisense and debugging.</span></span> <span data-ttu-id="80003-257">此外，如果模組在執行階段失敗，則會提供完整的 Python 堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="80003-257">Also, if the module fails at runtime, the full Python stack trace is available.</span></span> <span data-ttu-id="80003-258">但是，它必須在模組的輸出記錄檔中檢視。</span><span class="sxs-lookup"><span data-stu-id="80003-258">But it must be viewed in the output log for the module.</span></span> <span data-ttu-id="80003-259">我們目前建議您在如 IPython 的環境中開發 Python 指令碼及進行偵錯，然後將程式碼匯入到模組。</span><span class="sxs-lookup"><span data-stu-id="80003-259">We currently recommend that you develop and debug Python scripts in an environment such as IPython and then import the code into the module.</span></span>
3. <span data-ttu-id="80003-260">*單一資料框架輸出。*</span><span class="sxs-lookup"><span data-stu-id="80003-260">*Single data frame output.*</span></span> <span data-ttu-id="80003-261">Python 進入點是唯一獲得允許的位置，可以將單一資料框架傳回為輸出。</span><span class="sxs-lookup"><span data-stu-id="80003-261">The Python entry point is only permitted to return a single data frame as output.</span></span> <span data-ttu-id="80003-262">目前無法直接將任意 Python 物件 (例如訓練模型) 傳回 Azure Machine Learning 執行階段。</span><span class="sxs-lookup"><span data-stu-id="80003-262">It is not currently possible to return arbitrary Python objects such as trained models directly back to the Azure Machine Learning runtime.</span></span> <span data-ttu-id="80003-263">如同[執行 R 指令碼][execute-r-script] (具有相同的限制)，在許多情況下可以將物件存放至位元組陣列，然後在資料框架內傳回。</span><span class="sxs-lookup"><span data-stu-id="80003-263">Like [Execute R Script][execute-r-script], which has the same limitation, it is possible in many cases to pickle objects into a byte array and then return that inside of a data frame.</span></span>
4. <span data-ttu-id="80003-264">*無法自訂 Python 安裝*。</span><span class="sxs-lookup"><span data-stu-id="80003-264">*Inability to customize Python installation*.</span></span> <span data-ttu-id="80003-265">目前，新增自訂 Python 模組的唯一方法是透過稍早所述的 zip 檔案機制。</span><span class="sxs-lookup"><span data-stu-id="80003-265">Currently, the only way to add custom Python modules is via the zip file mechanism described earlier.</span></span> <span data-ttu-id="80003-266">對於小模組可行，但是對於大模組 (特別是具有原生 DLL 的模組) 和大量模組而言則顯得繁瑣。</span><span class="sxs-lookup"><span data-stu-id="80003-266">While this is feasible for small modules, it is cumbersome for large modules (especially those with native DLLs) or a large number of modules.</span></span> 

## <a name="conclusions"></a><span data-ttu-id="80003-267">結論</span><span class="sxs-lookup"><span data-stu-id="80003-267">Conclusions</span></span>
<span data-ttu-id="80003-268">[執行 Python 指令碼][execute-python-script]模組可讓資料科學家將現有 Python 程式碼併入 Azure Machine Learning 中雲端託管的機器學習服務工作流程，並當作 Web 服務的一部分來順暢運作。</span><span class="sxs-lookup"><span data-stu-id="80003-268">The [Execute Python Script][execute-python-script] module allows a data scientist to incorporate existing Python code into cloud-hosted machine learning workflows in Azure Machine Learning and to seamlessly operationalize them as part of a web service.</span></span> <span data-ttu-id="80003-269">Python 指令碼模組可與 Azure Machine Learning 中的其他模組自然互通。</span><span class="sxs-lookup"><span data-stu-id="80003-269">The Python script module interoperates naturally with other modules in Azure Machine Learning.</span></span> <span data-ttu-id="80003-270">模組可以用於許多工作，從資料探索到預先處理和功能擷取，然後到結果評估與後續處理。</span><span class="sxs-lookup"><span data-stu-id="80003-270">The module can be used for a range of tasks from data exploration to pre-processing and feature extraction, and then to evaluation and post-processing of the results.</span></span> <span data-ttu-id="80003-271">用於執行的後端執行階段是以 Anaconda 為根據，這是一個經過良好測試及廣泛使用的 Python 散佈。</span><span class="sxs-lookup"><span data-stu-id="80003-271">The backend runtime used for execution is based on Anaconda, a well-tested and widely used Python distribution.</span></span> <span data-ttu-id="80003-272">此後端可讓您方便將現有程式碼資產加入雲端。</span><span class="sxs-lookup"><span data-stu-id="80003-272">This backend makes it simple for you to on-board existing code assets into the cloud.</span></span>

<span data-ttu-id="80003-273">我們預期在[執行 Python 指令碼][execute-python-script]模組中提供其他功能，例如能夠在 Python 中訓練和運作模型，以及新增更好的支援在 Azure Machine Learning Studio 中開發和偵錯程式碼。</span><span class="sxs-lookup"><span data-stu-id="80003-273">We expect to provide additional functionality to the [Execute Python Script][execute-python-script] module such as the ability to train and operationalize models in Python and to add better support for the development and debugging code in Azure Machine Learning Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80003-274">後續步驟</span><span class="sxs-lookup"><span data-stu-id="80003-274">Next steps</span></span>
<span data-ttu-id="80003-275">如需詳細資訊，請參閱 [Python 開發人員中心](https://azure.microsoft.com/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="80003-275">For more information, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span>

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

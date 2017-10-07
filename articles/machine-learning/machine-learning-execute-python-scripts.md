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
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a><span data-ttu-id="6f107-104">在 Azure Machine Learning Studio 中執行 Python 機器學習服務指令碼</span><span class="sxs-lookup"><span data-stu-id="6f107-104">Execute Python machine learning scripts in Azure Machine Learning Studio</span></span>

<span data-ttu-id="6f107-105">本主題描述基礎 hello Azure Machine Learning 中的 Python 指令碼目前支援的 hello 設計原則。</span><span class="sxs-lookup"><span data-stu-id="6f107-105">This topic describes hello design principles underlying hello current support for Python scripts in Azure Machine Learning.</span></span> <span data-ttu-id="6f107-106">也說明了 hello 所提供的主要功能，包括：</span><span class="sxs-lookup"><span data-stu-id="6f107-106">hello main capabilities provided are also outlined, including:</span></span>

- <span data-ttu-id="6f107-107">執行基本的使用方式案例</span><span class="sxs-lookup"><span data-stu-id="6f107-107">execute basic usage scenarios</span></span>
- <span data-ttu-id="6f107-108">為 Web 服務中的實驗評分</span><span class="sxs-lookup"><span data-stu-id="6f107-108">score an experiment in a web service</span></span>
- <span data-ttu-id="6f107-109">支援匯入現有的程式碼</span><span class="sxs-lookup"><span data-stu-id="6f107-109">support for importing existing code</span></span>
- <span data-ttu-id="6f107-110">匯出視覺效果</span><span class="sxs-lookup"><span data-stu-id="6f107-110">export visualizations</span></span>
- <span data-ttu-id="6f107-111">執行受監督的功能選取</span><span class="sxs-lookup"><span data-stu-id="6f107-111">perform supervised feature selection</span></span>
- <span data-ttu-id="6f107-112">了解部分限制</span><span class="sxs-lookup"><span data-stu-id="6f107-112">understand some limitations</span></span>

<span data-ttu-id="6f107-113">[Python](https://www.python.org/)是不可或缺的工具中的許多資料科學家 hello 工具箱子。</span><span class="sxs-lookup"><span data-stu-id="6f107-113">[Python](https://www.python.org/) is an indispensable tool in hello tool chest of many data scientists.</span></span> <span data-ttu-id="6f107-114">其中包含：</span><span class="sxs-lookup"><span data-stu-id="6f107-114">It has:</span></span>

* <span data-ttu-id="6f107-115">優雅簡潔的語法，</span><span class="sxs-lookup"><span data-stu-id="6f107-115">an elegant and concise syntax,</span></span> 
* <span data-ttu-id="6f107-116">跨平台支援，</span><span class="sxs-lookup"><span data-stu-id="6f107-116">cross-platform support,</span></span> 
* <span data-ttu-id="6f107-117">大量功能強大的程式庫集合，以及</span><span class="sxs-lookup"><span data-stu-id="6f107-117">a vast collection of powerful libraries, and</span></span> 
* <span data-ttu-id="6f107-118">臻致完善的開發工具。</span><span class="sxs-lookup"><span data-stu-id="6f107-118">mature development tools.</span></span> 

<span data-ttu-id="6f107-119">Python 是在工作流程的所有階段中使用 (通常使用於機器學習模型化)：</span><span class="sxs-lookup"><span data-stu-id="6f107-119">Python is being used in all phases of a workflow typically used in machine learning modeling:</span></span>

- <span data-ttu-id="6f107-120">資料內嵌和處理</span><span class="sxs-lookup"><span data-stu-id="6f107-120">data ingest and processing</span></span> 
- <span data-ttu-id="6f107-121">功能建構</span><span class="sxs-lookup"><span data-stu-id="6f107-121">feature construction</span></span>
- <span data-ttu-id="6f107-122">模型訓練</span><span class="sxs-lookup"><span data-stu-id="6f107-122">model training</span></span> 
- <span data-ttu-id="6f107-123">模型驗證</span><span class="sxs-lookup"><span data-stu-id="6f107-123">model validation</span></span>
- <span data-ttu-id="6f107-124">部署的 hello 模型</span><span class="sxs-lookup"><span data-stu-id="6f107-124">deployment of hello models</span></span>

<span data-ttu-id="6f107-125">Azure Machine Learning Studio 支援將 Python 指令碼內嵌至機器學習實驗的各個部分，並且順暢地將其發佈為 Microsoft Azure 上的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="6f107-125">Azure Machine Learning Studio supports embedding Python scripts into various parts of a machine learning experiment and also seamlessly publishing them as web services on Microsoft Azure.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a><span data-ttu-id="6f107-126">在 Machine Learning 中設計 Python 指令碼的原則</span><span class="sxs-lookup"><span data-stu-id="6f107-126">Design principles of Python scripts in Machine Learning</span></span>

<span data-ttu-id="6f107-127">Azure Machine Learning Studio 中的 hello 主要介面 tooPython 是透過 hello[執行 Python 指令碼][ execute-python-script]圖 1 所示的模組。</span><span class="sxs-lookup"><span data-stu-id="6f107-127">hello primary interface tooPython in Azure Machine Learning Studio is via hello [Execute Python Script][execute-python-script] module shown in Figure 1.</span></span>

![image1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![image2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

<span data-ttu-id="6f107-130">圖 1.</span><span class="sxs-lookup"><span data-stu-id="6f107-130">Figure 1.</span></span> <span data-ttu-id="6f107-131">hello**執行 Python 指令碼**模組。</span><span class="sxs-lookup"><span data-stu-id="6f107-131">hello **Execute Python Script** module.</span></span>

<span data-ttu-id="6f107-132">hello[執行 Python 指令碼][ execute-python-script] Azure ML Studio 中的模組接受向上 toothree 輸入，並產生向上 tootwo 輸出 （hello 之後 > 一節中討論），其 R 的類比，像是 hello [執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="6f107-132">hello [Execute Python Script][execute-python-script] module in Azure ML Studio accepts up toothree inputs and produces up tootwo outputs (discussed in hello following section), like its R analogue, hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="6f107-133">hello 執行 Python 程式碼 toobe 是 hello 參數中輸入特殊命名為進入點函式，呼叫`azureml_main`。</span><span class="sxs-lookup"><span data-stu-id="6f107-133">hello Python code toobe executed is entered into hello parameter box as a specially named entry-point function called `azureml_main`.</span></span> <span data-ttu-id="6f107-134">以下是 hello 原則使用 tooimplement 本單元的重要設計：</span><span class="sxs-lookup"><span data-stu-id="6f107-134">Here are hello key design principles used tooimplement this module:</span></span>

1. <span data-ttu-id="6f107-135">*必須是 Python 使用者慣用的。*</span><span class="sxs-lookup"><span data-stu-id="6f107-135">*Must be idiomatic for Python users.*</span></span> <span data-ttu-id="6f107-136">大多數 Python 使用者將其程式碼視為模組中的函式。</span><span class="sxs-lookup"><span data-stu-id="6f107-136">Most Python users factor their code as functions inside modules.</span></span> <span data-ttu-id="6f107-137">因此，將大量的可執行陳述式放在最上層的模組相當罕見。</span><span class="sxs-lookup"><span data-stu-id="6f107-137">So putting a lot of executable statements in a top-level module is relatively rare.</span></span> <span data-ttu-id="6f107-138">如此一來，hello 指令碼 方塊也會採用特殊命名的 Python 函式做為相對於 toojust 陳述式的序列。</span><span class="sxs-lookup"><span data-stu-id="6f107-138">As a result, hello script box also takes a specially named Python function as opposed toojust a sequence of statements.</span></span> <span data-ttu-id="6f107-139">hello hello 函式中公開的物件是標準的 Python 程式庫類型例如[熊](http://pandas.pydata.org/)資料框架和[NumPy](http://www.numpy.org/)陣列。</span><span class="sxs-lookup"><span data-stu-id="6f107-139">hello objects exposed in hello function are standard Python library types such as [Pandas](http://pandas.pydata.org/) data frames and [NumPy](http://www.numpy.org/) arrays.</span></span>
2. <span data-ttu-id="6f107-140">*必須在本機和雲端執行之間具有高畫質。*</span><span class="sxs-lookup"><span data-stu-id="6f107-140">*Must have high-fidelity between local and cloud executions.*</span></span> <span data-ttu-id="6f107-141">hello 後端使用 tooexecute hello Python 程式碼根據[Anaconda](https://store.continuum.io/cshop/anaconda/)、 廣泛使用跨平台科學 Python 的散發。</span><span class="sxs-lookup"><span data-stu-id="6f107-141">hello backend used tooexecute hello Python code is based on [Anaconda](https://store.continuum.io/cshop/anaconda/), a widely used cross-platform scientific Python distribution.</span></span> <span data-ttu-id="6f107-142">它隨附關閉 too200 的 hello 最常見的 Python 封裝。</span><span class="sxs-lookup"><span data-stu-id="6f107-142">It comes with close too200 of hello most common Python packages.</span></span> <span data-ttu-id="6f107-143">因此，資料科學家可在其本機 Azure Machine Learning 相容的 Anaconda 環境中，對程式碼進行偵錯與限定。</span><span class="sxs-lookup"><span data-stu-id="6f107-143">Therefore, data scientists can debug and qualify their code on their local Azure Machine Learning-compatible Anaconda environment.</span></span> <span data-ttu-id="6f107-144">然後使用現有的開發環境，例如[IPython](http://ipython.org/)筆記型電腦或[Python Tools for Visual Studio](http://aka.ms/ptvs)，toorun 做為 Azure ML 實驗的一部分。</span><span class="sxs-lookup"><span data-stu-id="6f107-144">Then use an existing development environment, such as [IPython](http://ipython.org/) notebook or [Python Tools for Visual Studio](http://aka.ms/ptvs), toorun it as part of an Azure ML experiment.</span></span> <span data-ttu-id="6f107-145">hello`azureml_main`進入點是香草 Python 函式，因此 * * * Azure ML 專屬的程式碼不可以用來撰寫或 hello 安裝 SDK。</span><span class="sxs-lookup"><span data-stu-id="6f107-145">hello `azureml_main` entry point is a vanilla Python function and so ****can be authored without Azure ML-specific code or hello SDK installed.</span></span>
3. <span data-ttu-id="6f107-146">*必須可以順暢地與其他 Azure Machine Learning 模組組合。*</span><span class="sxs-lookup"><span data-stu-id="6f107-146">*Must be seamlessly composable with other Azure Machine Learning modules.*</span></span> <span data-ttu-id="6f107-147">hello[執行 Python 指令碼][ execute-python-script]模組接受，做為輸入及輸出，標準 Azure Machine Learning 資料集。</span><span class="sxs-lookup"><span data-stu-id="6f107-147">hello [Execute Python Script][execute-python-script] module accepts, as inputs and outputs, standard Azure Machine Learning datasets.</span></span> <span data-ttu-id="6f107-148">hello 基礎架構明確而有效率地橋接器 hello Azure ML 和 Python 執行階段。</span><span class="sxs-lookup"><span data-stu-id="6f107-148">hello underlying framework transparently and efficiently bridges hello Azure ML and Python runtimes.</span></span> <span data-ttu-id="6f107-149">因此，Python 可以用於與現有 Azure ML 工作流程接合，包括呼叫 R 和 SQLite 的那些工作流程。</span><span class="sxs-lookup"><span data-stu-id="6f107-149">So Python can be used in conjunction with existing Azure ML workflows, including those that call into R and SQLite.</span></span> <span data-ttu-id="6f107-150">因此，資料科學家可以撰寫執行下列工作的工作流程：</span><span class="sxs-lookup"><span data-stu-id="6f107-150">A  result, data scientist could compose workflows that:</span></span>
   * <span data-ttu-id="6f107-151">使用 Python 和 Pandas 進行資料前處理和清除</span><span class="sxs-lookup"><span data-stu-id="6f107-151">use Python and Pandas for data pre-processing and cleaning</span></span>
   * <span data-ttu-id="6f107-152">摘要 hello 資料 tooa SQL 轉換，聯結多個資料集 tooform 功能</span><span class="sxs-lookup"><span data-stu-id="6f107-152">feed hello data tooa SQL transformation, joining multiple datasets tooform features</span></span>
   * <span data-ttu-id="6f107-153">使用 Azure Machine Learning 中的 hello 演算法定型模型</span><span class="sxs-lookup"><span data-stu-id="6f107-153">train models using hello algorithms in Azure Machine Learning</span></span> 
   * <span data-ttu-id="6f107-154">評估並使用 r 的 hello 結果進行後置處理</span><span class="sxs-lookup"><span data-stu-id="6f107-154">evaluate and post-process hello results using R.</span></span>


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a><span data-ttu-id="6f107-155">ML 中 Python 指令碼的基本使用案例</span><span class="sxs-lookup"><span data-stu-id="6f107-155">Basic usage scenarios in ML for Python scripts</span></span>

<span data-ttu-id="6f107-156">在本節中，我們的問卷的部分 hello 基本用法的 hello[執行 Python 指令碼][ execute-python-script]模組。</span><span class="sxs-lookup"><span data-stu-id="6f107-156">In this section, we survey some of hello basic uses of hello [Execute Python Script][execute-python-script] module.</span></span> <span data-ttu-id="6f107-157">輸入 toohello Python 模組會公開為熊資料框架。</span><span class="sxs-lookup"><span data-stu-id="6f107-157">Inputs toohello Python module are exposed as Pandas data frames.</span></span> <span data-ttu-id="6f107-158">hello 函式必須傳回單一熊資料框架內 Python 封裝[順序](https://docs.python.org/2/c-api/sequence.html)例如 tuple、 清單或 NumPy 陣列。</span><span class="sxs-lookup"><span data-stu-id="6f107-158">hello function must return a single Pandas data frame packaged inside of a Python [sequence](https://docs.python.org/2/c-api/sequence.html) such as a tuple, list, or NumPy array.</span></span> <span data-ttu-id="6f107-159">hello 第一個輸出連接埠 hello 模組然後就會傳回 hello 這個序列的第一個項目。</span><span class="sxs-lookup"><span data-stu-id="6f107-159">hello first element of this sequence is then returned in hello first output port of hello module.</span></span> <span data-ttu-id="6f107-160">此配置顯示在「圖 2」中。</span><span class="sxs-lookup"><span data-stu-id="6f107-160">This scheme is shown in Figure 2.</span></span>

![image3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

<span data-ttu-id="6f107-162">圖 2.</span><span class="sxs-lookup"><span data-stu-id="6f107-162">Figure 2.</span></span> <span data-ttu-id="6f107-163">輸入連接埠 tooparameters 和傳回值 toooutput 連接埠的對應。</span><span class="sxs-lookup"><span data-stu-id="6f107-163">Mapping of input ports tooparameters and return value toooutput port.</span></span>

<span data-ttu-id="6f107-164">詳細的 hello 輸入連接埠如何取得對應的 hello tooparameters 語意`azureml_main`函式 資料表 1 所示：</span><span class="sxs-lookup"><span data-stu-id="6f107-164">More detailed semantics of how hello input ports get mapped tooparameters of hello `azureml_main` function are shown in Table 1:</span></span>

![image1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

<span data-ttu-id="6f107-166">表 1.</span><span class="sxs-lookup"><span data-stu-id="6f107-166">Table 1.</span></span> <span data-ttu-id="6f107-167">輸入連接埠 toofunction 參數的對應。</span><span class="sxs-lookup"><span data-stu-id="6f107-167">Mapping of input ports toofunction parameters.</span></span>

<span data-ttu-id="6f107-168">輸入連接埠與函式參數之間的 hello 對應是位置性：</span><span class="sxs-lookup"><span data-stu-id="6f107-168">hello mapping between input ports and function parameters is positional:</span></span>

- <span data-ttu-id="6f107-169">hello 第一個連接輸入連接埠是對應的 toohello hello 函式的第一個參數。</span><span class="sxs-lookup"><span data-stu-id="6f107-169">hello first connected input port is mapped toohello first parameter of hello function.</span></span> 
- <span data-ttu-id="6f107-170">hello 第二個輸入 （如果連接） 是對應的 toohello hello 函式的第二個參數。</span><span class="sxs-lookup"><span data-stu-id="6f107-170">hello second input (if connected) is mapped toohello second parameter of hello function.</span></span>

<span data-ttu-id="6f107-171">請參閱*資料分析的 Python* (O'Reilly 2012) 由西部 McKinney 如需詳細資訊和如何它可以是使用的 toomanipulate 資料有效地和 Python 熊上。</span><span class="sxs-lookup"><span data-stu-id="6f107-171">See *Python for Data Analysis* (O'Reilly, 2012) by W. McKinney for more information on Python Pandas and on how it can be used toomanipulate data effectively and efficiently.</span></span> 


## <a name="translation-of-input-and-output-types"></a><span data-ttu-id="6f107-172">輸入和輸出類型的轉譯</span><span class="sxs-lookup"><span data-stu-id="6f107-172">Translation of input and output types</span></span> 
<span data-ttu-id="6f107-173">在 Azure ML 的輸入資料集是轉換的 toodata 框架熊中。</span><span class="sxs-lookup"><span data-stu-id="6f107-173">Input datasets in Azure ML are converted toodata frames in Pandas.</span></span> <span data-ttu-id="6f107-174">輸出資料框架會轉換後 tooAzure ML 資料集。</span><span class="sxs-lookup"><span data-stu-id="6f107-174">Output data frames are converted back tooAzure ML datasets.</span></span> <span data-ttu-id="6f107-175">請執行下列轉換 hello:</span><span class="sxs-lookup"><span data-stu-id="6f107-175">hello following conversions are performed:</span></span>

1. <span data-ttu-id="6f107-176">字串和數值資料行轉換成-為資料集內的遺漏值，而 已轉換的 too'NA' 熊中的值。</span><span class="sxs-lookup"><span data-stu-id="6f107-176">String and numeric columns are converted as-is and missing values in a dataset are converted too‘NA’ values in Pandas.</span></span> <span data-ttu-id="6f107-177">hello 相同轉換發生在 hello 回溯 （熊 NA 值是在 Azure ML 轉換的 toomissing 值）。</span><span class="sxs-lookup"><span data-stu-id="6f107-177">hello same conversion happens on hello way back (NA values in Pandas are converted toomissing values in Azure ML).</span></span>
2. <span data-ttu-id="6f107-178">Azure ML 不支援 Pandas 中的索引向量。</span><span class="sxs-lookup"><span data-stu-id="6f107-178">Index vectors in Pandas are not supported in Azure ML.</span></span> <span data-ttu-id="6f107-179">Hello Python 函式中的所有輸入的資料框架一律有 0 toohello 資料列數目減 1 的 64 位元數字索引。</span><span class="sxs-lookup"><span data-stu-id="6f107-179">All input data frames in hello Python function always have a 64-bit numerical index from 0 toohello number of rows minus 1.</span></span> 
3. <span data-ttu-id="6f107-180">Azure ML 資料集無法具有重複的資料行名稱或非字串的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="6f107-180">Azure ML datasets cannot have duplicate column names and column names that are not strings.</span></span> <span data-ttu-id="6f107-181">如果輸出資料框架中包含非數值資料行，hello 架構會呼叫`str`hello 資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="6f107-181">If an output data frame contains non-numeric columns, hello framework calls `str` on hello column names.</span></span> <span data-ttu-id="6f107-182">同樣地，任何重複的資料行名稱都是自動 mangled 的 tooinsure hello 名稱是唯一的。</span><span class="sxs-lookup"><span data-stu-id="6f107-182">Likewise, any duplicate column names are automatically mangled tooinsure hello names are unique.</span></span> <span data-ttu-id="6f107-183">hello 尾碼 (2) 新增 toohello 第一個重複項目、 (3) toohello 第二個重複項目，依此類推。</span><span class="sxs-lookup"><span data-stu-id="6f107-183">hello suffix (2) is added toohello first duplicate, (3) toohello second duplicate, and so on.</span></span>


## <a name="operationalizing-python-scripts"></a><span data-ttu-id="6f107-184">運作 Python 指令碼</span><span class="sxs-lookup"><span data-stu-id="6f107-184">Operationalizing Python scripts</span></span>

<span data-ttu-id="6f107-185">當評分實驗中使用的任何[執行 Python 指令碼][execute-python-script]模組發佈為 Web 服務時，系統會呼叫這些模組。</span><span class="sxs-lookup"><span data-stu-id="6f107-185">Any [Execute Python Script][execute-python-script] modules used in a scoring experiment are called when published as a web service.</span></span> <span data-ttu-id="6f107-186">例如，圖 3 顯示包含 hello 程式碼 tooevaluate 單一 Python 運算式計分實驗。</span><span class="sxs-lookup"><span data-stu-id="6f107-186">For example, Figure 3 shows a scoring experiment that contains hello code tooevaluate a single Python expression.</span></span> 

![image4](./media/machine-learning-execute-python-scripts/figure3a.png)

![image5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

<span data-ttu-id="6f107-189">圖 3.</span><span class="sxs-lookup"><span data-stu-id="6f107-189">Figure 3.</span></span> <span data-ttu-id="6f107-190">用以評估 Python 運算式的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="6f107-190">Web service for evaluating a Python expression.</span></span>

<span data-ttu-id="6f107-191">從此實驗建立的 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="6f107-191">A web service created from this experiment:</span></span>

- <span data-ttu-id="6f107-192">會將 Python 運算式作為輸入 (字串)</span><span class="sxs-lookup"><span data-stu-id="6f107-192">takes as input a Python expression (as a string)</span></span>
- <span data-ttu-id="6f107-193">將它傳送 toohello Python 解譯器</span><span class="sxs-lookup"><span data-stu-id="6f107-193">sends it toohello Python interpreter</span></span> 
- <span data-ttu-id="6f107-194">傳回表格，內含 hello 運算式和 hello 評估結果。</span><span class="sxs-lookup"><span data-stu-id="6f107-194">returns a table containing both hello expression and hello evaluated result.</span></span>


## <a name="importing-existing-python-script-modules"></a><span data-ttu-id="6f107-195">匯入現有的 Python 指令碼模組</span><span class="sxs-lookup"><span data-stu-id="6f107-195">Importing existing Python script modules</span></span>

<span data-ttu-id="6f107-196">常見使用案例的許多資料科學家是 tooincorporate 現有 Python 指令碼 Azure ML 實驗。</span><span class="sxs-lookup"><span data-stu-id="6f107-196">A common use-case for many data scientists is tooincorporate existing Python scripts into Azure ML experiments.</span></span> <span data-ttu-id="6f107-197">而不是要求所有的程式碼即將串連並貼到單一指令碼 方塊，hello[執行 Python 指令碼][ execute-python-script]模組接受包含在 hello 第三個輸入連接埠的 Python 模組 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="6f107-197">Instead of requiring that all code be concatenated and pasted into a single script box, hello [Execute Python Script][execute-python-script] module accepts a zip file that contains Python modules at hello third input port.</span></span> <span data-ttu-id="6f107-198">hello 檔案會解壓縮 hello 執行架構，在執行階段和 hello 內容加入 toohello hello Python 解譯器程式庫路徑。</span><span class="sxs-lookup"><span data-stu-id="6f107-198">hello file is unzipped by hello execution framework at runtime and hello contents are added toohello library path of hello Python interpreter.</span></span> <span data-ttu-id="6f107-199">hello`azureml_main`函式可以再直接匯入這些模組的進入點。</span><span class="sxs-lookup"><span data-stu-id="6f107-199">hello `azureml_main` entry point function can then import these modules directly.</span></span>

<span data-ttu-id="6f107-200">例如，請考慮 hello 檔案 Hello.py 包含簡單的"Hello，World"函式。</span><span class="sxs-lookup"><span data-stu-id="6f107-200">As an example, consider hello file Hello.py containing a simple “Hello, World” function.</span></span>

![image6](./media/machine-learning-execute-python-scripts/figure4.png)

<span data-ttu-id="6f107-202">圖 4.</span><span class="sxs-lookup"><span data-stu-id="6f107-202">Figure 4.</span></span> <span data-ttu-id="6f107-203">Hello.py 檔案中的使用者定義函式。</span><span class="sxs-lookup"><span data-stu-id="6f107-203">User-defined function in Hello.py file.</span></span>

<span data-ttu-id="6f107-204">接下來，我們會建立包含 Hello.py 的 Hello.zip 檔案：</span><span class="sxs-lookup"><span data-stu-id="6f107-204">Next, we create a file Hello.zip that contains Hello.py:</span></span>

![image7](./media/machine-learning-execute-python-scripts/figure5.png)

<span data-ttu-id="6f107-206">圖 5.</span><span class="sxs-lookup"><span data-stu-id="6f107-206">Figure 5.</span></span> <span data-ttu-id="6f107-207">包含使用者定義 Python 程式碼的 Zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="6f107-207">Zip file containing user-defined Python code.</span></span>

<span data-ttu-id="6f107-208">做為資料集 hello zip 檔案上傳至 Azure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="6f107-208">Upload hello zip file as a dataset into Azure Machine Learning Studio.</span></span> <span data-ttu-id="6f107-209">然後建立並執行的實驗使用 hello Hello.zip 檔案中的 hello Python 程式碼，方法是將它附加 toohello 第三個輸入連接埠的 hello**執行 Python 指令碼**模組，如本圖所示。</span><span class="sxs-lookup"><span data-stu-id="6f107-209">Then create and run an experiment that uses hello Python code in hello Hello.zip file by attaching it toohello third input port of hello **Execute Python Script** module, as shown in this figure.</span></span>

![image8](./media/machine-learning-execute-python-scripts/figure6a.png)

![image9](./media/machine-learning-execute-python-scripts/figure6b.png)

<span data-ttu-id="6f107-212">圖 6.</span><span class="sxs-lookup"><span data-stu-id="6f107-212">Figure 6.</span></span> <span data-ttu-id="6f107-213">範例實驗，具有上傳為 zip 檔案的使用者定義 Python 程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f107-213">Sample experiment with user-defined Python code uploaded as a zip file.</span></span>

<span data-ttu-id="6f107-214">hello 模組輸出會顯示該 hello zip 檔已解除封裝及該 hello 函式`print_hello`已執行。</span><span class="sxs-lookup"><span data-stu-id="6f107-214">hello module output shows that hello zip file has been unpackaged and that hello function `print_hello` has been run.</span></span>
<span data-ttu-id="6f107-215"> 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)</span><span class="sxs-lookup"><span data-stu-id="6f107-215"> 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)</span></span>

<span data-ttu-id="6f107-216">圖 7.</span><span class="sxs-lookup"><span data-stu-id="6f107-216">Figure 7.</span></span> <span data-ttu-id="6f107-217">Hello 內的使用中的使用者定義函數[執行 Python 指令碼][ execute-python-script]模組。</span><span class="sxs-lookup"><span data-stu-id="6f107-217">User-defined function in use inside hello [Execute Python Script][execute-python-script] module.</span></span>


## <a name="working-with-visualizations"></a><span data-ttu-id="6f107-218">使用視覺效果</span><span class="sxs-lookup"><span data-stu-id="6f107-218">Working with visualizations</span></span>

<span data-ttu-id="6f107-219">建立 hello 瀏覽器上使用 MatplotLib 可以視覺化的繪圖可以傳回 hello[執行 Python 指令碼][execute-python-script]。</span><span class="sxs-lookup"><span data-stu-id="6f107-219">Plots created using MatplotLib that can be visualized on hello browser can be returned by hello [Execute Python Script][execute-python-script].</span></span> <span data-ttu-id="6f107-220">但是 hello 繪圖不自動重新導向的 tooimages 如時使用。因此 hello 使用者必須明確儲存任何繪圖 tooPNG 檔案有 toobe 傳回後 tooAzure 機器學習。</span><span class="sxs-lookup"><span data-stu-id="6f107-220">But hello plots are not automatically redirected tooimages as they are when using R. So hello user must explicitly save any plots tooPNG files if they are toobe returned back tooAzure Machine Learning.</span></span> 

<span data-ttu-id="6f107-221">MatplotLib toogenerate 映像，您必須完成下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="6f107-221">toogenerate images from MatplotLib, you must complete hello following procedure:</span></span>

* <span data-ttu-id="6f107-222">切換 hello 後端 」 彙總 」 從 hello 太預設 Qt 為基礎的轉譯器</span><span class="sxs-lookup"><span data-stu-id="6f107-222">switch hello backend too“AGG” from hello default Qt-based renderer</span></span> 
* <span data-ttu-id="6f107-223">建立新的圖表物件</span><span class="sxs-lookup"><span data-stu-id="6f107-223">create a new figure object</span></span> 
* <span data-ttu-id="6f107-224">取得 hello 座標軸，並產生到它所有的繪圖</span><span class="sxs-lookup"><span data-stu-id="6f107-224">get hello axis and generate all plots into it</span></span> 
* <span data-ttu-id="6f107-225">儲存 hello 圖 tooa PNG 檔案</span><span class="sxs-lookup"><span data-stu-id="6f107-225">save hello figure tooa PNG file</span></span> 

<span data-ttu-id="6f107-226">此程序是以 hello 遵循建立散佈圖矩陣中熊使用 hello scatter_matrix 函式的圖 8 所示。</span><span class="sxs-lookup"><span data-stu-id="6f107-226">This process is illustrated in hello following Figure 8 that creates a scatter plot matrix using hello scatter_matrix function in Pandas.</span></span>

![image1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

<span data-ttu-id="6f107-228">圖 8.</span><span class="sxs-lookup"><span data-stu-id="6f107-228">Figure 8.</span></span> <span data-ttu-id="6f107-229">程式碼的 toosave MatplotLib 圖 tooimages。</span><span class="sxs-lookup"><span data-stu-id="6f107-229">Code toosave MatplotLib figures tooimages.</span></span>

<span data-ttu-id="6f107-230">圖 9 顯示的實驗使用先前所示 tooreturn 繪製從 hello 第二個輸出連接埠傳送的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="6f107-230">Figure 9 shows an experiment that uses hello script shown previously tooreturn plots via hello second output port.</span></span>

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

<span data-ttu-id="6f107-233">圖 9.</span><span class="sxs-lookup"><span data-stu-id="6f107-233">Figure 9.</span></span> <span data-ttu-id="6f107-234">視覺化從 Python 程式碼產生的繪圖。</span><span class="sxs-lookup"><span data-stu-id="6f107-234">Visualizing plots generated from Python code.</span></span>

<span data-ttu-id="6f107-235">可能的 tooreturn 多個圖表將其儲存到不同的映像、 hello Azure 機器學習服務執行階段拾取所有映像並將它們串連視覺效果。</span><span class="sxs-lookup"><span data-stu-id="6f107-235">It is possible tooreturn multiple figures by saving them into different images, hello Azure Machine Learning runtime picks up all images and concatenates them for visualization.</span></span>


## <a name="advanced-examples"></a><span data-ttu-id="6f107-236">進階範例</span><span class="sxs-lookup"><span data-stu-id="6f107-236">Advanced examples</span></span>

<span data-ttu-id="6f107-237">安裝 Azure Machine Learning 中的 hello Anaconda 環境包含常見的封裝，例如 NumPy、 SciPy 和 Scikits-learn。</span><span class="sxs-lookup"><span data-stu-id="6f107-237">hello Anaconda environment installed in Azure Machine Learning contains common packages such as NumPy, SciPy, and Scikits-Learn.</span></span> <span data-ttu-id="6f107-238">這些套件可以有效地用於機器學習管線中的各種資料處理工作。</span><span class="sxs-lookup"><span data-stu-id="6f107-238">These packages can be effectively used for various data processing tasks in a machine learning pipeline.</span></span> <span data-ttu-id="6f107-239">例如，hello 下列實驗和指令碼說明 hello 用途中 Scikits-learn toocompute 功能重要性分數的集團學習模組資料集。</span><span class="sxs-lookup"><span data-stu-id="6f107-239">As an example, hello following experiment and script illustrate hello use of ensemble learners in Scikits-Learn toocompute feature importance scores for a dataset.</span></span> <span data-ttu-id="6f107-240">hello 分數可以是使用的 tooperform 監督式特徵選取之前饋送至另一個 ML 模型。</span><span class="sxs-lookup"><span data-stu-id="6f107-240">hello scores can be used tooperform supervised feature selection before being fed into another ML model.</span></span>

<span data-ttu-id="6f107-241">以下是 hello Python 用函式 toocompute hello 重要性分數和根據 hello 分數的順序 hello 功能：</span><span class="sxs-lookup"><span data-stu-id="6f107-241">Here is hello Python function used toocompute hello importance scores and order hello features based on hello scores:</span></span>

![image11](./media/machine-learning-execute-python-scripts/figure8.png)

<span data-ttu-id="6f107-243">圖 10.</span><span class="sxs-lookup"><span data-stu-id="6f107-243">Figure 10.</span></span> <span data-ttu-id="6f107-244">函式 toorank 功能分數。</span><span class="sxs-lookup"><span data-stu-id="6f107-244">Function toorank features by scores.</span></span>
<span data-ttu-id="6f107-245"> hello 下列實驗計算，然後在 Azure Machine Learning 中的 hello"Pima 印度洋糖尿病"資料集中傳回 hello 重要性分數的功能：</span><span class="sxs-lookup"><span data-stu-id="6f107-245">  hello following experiment then computes and returns hello importance scores of features in hello “Pima Indian Diabetes” dataset in Azure Machine Learning:</span></span>

<span data-ttu-id="6f107-246">![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)</span><span class="sxs-lookup"><span data-stu-id="6f107-246">![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)</span></span>    

<span data-ttu-id="6f107-247">圖 11.</span><span class="sxs-lookup"><span data-stu-id="6f107-247">Figure 11.</span></span> <span data-ttu-id="6f107-248">實驗 toorank hello Pima 印度洋糖尿病資料集中的功能。</span><span class="sxs-lookup"><span data-stu-id="6f107-248">Experiment toorank features in hello Pima Indian Diabetes dataset.</span></span>

## <a name="limitations"></a><span data-ttu-id="6f107-249">限制</span><span class="sxs-lookup"><span data-stu-id="6f107-249">Limitations</span></span>
<span data-ttu-id="6f107-250">hello[執行 Python 指令碼][ execute-python-script]目前有下列限制的 hello:</span><span class="sxs-lookup"><span data-stu-id="6f107-250">hello [Execute Python Script][execute-python-script] currently has hello following limitations:</span></span>

1. <span data-ttu-id="6f107-251">*沙箱化執行。*</span><span class="sxs-lookup"><span data-stu-id="6f107-251">*Sandboxed execution.*</span></span> <span data-ttu-id="6f107-252">hello Python 執行階段目前沙箱化，如此一來，不允許存取 toohello 網路或 toohello 本機檔案系統中以持續方式。</span><span class="sxs-lookup"><span data-stu-id="6f107-252">hello Python runtime is currently sandboxed and, as a result, does not allow access toohello network or toohello local file system in a persistent manner.</span></span> <span data-ttu-id="6f107-253">儲存在本機的所有檔案會隔離，並 hello 模組完成之後刪除。</span><span class="sxs-lookup"><span data-stu-id="6f107-253">All files saved locally are isolated and deleted once hello module finishes.</span></span> <span data-ttu-id="6f107-254">hello Python 程式碼無法執行該 hello 機器上的大部分目錄的存取，目前的目錄和子目錄 hello 例外狀況正在 hello。</span><span class="sxs-lookup"><span data-stu-id="6f107-254">hello Python code cannot access most directories on hello machine it runs on, hello exception being hello current directory and its subdirectories.</span></span>
2. <span data-ttu-id="6f107-255">*缺少精細的開發和偵錯支援。*</span><span class="sxs-lookup"><span data-stu-id="6f107-255">*Lack of sophisticated development and debugging support.*</span></span> <span data-ttu-id="6f107-256">hello Python 模組目前不支援 intellisense 和偵錯等 IDE 功能。</span><span class="sxs-lookup"><span data-stu-id="6f107-256">hello Python module currently does not support IDE features such as intellisense and debugging.</span></span> <span data-ttu-id="6f107-257">此外，如果 hello 模組在執行階段，hello 完整 Python 堆疊追蹤會提供。</span><span class="sxs-lookup"><span data-stu-id="6f107-257">Also, if hello module fails at runtime, hello full Python stack trace is available.</span></span> <span data-ttu-id="6f107-258">但是，它必須在 hello hello 模組的輸出記錄檔中的檢視。</span><span class="sxs-lookup"><span data-stu-id="6f107-258">But it must be viewed in hello output log for hello module.</span></span> <span data-ttu-id="6f107-259">目前建議您開發及偵錯這類 IPython 的環境中的 Python 指令碼，然後匯入 hello 模組的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f107-259">We currently recommend that you develop and debug Python scripts in an environment such as IPython and then import hello code into hello module.</span></span>
3. <span data-ttu-id="6f107-260">*單一資料框架輸出。*</span><span class="sxs-lookup"><span data-stu-id="6f107-260">*Single data frame output.*</span></span> <span data-ttu-id="6f107-261">hello Python 進入點是只允許的 tooreturn 單一資料框架，做為輸出。</span><span class="sxs-lookup"><span data-stu-id="6f107-261">hello Python entry point is only permitted tooreturn a single data frame as output.</span></span> <span data-ttu-id="6f107-262">它不是目前 tooreturn 任意 Python 物件，例如定型的模型直接回 toohello Azure 機器學習服務執行階段。</span><span class="sxs-lookup"><span data-stu-id="6f107-262">It is not currently possible tooreturn arbitrary Python objects such as trained models directly back toohello Azure Machine Learning runtime.</span></span> <span data-ttu-id="6f107-263">像[執行 R 指令碼][execute-r-script]，其具有 hello 很可能在許多情況下 toopickle 物件至位元組陣列，然後再回頭執行資料框架內，相同的限制。</span><span class="sxs-lookup"><span data-stu-id="6f107-263">Like [Execute R Script][execute-r-script], which has hello same limitation, it is possible in many cases toopickle objects into a byte array and then return that inside of a data frame.</span></span>
4. <span data-ttu-id="6f107-264">*無法 toocustomize Python 安裝*。</span><span class="sxs-lookup"><span data-stu-id="6f107-264">*Inability toocustomize Python installation*.</span></span> <span data-ttu-id="6f107-265">目前，hello 只有方式 tooadd 自訂 Python 模組是透過 hello zip 檔案機制稍早所述。</span><span class="sxs-lookup"><span data-stu-id="6f107-265">Currently, hello only way tooadd custom Python modules is via hello zip file mechanism described earlier.</span></span> <span data-ttu-id="6f107-266">對於小模組可行，但是對於大模組 (特別是具有原生 DLL 的模組) 和大量模組而言則顯得繁瑣。</span><span class="sxs-lookup"><span data-stu-id="6f107-266">While this is feasible for small modules, it is cumbersome for large modules (especially those with native DLLs) or a large number of modules.</span></span> 

## <a name="conclusions"></a><span data-ttu-id="6f107-267">結論</span><span class="sxs-lookup"><span data-stu-id="6f107-267">Conclusions</span></span>
<span data-ttu-id="6f107-268">hello[執行 Python 指令碼][ execute-python-script]模組可讓資料科學家 tooincorporate 現有 Python 程式碼在 Azure 機器學習和 tooseamlessly 的雲端裝載的機器學習工作流程實施它們做為 web 服務的一部分。</span><span class="sxs-lookup"><span data-stu-id="6f107-268">hello [Execute Python Script][execute-python-script] module allows a data scientist tooincorporate existing Python code into cloud-hosted machine learning workflows in Azure Machine Learning and tooseamlessly operationalize them as part of a web service.</span></span> <span data-ttu-id="6f107-269">hello Python 指令碼模組可與 Azure Machine Learning 中的其他模組自然互通。</span><span class="sxs-lookup"><span data-stu-id="6f107-269">hello Python script module interoperates naturally with other modules in Azure Machine Learning.</span></span> <span data-ttu-id="6f107-270">hello 模組可以用於許多工作，從 資料瀏覽 toopre 處理及擷取特徵，然後 tooevaluation 和 hello 結果的後續處理。</span><span class="sxs-lookup"><span data-stu-id="6f107-270">hello module can be used for a range of tasks from data exploration toopre-processing and feature extraction, and then tooevaluation and post-processing of hello results.</span></span> <span data-ttu-id="6f107-271">用於執行 hello 後端執行階段為基礎 Anaconda，經過完整測試也廣泛使用的 Python 發佈。</span><span class="sxs-lookup"><span data-stu-id="6f107-271">hello backend runtime used for execution is based on Anaconda, a well-tested and widely used Python distribution.</span></span> <span data-ttu-id="6f107-272">這個後端可簡化您的現有程式碼資產 tooon 面板到 hello 的雲端。</span><span class="sxs-lookup"><span data-stu-id="6f107-272">This backend makes it simple for you tooon-board existing code assets into hello cloud.</span></span>

<span data-ttu-id="6f107-273">我們預期 tooprovide 額外的功能 toohello[執行 Python 指令碼][ execute-python-script]模組例如 hello 能力 tootrain 實施模型以 Python 和 tooadd 更佳的 hello 支援開發和偵錯在 Azure Machine Learning Studio 中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f107-273">We expect tooprovide additional functionality toohello [Execute Python Script][execute-python-script] module such as hello ability tootrain and operationalize models in Python and tooadd better support for hello development and debugging code in Azure Machine Learning Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f107-274">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f107-274">Next steps</span></span>
<span data-ttu-id="6f107-275">如需詳細資訊，請參閱 hello [Python 開發人員中心](https://azure.microsoft.com/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="6f107-275">For more information, see hello [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span>

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

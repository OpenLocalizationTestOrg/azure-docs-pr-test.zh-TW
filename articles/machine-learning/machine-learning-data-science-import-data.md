---
title: "將資料匯入 Machine Learning Studio | Microsoft Docs"
description: "如何從各種資料來源將資料匯入 Azure Machine Learning Studio。 了解支援的資料類型和資料格式。"
keywords: "匯入資料,資料格式,資料類型,資料來源,定型資料"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: b92b480e62f4ce4f4836dc5d0f6afbe80c6b664a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="772a0-105">從各種資料來源將訓練資料匯入 Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="772a0-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="772a0-106">若要在 Machine Learning Studio 中使用您自己的資料來開發和訓練預測性分析方案，您可以：</span><span class="sxs-lookup"><span data-stu-id="772a0-106">To use your own data in Machine Learning Studio to develop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="772a0-107">事先上傳硬碟中**本機檔案**資料，在工作區中建立資料集模組</span><span class="sxs-lookup"><span data-stu-id="772a0-107">upload data from a **local file** ahead of time from your hard drive to create a dataset module in your workspace</span></span>
* <span data-ttu-id="772a0-108">使用[匯入資料][import-data]模組，在實驗進行時，從數個**線上資料來源**其中之一存取資料</span><span class="sxs-lookup"><span data-stu-id="772a0-108">access data from one of several **online data sources** while your experiment is running using the [Import Data][import-data] module</span></span> 
* <span data-ttu-id="772a0-109">使用其他 Azure Machine Learning **實驗**中儲存為資料集的資料</span><span class="sxs-lookup"><span data-stu-id="772a0-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="772a0-110">使用內部部署 **SQL Server 資料庫**中的資料</span><span class="sxs-lookup"><span data-stu-id="772a0-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="772a0-111">上述選項都在下方選單的其中一個主題裡說明。</span><span class="sxs-lookup"><span data-stu-id="772a0-111">Each of these options is described in one of the topics on the menu below.</span></span> <span data-ttu-id="772a0-112">這些主題說明如何從各種資料來源匯入用於 Machine Learning Studio 的資料。</span><span class="sxs-lookup"><span data-stu-id="772a0-112">These topics show you how to import data from these various data sources to use in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="772a0-113">Machine Learning Studio 中有一些可用於訓練資料的範例資料集。</span><span class="sxs-lookup"><span data-stu-id="772a0-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="772a0-114">如需這些資訊，請參閱 [在 Azure Machine Learning Studio 中使用範例資料集](machine-learning-use-sample-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="772a0-114">For information on these, see [Use the sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="772a0-115">這個簡介主題也會討論如何備妥資料供 Machine Learning Studio 使用，並描述支援的資料格式和資料類型。</span><span class="sxs-lookup"><span data-stu-id="772a0-115">This introductory topic also discusses how to get data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="772a0-116">備妥資料以在 Azure Machine Learning Studio 中使用</span><span class="sxs-lookup"><span data-stu-id="772a0-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="772a0-117">Machine Learning Studio 是專為與矩形或表格式資料搭配使用而設計，例如分隔的文字資料，或資料庫的結構化資料，雖然在某些情況下可能會使用非矩形資料。</span><span class="sxs-lookup"><span data-stu-id="772a0-117">Machine Learning Studio is designed to work with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="772a0-118">如果您的資料相對乾淨是最佳狀況。</span><span class="sxs-lookup"><span data-stu-id="772a0-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="772a0-119">也就是說，在您將資料上傳至您的實驗之前，您要關注如不具引號的字串的問題。</span><span class="sxs-lookup"><span data-stu-id="772a0-119">That is, you'll want to take care of issues such as unquoted strings before you upload the data into your experiment.</span></span>

<span data-ttu-id="772a0-120">但是，Machine Learning Studio 中有模組可讓您在實驗中進行一些資料操作。</span><span class="sxs-lookup"><span data-stu-id="772a0-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="772a0-121">依據您使用的機器學習演算法，您可能需要決定如何處理資料結構問題，例如遺漏值和疏鬆資料，有模組可以協助處理。</span><span class="sxs-lookup"><span data-stu-id="772a0-121">Depending on the machine learning algorithms you'll be using, you may need to decide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="772a0-122">請參閱模組調色盤的 **資料轉換** 區段，以取得執行這些功能的模組。</span><span class="sxs-lookup"><span data-stu-id="772a0-122">Look in the **Data Transformation** section of the module palette for modules that perform these functions.</span></span>

<span data-ttu-id="772a0-123">您可以在實驗的任何位置，檢視或下載模組產生的資料，方法是按一下輸出連接埠。</span><span class="sxs-lookup"><span data-stu-id="772a0-123">At any point in your experiment you can view or download the data that's produced by a module by clicking the output port.</span></span> <span data-ttu-id="772a0-124">視模組而定，可能會提供不同的下載選項，或者可以在 Machine Learning Studio 中的網頁瀏覽器將資料視覺化呈現。</span><span class="sxs-lookup"><span data-stu-id="772a0-124">Depending on the module, there may be different download options available, or you may be able to visualize the data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="772a0-125">支援的資料格式和資料類型</span><span class="sxs-lookup"><span data-stu-id="772a0-125">Data formats and data types supported</span></span>
<span data-ttu-id="772a0-126">視您用來匯入資料的機制及其來源而定，您可以將一些資料類型匯入您的實驗：</span><span class="sxs-lookup"><span data-stu-id="772a0-126">You can import a number of data types into your experiment, depending on what mechanism you use to import data and where it's coming from:</span></span>

* <span data-ttu-id="772a0-127">純文字 (.txt)</span><span class="sxs-lookup"><span data-stu-id="772a0-127">Plain text (.txt)</span></span>
* <span data-ttu-id="772a0-128">逗號分隔值 (CSV)，具有標頭 (.csv) 或不具標頭 (.nh.csv)</span><span class="sxs-lookup"><span data-stu-id="772a0-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="772a0-129">定位鍵分隔值 (TSV)，具有標頭 (.tsv) 或不具標頭 (.nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="772a0-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="772a0-130">Excel 檔案</span><span class="sxs-lookup"><span data-stu-id="772a0-130">Excel file</span></span>
* <span data-ttu-id="772a0-131">Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="772a0-131">Azure table</span></span>
* <span data-ttu-id="772a0-132">Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="772a0-132">Hive table</span></span>
* <span data-ttu-id="772a0-133">SQL 資料庫資料表</span><span class="sxs-lookup"><span data-stu-id="772a0-133">SQL database table</span></span>
* <span data-ttu-id="772a0-134">OData 值</span><span class="sxs-lookup"><span data-stu-id="772a0-134">OData values</span></span>
* <span data-ttu-id="772a0-135">SVMLight 資料 (.svmlight) (請參閱 [SVMLight 定義](http://svmlight.joachims.org/) 以了解格式資訊)</span><span class="sxs-lookup"><span data-stu-id="772a0-135">SVMLight data (.svmlight) (see the [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="772a0-136">屬性關係檔案格式 (ARFF) 資料 (.arff) (請參閱 [ARFF 定義](http://weka.wikispaces.com/ARFF) 以了解格式資訊)</span><span class="sxs-lookup"><span data-stu-id="772a0-136">Attribute Relation File Format (ARFF) data (.arff) (see the [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="772a0-137">Zip 檔案 (.zip)</span><span class="sxs-lookup"><span data-stu-id="772a0-137">Zip file (.zip)</span></span>
* <span data-ttu-id="772a0-138">R 物件或工作區檔案 (.RData)</span><span class="sxs-lookup"><span data-stu-id="772a0-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="772a0-139">如果您以 ARFF 格式匯入內含中繼資料的資料，Machine Learning Studio 會使用此中繼資料定義每個資料行的標題和資料類型。</span><span class="sxs-lookup"><span data-stu-id="772a0-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata to define the heading and data type of each column.</span></span>

<span data-ttu-id="772a0-140">如果您以 TSV 或 CSV 格式匯入不包含此中繼資料的資料，Machine Learning Studio 會透過取樣資料來推斷每個資料行的資料類型。</span><span class="sxs-lookup"><span data-stu-id="772a0-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers the data type for each column by sampling the data.</span></span> <span data-ttu-id="772a0-141">如果資料也沒有資料行標題，Machine Learning Studio 會提供預設名稱。</span><span class="sxs-lookup"><span data-stu-id="772a0-141">If the data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="772a0-142">您可以使用 [編輯中繼資料][edit-metadata]，明確指定或變更資料行的標題和資料類型。</span><span class="sxs-lookup"><span data-stu-id="772a0-142">You can explicitly specify or change the headings and data types for columns using the [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="772a0-143">Machine Learning Studio 可辨識下列 **資料類型** ：</span><span class="sxs-lookup"><span data-stu-id="772a0-143">The following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="772a0-144">String</span><span class="sxs-lookup"><span data-stu-id="772a0-144">String</span></span>
* <span data-ttu-id="772a0-145">Integer</span><span class="sxs-lookup"><span data-stu-id="772a0-145">Integer</span></span>
* <span data-ttu-id="772a0-146">兩倍</span><span class="sxs-lookup"><span data-stu-id="772a0-146">Double</span></span>
* <span data-ttu-id="772a0-147">Boolean</span><span class="sxs-lookup"><span data-stu-id="772a0-147">Boolean</span></span>
* <span data-ttu-id="772a0-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="772a0-148">DateTime</span></span>
* <span data-ttu-id="772a0-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="772a0-149">TimeSpan</span></span>

<span data-ttu-id="772a0-150">Machine Learning Studio 使用名為***資料表格***的內部資料類型以在模組之間傳遞資料。</span><span class="sxs-lookup"><span data-stu-id="772a0-150">Machine Learning Studio uses an internal data type called ***Data Table*** to pass data between modules.</span></span> <span data-ttu-id="772a0-151">您可以使用[轉換為資料集][convert-to-dataset]模組，明確地將資料轉換為「資料表格」格式。</span><span class="sxs-lookup"><span data-stu-id="772a0-151">You can explicitly convert your data into Data Table format using the [Convert to Dataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="772a0-152">接受「資料表格」以外格式的任何模組，會在將資料傳遞至下一個模組之前，無訊息地將資料轉換為「資料表格」。</span><span class="sxs-lookup"><span data-stu-id="772a0-152">Any module that accepts formats other than Data Table will convert the data to Data Table silently before passing it to the next module.</span></span>

<span data-ttu-id="772a0-153">您可以視需要使用其他轉換模組，將「資料表格」格式轉換回 CSV、TSV、ARFF 或 SVMLight 格式。</span><span class="sxs-lookup"><span data-stu-id="772a0-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="772a0-154">請參閱模組調色盤的 **資料格式轉換** 區段，以取得執行這些功能的模組。</span><span class="sxs-lookup"><span data-stu-id="772a0-154">Look in the **Data Format Conversions** section of the module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

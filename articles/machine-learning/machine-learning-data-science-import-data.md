---
title: "Machine Learning Studio aaaImport 資料 |Microsoft 文件"
description: "如何 tooimport 您 Azure Machine Learning Studio 從各種資料來源的資料。 了解支援的資料類型和資料格式。"
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
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="60f8d-105">從各種資料來源將訓練資料匯入 Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="60f8d-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="60f8d-106">toouse 自己在 Machine Learning Studio toodevelop 和定型預測性分析方案中的資料，您可以：</span><span class="sxs-lookup"><span data-stu-id="60f8d-106">toouse your own data in Machine Learning Studio toodevelop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="60f8d-107">從資料上傳**本機檔案**提前時間從硬碟機 toocreate 工作區中的資料集模組</span><span class="sxs-lookup"><span data-stu-id="60f8d-107">upload data from a **local file** ahead of time from your hard drive toocreate a dataset module in your workspace</span></span>
* <span data-ttu-id="60f8d-108">存取資料，從一種**線上資料來源**實驗執行時使用 hello[匯入資料][ import-data]模組</span><span class="sxs-lookup"><span data-stu-id="60f8d-108">access data from one of several **online data sources** while your experiment is running using hello [Import Data][import-data] module</span></span> 
* <span data-ttu-id="60f8d-109">使用其他 Azure Machine Learning **實驗**中儲存為資料集的資料</span><span class="sxs-lookup"><span data-stu-id="60f8d-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="60f8d-110">使用內部部署 **SQL Server 資料庫**中的資料</span><span class="sxs-lookup"><span data-stu-id="60f8d-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="60f8d-111">每個選項所述其中一個 hello 主題下方的 hello 功能表上。</span><span class="sxs-lookup"><span data-stu-id="60f8d-111">Each of these options is described in one of hello topics on hello menu below.</span></span> <span data-ttu-id="60f8d-112">這些主題顯示如何從各種資料 tooimport 資料來源 toouse Machine Learning Studio 中。</span><span class="sxs-lookup"><span data-stu-id="60f8d-112">These topics show you how tooimport data from these various data sources toouse in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="60f8d-113">Machine Learning Studio 中有一些可用於訓練資料的範例資料集。</span><span class="sxs-lookup"><span data-stu-id="60f8d-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="60f8d-114">如需這些資訊，請參閱[使用 Azure Machine Learning Studio 中的 hello 範例資料集](machine-learning-use-sample-datasets.md))。</span><span class="sxs-lookup"><span data-stu-id="60f8d-114">For information on these, see [Use hello sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="60f8d-115">這個簡介主題也會討論 tooget 資料供 Machine Learning Studio 中的使用方式，並描述支援的資料格式和資料類型。</span><span class="sxs-lookup"><span data-stu-id="60f8d-115">This introductory topic also discusses how tooget data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="60f8d-116">備妥資料以在 Azure Machine Learning Studio 中使用</span><span class="sxs-lookup"><span data-stu-id="60f8d-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="60f8d-117">Machine Learning Studio 是設計的 toowork 矩形或表格式資料，例如結構化資料，從資料庫，不過，在某些情況下可能會使用非矩形的資料或分隔的文字資料。</span><span class="sxs-lookup"><span data-stu-id="60f8d-117">Machine Learning Studio is designed toowork with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="60f8d-118">如果您的資料相對乾淨是最佳狀況。</span><span class="sxs-lookup"><span data-stu-id="60f8d-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="60f8d-119">也就是說，您會想 tootake care of 問題，例如未加引號的字串之前，您將 hello 資料上傳到您的經驗。</span><span class="sxs-lookup"><span data-stu-id="60f8d-119">That is, you'll want tootake care of issues such as unquoted strings before you upload hello data into your experiment.</span></span>

<span data-ttu-id="60f8d-120">但是，Machine Learning Studio 中有模組可讓您在實驗中進行一些資料操作。</span><span class="sxs-lookup"><span data-stu-id="60f8d-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="60f8d-121">根據您要使用的 hello 機器學習演算法，您可能會如何需要 toodecide 您將處理資料結構的問題，例如遺漏值和疏鬆的資料，且可以有幫助的模組。</span><span class="sxs-lookup"><span data-stu-id="60f8d-121">Depending on hello machine learning algorithms you'll be using, you may need toodecide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="60f8d-122">查看 hello**資料轉換**hello 模組調色盤的模組，執行這些功能的一節。</span><span class="sxs-lookup"><span data-stu-id="60f8d-122">Look in hello **Data Transformation** section of hello module palette for modules that perform these functions.</span></span>

<span data-ttu-id="60f8d-123">在您實驗中的任何一點，您可以檢視或下載 hello 按一下 hello 輸出連接埠模組所產生的資料。</span><span class="sxs-lookup"><span data-stu-id="60f8d-123">At any point in your experiment you can view or download hello data that's produced by a module by clicking hello output port.</span></span> <span data-ttu-id="60f8d-124">根據 hello 模組可能會有不同的下載選項可用，或者您可能無法 toovisualize hello 資料在 Machine Learning Studio 中 web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="60f8d-124">Depending on hello module, there may be different download options available, or you may be able toovisualize hello data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="60f8d-125">支援的資料格式和資料類型</span><span class="sxs-lookup"><span data-stu-id="60f8d-125">Data formats and data types supported</span></span>
<span data-ttu-id="60f8d-126">您可以數種資料類型匯入您的經驗，根據哪些機制使用 tooimport 資料和此流量來自：</span><span class="sxs-lookup"><span data-stu-id="60f8d-126">You can import a number of data types into your experiment, depending on what mechanism you use tooimport data and where it's coming from:</span></span>

* <span data-ttu-id="60f8d-127">純文字 (.txt)</span><span class="sxs-lookup"><span data-stu-id="60f8d-127">Plain text (.txt)</span></span>
* <span data-ttu-id="60f8d-128">逗號分隔值 (CSV)，具有標頭 (.csv) 或不具標頭 (.nh.csv)</span><span class="sxs-lookup"><span data-stu-id="60f8d-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="60f8d-129">定位鍵分隔值 (TSV)，具有標頭 (.tsv) 或不具標頭 (.nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="60f8d-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="60f8d-130">Excel 檔案</span><span class="sxs-lookup"><span data-stu-id="60f8d-130">Excel file</span></span>
* <span data-ttu-id="60f8d-131">Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="60f8d-131">Azure table</span></span>
* <span data-ttu-id="60f8d-132">Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="60f8d-132">Hive table</span></span>
* <span data-ttu-id="60f8d-133">SQL 資料庫資料表</span><span class="sxs-lookup"><span data-stu-id="60f8d-133">SQL database table</span></span>
* <span data-ttu-id="60f8d-134">OData 值</span><span class="sxs-lookup"><span data-stu-id="60f8d-134">OData values</span></span>
* <span data-ttu-id="60f8d-135">SVMLight 資料 (.svmlight) (請參閱 hello [SVMLight 定義](http://svmlight.joachims.org/)格式資訊)</span><span class="sxs-lookup"><span data-stu-id="60f8d-135">SVMLight data (.svmlight) (see hello [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="60f8d-136">屬性關聯檔案格式 (ARFF) 資料 (.arff) (請參閱 hello [ARFF 定義](http://weka.wikispaces.com/ARFF)格式資訊)</span><span class="sxs-lookup"><span data-stu-id="60f8d-136">Attribute Relation File Format (ARFF) data (.arff) (see hello [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="60f8d-137">Zip 檔案 (.zip)</span><span class="sxs-lookup"><span data-stu-id="60f8d-137">Zip file (.zip)</span></span>
* <span data-ttu-id="60f8d-138">R 物件或工作區檔案 (.RData)</span><span class="sxs-lookup"><span data-stu-id="60f8d-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="60f8d-139">如果您匯入資料例如 ARFF 包含中繼資料的格式，Machine Learning Studio 會使用此中繼資料 toodefine hello 標題和每個資料行的資料類型。</span><span class="sxs-lookup"><span data-stu-id="60f8d-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata toodefine hello heading and data type of each column.</span></span>

<span data-ttu-id="60f8d-140">如果您匯入資料，例如不包含這個中繼資料的 TSV 或 CSV 格式，Machine Learning Studio 就會由取樣 hello 資料推斷 hello 每個資料行的資料類型。</span><span class="sxs-lookup"><span data-stu-id="60f8d-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers hello data type for each column by sampling hello data.</span></span> <span data-ttu-id="60f8d-141">如果 hello 資料也不會有資料行標題，Machine Learning Studio 提供預設名稱。</span><span class="sxs-lookup"><span data-stu-id="60f8d-141">If hello data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="60f8d-142">您可以明確指定或變更 hello 標題和資料類型資料行使用 hello[編輯中繼資料][edit-metadata]。</span><span class="sxs-lookup"><span data-stu-id="60f8d-142">You can explicitly specify or change hello headings and data types for columns using hello [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="60f8d-143">hello 下列**資料型別**Machine Learning Studio 可辨識：</span><span class="sxs-lookup"><span data-stu-id="60f8d-143">hello following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="60f8d-144">String</span><span class="sxs-lookup"><span data-stu-id="60f8d-144">String</span></span>
* <span data-ttu-id="60f8d-145">Integer</span><span class="sxs-lookup"><span data-stu-id="60f8d-145">Integer</span></span>
* <span data-ttu-id="60f8d-146">兩倍</span><span class="sxs-lookup"><span data-stu-id="60f8d-146">Double</span></span>
* <span data-ttu-id="60f8d-147">Boolean</span><span class="sxs-lookup"><span data-stu-id="60f8d-147">Boolean</span></span>
* <span data-ttu-id="60f8d-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="60f8d-148">DateTime</span></span>
* <span data-ttu-id="60f8d-149">時間範圍</span><span class="sxs-lookup"><span data-stu-id="60f8d-149">TimeSpan</span></span>

<span data-ttu-id="60f8d-150">Machine Learning Studio 使用內部的資料類型呼叫***資料表***toopass 模組之間的資料。</span><span class="sxs-lookup"><span data-stu-id="60f8d-150">Machine Learning Studio uses an internal data type called ***Data Table*** toopass data between modules.</span></span> <span data-ttu-id="60f8d-151">您可以明確將資料轉換成資料表格式使用 hello[轉換 tooDataset] [ convert-to-dataset]模組。</span><span class="sxs-lookup"><span data-stu-id="60f8d-151">You can explicitly convert your data into Data Table format using hello [Convert tooDataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="60f8d-152">任何模組可接受資料表以外的格式會以無訊息模式轉換 hello 資料 tooData 資料表，再將其傳遞 toohello 下一個模組。</span><span class="sxs-lookup"><span data-stu-id="60f8d-152">Any module that accepts formats other than Data Table will convert hello data tooData Table silently before passing it toohello next module.</span></span>

<span data-ttu-id="60f8d-153">您可以視需要使用其他轉換模組，將「資料表格」格式轉換回 CSV、TSV、ARFF 或 SVMLight 格式。</span><span class="sxs-lookup"><span data-stu-id="60f8d-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="60f8d-154">查看 hello**資料格式轉換**hello 模組調色盤的模組，執行這些功能的一節。</span><span class="sxs-lookup"><span data-stu-id="60f8d-154">Look in hello **Data Format Conversions** section of hello module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

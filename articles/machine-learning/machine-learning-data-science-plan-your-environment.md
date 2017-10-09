---
title: "aaaIdentify 案例和規劃您的分析程序-Azure |Microsoft 文件"
description: "考慮一系列重要問題來規劃進階分析環境。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 421520dd-7728-4d29-889c-ebe6a0a6fb07
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: e445973be0d020a4f9949e5c9d8554fbbd4b515f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooidentify-scenarios-and-plan-for-advanced-analytics-data-processing"></a><span data-ttu-id="5d376-103">Tooidentify 案例和規劃的進階分析資料處理</span><span class="sxs-lookup"><span data-stu-id="5d376-103">How tooidentify scenarios and plan for advanced analytics data processing</span></span>
<span data-ttu-id="5d376-104">資源應該您計劃 tooinclude 時設定環境 toodo 進階分析的資料集處理？</span><span class="sxs-lookup"><span data-stu-id="5d376-104">What resources should you plan tooinclude when setting up an environment toodo advanced analytics processing on a dataset?</span></span> <span data-ttu-id="5d376-105">這篇文章會建議一系列的有助於找出 hello 工作和資源相關的問題 tooask 您的案例。</span><span class="sxs-lookup"><span data-stu-id="5d376-105">This article suggests a series of questions tooask that will help identify hello tasks and resources relevant your scenario.</span></span> <span data-ttu-id="5d376-106">predictive analytics 的高階步驟 hello 順序中所述[hello 小組資料科學程序 (TDSP) 是什麼？](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5d376-106">hello order of high-level steps for predictive analytics is outlined in [What is hello Team Data Science Process (TDSP)?](data-science-process-overview.md).</span></span> <span data-ttu-id="5d376-107">每個步驟將 hello 工作相關的 tooyour 特定案例需要特定的資源。</span><span class="sxs-lookup"><span data-stu-id="5d376-107">Each of these steps will require specific resources for hello  tasks relevant tooyour particular scenario.</span></span> <span data-ttu-id="5d376-108">hello 重要的問題 tooidentify 您案例考量資料邏輯特性，hello hello 資料集，和 hello 工具和語言偏好 toodo hello 分析的品質。</span><span class="sxs-lookup"><span data-stu-id="5d376-108">hello key questions tooidentify your scenario concern data logistics, characteristics, hello quality of hello datasets, and hello tools and languages you prefer toodo hello analysis.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="logistic-questions-data-locations-and-movement"></a><span data-ttu-id="5d376-109">邏輯問題：資料位置和移動</span><span class="sxs-lookup"><span data-stu-id="5d376-109">Logistic questions: data locations and movement</span></span>
<span data-ttu-id="5d376-110">hello 羅吉斯問題有關的 hello hello 位置**資料來源**，hello**目標目的地**在 Azure 中，與 hello 資料移動的需求，包括 hello 排程、 數量和資源涉及。</span><span class="sxs-lookup"><span data-stu-id="5d376-110">hello logistic questions concern hello location of hello **data source**, hello **target destination** in Azure, and requirements for moving hello data, including hello schedule, amount and resources involved.</span></span> <span data-ttu-id="5d376-111">hello 資料可能需要 toobe hello 分析程序期間移數次。</span><span class="sxs-lookup"><span data-stu-id="5d376-111">hello data may need toobe moved several times during hello analytics process.</span></span> <span data-ttu-id="5d376-112">常見的案例是到某種形式的 Azure 上儲存體中，然後將 Machine Learning Studio toomove 本機資料。</span><span class="sxs-lookup"><span data-stu-id="5d376-112">A common scenario is toomove local data into some form of storage on Azure and then into Machine Learning Studio.</span></span>

1. <span data-ttu-id="5d376-113">**資料來源是什麼？**</span><span class="sxs-lookup"><span data-stu-id="5d376-113">**What is your data source?**</span></span> <span data-ttu-id="5d376-114">是本機還是 hello 雲端？</span><span class="sxs-lookup"><span data-stu-id="5d376-114">Is it local or in hello cloud?</span></span> <span data-ttu-id="5d376-115">例如：</span><span class="sxs-lookup"><span data-stu-id="5d376-115">For example:</span></span>
   
   * <span data-ttu-id="5d376-116">可公開使用的 HTTP 位址在 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="5d376-116">hello data is publicly available at an HTTP address.</span></span>
   * <span data-ttu-id="5d376-117">hello 資料位於本機或網路檔案位置。</span><span class="sxs-lookup"><span data-stu-id="5d376-117">hello data resides in a local/network file location.</span></span>
   * <span data-ttu-id="5d376-118">hello 資料是在 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="5d376-118">hello data is in a SQL Server database.</span></span>
   * <span data-ttu-id="5d376-119">hello 資料會儲存在 Azure 儲存體容器</span><span class="sxs-lookup"><span data-stu-id="5d376-119">hello data is stored in an Azure storage container</span></span>
2. <span data-ttu-id="5d376-120">**Hello Azure 的目的是什麼？**</span><span class="sxs-lookup"><span data-stu-id="5d376-120">**What is hello Azure destination?**</span></span> <span data-ttu-id="5d376-121">其中是否需要 toobe 為處理，或建立模型？</span><span class="sxs-lookup"><span data-stu-id="5d376-121">Where does it need toobe for processing or modeling?</span></span> <span data-ttu-id="5d376-122">例如：</span><span class="sxs-lookup"><span data-stu-id="5d376-122">For example:</span></span>
   
   * <span data-ttu-id="5d376-123">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="5d376-123">Azure Blob Storage</span></span>
   * <span data-ttu-id="5d376-124">SQL Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="5d376-124">SQL Azure databases</span></span>
   * <span data-ttu-id="5d376-125">在 Azure VM 上的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="5d376-125">SQL Server on Azure VM</span></span>
   * <span data-ttu-id="5d376-126">HDInsight (Azure 上的 Hadoop) 或 Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="5d376-126">HDInsight (Hadoop on Azure) or Hive tables</span></span>
   * <span data-ttu-id="5d376-127">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5d376-127">Azure Machine Learning</span></span>
   * <span data-ttu-id="5d376-128">可裝載的 Azure 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="5d376-128">Mountable Azure virtual hard disks.</span></span>
3. <span data-ttu-id="5d376-129">**您要如何 toomove hello 資料？** hello 下列主題中所述的 hello 程序和資源使用 tooingest 或載入資料到各種不同的儲存和處理環境。</span><span class="sxs-lookup"><span data-stu-id="5d376-129">**How are you going toomove hello data?** hello procedures and resources available tooingest or load data into a variety of different storage and processing environments are outlined in hello following topics.</span></span>
   
   * [<span data-ttu-id="5d376-130">將資料載入至儲存體環境以便進行分析</span><span class="sxs-lookup"><span data-stu-id="5d376-130">Load data into storage environments for analytics</span></span>](machine-learning-data-science-ingest-data.md)
   * <span data-ttu-id="5d376-131">[從各種資料來源將定型資料匯入 Azure Machine Learning Studio](machine-learning-data-science-import-data.md)。</span><span class="sxs-lookup"><span data-stu-id="5d376-131">[Import your training data into Azure Machine Learning Studio from various data sources](machine-learning-data-science-import-data.md).</span></span>
4. <span data-ttu-id="5d376-132">**Hello 資料需要定期移動或移轉期間修改 toobe 嗎？**</span><span class="sxs-lookup"><span data-stu-id="5d376-132">**Does hello data need toobe moved on a regular schedule or modified during migration?**</span></span> <span data-ttu-id="5d376-133">請考慮使用 Azure 資料處理站 (ADF)，資料需求 toobe 持續在移轉時，尤其是混合式案例，用來存取這兩個內部部署和雲端資源與此有關，或何時 hello 資料交易式或需要修改 toobe 或商務邏輯加入 tooit hello 期間正在移轉。</span><span class="sxs-lookup"><span data-stu-id="5d376-133">Consider using Azure Data Factory (ADF) when data needs toobe continually migrated, particularly if a hybrid scenario that accesses both on-premises and cloud resources is involved, or when hello data is transacted or needs toobe modified or have business logic added tooit in hello course of being migrated.</span></span> <span data-ttu-id="5d376-134">如需詳細資訊，請參閱[移動資料從內部部署 SQL server tooSQL Azure 與 Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md)</span><span class="sxs-lookup"><span data-stu-id="5d376-134">For further information, see [Move data from an on-premises SQL server tooSQL Azure with Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md)</span></span>
5. <span data-ttu-id="5d376-135">**Hello 資料中有多少是移動 toobe tooAzure？**</span><span class="sxs-lookup"><span data-stu-id="5d376-135">**How much of hello data is toobe moved tooAzure?**</span></span> <span data-ttu-id="5d376-136">非常大的資料集可能會超過特定環境的 hello 儲存容量。</span><span class="sxs-lookup"><span data-stu-id="5d376-136">Datasets that are very large may exceed hello storage capacity of certain environments.</span></span> <span data-ttu-id="5d376-137">如需範例，請參閱 hello 討論的大小限制為 Machine Learning Studio hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="5d376-137">For an example, see hello discussion of size limits for Machine Learning Studio in hello next section.</span></span> <span data-ttu-id="5d376-138">在這種情況下可能 hello 分析期間使用 hello 資料的範例。</span><span class="sxs-lookup"><span data-stu-id="5d376-138">In such cases a sample of hello data may be used during hello analysis.</span></span> <span data-ttu-id="5d376-139">如需如何 toodown 範例資料集在各種 Azure 環境的詳細資訊，請參閱[範例 hello 小組資料科學程序中的資料](machine-learning-data-science-sample-data.md)。</span><span class="sxs-lookup"><span data-stu-id="5d376-139">For details of how toodown-sample a dataset in various Azure environments, see [Sample data in hello Team Data Science Process](machine-learning-data-science-sample-data.md).</span></span>

## <a name="data-characteristics-questions-type-format-and-size"></a><span data-ttu-id="5d376-140">資料特性問題：類型、格式和大小</span><span class="sxs-lookup"><span data-stu-id="5d376-140">Data characteristics questions: type, format and size</span></span>
<span data-ttu-id="5d376-141">這些問題是您的儲存體金鑰 tooplanning 和處理的環境，其中每一個都是適當 toovarious 和每一種類型的資料有一些限制。</span><span class="sxs-lookup"><span data-stu-id="5d376-141">These questions are key tooplanning your storage and processing environments, each of which are appropriate toovarious types of data and each of which have certain restrictions.</span></span>

1. <span data-ttu-id="5d376-142">**Hello 資料類型為何？**</span><span class="sxs-lookup"><span data-stu-id="5d376-142">**What are hello data types?**</span></span> <span data-ttu-id="5d376-143">例如：</span><span class="sxs-lookup"><span data-stu-id="5d376-143">For Example:</span></span>
   
   * <span data-ttu-id="5d376-144">數值</span><span class="sxs-lookup"><span data-stu-id="5d376-144">Numerical</span></span>
   * <span data-ttu-id="5d376-145">類別</span><span class="sxs-lookup"><span data-stu-id="5d376-145">Categorical</span></span>
   * <span data-ttu-id="5d376-146">字串</span><span class="sxs-lookup"><span data-stu-id="5d376-146">Strings</span></span>
   * <span data-ttu-id="5d376-147">Binary</span><span class="sxs-lookup"><span data-stu-id="5d376-147">Binary</span></span>
2. <span data-ttu-id="5d376-148">**如何將資料格式化？**</span><span class="sxs-lookup"><span data-stu-id="5d376-148">**How is your data formatted?**</span></span> <span data-ttu-id="5d376-149">例如：</span><span class="sxs-lookup"><span data-stu-id="5d376-149">For Example:</span></span>
   
   * <span data-ttu-id="5d376-150">逗號分隔 (CSV) 或定位鍵分隔 (TSV) 一般檔案</span><span class="sxs-lookup"><span data-stu-id="5d376-150">Comma-separated (CSV) or tab-separated (TSV) flat files</span></span>
   * <span data-ttu-id="5d376-151">已壓縮或未壓縮</span><span class="sxs-lookup"><span data-stu-id="5d376-151">Compressed or uncompressed</span></span>
   * <span data-ttu-id="5d376-152">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="5d376-152">Azure blobs</span></span>
   * <span data-ttu-id="5d376-153">Hadoop Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="5d376-153">Hadoop Hive tables</span></span>
   * <span data-ttu-id="5d376-154">SQL Server 資料表</span><span class="sxs-lookup"><span data-stu-id="5d376-154">SQL Server tables</span></span>
3. <span data-ttu-id="5d376-155">**您的資料大小為何？**</span><span class="sxs-lookup"><span data-stu-id="5d376-155">**How large is your data?**</span></span>
   
   * <span data-ttu-id="5d376-156">小型：小於 2 GB</span><span class="sxs-lookup"><span data-stu-id="5d376-156">Small: Less than 2GB</span></span>
   * <span data-ttu-id="5d376-157">中型：大於 2 GB 且小於 10 GB</span><span class="sxs-lookup"><span data-stu-id="5d376-157">Medium: Greater than 2GB and less than 10GB</span></span>
   * <span data-ttu-id="5d376-158">大型：大於 10 GB</span><span class="sxs-lookup"><span data-stu-id="5d376-158">Large: Greater than 10GB</span></span>

<span data-ttu-id="5d376-159">Hello Azure Machine Learning Studio 環境為例：</span><span class="sxs-lookup"><span data-stu-id="5d376-159">Take hello Azure Machine Learning Studio environment for example:</span></span>

* <span data-ttu-id="5d376-160">如需 hello 資料格式和 Azure Machine Learning Studio 所支援類型的清單，請參閱[資料格式和支援的資料型別](machine-learning-data-science-import-data.md#data-formats-and-data-types-supported)> 一節。</span><span class="sxs-lookup"><span data-stu-id="5d376-160">For a list of hello data formats and types supported by Azure Machine Learning Studio, see [Data formats and data types supported](machine-learning-data-science-import-data.md#data-formats-and-data-types-supported) section.</span></span>
* <span data-ttu-id="5d376-161">如需 Azure Machine Learning Studio 中的資料限制資訊，請參閱 hello**大 hello 資料集可適用於我模組？**區段[匯入及匯出資料的機器學習](machine-learning-faq.md#machine-learning-studio-questions)</span><span class="sxs-lookup"><span data-stu-id="5d376-161">For information on data limitations for Azure Machine Learning Studio, see hello **How large can hello data set be for my modules?** section of [Importing and exporting data for Machine Learning](machine-learning-faq.md#machine-learning-studio-questions)</span></span>

<span data-ttu-id="5d376-162">Hello 限制 hello 分析程序中使用其他 Azure 服務的詳細資訊，請參閱[Azure 訂用帳戶和服務限制、 配額和條件約束](../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="5d376-162">For information on hello limitations of other Azure services used in hello analytics process, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

## <a name="data-quality-questions-exploration-and-pre-processing"></a><span data-ttu-id="5d376-163">資料品質問題：探索和前置處理</span><span class="sxs-lookup"><span data-stu-id="5d376-163">Data quality questions: exploration and pre-processing</span></span>
1. <span data-ttu-id="5d376-164">**您對資料的熟悉程度為何？**</span><span class="sxs-lookup"><span data-stu-id="5d376-164">**What do you know about your data?**</span></span> <span data-ttu-id="5d376-165">瀏覽資料時需要 toogain 了解其基本特性。</span><span class="sxs-lookup"><span data-stu-id="5d376-165">Explore data when you need toogain an understand its basic characteristics.</span></span> <span data-ttu-id="5d376-166">資料呈現什麼模式或趨勢、有什麼極端值或遺漏多少值。</span><span class="sxs-lookup"><span data-stu-id="5d376-166">What patterns or trends it exhibits, what outliers is has or how many values are missing.</span></span> <span data-ttu-id="5d376-167">這個步驟很重要決定 hello 需要制定假設，藉以而建議 hello 最適當的功能，或輸入的分析，以及制定計劃的其他資料收集的前置處理的程度。</span><span class="sxs-lookup"><span data-stu-id="5d376-167">This step is important for determining hello extent of pre-processing needed, for formulating hypotheses that could suggest hello most appropriate features or type of analysis, and for formulating plans for additional data collection.</span></span> <span data-ttu-id="5d376-168">計算描述性統計資料和繪製視覺效果是很有用的資料檢查技術。</span><span class="sxs-lookup"><span data-stu-id="5d376-168">Calculating descriptive statistics and plotting visualizations are useful techniques for data inspection.</span></span> <span data-ttu-id="5d376-169">如需詳細資訊的方式 tooexplore 資料集在各種 Azure 環境中，請參閱[hello 小組資料科學程序中的資料瀏覽](machine-learning-data-science-explore-data.md)。</span><span class="sxs-lookup"><span data-stu-id="5d376-169">For details of how tooexplore a dataset in various Azure environments, see [Explore data in hello Team Data Science Process](machine-learning-data-science-explore-data.md).</span></span>
2. <span data-ttu-id="5d376-170">**Hello 資料需要前置處理，或清除嗎？**</span><span class="sxs-lookup"><span data-stu-id="5d376-170">**Does hello data require pre-processing or cleaning?**</span></span>
   <span data-ttu-id="5d376-171">前置處理和清除資料是很重要的工作，必須先執行這些工作，才能有效地將資料集用於機器學習服務。</span><span class="sxs-lookup"><span data-stu-id="5d376-171">Pre-processing and cleaning data are important tasks that typically must be conducted before dataset can be used effectively for machine learning.</span></span> <span data-ttu-id="5d376-172">未經處理的資料通常會有雜訊且不可靠，還可能會有遺漏值。</span><span class="sxs-lookup"><span data-stu-id="5d376-172">Raw data is often noisy and unreliable, and may be missing values.</span></span> <span data-ttu-id="5d376-173">使用這類資料進行模型化可能會產生誤導的結果。</span><span class="sxs-lookup"><span data-stu-id="5d376-173">Using such data for modeling can produce misleading results.</span></span> <span data-ttu-id="5d376-174">如需說明，請參閱[任務 tooprepare 資料增強的機器學習](machine-learning-data-science-prepare-data.md)。</span><span class="sxs-lookup"><span data-stu-id="5d376-174">For a description, see [Tasks tooprepare data for enhanced machine learning](machine-learning-data-science-prepare-data.md).</span></span>

## <a name="tools-and-languages-questions"></a><span data-ttu-id="5d376-175">工具和語言的問題</span><span class="sxs-lookup"><span data-stu-id="5d376-175">Tools and languages questions</span></span>
<span data-ttu-id="5d376-176">根據您需要或最喜歡使用的語言和開發環境或工具而定，這裡有許多選項可選擇。</span><span class="sxs-lookup"><span data-stu-id="5d376-176">There are lots of options here depending on what languages and development environments or tools you need or are most conformable using.</span></span>

1. <span data-ttu-id="5d376-177">**語言怎麼辦偏好 toouse 分析？**</span><span class="sxs-lookup"><span data-stu-id="5d376-177">**What languages do you prefer toouse for analysis?**</span></span>  
   
   * <span data-ttu-id="5d376-178">R</span><span class="sxs-lookup"><span data-stu-id="5d376-178">R</span></span>
   * <span data-ttu-id="5d376-179">Python</span><span class="sxs-lookup"><span data-stu-id="5d376-179">Python</span></span>
   * <span data-ttu-id="5d376-180">SQL</span><span class="sxs-lookup"><span data-stu-id="5d376-180">SQL</span></span>
2. <span data-ttu-id="5d376-181">**您應該使用哪些工具進行資料分析？**</span><span class="sxs-lookup"><span data-stu-id="5d376-181">**What tools should you use for data analysis?**</span></span>
   
   * <span data-ttu-id="5d376-182">[Microsoft Azure Powershell](/powershell/azure/overview) -指令碼語言 tooadminister 您的 Azure 資源中使用指令碼語言。</span><span class="sxs-lookup"><span data-stu-id="5d376-182">[Microsoft Azure Powershell](/powershell/azure/overview) - a script language used tooadminister your Azure resources in a script language.</span></span>
   * [<span data-ttu-id="5d376-183">Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5d376-183">Azure Machine Learning Studio</span></span>](machine-learning-what-is-ml-studio.md)
   * [<span data-ttu-id="5d376-184">Revolution Analytics</span><span class="sxs-lookup"><span data-stu-id="5d376-184">Revolution Analytics</span></span>](http://www.revolutionanalytics.com/revolution-r-open)
   * [<span data-ttu-id="5d376-185">RStudio</span><span class="sxs-lookup"><span data-stu-id="5d376-185">RStudio</span></span>](http://www.rstudio.com)
   * [<span data-ttu-id="5d376-186">Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5d376-186">Python Tools for Visual Studio</span></span>](http://microsoft.github.io/PTVS/)
   * [<span data-ttu-id="5d376-187">Anaconda</span><span class="sxs-lookup"><span data-stu-id="5d376-187">Anaconda</span></span>](https://www.continuum.io/why-anaconda)
   * [<span data-ttu-id="5d376-188">Jupyter 筆記本</span><span class="sxs-lookup"><span data-stu-id="5d376-188">Jupyter notebooks</span></span>](http://jupyter.org/)
   * [<span data-ttu-id="5d376-189">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="5d376-189">Microsoft Power BI</span></span>](http://powerbi.microsoft.com)

## <a name="identify-your-advanced-analytics-scenario"></a><span data-ttu-id="5d376-190">識別您的進階分析案例</span><span class="sxs-lookup"><span data-stu-id="5d376-190">Identify your advanced analytics scenario</span></span>
<span data-ttu-id="5d376-191">一旦您已回答 hello 上一節中的 hello 問題，即準備好 toodetermine 最佳的案例符合您的案例。</span><span class="sxs-lookup"><span data-stu-id="5d376-191">Once you have answered hello questions in hello previous section, you are ready toodetermine which scenario best fits your case.</span></span> <span data-ttu-id="5d376-192">hello 範例案例所述[Azure Machine Learning 中的進階分析的案例](machine-learning-data-science-plan-sample-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="5d376-192">hello sample scenarios are outlined in [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md).</span></span>


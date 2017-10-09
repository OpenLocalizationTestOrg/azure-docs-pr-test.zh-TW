---
title: "Azure Machine Learning 的進階分析案例 aaaIdentify |Microsoft 文件"
description: "選取適當 hello 的案例提供執行進階預測分析以 hello 小組資料科學程序。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="b54f6-103">在 Azure 機器學習中的進階分析案例</span><span class="sxs-lookup"><span data-stu-id="b54f6-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="b54f6-104">本文概述 hello 各種不同的範例資料來源和目標案例，可以由 hello[小組資料科學程序 (TDSP)](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-104">This article outlines hello variety of sample data sources and target scenarios that can be handled by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="b54f6-105">hello TDSP 小組 toocollaborate 上建置的智慧型應用程式提供系統化的方法。</span><span class="sxs-lookup"><span data-stu-id="b54f6-105">hello TDSP provides a systematic approach for teams toocollaborate on building intelligent applications.</span></span> <span data-ttu-id="b54f6-106">這裡所呈現的 hello 案例說明可用的選項 hello 資料處理工作流程中的 hello 資料特性、 來源位置，以及在 Azure 中的目標儲存機制而定。</span><span class="sxs-lookup"><span data-stu-id="b54f6-106">hello scenarios presented here illustrate options available in hello data processing workflow that depend on hello data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="b54f6-107">hello**決策樹**的選取適合您的資料和目標的 hello 範例案例會以 hello 最後一節。</span><span class="sxs-lookup"><span data-stu-id="b54f6-107">hello **decision tree** for selecting hello sample scenarios that is appropriate for your data and objective is presented in hello last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="b54f6-108">每個 hello 下列各節提供範例案例。</span><span class="sxs-lookup"><span data-stu-id="b54f6-108">Each of hello following sections presents a sample scenario.</span></span> <span data-ttu-id="b54f6-109">在每個案例中，都會列出可能的資料科學或進階分析流程，以及支援的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="b54f6-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="b54f6-110">**針對所有 hello 下列案例中，您都需要：**
> </span><span class="sxs-lookup"><span data-stu-id="b54f6-110">**For all of hello following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="b54f6-111">[建立儲存體帳戶](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="b54f6-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="b54f6-112">建立 Azure Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="b54f6-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="b54f6-113"><a name="smalllocal"></a>案例\#1： 小 toomedium 本機檔案中的表格式資料集</span><span class="sxs-lookup"><span data-stu-id="b54f6-113"><a name="smalllocal"></a>Scenario \#1: Small toomedium tabular dataset in a local files</span></span>
![小型 toomedium 本機檔案][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="b54f6-115">其他 Azure 資源：無</span><span class="sxs-lookup"><span data-stu-id="b54f6-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="b54f6-116">登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-116">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="b54f6-117">上傳資料集。</span><span class="sxs-lookup"><span data-stu-id="b54f6-117">Upload a dataset.</span></span>
3. <span data-ttu-id="b54f6-118">建置從上傳的資料集開始的 Azure 機器學習實驗流程。</span><span class="sxs-lookup"><span data-stu-id="b54f6-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="b54f6-119"><a name="smalllocalprocess"></a>案例\#2： 小 toomedium 的本機檔案需要處理的資料集</span><span class="sxs-lookup"><span data-stu-id="b54f6-119"><a name="smalllocalprocess"></a>Scenario \#2: Small toomedium dataset of local files that require processing</span></span>
![處理小型 toomedium 本機檔案][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="b54f6-121">其他 Azure 資源：Azure 虛擬機器 (IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="b54f6-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="b54f6-122">建立執行 IPython Notebook 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b54f6-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="b54f6-123">上傳資料 tooan Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="b54f6-123">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="b54f6-124">前置處理和清除 IPython Notebook 中的資料 (從 Azure 儲存體容器存取資料)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="b54f6-125">轉換資料 toocleaned，表格形式。</span><span class="sxs-lookup"><span data-stu-id="b54f6-125">Transform data toocleaned, tabular form.</span></span>
5. <span data-ttu-id="b54f6-126">將轉換的資料儲存在 Azure Blob 中。</span><span class="sxs-lookup"><span data-stu-id="b54f6-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="b54f6-127">登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-127">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="b54f6-128">讀取 hello 資料從 Azure blob 使用 hello[匯入資料][ import-data]模組。</span><span class="sxs-lookup"><span data-stu-id="b54f6-128">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="b54f6-129">建置從內嵌的資料集開始的 Azure 機器學習實驗流程。</span><span class="sxs-lookup"><span data-stu-id="b54f6-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="b54f6-130"><a name="largelocal"></a>案例 \#3：本機檔案的大型資料集，以 Azure Blob 為目標</span><span class="sxs-lookup"><span data-stu-id="b54f6-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![大型本機檔案][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="b54f6-132">其他 Azure 資源：Azure 虛擬機器 (IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="b54f6-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="b54f6-133">建立執行 IPython Notebook 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b54f6-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="b54f6-134">上傳資料 tooan Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="b54f6-134">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="b54f6-135">前置處理和清除 IPython Notebook 中的資料 (從 Azure Blob 存取資料)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="b54f6-136">如有需要轉換資料 toocleaned，表格式。</span><span class="sxs-lookup"><span data-stu-id="b54f6-136">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="b54f6-137">視需要瀏覽資料並建立功能。</span><span class="sxs-lookup"><span data-stu-id="b54f6-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="b54f6-138">擷取中小型資料範例。</span><span class="sxs-lookup"><span data-stu-id="b54f6-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="b54f6-139">在 Azure blob 儲存 hello 取樣資料。</span><span class="sxs-lookup"><span data-stu-id="b54f6-139">Save hello sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="b54f6-140">登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-140">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="b54f6-141">讀取 hello 資料從 Azure blob 使用 hello[匯入資料][ import-data]模組。</span><span class="sxs-lookup"><span data-stu-id="b54f6-141">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="b54f6-142">建置從內嵌的資料集開始的 Azure 機器學習實驗流程。</span><span class="sxs-lookup"><span data-stu-id="b54f6-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="b54f6-143"><a name="smalllocaltodb"></a>案例\#4： 小 toomedium 資料集的目標 Azure 虛擬機器中的 SQL Server 的本機檔案</span><span class="sxs-lookup"><span data-stu-id="b54f6-143"><a name="smalllocaltodb"></a>Scenario \#4: Small toomedium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![在 Azure 中的小型 toomedium 本機檔案 tooSQL DB][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="b54f6-145">其他 Azure 資源：Azure 虛擬機器 (SQL Server / IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="b54f6-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="b54f6-146">建立執行 SQL Server + IPython Notebook 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b54f6-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="b54f6-147">上傳資料 tooan Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="b54f6-147">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="b54f6-148">使用 IPython Notebook 前置處理和清除 Azure 儲存體容器中的資料。</span><span class="sxs-lookup"><span data-stu-id="b54f6-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="b54f6-149">如有需要轉換資料 toocleaned，表格式。</span><span class="sxs-lookup"><span data-stu-id="b54f6-149">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="b54f6-150">儲存資料 tooVM 本機檔案 （IPython 筆記型電腦在 VM 上執行，本機磁碟機，請參閱 tooVM 磁碟機）。</span><span class="sxs-lookup"><span data-stu-id="b54f6-150">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
6. <span data-ttu-id="b54f6-151">在 Azure VM 上執行負載資料 tooSQL 伺服器資料庫。</span><span class="sxs-lookup"><span data-stu-id="b54f6-151">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="b54f6-152">選項 \#1：使用 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="b54f6-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="b54f6-153">登入 tooSQL Server VM</span><span class="sxs-lookup"><span data-stu-id="b54f6-153">Login tooSQL Server VM</span></span>
   * <span data-ttu-id="b54f6-154">執行 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="b54f6-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="b54f6-155">建立資料庫和目標資料表。</span><span class="sxs-lookup"><span data-stu-id="b54f6-155">Create database and target tables.</span></span>
   * <span data-ttu-id="b54f6-156">從 VM 本機檔案，使用其中一個 hello 大量匯入方法 tooload hello 資料。</span><span class="sxs-lookup"><span data-stu-id="b54f6-156">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
   
   <span data-ttu-id="b54f6-157">選項 \#2：使用 IPython Notebook – 不建議用於中型和大型資料集</span><span class="sxs-lookup"><span data-stu-id="b54f6-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="b54f6-158">使用 ODBC 連接字串 tooaccess SQL Server VM 上。</span><span class="sxs-lookup"><span data-stu-id="b54f6-158">Use ODBC connection string tooaccess SQL Server on VM.</span></span>
   * <span data-ttu-id="b54f6-159">建立資料庫和目標資料表。</span><span class="sxs-lookup"><span data-stu-id="b54f6-159">Create database and target tables.</span></span>
   * <span data-ttu-id="b54f6-160">從 VM 本機檔案，使用其中一個 hello 大量匯入方法 tooload hello 資料。</span><span class="sxs-lookup"><span data-stu-id="b54f6-160">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
7. <span data-ttu-id="b54f6-161">視需要瀏覽資料並建立功能。</span><span class="sxs-lookup"><span data-stu-id="b54f6-161">Explore data, create features as needed.</span></span> <span data-ttu-id="b54f6-162">請注意，hello 功能不需要 toobe hello 資料庫資料表中具體化。</span><span class="sxs-lookup"><span data-stu-id="b54f6-162">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="b54f6-163">只有附註 hello 必要查詢 toocreate 它們。</span><span class="sxs-lookup"><span data-stu-id="b54f6-163">Only note hello necessary query toocreate them.</span></span>
8. <span data-ttu-id="b54f6-164">若有需要，請決定資料範例大小。</span><span class="sxs-lookup"><span data-stu-id="b54f6-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="b54f6-165">登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-165">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="b54f6-166">讀取的 hello 資料直接從 hello SQL Server 使用 hello[匯入資料][ import-data]模組。</span><span class="sxs-lookup"><span data-stu-id="b54f6-166">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="b54f6-167">貼上 hello 必要查詢擷取的欄位，建立功能，以及範例資料，如有需要直接在 hello[匯入資料][ import-data]查詢。</span><span class="sxs-lookup"><span data-stu-id="b54f6-167">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="b54f6-168">建置從內嵌的資料集開始的 Azure 機器學習實驗流程。</span><span class="sxs-lookup"><span data-stu-id="b54f6-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="b54f6-169"><a name="largelocaltodb"></a>案例 \#5：本機資料中的大型資料集，目標 Azure VM 中的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="b54f6-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![在 Azure 中的大型的本機檔案 tooSQL DB][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="b54f6-171">其他 Azure 資源：Azure 虛擬機器 (SQL Server / IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="b54f6-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="b54f6-172">建立執行 SQL Server 和 IPython Notebook 伺服器的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b54f6-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="b54f6-173">上傳資料 tooan Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="b54f6-173">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="b54f6-174">(選擇性) 前置處理和清除資料。</span><span class="sxs-lookup"><span data-stu-id="b54f6-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="b54f6-175">a.</span><span class="sxs-lookup"><span data-stu-id="b54f6-175">a.</span></span>  <span data-ttu-id="b54f6-176">前置處理和清除 IPython Notebook 中的資料，從 Azure 存取資料</span><span class="sxs-lookup"><span data-stu-id="b54f6-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="b54f6-177">b.</span><span class="sxs-lookup"><span data-stu-id="b54f6-177">b.</span></span>  <span data-ttu-id="b54f6-178">如有需要轉換資料 toocleaned，表格式。</span><span class="sxs-lookup"><span data-stu-id="b54f6-178">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="b54f6-179">c.</span><span class="sxs-lookup"><span data-stu-id="b54f6-179">c.</span></span>  <span data-ttu-id="b54f6-180">儲存資料 tooVM 本機檔案 （IPython 筆記型電腦在 VM 上執行，本機磁碟機，請參閱 tooVM 磁碟機）。</span><span class="sxs-lookup"><span data-stu-id="b54f6-180">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="b54f6-181">在 Azure VM 上執行負載資料 tooSQL 伺服器資料庫。</span><span class="sxs-lookup"><span data-stu-id="b54f6-181">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="b54f6-182">a.</span><span class="sxs-lookup"><span data-stu-id="b54f6-182">a.</span></span>  <span data-ttu-id="b54f6-183">登入 tooSQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="b54f6-183">Login tooSQL Server VM.</span></span>
   
   <span data-ttu-id="b54f6-184">b.</span><span class="sxs-lookup"><span data-stu-id="b54f6-184">b.</span></span>  <span data-ttu-id="b54f6-185">如果資料尚未儲存，請從 Azure 下載資料檔案</span><span class="sxs-lookup"><span data-stu-id="b54f6-185">If data not saved already, download data files from Azure</span></span>
   
       storage container toolocal-VM folder.
   
   <span data-ttu-id="b54f6-186">c.</span><span class="sxs-lookup"><span data-stu-id="b54f6-186">c.</span></span>  <span data-ttu-id="b54f6-187">執行 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="b54f6-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="b54f6-188">d.</span><span class="sxs-lookup"><span data-stu-id="b54f6-188">d.</span></span>  <span data-ttu-id="b54f6-189">建立資料庫和目標資料表。</span><span class="sxs-lookup"><span data-stu-id="b54f6-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="b54f6-190">e.</span><span class="sxs-lookup"><span data-stu-id="b54f6-190">e.</span></span>  <span data-ttu-id="b54f6-191">使用其中一個 hello 大量匯入方法 tooload hello 資料。</span><span class="sxs-lookup"><span data-stu-id="b54f6-191">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="b54f6-192">f.</span><span class="sxs-lookup"><span data-stu-id="b54f6-192">f.</span></span>  <span data-ttu-id="b54f6-193">如果需要資料表聯結，來建立索引 tooexpedite 聯結。</span><span class="sxs-lookup"><span data-stu-id="b54f6-193">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b54f6-194">大型的資料大小更快載入，建議您建立資料分割的資料表和資料大量匯入 hello 以平行方式。</span><span class="sxs-lookup"><span data-stu-id="b54f6-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import hello data in parallel.</span></span> <span data-ttu-id="b54f6-195">如需詳細資訊，請參閱[平行資料匯入 tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-195">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="b54f6-196">視需要瀏覽資料並建立功能。</span><span class="sxs-lookup"><span data-stu-id="b54f6-196">Explore data, create features as needed.</span></span> <span data-ttu-id="b54f6-197">請注意，hello 功能不需要 toobe hello 資料庫資料表中具體化。</span><span class="sxs-lookup"><span data-stu-id="b54f6-197">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="b54f6-198">只有附註 hello 必要查詢 toocreate 它們。</span><span class="sxs-lookup"><span data-stu-id="b54f6-198">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="b54f6-199">若有需要，請決定資料範例大小。</span><span class="sxs-lookup"><span data-stu-id="b54f6-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="b54f6-200">登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-200">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="b54f6-201">讀取的 hello 資料直接從 hello SQL Server 使用 hello[匯入資料][ import-data]模組。</span><span class="sxs-lookup"><span data-stu-id="b54f6-201">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="b54f6-202">貼上 hello 必要查詢擷取的欄位，建立功能，以及範例資料，如有需要直接在 hello[匯入資料][ import-data]查詢。</span><span class="sxs-lookup"><span data-stu-id="b54f6-202">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="b54f6-203">從上傳的資料集開始的簡單 Azure Machine Learning 實驗流程</span><span class="sxs-lookup"><span data-stu-id="b54f6-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="b54f6-204"><a name="largedbtodb"></a>案例 \#6：SQL Server 資料庫內部部署中的大型資料集，以 Azure 虛擬機器中的 SQL Server 為目標</span><span class="sxs-lookup"><span data-stu-id="b54f6-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![在 Azure 中的大型 SQL 資料庫內部 tooSQL DB][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="b54f6-206">其他 Azure 資源：Azure 虛擬機器 (SQL Server / IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="b54f6-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="b54f6-207">建立執行 SQL Server 和 IPython Notebook 伺服器的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b54f6-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="b54f6-208">使用其中一個 hello 資料從 SQL Server toodump 檔案匯出方法 tooexport hello 資料。</span><span class="sxs-lookup"><span data-stu-id="b54f6-208">Use one of hello data export methods tooexport hello data from SQL Server toodump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b54f6-209">如果您決定 toomove hello 內部資料庫，替代 （較快） 方法 toomove hello 完整資料庫 toothe SQL Server 執行個體在 Azure 中的所有資料。</span><span class="sxs-lookup"><span data-stu-id="b54f6-209">If you decide toomove all data from hello on-prem database, an alternate (faster) method toomove hello full database toothe SQL Server instance in Azure.</span></span> <span data-ttu-id="b54f6-210">略過 hello 步驟 tooexport 資料、 建立資料庫，以及負載/匯入資料 toohello 目標資料庫，並遵循 hello 替代方法。</span><span class="sxs-lookup"><span data-stu-id="b54f6-210">Skip hello steps tooexport data, create database, and load/import data toohello target database and follow hello alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="b54f6-211">上傳傾印檔案 tooAzure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="b54f6-211">Upload dump files tooAzure storage container.</span></span>
4. <span data-ttu-id="b54f6-212">載入執行 Azure 虛擬機器上的 hello 資料 tooa SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b54f6-212">Load hello data tooa SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="b54f6-213">a.</span><span class="sxs-lookup"><span data-stu-id="b54f6-213">a.</span></span>  <span data-ttu-id="b54f6-214">登入 toohello SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="b54f6-214">Login toohello SQL Server VM.</span></span>
   
   <span data-ttu-id="b54f6-215">b.</span><span class="sxs-lookup"><span data-stu-id="b54f6-215">b.</span></span>  <span data-ttu-id="b54f6-216">從 Azure 儲存體容器 toohello 本機 VM 資料夾下載資料檔案。</span><span class="sxs-lookup"><span data-stu-id="b54f6-216">Download data files from an Azure storage container toohello local-VM folder.</span></span>
   
   <span data-ttu-id="b54f6-217">c.</span><span class="sxs-lookup"><span data-stu-id="b54f6-217">c.</span></span>  <span data-ttu-id="b54f6-218">執行 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="b54f6-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="b54f6-219">d.</span><span class="sxs-lookup"><span data-stu-id="b54f6-219">d.</span></span>  <span data-ttu-id="b54f6-220">建立資料庫和目標資料表。</span><span class="sxs-lookup"><span data-stu-id="b54f6-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="b54f6-221">e.</span><span class="sxs-lookup"><span data-stu-id="b54f6-221">e.</span></span>  <span data-ttu-id="b54f6-222">使用其中一個 hello 大量匯入方法 tooload hello 資料。</span><span class="sxs-lookup"><span data-stu-id="b54f6-222">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="b54f6-223">f.</span><span class="sxs-lookup"><span data-stu-id="b54f6-223">f.</span></span>  <span data-ttu-id="b54f6-224">如果需要資料表聯結，來建立索引 tooexpedite 聯結。</span><span class="sxs-lookup"><span data-stu-id="b54f6-224">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b54f6-225">更快載入大型的資料大小，建立資料分割的資料表和 toobulk hello 資料匯入以平行方式。</span><span class="sxs-lookup"><span data-stu-id="b54f6-225">For faster loading of large data sizes, create partitioned tables and toobulk import hello data in parallel.</span></span> <span data-ttu-id="b54f6-226">如需詳細資訊，請參閱[平行資料匯入 tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-226">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="b54f6-227">視需要瀏覽資料並建立功能。</span><span class="sxs-lookup"><span data-stu-id="b54f6-227">Explore data, create features as needed.</span></span> <span data-ttu-id="b54f6-228">請注意，hello 功能不需要 toobe hello 資料庫資料表中具體化。</span><span class="sxs-lookup"><span data-stu-id="b54f6-228">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="b54f6-229">只有附註 hello 必要查詢 toocreate 它們。</span><span class="sxs-lookup"><span data-stu-id="b54f6-229">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="b54f6-230">若有需要，請決定資料範例大小。</span><span class="sxs-lookup"><span data-stu-id="b54f6-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="b54f6-231">登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-231">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="b54f6-232">讀取的 hello 資料直接從 hello SQL Server 使用 hello[匯入資料][ import-data]模組。</span><span class="sxs-lookup"><span data-stu-id="b54f6-232">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="b54f6-233">貼上 hello 必要查詢擷取的欄位，建立功能，以及範例資料，如有需要直接在 hello[匯入資料][ import-data]查詢。</span><span class="sxs-lookup"><span data-stu-id="b54f6-233">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="b54f6-234">從上傳的資料集開始的簡單 Azure Machine Learning 實驗流程。</span><span class="sxs-lookup"><span data-stu-id="b54f6-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a><span data-ttu-id="b54f6-235">替代方法 toocopy 完整的資料庫從內部部署 SQL Server tooAzure SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="b54f6-235">Alternate method toocopy a full database from an on-premises  SQL Server tooAzure SQL Database</span></span>
![Local DB 卸離和附加 tooSQL DB 在 Azure 中][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="b54f6-237">其他 Azure 資源：Azure 虛擬機器 (SQL Server / IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="b54f6-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="b54f6-238">tooreplicate hello 整個 SQL Server 資料庫的 SQL Server VM，您應該複製資料庫從一個位置/伺服器 tooanother，假設該 hello 可以讓資料庫離線暫時。</span><span class="sxs-lookup"><span data-stu-id="b54f6-238">tooreplicate hello entire SQL Server database in your SQL Server VM, you should copy a database from one location/server tooanother, assuming that hello database can be taken temporarily offline.</span></span> <span data-ttu-id="b54f6-239">您在 hello SQL Server Management Studio 物件總管 中，或是使用 hello 對等的 TRANSACT-SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="b54f6-239">You do this in hello SQL Server Management Studio Object Explorer, or using hello equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="b54f6-240">卸離 hello hello 來源位置的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b54f6-240">Detach hello database at hello source location.</span></span> <span data-ttu-id="b54f6-241">如需詳細資訊，請參閱[卸離資料庫](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="b54f6-242">在 Windows 檔案總管或 Windows 命令提示字元視窗中，複製 hello 卸離資料庫檔案或檔案和記錄檔或 hello Azure 中的 SQL Server VM 上的檔案 toohello 目標位置。</span><span class="sxs-lookup"><span data-stu-id="b54f6-242">In Windows Explorer or Windows Command Prompt window, copy hello detached database file or files and log file or files toohello target location on hello SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="b54f6-243">附加複製的 hello 檔案 toohello 目標 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b54f6-243">Attach hello copied files toohello target SQL Server instance.</span></span> <span data-ttu-id="b54f6-244">如需詳細資訊，請參閱[連結資料庫](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="b54f6-245">[使用卸離和連結來移動資料庫 (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="b54f6-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="b54f6-246"><a name="largedbtohive"></a>案例 \#7：本機檔案中的巨量資料，目標 Azure HDInsight Hadoop 叢集中的 Hive 資料庫</span><span class="sxs-lookup"><span data-stu-id="b54f6-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![本機目標 Hive 中的巨量資料][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="b54f6-248">其他 Azure 資源：Azure HDInsight Hadoop 叢集和 Azure 虛擬機器 (IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="b54f6-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="b54f6-249">建立執行 IPython Notebook 伺服器的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b54f6-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="b54f6-250">建立 Azure HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="b54f6-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="b54f6-251">(選擇性) 前置處理和清除資料。</span><span class="sxs-lookup"><span data-stu-id="b54f6-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="b54f6-252">a.</span><span class="sxs-lookup"><span data-stu-id="b54f6-252">a.</span></span>  <span data-ttu-id="b54f6-253">前置處理和清除 IPython Notebook 中的資料，從 Azure 存取資料</span><span class="sxs-lookup"><span data-stu-id="b54f6-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="b54f6-254">b.</span><span class="sxs-lookup"><span data-stu-id="b54f6-254">b.</span></span>  <span data-ttu-id="b54f6-255">如有需要轉換資料 toocleaned，表格式。</span><span class="sxs-lookup"><span data-stu-id="b54f6-255">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="b54f6-256">c.</span><span class="sxs-lookup"><span data-stu-id="b54f6-256">c.</span></span>  <span data-ttu-id="b54f6-257">儲存資料 tooVM 本機檔案 （IPython 筆記型電腦在 VM 上執行，本機磁碟機，請參閱 tooVM 磁碟機）。</span><span class="sxs-lookup"><span data-stu-id="b54f6-257">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="b54f6-258">上傳所選 hello 步驟 2 中的 hello Hadoop 叢集的資料 toohello 預設容器。</span><span class="sxs-lookup"><span data-stu-id="b54f6-258">Upload data toohello default container of hello Hadoop cluster selected in hello step 2.</span></span>
5. <span data-ttu-id="b54f6-259">載入 Azure HDInsight Hadoop 叢集中的資料 tooHive 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b54f6-259">Load data tooHive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="b54f6-260">a.</span><span class="sxs-lookup"><span data-stu-id="b54f6-260">a.</span></span>  <span data-ttu-id="b54f6-261">登入 toohello hello Hadoop 叢集前端節點</span><span class="sxs-lookup"><span data-stu-id="b54f6-261">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="b54f6-262">b.</span><span class="sxs-lookup"><span data-stu-id="b54f6-262">b.</span></span>  <span data-ttu-id="b54f6-263">開啟 hello Hadoop 命令列。</span><span class="sxs-lookup"><span data-stu-id="b54f6-263">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="b54f6-264">c.</span><span class="sxs-lookup"><span data-stu-id="b54f6-264">c.</span></span>  <span data-ttu-id="b54f6-265">命令所輸入 hello Hive 根目錄`cd %hive_home%\bin`Hadoop 命令列中。</span><span class="sxs-lookup"><span data-stu-id="b54f6-265">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="b54f6-266">d.</span><span class="sxs-lookup"><span data-stu-id="b54f6-266">d.</span></span>  <span data-ttu-id="b54f6-267">執行 hello Hive 查詢 toocreate 資料庫和資料表，並從 blob 儲存體 tooHive 資料表載入資料。</span><span class="sxs-lookup"><span data-stu-id="b54f6-267">Run hello Hive queries toocreate database and tables, and load data from blob storage tooHive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b54f6-268">如果大 hello 資料，使用者可以建立 hello Hive 資料表與資料分割。</span><span class="sxs-lookup"><span data-stu-id="b54f6-268">If hello data is big, users can create hello Hive table with partitions.</span></span> <span data-ttu-id="b54f6-269">然後，使用者可以使用`for`hello 前端節點 tooload 資料至 hello Hive 資料表的資料分割來分割 hello Hadoop 命令列中的迴圈。</span><span class="sxs-lookup"><span data-stu-id="b54f6-269">Then, users can use a `for` loop in hello Hadoop Command Line on hello head node tooload data into hello Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="b54f6-270">在 Hadoop 命令列中，視需要瀏覽資料並建立功能。</span><span class="sxs-lookup"><span data-stu-id="b54f6-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="b54f6-271">請注意，hello 功能不需要 toobe hello 資料庫資料表中具體化。</span><span class="sxs-lookup"><span data-stu-id="b54f6-271">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="b54f6-272">只有附註 hello 必要查詢 toocreate 它們。</span><span class="sxs-lookup"><span data-stu-id="b54f6-272">Only note hello necessary query toocreate them.</span></span>
   
   <span data-ttu-id="b54f6-273">a.</span><span class="sxs-lookup"><span data-stu-id="b54f6-273">a.</span></span>  <span data-ttu-id="b54f6-274">登入 toohello hello Hadoop 叢集前端節點</span><span class="sxs-lookup"><span data-stu-id="b54f6-274">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="b54f6-275">b.</span><span class="sxs-lookup"><span data-stu-id="b54f6-275">b.</span></span>  <span data-ttu-id="b54f6-276">開啟 hello Hadoop 命令列。</span><span class="sxs-lookup"><span data-stu-id="b54f6-276">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="b54f6-277">c.</span><span class="sxs-lookup"><span data-stu-id="b54f6-277">c.</span></span>  <span data-ttu-id="b54f6-278">命令所輸入 hello Hive 根目錄`cd %hive_home%\bin`Hadoop 命令列中。</span><span class="sxs-lookup"><span data-stu-id="b54f6-278">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="b54f6-279">d.</span><span class="sxs-lookup"><span data-stu-id="b54f6-279">d.</span></span>  <span data-ttu-id="b54f6-280">Hello hello Hadoop 叢集 tooexplore hello 資料的前端節點上執行 hello Hive 查詢 Hadoop 命令列中，建立所需的功能。</span><span class="sxs-lookup"><span data-stu-id="b54f6-280">Run hello Hive queries in Hadoop Command Line on hello head node of hello Hadoop cluster tooexplore hello data and create features as needed.</span></span>
7. <span data-ttu-id="b54f6-281">如果需要和/或所需，Azure Machine Learning Studio 中的 hello 資料 toofit 的範例。</span><span class="sxs-lookup"><span data-stu-id="b54f6-281">If needed and/or desired, sample hello data toofit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="b54f6-282">登入 toohello [Azure Machine Learning Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-282">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="b54f6-283">直接從 hello 讀取 hello 資料`Hive Queries`使用 hello[匯入資料][ import-data]模組。</span><span class="sxs-lookup"><span data-stu-id="b54f6-283">Read hello data directly from hello `Hive Queries` using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="b54f6-284">貼上 hello 必要查詢擷取的欄位，建立功能，以及範例資料，如有需要直接在 hello[匯入資料][ import-data]查詢。</span><span class="sxs-lookup"><span data-stu-id="b54f6-284">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="b54f6-285">從上傳的資料集開始的簡單 Azure Machine Learning 實驗流程。</span><span class="sxs-lookup"><span data-stu-id="b54f6-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="b54f6-286"><a name="decisiontree"></a>用於案例選擇的決策樹</span><span class="sxs-lookup"><span data-stu-id="b54f6-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="b54f6-287">hello 圖摘要說明上述的 hello 案例和 hello 進階分析程序和技術做選擇的 hello 分項案例 tooeach 引導您。</span><span class="sxs-lookup"><span data-stu-id="b54f6-287">hello following diagram summarizes hello scenarios described above and hello Advanced Analytics Process and Technology choices made that take you tooeach of hello itemized scenarios.</span></span> <span data-ttu-id="b54f6-288">請注意，可能需要資料處理、 瀏覽、 特徵設計和取樣置於一或多個方法/環境-hello 來源、 中繼、 和/或目標環境 – 並，仍然可以視需要重複。</span><span class="sxs-lookup"><span data-stu-id="b54f6-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at hello source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="b54f6-289">hello 圖表只會做為一些可能的流程的說明，並不提供詳盡的列舉型別。</span><span class="sxs-lookup"><span data-stu-id="b54f6-289">hello diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![範例 DS 程序逐步解說案例][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="b54f6-291">進階分析實務範例</span><span class="sxs-lookup"><span data-stu-id="b54f6-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="b54f6-292">如需端對端 Azure Machine Learning 逐步解說採用 hello 進階分析程序和技術使用公用資料集，請參閱：</span><span class="sxs-lookup"><span data-stu-id="b54f6-292">For end-to-end Azure Machine Learning walkthroughs that employ hello Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="b54f6-293">[Team Data Science Process 實務：使用 SQL Server](machine-learning-data-science-process-sql-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="b54f6-294">[Team Data Science Process 實務：使用 HDInsight Hadoop 叢集](machine-learning-data-science-process-hive-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="b54f6-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

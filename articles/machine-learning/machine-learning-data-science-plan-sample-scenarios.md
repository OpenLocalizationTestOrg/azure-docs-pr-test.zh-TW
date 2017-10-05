---
title: "識別 Azure Machine Learning 的進階分析案例 | Microsoft Docs"
description: "選取適合使用 Team Data Science Process 進行進階預測性分析的案例。"
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
ms.openlocfilehash: fe4f74f2e0602d13eedb6ca186480291a9a5724f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="9ca00-103">在 Azure 機器學習中的進階分析案例</span><span class="sxs-lookup"><span data-stu-id="9ca00-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="9ca00-104">本文概述可以運用 [Team Data Science Process (TDSP)](data-science-process-overview.md)來處理的各種範例資料來源和目標案例。</span><span class="sxs-lookup"><span data-stu-id="9ca00-104">This article outlines the variety of sample data sources and target scenarios that can be handled by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="9ca00-105">TDSP 提供系統化的方法，可讓小組共同建置智慧型應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ca00-105">The TDSP provides a systematic approach for teams to collaborate on building intelligent applications.</span></span> <span data-ttu-id="9ca00-106">此處呈現的案例將根據資料特性、來源位置和在 Azure 中的目標儲存機制，來說明資料處理工作流程中可用的選項。</span><span class="sxs-lookup"><span data-stu-id="9ca00-106">The scenarios presented here illustrate options available in the data processing workflow that depend on the data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="9ca00-107">最後一節提供 **決策樹** ，讓您在選取適合您資料和目標的範例案例時可以使用。</span><span class="sxs-lookup"><span data-stu-id="9ca00-107">The **decision tree** for selecting the sample scenarios that is appropriate for your data and objective is presented in the last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="9ca00-108">下列各節均提供一個範例案例。</span><span class="sxs-lookup"><span data-stu-id="9ca00-108">Each of the following sections presents a sample scenario.</span></span> <span data-ttu-id="9ca00-109">在每個案例中，都會列出可能的資料科學或進階分析流程，以及支援的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="9ca00-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="9ca00-110">**對於所有下列案例，您必須：**
> </span><span class="sxs-lookup"><span data-stu-id="9ca00-110">**For all of the following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="9ca00-111">[建立儲存體帳戶](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="9ca00-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="9ca00-112">建立 Azure Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="9ca00-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="9ca00-113"><a name="smalllocal"></a>案例 \#1：本機檔案中的中小型表格式資料集</span><span class="sxs-lookup"><span data-stu-id="9ca00-113"><a name="smalllocal"></a>Scenario \#1: Small to medium tabular dataset in a local files</span></span>
![中小型本機檔案][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="9ca00-115">其他 Azure 資源：無</span><span class="sxs-lookup"><span data-stu-id="9ca00-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="9ca00-116">登入 [Azure 機器學習 Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-116">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="9ca00-117">上傳資料集。</span><span class="sxs-lookup"><span data-stu-id="9ca00-117">Upload a dataset.</span></span>
3. <span data-ttu-id="9ca00-118">建置從上傳的資料集開始的 Azure 機器學習實驗流程。</span><span class="sxs-lookup"><span data-stu-id="9ca00-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="9ca00-119"><a name="smalllocalprocess"></a>案例 \#2：本機檔案中需要處理的中小型資料集</span><span class="sxs-lookup"><span data-stu-id="9ca00-119"><a name="smalllocalprocess"></a>Scenario \#2: Small to medium dataset of local files that require processing</span></span>
![需要處理的中小型本機檔案][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="9ca00-121">其他 Azure 資源：Azure 虛擬機器 (IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="9ca00-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="9ca00-122">建立執行 IPython Notebook 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9ca00-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="9ca00-123">將資料上傳至 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="9ca00-123">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="9ca00-124">前置處理和清除 IPython Notebook 中的資料 (從 Azure 儲存體容器存取資料)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="9ca00-125">將資料轉換為已清理的表格式格式。</span><span class="sxs-lookup"><span data-stu-id="9ca00-125">Transform data to cleaned, tabular form.</span></span>
5. <span data-ttu-id="9ca00-126">將轉換的資料儲存在 Azure Blob 中。</span><span class="sxs-lookup"><span data-stu-id="9ca00-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="9ca00-127">登入 [Azure 機器學習 Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-127">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="9ca00-128">使用[匯入資料][import-data]模組從 Azure Blob 讀取資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-128">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="9ca00-129">建置從內嵌的資料集開始的 Azure 機器學習實驗流程。</span><span class="sxs-lookup"><span data-stu-id="9ca00-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="9ca00-130"><a name="largelocal"></a>案例 \#3：本機檔案的大型資料集，以 Azure Blob 為目標</span><span class="sxs-lookup"><span data-stu-id="9ca00-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![大型本機檔案][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="9ca00-132">其他 Azure 資源：Azure 虛擬機器 (IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="9ca00-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="9ca00-133">建立執行 IPython Notebook 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9ca00-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="9ca00-134">將資料上傳至 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="9ca00-134">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="9ca00-135">前置處理和清除 IPython Notebook 中的資料 (從 Azure Blob 存取資料)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="9ca00-136">若有需要，請將資料轉換為已清理的表格式格式。</span><span class="sxs-lookup"><span data-stu-id="9ca00-136">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="9ca00-137">視需要瀏覽資料並建立功能。</span><span class="sxs-lookup"><span data-stu-id="9ca00-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="9ca00-138">擷取中小型資料範例。</span><span class="sxs-lookup"><span data-stu-id="9ca00-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="9ca00-139">將取樣資料儲存在 Azure Blob 中。</span><span class="sxs-lookup"><span data-stu-id="9ca00-139">Save the sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="9ca00-140">登入 [Azure 機器學習 Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-140">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="9ca00-141">使用[匯入資料][import-data]模組從 Azure Blob 讀取資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-141">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="9ca00-142">建置從內嵌的資料集開始的 Azure 機器學習實驗流程。</span><span class="sxs-lookup"><span data-stu-id="9ca00-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="9ca00-143"><a name="smalllocaltodb"></a>案例 \#4：本機檔案的中小型資料集，以 Azure 虛擬機器中的 SQL Server 為目標</span><span class="sxs-lookup"><span data-stu-id="9ca00-143"><a name="smalllocaltodb"></a>Scenario \#4: Small to medium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![中小型本機檔案至 Azure 中的 SQL DB][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="9ca00-145">其他 Azure 資源：Azure 虛擬機器 (SQL Server / IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="9ca00-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="9ca00-146">建立執行 SQL Server + IPython Notebook 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9ca00-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="9ca00-147">將資料上傳至 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="9ca00-147">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="9ca00-148">使用 IPython Notebook 前置處理和清除 Azure 儲存體容器中的資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="9ca00-149">若有需要，請將資料轉換為已清理的表格式格式。</span><span class="sxs-lookup"><span data-stu-id="9ca00-149">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="9ca00-150">將資料儲存至 VM-local 檔案 (IPython Notebook 會在 VM 上執行，本機磁碟是指 VM 磁碟機)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-150">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
6. <span data-ttu-id="9ca00-151">將資料載入執行於 Azure VM 的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9ca00-151">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="9ca00-152">選項 \#1：使用 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="9ca00-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="9ca00-153">登入 SQL Server VM</span><span class="sxs-lookup"><span data-stu-id="9ca00-153">Login to SQL Server VM</span></span>
   * <span data-ttu-id="9ca00-154">執行 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="9ca00-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="9ca00-155">建立資料庫和目標資料表。</span><span class="sxs-lookup"><span data-stu-id="9ca00-155">Create database and target tables.</span></span>
   * <span data-ttu-id="9ca00-156">使用其中一種大量匯入方法，從 VM 本機檔案載入資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-156">Use one of the bulk import methods to load the data from VM-local files.</span></span>
   
   <span data-ttu-id="9ca00-157">選項 \#2：使用 IPython Notebook – 不建議用於中型和大型資料集</span><span class="sxs-lookup"><span data-stu-id="9ca00-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="9ca00-158">使用 ODBC 連線字串，存取 VM 上的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="9ca00-158">Use ODBC connection string to access SQL Server on VM.</span></span>
   * <span data-ttu-id="9ca00-159">建立資料庫和目標資料表。</span><span class="sxs-lookup"><span data-stu-id="9ca00-159">Create database and target tables.</span></span>
   * <span data-ttu-id="9ca00-160">使用其中一種大量匯入方法，從 VM 本機檔案載入資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-160">Use one of the bulk import methods to load the data from VM-local files.</span></span>
7. <span data-ttu-id="9ca00-161">視需要瀏覽資料並建立功能。</span><span class="sxs-lookup"><span data-stu-id="9ca00-161">Explore data, create features as needed.</span></span> <span data-ttu-id="9ca00-162">請注意，功能在資料庫資料表中無需具體化。</span><span class="sxs-lookup"><span data-stu-id="9ca00-162">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="9ca00-163">僅注意建立這些功能的必要查詢。</span><span class="sxs-lookup"><span data-stu-id="9ca00-163">Only note the necessary query to create them.</span></span>
8. <span data-ttu-id="9ca00-164">若有需要，請決定資料範例大小。</span><span class="sxs-lookup"><span data-stu-id="9ca00-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="9ca00-165">登入 [Azure 機器學習 Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-165">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="9ca00-166">使用[匯入資料][import-data]模組直接從 SQL Server 讀取資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-166">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="9ca00-167">視需要，將可擷取欄位、建立功能及對資料取樣的必要查詢，直接貼到[匯入資料][import-data]查詢中。</span><span class="sxs-lookup"><span data-stu-id="9ca00-167">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="9ca00-168">建置從內嵌的資料集開始的 Azure 機器學習實驗流程。</span><span class="sxs-lookup"><span data-stu-id="9ca00-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="9ca00-169"><a name="largelocaltodb"></a>案例 \#5：本機資料中的大型資料集，目標 Azure VM 中的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="9ca00-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![大型本機檔案至 Azure 中的 SQL DB][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="9ca00-171">其他 Azure 資源：Azure 虛擬機器 (SQL Server / IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="9ca00-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="9ca00-172">建立執行 SQL Server 和 IPython Notebook 伺服器的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9ca00-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="9ca00-173">將資料上傳至 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="9ca00-173">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="9ca00-174">(選擇性) 前置處理和清除資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="9ca00-175">a.</span><span class="sxs-lookup"><span data-stu-id="9ca00-175">a.</span></span>  <span data-ttu-id="9ca00-176">前置處理和清除 IPython Notebook 中的資料，從 Azure 存取資料</span><span class="sxs-lookup"><span data-stu-id="9ca00-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="9ca00-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ca00-177">b.</span></span>  <span data-ttu-id="9ca00-178">若有需要，請將資料轉換為已清理的表格式格式。</span><span class="sxs-lookup"><span data-stu-id="9ca00-178">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="9ca00-179">c.</span><span class="sxs-lookup"><span data-stu-id="9ca00-179">c.</span></span>  <span data-ttu-id="9ca00-180">將資料儲存至 VM-local 檔案 (IPython Notebook 會在 VM 上執行，本機磁碟是指 VM 磁碟機)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-180">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="9ca00-181">將資料載入執行於 Azure VM 的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9ca00-181">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="9ca00-182">a.</span><span class="sxs-lookup"><span data-stu-id="9ca00-182">a.</span></span>  <span data-ttu-id="9ca00-183">登入 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="9ca00-183">Login to SQL Server VM.</span></span>
   
   <span data-ttu-id="9ca00-184">b.</span><span class="sxs-lookup"><span data-stu-id="9ca00-184">b.</span></span>  <span data-ttu-id="9ca00-185">如果資料尚未儲存，請從 Azure 下載資料檔案</span><span class="sxs-lookup"><span data-stu-id="9ca00-185">If data not saved already, download data files from Azure</span></span>
   
       storage container to local-VM folder.
   
   <span data-ttu-id="9ca00-186">c.</span><span class="sxs-lookup"><span data-stu-id="9ca00-186">c.</span></span>  <span data-ttu-id="9ca00-187">執行 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="9ca00-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="9ca00-188">d.</span><span class="sxs-lookup"><span data-stu-id="9ca00-188">d.</span></span>  <span data-ttu-id="9ca00-189">建立資料庫和目標資料表。</span><span class="sxs-lookup"><span data-stu-id="9ca00-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="9ca00-190">e.</span><span class="sxs-lookup"><span data-stu-id="9ca00-190">e.</span></span>  <span data-ttu-id="9ca00-191">使用其中一個大量匯入方法來載入資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-191">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="9ca00-192">f.</span><span class="sxs-lookup"><span data-stu-id="9ca00-192">f.</span></span>  <span data-ttu-id="9ca00-193">如果需要資料表聯結，請建立索引以加速聯結。</span><span class="sxs-lookup"><span data-stu-id="9ca00-193">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9ca00-194">如需加快大型資料的載入速度，建議您建立分割資料表並大量平行匯入資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import the data in parallel.</span></span> <span data-ttu-id="9ca00-195">如需詳細資訊，請參閱 [平行資料匯入至 SQL 分割資料表](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-195">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="9ca00-196">視需要瀏覽資料並建立功能。</span><span class="sxs-lookup"><span data-stu-id="9ca00-196">Explore data, create features as needed.</span></span> <span data-ttu-id="9ca00-197">請注意，功能在資料庫資料表中無需具體化。</span><span class="sxs-lookup"><span data-stu-id="9ca00-197">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="9ca00-198">僅注意建立這些功能的必要查詢。</span><span class="sxs-lookup"><span data-stu-id="9ca00-198">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="9ca00-199">若有需要，請決定資料範例大小。</span><span class="sxs-lookup"><span data-stu-id="9ca00-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="9ca00-200">登入 [Azure 機器學習 Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-200">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="9ca00-201">使用[匯入資料][import-data]模組直接從 SQL Server 讀取資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-201">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="9ca00-202">視需要，將可擷取欄位、建立功能及對資料取樣的必要查詢，直接貼到[匯入資料][import-data]查詢中。</span><span class="sxs-lookup"><span data-stu-id="9ca00-202">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="9ca00-203">從上傳的資料集開始的簡單 Azure Machine Learning 實驗流程</span><span class="sxs-lookup"><span data-stu-id="9ca00-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="9ca00-204"><a name="largedbtodb"></a>案例 \#6：SQL Server 資料庫內部部署中的大型資料集，以 Azure 虛擬機器中的 SQL Server 為目標</span><span class="sxs-lookup"><span data-stu-id="9ca00-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![大型 SQL DB 內部部署至 Azure 中的 SQL DB][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="9ca00-206">其他 Azure 資源：Azure 虛擬機器 (SQL Server / IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="9ca00-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="9ca00-207">建立執行 SQL Server 和 IPython Notebook 伺服器的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9ca00-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="9ca00-208">使用其中一個資料匯出方法來將資料從 SQL Server 匯出成傾印檔案。</span><span class="sxs-lookup"><span data-stu-id="9ca00-208">Use one of the data export methods to export the data from SQL Server to dump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9ca00-209">如果您決定從內部部署資料庫移動所有資料，一個替代 (較快速) 方法是將整個資料庫移到 Azure 中的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="9ca00-209">If you decide to move all data from the on-prem database, an alternate (faster) method to move the full database to the SQL Server instance in Azure.</span></span> <span data-ttu-id="9ca00-210">略過匯出資料、建立資料庫，和將資料載入/匯入目標資料庫等步驟，並依照替代方法進行。</span><span class="sxs-lookup"><span data-stu-id="9ca00-210">Skip the steps to export data, create database, and load/import data to the target database and follow the alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="9ca00-211">將傾印檔案上傳至 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="9ca00-211">Upload dump files to Azure storage container.</span></span>
4. <span data-ttu-id="9ca00-212">將資料載入執行於 Azure 虛擬機器的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9ca00-212">Load the data to a SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="9ca00-213">a.</span><span class="sxs-lookup"><span data-stu-id="9ca00-213">a.</span></span>  <span data-ttu-id="9ca00-214">登入 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="9ca00-214">Login to the SQL Server VM.</span></span>
   
   <span data-ttu-id="9ca00-215">b.</span><span class="sxs-lookup"><span data-stu-id="9ca00-215">b.</span></span>  <span data-ttu-id="9ca00-216">將資料檔案從 Azure 儲存體容器下載到 local-VM 資料夾。</span><span class="sxs-lookup"><span data-stu-id="9ca00-216">Download data files from an Azure storage container to the local-VM folder.</span></span>
   
   <span data-ttu-id="9ca00-217">c.</span><span class="sxs-lookup"><span data-stu-id="9ca00-217">c.</span></span>  <span data-ttu-id="9ca00-218">執行 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="9ca00-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="9ca00-219">d.</span><span class="sxs-lookup"><span data-stu-id="9ca00-219">d.</span></span>  <span data-ttu-id="9ca00-220">建立資料庫和目標資料表。</span><span class="sxs-lookup"><span data-stu-id="9ca00-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="9ca00-221">e.</span><span class="sxs-lookup"><span data-stu-id="9ca00-221">e.</span></span>  <span data-ttu-id="9ca00-222">使用其中一個大量匯入方法來載入資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-222">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="9ca00-223">f.</span><span class="sxs-lookup"><span data-stu-id="9ca00-223">f.</span></span>  <span data-ttu-id="9ca00-224">如果需要資料表聯結，請建立索引以加速聯結。</span><span class="sxs-lookup"><span data-stu-id="9ca00-224">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9ca00-225">如需加快大型資料的載入速度，請建立分割資料表並大量平行匯入資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-225">For faster loading of large data sizes, create partitioned tables and to bulk import the data in parallel.</span></span> <span data-ttu-id="9ca00-226">如需詳細資訊，請參閱 [平行資料匯入至 SQL 分割資料表](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-226">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="9ca00-227">視需要瀏覽資料並建立功能。</span><span class="sxs-lookup"><span data-stu-id="9ca00-227">Explore data, create features as needed.</span></span> <span data-ttu-id="9ca00-228">請注意，功能在資料庫資料表中無需具體化。</span><span class="sxs-lookup"><span data-stu-id="9ca00-228">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="9ca00-229">僅注意建立這些功能的必要查詢。</span><span class="sxs-lookup"><span data-stu-id="9ca00-229">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="9ca00-230">若有需要，請決定資料範例大小。</span><span class="sxs-lookup"><span data-stu-id="9ca00-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="9ca00-231">登入 [Azure 機器學習 Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-231">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="9ca00-232">使用[匯入資料][import-data]模組直接從 SQL Server 讀取資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-232">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="9ca00-233">視需要，將可擷取欄位、建立功能及對資料取樣的必要查詢，直接貼到[匯入資料][import-data]查詢中。</span><span class="sxs-lookup"><span data-stu-id="9ca00-233">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="9ca00-234">從上傳的資料集開始的簡單 Azure Machine Learning 實驗流程。</span><span class="sxs-lookup"><span data-stu-id="9ca00-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-to-copy-a-full-database-from-an-on-premises--sql-server-to-azure-sql-database"></a><span data-ttu-id="9ca00-235">將整個資料庫從內部部署 SQL Server 複製到 Azure SQL Database 的替代方法</span><span class="sxs-lookup"><span data-stu-id="9ca00-235">Alternate method to copy a full database from an on-premises  SQL Server to Azure SQL Database</span></span>
![卸離本機 DB 和連結至 Azure 中的 SQL DB][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="9ca00-237">其他 Azure 資源：Azure 虛擬機器 (SQL Server / IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="9ca00-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="9ca00-238">若要在您的 SQL Server VM 中複寫整個 SQL Server 資料庫，您應將資料庫從一個位置/伺服器複製到另一個位置/伺服器 (假設資料庫可以暫時設定離線)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-238">To replicate the entire SQL Server database in your SQL Server VM, you should copy a database from one location/server to another, assuming that the database can be taken temporarily offline.</span></span> <span data-ttu-id="9ca00-239">您可以在 SQL Server Management Studio Object Explorer 中，或使用對等的 Transact-SQL 命令來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="9ca00-239">You do this in the SQL Server Management Studio Object Explorer, or using the equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="9ca00-240">在來源位置卸離資料庫。</span><span class="sxs-lookup"><span data-stu-id="9ca00-240">Detach the database at the source location.</span></span> <span data-ttu-id="9ca00-241">如需詳細資訊，請參閱[卸離資料庫](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="9ca00-242">在 Windows 檔案總管或 Windows 命令提示字元視窗中，將已卸離的資料庫檔案和記錄檔複製到位於 Azure 中 SQL Server VM 上的目標位置。</span><span class="sxs-lookup"><span data-stu-id="9ca00-242">In Windows Explorer or Windows Command Prompt window, copy the detached database file or files and log file or files to the target location on the SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="9ca00-243">將複製檔案連結至目標 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="9ca00-243">Attach the copied files to the target SQL Server instance.</span></span> <span data-ttu-id="9ca00-244">如需詳細資訊，請參閱[連結資料庫](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="9ca00-245">[使用卸離和連結來移動資料庫 (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="9ca00-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="9ca00-246"><a name="largedbtohive"></a>案例 \#7：本機檔案中的巨量資料，目標 Azure HDInsight Hadoop 叢集中的 Hive 資料庫</span><span class="sxs-lookup"><span data-stu-id="9ca00-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![本機目標 Hive 中的巨量資料][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="9ca00-248">其他 Azure 資源：Azure HDInsight Hadoop 叢集和 Azure 虛擬機器 (IPython Notebook 伺服器)</span><span class="sxs-lookup"><span data-stu-id="9ca00-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="9ca00-249">建立執行 IPython Notebook 伺服器的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9ca00-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="9ca00-250">建立 Azure HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="9ca00-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="9ca00-251">(選擇性) 前置處理和清除資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="9ca00-252">a.</span><span class="sxs-lookup"><span data-stu-id="9ca00-252">a.</span></span>  <span data-ttu-id="9ca00-253">前置處理和清除 IPython Notebook 中的資料，從 Azure 存取資料</span><span class="sxs-lookup"><span data-stu-id="9ca00-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="9ca00-254">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ca00-254">b.</span></span>  <span data-ttu-id="9ca00-255">若有需要，請將資料轉換為已清理的表格式格式。</span><span class="sxs-lookup"><span data-stu-id="9ca00-255">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="9ca00-256">c.</span><span class="sxs-lookup"><span data-stu-id="9ca00-256">c.</span></span>  <span data-ttu-id="9ca00-257">將資料儲存至 VM-local 檔案 (IPython Notebook 會在 VM 上執行，本機磁碟是指 VM 磁碟機)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-257">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="9ca00-258">將資料上傳至步驟 2 中已選取 Hadoop 叢集的預設容器。</span><span class="sxs-lookup"><span data-stu-id="9ca00-258">Upload data to the default container of the Hadoop cluster selected in the step 2.</span></span>
5. <span data-ttu-id="9ca00-259">將資料載入 Azure HDInsight Hadoop 叢集中的 Hive 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9ca00-259">Load data to Hive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="9ca00-260">a.</span><span class="sxs-lookup"><span data-stu-id="9ca00-260">a.</span></span>  <span data-ttu-id="9ca00-261">登入 Hadoop 叢集的前端節點</span><span class="sxs-lookup"><span data-stu-id="9ca00-261">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="9ca00-262">b.</span><span class="sxs-lookup"><span data-stu-id="9ca00-262">b.</span></span>  <span data-ttu-id="9ca00-263">開啟 Hadoop 命令列。</span><span class="sxs-lookup"><span data-stu-id="9ca00-263">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="9ca00-264">c.</span><span class="sxs-lookup"><span data-stu-id="9ca00-264">c.</span></span>  <span data-ttu-id="9ca00-265">透過 Hadoop 命令列中的 `cd %hive_home%\bin` 命令進入 Hive 根目錄。</span><span class="sxs-lookup"><span data-stu-id="9ca00-265">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="9ca00-266">d.</span><span class="sxs-lookup"><span data-stu-id="9ca00-266">d.</span></span>  <span data-ttu-id="9ca00-267">執行 Hive 查詢以建立資料庫和資料表，並將資料從 Blob 儲存體載入 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="9ca00-267">Run the Hive queries to create database and tables, and load data from blob storage to Hive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9ca00-268">如果資料太大，使用者可以建立包含分割區的 Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="9ca00-268">If the data is big, users can create the Hive table with partitions.</span></span> <span data-ttu-id="9ca00-269">接著，使用者可以在前端節點上的 Hadoop 命令列中使用 `for` 迴圈，以將資料載入使用資料分割的 Hive 分割資料表。</span><span class="sxs-lookup"><span data-stu-id="9ca00-269">Then, users can use a `for` loop in the Hadoop Command Line on the head node to load data into the Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="9ca00-270">在 Hadoop 命令列中，視需要瀏覽資料並建立功能。</span><span class="sxs-lookup"><span data-stu-id="9ca00-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="9ca00-271">請注意，功能在資料庫資料表中無需具體化。</span><span class="sxs-lookup"><span data-stu-id="9ca00-271">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="9ca00-272">僅注意建立這些功能的必要查詢。</span><span class="sxs-lookup"><span data-stu-id="9ca00-272">Only note the necessary query to create them.</span></span>
   
   <span data-ttu-id="9ca00-273">a.</span><span class="sxs-lookup"><span data-stu-id="9ca00-273">a.</span></span>  <span data-ttu-id="9ca00-274">登入 Hadoop 叢集的前端節點</span><span class="sxs-lookup"><span data-stu-id="9ca00-274">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="9ca00-275">b.</span><span class="sxs-lookup"><span data-stu-id="9ca00-275">b.</span></span>  <span data-ttu-id="9ca00-276">開啟 Hadoop 命令列。</span><span class="sxs-lookup"><span data-stu-id="9ca00-276">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="9ca00-277">c.</span><span class="sxs-lookup"><span data-stu-id="9ca00-277">c.</span></span>  <span data-ttu-id="9ca00-278">透過 Hadoop 命令列中的 `cd %hive_home%\bin` 命令進入 Hive 根目錄。</span><span class="sxs-lookup"><span data-stu-id="9ca00-278">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="9ca00-279">d.</span><span class="sxs-lookup"><span data-stu-id="9ca00-279">d.</span></span>  <span data-ttu-id="9ca00-280">在 Hadoop 叢集前端節點的 Hadoop 命令列中執行 Hive 查詢，以瀏覽資料並視需要建立功能。</span><span class="sxs-lookup"><span data-stu-id="9ca00-280">Run the Hive queries in Hadoop Command Line on the head node of the Hadoop cluster to explore the data and create features as needed.</span></span>
7. <span data-ttu-id="9ca00-281">若有需要，取樣資料以符合 Azure Machine Learning Studio 需求。</span><span class="sxs-lookup"><span data-stu-id="9ca00-281">If needed and/or desired, sample the data to fit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="9ca00-282">登入 [Azure 機器學習 Studio](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-282">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="9ca00-283">使用[匯入資料][import-data]模組直接從 `Hive Queries` 讀取資料。</span><span class="sxs-lookup"><span data-stu-id="9ca00-283">Read the data directly from the `Hive Queries` using the [Import Data][import-data] module.</span></span> <span data-ttu-id="9ca00-284">視需要，將可擷取欄位、建立功能及對資料取樣的必要查詢，直接貼到[匯入資料][import-data]查詢中。</span><span class="sxs-lookup"><span data-stu-id="9ca00-284">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="9ca00-285">從上傳的資料集開始的簡單 Azure Machine Learning 實驗流程。</span><span class="sxs-lookup"><span data-stu-id="9ca00-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="9ca00-286"><a name="decisiontree"></a>用於案例選擇的決策樹</span><span class="sxs-lookup"><span data-stu-id="9ca00-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="9ca00-287">下圖摘要說明上述案例，以及讓您連結到每個分項案例的「進階分析程序和技術」選擇。</span><span class="sxs-lookup"><span data-stu-id="9ca00-287">The following diagram summarizes the scenarios described above and the Advanced Analytics Process and Technology choices made that take you to each of the itemized scenarios.</span></span> <span data-ttu-id="9ca00-288">請注意，資料處理、資料探索、功能工程和取樣可能會出現在一或多個方法/環境中 (在來源、中繼和/或目標環境中)，且可以視需要反覆處理。</span><span class="sxs-lookup"><span data-stu-id="9ca00-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at the source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="9ca00-289">圖表的目的只是說明一些可能的流程，並不提供詳盡的列舉。</span><span class="sxs-lookup"><span data-stu-id="9ca00-289">The diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![範例 DS 程序逐步解說案例][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="9ca00-291">進階分析實務範例</span><span class="sxs-lookup"><span data-stu-id="9ca00-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="9ca00-292">如需透過公用資料集運用進階分析程序和技術的端對端 Azure Machine Learning 逐步解說，請參閱：</span><span class="sxs-lookup"><span data-stu-id="9ca00-292">For end-to-end Azure Machine Learning walkthroughs that employ the Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="9ca00-293">[Team Data Science Process 實務：使用 SQL Server](machine-learning-data-science-process-sql-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="9ca00-294">[Team Data Science Process 實務：使用 HDInsight Hadoop 叢集](machine-learning-data-science-process-hive-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="9ca00-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

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

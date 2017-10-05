---
title: "Azure Data Factory 支援的計算環境 | Microsoft Docs"
description: "了解您可以在 Azure Data Factory 管線中 (如 Azure HDInsight) 用來轉換/處理資料的計算環境。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6877a7e8-1a58-4cfb-bbd3-252ac72e4145
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/25/2017
ms.author: shlo
ms.openlocfilehash: da7110614e684656da3ef9830780606e1576684d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a><span data-ttu-id="64e0e-103">Azure Data Factory 支援的計算環境</span><span class="sxs-lookup"><span data-stu-id="64e0e-103">Compute environments supported by Azure Data Factory</span></span>
<span data-ttu-id="64e0e-104">本文說明您可用來處理或轉換資料的各種計算環境。</span><span class="sxs-lookup"><span data-stu-id="64e0e-104">This article explains different compute environments that you can use to process or transform data.</span></span> <span data-ttu-id="64e0e-105">其中還提供在設定將這些計算環境連結至 Azure Data Factory 的連結服務時，Data Factory 所支援的不同組態 (隨選與自備) 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="64e0e-105">It also provides details about different configurations (on-demand vs. bring your own) supported by Data Factory when configuring linked services linking these compute environments to an Azure data factory.</span></span>

<span data-ttu-id="64e0e-106">下表列出 Data Factory 支援的計算環境以及可在環境上執行的活動。</span><span class="sxs-lookup"><span data-stu-id="64e0e-106">The following table provides a list of compute environments supported by Data Factory and the activities that can run on them.</span></span> 

| <span data-ttu-id="64e0e-107">計算環境</span><span class="sxs-lookup"><span data-stu-id="64e0e-107">Compute environment</span></span> | <span data-ttu-id="64e0e-108">活動</span><span class="sxs-lookup"><span data-stu-id="64e0e-108">activities</span></span> |
| --- | --- |
| <span data-ttu-id="64e0e-109">[隨選 HDInsight 叢集](#azure-hdinsight-on-demand-linked-service)或[您自己的 HDInsight 叢集](#azure-hdinsight-linked-service)</span><span class="sxs-lookup"><span data-stu-id="64e0e-109">[On-demand HDInsight cluster](#azure-hdinsight-on-demand-linked-service) or [your own HDInsight cluster](#azure-hdinsight-linked-service)</span></span> |<span data-ttu-id="64e0e-110">[DotNet](data-factory-use-custom-activities.md)、[Hive](data-factory-hive-activity.md)、[Pig](data-factory-pig-activity.md)、[MapReduce](data-factory-map-reduce.md)、[Hadoop 串流](data-factory-hadoop-streaming-activity.md)</span><span class="sxs-lookup"><span data-stu-id="64e0e-110">[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop Streaming](data-factory-hadoop-streaming-activity.md)</span></span> |
| [<span data-ttu-id="64e0e-111">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="64e0e-111">Azure Batch</span></span>](#azure-batch-linked-service) |[<span data-ttu-id="64e0e-112">DotNet</span><span class="sxs-lookup"><span data-stu-id="64e0e-112">DotNet</span></span>](data-factory-use-custom-activities.md) |
| [<span data-ttu-id="64e0e-113">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="64e0e-113">Azure Machine Learning</span></span>](#azure-machine-learning-linked-service) |[<span data-ttu-id="64e0e-114">Machine Learning 活動︰批次執行和更新資源</span><span class="sxs-lookup"><span data-stu-id="64e0e-114">Machine Learning activities: Batch Execution and Update Resource</span></span>](data-factory-azure-ml-batch-execution-activity.md) |
| [<span data-ttu-id="64e0e-115">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="64e0e-115">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics-linked-service) |[<span data-ttu-id="64e0e-116">Data Lake Analytics U-SQL</span><span class="sxs-lookup"><span data-stu-id="64e0e-116">Data Lake Analytics U-SQL</span></span>](data-factory-usql-activity.md) |
| <span data-ttu-id="64e0e-117">[Azure SQL](#azure-sql-linked-service)、[Azure SQL 資料倉儲](#azure-sql-data-warehouse-linked-service)、[SQL Server](#sql-server-linked-service)</span><span class="sxs-lookup"><span data-stu-id="64e0e-117">[Azure SQL](#azure-sql-linked-service), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service)</span></span> |[<span data-ttu-id="64e0e-118">預存程序</span><span class="sxs-lookup"><span data-stu-id="64e0e-118">Stored Procedure</span></span>](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a><span data-ttu-id="64e0e-119">Azure Data Factory 中支援的 HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="64e0e-119">Supported HDInsight versions in Azure Data Factory</span></span>
<span data-ttu-id="64e0e-120">Azure HDInsight 支援多個可隨時部署的 Hadoop 叢集版本。</span><span class="sxs-lookup"><span data-stu-id="64e0e-120">Azure HDInsight supports multiple Hadoop cluster versions that can be deployed at any time.</span></span> <span data-ttu-id="64e0e-121">每一個版本選擇都會建立特定版本的 Hortonworks Data Platform (HDP) 散發，以及該散發內包含的一組元件。</span><span class="sxs-lookup"><span data-stu-id="64e0e-121">Each version choice creates a specific version of the Hortonworks Data Platform (HDP) distribution and a set of components that are contained within that distribution.</span></span> <span data-ttu-id="64e0e-122">Microsoft 會持續更新所支援 HDInsight 版本的清單，以提供最新的 Hadoop 生態系統元件和修正程式。</span><span class="sxs-lookup"><span data-stu-id="64e0e-122">Microsoft keeps updating the list of supported versions of HDInsight to provide latest Hadoop ecosystem components and fixes.</span></span> <span data-ttu-id="64e0e-123">HDInsight 3.2 在 2017 年 4 月 1 日已被取代。</span><span class="sxs-lookup"><span data-stu-id="64e0e-123">The HDInsight 3.2 is deprecated on April 1, 2017.</span></span> <span data-ttu-id="64e0e-124">如需詳細資訊，請參閱[支援的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-124">For detailed information, see [supported HDInsight versions](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>

<span data-ttu-id="64e0e-125">這會影響具有對 HDInsight 3.2 叢集執行活動的現有 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="64e0e-125">This impacts existing Azure Data Factories that have Activities running against HDInsight 3.2 clusters.</span></span> <span data-ttu-id="64e0e-126">我們建議使用者遵循下一節的指導方針來更新受影響的 Data Factory：</span><span class="sxs-lookup"><span data-stu-id="64e0e-126">We recommend users to follow the guidelines in the following section to update the impacted Data Factories:</span></span>

### <a name="for-linked-services-pointing-to-your-own-hdinsight-clusters"></a><span data-ttu-id="64e0e-127">針對指向您自己的 HDInsight 叢集的連結服務</span><span class="sxs-lookup"><span data-stu-id="64e0e-127">For Linked Services pointing to your own HDInsight clusters</span></span>
* <span data-ttu-id="64e0e-128">**指向您自己的 HDInsight 3.2 或舊版叢集的 HDInsight 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="64e0e-128">**HDInsight Linked Services pointing to your own HDInsight 3.2 or below clusters:**</span></span>

  <span data-ttu-id="64e0e-129">Azure Data Factory 支援將作業提交至您自己的 HDInsight 叢集，從 HDI 3.1 至[最新支援的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-129">Azure Data Factory supports submitting jobs to your own HDInsight clusters from HDI 3.1 to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span> <span data-ttu-id="64e0e-130">不過，根據[支援的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)中記載的取代原則，在 2017 年 4 月 1 日之後，您無法再建立 HDInsight 3.2 叢集。</span><span class="sxs-lookup"><span data-stu-id="64e0e-130">However, you can no longer create HDInsight 3.2 cluster after April 1, 2017 based on the deprecation policy documented in [supported HDInsight versions](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>  

  <span data-ttu-id="64e0e-131">**建議：**</span><span class="sxs-lookup"><span data-stu-id="64e0e-131">**Recommendations:**</span></span> 
  * <span data-ttu-id="64e0e-132">利用[可以搭配不同 HDInsight 版本使用的 Hadoop 元件](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions)和[與 HDInsight 版本相關聯的 Hortonworks 版本資訊](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)中記載的資訊，執行測試以確保參考此連結服務之活動的相容性為[最新支援的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-132">Perform tests to ensure the compatibility of the Activities that reference this Linked Services to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) with information documented in [Hadoop components available with different HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) and [Hortonworks release notes associated with HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).</span></span>
  * <span data-ttu-id="64e0e-133">將您的 HDInsight 3.2 叢集升級為[最新支援的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)，以取得最新的 Hadoop 生態系統元件和修正程式。</span><span class="sxs-lookup"><span data-stu-id="64e0e-133">Upgrade your HDInsight 3.2 cluster to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) to get the latest Hadoop ecosystem components and fixes.</span></span> 

* <span data-ttu-id="64e0e-134">**指向您自己的 HDInsight 3.3 或以上叢集的 HDInsight 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="64e0e-134">**HDInsight Linked Services pointing to your own HDInsight 3.3 or above clusters:**</span></span>

  <span data-ttu-id="64e0e-135">Azure Data Factory 支援將作業提交至您自己的 HDInsight 叢集，從 HDI 3.1 至[最新支援的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-135">Azure Data Factory supports submitting jobs to your own HDInsight clusters from HDI 3.1 to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span> 
  
  <span data-ttu-id="64e0e-136">**建議：**</span><span class="sxs-lookup"><span data-stu-id="64e0e-136">**Recommendations:**</span></span> 
  * <span data-ttu-id="64e0e-137">從 Data Factory 的觀點來看，不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="64e0e-137">No action is required from Data Factory perspective.</span></span> <span data-ttu-id="64e0e-138">不過，如果您是在較低版本的 HDInsight，仍建議您升級至[最新支援的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)，以取得最新的 Hadoop 生態系統元件和修正程式。</span><span class="sxs-lookup"><span data-stu-id="64e0e-138">However, if you are on a lower version of HDInsight, we still recommend upgrading to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) to get the latest Hadoop ecosystem components and fixes.</span></span>

### <a name="for-hdinsight-on-demand-linked-services"></a><span data-ttu-id="64e0e-139">針對 HDInsight 隨選連結服務</span><span class="sxs-lookup"><span data-stu-id="64e0e-139">For HDInsight On-Demand Linked Services</span></span>
* <span data-ttu-id="64e0e-140">**3.2 版或以下版本是在 HDInsight 隨選連結服務 JSON 定義中指定：**</span><span class="sxs-lookup"><span data-stu-id="64e0e-140">**Version 3.2 or below is specified in HDInsight On-Demand Linked Services JSON definition:**</span></span>
  
  <span data-ttu-id="64e0e-141">自 **2017/05/15** 起，Azure Data Factory 支援建立隨選 HDInsight 叢集 3.3 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="64e0e-141">Azure Data Factory will support creation of On-Demand HDInsight clusters of version 3.3 or more from **05/15/2017** onwards.</span></span> <span data-ttu-id="64e0e-142">對現有隨選 HDInsight 3.2 連結服務的支援期限已延長至 **2017/07/15**。</span><span class="sxs-lookup"><span data-stu-id="64e0e-142">And, the end of support for existing on-demand HDInsight 3.2 linked services is extended to **07/15/2017**.</span></span>  

  <span data-ttu-id="64e0e-143">**建議：**</span><span class="sxs-lookup"><span data-stu-id="64e0e-143">**Recommendations:**</span></span> 
  * <span data-ttu-id="64e0e-144">利用[可以搭配不同 HDInsight 版本使用的 Hadoop 元件](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions)和[與 HDInsight 版本相關聯的 Hortonworks 版本資訊](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)中記載的資訊，執行測試以確保參考此連結服務之活動的相容性為[最新支援的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-144">Perform tests to ensure the compatibility of the Activities that reference this Linked Services to  [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) with information documented in [Hadoop components available with different HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) and [Hortonworks release notes associated with HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).</span></span>
  * <span data-ttu-id="64e0e-145">在 **2017/07/15** 之前，請將隨選 HDI 連結服務 JSON 定義中的 Version 屬性更新為[最新支援的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)，以取得最新的 Hadoop 生態系統元件和修正程式。</span><span class="sxs-lookup"><span data-stu-id="64e0e-145">Before **07/15/2017**, update the Version property in On-Demand HDI Linked Service JSON definition to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) to get the latest Hadoop ecosystem components and fixes.</span></span> <span data-ttu-id="64e0e-146">如需詳細的 JSON 定義，請參閱 [Azure HDInsight 隨選連結服務範例](#azure-hdinsight-on-demand-linked-service)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-146">For detailed JSON definition, refer to the [Azure HDInsight On-Demand Linked Service sample](#azure-hdinsight-on-demand-linked-service).</span></span> 

* <span data-ttu-id="64e0e-147">**隨選 HDInsight 連結服務中未指定的版本：**</span><span class="sxs-lookup"><span data-stu-id="64e0e-147">**Version not specified in On-Demand HDInsight Linked Services:**</span></span>
  
  <span data-ttu-id="64e0e-148">自 **2017/05/15** 起，Azure Data Factory 支援建立隨選 HDInsight 叢集 3.3 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="64e0e-148">Azure Data Factory will support creation of on-demand HDInsight clusters of version 3.3 or more from **05/15/2017** onwards.</span></span> <span data-ttu-id="64e0e-149">對現有隨選 HDInsight 3.2 連結服務的支援期限已延長至 **2017/07/15**。</span><span class="sxs-lookup"><span data-stu-id="64e0e-149">And, the end of support to existing on-demand HDInsight 3.2 linked services is extended to **07/15/2017**.</span></span> 

  <span data-ttu-id="64e0e-150">在 **2017/07/15** 之前，如果 version 和 osType 屬性保留空白，則預設值為：</span><span class="sxs-lookup"><span data-stu-id="64e0e-150">Before **07/15/2017**, if left blank, the default values for version and osType properties are:</span></span> 

  | <span data-ttu-id="64e0e-151">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-151">Property</span></span> | <span data-ttu-id="64e0e-152">預設值</span><span class="sxs-lookup"><span data-stu-id="64e0e-152">Default Value</span></span> | <span data-ttu-id="64e0e-153">必要</span><span class="sxs-lookup"><span data-stu-id="64e0e-153">Required</span></span> |
  | --- | --- | --- |
  <span data-ttu-id="64e0e-154">版本</span><span class="sxs-lookup"><span data-stu-id="64e0e-154">Version</span></span>   | <span data-ttu-id="64e0e-155">Windows 叢集為 HDI 3.1，Linux 叢集為 HDI 3.2。</span><span class="sxs-lookup"><span data-stu-id="64e0e-155">HDI 3.1 for Windows cluster and HDI 3.2 for Linux cluster.</span></span>| <span data-ttu-id="64e0e-156">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-156">No</span></span>
  <span data-ttu-id="64e0e-157">osType</span><span class="sxs-lookup"><span data-stu-id="64e0e-157">osType</span></span> | <span data-ttu-id="64e0e-158">預設值為 Windows</span><span class="sxs-lookup"><span data-stu-id="64e0e-158">The default is Windows</span></span> | <span data-ttu-id="64e0e-159">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-159">No</span></span>

  <span data-ttu-id="64e0e-160">在 **2017/07/15** 之後，如果 version 和 osType 屬性保留空白，則預設值為：</span><span class="sxs-lookup"><span data-stu-id="64e0e-160">After **07/15/2017**, if left blank, the default values for version and osType properties are:</span></span>

  | <span data-ttu-id="64e0e-161">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-161">Property</span></span> | <span data-ttu-id="64e0e-162">預設值</span><span class="sxs-lookup"><span data-stu-id="64e0e-162">Default Value</span></span> | <span data-ttu-id="64e0e-163">必要</span><span class="sxs-lookup"><span data-stu-id="64e0e-163">Required</span></span> |
  | --- | --- | --- |
  <span data-ttu-id="64e0e-164">版本</span><span class="sxs-lookup"><span data-stu-id="64e0e-164">Version</span></span>   | <span data-ttu-id="64e0e-165">Windows 叢集為 HDI 3.3，Linux 叢集為 3.5。</span><span class="sxs-lookup"><span data-stu-id="64e0e-165">HDI 3.3 for Windows cluster and 3.5 for Linux cluster.</span></span>    | <span data-ttu-id="64e0e-166">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-166">No</span></span>
  <span data-ttu-id="64e0e-167">osType</span><span class="sxs-lookup"><span data-stu-id="64e0e-167">osType</span></span> | <span data-ttu-id="64e0e-168">預設值為 Linux</span><span class="sxs-lookup"><span data-stu-id="64e0e-168">The default is Linux</span></span> | <span data-ttu-id="64e0e-169">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-169">No</span></span>

  <span data-ttu-id="64e0e-170">**建議：**</span><span class="sxs-lookup"><span data-stu-id="64e0e-170">**Recommendations:**</span></span> 
  * <span data-ttu-id="64e0e-171">在 **2017/07/15** 之前利用[可以搭配不同 HDInsight 版本使用的 Hadoop 元件](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions)和[與 HDInsight 版本相關聯的 Hortonworks 版本資訊](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)中記載的資訊，執行測試以確保參考此連結服務之活動的相容性為[最新支援的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-171">Before **07/15/2017**, perform tests to ensure the compatibility of the Activities that reference this Linked Services to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) with information documented in [Hadoop components available with different HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) and [Hortonworks release notes associated with HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).</span></span>  
  * <span data-ttu-id="64e0e-172">在 **2017/07/15** 之後，如果您想要覆寫預設設定，請務必明確指定 osType 和版本值。</span><span class="sxs-lookup"><span data-stu-id="64e0e-172">After **07/15/2017**, make sure you explicitly specify osType and version values if you would like to override the default settings.</span></span> 

>[!Note]
><span data-ttu-id="64e0e-173">目前 Azure Data Factory 不支援使用 Azure Data Lake Store 作為主要存放區的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="64e0e-173">Currently Azure Data Factory does not support HDInsight clusters using Azure Data Lake Store as primary store.</span></span> <span data-ttu-id="64e0e-174">使用 Azure 儲存體作為 HDInsight 叢集的主要存放區。</span><span class="sxs-lookup"><span data-stu-id="64e0e-174">Use Azure Storage as primary store for HDInsight clusters.</span></span> 
>  
>  

## <a name="on-demand-compute-environment"></a><span data-ttu-id="64e0e-175">隨選計算環境</span><span class="sxs-lookup"><span data-stu-id="64e0e-175">On-demand compute environment</span></span>
<span data-ttu-id="64e0e-176">在這種組態中，運算環境完全是由 Azure Data Factory 服務管理。</span><span class="sxs-lookup"><span data-stu-id="64e0e-176">In this type of configuration, the computing environment is fully managed by the Azure Data Factory service.</span></span> <span data-ttu-id="64e0e-177">Data Factory 服務會在工作提交前自動建立運算環境以處理資料，而在工作完成時予以移除。</span><span class="sxs-lookup"><span data-stu-id="64e0e-177">It is automatically created by the Data Factory service before a job is submitted to process data and removed when the job is completed.</span></span> <span data-ttu-id="64e0e-178">您可以建立隨選計算環境的連結服務、加以設定，以及控制工作執行、叢集管理和啟動動作的細微設定。</span><span class="sxs-lookup"><span data-stu-id="64e0e-178">You can create a linked service for the on-demand compute environment, configure it, and control granular settings for job execution, cluster management, and bootstrapping actions.</span></span>

> [!NOTE]
> <span data-ttu-id="64e0e-179">目前僅支援 Azure HDInsight 叢集的隨選組態。</span><span class="sxs-lookup"><span data-stu-id="64e0e-179">The on-demand configuration is currently supported only for Azure HDInsight clusters.</span></span>
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a><span data-ttu-id="64e0e-180">Azure HDInsight 隨選連結服務</span><span class="sxs-lookup"><span data-stu-id="64e0e-180">Azure HDInsight On-Demand Linked Service</span></span>
<span data-ttu-id="64e0e-181">Azure Data Factory 服務可自動建立以 Windows/Linux 為基礎的隨選 HDInsight 叢集來處理資料。</span><span class="sxs-lookup"><span data-stu-id="64e0e-181">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span></span> <span data-ttu-id="64e0e-182">此叢集會建立在與叢集相關聯的儲存體帳戶 (JSON 中的 linkedServiceName 屬性) 相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="64e0e-182">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span></span> <span data-ttu-id="64e0e-183">儲存體帳戶必須是一般目的標準 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="64e0e-183">The storage account must be a general-purpose standard Azure storage account.</span></span> 

<span data-ttu-id="64e0e-184">請注意下列有關隨選 HDInsight 連結服務的 **重點** ：</span><span class="sxs-lookup"><span data-stu-id="64e0e-184">Note the following **important** points about on-demand HDInsight linked service:</span></span>

* <span data-ttu-id="64e0e-185">您不會看到 Azure 訂用帳戶中建立的隨選 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="64e0e-185">You do not see the on-demand HDInsight cluster created in your Azure subscription.</span></span> <span data-ttu-id="64e0e-186">Azure Data Factory 服務會代您管理隨選 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="64e0e-186">the Azure Data Factory service manages the on-demand HDInsight cluster on your behalf.</span></span>
* <span data-ttu-id="64e0e-187">在隨選 HDInsight 叢集上執行之工作的記錄檔會被複製到與 HDInsight 叢集相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="64e0e-187">The logs for jobs that are run on an on-demand HDInsight cluster are copied to the storage account associated with the HDInsight cluster.</span></span> <span data-ttu-id="64e0e-188">您可以從 Azure 入口網站的 [活動執行詳細資料]  刀鋒視窗存取這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="64e0e-188">You can access these logs from the Azure portal in the **Activity Run Details** blade.</span></span> <span data-ttu-id="64e0e-189">如需詳細資訊，請參閱 [監視及管理管線](data-factory-monitor-manage-pipelines.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="64e0e-189">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>
* <span data-ttu-id="64e0e-190">只會針對 HDInsight 叢集啟動並執行工作的時間來向您收取費用。</span><span class="sxs-lookup"><span data-stu-id="64e0e-190">You are charged only for the time when the HDInsight cluster is up and running jobs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64e0e-191">通常會花費 **20 分鐘**或更久的時間來佈建隨選 Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="64e0e-191">It typically takes **20 minutes** or more to provision an Azure HDInsight cluster on demand.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="64e0e-192">範例</span><span class="sxs-lookup"><span data-stu-id="64e0e-192">Example</span></span>
<span data-ttu-id="64e0e-193">下列 JSON 會定義以 Linux 為基礎的隨選 HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="64e0e-193">The following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="64e0e-194">Data Factory 服務會在處理資料配量時自動建立 **以 Linux 為基礎的** HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="64e0e-194">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

<span data-ttu-id="64e0e-195">若要使用以 Windows 為基礎的 HDInsight 叢集，請將 **osType** 設為 **windows**，或者不要使用此屬性，因為預設值是︰windows。</span><span class="sxs-lookup"><span data-stu-id="64e0e-195">To use a Windows-based HDInsight cluster, set **osType** to **windows** or do not use the property as the default value is: windows.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="64e0e-196">HDInsight 叢集會在您於 JSON 中指定的 Blob 儲存體 (**linkedServiceName**) 建立**預設容器**。</span><span class="sxs-lookup"><span data-stu-id="64e0e-196">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="64e0e-197">HDInsight 不會在刪除叢集時刪除此容器。</span><span class="sxs-lookup"><span data-stu-id="64e0e-197">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="64e0e-198">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="64e0e-198">This behavior is by design.</span></span> <span data-ttu-id="64e0e-199">在使用 HDInsight 隨選連結服務時，除非有現有的即時叢集 (**timeToLive**)，否則每當需要處理配量時，就會建立 HDInsight 叢集，並在處理完成時予以刪除。</span><span class="sxs-lookup"><span data-stu-id="64e0e-199">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span> 
> 
> <span data-ttu-id="64e0e-200">隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。</span><span class="sxs-lookup"><span data-stu-id="64e0e-200">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="64e0e-201">如果在疑難排解作業時不需要這些容器，建議您加以刪除以降低儲存成本。</span><span class="sxs-lookup"><span data-stu-id="64e0e-201">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="64e0e-202">這些容器的名稱會遵循模式︰`adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`。</span><span class="sxs-lookup"><span data-stu-id="64e0e-202">The names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="64e0e-203">請使用 [Microsoft 儲存體總管](http://storageexplorer.com/) 之類的工具刪除 Azure Blob 儲存體中的容器。</span><span class="sxs-lookup"><span data-stu-id="64e0e-203">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="64e0e-204">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-204">Properties</span></span>
| <span data-ttu-id="64e0e-205">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-205">Property</span></span> | <span data-ttu-id="64e0e-206">說明</span><span class="sxs-lookup"><span data-stu-id="64e0e-206">Description</span></span> | <span data-ttu-id="64e0e-207">必要</span><span class="sxs-lookup"><span data-stu-id="64e0e-207">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64e0e-208">類型</span><span class="sxs-lookup"><span data-stu-id="64e0e-208">type</span></span> |<span data-ttu-id="64e0e-209">type 屬性應設為 **HDInsightOnDemand**。</span><span class="sxs-lookup"><span data-stu-id="64e0e-209">The type property should be set to **HDInsightOnDemand**.</span></span> |<span data-ttu-id="64e0e-210">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-210">Yes</span></span> |
| <span data-ttu-id="64e0e-211">clusterSize</span><span class="sxs-lookup"><span data-stu-id="64e0e-211">clusterSize</span></span> |<span data-ttu-id="64e0e-212">叢集中的背景工作/資料節點數。</span><span class="sxs-lookup"><span data-stu-id="64e0e-212">Number of worker/data nodes in the cluster.</span></span> <span data-ttu-id="64e0e-213">HDInsight 叢集會利用您為此屬性指定的 2 個前端節點以及背景工作節點數目來建立。</span><span class="sxs-lookup"><span data-stu-id="64e0e-213">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span></span> <span data-ttu-id="64e0e-214">節點大小為具有 4 個核心的 Standard_D3，因此 4 個背景工作節點的叢集需要 24 個核心 (4\*4 = 16 個核心用於背景工作節點，加上 2\*4 = 8 個核心用於前端節點)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-214">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="64e0e-215">如需 Standard_D3 層的詳細資料，請參閱[在 HDInsight 中建立 Linux 型 Hadoop 叢集](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-215">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span></span> |<span data-ttu-id="64e0e-216">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-216">Yes</span></span> |
| <span data-ttu-id="64e0e-217">timetolive</span><span class="sxs-lookup"><span data-stu-id="64e0e-217">timetolive</span></span> |<span data-ttu-id="64e0e-218">隨選 HDInsight 叢集允許的閒置時間。</span><span class="sxs-lookup"><span data-stu-id="64e0e-218">The allowed idle time for the on-demand HDInsight cluster.</span></span> <span data-ttu-id="64e0e-219">指定在活動執行完成後，如果叢集中沒有其他作用中的作業，隨選 HDInsight 叢集要保持運作多久。</span><span class="sxs-lookup"><span data-stu-id="64e0e-219">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span></span><br/><br/><span data-ttu-id="64e0e-220">例如，如果活動執行花費 6 分鐘，而 timetolive 設為 5 分鐘，叢集會在處理活動執行的 6 分鐘期間之後保持運作 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="64e0e-220">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span></span> <span data-ttu-id="64e0e-221">如果 6 分鐘期間內執行另一個活動，則會由相同叢集來處理。</span><span class="sxs-lookup"><span data-stu-id="64e0e-221">If another activity run is executed with the 6-minutes window, it is processed by the same cluster.</span></span><br/><br/><span data-ttu-id="64e0e-222">建立隨選 HDInsight 叢集是昂貴的作業 (可能需要一段時間)，因此請視需要使用這項設定，重複使用隨選 HDInsight 叢集以改善 Data Factory 的效能。</span><span class="sxs-lookup"><span data-stu-id="64e0e-222">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="64e0e-223">如果您將 timetolive 值設為 0，叢集會在活動執行完成後立即刪除。</span><span class="sxs-lookup"><span data-stu-id="64e0e-223">If you set timetolive value to 0, the cluster is deleted as soon as the activity run completes.</span></span> <span data-ttu-id="64e0e-224">然而，如果您設定較高的值，叢集可能會有不必要的閒置而導致高成本。</span><span class="sxs-lookup"><span data-stu-id="64e0e-224">Whereas, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="64e0e-225">因此，請務必根據您的需求設定適當的值。</span><span class="sxs-lookup"><span data-stu-id="64e0e-225">Therefore, it is important that you set the appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="64e0e-226">如果適當地設定 timetolive 屬性值，則多個管線可以共用隨選 HDInsight 叢集的執行個體。</span><span class="sxs-lookup"><span data-stu-id="64e0e-226">If the timetolive property value is appropriately set, multiple pipelines can share the instance of the on-demand HDInsight cluster.</span></span>  |<span data-ttu-id="64e0e-227">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-227">Yes</span></span> |
| <span data-ttu-id="64e0e-228">版本</span><span class="sxs-lookup"><span data-stu-id="64e0e-228">version</span></span> |<span data-ttu-id="64e0e-229">HDInsight 叢集的版本。</span><span class="sxs-lookup"><span data-stu-id="64e0e-229">Version of the HDInsight cluster.</span></span> <span data-ttu-id="64e0e-230">針對 Windows 叢集的預設值為 3.1，針對 Linux 叢集的預設值為 3.2。</span><span class="sxs-lookup"><span data-stu-id="64e0e-230">The default value is 3.1 for Windows cluster and 3.2 for Linux cluster.</span></span> |<span data-ttu-id="64e0e-231">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-231">No</span></span> |
| <span data-ttu-id="64e0e-232">預設容器</span><span class="sxs-lookup"><span data-stu-id="64e0e-232">linkedServiceName</span></span> | <span data-ttu-id="64e0e-233">隨選叢集用於儲存及處理資料的 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="64e0e-233">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span></span> <span data-ttu-id="64e0e-234">建立 HDInsight 叢集的區域和這個 Azure 儲存體帳戶的區域相同。</span><span class="sxs-lookup"><span data-stu-id="64e0e-234">The HDInsight cluster is created in the same region as this Azure Storage account.</span></span><p><span data-ttu-id="64e0e-235">目前，您無法建立使用 Azure Data Lake Store 做為儲存體的隨選 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="64e0e-235">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span></span> <span data-ttu-id="64e0e-236">如果您想要在 Azure Data Lake Store 中儲存 HDInsight 處理的結果資料，可使用複製活動將 Azure Blob 儲存體的資料複製到 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="64e0e-236">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span></span> </p>  | <span data-ttu-id="64e0e-237">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-237">Yes</span></span> |
| <span data-ttu-id="64e0e-238">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="64e0e-238">additionalLinkedServiceNames</span></span> |<span data-ttu-id="64e0e-239">指定 HDInsight 連結服務的其他儲存體帳戶，讓 Data Factory 服務代表您註冊它們。</span><span class="sxs-lookup"><span data-stu-id="64e0e-239">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> <span data-ttu-id="64e0e-240">這些儲存體帳戶與 HDInsight 叢集必須在相同區域，而建立此叢集的區域與 linkedServiceName 所指定之儲存體帳戶的區域相同。</span><span class="sxs-lookup"><span data-stu-id="64e0e-240">These storage accounts must be in the same region as the HDInsight cluster, which is created in the same region as the storage account specified by linkedServiceName.</span></span> |<span data-ttu-id="64e0e-241">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-241">No</span></span> |
| <span data-ttu-id="64e0e-242">osType</span><span class="sxs-lookup"><span data-stu-id="64e0e-242">osType</span></span> |<span data-ttu-id="64e0e-243">作業系統的類型。</span><span class="sxs-lookup"><span data-stu-id="64e0e-243">Type of operating system.</span></span> <span data-ttu-id="64e0e-244">允許的值為：Windows (預設值) 和 linux</span><span class="sxs-lookup"><span data-stu-id="64e0e-244">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="64e0e-245">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-245">No</span></span> |
| <span data-ttu-id="64e0e-246">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="64e0e-246">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="64e0e-247">指向 HCatalog 資料庫的 Azure SQL 連結服務名稱。</span><span class="sxs-lookup"><span data-stu-id="64e0e-247">The name of Azure SQL linked service that point to the HCatalog database.</span></span> <span data-ttu-id="64e0e-248">會使用 Azure SQL 資料庫作為中繼存放區，建立隨選 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="64e0e-248">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span></span> |<span data-ttu-id="64e0e-249">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-249">No</span></span> |

#### <a name="additionallinkedservicenames-json-example"></a><span data-ttu-id="64e0e-250">additionalLinkedServiceNames JSON 範例</span><span class="sxs-lookup"><span data-stu-id="64e0e-250">additionalLinkedServiceNames JSON example</span></span>

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a><span data-ttu-id="64e0e-251">進階屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-251">Advanced Properties</span></span>
<span data-ttu-id="64e0e-252">您也可以針對隨選 HDInsight 叢集的細微組態指定下列屬性。</span><span class="sxs-lookup"><span data-stu-id="64e0e-252">You can also specify the following properties for the granular configuration of the on-demand HDInsight cluster.</span></span>

| <span data-ttu-id="64e0e-253">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-253">Property</span></span> | <span data-ttu-id="64e0e-254">說明</span><span class="sxs-lookup"><span data-stu-id="64e0e-254">Description</span></span> | <span data-ttu-id="64e0e-255">必要</span><span class="sxs-lookup"><span data-stu-id="64e0e-255">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="64e0e-256">coreConfiguration</span><span class="sxs-lookup"><span data-stu-id="64e0e-256">coreConfiguration</span></span> |<span data-ttu-id="64e0e-257">指定要建立之 HDInsight 叢集的核心組態參數 (如 core-site.xml 所示)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-257">Specifies the core configuration parameters (as in core-site.xml) for the HDInsight cluster to be created.</span></span> |<span data-ttu-id="64e0e-258">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-258">No</span></span> |
| <span data-ttu-id="64e0e-259">hBaseConfiguration</span><span class="sxs-lookup"><span data-stu-id="64e0e-259">hBaseConfiguration</span></span> |<span data-ttu-id="64e0e-260">指定 HDInsight 叢集的 HBase 組態參數 (hbase-site.xml)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-260">Specifies the HBase configuration parameters (hbase-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="64e0e-261">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-261">No</span></span> |
| <span data-ttu-id="64e0e-262">hdfsConfiguration</span><span class="sxs-lookup"><span data-stu-id="64e0e-262">hdfsConfiguration</span></span> |<span data-ttu-id="64e0e-263">指定 HDInsight 叢集的 HDFS 組態參數 (hdfs-site.xml)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-263">Specifies the HDFS configuration parameters (hdfs-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="64e0e-264">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-264">No</span></span> |
| <span data-ttu-id="64e0e-265">hiveConfiguration</span><span class="sxs-lookup"><span data-stu-id="64e0e-265">hiveConfiguration</span></span> |<span data-ttu-id="64e0e-266">指定 HDInsight 叢集的 hive 組態參數 (hive-site.xml)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-266">Specifies the hive configuration parameters (hive-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="64e0e-267">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-267">No</span></span> |
| <span data-ttu-id="64e0e-268">mapReduceConfiguration</span><span class="sxs-lookup"><span data-stu-id="64e0e-268">mapReduceConfiguration</span></span> |<span data-ttu-id="64e0e-269">指定 HDInsight 叢集的 MapReduce 組態參數 (mapred-site.xml)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-269">Specifies the MapReduce configuration parameters (mapred-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="64e0e-270">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-270">No</span></span> |
| <span data-ttu-id="64e0e-271">oozieConfiguration</span><span class="sxs-lookup"><span data-stu-id="64e0e-271">oozieConfiguration</span></span> |<span data-ttu-id="64e0e-272">指定 HDInsight 叢集的 Oozie 組態參數 (oozie-site.xml)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-272">Specifies the Oozie configuration parameters (oozie-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="64e0e-273">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-273">No</span></span> |
| <span data-ttu-id="64e0e-274">stormConfiguration</span><span class="sxs-lookup"><span data-stu-id="64e0e-274">stormConfiguration</span></span> |<span data-ttu-id="64e0e-275">指定 HDInsight 叢集的 Storm 組態參數 (storm-site.xml)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-275">Specifies the Storm configuration parameters (storm-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="64e0e-276">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-276">No</span></span> |
| <span data-ttu-id="64e0e-277">yarnConfiguration</span><span class="sxs-lookup"><span data-stu-id="64e0e-277">yarnConfiguration</span></span> |<span data-ttu-id="64e0e-278">指定 HDInsight 叢集的 Yarn 組態參數 (yarn-site.xml)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-278">Specifies the Yarn configuration parameters (yarn-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="64e0e-279">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-279">No</span></span> |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a><span data-ttu-id="64e0e-280">範例 – 包含進階屬性的隨選 HDInsight 叢集組態</span><span class="sxs-lookup"><span data-stu-id="64e0e-280">Example – On-demand HDInsight cluster configuration with advanced properties</span></span>

```json
{
  "name": " HDInsightOnDemandLinkedService",
  "properties": {
    "type": "HDInsightOnDemand",
    "typeProperties": {
      "clusterSize": 16,
      "timeToLive": "01:30:00",
      "linkedServiceName": "adfods1",
      "coreConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "hiveConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "mapReduceConfiguration": {
        "mapreduce.reduce.java.opts": "-Xmx4000m",
        "mapreduce.map.java.opts": "-Xmx4000m",
        "mapreduce.map.memory.mb": "5000",
        "mapreduce.reduce.memory.mb": "5000",
        "mapreduce.job.reduce.slowstart.completedmaps": "0.8"
      },
      "yarnConfiguration": {
        "yarn.app.mapreduce.am.resource.mb": "5000",
        "mapreduce.map.memory.mb": "5000"
      },
      "additionalLinkedServiceNames": [
        "datafeeds",
        "adobedatafeed"
      ]
    }
  }
}
```

### <a name="node-sizes"></a><span data-ttu-id="64e0e-281">節點大小</span><span class="sxs-lookup"><span data-stu-id="64e0e-281">Node sizes</span></span>
<span data-ttu-id="64e0e-282">您可使用下列屬性指定前端、資料和的 zookeeper 節點的大小：</span><span class="sxs-lookup"><span data-stu-id="64e0e-282">You can specify the sizes of head, data, and zookeeper nodes using the following properties:</span></span> 

| <span data-ttu-id="64e0e-283">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-283">Property</span></span> | <span data-ttu-id="64e0e-284">說明</span><span class="sxs-lookup"><span data-stu-id="64e0e-284">Description</span></span> | <span data-ttu-id="64e0e-285">必要</span><span class="sxs-lookup"><span data-stu-id="64e0e-285">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="64e0e-286">headNodeSize</span><span class="sxs-lookup"><span data-stu-id="64e0e-286">headNodeSize</span></span> |<span data-ttu-id="64e0e-287">指定前端節點的大小。</span><span class="sxs-lookup"><span data-stu-id="64e0e-287">Specifies the size of the head node.</span></span> <span data-ttu-id="64e0e-288">預設值為：Standard_D3。</span><span class="sxs-lookup"><span data-stu-id="64e0e-288">The default value is: Standard_D3.</span></span> <span data-ttu-id="64e0e-289">如需詳細資料，請參閱**指定節點大小**一節。</span><span class="sxs-lookup"><span data-stu-id="64e0e-289">See the **Specifying node sizes** section for details.</span></span> |<span data-ttu-id="64e0e-290">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-290">No</span></span> |
| <span data-ttu-id="64e0e-291">dataNodeSize</span><span class="sxs-lookup"><span data-stu-id="64e0e-291">dataNodeSize</span></span> |<span data-ttu-id="64e0e-292">指定資料節點的大小。</span><span class="sxs-lookup"><span data-stu-id="64e0e-292">Specifies the size of the data node.</span></span> <span data-ttu-id="64e0e-293">預設值為：Standard_D3。</span><span class="sxs-lookup"><span data-stu-id="64e0e-293">The default value is: Standard_D3.</span></span> |<span data-ttu-id="64e0e-294">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-294">No</span></span> |
| <span data-ttu-id="64e0e-295">zookeeperNodeSize</span><span class="sxs-lookup"><span data-stu-id="64e0e-295">zookeeperNodeSize</span></span> |<span data-ttu-id="64e0e-296">指定 Zoo Keeper 節點的大小。</span><span class="sxs-lookup"><span data-stu-id="64e0e-296">Specifies the size of the Zoo Keeper node.</span></span> <span data-ttu-id="64e0e-297">預設值為：Standard_D3。</span><span class="sxs-lookup"><span data-stu-id="64e0e-297">The default value is: Standard_D3.</span></span> |<span data-ttu-id="64e0e-298">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-298">No</span></span> |

#### <a name="specifying-node-sizes"></a><span data-ttu-id="64e0e-299">指定節點大小</span><span class="sxs-lookup"><span data-stu-id="64e0e-299">Specifying node sizes</span></span>
<span data-ttu-id="64e0e-300">有關您在上一節所述的屬性中需要指定的字串值，請參閱[虛擬機器的大小](../virtual-machines/linux/sizes.md)一文。</span><span class="sxs-lookup"><span data-stu-id="64e0e-300">See the [Sizes of Virtual Machines](../virtual-machines/linux/sizes.md) article for string values you need to specify for the properties mentioned in the previous section.</span></span> <span data-ttu-id="64e0e-301">值必須符合本文件中所參考的 **CMDLET 與 APIS**。</span><span class="sxs-lookup"><span data-stu-id="64e0e-301">The values need to conform to the **CMDLETs & APIS** referenced in the article.</span></span> <span data-ttu-id="64e0e-302">如文中所述，「大型」(預設值) 資料節點的記憶體大小為 7-GB，但這可能不適用於您的案例。</span><span class="sxs-lookup"><span data-stu-id="64e0e-302">As you can see in the article, the data node of Large (default) size has 7-GB memory, which may not be good enough for your scenario.</span></span> 

<span data-ttu-id="64e0e-303">若想要建立 D4 大小的前端節點與背景工作節點，請指定 **Standard_D4** 作為 headNodeSize 與 dataNodeSize 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="64e0e-303">If you want to create D4 sized head nodes and worker nodes, specify **Standard_D4** as the value for headNodeSize and dataNodeSize properties.</span></span> 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

<span data-ttu-id="64e0e-304">若您為這些屬性指定錯誤的值，可能會顯示下列 **錯誤：** 無法建立叢集。</span><span class="sxs-lookup"><span data-stu-id="64e0e-304">If you specify a wrong value for these properties, you may receive the following **error:** Failed to create cluster.</span></span> <span data-ttu-id="64e0e-305">例外狀況：無法完成叢集建立作業。</span><span class="sxs-lookup"><span data-stu-id="64e0e-305">Exception: Unable to complete the cluster create operation.</span></span> <span data-ttu-id="64e0e-306">作業失敗，錯誤碼為 '400'。</span><span class="sxs-lookup"><span data-stu-id="64e0e-306">Operation failed with code '400'.</span></span> <span data-ttu-id="64e0e-307">叢集剩餘狀態：「錯誤」。</span><span class="sxs-lookup"><span data-stu-id="64e0e-307">Cluster left behind state: 'Error'.</span></span> <span data-ttu-id="64e0e-308">訊息：「PreClusterCreationValidationFailure」。</span><span class="sxs-lookup"><span data-stu-id="64e0e-308">Message: 'PreClusterCreationValidationFailure'.</span></span> <span data-ttu-id="64e0e-309">出現此錯誤時，請確定您是使用[虛擬機器的大小](../virtual-machines/linux/sizes.md)一文的表格中的 **CMDLET 與 API** 名稱。</span><span class="sxs-lookup"><span data-stu-id="64e0e-309">When you receive this error, ensure that you are using the **CMDLET & APIS** name from the table in the [Sizes of Virtual Machines](../virtual-machines/linux/sizes.md) article.</span></span>  

## <a name="bring-your-own-compute-environment"></a><span data-ttu-id="64e0e-310">自備計算環境</span><span class="sxs-lookup"><span data-stu-id="64e0e-310">Bring your own compute environment</span></span>
<span data-ttu-id="64e0e-311">在這種組態中，使用者可以將現有的運算環境註冊為 Data Factory 中的連結服務。</span><span class="sxs-lookup"><span data-stu-id="64e0e-311">In this type of configuration, users can register an already existing computing environment as a linked service in Data Factory.</span></span> <span data-ttu-id="64e0e-312">此運算環境是由使用者管理並由 Data Factory 服務用來執行活動。</span><span class="sxs-lookup"><span data-stu-id="64e0e-312">The computing environment is managed by the user and the Data Factory service uses it to execute the activities.</span></span>

<span data-ttu-id="64e0e-313">下列計算環境可支援這類型的組態：</span><span class="sxs-lookup"><span data-stu-id="64e0e-313">This type of configuration is supported for the following compute environments:</span></span>

* <span data-ttu-id="64e0e-314">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="64e0e-314">Azure HDInsight</span></span>
* <span data-ttu-id="64e0e-315">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="64e0e-315">Azure Batch</span></span>
* <span data-ttu-id="64e0e-316">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="64e0e-316">Azure Machine Learning</span></span>
* <span data-ttu-id="64e0e-317">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="64e0e-317">Azure Data Lake Analytics</span></span>
* <span data-ttu-id="64e0e-318">Azure SQL DB、Azure SQL DW、SQL Server</span><span class="sxs-lookup"><span data-stu-id="64e0e-318">Azure SQL DB, Azure SQL DW, SQL Server</span></span>

## <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="64e0e-319">Azure HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="64e0e-319">Azure HDInsight Linked Service</span></span>
<span data-ttu-id="64e0e-320">您可以建立 Azure HDInsight 連結服務，以向 Data Factory 註冊自己的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="64e0e-320">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span></span>

### <a name="example"></a><span data-ttu-id="64e0e-321">範例</span><span class="sxs-lookup"><span data-stu-id="64e0e-321">Example</span></span>

```json
{
  "name": "HDInsightLinkedService",
  "properties": {
    "type": "HDInsight",
    "typeProperties": {
      "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
      "userName": "admin",
      "password": "<password>",
      "linkedServiceName": "MyHDInsightStoragelinkedService"
    }
  }
}
```

### <a name="properties"></a><span data-ttu-id="64e0e-322">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-322">Properties</span></span>
| <span data-ttu-id="64e0e-323">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-323">Property</span></span> | <span data-ttu-id="64e0e-324">說明</span><span class="sxs-lookup"><span data-stu-id="64e0e-324">Description</span></span> | <span data-ttu-id="64e0e-325">必要</span><span class="sxs-lookup"><span data-stu-id="64e0e-325">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64e0e-326">類型</span><span class="sxs-lookup"><span data-stu-id="64e0e-326">type</span></span> |<span data-ttu-id="64e0e-327">type 屬性應設為 **HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="64e0e-327">The type property should be set to **HDInsight**.</span></span> |<span data-ttu-id="64e0e-328">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-328">Yes</span></span> |
| <span data-ttu-id="64e0e-329">clusterUri</span><span class="sxs-lookup"><span data-stu-id="64e0e-329">clusterUri</span></span> |<span data-ttu-id="64e0e-330">HDInsight 叢集的 URI。</span><span class="sxs-lookup"><span data-stu-id="64e0e-330">The URI of the HDInsight cluster.</span></span> |<span data-ttu-id="64e0e-331">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-331">Yes</span></span> |
| <span data-ttu-id="64e0e-332">username</span><span class="sxs-lookup"><span data-stu-id="64e0e-332">username</span></span> |<span data-ttu-id="64e0e-333">指定要用來連接到現有 HDInsight 叢集的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="64e0e-333">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span></span> |<span data-ttu-id="64e0e-334">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-334">Yes</span></span> |
| <span data-ttu-id="64e0e-335">password</span><span class="sxs-lookup"><span data-stu-id="64e0e-335">password</span></span> |<span data-ttu-id="64e0e-336">指定使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="64e0e-336">Specify password for the user account.</span></span> |<span data-ttu-id="64e0e-337">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-337">Yes</span></span> |
| <span data-ttu-id="64e0e-338">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="64e0e-338">linkedServiceName</span></span> | <span data-ttu-id="64e0e-339">參照 HDInsight 叢集所使用 Azure Blob 儲存體的 Azure 儲存體連結服務名稱。</span><span class="sxs-lookup"><span data-stu-id="64e0e-339">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span></span> <p><span data-ttu-id="64e0e-340">目前，您無法針對此屬性指定 Azure Data Lake Store 連結服務。</span><span class="sxs-lookup"><span data-stu-id="64e0e-340">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="64e0e-341">如果 HDInsight 叢集可存取 Data Lake Store，您可以透過 Hive/Pig 指令碼存取 Azure Data Lake Store 中的資料。</span><span class="sxs-lookup"><span data-stu-id="64e0e-341">If the HDInsight cluster has access to the Data Lake Store, you may access data in the Azure Data Lake Store from Hive/Pig scripts.</span></span> </p>  |<span data-ttu-id="64e0e-342">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-342">Yes</span></span> |

## <a name="azure-batch-linked-service"></a><span data-ttu-id="64e0e-343">Azure Batch 連結服務</span><span class="sxs-lookup"><span data-stu-id="64e0e-343">Azure Batch Linked Service</span></span>
<span data-ttu-id="64e0e-344">您可以建立 Azure Batch 連結服務，以向 Data Factory 註冊虛擬機器 (VM) 的 Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="64e0e-344">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) to a data factory.</span></span> <span data-ttu-id="64e0e-345">您可以使用 Azure Batch 或 Azure HDInsight 執行 .NET 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="64e0e-345">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span>

<span data-ttu-id="64e0e-346">如果您不熟悉 Azure Batch 服務，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="64e0e-346">See following topics if you are new to Azure Batch service:</span></span>

* <span data-ttu-id="64e0e-347">[Azure Batch 基本知識](../batch/batch-technical-overview.md) ，以取得 Azure Batch 服務的概觀。</span><span class="sxs-lookup"><span data-stu-id="64e0e-347">[Azure Batch basics](../batch/batch-technical-overview.md) for an overview of the Azure Batch service.</span></span>
* <span data-ttu-id="64e0e-348">[New-AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) Cmdlet 可建立 Azure Batch 帳戶 (或) [Azure 入口網站](../batch/batch-account-create-portal.md)，以使用 Azure 入口網站建立 Azure Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="64e0e-348">[New-AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) cmdlet to create an Azure Batch account (or) [Azure portal](../batch/batch-account-create-portal.md) to create the Azure Batch account using Azure portal.</span></span> <span data-ttu-id="64e0e-349">如需使用此 Cmdlet 的詳細指示，請參閱 [使用 PowerShell 管理 Azure Batch 帳戶](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) 主題。</span><span class="sxs-lookup"><span data-stu-id="64e0e-349">See [Using PowerShell to manage Azure Batch Account](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) topic for detailed instructions on using the cmdlet.</span></span>
* <span data-ttu-id="64e0e-350">[New-AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) Cmdlet 可建立 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="64e0e-350">[New-AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet to create an Azure Batch pool.</span></span>

### <a name="example"></a><span data-ttu-id="64e0e-351">範例</span><span class="sxs-lookup"><span data-stu-id="64e0e-351">Example</span></span>

```json
{
  "name": "AzureBatchLinkedService",
  "properties": {
    "type": "AzureBatch",
    "typeProperties": {
      "accountName": "<Azure Batch account name>",
      "accessKey": "<Azure Batch account key>",
      "poolName": "<Azure Batch pool name>",
      "linkedServiceName": "<Specify associated storage linked service reference here>"
    }
  }
}
```

<span data-ttu-id="64e0e-352">將 "**.\<區域名稱\>**" 附加至為 **accountName** 屬性所用的 Batch 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="64e0e-352">Append "**.\<region name\>**" to the name of your batch account for the **accountName** property.</span></span> <span data-ttu-id="64e0e-353">範例：</span><span class="sxs-lookup"><span data-stu-id="64e0e-353">Example:</span></span>

```json
"accountName": "mybatchaccount.eastus"
```

<span data-ttu-id="64e0e-354">另一個選項是提供 batchUri 端點，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="64e0e-354">Another option is to provide the batchUri endpoint as shown in the following sample:</span></span>

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a><span data-ttu-id="64e0e-355">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-355">Properties</span></span>
| <span data-ttu-id="64e0e-356">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-356">Property</span></span> | <span data-ttu-id="64e0e-357">說明</span><span class="sxs-lookup"><span data-stu-id="64e0e-357">Description</span></span> | <span data-ttu-id="64e0e-358">必要</span><span class="sxs-lookup"><span data-stu-id="64e0e-358">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64e0e-359">類型</span><span class="sxs-lookup"><span data-stu-id="64e0e-359">type</span></span> |<span data-ttu-id="64e0e-360">type 屬性應設為 **AzureBatch**。</span><span class="sxs-lookup"><span data-stu-id="64e0e-360">The type property should be set to **AzureBatch**.</span></span> |<span data-ttu-id="64e0e-361">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-361">Yes</span></span> |
| <span data-ttu-id="64e0e-362">accountName</span><span class="sxs-lookup"><span data-stu-id="64e0e-362">accountName</span></span> |<span data-ttu-id="64e0e-363">建立 Azure Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="64e0e-363">Name of the Azure Batch account.</span></span> |<span data-ttu-id="64e0e-364">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-364">Yes</span></span> |
| <span data-ttu-id="64e0e-365">accessKey</span><span class="sxs-lookup"><span data-stu-id="64e0e-365">accessKey</span></span> |<span data-ttu-id="64e0e-366">Azure Batch 帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="64e0e-366">Access key for the Azure Batch account.</span></span> |<span data-ttu-id="64e0e-367">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-367">Yes</span></span> |
| <span data-ttu-id="64e0e-368">poolName</span><span class="sxs-lookup"><span data-stu-id="64e0e-368">poolName</span></span> |<span data-ttu-id="64e0e-369">虛擬機器的集區名稱。</span><span class="sxs-lookup"><span data-stu-id="64e0e-369">Name of the pool of virtual machines.</span></span> |<span data-ttu-id="64e0e-370">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-370">Yes</span></span> |
| <span data-ttu-id="64e0e-371">預設容器</span><span class="sxs-lookup"><span data-stu-id="64e0e-371">linkedServiceName</span></span> |<span data-ttu-id="64e0e-372">與此 Azure Batch 連結服務相關聯的 Azure 儲存體服務連結名稱。</span><span class="sxs-lookup"><span data-stu-id="64e0e-372">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="64e0e-373">此連結服務用於執行活動及儲存活動執行記錄檔所需的暫存檔案。</span><span class="sxs-lookup"><span data-stu-id="64e0e-373">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span></span> |<span data-ttu-id="64e0e-374">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-374">Yes</span></span> |

## <a name="azure-machine-learning-linked-service"></a><span data-ttu-id="64e0e-375">Azure Machine Learning 連結服務</span><span class="sxs-lookup"><span data-stu-id="64e0e-375">Azure Machine Learning Linked Service</span></span>
<span data-ttu-id="64e0e-376">您可建立 Azure Machine Learning 連結服務，以向 Data Factory 註冊 Machine Learning 批次評分端點。</span><span class="sxs-lookup"><span data-stu-id="64e0e-376">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint to a data factory.</span></span>

### <a name="example"></a><span data-ttu-id="64e0e-377">範例</span><span class="sxs-lookup"><span data-stu-id="64e0e-377">Example</span></span>

```json
{
  "name": "AzureMLLinkedService",
  "properties": {
    "type": "AzureML",
    "typeProperties": {
      "mlEndpoint": "https://[batch scoring endpoint]/jobs",
      "apiKey": "<apikey>"
    }
  }
}
```

### <a name="properties"></a><span data-ttu-id="64e0e-378">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-378">Properties</span></span>
| <span data-ttu-id="64e0e-379">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-379">Property</span></span> | <span data-ttu-id="64e0e-380">說明</span><span class="sxs-lookup"><span data-stu-id="64e0e-380">Description</span></span> | <span data-ttu-id="64e0e-381">必要</span><span class="sxs-lookup"><span data-stu-id="64e0e-381">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64e0e-382">類型</span><span class="sxs-lookup"><span data-stu-id="64e0e-382">Type</span></span> |<span data-ttu-id="64e0e-383">type 屬性應設為： **AzureML**。</span><span class="sxs-lookup"><span data-stu-id="64e0e-383">The type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="64e0e-384">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-384">Yes</span></span> |
| <span data-ttu-id="64e0e-385">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="64e0e-385">mlEndpoint</span></span> |<span data-ttu-id="64e0e-386">批次評分 URL。</span><span class="sxs-lookup"><span data-stu-id="64e0e-386">The batch scoring URL.</span></span> |<span data-ttu-id="64e0e-387">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-387">Yes</span></span> |
| <span data-ttu-id="64e0e-388">apiKey</span><span class="sxs-lookup"><span data-stu-id="64e0e-388">apiKey</span></span> |<span data-ttu-id="64e0e-389">已發佈的工作區模型的 API。</span><span class="sxs-lookup"><span data-stu-id="64e0e-389">The published workspace model’s API.</span></span> |<span data-ttu-id="64e0e-390">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-390">Yes</span></span> |

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="64e0e-391">Azure Data Lake Analytics 連結服務</span><span class="sxs-lookup"><span data-stu-id="64e0e-391">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="64e0e-392">您需建立 **Azure Data Lake Analytics** 連結服務，來將 Azure Data Lake Analytics 計算服務連結到 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="64e0e-392">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span></span> <span data-ttu-id="64e0e-393">管線中的 Data Lake Analytics U-SQL 活動會參考此連結服務。</span><span class="sxs-lookup"><span data-stu-id="64e0e-393">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span></span> 

<span data-ttu-id="64e0e-394">下表提供 JSON 定義中所使用之一般屬性的描述。</span><span class="sxs-lookup"><span data-stu-id="64e0e-394">The following table provides descriptions for the generic properties used in the JSON definition.</span></span> <span data-ttu-id="64e0e-395">您可以在服務主體與使用者認證驗證之間進一步選擇。</span><span class="sxs-lookup"><span data-stu-id="64e0e-395">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="64e0e-396">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-396">Property</span></span> | <span data-ttu-id="64e0e-397">說明</span><span class="sxs-lookup"><span data-stu-id="64e0e-397">Description</span></span> | <span data-ttu-id="64e0e-398">必要</span><span class="sxs-lookup"><span data-stu-id="64e0e-398">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64e0e-399">**type**</span><span class="sxs-lookup"><span data-stu-id="64e0e-399">**type**</span></span> |<span data-ttu-id="64e0e-400">type 屬性應設為： **AzureDataLakeAnalytics**。</span><span class="sxs-lookup"><span data-stu-id="64e0e-400">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="64e0e-401">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-401">Yes</span></span> |
| <span data-ttu-id="64e0e-402">**accountName**</span><span class="sxs-lookup"><span data-stu-id="64e0e-402">**accountName**</span></span> |<span data-ttu-id="64e0e-403">Azure Data Lake Analytics 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="64e0e-403">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="64e0e-404">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-404">Yes</span></span> |
| <span data-ttu-id="64e0e-405">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="64e0e-405">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="64e0e-406">Azure Data Lake Analytics URI。</span><span class="sxs-lookup"><span data-stu-id="64e0e-406">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="64e0e-407">否</span><span class="sxs-lookup"><span data-stu-id="64e0e-407">No</span></span> |
| <span data-ttu-id="64e0e-408">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="64e0e-408">**subscriptionId**</span></span> |<span data-ttu-id="64e0e-409">Azure 訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="64e0e-409">Azure subscription id</span></span> |<span data-ttu-id="64e0e-410">否 (如果未指定，便會使用 Data Factory 的訂用帳戶)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-410">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="64e0e-411">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="64e0e-411">**resourceGroupName**</span></span> |<span data-ttu-id="64e0e-412">Azure 資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="64e0e-412">Azure resource group name</span></span> |<span data-ttu-id="64e0e-413">否 (若未指定，便會使用 Data Factory 的資源群組)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-413">No (If not specified, resource group of the data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="64e0e-414">服務主體驗證 (建議)</span><span class="sxs-lookup"><span data-stu-id="64e0e-414">Service principal authentication (recommended)</span></span>
<span data-ttu-id="64e0e-415">若要使用服務主體驗證，請在 Azure Active Directory (Azure AD) 中註冊應用程式實體，並授與其 Data Lake Store 存取權。</span><span class="sxs-lookup"><span data-stu-id="64e0e-415">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="64e0e-416">如需詳細的步驟，請參閱[服務對服務驗證](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-416">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="64e0e-417">請記下以下的值，您可以使用這些值來定義連結服務：</span><span class="sxs-lookup"><span data-stu-id="64e0e-417">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="64e0e-418">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="64e0e-418">Application ID</span></span>
* <span data-ttu-id="64e0e-419">應用程式金鑰</span><span class="sxs-lookup"><span data-stu-id="64e0e-419">Application key</span></span> 
* <span data-ttu-id="64e0e-420">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="64e0e-420">Tenant ID</span></span>

<span data-ttu-id="64e0e-421">指定下列屬性以使用服務主體驗證：</span><span class="sxs-lookup"><span data-stu-id="64e0e-421">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="64e0e-422">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-422">Property</span></span> | <span data-ttu-id="64e0e-423">說明</span><span class="sxs-lookup"><span data-stu-id="64e0e-423">Description</span></span> | <span data-ttu-id="64e0e-424">必要</span><span class="sxs-lookup"><span data-stu-id="64e0e-424">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="64e0e-425">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="64e0e-425">**servicePrincipalId**</span></span> | <span data-ttu-id="64e0e-426">指定應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="64e0e-426">Specify the application's client ID.</span></span> | <span data-ttu-id="64e0e-427">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-427">Yes</span></span> |
| <span data-ttu-id="64e0e-428">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="64e0e-428">**servicePrincipalKey**</span></span> | <span data-ttu-id="64e0e-429">指定應用程式的金鑰。</span><span class="sxs-lookup"><span data-stu-id="64e0e-429">Specify the application's key.</span></span> | <span data-ttu-id="64e0e-430">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-430">Yes</span></span> |
| <span data-ttu-id="64e0e-431">**tenant**</span><span class="sxs-lookup"><span data-stu-id="64e0e-431">**tenant**</span></span> | <span data-ttu-id="64e0e-432">指定您的應用程式所在租用戶的資訊 (網域名稱或租用戶識別碼)。</span><span class="sxs-lookup"><span data-stu-id="64e0e-432">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="64e0e-433">將滑鼠游標暫留在 Azure 入口網站右上角，即可擷取它。</span><span class="sxs-lookup"><span data-stu-id="64e0e-433">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="64e0e-434">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-434">Yes</span></span> |

<span data-ttu-id="64e0e-435">**範例：服務主體驗證**</span><span class="sxs-lookup"><span data-stu-id="64e0e-435">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="64e0e-436">使用者認證驗證</span><span class="sxs-lookup"><span data-stu-id="64e0e-436">User credential authentication</span></span>
<span data-ttu-id="64e0e-437">或者，您也可以藉由指定下列屬性，使用 Data Lake Analytics 的使用者認證驗證：</span><span class="sxs-lookup"><span data-stu-id="64e0e-437">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying the following properties:</span></span>

| <span data-ttu-id="64e0e-438">屬性</span><span class="sxs-lookup"><span data-stu-id="64e0e-438">Property</span></span> | <span data-ttu-id="64e0e-439">說明</span><span class="sxs-lookup"><span data-stu-id="64e0e-439">Description</span></span> | <span data-ttu-id="64e0e-440">必要</span><span class="sxs-lookup"><span data-stu-id="64e0e-440">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="64e0e-441">**authorization**</span><span class="sxs-lookup"><span data-stu-id="64e0e-441">**authorization**</span></span> | <span data-ttu-id="64e0e-442">按一下「資料處理站編輯器」中的 [授權] 按鈕，然後輸入您的認證，此動作會將自動產生的授權 URL 指派給此屬性。</span><span class="sxs-lookup"><span data-stu-id="64e0e-442">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="64e0e-443">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-443">Yes</span></span> |
| <span data-ttu-id="64e0e-444">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="64e0e-444">**sessionId**</span></span> | <span data-ttu-id="64e0e-445">OAuth 授權工作階段的 OAuth 工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="64e0e-445">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="64e0e-446">每個工作階段識別碼都是唯一的，只能使用一次。</span><span class="sxs-lookup"><span data-stu-id="64e0e-446">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="64e0e-447">當您使用「資料處理站編輯器」時便會自動產生此設定。</span><span class="sxs-lookup"><span data-stu-id="64e0e-447">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="64e0e-448">是</span><span class="sxs-lookup"><span data-stu-id="64e0e-448">Yes</span></span> |

<span data-ttu-id="64e0e-449">**範例：使用者認證授權**</span><span class="sxs-lookup"><span data-stu-id="64e0e-449">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="64e0e-450">權杖到期</span><span class="sxs-lookup"><span data-stu-id="64e0e-450">Token expiration</span></span>
<span data-ttu-id="64e0e-451">您使用 [授權] 按鈕所產生的授權碼在一段時間後會到期。</span><span class="sxs-lookup"><span data-stu-id="64e0e-451">The authorization code you generated by using the **Authorize** button expires after sometime.</span></span> <span data-ttu-id="64e0e-452">請參閱下表以了解不同類型的使用者帳戶的到期時間。</span><span class="sxs-lookup"><span data-stu-id="64e0e-452">See the following table for the expiration times for different types of user accounts.</span></span> <span data-ttu-id="64e0e-453">當驗證**權杖到期**時，您可能會看到下列錯誤訊息：認證作業發生錯誤：invalid_grant - AADSTS70002：驗證認證時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="64e0e-453">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="64e0e-454">AADSTS70008：提供的存取授權已過期或撤銷。</span><span class="sxs-lookup"><span data-stu-id="64e0e-454">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="64e0e-455">追蹤識別碼：d18629e8-af88-43c5-88e3-d8419eb1fca1 相互關連識別碼：fac30a0c-6be6-4e02-8d69-a776d2ffefd7 時間戳記：2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="64e0e-455">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="64e0e-456">使用者類型</span><span class="sxs-lookup"><span data-stu-id="64e0e-456">User type</span></span> | <span data-ttu-id="64e0e-457">到期時間</span><span class="sxs-lookup"><span data-stu-id="64e0e-457">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="64e0e-458">不受 Azure Active Directory 管理的使用者帳戶 (@hotmail.com、@live.com 等)</span><span class="sxs-lookup"><span data-stu-id="64e0e-458">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="64e0e-459">12 小時</span><span class="sxs-lookup"><span data-stu-id="64e0e-459">12 hours</span></span> |
| <span data-ttu-id="64e0e-460">受 Azure Active Directory (AAD) 管理的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="64e0e-460">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="64e0e-461">最後一次執行配量後的 14 天。</span><span class="sxs-lookup"><span data-stu-id="64e0e-461">14 days after the last slice run.</span></span> <br/><br/><span data-ttu-id="64e0e-462">如果以 OAuth 式連結服務為基礎的配量至少每 14 天執行一次，則為 90 天。</span><span class="sxs-lookup"><span data-stu-id="64e0e-462">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="64e0e-463">如果要避免/解決此錯誤，請在**權杖到期**時使用 [授權] 按鈕重新授權，然後重新部署連結服務。</span><span class="sxs-lookup"><span data-stu-id="64e0e-463">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span></span> <span data-ttu-id="64e0e-464">您也可以如下使用程式碼，以程式設計方式產生 **sessionId** 和 **authorization** 屬性的值：</span><span class="sxs-lookup"><span data-stu-id="64e0e-464">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

<span data-ttu-id="64e0e-465">請參閱 [AzureDataLakeStoreLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)、[AzureDataLakeAnalyticsLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)和 [AuthorizationSessionGetResponse 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx)主題，以取得在程式碼中使用的 Data Factory 類別的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="64e0e-465">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span></span> <span data-ttu-id="64e0e-466">請針對 WindowsFormsWebAuthenticationDialog 類別，新增對下列項目的參考：Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll。</span><span class="sxs-lookup"><span data-stu-id="64e0e-466">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="azure-sql-linked-service"></a><span data-ttu-id="64e0e-467">Azure SQL 連結服務</span><span class="sxs-lookup"><span data-stu-id="64e0e-467">Azure SQL Linked Service</span></span>
<span data-ttu-id="64e0e-468">您可建立 Azure SQL 連結服務，並將其與 [預存程序活動](data-factory-stored-proc-activity.md) 搭配使用，以叫用 Data Factory 管線中的預存程序。</span><span class="sxs-lookup"><span data-stu-id="64e0e-468">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> <span data-ttu-id="64e0e-469">如需此連結服務的詳細資料，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#linked-service-properties) 一文。</span><span class="sxs-lookup"><span data-stu-id="64e0e-469">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse-linked-service"></a><span data-ttu-id="64e0e-470">Azure SQL 資料倉儲連結服務</span><span class="sxs-lookup"><span data-stu-id="64e0e-470">Azure SQL Data Warehouse Linked Service</span></span>
<span data-ttu-id="64e0e-471">您可以建立 Azure SQL 資料倉儲連結服務，並將其與 [預存程序活動](data-factory-stored-proc-activity.md) 搭配使用，以叫用 Data Factory 管線中的預存程序。</span><span class="sxs-lookup"><span data-stu-id="64e0e-471">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> <span data-ttu-id="64e0e-472">如需此連結服務的詳細資料，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) 一文。</span><span class="sxs-lookup"><span data-stu-id="64e0e-472">See [Azure SQL Data Warehouse Connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="sql-server-linked-service"></a><span data-ttu-id="64e0e-473">SQL Server 連結服務</span><span class="sxs-lookup"><span data-stu-id="64e0e-473">SQL Server Linked Service</span></span>
<span data-ttu-id="64e0e-474">您可以建立 SQL Server 連結服務，並將其與 [預存程序活動](data-factory-stored-proc-activity.md) 搭配使用，以叫用 Data Factory 管線中的預存程序。</span><span class="sxs-lookup"><span data-stu-id="64e0e-474">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> <span data-ttu-id="64e0e-475">如需此連結服務的詳細資料，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#linked-service-properties) 一文。</span><span class="sxs-lookup"><span data-stu-id="64e0e-475">See [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article for details about this linked service.</span></span>


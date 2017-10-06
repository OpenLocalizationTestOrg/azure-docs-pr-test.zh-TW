---
title: "Azure Data Factory 支援 aaaCompute 環境 |Microsoft 文件"
description: "深入了解您可以使用 Azure Data Factory 管線 （例如 Azure HDInsight) tootransform 或處理資料中的運算環境。"
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
ms.openlocfilehash: aba7d7de695bc1c7d475f1e741ee3b3e884151c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a><span data-ttu-id="f6a6b-103">Azure Data Factory 支援的計算環境</span><span class="sxs-lookup"><span data-stu-id="f6a6b-103">Compute environments supported by Azure Data Factory</span></span>
<span data-ttu-id="f6a6b-104">本文說明不同的運算環境，您可以使用 tooprocess 或轉換資料。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-104">This article explains different compute environments that you can use tooprocess or transform data.</span></span> <span data-ttu-id="f6a6b-105">它也提供詳細資料 （與指定 「 整合您自己） 不同的組態設定連結這些計算環境 tooan 的 Azure data factory 已連結的服務時，Data Factory 支援。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-105">It also provides details about different configurations (on-demand vs. bring your own) supported by Data Factory when configuring linked services linking these compute environments tooan Azure data factory.</span></span>

<span data-ttu-id="f6a6b-106">hello 下表提供支援的 Data Factory 和 hello 的活動可以在其上執行的運算環境的清單。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-106">hello following table provides a list of compute environments supported by Data Factory and hello activities that can run on them.</span></span> 

| <span data-ttu-id="f6a6b-107">計算環境</span><span class="sxs-lookup"><span data-stu-id="f6a6b-107">Compute environment</span></span> | <span data-ttu-id="f6a6b-108">活動</span><span class="sxs-lookup"><span data-stu-id="f6a6b-108">activities</span></span> |
| --- | --- |
| <span data-ttu-id="f6a6b-109">[隨選 HDInsight 叢集](#azure-hdinsight-on-demand-linked-service)或[您自己的 HDInsight 叢集](#azure-hdinsight-linked-service)</span><span class="sxs-lookup"><span data-stu-id="f6a6b-109">[On-demand HDInsight cluster](#azure-hdinsight-on-demand-linked-service) or [your own HDInsight cluster](#azure-hdinsight-linked-service)</span></span> |<span data-ttu-id="f6a6b-110">[DotNet](data-factory-use-custom-activities.md)、[Hive](data-factory-hive-activity.md)、[Pig](data-factory-pig-activity.md)、[MapReduce](data-factory-map-reduce.md)、[Hadoop 串流](data-factory-hadoop-streaming-activity.md)</span><span class="sxs-lookup"><span data-stu-id="f6a6b-110">[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop Streaming](data-factory-hadoop-streaming-activity.md)</span></span> |
| [<span data-ttu-id="f6a6b-111">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="f6a6b-111">Azure Batch</span></span>](#azure-batch-linked-service) |[<span data-ttu-id="f6a6b-112">DotNet</span><span class="sxs-lookup"><span data-stu-id="f6a6b-112">DotNet</span></span>](data-factory-use-custom-activities.md) |
| [<span data-ttu-id="f6a6b-113">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f6a6b-113">Azure Machine Learning</span></span>](#azure-machine-learning-linked-service) |[<span data-ttu-id="f6a6b-114">Machine Learning 活動︰批次執行和更新資源</span><span class="sxs-lookup"><span data-stu-id="f6a6b-114">Machine Learning activities: Batch Execution and Update Resource</span></span>](data-factory-azure-ml-batch-execution-activity.md) |
| [<span data-ttu-id="f6a6b-115">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f6a6b-115">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics-linked-service) |[<span data-ttu-id="f6a6b-116">Data Lake Analytics U-SQL</span><span class="sxs-lookup"><span data-stu-id="f6a6b-116">Data Lake Analytics U-SQL</span></span>](data-factory-usql-activity.md) |
| <span data-ttu-id="f6a6b-117">[Azure SQL](#azure-sql-linked-service)、[Azure SQL 資料倉儲](#azure-sql-data-warehouse-linked-service)、[SQL Server](#sql-server-linked-service)</span><span class="sxs-lookup"><span data-stu-id="f6a6b-117">[Azure SQL](#azure-sql-linked-service), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service)</span></span> |[<span data-ttu-id="f6a6b-118">預存程序</span><span class="sxs-lookup"><span data-stu-id="f6a6b-118">Stored Procedure</span></span>](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a><span data-ttu-id="f6a6b-119">Azure Data Factory 中支援的 HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="f6a6b-119">Supported HDInsight versions in Azure Data Factory</span></span>
<span data-ttu-id="f6a6b-120">Azure HDInsight 支援多個可隨時部署的 Hadoop 叢集版本。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-120">Azure HDInsight supports multiple Hadoop cluster versions that can be deployed at any time.</span></span> <span data-ttu-id="f6a6b-121">特定版本的 hello Hortonworks Data Platform (HDP) 發佈和一組包含在該發佈的元件，會建立每個版本的選擇。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-121">Each version choice creates a specific version of hello Hortonworks Data Platform (HDP) distribution and a set of components that are contained within that distribution.</span></span> <span data-ttu-id="f6a6b-122">Microsoft 會持續更新 hello HDInsight tooprovide 最新 Hadoop 生態系統的元件和修正程式的支援版本清單。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-122">Microsoft keeps updating hello list of supported versions of HDInsight tooprovide latest Hadoop ecosystem components and fixes.</span></span> <span data-ttu-id="f6a6b-123">在 2017 年 4 月 1，已被取代 hello HDInsight 3.2。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-123">hello HDInsight 3.2 is deprecated on April 1, 2017.</span></span> <span data-ttu-id="f6a6b-124">如需詳細資訊，請參閱[支援的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-124">For detailed information, see [supported HDInsight versions](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>

<span data-ttu-id="f6a6b-125">這會影響具有對 HDInsight 3.2 叢集執行活動的現有 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-125">This impacts existing Azure Data Factories that have Activities running against HDInsight 3.2 clusters.</span></span> <span data-ttu-id="f6a6b-126">我們建議使用者 toofollow hello 指導方針，在下列章節 tooupdate hello hello 受影響的 Data Factory:</span><span class="sxs-lookup"><span data-stu-id="f6a6b-126">We recommend users toofollow hello guidelines in hello following section tooupdate hello impacted Data Factories:</span></span>

### <a name="for-linked-services-pointing-tooyour-own-hdinsight-clusters"></a><span data-ttu-id="f6a6b-127">連結的服務為指向 tooyour 自己的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="f6a6b-127">For Linked Services pointing tooyour own HDInsight clusters</span></span>
* <span data-ttu-id="f6a6b-128">**指向 tooyour HDInsight 連結的服務擁有 HDInsight 3.2 或叢集如下：**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-128">**HDInsight Linked Services pointing tooyour own HDInsight 3.2 or below clusters:**</span></span>

  <span data-ttu-id="f6a6b-129">Azure Data Factory 支援自己的 HDInsight 叢集的 HDI 3.1 太正在提交作業 tooyour[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-129">Azure Data Factory supports submitting jobs tooyour own HDInsight clusters from HDI 3.1 too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span> <span data-ttu-id="f6a6b-130">不過，您可以再建立 HDInsight 3.2 叢集之後 2017 年 4 月 1，根據所述的 hello 過時原則[支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-130">However, you can no longer create HDInsight 3.2 cluster after April 1, 2017 based on hello deprecation policy documented in [supported HDInsight versions](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>  

  <span data-ttu-id="f6a6b-131">**建議：**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-131">**Recommendations:**</span></span> 
  * <span data-ttu-id="f6a6b-132">執行測試 tooensure hello 相容性的 hello 太參照此連結的服務活動都會[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)資訊記載於[Hadoop 元件適用於不同的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions)和[Hortonworks 版本資訊與 HDInsight 版本相關聯](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-132">Perform tests tooensure hello compatibility of hello Activities that reference this Linked Services too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) with information documented in [Hadoop components available with different HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) and [Hortonworks release notes associated with HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).</span></span>
  * <span data-ttu-id="f6a6b-133">升級您的 HDInsight 3.2 叢集太[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)tooget hello 最新的 Hadoop 生態系統元件和修正程式。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-133">Upgrade your HDInsight 3.2 cluster too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello latest Hadoop ecosystem components and fixes.</span></span> 

* <span data-ttu-id="f6a6b-134">**指向 tooyour HDInsight 連結的服務擁有 HDInsight 3.3 或更新版本的叢集：**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-134">**HDInsight Linked Services pointing tooyour own HDInsight 3.3 or above clusters:**</span></span>

  <span data-ttu-id="f6a6b-135">Azure Data Factory 支援自己的 HDInsight 叢集的 HDI 3.1 太正在提交作業 tooyour[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-135">Azure Data Factory supports submitting jobs tooyour own HDInsight clusters from HDI 3.1 too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span> 
  
  <span data-ttu-id="f6a6b-136">**建議：**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-136">**Recommendations:**</span></span> 
  * <span data-ttu-id="f6a6b-137">從 Data Factory 的觀點來看，不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-137">No action is required from Data Factory perspective.</span></span> <span data-ttu-id="f6a6b-138">不過，如果您是在較低版本的 HDInsight 上，我們仍建議您升級太[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)tooget hello 最新的 Hadoop 生態系統元件和修正程式。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-138">However, if you are on a lower version of HDInsight, we still recommend upgrading too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello latest Hadoop ecosystem components and fixes.</span></span>

### <a name="for-hdinsight-on-demand-linked-services"></a><span data-ttu-id="f6a6b-139">針對 HDInsight 隨選連結服務</span><span class="sxs-lookup"><span data-stu-id="f6a6b-139">For HDInsight On-Demand Linked Services</span></span>
* <span data-ttu-id="f6a6b-140">**3.2 版或以下版本是在 HDInsight 隨選連結服務 JSON 定義中指定：**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-140">**Version 3.2 or below is specified in HDInsight On-Demand Linked Services JSON definition:**</span></span>
  
  <span data-ttu-id="f6a6b-141">自 **2017/05/15** 起，Azure Data Factory 支援建立隨選 HDInsight 叢集 3.3 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-141">Azure Data Factory will support creation of On-Demand HDInsight clusters of version 3.3 or more from **05/15/2017** onwards.</span></span> <span data-ttu-id="f6a6b-142">和 hello 結束支援適用於現有連結的服務會擴充太隨 HDInsight 3.2**07/15/2017年**。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-142">And, hello end of support for existing on-demand HDInsight 3.2 linked services is extended too**07/15/2017**.</span></span>  

  <span data-ttu-id="f6a6b-143">**建議：**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-143">**Recommendations:**</span></span> 
  * <span data-ttu-id="f6a6b-144">執行測試 tooensure hello 相容性的 hello 太參照此連結的服務活動都會[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)資訊記載於[Hadoop 元件適用於不同的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions)和[Hortonworks 版本資訊與 HDInsight 版本相關聯](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-144">Perform tests tooensure hello compatibility of hello Activities that reference this Linked Services too [hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) with information documented in [Hadoop components available with different HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) and [Hortonworks release notes associated with HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).</span></span>
  * <span data-ttu-id="f6a6b-145">之前**07/15/2017年**，視 HDI 連結的服務 JSON 定義中的 hello 版本屬性更新太[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)tooget hello 最新 Hadoop 生態系統的元件和修正程式。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-145">Before **07/15/2017**, update hello Version property in On-Demand HDI Linked Service JSON definition too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello latest Hadoop ecosystem components and fixes.</span></span> <span data-ttu-id="f6a6b-146">如需詳細的 JSON 定義中，請參閱 toohello [Azure HDInsight 隨連結的服務範例](#azure-hdinsight-on-demand-linked-service)。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-146">For detailed JSON definition, refer toohello [Azure HDInsight On-Demand Linked Service sample](#azure-hdinsight-on-demand-linked-service).</span></span> 

* <span data-ttu-id="f6a6b-147">**隨選 HDInsight 連結服務中未指定的版本：**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-147">**Version not specified in On-Demand HDInsight Linked Services:**</span></span>
  
  <span data-ttu-id="f6a6b-148">自 **2017/05/15** 起，Azure Data Factory 支援建立隨選 HDInsight 叢集 3.3 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-148">Azure Data Factory will support creation of on-demand HDInsight clusters of version 3.3 or more from **05/15/2017** onwards.</span></span> <span data-ttu-id="f6a6b-149">和支援 tooexisting 隨 HDInsight 3.2 連結服務的 hello 結尾延伸太**07/15/2017年**。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-149">And, hello end of support tooexisting on-demand HDInsight 3.2 linked services is extended too**07/15/2017**.</span></span> 

  <span data-ttu-id="f6a6b-150">之前**07/15/2017年**，如果保留空白，hello 的預設值的版本與 osType 屬性：</span><span class="sxs-lookup"><span data-stu-id="f6a6b-150">Before **07/15/2017**, if left blank, hello default values for version and osType properties are:</span></span> 

  | <span data-ttu-id="f6a6b-151">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-151">Property</span></span> | <span data-ttu-id="f6a6b-152">預設值</span><span class="sxs-lookup"><span data-stu-id="f6a6b-152">Default Value</span></span> | <span data-ttu-id="f6a6b-153">必要</span><span class="sxs-lookup"><span data-stu-id="f6a6b-153">Required</span></span> |
  | --- | --- | --- |
  <span data-ttu-id="f6a6b-154">版本</span><span class="sxs-lookup"><span data-stu-id="f6a6b-154">Version</span></span>   | <span data-ttu-id="f6a6b-155">Windows 叢集為 HDI 3.1，Linux 叢集為 HDI 3.2。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-155">HDI 3.1 for Windows cluster and HDI 3.2 for Linux cluster.</span></span>| <span data-ttu-id="f6a6b-156">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-156">No</span></span>
  <span data-ttu-id="f6a6b-157">osType</span><span class="sxs-lookup"><span data-stu-id="f6a6b-157">osType</span></span> | <span data-ttu-id="f6a6b-158">hello 預設值是 Windows</span><span class="sxs-lookup"><span data-stu-id="f6a6b-158">hello default is Windows</span></span> | <span data-ttu-id="f6a6b-159">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-159">No</span></span>

  <span data-ttu-id="f6a6b-160">之後**07/15/2017年**，如果保留空白，hello 的預設值的版本與 osType 屬性：</span><span class="sxs-lookup"><span data-stu-id="f6a6b-160">After **07/15/2017**, if left blank, hello default values for version and osType properties are:</span></span>

  | <span data-ttu-id="f6a6b-161">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-161">Property</span></span> | <span data-ttu-id="f6a6b-162">預設值</span><span class="sxs-lookup"><span data-stu-id="f6a6b-162">Default Value</span></span> | <span data-ttu-id="f6a6b-163">必要</span><span class="sxs-lookup"><span data-stu-id="f6a6b-163">Required</span></span> |
  | --- | --- | --- |
  <span data-ttu-id="f6a6b-164">版本</span><span class="sxs-lookup"><span data-stu-id="f6a6b-164">Version</span></span>   | <span data-ttu-id="f6a6b-165">Windows 叢集為 HDI 3.3，Linux 叢集為 3.5。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-165">HDI 3.3 for Windows cluster and 3.5 for Linux cluster.</span></span>    | <span data-ttu-id="f6a6b-166">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-166">No</span></span>
  <span data-ttu-id="f6a6b-167">osType</span><span class="sxs-lookup"><span data-stu-id="f6a6b-167">osType</span></span> | <span data-ttu-id="f6a6b-168">hello 預設值是 Linux</span><span class="sxs-lookup"><span data-stu-id="f6a6b-168">hello default is Linux</span></span>   | <span data-ttu-id="f6a6b-169">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-169">No</span></span>

  <span data-ttu-id="f6a6b-170">**建議：**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-170">**Recommendations:**</span></span> 
  * <span data-ttu-id="f6a6b-171">之前**07/15/2017年**，執行測試 tooensure hello 相容性的 hello 太參照此連結的服務活動都會[hello 最新支援 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)記錄的資訊在[Hadoop 元件使用不同的 HDInsight 版本](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions)和[Hortonworks 版本資訊與 HDInsight 版本相關聯](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-171">Before **07/15/2017**, perform tests tooensure hello compatibility of hello Activities that reference this Linked Services too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) with information documented in [Hadoop components available with different HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) and [Hortonworks release notes associated with HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).</span></span>  
  * <span data-ttu-id="f6a6b-172">之後**07/15/2017年**，請確定您明確指定 osType 和版本值，如果您想要 toooverride hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-172">After **07/15/2017**, make sure you explicitly specify osType and version values if you would like toooverride hello default settings.</span></span> 

>[!Note]
><span data-ttu-id="f6a6b-173">目前 Azure Data Factory 不支援使用 Azure Data Lake Store 作為主要存放區的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-173">Currently Azure Data Factory does not support HDInsight clusters using Azure Data Lake Store as primary store.</span></span> <span data-ttu-id="f6a6b-174">使用 Azure 儲存體作為 HDInsight 叢集的主要存放區。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-174">Use Azure Storage as primary store for HDInsight clusters.</span></span> 
>  
>  

## <a name="on-demand-compute-environment"></a><span data-ttu-id="f6a6b-175">隨選計算環境</span><span class="sxs-lookup"><span data-stu-id="f6a6b-175">On-demand compute environment</span></span>
<span data-ttu-id="f6a6b-176">在這種設定中完全是由 hello Azure Data Factory 服務管理 hello 運算環境。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-176">In this type of configuration, hello computing environment is fully managed by hello Azure Data Factory service.</span></span> <span data-ttu-id="f6a6b-177">它會自動建立 hello Data Factory 服務作業送出的 tooprocess 資料之前，移除 hello 工作完成時。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-177">It is automatically created by hello Data Factory service before a job is submitted tooprocess data and removed when hello job is completed.</span></span> <span data-ttu-id="f6a6b-178">您可以建立 hello 隨計算環境是連結的服務、 加以設定，並控制細微作業執行，叢集管理，以及設定啟動載入動作。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-178">You can create a linked service for hello on-demand compute environment, configure it, and control granular settings for job execution, cluster management, and bootstrapping actions.</span></span>

> [!NOTE]
> <span data-ttu-id="f6a6b-179">目前的 Azure HDInsight 叢集才支援 hello 上隨選安裝設定。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-179">hello on-demand configuration is currently supported only for Azure HDInsight clusters.</span></span>
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a><span data-ttu-id="f6a6b-180">Azure HDInsight 隨選連結服務</span><span class="sxs-lookup"><span data-stu-id="f6a6b-180">Azure HDInsight On-Demand Linked Service</span></span>
<span data-ttu-id="f6a6b-181">hello Azure Data Factory 服務會自動建立 Windows/Linux 為基礎-隨選 HDInsight 叢集 tooprocess 資料。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-181">hello Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster tooprocess data.</span></span> <span data-ttu-id="f6a6b-182">hello 叢集建立在 hello 與 hello 叢集與 hello 儲存體帳戶 （hello JSON 中的 linkedServiceName 屬性） 相同的區域相關聯。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-182">hello cluster is created in hello same region as hello storage account (linkedServiceName property in hello JSON) associated with hello cluster.</span></span> <span data-ttu-id="f6a6b-183">hello 儲存體帳戶必須是一般用途的標準 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-183">hello storage account must be a general-purpose standard Azure storage account.</span></span> 

<span data-ttu-id="f6a6b-184">請注意下列 hello**重要**要點隨 HDInsight 連結服務：</span><span class="sxs-lookup"><span data-stu-id="f6a6b-184">Note hello following **important** points about on-demand HDInsight linked service:</span></span>

* <span data-ttu-id="f6a6b-185">您不會看到 hello 隨您的 Azure 訂用帳戶中建立的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-185">You do not see hello on-demand HDInsight cluster created in your Azure subscription.</span></span> <span data-ttu-id="f6a6b-186">hello Azure Data Factory 服務管理您的名義 hello 隨 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-186">hello Azure Data Factory service manages hello on-demand HDInsight cluster on your behalf.</span></span>
* <span data-ttu-id="f6a6b-187">hello 的點播 HDInsight 叢集執行的作業記錄檔複製 toohello hello HDInsight 叢集相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-187">hello logs for jobs that are run on an on-demand HDInsight cluster are copied toohello storage account associated with hello HDInsight cluster.</span></span> <span data-ttu-id="f6a6b-188">您可以從 hello hello 在 Azure 入口網站存取這些記錄檔**活動執行詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-188">You can access these logs from hello Azure portal in hello **Activity Run Details** blade.</span></span> <span data-ttu-id="f6a6b-189">如需詳細資訊，請參閱 [監視及管理管線](data-factory-monitor-manage-pipelines.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-189">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>
* <span data-ttu-id="f6a6b-190">您必須支付只 hello 時間 hello HDInsight 叢集已啟動並執行工作。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-190">You are charged only for hello time when hello HDInsight cluster is up and running jobs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6a6b-191">通常可以花**20 分鐘**或依需求的詳細 tooprovision Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-191">It typically takes **20 minutes** or more tooprovision an Azure HDInsight cluster on demand.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="f6a6b-192">範例</span><span class="sxs-lookup"><span data-stu-id="f6a6b-192">Example</span></span>
<span data-ttu-id="f6a6b-193">下列 JSON hello 定義以 Linux 為基礎的隨選 HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-193">hello following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="f6a6b-194">hello Data Factory 服務會自動建立**linux**時處理資料配量的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-194">hello Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

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

<span data-ttu-id="f6a6b-195">設定 Windows 為基礎的 HDInsight 叢集，toouse **osType**太**windows**或請勿使用 hello 屬性，因為 hello 預設值是： windows。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-195">toouse a Windows-based HDInsight cluster, set **osType** too**windows** or do not use hello property as hello default value is: windows.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="f6a6b-196">hello HDInsight 叢集建立**預設容器**hello hello JSON 中指定的 blob 儲存體中 (**linkedServiceName**)。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-196">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="f6a6b-197">HDInsight 刪除 hello 叢集時，不會刪除此容器。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-197">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="f6a6b-198">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-198">This behavior is by design.</span></span> <span data-ttu-id="f6a6b-199">HDInsight 叢集隨 HDInsight 連結服務，以建立每次配量需要處理現有的叢集即時除非 toobe (**timeToLive**) 和 hello 處理完成時刪除。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-199">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span> 
> 
> <span data-ttu-id="f6a6b-200">隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-200">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="f6a6b-201">如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-201">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="f6a6b-202">這些容器的 hello 名稱遵循模式： `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-202">hello names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="f6a6b-203">使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-203">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="f6a6b-204">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-204">Properties</span></span>
| <span data-ttu-id="f6a6b-205">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-205">Property</span></span> | <span data-ttu-id="f6a6b-206">說明</span><span class="sxs-lookup"><span data-stu-id="f6a6b-206">Description</span></span> | <span data-ttu-id="f6a6b-207">必要</span><span class="sxs-lookup"><span data-stu-id="f6a6b-207">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f6a6b-208">類型</span><span class="sxs-lookup"><span data-stu-id="f6a6b-208">type</span></span> |<span data-ttu-id="f6a6b-209">hello 類型屬性應該設定太**HDInsightOnDemand**。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-209">hello type property should be set too**HDInsightOnDemand**.</span></span> |<span data-ttu-id="f6a6b-210">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-210">Yes</span></span> |
| <span data-ttu-id="f6a6b-211">clusterSize</span><span class="sxs-lookup"><span data-stu-id="f6a6b-211">clusterSize</span></span> |<span data-ttu-id="f6a6b-212">背景工作/資料 hello 叢集中的節點數目。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-212">Number of worker/data nodes in hello cluster.</span></span> <span data-ttu-id="f6a6b-213">以及您為此屬性指定的背景工作角色節點的 hello 數目的 2 個前端節點建立 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-213">hello HDInsight cluster is created with 2 head nodes along with hello number of worker nodes you specify for this property.</span></span> <span data-ttu-id="f6a6b-214">hello 節點有大小有 4 個核心，因此 4 的背景工作節點叢集會採用 24 個核心的 Standard_D3 (4\*4 = 16 個核心的背景工作節點，再加上 2\*4 = 8 個核心的前端節點)。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-214">hello nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="f6a6b-215">請參閱[HDInsight 叢集建立 Linux Hadoop](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) hello Standard_D3 層的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-215">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about hello Standard_D3 tier.</span></span> |<span data-ttu-id="f6a6b-216">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-216">Yes</span></span> |
| <span data-ttu-id="f6a6b-217">timetolive</span><span class="sxs-lookup"><span data-stu-id="f6a6b-217">timetolive</span></span> |<span data-ttu-id="f6a6b-218">hello 允許 hello 隨選 HDInsight 叢集的閒置時間。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-218">hello allowed idle time for hello on-demand HDInsight cluster.</span></span> <span data-ttu-id="f6a6b-219">指定多久 hello 隨選 HDInsight 叢集會保持運作如果 hello 叢集中沒有其他作用中的工作執行的活動完成後。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-219">Specifies how long hello on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in hello cluster.</span></span><br/><br/><span data-ttu-id="f6a6b-220">例如，如果在 6 分鐘和 timetolive 執行的活動是設定 too5 分鐘，hello 叢集會保持運作 5 分鐘之後 hello 6 分鐘處理 hello 活動執行。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-220">For example, if an activity run takes 6 minutes and timetolive is set too5 minutes, hello cluster stays alive for 5 minutes after hello 6 minutes of processing hello activity run.</span></span> <span data-ttu-id="f6a6b-221">如果另一個執行的活動與 hello 6 分鐘內視窗執行時，處理 hello 相同叢集中。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-221">If another activity run is executed with hello 6-minutes window, it is processed by hello same cluster.</span></span><br/><br/><span data-ttu-id="f6a6b-222">建立隨選 HDInsight 叢集是昂貴的作業 （可能需要一些時間），因此使用這項設定的 data factory 所需的 tooimprove 效能重複使用隨選 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-222">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed tooimprove performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="f6a6b-223">如果您設定 timetolive 值 too0，hello 活動執行完成時，會刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-223">If you set timetolive value too0, hello cluster is deleted as soon as hello activity run completes.</span></span> <span data-ttu-id="f6a6b-224">不過，如果您設定較高的值，hello 叢集可能會維持閒置的不必要地產生高成本。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-224">Whereas, if you set a high value, hello cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="f6a6b-225">因此，很重要，您會設定 hello 適當的值，根據您的需求。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-225">Therefore, it is important that you set hello appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="f6a6b-226">適當地設定 hello timetolive 屬性值，如果多個管線可以共用 hello hello 隨選 HDInsight 叢集執行個體。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-226">If hello timetolive property value is appropriately set, multiple pipelines can share hello instance of hello on-demand HDInsight cluster.</span></span>  |<span data-ttu-id="f6a6b-227">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-227">Yes</span></span> |
| <span data-ttu-id="f6a6b-228">版本</span><span class="sxs-lookup"><span data-stu-id="f6a6b-228">version</span></span> |<span data-ttu-id="f6a6b-229">Hello HDInsight 叢集的版本。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-229">Version of hello HDInsight cluster.</span></span> <span data-ttu-id="f6a6b-230">hello 預設值是 Windows 叢集的 3.1 和 3.2 for Linux 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-230">hello default value is 3.1 for Windows cluster and 3.2 for Linux cluster.</span></span> |<span data-ttu-id="f6a6b-231">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-231">No</span></span> |
| <span data-ttu-id="f6a6b-232">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f6a6b-232">linkedServiceName</span></span> | <span data-ttu-id="f6a6b-233">Azure 儲存體連結服務 toobe hello 視叢集使用的儲存及處理資料。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-233">Azure Storage linked service toobe used by hello on-demand cluster for storing and processing data.</span></span> <span data-ttu-id="f6a6b-234">hello HDInsight 叢集建立在 hello 相同與此 Azure 儲存體帳戶的區域。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-234">hello HDInsight cluster is created in hello same region as this Azure Storage account.</span></span><p><span data-ttu-id="f6a6b-235">目前，您無法建立使用 Azure 資料湖存放區為 hello 存放裝置的隨 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-235">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as hello storage.</span></span> <span data-ttu-id="f6a6b-236">如果您想要從 HDInsight 處理 Azure 資料湖存放區中的 toostore hello 結果資料，請使用 hello Azure Blob 儲存體 toohello Azure Data Lake Store 複製活動 toocopy hello 資料。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-236">If you want toostore hello result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity toocopy hello data from hello Azure Blob Storage toohello Azure Data Lake Store.</span></span> </p>  | <span data-ttu-id="f6a6b-237">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-237">Yes</span></span> |
| <span data-ttu-id="f6a6b-238">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="f6a6b-238">additionalLinkedServiceNames</span></span> |<span data-ttu-id="f6a6b-239">指定額外的儲存體帳戶的 hello HDInsight 連結服務，以便 hello Data Factory 服務可以代表您註冊它們。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-239">Specifies additional storage accounts for hello HDInsight linked service so that hello Data Factory service can register them on your behalf.</span></span> <span data-ttu-id="f6a6b-240">這些儲存體帳戶必須在 hello 與 hello HDInsight 叢集，這是在 hello 相同相同的區域與 hello linkedServiceName 所指定的儲存體帳戶的區域。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-240">These storage accounts must be in hello same region as hello HDInsight cluster, which is created in hello same region as hello storage account specified by linkedServiceName.</span></span> |<span data-ttu-id="f6a6b-241">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-241">No</span></span> |
| <span data-ttu-id="f6a6b-242">osType</span><span class="sxs-lookup"><span data-stu-id="f6a6b-242">osType</span></span> |<span data-ttu-id="f6a6b-243">作業系統的類型。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-243">Type of operating system.</span></span> <span data-ttu-id="f6a6b-244">允許的值為：Windows (預設值) 和 linux</span><span class="sxs-lookup"><span data-stu-id="f6a6b-244">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="f6a6b-245">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-245">No</span></span> |
| <span data-ttu-id="f6a6b-246">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f6a6b-246">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="f6a6b-247">該點 toohello HCatalog 資料庫服務的 Azure SQL 連結的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-247">hello name of Azure SQL linked service that point toohello HCatalog database.</span></span> <span data-ttu-id="f6a6b-248">hello 隨選 HDInsight 叢集會建立使用 hello Azure SQL database 當做 hello 中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-248">hello on-demand HDInsight cluster is created by using hello Azure SQL database as hello metastore.</span></span> |<span data-ttu-id="f6a6b-249">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-249">No</span></span> |

#### <a name="additionallinkedservicenames-json-example"></a><span data-ttu-id="f6a6b-250">additionalLinkedServiceNames JSON 範例</span><span class="sxs-lookup"><span data-stu-id="f6a6b-250">additionalLinkedServiceNames JSON example</span></span>

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a><span data-ttu-id="f6a6b-251">進階屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-251">Advanced Properties</span></span>
<span data-ttu-id="f6a6b-252">您也可以指定 hello hello 細微 hello 隨選 HDInsight 叢集組態的下列屬性。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-252">You can also specify hello following properties for hello granular configuration of hello on-demand HDInsight cluster.</span></span>

| <span data-ttu-id="f6a6b-253">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-253">Property</span></span> | <span data-ttu-id="f6a6b-254">說明</span><span class="sxs-lookup"><span data-stu-id="f6a6b-254">Description</span></span> | <span data-ttu-id="f6a6b-255">必要</span><span class="sxs-lookup"><span data-stu-id="f6a6b-255">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f6a6b-256">coreConfiguration</span><span class="sxs-lookup"><span data-stu-id="f6a6b-256">coreConfiguration</span></span> |<span data-ttu-id="f6a6b-257">指定建立 hello HDInsight 叢集 toobe hello 核心組態參數 （如 core-site.xml 所示）。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-257">Specifies hello core configuration parameters (as in core-site.xml) for hello HDInsight cluster toobe created.</span></span> |<span data-ttu-id="f6a6b-258">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-258">No</span></span> |
| <span data-ttu-id="f6a6b-259">hBaseConfiguration</span><span class="sxs-lookup"><span data-stu-id="f6a6b-259">hBaseConfiguration</span></span> |<span data-ttu-id="f6a6b-260">指定 hello HBase 組態參數 (hbase-site.xml) hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-260">Specifies hello HBase configuration parameters (hbase-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="f6a6b-261">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-261">No</span></span> |
| <span data-ttu-id="f6a6b-262">hdfsConfiguration</span><span class="sxs-lookup"><span data-stu-id="f6a6b-262">hdfsConfiguration</span></span> |<span data-ttu-id="f6a6b-263">指定 hello HDFS 組態參數 (hdfs-site.xml) hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-263">Specifies hello HDFS configuration parameters (hdfs-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="f6a6b-264">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-264">No</span></span> |
| <span data-ttu-id="f6a6b-265">hiveConfiguration</span><span class="sxs-lookup"><span data-stu-id="f6a6b-265">hiveConfiguration</span></span> |<span data-ttu-id="f6a6b-266">指定 hello hive 組態參數 (hive-site.xml) hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-266">Specifies hello hive configuration parameters (hive-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="f6a6b-267">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-267">No</span></span> |
| <span data-ttu-id="f6a6b-268">mapReduceConfiguration</span><span class="sxs-lookup"><span data-stu-id="f6a6b-268">mapReduceConfiguration</span></span> |<span data-ttu-id="f6a6b-269">指定 hello MapReduce 組態參數 (mapred-site.xml) hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-269">Specifies hello MapReduce configuration parameters (mapred-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="f6a6b-270">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-270">No</span></span> |
| <span data-ttu-id="f6a6b-271">oozieConfiguration</span><span class="sxs-lookup"><span data-stu-id="f6a6b-271">oozieConfiguration</span></span> |<span data-ttu-id="f6a6b-272">指定 hello Oozie 組態參數 (oozie-site.xml) hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-272">Specifies hello Oozie configuration parameters (oozie-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="f6a6b-273">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-273">No</span></span> |
| <span data-ttu-id="f6a6b-274">stormConfiguration</span><span class="sxs-lookup"><span data-stu-id="f6a6b-274">stormConfiguration</span></span> |<span data-ttu-id="f6a6b-275">指定 hello Storm 組態參數 (storm-site.xml) hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-275">Specifies hello Storm configuration parameters (storm-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="f6a6b-276">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-276">No</span></span> |
| <span data-ttu-id="f6a6b-277">yarnConfiguration</span><span class="sxs-lookup"><span data-stu-id="f6a6b-277">yarnConfiguration</span></span> |<span data-ttu-id="f6a6b-278">指定 hello Yarn 組態參數 (yarn-site.xml) hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-278">Specifies hello Yarn configuration parameters (yarn-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="f6a6b-279">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-279">No</span></span> |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a><span data-ttu-id="f6a6b-280">範例 – 包含進階屬性的隨選 HDInsight 叢集組態</span><span class="sxs-lookup"><span data-stu-id="f6a6b-280">Example – On-demand HDInsight cluster configuration with advanced properties</span></span>

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

### <a name="node-sizes"></a><span data-ttu-id="f6a6b-281">節點大小</span><span class="sxs-lookup"><span data-stu-id="f6a6b-281">Node sizes</span></span>
<span data-ttu-id="f6a6b-282">您可以指定標頭、 資料和動物園管理員的節點，使用下列屬性的 hello hello 的大小：</span><span class="sxs-lookup"><span data-stu-id="f6a6b-282">You can specify hello sizes of head, data, and zookeeper nodes using hello following properties:</span></span> 

| <span data-ttu-id="f6a6b-283">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-283">Property</span></span> | <span data-ttu-id="f6a6b-284">說明</span><span class="sxs-lookup"><span data-stu-id="f6a6b-284">Description</span></span> | <span data-ttu-id="f6a6b-285">必要</span><span class="sxs-lookup"><span data-stu-id="f6a6b-285">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f6a6b-286">headNodeSize</span><span class="sxs-lookup"><span data-stu-id="f6a6b-286">headNodeSize</span></span> |<span data-ttu-id="f6a6b-287">指定 hello hello 前端節點大小。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-287">Specifies hello size of hello head node.</span></span> <span data-ttu-id="f6a6b-288">hello 預設值是： Standard_D3。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-288">hello default value is: Standard_D3.</span></span> <span data-ttu-id="f6a6b-289">請參閱 hello**指定節點大小**如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-289">See hello **Specifying node sizes** section for details.</span></span> |<span data-ttu-id="f6a6b-290">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-290">No</span></span> |
| <span data-ttu-id="f6a6b-291">dataNodeSize</span><span class="sxs-lookup"><span data-stu-id="f6a6b-291">dataNodeSize</span></span> |<span data-ttu-id="f6a6b-292">指定 hello 大小 hello 資料節點。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-292">Specifies hello size of hello data node.</span></span> <span data-ttu-id="f6a6b-293">hello 預設值是： Standard_D3。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-293">hello default value is: Standard_D3.</span></span> |<span data-ttu-id="f6a6b-294">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-294">No</span></span> |
| <span data-ttu-id="f6a6b-295">zookeeperNodeSize</span><span class="sxs-lookup"><span data-stu-id="f6a6b-295">zookeeperNodeSize</span></span> |<span data-ttu-id="f6a6b-296">指定 hello 大小 hello Zoo 持有者節點。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-296">Specifies hello size of hello Zoo Keeper node.</span></span> <span data-ttu-id="f6a6b-297">hello 預設值是： Standard_D3。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-297">hello default value is: Standard_D3.</span></span> |<span data-ttu-id="f6a6b-298">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-298">No</span></span> |

#### <a name="specifying-node-sizes"></a><span data-ttu-id="f6a6b-299">指定節點大小</span><span class="sxs-lookup"><span data-stu-id="f6a6b-299">Specifying node sizes</span></span>
<span data-ttu-id="f6a6b-300">請參閱 hello[虛擬機器的大小](../virtual-machines/linux/sizes.md)發行項的字串值，您需要 toospecify hello hello 前一節中所述的屬性。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-300">See hello [Sizes of Virtual Machines](../virtual-machines/linux/sizes.md) article for string values you need toospecify for hello properties mentioned in hello previous section.</span></span> <span data-ttu-id="f6a6b-301">hello 值需要 tooconform toohello**指令程式 （& s) API** hello 文件中參考。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-301">hello values need tooconform toohello **CMDLETs & APIS** referenced in hello article.</span></span> <span data-ttu-id="f6a6b-302">您可以看到 hello 文件中，大型 （預設值） 大小的 hello 資料節點有 7 GB 記憶體，但這不是適用於您的案例。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-302">As you can see in hello article, hello data node of Large (default) size has 7-GB memory, which may not be good enough for your scenario.</span></span> 

<span data-ttu-id="f6a6b-303">如果您想 toocreate D4 大小前端節點和背景工作節點，請指定**Standard_D4**為 hello headNodeSize 和 dataNodeSize 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-303">If you want toocreate D4 sized head nodes and worker nodes, specify **Standard_D4** as hello value for headNodeSize and dataNodeSize properties.</span></span> 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

<span data-ttu-id="f6a6b-304">如果您指定這些屬性的值錯誤時，您可能會收到 hello 下列**錯誤：**失敗 toocreate 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-304">If you specify a wrong value for these properties, you may receive hello following **error:** Failed toocreate cluster.</span></span> <span data-ttu-id="f6a6b-305">例外狀況： 無法 toocomplete hello 叢集建立作業。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-305">Exception: Unable toocomplete hello cluster create operation.</span></span> <span data-ttu-id="f6a6b-306">作業失敗，錯誤碼為 '400'。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-306">Operation failed with code '400'.</span></span> <span data-ttu-id="f6a6b-307">叢集剩餘狀態：「錯誤」。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-307">Cluster left behind state: 'Error'.</span></span> <span data-ttu-id="f6a6b-308">訊息：「PreClusterCreationValidationFailure」。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-308">Message: 'PreClusterCreationValidationFailure'.</span></span> <span data-ttu-id="f6a6b-309">當您收到這個錯誤時，請確定您使用 hello**指令程式 （& s) API** hello hello 表格名稱[虛擬機器的大小](../virtual-machines/linux/sizes.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-309">When you receive this error, ensure that you are using hello **CMDLET & APIS** name from hello table in hello [Sizes of Virtual Machines](../virtual-machines/linux/sizes.md) article.</span></span>  

## <a name="bring-your-own-compute-environment"></a><span data-ttu-id="f6a6b-310">自備計算環境</span><span class="sxs-lookup"><span data-stu-id="f6a6b-310">Bring your own compute environment</span></span>
<span data-ttu-id="f6a6b-311">在這種組態中，使用者可以將現有的運算環境註冊為 Data Factory 中的連結服務。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-311">In this type of configuration, users can register an already existing computing environment as a linked service in Data Factory.</span></span> <span data-ttu-id="f6a6b-312">hello 運算環境是由管理 hello 使用者並 hello Data Factory 服務會使用它 tooexecute hello 活動。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-312">hello computing environment is managed by hello user and hello Data Factory service uses it tooexecute hello activities.</span></span>

<span data-ttu-id="f6a6b-313">Hello 下列計算環境支援這種設定：</span><span class="sxs-lookup"><span data-stu-id="f6a6b-313">This type of configuration is supported for hello following compute environments:</span></span>

* <span data-ttu-id="f6a6b-314">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f6a6b-314">Azure HDInsight</span></span>
* <span data-ttu-id="f6a6b-315">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="f6a6b-315">Azure Batch</span></span>
* <span data-ttu-id="f6a6b-316">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f6a6b-316">Azure Machine Learning</span></span>
* <span data-ttu-id="f6a6b-317">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f6a6b-317">Azure Data Lake Analytics</span></span>
* <span data-ttu-id="f6a6b-318">Azure SQL DB、Azure SQL DW、SQL Server</span><span class="sxs-lookup"><span data-stu-id="f6a6b-318">Azure SQL DB, Azure SQL DW, SQL Server</span></span>

## <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="f6a6b-319">Azure HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="f6a6b-319">Azure HDInsight Linked Service</span></span>
<span data-ttu-id="f6a6b-320">您可以使用 Data Factory 建立 Azure HDInsight 連結服務 tooregister HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-320">You can create an Azure HDInsight linked service tooregister your own HDInsight cluster with Data Factory.</span></span>

### <a name="example"></a><span data-ttu-id="f6a6b-321">範例</span><span class="sxs-lookup"><span data-stu-id="f6a6b-321">Example</span></span>

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

### <a name="properties"></a><span data-ttu-id="f6a6b-322">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-322">Properties</span></span>
| <span data-ttu-id="f6a6b-323">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-323">Property</span></span> | <span data-ttu-id="f6a6b-324">說明</span><span class="sxs-lookup"><span data-stu-id="f6a6b-324">Description</span></span> | <span data-ttu-id="f6a6b-325">必要</span><span class="sxs-lookup"><span data-stu-id="f6a6b-325">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f6a6b-326">類型</span><span class="sxs-lookup"><span data-stu-id="f6a6b-326">type</span></span> |<span data-ttu-id="f6a6b-327">hello 類型屬性應該設定太**HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-327">hello type property should be set too**HDInsight**.</span></span> |<span data-ttu-id="f6a6b-328">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-328">Yes</span></span> |
| <span data-ttu-id="f6a6b-329">clusterUri</span><span class="sxs-lookup"><span data-stu-id="f6a6b-329">clusterUri</span></span> |<span data-ttu-id="f6a6b-330">hello hello HDInsight 叢集的 URI。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-330">hello URI of hello HDInsight cluster.</span></span> |<span data-ttu-id="f6a6b-331">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-331">Yes</span></span> |
| <span data-ttu-id="f6a6b-332">username</span><span class="sxs-lookup"><span data-stu-id="f6a6b-332">username</span></span> |<span data-ttu-id="f6a6b-333">指定的 hello 使用者 toobe hello 名稱使用 tooconnect tooan 現有 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-333">Specify hello name of hello user toobe used tooconnect tooan existing HDInsight cluster.</span></span> |<span data-ttu-id="f6a6b-334">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-334">Yes</span></span> |
| <span data-ttu-id="f6a6b-335">password</span><span class="sxs-lookup"><span data-stu-id="f6a6b-335">password</span></span> |<span data-ttu-id="f6a6b-336">指定 hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-336">Specify password for hello user account.</span></span> |<span data-ttu-id="f6a6b-337">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-337">Yes</span></span> |
| <span data-ttu-id="f6a6b-338">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f6a6b-338">linkedServiceName</span></span> | <span data-ttu-id="f6a6b-339">Hello HDInsight 叢集供 hello 參照 toohello Azure blob 儲存體的 Azure 儲存體連結服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-339">Name of hello Azure Storage linked service that refers toohello Azure blob storage used by hello HDInsight cluster.</span></span> <p><span data-ttu-id="f6a6b-340">目前，您無法針對此屬性指定 Azure Data Lake Store 連結服務。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-340">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="f6a6b-341">如果 hello HDInsight 叢集已存取 toohello 資料湖存放區，您可能會從 Hive/Pig 指令碼來存取 hello Azure 資料湖存放區中的資料。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-341">If hello HDInsight cluster has access toohello Data Lake Store, you may access data in hello Azure Data Lake Store from Hive/Pig scripts.</span></span> </p>  |<span data-ttu-id="f6a6b-342">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-342">Yes</span></span> |

## <a name="azure-batch-linked-service"></a><span data-ttu-id="f6a6b-343">Azure Batch 連結服務</span><span class="sxs-lookup"><span data-stu-id="f6a6b-343">Azure Batch Linked Service</span></span>
<span data-ttu-id="f6a6b-344">您可以建立 Azure 批次連結服務 tooregister 批次集區的虛擬機器 (Vm) tooa data factory。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-344">You can create an Azure Batch linked service tooregister a Batch pool of virtual machines (VMs) tooa data factory.</span></span> <span data-ttu-id="f6a6b-345">您可以使用 Azure Batch 或 Azure HDInsight 執行 .NET 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-345">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span>

<span data-ttu-id="f6a6b-346">請參閱下列主題，如果您是新 tooAzure 批次服務：</span><span class="sxs-lookup"><span data-stu-id="f6a6b-346">See following topics if you are new tooAzure Batch service:</span></span>

* <span data-ttu-id="f6a6b-347">[Azure 批次的基本概念](../batch/batch-technical-overview.md)hello Azure 批次服務的概觀。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-347">[Azure Batch basics](../batch/batch-technical-overview.md) for an overview of hello Azure Batch service.</span></span>
* <span data-ttu-id="f6a6b-348">[新 AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) cmdlet toocreate Azure Batch 帳戶 （或） [Azure 入口網站](../batch/batch-account-create-portal.md)toocreate hello Azure Batch 帳戶使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-348">[New-AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) cmdlet toocreate an Azure Batch account (or) [Azure portal](../batch/batch-account-create-portal.md) toocreate hello Azure Batch account using Azure portal.</span></span> <span data-ttu-id="f6a6b-349">請參閱[使用 PowerShell toomanage Azure Batch 帳戶](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx)主題，如需使用 hello cmdlet 的詳細指示。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-349">See [Using PowerShell toomanage Azure Batch Account](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) topic for detailed instructions on using hello cmdlet.</span></span>
* <span data-ttu-id="f6a6b-350">[新 AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet toocreate Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-350">[New-AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet toocreate an Azure Batch pool.</span></span>

### <a name="example"></a><span data-ttu-id="f6a6b-351">範例</span><span class="sxs-lookup"><span data-stu-id="f6a6b-351">Example</span></span>

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

<span data-ttu-id="f6a6b-352">附加"**。\<區域名稱\>**"toohello 您的批次帳戶名稱 hello **accountName**屬性。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-352">Append "**.\<region name\>**" toohello name of your batch account for hello **accountName** property.</span></span> <span data-ttu-id="f6a6b-353">範例：</span><span class="sxs-lookup"><span data-stu-id="f6a6b-353">Example:</span></span>

```json
"accountName": "mybatchaccount.eastus"
```

<span data-ttu-id="f6a6b-354">另一個選項是 tooprovide hello batchUri 端點 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f6a6b-354">Another option is tooprovide hello batchUri endpoint as shown in hello following sample:</span></span>

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a><span data-ttu-id="f6a6b-355">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-355">Properties</span></span>
| <span data-ttu-id="f6a6b-356">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-356">Property</span></span> | <span data-ttu-id="f6a6b-357">說明</span><span class="sxs-lookup"><span data-stu-id="f6a6b-357">Description</span></span> | <span data-ttu-id="f6a6b-358">必要</span><span class="sxs-lookup"><span data-stu-id="f6a6b-358">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f6a6b-359">類型</span><span class="sxs-lookup"><span data-stu-id="f6a6b-359">type</span></span> |<span data-ttu-id="f6a6b-360">hello 類型屬性應該設定太**AzureBatch**。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-360">hello type property should be set too**AzureBatch**.</span></span> |<span data-ttu-id="f6a6b-361">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-361">Yes</span></span> |
| <span data-ttu-id="f6a6b-362">accountName</span><span class="sxs-lookup"><span data-stu-id="f6a6b-362">accountName</span></span> |<span data-ttu-id="f6a6b-363">Hello Azure Batch 帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-363">Name of hello Azure Batch account.</span></span> |<span data-ttu-id="f6a6b-364">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-364">Yes</span></span> |
| <span data-ttu-id="f6a6b-365">accessKey</span><span class="sxs-lookup"><span data-stu-id="f6a6b-365">accessKey</span></span> |<span data-ttu-id="f6a6b-366">Hello Azure Batch 帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-366">Access key for hello Azure Batch account.</span></span> |<span data-ttu-id="f6a6b-367">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-367">Yes</span></span> |
| <span data-ttu-id="f6a6b-368">poolName</span><span class="sxs-lookup"><span data-stu-id="f6a6b-368">poolName</span></span> |<span data-ttu-id="f6a6b-369">Hello 集區的虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-369">Name of hello pool of virtual machines.</span></span> |<span data-ttu-id="f6a6b-370">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-370">Yes</span></span> |
| <span data-ttu-id="f6a6b-371">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f6a6b-371">linkedServiceName</span></span> |<span data-ttu-id="f6a6b-372">Hello 與此 Azure Batch 連結服務相關聯的 Azure 儲存體連結服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-372">Name of hello Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="f6a6b-373">這項連結的服務用於暫存檔案需要 toorun hello 活動與 hello 活動執行記錄的儲存。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-373">This linked service is used for staging files required toorun hello activity and storing hello activity execution logs.</span></span> |<span data-ttu-id="f6a6b-374">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-374">Yes</span></span> |

## <a name="azure-machine-learning-linked-service"></a><span data-ttu-id="f6a6b-375">Azure Machine Learning 連結服務</span><span class="sxs-lookup"><span data-stu-id="f6a6b-375">Azure Machine Learning Linked Service</span></span>
<span data-ttu-id="f6a6b-376">建立 Azure Machine Learning 連結服務 tooregister Machine Learning 批次計分端點 tooa 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-376">You create an Azure Machine Learning linked service tooregister a Machine Learning batch scoring endpoint tooa data factory.</span></span>

### <a name="example"></a><span data-ttu-id="f6a6b-377">範例</span><span class="sxs-lookup"><span data-stu-id="f6a6b-377">Example</span></span>

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

### <a name="properties"></a><span data-ttu-id="f6a6b-378">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-378">Properties</span></span>
| <span data-ttu-id="f6a6b-379">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-379">Property</span></span> | <span data-ttu-id="f6a6b-380">說明</span><span class="sxs-lookup"><span data-stu-id="f6a6b-380">Description</span></span> | <span data-ttu-id="f6a6b-381">必要</span><span class="sxs-lookup"><span data-stu-id="f6a6b-381">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f6a6b-382">類型</span><span class="sxs-lookup"><span data-stu-id="f6a6b-382">Type</span></span> |<span data-ttu-id="f6a6b-383">hello 類型屬性應該設定為： **AzureML**。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-383">hello type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="f6a6b-384">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-384">Yes</span></span> |
| <span data-ttu-id="f6a6b-385">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="f6a6b-385">mlEndpoint</span></span> |<span data-ttu-id="f6a6b-386">hello 批次評分 URL。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-386">hello batch scoring URL.</span></span> |<span data-ttu-id="f6a6b-387">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-387">Yes</span></span> |
| <span data-ttu-id="f6a6b-388">apiKey</span><span class="sxs-lookup"><span data-stu-id="f6a6b-388">apiKey</span></span> |<span data-ttu-id="f6a6b-389">hello 發行工作區模型的 API。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-389">hello published workspace model’s API.</span></span> |<span data-ttu-id="f6a6b-390">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-390">Yes</span></span> |

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="f6a6b-391">Azure Data Lake Analytics 連結服務</span><span class="sxs-lookup"><span data-stu-id="f6a6b-391">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="f6a6b-392">您建立**Azure Data Lake Analytics**連結服務 toolink Azure Data Lake Analytics 計算服務 tooan Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-392">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory.</span></span> <span data-ttu-id="f6a6b-393">hello hello 管線中的資料 Lake Analytics U-SQL 活動指的是 toothis 連結服務。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-393">hello Data Lake Analytics U-SQL activity in hello pipeline refers toothis linked service.</span></span> 

<span data-ttu-id="f6a6b-394">hello 下表提供說明 hello hello JSON 定義中使用的一般內容。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-394">hello following table provides descriptions for hello generic properties used in hello JSON definition.</span></span> <span data-ttu-id="f6a6b-395">您可以在服務主體與使用者認證驗證之間進一步選擇。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-395">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="f6a6b-396">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-396">Property</span></span> | <span data-ttu-id="f6a6b-397">說明</span><span class="sxs-lookup"><span data-stu-id="f6a6b-397">Description</span></span> | <span data-ttu-id="f6a6b-398">必要</span><span class="sxs-lookup"><span data-stu-id="f6a6b-398">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f6a6b-399">**type**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-399">**type**</span></span> |<span data-ttu-id="f6a6b-400">hello 類型屬性應該設定為： **AzureDataLakeAnalytics**。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-400">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="f6a6b-401">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-401">Yes</span></span> |
| <span data-ttu-id="f6a6b-402">**accountName**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-402">**accountName**</span></span> |<span data-ttu-id="f6a6b-403">Azure Data Lake Analytics 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-403">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="f6a6b-404">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-404">Yes</span></span> |
| <span data-ttu-id="f6a6b-405">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-405">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="f6a6b-406">Azure Data Lake Analytics URI。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-406">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="f6a6b-407">否</span><span class="sxs-lookup"><span data-stu-id="f6a6b-407">No</span></span> |
| <span data-ttu-id="f6a6b-408">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-408">**subscriptionId**</span></span> |<span data-ttu-id="f6a6b-409">Azure 訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="f6a6b-409">Azure subscription id</span></span> |<span data-ttu-id="f6a6b-410">否 （如果未指定，訂用帳戶的資料處理站可用的 hello）。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-410">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="f6a6b-411">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-411">**resourceGroupName**</span></span> |<span data-ttu-id="f6a6b-412">Azure 資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="f6a6b-412">Azure resource group name</span></span> |<span data-ttu-id="f6a6b-413">否 （如果未指定，資源群組的資料處理站可用的 hello）。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-413">No (If not specified, resource group of hello data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="f6a6b-414">服務主體驗證 (建議)</span><span class="sxs-lookup"><span data-stu-id="f6a6b-414">Service principal authentication (recommended)</span></span>
<span data-ttu-id="f6a6b-415">服務主體驗證 toouse，註冊在 Azure Active Directory (Azure AD) 和授與它 hello 應用程式的實體存取 tooData 湖存放區。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-415">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="f6a6b-416">如需詳細的步驟，請參閱[服務對服務驗證](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-416">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="f6a6b-417">請記下的下列值，您使用的 hello toodefine hello 連結服務：</span><span class="sxs-lookup"><span data-stu-id="f6a6b-417">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="f6a6b-418">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="f6a6b-418">Application ID</span></span>
* <span data-ttu-id="f6a6b-419">應用程式金鑰</span><span class="sxs-lookup"><span data-stu-id="f6a6b-419">Application key</span></span> 
* <span data-ttu-id="f6a6b-420">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="f6a6b-420">Tenant ID</span></span>

<span data-ttu-id="f6a6b-421">您可以使用服務主體的驗證方法是指定 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="f6a6b-421">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="f6a6b-422">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-422">Property</span></span> | <span data-ttu-id="f6a6b-423">說明</span><span class="sxs-lookup"><span data-stu-id="f6a6b-423">Description</span></span> | <span data-ttu-id="f6a6b-424">必要</span><span class="sxs-lookup"><span data-stu-id="f6a6b-424">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f6a6b-425">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-425">**servicePrincipalId**</span></span> | <span data-ttu-id="f6a6b-426">指定 hello 應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-426">Specify hello application's client ID.</span></span> | <span data-ttu-id="f6a6b-427">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-427">Yes</span></span> |
| <span data-ttu-id="f6a6b-428">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-428">**servicePrincipalKey**</span></span> | <span data-ttu-id="f6a6b-429">指定 hello 應用程式的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-429">Specify hello application's key.</span></span> | <span data-ttu-id="f6a6b-430">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-430">Yes</span></span> |
| <span data-ttu-id="f6a6b-431">**tenant**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-431">**tenant**</span></span> | <span data-ttu-id="f6a6b-432">指定在您的應用程式所在的 hello 租用戶資訊 (網域名稱或租用戶 ID)。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-432">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="f6a6b-433">您可以透過暫留在 hello 右上角的 hello Azure 入口網站中的 hello 滑鼠擷取它。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-433">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="f6a6b-434">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-434">Yes</span></span> |

<span data-ttu-id="f6a6b-435">**範例：服務主體驗證**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-435">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="f6a6b-436">使用者認證驗證</span><span class="sxs-lookup"><span data-stu-id="f6a6b-436">User credential authentication</span></span>
<span data-ttu-id="f6a6b-437">或者，您可以使用使用者認證驗證的 Data Lake Analytics 藉由指定下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="f6a6b-437">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying hello following properties:</span></span>

| <span data-ttu-id="f6a6b-438">屬性</span><span class="sxs-lookup"><span data-stu-id="f6a6b-438">Property</span></span> | <span data-ttu-id="f6a6b-439">說明</span><span class="sxs-lookup"><span data-stu-id="f6a6b-439">Description</span></span> | <span data-ttu-id="f6a6b-440">必要</span><span class="sxs-lookup"><span data-stu-id="f6a6b-440">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f6a6b-441">**authorization**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-441">**authorization**</span></span> | <span data-ttu-id="f6a6b-442">按一下 hello**授權**按鈕 hello Data Factory 編輯器中，並輸入您 hello 自動產生的授權 URL toothis 屬性指派的認證。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-442">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="f6a6b-443">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-443">Yes</span></span> |
| <span data-ttu-id="f6a6b-444">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-444">**sessionId**</span></span> | <span data-ttu-id="f6a6b-445">從 hello OAuth 授權工作階段的 OAuth 工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-445">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="f6a6b-446">每個工作階段識別碼都是唯一的，只能使用一次。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-446">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="f6a6b-447">當您使用 hello Data Factory 編輯器時，此設定會自動產生。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-447">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="f6a6b-448">是</span><span class="sxs-lookup"><span data-stu-id="f6a6b-448">Yes</span></span> |

<span data-ttu-id="f6a6b-449">**範例：使用者認證授權**</span><span class="sxs-lookup"><span data-stu-id="f6a6b-449">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="f6a6b-450">權杖到期</span><span class="sxs-lookup"><span data-stu-id="f6a6b-450">Token expiration</span></span>
<span data-ttu-id="f6a6b-451">hello 您使用 hello 所產生的授權碼**授權**一段時間後到期 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-451">hello authorization code you generated by using hello **Authorize** button expires after sometime.</span></span> <span data-ttu-id="f6a6b-452">請參閱下表針對不同類型的使用者帳戶的 hello 逾期時間的 hello。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-452">See hello following table for hello expiration times for different types of user accounts.</span></span> <span data-ttu-id="f6a6b-453">您可能會看到下列錯誤訊息的 hello 當 hello 驗證**權杖到期**： 認證作業發生錯誤： invalid_grant-AADSTS70002： 驗證認證時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-453">You may see hello following error message when hello authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="f6a6b-454">AADSTS70008: hello 提供存取權限已過期或撤銷。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-454">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="f6a6b-455">追蹤識別碼：d18629e8-af88-43c5-88e3-d8419eb1fca1 相互關連識別碼：fac30a0c-6be6-4e02-8d69-a776d2ffefd7 時間戳記：2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="f6a6b-455">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="f6a6b-456">使用者類型</span><span class="sxs-lookup"><span data-stu-id="f6a6b-456">User type</span></span> | <span data-ttu-id="f6a6b-457">到期時間</span><span class="sxs-lookup"><span data-stu-id="f6a6b-457">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="f6a6b-458">不受 Azure Active Directory 管理的使用者帳戶 (@hotmail.com、@live.com 等)</span><span class="sxs-lookup"><span data-stu-id="f6a6b-458">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="f6a6b-459">12 小時</span><span class="sxs-lookup"><span data-stu-id="f6a6b-459">12 hours</span></span> |
| <span data-ttu-id="f6a6b-460">受 Azure Active Directory (AAD) 管理的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="f6a6b-460">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="f6a6b-461">14 天之後 hello 最後一個配量執行。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-461">14 days after hello last slice run.</span></span> <br/><br/><span data-ttu-id="f6a6b-462">如果以 OAuth 式連結服務為基礎的配量至少每 14 天執行一次，則為 90 天。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-462">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="f6a6b-463">tooavoid/解決這個錯誤，重新授權使用 hello**授權**按鈕時 hello**權杖到期**然後重新部署 hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-463">tooavoid/resolve this error, reauthorize using hello **Authorize** button when hello **token expires** and redeploy hello linked service.</span></span> <span data-ttu-id="f6a6b-464">您也可以如下使用程式碼，以程式設計方式產生 **sessionId** 和 **authorization** 屬性的值：</span><span class="sxs-lookup"><span data-stu-id="f6a6b-464">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="f6a6b-465">請參閱[AzureDataLakeStoreLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)， [AzureDataLakeAnalyticsLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)，和[AuthorizationSessionGetResponse 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx)主題的詳細資訊關於 hello hello 程式碼中使用的 Data Factory 類別。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-465">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about hello Data Factory classes used in hello code.</span></span> <span data-ttu-id="f6a6b-466">加入的參考： Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll hello WindowsFormsWebAuthenticationDialog 類別。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-466">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for hello WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="azure-sql-linked-service"></a><span data-ttu-id="f6a6b-467">Azure SQL 連結服務</span><span class="sxs-lookup"><span data-stu-id="f6a6b-467">Azure SQL Linked Service</span></span>
<span data-ttu-id="f6a6b-468">您建立 Azure SQL 連結服務，並使用它搭配 hello[預存程序活動](data-factory-stored-proc-activity.md)tooinvoke 從 Data Factory 管線的預存程序。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-468">You create an Azure SQL linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> <span data-ttu-id="f6a6b-469">如需此連結服務的詳細資料，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#linked-service-properties) 一文。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-469">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse-linked-service"></a><span data-ttu-id="f6a6b-470">Azure SQL 資料倉儲連結服務</span><span class="sxs-lookup"><span data-stu-id="f6a6b-470">Azure SQL Data Warehouse Linked Service</span></span>
<span data-ttu-id="f6a6b-471">您建立連結的 Azure SQL 資料倉儲服務，並使用它搭配 hello[預存程序活動](data-factory-stored-proc-activity.md)tooinvoke 從 Data Factory 管線的預存程序。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-471">You create an Azure SQL Data Warehouse linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> <span data-ttu-id="f6a6b-472">如需此連結服務的詳細資料，請參閱 [Azure SQL 資料倉儲連接器](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) 一文。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-472">See [Azure SQL Data Warehouse Connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="sql-server-linked-service"></a><span data-ttu-id="f6a6b-473">SQL Server 連結服務</span><span class="sxs-lookup"><span data-stu-id="f6a6b-473">SQL Server Linked Service</span></span>
<span data-ttu-id="f6a6b-474">建立連結的 SQL Server 服務，並使用以 hello[預存程序活動](data-factory-stored-proc-activity.md)tooinvoke 從 Data Factory 管線的預存程序。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-474">You create a SQL Server linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> <span data-ttu-id="f6a6b-475">如需此連結服務的詳細資料，請參閱 [SQL Server 連接器](data-factory-sqlserver-connector.md#linked-service-properties) 一文。</span><span class="sxs-lookup"><span data-stu-id="f6a6b-475">See [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article for details about this linked service.</span></span>


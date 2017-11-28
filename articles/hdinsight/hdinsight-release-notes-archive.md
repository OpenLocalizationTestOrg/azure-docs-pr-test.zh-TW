---
title: "封存版本資訊 - Azure HDInsight 上的 Hadoop 元件 | Microsoft Docs"
description: "Azure HDInsight 之舊版 Hadoop 元件的封存版本資訊。"
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 04278aac85171601b5801b0890d14a9076060444
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="release-notes-archive-for-hadoop-components-on-azure-hdinsight"></a><span data-ttu-id="5e176-103">Azure HDInsight 上 Hadoop 元件的版本資訊 (封存)</span><span class="sxs-lookup"><span data-stu-id="5e176-103">Release notes (archive) for Hadoop components on Azure HDInsight</span></span>

<span data-ttu-id="5e176-104">此文章提供有關**較舊** Azure HDInsight 版本更新的資訊。</span><span class="sxs-lookup"><span data-stu-id="5e176-104">This article provides information about the **older** Azure HDInsight release updates.</span></span> <span data-ttu-id="5e176-105">如需有關最近版本的詳細資訊，請參閱 [HDInsight 版本資訊](hdinsight-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="5e176-105">For information on more recent releases, see [HDInsight Release Notes](hdinsight-release-notes.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e176-106">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="5e176-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5e176-107">如需詳細資訊，請參閱 [HDInsight 版本控制文件](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="5e176-107">For more information, see [HDInsight versioning article](hdinsight-component-versioning.md).</span></span>



## <a name="notes-for-08302016-release-of-hdinsight"></a><span data-ttu-id="5e176-108">HDInsight 08/30/2016 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-108">Notes for 08/30/2016 release of HDInsight</span></span>
<span data-ttu-id="5e176-109">使用此版本部署的 Linux 型 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-109">The full version numbers for Linux-based HDInsight clusters deployed with this release:</span></span>

| <span data-ttu-id="5e176-110">HDI</span><span class="sxs-lookup"><span data-stu-id="5e176-110">HDI</span></span> | <span data-ttu-id="5e176-111">HDI 叢集版本</span><span class="sxs-lookup"><span data-stu-id="5e176-111">HDI cluster version</span></span> | <span data-ttu-id="5e176-112">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-112">HDP</span></span> | <span data-ttu-id="5e176-113">HDP 組建</span><span class="sxs-lookup"><span data-stu-id="5e176-113">HDP Build</span></span> | <span data-ttu-id="5e176-114">Ambari 組建</span><span class="sxs-lookup"><span data-stu-id="5e176-114">Ambari Build</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-115">3.2</span><span class="sxs-lookup"><span data-stu-id="5e176-115">3.2</span></span> |<span data-ttu-id="5e176-116">3.2.1000.0.8268980</span><span class="sxs-lookup"><span data-stu-id="5e176-116">3.2.1000.0.8268980</span></span> |<span data-ttu-id="5e176-117">2.2</span><span class="sxs-lookup"><span data-stu-id="5e176-117">2.2</span></span> |<span data-ttu-id="5e176-118">2.2.9.1-19</span><span class="sxs-lookup"><span data-stu-id="5e176-118">2.2.9.1-19</span></span> |<span data-ttu-id="5e176-119">2.2.1.12-4</span><span class="sxs-lookup"><span data-stu-id="5e176-119">2.2.1.12-4</span></span> |
| <span data-ttu-id="5e176-120">3.3</span><span class="sxs-lookup"><span data-stu-id="5e176-120">3.3</span></span> |<span data-ttu-id="5e176-121">3.3.1000.0.8268980</span><span class="sxs-lookup"><span data-stu-id="5e176-121">3.3.1000.0.8268980</span></span> |<span data-ttu-id="5e176-122">2.3</span><span class="sxs-lookup"><span data-stu-id="5e176-122">2.3</span></span> |<span data-ttu-id="5e176-123">2.3.3.1-25</span><span class="sxs-lookup"><span data-stu-id="5e176-123">2.3.3.1-25</span></span> |<span data-ttu-id="5e176-124">2.2.1.12-4</span><span class="sxs-lookup"><span data-stu-id="5e176-124">2.2.1.12-4</span></span> |
| <span data-ttu-id="5e176-125">3.4</span><span class="sxs-lookup"><span data-stu-id="5e176-125">3.4</span></span> |<span data-ttu-id="5e176-126">3.4.1000.0.8269383</span><span class="sxs-lookup"><span data-stu-id="5e176-126">3.4.1000.0.8269383</span></span> |<span data-ttu-id="5e176-127">2.4</span><span class="sxs-lookup"><span data-stu-id="5e176-127">2.4</span></span> |<span data-ttu-id="5e176-128">2.4.2.4-5</span><span class="sxs-lookup"><span data-stu-id="5e176-128">2.4.2.4-5</span></span> |<span data-ttu-id="5e176-129">2.2.1.12-4</span><span class="sxs-lookup"><span data-stu-id="5e176-129">2.2.1.12-4</span></span> |

<span data-ttu-id="5e176-130">使用此版本部署的 Windows 型 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-130">The full version numbers for Windows-based HDInsight clusters deployed with this release:</span></span>

| <span data-ttu-id="5e176-131">HDI</span><span class="sxs-lookup"><span data-stu-id="5e176-131">HDI</span></span> | <span data-ttu-id="5e176-132">HDI 叢集版本</span><span class="sxs-lookup"><span data-stu-id="5e176-132">HDI cluster version</span></span> | <span data-ttu-id="5e176-133">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-133">HDP</span></span> | <span data-ttu-id="5e176-134">HDP 組建</span><span class="sxs-lookup"><span data-stu-id="5e176-134">HDP Build</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5e176-135">2.1</span><span class="sxs-lookup"><span data-stu-id="5e176-135">2.1</span></span> |<span data-ttu-id="5e176-136">2.1.10.1033.2559206</span><span class="sxs-lookup"><span data-stu-id="5e176-136">2.1.10.1033.2559206</span></span> |<span data-ttu-id="5e176-137">1.3</span><span class="sxs-lookup"><span data-stu-id="5e176-137">1.3</span></span> |<span data-ttu-id="5e176-138">1.3.12.0-01795</span><span class="sxs-lookup"><span data-stu-id="5e176-138">1.3.12.0-01795</span></span> |
| <span data-ttu-id="5e176-139">3.0</span><span class="sxs-lookup"><span data-stu-id="5e176-139">3.0</span></span> |<span data-ttu-id="5e176-140">3.0.6.1033.2559206</span><span class="sxs-lookup"><span data-stu-id="5e176-140">3.0.6.1033.2559206</span></span> |<span data-ttu-id="5e176-141">2.0</span><span class="sxs-lookup"><span data-stu-id="5e176-141">2.0</span></span> |<span data-ttu-id="5e176-142">2.0.13.0-2117</span><span class="sxs-lookup"><span data-stu-id="5e176-142">2.0.13.0-2117</span></span> |
| <span data-ttu-id="5e176-143">3.1</span><span class="sxs-lookup"><span data-stu-id="5e176-143">3.1</span></span> |<span data-ttu-id="5e176-144">3.1.4.1033.2559206</span><span class="sxs-lookup"><span data-stu-id="5e176-144">3.1.4.1033.2559206</span></span> |<span data-ttu-id="5e176-145">2.1</span><span class="sxs-lookup"><span data-stu-id="5e176-145">2.1</span></span> |<span data-ttu-id="5e176-146">2.1.16.0-2374</span><span class="sxs-lookup"><span data-stu-id="5e176-146">2.1.16.0-2374</span></span> |
| <span data-ttu-id="5e176-147">3.2</span><span class="sxs-lookup"><span data-stu-id="5e176-147">3.2</span></span> |<span data-ttu-id="5e176-148">3.2.7.1033.2559206</span><span class="sxs-lookup"><span data-stu-id="5e176-148">3.2.7.1033.2559206</span></span> |<span data-ttu-id="5e176-149">2.2</span><span class="sxs-lookup"><span data-stu-id="5e176-149">2.2</span></span> |<span data-ttu-id="5e176-150">2.2.9.1-11</span><span class="sxs-lookup"><span data-stu-id="5e176-150">2.2.9.1-11</span></span> |
| <span data-ttu-id="5e176-151">3.3</span><span class="sxs-lookup"><span data-stu-id="5e176-151">3.3</span></span> |<span data-ttu-id="5e176-152">3.3.0.1033.2559206</span><span class="sxs-lookup"><span data-stu-id="5e176-152">3.3.0.1033.2559206</span></span> |<span data-ttu-id="5e176-153">2.3</span><span class="sxs-lookup"><span data-stu-id="5e176-153">2.3</span></span> |<span data-ttu-id="5e176-154">2.3.3.1-25</span><span class="sxs-lookup"><span data-stu-id="5e176-154">2.3.3.1-25</span></span> |


## <a name="08172016---release-of-r-server-on-hdinsight"></a><span data-ttu-id="5e176-155">2016/8/17 - HDInsight 上的 R 伺服器版本資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-155">08/17/2016 - Release of R Server on HDInsight</span></span>
* <span data-ttu-id="5e176-156">R 伺服器 8.0.5 - 主要為修正程式的版本。</span><span class="sxs-lookup"><span data-stu-id="5e176-156">R Server 8.0.5 - mainly a bug fix release.</span></span> <span data-ttu-id="5e176-157">詳細資訊請參閱 [R 伺服器版本資訊](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) 。</span><span class="sxs-lookup"><span data-stu-id="5e176-157">See the [R Server Release Notes](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) for more info.</span></span>
* <span data-ttu-id="5e176-158">邊緣節點上的 AzureML 封裝 - [此 R 封裝](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) 使 R 模型可以做為 Azure ML Web 服務來發佈和取用。</span><span class="sxs-lookup"><span data-stu-id="5e176-158">AzureML package on the edge node - [this R package](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) enables R models to be published and consumed as an Azure ML web service.</span></span>  <span data-ttu-id="5e176-159">詳細資訊請參閱我們的 [HDInsight 上的 R 伺服器概觀](hdinsight-hadoop-r-server-overview.md)文章中的[實作模型](hdinsight-hadoop-r-server-overview.md#operationalize-a-model)一節。</span><span class="sxs-lookup"><span data-stu-id="5e176-159">See the ["Operationalize a Model"](hdinsight-hadoop-r-server-overview.md#operationalize-a-model) section of our ["Overview of R Server on HDInsight"](hdinsight-hadoop-r-server-overview.md) article for more info.</span></span>
* <span data-ttu-id="5e176-160">[前 100 名熱門 R 封裝](https://github.com/metacran/cranlogs) 的 Linux 相依性 - 現在，這些 Linux 封裝相依性都是預先安裝好。</span><span class="sxs-lookup"><span data-stu-id="5e176-160">Linux dependencies of the [top 100 most popular R packages](https://github.com/metacran/cranlogs) - these Linux package dependencies are now pre-installed.</span></span>
* <span data-ttu-id="5e176-161">新增 R 封裝至資料節點時使用 CRAN 儲存機制的選項。</span><span class="sxs-lookup"><span data-stu-id="5e176-161">Option to use the CRAN repo when adding R packages to the data nodes.</span></span> <span data-ttu-id="5e176-162">如需詳細資訊，請參閱[開始使用 HDInsight 上的 R 伺服器](hdinsight-hadoop-r-server-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="5e176-162">For more information, see ["Get started using R Server on HDInsight"](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="5e176-163">改善叢集建立時 R 伺服器佈建的可靠性。</span><span class="sxs-lookup"><span data-stu-id="5e176-163">Improved the reliability of R Server provisioning when clusters are created.</span></span>

## <a name="notes-for-08012016-release-of-hdinsight"></a><span data-ttu-id="5e176-164">HDInsight 2016/08/01 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-164">Notes for 08/01/2016 release of HDInsight</span></span>
<span data-ttu-id="5e176-165">使用此版本部署的 Linux 型 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-165">The full version numbers for Linux-based HDInsight clusters deployed with this release:</span></span>

| <span data-ttu-id="5e176-166">HDI</span><span class="sxs-lookup"><span data-stu-id="5e176-166">HDI</span></span> | <span data-ttu-id="5e176-167">HDI 叢集版本</span><span class="sxs-lookup"><span data-stu-id="5e176-167">HDI cluster version</span></span> | <span data-ttu-id="5e176-168">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-168">HDP</span></span> | <span data-ttu-id="5e176-169">HDP 組建</span><span class="sxs-lookup"><span data-stu-id="5e176-169">HDP Build</span></span> | <span data-ttu-id="5e176-170">Ambari 組建</span><span class="sxs-lookup"><span data-stu-id="5e176-170">Ambari Build</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-171">3.2</span><span class="sxs-lookup"><span data-stu-id="5e176-171">3.2</span></span> |<span data-ttu-id="5e176-172">3.2.1000.0.8028416</span><span class="sxs-lookup"><span data-stu-id="5e176-172">3.2.1000.0.8028416</span></span> |<span data-ttu-id="5e176-173">2.2</span><span class="sxs-lookup"><span data-stu-id="5e176-173">2.2</span></span> |<span data-ttu-id="5e176-174">2.2.9.1-19</span><span class="sxs-lookup"><span data-stu-id="5e176-174">2.2.9.1-19</span></span> |<span data-ttu-id="5e176-175">2.2.1.12-4</span><span class="sxs-lookup"><span data-stu-id="5e176-175">2.2.1.12-4</span></span> |
| <span data-ttu-id="5e176-176">3.3</span><span class="sxs-lookup"><span data-stu-id="5e176-176">3.3</span></span> |<span data-ttu-id="5e176-177">3.3.1000.0.8028416</span><span class="sxs-lookup"><span data-stu-id="5e176-177">3.3.1000.0.8028416</span></span> |<span data-ttu-id="5e176-178">2.3</span><span class="sxs-lookup"><span data-stu-id="5e176-178">2.3</span></span> |<span data-ttu-id="5e176-179">2.3.3.1-25</span><span class="sxs-lookup"><span data-stu-id="5e176-179">2.3.3.1-25</span></span> |<span data-ttu-id="5e176-180">2.2.1.12-4</span><span class="sxs-lookup"><span data-stu-id="5e176-180">2.2.1.12-4</span></span> |
| <span data-ttu-id="5e176-181">3.4</span><span class="sxs-lookup"><span data-stu-id="5e176-181">3.4</span></span> |<span data-ttu-id="5e176-182">3.4.1000.0.8053402</span><span class="sxs-lookup"><span data-stu-id="5e176-182">3.4.1000.0.8053402</span></span> |<span data-ttu-id="5e176-183">2.4</span><span class="sxs-lookup"><span data-stu-id="5e176-183">2.4</span></span> |<span data-ttu-id="5e176-184">2.4.2.4-5</span><span class="sxs-lookup"><span data-stu-id="5e176-184">2.4.2.4-5</span></span> |<span data-ttu-id="5e176-185">2.2.1.12-4</span><span class="sxs-lookup"><span data-stu-id="5e176-185">2.2.1.12-4</span></span> |

<span data-ttu-id="5e176-186">使用此版本部署的 Windows 型 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-186">The full version numbers for Windows-based HDInsight clusters deployed with this release:</span></span>

| <span data-ttu-id="5e176-187">HDI</span><span class="sxs-lookup"><span data-stu-id="5e176-187">HDI</span></span> | <span data-ttu-id="5e176-188">HDI 叢集版本</span><span class="sxs-lookup"><span data-stu-id="5e176-188">HDI cluster version</span></span> | <span data-ttu-id="5e176-189">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-189">HDP</span></span> | <span data-ttu-id="5e176-190">HDP 組建</span><span class="sxs-lookup"><span data-stu-id="5e176-190">HDP Build</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5e176-191">2.1</span><span class="sxs-lookup"><span data-stu-id="5e176-191">2.1</span></span> |<span data-ttu-id="5e176-192">2.1.10.1005.2488842</span><span class="sxs-lookup"><span data-stu-id="5e176-192">2.1.10.1005.2488842</span></span> |<span data-ttu-id="5e176-193">1.3</span><span class="sxs-lookup"><span data-stu-id="5e176-193">1.3</span></span> |<span data-ttu-id="5e176-194">1.3.12.0-01795</span><span class="sxs-lookup"><span data-stu-id="5e176-194">1.3.12.0-01795</span></span> |
| <span data-ttu-id="5e176-195">3.0</span><span class="sxs-lookup"><span data-stu-id="5e176-195">3.0</span></span> |<span data-ttu-id="5e176-196">3.0.6.1005.2488842</span><span class="sxs-lookup"><span data-stu-id="5e176-196">3.0.6.1005.2488842</span></span> |<span data-ttu-id="5e176-197">2.0</span><span class="sxs-lookup"><span data-stu-id="5e176-197">2.0</span></span> |<span data-ttu-id="5e176-198">2.0.13.0-2117</span><span class="sxs-lookup"><span data-stu-id="5e176-198">2.0.13.0-2117</span></span> |
| <span data-ttu-id="5e176-199">3.1</span><span class="sxs-lookup"><span data-stu-id="5e176-199">3.1</span></span> |<span data-ttu-id="5e176-200">3.1.4.1005.2488842</span><span class="sxs-lookup"><span data-stu-id="5e176-200">3.1.4.1005.2488842</span></span> |<span data-ttu-id="5e176-201">2.1</span><span class="sxs-lookup"><span data-stu-id="5e176-201">2.1</span></span> |<span data-ttu-id="5e176-202">2.1.16.0-2374</span><span class="sxs-lookup"><span data-stu-id="5e176-202">2.1.16.0-2374</span></span> |
| <span data-ttu-id="5e176-203">3.2</span><span class="sxs-lookup"><span data-stu-id="5e176-203">3.2</span></span> |<span data-ttu-id="5e176-204">3.2.7.1005.2488842</span><span class="sxs-lookup"><span data-stu-id="5e176-204">3.2.7.1005.2488842</span></span> |<span data-ttu-id="5e176-205">2.2</span><span class="sxs-lookup"><span data-stu-id="5e176-205">2.2</span></span> |<span data-ttu-id="5e176-206">2.2.9.1-11</span><span class="sxs-lookup"><span data-stu-id="5e176-206">2.2.9.1-11</span></span> |
| <span data-ttu-id="5e176-207">3.3</span><span class="sxs-lookup"><span data-stu-id="5e176-207">3.3</span></span> |<span data-ttu-id="5e176-208">3.3.0.1005.2488842</span><span class="sxs-lookup"><span data-stu-id="5e176-208">3.3.0.1005.2488842</span></span> |<span data-ttu-id="5e176-209">2.3</span><span class="sxs-lookup"><span data-stu-id="5e176-209">2.3</span></span> |<span data-ttu-id="5e176-210">2.3.3.1-25</span><span class="sxs-lookup"><span data-stu-id="5e176-210">2.3.3.1-25</span></span> |

<span data-ttu-id="5e176-211">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-211">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-212">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-212">Title</span></span> | <span data-ttu-id="5e176-213">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-213">Description</span></span> | <span data-ttu-id="5e176-214">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-214">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-215">叢集類型 (例如 Spark、Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-215">Cluster Type (for example Spark, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-216">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-216">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-217">HDInsight 3.4 叢集的變更</span><span class="sxs-lookup"><span data-stu-id="5e176-217">Changes to HDInsight 3.4 clusters</span></span> |<span data-ttu-id="5e176-218">為了提升效能，下列 Hive 組態的預設值已變更</span><span class="sxs-lookup"><span data-stu-id="5e176-218">The default values for following hive configurations are changed for better performance</span></span> <ul><li>`hive.vectorized.execution.reduce.enabled=true`</li><li>`hive.tez.min.partition.factor=1f`</li><li>`hive.tez.max.partition.factor=3f`</li><li>`tez.shuffle-vertex-manager.min-src-fraction=0.9`</li><li>`tez.shuffle-vertex-manager.max-src-fraction=0.95`</li><li>`tez.runtime.shuffle.connect.timeout= 30000`</li></ul> |<span data-ttu-id="5e176-219">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-219">Service</span></span> |<span data-ttu-id="5e176-220">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-220">All</span></span> |<span data-ttu-id="5e176-221">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-221">N/A</span></span> |
| <span data-ttu-id="5e176-222">此版本包含下列修正程式</span><span class="sxs-lookup"><span data-stu-id="5e176-222">Following fixes are included in this release</span></span> |<span data-ttu-id="5e176-223">HIVE-13632, HIVE-12897,HIVE-12907,HIVE-12908,HIVE-12988,HIVE-13510,HIVE-13572,HIVE-13716,HIVE-13726,HIVE-12505,HIVE-13632,HIVE-13661,HIVE-13705,HIVE-13743,HIVE-13810,HIVE-13857,HIVE-13902,HIVE-13911,HIVE-13933</span><span class="sxs-lookup"><span data-stu-id="5e176-223">HIVE-13632, HIVE-12897,HIVE-12907,HIVE-12908,HIVE-12988,HIVE-13510,HIVE-13572,HIVE-13716,HIVE-13726,HIVE-12505,HIVE-13632,HIVE-13661,HIVE-13705,HIVE-13743,HIVE-13810,HIVE-13857,HIVE-13902,HIVE-13911,HIVE-13933</span></span> |<span data-ttu-id="5e176-224">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-224">Service</span></span> |<span data-ttu-id="5e176-225">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-225">All</span></span> |<span data-ttu-id="5e176-226">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-226">N/A</span></span> |

## <a name="notes-for-07142016-release-of-hdinsight"></a><span data-ttu-id="5e176-227">HDInsight 2016/07/14 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-227">Notes for 07/14/2016 release of HDInsight</span></span>
<span data-ttu-id="5e176-228">使用此版本部署的 Linux 型 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-228">The full version numbers for Linux-based HDInsight clusters deployed with this release:</span></span>

| <span data-ttu-id="5e176-229">HDI</span><span class="sxs-lookup"><span data-stu-id="5e176-229">HDI</span></span> | <span data-ttu-id="5e176-230">HDI 叢集版本</span><span class="sxs-lookup"><span data-stu-id="5e176-230">HDI cluster version</span></span> | <span data-ttu-id="5e176-231">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-231">HDP</span></span> | <span data-ttu-id="5e176-232">HDP 組建</span><span class="sxs-lookup"><span data-stu-id="5e176-232">HDP Build</span></span> | <span data-ttu-id="5e176-233">Ambari 組建</span><span class="sxs-lookup"><span data-stu-id="5e176-233">Ambari Build</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-234">3.2</span><span class="sxs-lookup"><span data-stu-id="5e176-234">3.2</span></span> |<span data-ttu-id="5e176-235">3.2.1000.0.7932505</span><span class="sxs-lookup"><span data-stu-id="5e176-235">3.2.1000.0.7932505</span></span> |<span data-ttu-id="5e176-236">2.2</span><span class="sxs-lookup"><span data-stu-id="5e176-236">2.2</span></span> |<span data-ttu-id="5e176-237">2.2.9.1-11</span><span class="sxs-lookup"><span data-stu-id="5e176-237">2.2.9.1-11</span></span> |<span data-ttu-id="5e176-238">2.2.1.12-2</span><span class="sxs-lookup"><span data-stu-id="5e176-238">2.2.1.12-2</span></span> |
| <span data-ttu-id="5e176-239">3.3</span><span class="sxs-lookup"><span data-stu-id="5e176-239">3.3</span></span> |<span data-ttu-id="5e176-240">3.3.1000.0.7932505</span><span class="sxs-lookup"><span data-stu-id="5e176-240">3.3.1000.0.7932505</span></span> |<span data-ttu-id="5e176-241">2.3</span><span class="sxs-lookup"><span data-stu-id="5e176-241">2.3</span></span> |<span data-ttu-id="5e176-242">2.3.3.1-18</span><span class="sxs-lookup"><span data-stu-id="5e176-242">2.3.3.1-18</span></span> |<span data-ttu-id="5e176-243">2.2.1.12-2</span><span class="sxs-lookup"><span data-stu-id="5e176-243">2.2.1.12-2</span></span> |
| <span data-ttu-id="5e176-244">3.4</span><span class="sxs-lookup"><span data-stu-id="5e176-244">3.4</span></span> |<span data-ttu-id="5e176-245">3.4.1000.0.7933003</span><span class="sxs-lookup"><span data-stu-id="5e176-245">3.4.1000.0.7933003</span></span> |<span data-ttu-id="5e176-246">2.4</span><span class="sxs-lookup"><span data-stu-id="5e176-246">2.4</span></span> |<span data-ttu-id="5e176-247">2.4.2.0</span><span class="sxs-lookup"><span data-stu-id="5e176-247">2.4.2.0</span></span> |<span data-ttu-id="5e176-248">2.2.1.12-2</span><span class="sxs-lookup"><span data-stu-id="5e176-248">2.2.1.12-2</span></span> |

<span data-ttu-id="5e176-249">使用此版本部署的 Windows 型 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-249">The full version numbers for Windows-based HDInsight clusters deployed with this release:</span></span>

| <span data-ttu-id="5e176-250">HDI</span><span class="sxs-lookup"><span data-stu-id="5e176-250">HDI</span></span> | <span data-ttu-id="5e176-251">HDI 叢集版本</span><span class="sxs-lookup"><span data-stu-id="5e176-251">HDI cluster version</span></span> | <span data-ttu-id="5e176-252">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-252">HDP</span></span> | <span data-ttu-id="5e176-253">HDP 組建</span><span class="sxs-lookup"><span data-stu-id="5e176-253">HDP Build</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5e176-254">2.1</span><span class="sxs-lookup"><span data-stu-id="5e176-254">2.1</span></span> |<span data-ttu-id="5e176-255">2.1.10.989.2441725</span><span class="sxs-lookup"><span data-stu-id="5e176-255">2.1.10.989.2441725</span></span> |<span data-ttu-id="5e176-256">1.3</span><span class="sxs-lookup"><span data-stu-id="5e176-256">1.3</span></span> |<span data-ttu-id="5e176-257">1.3.12.0-01795</span><span class="sxs-lookup"><span data-stu-id="5e176-257">1.3.12.0-01795</span></span> |
| <span data-ttu-id="5e176-258">3.0</span><span class="sxs-lookup"><span data-stu-id="5e176-258">3.0</span></span> |<span data-ttu-id="5e176-259">3.0.6.989.2441725</span><span class="sxs-lookup"><span data-stu-id="5e176-259">3.0.6.989.2441725</span></span> |<span data-ttu-id="5e176-260">2.0</span><span class="sxs-lookup"><span data-stu-id="5e176-260">2.0</span></span> |<span data-ttu-id="5e176-261">2.0.13.0-2117</span><span class="sxs-lookup"><span data-stu-id="5e176-261">2.0.13.0-2117</span></span> |
| <span data-ttu-id="5e176-262">3.1</span><span class="sxs-lookup"><span data-stu-id="5e176-262">3.1</span></span> |<span data-ttu-id="5e176-263">3.1.4.989.2441725</span><span class="sxs-lookup"><span data-stu-id="5e176-263">3.1.4.989.2441725</span></span> |<span data-ttu-id="5e176-264">2.1</span><span class="sxs-lookup"><span data-stu-id="5e176-264">2.1</span></span> |<span data-ttu-id="5e176-265">2.1.16.0-2374</span><span class="sxs-lookup"><span data-stu-id="5e176-265">2.1.16.0-2374</span></span> |
| <span data-ttu-id="5e176-266">3.2</span><span class="sxs-lookup"><span data-stu-id="5e176-266">3.2</span></span> |<span data-ttu-id="5e176-267">3.2.7.989.2441725</span><span class="sxs-lookup"><span data-stu-id="5e176-267">3.2.7.989.2441725</span></span> |<span data-ttu-id="5e176-268">2.2</span><span class="sxs-lookup"><span data-stu-id="5e176-268">2.2</span></span> |<span data-ttu-id="5e176-269">2.2.9.1-11</span><span class="sxs-lookup"><span data-stu-id="5e176-269">2.2.9.1-11</span></span> |
| <span data-ttu-id="5e176-270">3.3</span><span class="sxs-lookup"><span data-stu-id="5e176-270">3.3</span></span> |<span data-ttu-id="5e176-271">3.3.0.989.2441725</span><span class="sxs-lookup"><span data-stu-id="5e176-271">3.3.0.989.2441725</span></span> |<span data-ttu-id="5e176-272">2.3</span><span class="sxs-lookup"><span data-stu-id="5e176-272">2.3</span></span> |<span data-ttu-id="5e176-273">2.3.3.1-21</span><span class="sxs-lookup"><span data-stu-id="5e176-273">2.3.3.1-21</span></span> |

## <a name="notes-for-07072016-release-of-hdinsight"></a><span data-ttu-id="5e176-274">HDInsight 2016/07/07 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-274">Notes for 07/07/2016 release of HDInsight</span></span>
<span data-ttu-id="5e176-275">使用此版本部署的 Linux 型 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-275">The full version numbers for Linux-based HDInsight clusters deployed with this release:</span></span>

| <span data-ttu-id="5e176-276">HDI</span><span class="sxs-lookup"><span data-stu-id="5e176-276">HDI</span></span> | <span data-ttu-id="5e176-277">HDI 叢集版本</span><span class="sxs-lookup"><span data-stu-id="5e176-277">HDI cluster version</span></span> | <span data-ttu-id="5e176-278">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-278">HDP</span></span> | <span data-ttu-id="5e176-279">HDP 組建</span><span class="sxs-lookup"><span data-stu-id="5e176-279">HDP Build</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5e176-280">3.2</span><span class="sxs-lookup"><span data-stu-id="5e176-280">3.2</span></span> |<span data-ttu-id="5e176-281">3.2.1000.0.7864996</span><span class="sxs-lookup"><span data-stu-id="5e176-281">3.2.1000.0.7864996</span></span> |<span data-ttu-id="5e176-282">2.2</span><span class="sxs-lookup"><span data-stu-id="5e176-282">2.2</span></span> |<span data-ttu-id="5e176-283">2.2.9.1-11</span><span class="sxs-lookup"><span data-stu-id="5e176-283">2.2.9.1-11</span></span> |
| <span data-ttu-id="5e176-284">3.3</span><span class="sxs-lookup"><span data-stu-id="5e176-284">3.3</span></span> |<span data-ttu-id="5e176-285">3.3.1000.0.7864996</span><span class="sxs-lookup"><span data-stu-id="5e176-285">3.3.1000.0.7864996</span></span> |<span data-ttu-id="5e176-286">2.3</span><span class="sxs-lookup"><span data-stu-id="5e176-286">2.3</span></span> |<span data-ttu-id="5e176-287">2.3.3.1-18</span><span class="sxs-lookup"><span data-stu-id="5e176-287">2.3.3.1-18</span></span> |
| <span data-ttu-id="5e176-288">3.4</span><span class="sxs-lookup"><span data-stu-id="5e176-288">3.4</span></span> |<span data-ttu-id="5e176-289">3.4.1000.0.7861906</span><span class="sxs-lookup"><span data-stu-id="5e176-289">3.4.1000.0.7861906</span></span> |<span data-ttu-id="5e176-290">2.4</span><span class="sxs-lookup"><span data-stu-id="5e176-290">2.4</span></span> |<span data-ttu-id="5e176-291">2.4.2.0</span><span class="sxs-lookup"><span data-stu-id="5e176-291">2.4.2.0</span></span> |

<span data-ttu-id="5e176-292">使用此版本部署的 Windows 型 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-292">The full version numbers for Windows-based HDInsight clusters deployed with this release:</span></span>

| <span data-ttu-id="5e176-293">HDI</span><span class="sxs-lookup"><span data-stu-id="5e176-293">HDI</span></span> | <span data-ttu-id="5e176-294">HDI 叢集版本</span><span class="sxs-lookup"><span data-stu-id="5e176-294">HDI cluster version</span></span> | <span data-ttu-id="5e176-295">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-295">HDP</span></span> | <span data-ttu-id="5e176-296">HDP 組建</span><span class="sxs-lookup"><span data-stu-id="5e176-296">HDP Build</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5e176-297">2.1</span><span class="sxs-lookup"><span data-stu-id="5e176-297">2.1</span></span> |<span data-ttu-id="5e176-298">2.1.10.977.2413853</span><span class="sxs-lookup"><span data-stu-id="5e176-298">2.1.10.977.2413853</span></span> |<span data-ttu-id="5e176-299">1.3</span><span class="sxs-lookup"><span data-stu-id="5e176-299">1.3</span></span> |<span data-ttu-id="5e176-300">1.3.12.0-01795</span><span class="sxs-lookup"><span data-stu-id="5e176-300">1.3.12.0-01795</span></span> |
| <span data-ttu-id="5e176-301">3.0</span><span class="sxs-lookup"><span data-stu-id="5e176-301">3.0</span></span> |<span data-ttu-id="5e176-302">3.0.6.977.2413853</span><span class="sxs-lookup"><span data-stu-id="5e176-302">3.0.6.977.2413853</span></span> |<span data-ttu-id="5e176-303">2.0</span><span class="sxs-lookup"><span data-stu-id="5e176-303">2.0</span></span> |<span data-ttu-id="5e176-304">2.0.13.0-2117</span><span class="sxs-lookup"><span data-stu-id="5e176-304">2.0.13.0-2117</span></span> |
| <span data-ttu-id="5e176-305">3.1</span><span class="sxs-lookup"><span data-stu-id="5e176-305">3.1</span></span> |<span data-ttu-id="5e176-306">3.1.4.977.2413853</span><span class="sxs-lookup"><span data-stu-id="5e176-306">3.1.4.977.2413853</span></span> |<span data-ttu-id="5e176-307">2.1</span><span class="sxs-lookup"><span data-stu-id="5e176-307">2.1</span></span> |<span data-ttu-id="5e176-308">2.1.16.0-2374</span><span class="sxs-lookup"><span data-stu-id="5e176-308">2.1.16.0-2374</span></span> |
| <span data-ttu-id="5e176-309">3.2</span><span class="sxs-lookup"><span data-stu-id="5e176-309">3.2</span></span> |<span data-ttu-id="5e176-310">3.2.7.977.2413853</span><span class="sxs-lookup"><span data-stu-id="5e176-310">3.2.7.977.2413853</span></span> |<span data-ttu-id="5e176-311">2.2</span><span class="sxs-lookup"><span data-stu-id="5e176-311">2.2</span></span> |<span data-ttu-id="5e176-312">2.2.9.1-11</span><span class="sxs-lookup"><span data-stu-id="5e176-312">2.2.9.1-11</span></span> |
| <span data-ttu-id="5e176-313">3.3</span><span class="sxs-lookup"><span data-stu-id="5e176-313">3.3</span></span> |<span data-ttu-id="5e176-314">3.3.0.977.2413853</span><span class="sxs-lookup"><span data-stu-id="5e176-314">3.3.0.977.2413853</span></span> |<span data-ttu-id="5e176-315">2.3</span><span class="sxs-lookup"><span data-stu-id="5e176-315">2.3</span></span> |<span data-ttu-id="5e176-316">2.3.3.1-21</span><span class="sxs-lookup"><span data-stu-id="5e176-316">2.3.3.1-21</span></span> |

<span data-ttu-id="5e176-317">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-317">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-318">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-318">Title</span></span> | <span data-ttu-id="5e176-319">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-319">Description</span></span> | <span data-ttu-id="5e176-320">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-320">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-321">叢集類型 (例如 Spark、Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-321">Cluster Type (for example Spark, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-322">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-322">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| [<span data-ttu-id="5e176-323">HDInsight Tools for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5e176-323">HDInsight Tools for IntelliJ</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md) |<span data-ttu-id="5e176-324">適用於 HDInsight Spark 叢集的 IntelliJ IDEA 外掛程式現在與適用於 IntelliJ 的 Azure 工具組整合。</span><span class="sxs-lookup"><span data-stu-id="5e176-324">IntelliJ IDEA plugin for HDInsight Spark clusters is now integrated with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="5e176-325">它支援 Azure SDK v2.9.1、最新的 Java SDK，以及包含獨立IntelliJ 之 HDInsight 外掛程式的所有功能。</span><span class="sxs-lookup"><span data-stu-id="5e176-325">It supports Azure SDK v2.9.1, latest Java SDKs, and includes all the features from the standalone HDInsight Plugin for IntelliJ.</span></span> |<span data-ttu-id="5e176-326">工具</span><span class="sxs-lookup"><span data-stu-id="5e176-326">Tools</span></span> |<span data-ttu-id="5e176-327">Spark</span><span class="sxs-lookup"><span data-stu-id="5e176-327">Spark</span></span> |<span data-ttu-id="5e176-328">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-328">N/A</span></span> |
| [<span data-ttu-id="5e176-329">HDInsight Tools for Eclipse</span><span class="sxs-lookup"><span data-stu-id="5e176-329">HDInsight Tools for Eclipse</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md) |<span data-ttu-id="5e176-330">適用於 Eclipse 的 Azure 工具組現在支援 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e176-330">Azure Toolkit for Eclipse now supports HDInsight Spark clusters.</span></span> <span data-ttu-id="5e176-331">它可啟用下列功能：</span><span class="sxs-lookup"><span data-stu-id="5e176-331">It enables the following features:</span></span> <ul><li><span data-ttu-id="5e176-332">透過針對 IntelliSense 的一流撰寫支援、自動格式化、錯誤檢查等功能，在 Scala 和 Java 中輕鬆建立並撰寫 Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e176-332">Create and write a Spark application easily in Scala and Java with first class authoring support for IntelliSense, auto format, error checking, etc.</span></span></li><li><span data-ttu-id="5e176-333">在本機測試 Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e176-333">Test the Spark application locally.</span></span></li><li><span data-ttu-id="5e176-334">將作業提交至 HDInsight Spark 叢集，並擷取結果。</span><span class="sxs-lookup"><span data-stu-id="5e176-334">Submit jobs to HDInsight Spark cluster and retrieve the results.</span></span></li><li><span data-ttu-id="5e176-335">登入 Azure，並存取與 Azure 訂用帳戶相關聯的所有 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e176-335">Log in to Azure and access all the Spark clusters associated with your Azure subscriptions.</span></span></li><li><span data-ttu-id="5e176-336">瀏覽 HDInsight Spark 叢集的所有相關聯儲存體資源。</span><span class="sxs-lookup"><span data-stu-id="5e176-336">Navigate all the associated storage resources of your HDInsight Spark cluster.</span></span></li></ul> |<span data-ttu-id="5e176-337">工具</span><span class="sxs-lookup"><span data-stu-id="5e176-337">Tools</span></span> |<span data-ttu-id="5e176-338">Spark</span><span class="sxs-lookup"><span data-stu-id="5e176-338">Spark</span></span> |<span data-ttu-id="5e176-339">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-339">N/A</span></span> |

<span data-ttu-id="5e176-340">從這個版本開始，我們針對以 Linux 為基礎的 HDInsight 叢集變更客體 OS 修補原則。</span><span class="sxs-lookup"><span data-stu-id="5e176-340">Starting with this release, we have changed the guest OS patching policy for Linux-based HDInsight clusters.</span></span> <span data-ttu-id="5e176-341">新原則的目標是大幅減少因為修補而產生的重新開機次數。</span><span class="sxs-lookup"><span data-stu-id="5e176-341">The goal of the new policy is to significantly reduce the number of reboots due to patching.</span></span> <span data-ttu-id="5e176-342">新的原則會在每個星期一或星期四 UTC 上午 12 時開始，以交錯方式在任何指定叢集的節點之間，修補 Linux 叢集上的虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="5e176-342">The new policy patches virtual machines (VMs) on Linux clusters every Monday or Thursday starting at 12AM UTC in a staggered fashion across nodes in any given cluster.</span></span> <span data-ttu-id="5e176-343">不過，任何指定的 VM 每隔 30 天只會因為客體 OS 修補而最多重新開機一次。</span><span class="sxs-lookup"><span data-stu-id="5e176-343">However, any given VM only reboots at most once every 30 days due to guest OS patching.</span></span> <span data-ttu-id="5e176-344">此外，新建立的叢集在叢集建立之後，也不會在 30 天內第一次重新開機。</span><span class="sxs-lookup"><span data-stu-id="5e176-344">In addition, the first reboot for a newly created cluster does not happen sooner than 30 days from the cluster creation date.</span></span>

> [!NOTE]
> <span data-ttu-id="5e176-345">這些變更只適用於等於或大於這個發行版本的新建立叢集。</span><span class="sxs-lookup"><span data-stu-id="5e176-345">These changes only apply to newly created clusters equal or greater than this release version.</span></span>
>
>

## <a name="notes-for-06062016-release-of-hdinsight"></a><span data-ttu-id="5e176-346">HDInsight 2016/06/06 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-346">Notes for 06/06/2016 release of HDInsight</span></span>
<span data-ttu-id="5e176-347">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-347">The full version numbers for HDInsight clusters deployed with this release:</span></span>

| <span data-ttu-id="5e176-348">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-348">HDP</span></span> | <span data-ttu-id="5e176-349">HDI 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-349">HDI Version</span></span> | <span data-ttu-id="5e176-350">Spark 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-350">Spark Version</span></span> | <span data-ttu-id="5e176-351">Ambari 組建編號</span><span class="sxs-lookup"><span data-stu-id="5e176-351">Ambari Build Number</span></span> | <span data-ttu-id="5e176-352">HDP 組建編號</span><span class="sxs-lookup"><span data-stu-id="5e176-352">HDP Build Number</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-353">2.3</span><span class="sxs-lookup"><span data-stu-id="5e176-353">2.3</span></span> |<span data-ttu-id="5e176-354">3.3.1000.0.7702215</span><span class="sxs-lookup"><span data-stu-id="5e176-354">3.3.1000.0.7702215</span></span> |<span data-ttu-id="5e176-355">1.5.2</span><span class="sxs-lookup"><span data-stu-id="5e176-355">1.5.2</span></span> |<span data-ttu-id="5e176-356">2.2.1.8-2</span><span class="sxs-lookup"><span data-stu-id="5e176-356">2.2.1.8-2</span></span> |<span data-ttu-id="5e176-357">2.3.3.1-18</span><span class="sxs-lookup"><span data-stu-id="5e176-357">2.3.3.1-18</span></span> |
| <span data-ttu-id="5e176-358">2.4</span><span class="sxs-lookup"><span data-stu-id="5e176-358">2.4</span></span> |<span data-ttu-id="5e176-359">3.4.1000.0.7702224</span><span class="sxs-lookup"><span data-stu-id="5e176-359">3.4.1000.0.7702224</span></span> |<span data-ttu-id="5e176-360">1.6.1</span><span class="sxs-lookup"><span data-stu-id="5e176-360">1.6.1</span></span> |<span data-ttu-id="5e176-361">2.2.1.8-2</span><span class="sxs-lookup"><span data-stu-id="5e176-361">2.2.1.8-2</span></span> |<span data-ttu-id="5e176-362">2.4.2.0</span><span class="sxs-lookup"><span data-stu-id="5e176-362">2.4.2.0</span></span> |

<span data-ttu-id="5e176-363">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-363">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-364">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-364">Title</span></span> | <span data-ttu-id="5e176-365">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-365">Description</span></span> | <span data-ttu-id="5e176-366">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-366">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-367">叢集類型 (例如 Spark、Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-367">Cluster Type (for example Spark, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-368">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-368">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-369">HDInsight 上的 Spark 已正式推出</span><span class="sxs-lookup"><span data-stu-id="5e176-369">Spark on HDInsight is generally available</span></span> |<span data-ttu-id="5e176-370">此版本會針對 HDInsight 上 Apache Spark 的開放原始碼提供改良的可用性、延展性和產能。</span><span class="sxs-lookup"><span data-stu-id="5e176-370">This release brings improvements in availability, scalability, and productivity to open source Apache Spark on HDInsight.</span></span> <ul><li><span data-ttu-id="5e176-371">業界領先的 99.9% 可用性 SLA，因此能應付企業要求嚴苛的工作負載。</span><span class="sxs-lookup"><span data-stu-id="5e176-371">Industry-leading availability SLA of 99.9% which makes it suitable for demanding enterprise workloads.</span></span></li><li><span data-ttu-id="5e176-372">使用 Azure Data Lake Store 的可調整儲存體層。</span><span class="sxs-lookup"><span data-stu-id="5e176-372">Scalable storage layer using Azure Data Lake Store.</span></span></li><li><span data-ttu-id="5e176-373">針對資料探索和開發的每個階段皆有相應的生產力工具。</span><span class="sxs-lookup"><span data-stu-id="5e176-373">Productivity tools for every phase of data exploration and development.</span></span> <span data-ttu-id="5e176-374">含自訂 Spark 核心的 Jupyter 筆記本會啟用互動式資料探索，並與 BI 儀表板 (例如 Power BI、Tableau 及 Qlik) 整合，非常適合快速資料共用和連續報告；IntelliJ 外掛程式是適用於長期程式碼構件開發和偵錯的可靠方式。</span><span class="sxs-lookup"><span data-stu-id="5e176-374">Jupyter notebooks with customized Spark kernel enable interactive data exploration, integration with BI dashboards like Power BI, Tableau and Qlik is good for quick data sharing and continuous reporting, IntelliJ plugin is reliable option for long term code artifact development and debugging.</span></span></li></ul> |<span data-ttu-id="5e176-375">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-375">Service</span></span> |<span data-ttu-id="5e176-376">Spark</span><span class="sxs-lookup"><span data-stu-id="5e176-376">Spark</span></span> |<span data-ttu-id="5e176-377">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-377">N/A</span></span> |
| <span data-ttu-id="5e176-378">HDInsight Tools for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5e176-378">HDInsight Tools for IntelliJ</span></span> |<span data-ttu-id="5e176-379">這是適用於 HDInsight Spark 叢集的 IntelliJ IDEA 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5e176-379">This is an IntelliJ IDEA plugin for HDInsight Spark clusters.</span></span> <span data-ttu-id="5e176-380">它可啟用下列功能：</span><span class="sxs-lookup"><span data-stu-id="5e176-380">It enables the following features:</span></span><ul><li><span data-ttu-id="5e176-381">透過針對 IntelliSense 的一流撰寫支援、自動格式化、錯誤檢查等功能，在 Scala 和 Java 中輕鬆建立並撰寫 Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e176-381">Create and write a Spark application easily in Scala and Java with first class authoring support for IntelliSense, auto format, error checking, etc.</span></span></li><li><span data-ttu-id="5e176-382">在本機測試 Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e176-382">Test the Spark application locally.</span></span></li><li><span data-ttu-id="5e176-383">將作業提交至 HDInsight Spark 叢集，並擷取結果。</span><span class="sxs-lookup"><span data-stu-id="5e176-383">Submit jobs to HDInsight Spark cluster and retrieve the results.</span></span></li><li><span data-ttu-id="5e176-384">登入 Azure，並存取與 Azure 訂用帳戶相關聯的所有 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e176-384">Log in to Azure and access all the Spark clusters associated with your Azure subscriptions.</span></span></li><li><span data-ttu-id="5e176-385">瀏覽 HDInsight Spark 叢集的所有相關聯儲存體資源。</span><span class="sxs-lookup"><span data-stu-id="5e176-385">Navigate all the associated storage resources of your HDInsight Spark cluster.</span></span></li><li><span data-ttu-id="5e176-386">瀏覽 HDInsight Spark 叢集的所有作業歷程記錄和作業資訊。</span><span class="sxs-lookup"><span data-stu-id="5e176-386">Navigate all the jobs history and job information for your HDInsight Spark cluster.</span></span></li><li><span data-ttu-id="5e176-387">從桌上型電腦遠端偵錯 Spark 作業。</span><span class="sxs-lookup"><span data-stu-id="5e176-387">Debug Spark jobs remotely from your desktop computer.</span></span></li></ul> |<span data-ttu-id="5e176-388">工具</span><span class="sxs-lookup"><span data-stu-id="5e176-388">Tools</span></span> |<span data-ttu-id="5e176-389">Spark</span><span class="sxs-lookup"><span data-stu-id="5e176-389">Spark</span></span> |<span data-ttu-id="5e176-390">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-390">N/A</span></span> |

## <a name="notes-for-05132016-release-of-hdinsight"></a><span data-ttu-id="5e176-391">HDInsight 2016/05/13 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-391">Notes for 05/13/2016 release of HDInsight</span></span>
<span data-ttu-id="5e176-392">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-392">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-393">HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-393">HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-394">HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-394">HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-395">HDInsight    (Windows)         3.1.4.922.2266903  (HDP 2.1.15.0-2374 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-395">HDInsight    (Windows)         3.1.4.922.2266903  (HDP 2.1.15.0-2374 - unchanged)</span></span>
* <span data-ttu-id="5e176-396">HDInsight    (Windows)        3.2.7.922.2266903  (HDP 2.2.9.1-11)</span><span class="sxs-lookup"><span data-stu-id="5e176-396">HDInsight    (Windows)        3.2.7.922.2266903  (HDP 2.2.9.1-11)</span></span>
* <span data-ttu-id="5e176-397">HDInsight (Windows)        3.3.0.922.2266903  (HDP 2.3.3.1-18)</span><span class="sxs-lookup"><span data-stu-id="5e176-397">HDInsight (Windows)        3.3.0.922.2266903  (HDP 2.3.3.1-18)</span></span>
* <span data-ttu-id="5e176-398">HDInsight    (Linux)            3.2.1000.0.7565644   (HDP    2.2.9.1-11)</span><span class="sxs-lookup"><span data-stu-id="5e176-398">HDInsight    (Linux)            3.2.1000.0.7565644   (HDP    2.2.9.1-11)</span></span>
* <span data-ttu-id="5e176-399">HDInsight (Linux)            3.3.1000.0.7565644   (HDP 2.3.3.1-18)</span><span class="sxs-lookup"><span data-stu-id="5e176-399">HDInsight (Linux)            3.3.1000.0.7565644   (HDP 2.3.3.1-18)</span></span>
* <span data-ttu-id="5e176-400">HDInsight (Linux)            3.4.1000.0.7548380   (HDP 2.4.2.0)</span><span class="sxs-lookup"><span data-stu-id="5e176-400">HDInsight (Linux)            3.4.1000.0.7548380   (HDP 2.4.2.0)</span></span>

<span data-ttu-id="5e176-401">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-401">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-402">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-402">Title</span></span> | <span data-ttu-id="5e176-403">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-403">Description</span></span> | <span data-ttu-id="5e176-404">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-404">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-405">叢集類型 (例如 Spark、Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-405">Cluster Type (for example Spark, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-406">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-406">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-407">Spark 版本更新和其他錯誤修正</span><span class="sxs-lookup"><span data-stu-id="5e176-407">Spark version update and other bug fixes</span></span> |<span data-ttu-id="5e176-408">此版本將 HDInsight 叢集中的 Spark 版本更新至 1.6.1，並修正其他錯誤</span><span class="sxs-lookup"><span data-stu-id="5e176-408">This release updates the Spark version in HDInsight cluster to 1.6.1, and fixes other bugs</span></span> |<span data-ttu-id="5e176-409">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-409">Service</span></span> |<span data-ttu-id="5e176-410">Spark</span><span class="sxs-lookup"><span data-stu-id="5e176-410">Spark</span></span> |<span data-ttu-id="5e176-411">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-411">N/A</span></span> |

## <a name="notes-for-04112016-release-of-hdinsight"></a><span data-ttu-id="5e176-412">HDInsight 2016/04/11 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-412">Notes for 04/11/2016 release of HDInsight</span></span>
<span data-ttu-id="5e176-413">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-413">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-414">HDInsight    (Windows)         2.1.10.889.2191206 (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-414">HDInsight    (Windows)         2.1.10.889.2191206 (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-415">HDInsight    (Windows)         3.0.6.889.2191206 (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-415">HDInsight    (Windows)         3.0.6.889.2191206 (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-416">HDInsight    (Windows)         3.1.4.889.2191206  (HDP 2.1.15.0-2374 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-416">HDInsight    (Windows)         3.1.4.889.2191206  (HDP 2.1.15.0-2374 - unchanged)</span></span>
* <span data-ttu-id="5e176-417">HDInsight    (Windows)        3.2.7.889.2191206  (HDP 2.2.9.1-10)</span><span class="sxs-lookup"><span data-stu-id="5e176-417">HDInsight    (Windows)        3.2.7.889.2191206  (HDP 2.2.9.1-10)</span></span>
* <span data-ttu-id="5e176-418">HDInsight (Windows)        3.3.0.889.2191206  (HDP 2.3.3.1-16 -未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-418">HDInsight (Windows)        3.3.0.889.2191206  (HDP 2.3.3.1-16 -unchanged)</span></span>
* <span data-ttu-id="5e176-419">HDInsight    (Linux)            3.2.1000.0.7339916   (HDP 2.2.9.1-10)</span><span class="sxs-lookup"><span data-stu-id="5e176-419">HDInsight    (Linux)            3.2.1000.0.7339916   (HDP 2.2.9.1-10)</span></span>
* <span data-ttu-id="5e176-420">HDInsight (Linux)            3.3.1000.0.7339916   (HDP 2.3.3.1-16)</span><span class="sxs-lookup"><span data-stu-id="5e176-420">HDInsight (Linux)            3.3.1000.0.7339916   (HDP 2.3.3.1-16)</span></span>
* <span data-ttu-id="5e176-421">HDInsight (Linux)            3.4.1000.0.7338911   (HDP 2.4.1.1-3)</span><span class="sxs-lookup"><span data-stu-id="5e176-421">HDInsight (Linux)            3.4.1000.0.7338911   (HDP 2.4.1.1-3)</span></span>
* <span data-ttu-id="5e176-422">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-422">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-423">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-423">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-424">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-424">Title</span></span> | <span data-ttu-id="5e176-425">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-425">Description</span></span> | <span data-ttu-id="5e176-426">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-426">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-427">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-427">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-428">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-428">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-429">HDI 3.4 的自訂中繼存放區升級問題</span><span class="sxs-lookup"><span data-stu-id="5e176-429">Custom metastore upgrade issues for HDI 3.4</span></span> |<span data-ttu-id="5e176-430">如果您使用先前在另一個較低版本的 HDInsight 叢集上使用的自訂中繼存放區，則叢集會建立失敗。</span><span class="sxs-lookup"><span data-stu-id="5e176-430">Cluster creation would fail if you used a custom metastore, which was previously used on a lower version of another HDInsight cluster.</span></span> <span data-ttu-id="5e176-431">這是因為升級指令碼時發生的錯誤現在已修正</span><span class="sxs-lookup"><span data-stu-id="5e176-431">This was due to an upgrade script error that has now been fixed</span></span> |<span data-ttu-id="5e176-432">叢集建立</span><span class="sxs-lookup"><span data-stu-id="5e176-432">Cluster creation</span></span> |<span data-ttu-id="5e176-433">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-433">All</span></span> |<span data-ttu-id="5e176-434">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-434">N/A</span></span> |
| <span data-ttu-id="5e176-435">Livy Crash 復原</span><span class="sxs-lookup"><span data-stu-id="5e176-435">Livy Crash Recovery</span></span> |<span data-ttu-id="5e176-436">為所有已透過 Livy 提交的作業提供工作狀態復原</span><span class="sxs-lookup"><span data-stu-id="5e176-436">Provides job status resiliency for any job submitted through Livy</span></span> |<span data-ttu-id="5e176-437">可靠性</span><span class="sxs-lookup"><span data-stu-id="5e176-437">Reliability</span></span> |<span data-ttu-id="5e176-438">Spark on Linux</span><span class="sxs-lookup"><span data-stu-id="5e176-438">Spark on Linux</span></span> |<span data-ttu-id="5e176-439">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-439">N/A</span></span> |
| <span data-ttu-id="5e176-440">Jupyter 內容 HA</span><span class="sxs-lookup"><span data-stu-id="5e176-440">Jupyter Content HA</span></span> |<span data-ttu-id="5e176-441">提供儲存 Jupyter 筆記本內容，以及將此內容從與叢集相關的儲存體帳戶載入的功能。</span><span class="sxs-lookup"><span data-stu-id="5e176-441">Provides the ability to save and load Jupyter notebook contents to and from the storage account associated with the cluster.</span></span> <span data-ttu-id="5e176-442">如需詳細資訊，請參閱 [可供 Jupyter 筆記本使用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="5e176-442">For more information, see [Kernels available for Jupyter notebooks](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span> |<span data-ttu-id="5e176-443">筆記本</span><span class="sxs-lookup"><span data-stu-id="5e176-443">Notebooks</span></span> |<span data-ttu-id="5e176-444">Spark on Linux</span><span class="sxs-lookup"><span data-stu-id="5e176-444">Spark on Linux</span></span> |<span data-ttu-id="5e176-445">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-445">N/A</span></span> |
| <span data-ttu-id="5e176-446">移除 Jupyter 筆記本中的 hiveContext</span><span class="sxs-lookup"><span data-stu-id="5e176-446">Removal of hiveContext in Jupyter Notebooks</span></span> |<span data-ttu-id="5e176-447">使用 `%%sql` magic，而非 `%%hive` magic。</span><span class="sxs-lookup"><span data-stu-id="5e176-447">Use `%%sql` magic instead of `%%hive` magic.</span></span> <span data-ttu-id="5e176-448">SqlContext 等於 hiveContext。</span><span class="sxs-lookup"><span data-stu-id="5e176-448">SqlContext is equivalent to hiveContext.</span></span> <span data-ttu-id="5e176-449">如需詳細資訊，請參閱 [可供 Jupyter 筆記本使用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)</span><span class="sxs-lookup"><span data-stu-id="5e176-449">For more information, see [Kernels available for Jupyter notebooks](hdinsight-apache-spark-jupyter-notebook-kernels.md)</span></span> |<span data-ttu-id="5e176-450">筆記本</span><span class="sxs-lookup"><span data-stu-id="5e176-450">Notebooks</span></span> |<span data-ttu-id="5e176-451">Linux 上的 Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="5e176-451">Spark clusters on Linux</span></span> |<span data-ttu-id="5e176-452">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-452">N/A</span></span> |
| <span data-ttu-id="5e176-453">取代了舊版的 Spark</span><span class="sxs-lookup"><span data-stu-id="5e176-453">Deprecation of older Spark versions</span></span> |<span data-ttu-id="5e176-454">舊版的 Spark 1.3.1 會於 5 月 31 日從服務中移除</span><span class="sxs-lookup"><span data-stu-id="5e176-454">Older version Spark 1.3.1 was removed from the service on 5/31</span></span> |<span data-ttu-id="5e176-455">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-455">Service</span></span> |<span data-ttu-id="5e176-456">Windows 上的 Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="5e176-456">Spark clusters on Windows</span></span> |<span data-ttu-id="5e176-457">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-457">N/A</span></span> |

## <a name="notes-for-03292016-release-of-hdinsight"></a><span data-ttu-id="5e176-458">HDInsight 2016/03/29 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-458">Notes for 03/29/2016 release of HDInsight</span></span>
<span data-ttu-id="5e176-459">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-459">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-460">HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-460">HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-461">HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-461">HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-462">HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-462">HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - unchanged)</span></span>
* <span data-ttu-id="5e176-463">HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-463">HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - unchanged)</span></span>
* <span data-ttu-id="5e176-464">HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)</span><span class="sxs-lookup"><span data-stu-id="5e176-464">HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)</span></span>
* <span data-ttu-id="5e176-465">HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-465">HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - unchanged)</span></span>
* <span data-ttu-id="5e176-466">HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-466">HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - unchanged)</span></span>
* <span data-ttu-id="5e176-467">HDInsight (Linux)            3.4.1000.0.7195842   (HDP 2.4.1.0-327)</span><span class="sxs-lookup"><span data-stu-id="5e176-467">HDInsight (Linux)            3.4.1000.0.7195842   (HDP 2.4.1.0-327)</span></span>
* <span data-ttu-id="5e176-468">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-468">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-469">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-469">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-470">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-470">Title</span></span> | <span data-ttu-id="5e176-471">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-471">Description</span></span> | <span data-ttu-id="5e176-472">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-472">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-473">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-473">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-474">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-474">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-475">新增 HDInsight 3.4 版並更新所有 HDInsight 叢集的 HDP 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-475">Added HDInsight 3.4 version and updated HDP versions for all HDInsight clusters</span></span> |<span data-ttu-id="5e176-476">在此版本中，我們新增了 HDInsight v3.4 (以 HDP 2.4 為基礎) 並且更新了其他 HDP 版本。</span><span class="sxs-lookup"><span data-stu-id="5e176-476">With this release, we have added HDInsight v3.4 (based on HDP 2.4) and have also updated other HDP versions.</span></span> <span data-ttu-id="5e176-477">HDP 2.4 版本附註可在[這裡](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html)找到，而 HDInsight 版本的詳細資訊則可以在[這裡](hdinsight-component-versioning.md)找到。</span><span class="sxs-lookup"><span data-stu-id="5e176-477">HDP 2.4 release notes are available [here](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html) and more information on HDInsight versions can be found [here](hdinsight-component-versioning.md).</span></span> |<span data-ttu-id="5e176-478">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-478">Service</span></span> |<span data-ttu-id="5e176-479">所有 Linux 叢集</span><span class="sxs-lookup"><span data-stu-id="5e176-479">All Linux clusters</span></span> |<span data-ttu-id="5e176-480">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-480">N/A</span></span> |
| <span data-ttu-id="5e176-481">HDInsight Premium</span><span class="sxs-lookup"><span data-stu-id="5e176-481">HDInsight Premium</span></span> |<span data-ttu-id="5e176-482">HDInsight 現在有兩種類別：Standard 和 Premium。</span><span class="sxs-lookup"><span data-stu-id="5e176-482">HDInsight is now available in two categories - Standard and Premium.</span></span> <span data-ttu-id="5e176-483">HDInsight Premium 目前為預覽版，僅適用於 Linux 上的 Hadoop 和 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e176-483">HDInsight Premium is currently in Preview and available only for Hadoop and Spark clusters on Linux.</span></span> <span data-ttu-id="5e176-484">如需詳細資訊，請參閱[這裡](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)。</span><span class="sxs-lookup"><span data-stu-id="5e176-484">For more information, see [here](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).</span></span> |<span data-ttu-id="5e176-485">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-485">Service</span></span> |<span data-ttu-id="5e176-486">Linux 上的 Hadoop 和 Spark</span><span class="sxs-lookup"><span data-stu-id="5e176-486">Hadoop and Spark on Linux</span></span> |<span data-ttu-id="5e176-487">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-487">N/A</span></span> |
| <span data-ttu-id="5e176-488">Microsoft R 伺服器</span><span class="sxs-lookup"><span data-stu-id="5e176-488">Microsoft R Server</span></span> |<span data-ttu-id="5e176-489">HDInsight Premium 提供 Microsoft R 伺服器，它可以隨附於 Linux 上的 Hadoop 與 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e176-489">HDInsight Premium provides Microsoft R Server that can be included with Hadoop and Spark clusters on Linux.</span></span> <span data-ttu-id="5e176-490">如需詳細資訊，請參閱 [HDInsight 中的 R 伺服器概觀](hdinsight-hadoop-r-server-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5e176-490">For more information, see [Overview of R Server on HDInsight](hdinsight-hadoop-r-server-overview.md).</span></span> |<span data-ttu-id="5e176-491">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-491">Service</span></span> |<span data-ttu-id="5e176-492">Linux 上的 Hadoop 和 Spark</span><span class="sxs-lookup"><span data-stu-id="5e176-492">Hadoop and Spark on Linux</span></span> |<span data-ttu-id="5e176-493">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-493">N/A</span></span> |
| <span data-ttu-id="5e176-494">Spark 1.6.0</span><span class="sxs-lookup"><span data-stu-id="5e176-494">Spark 1.6.0</span></span> |<span data-ttu-id="5e176-495">HDInsight 3.4 叢集現在包含 Spark 1.6.0</span><span class="sxs-lookup"><span data-stu-id="5e176-495">HDInsight 3.4 clusters now include Spark 1.6.0</span></span> |<span data-ttu-id="5e176-496">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-496">Service</span></span> |<span data-ttu-id="5e176-497">Linux 上的 Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="5e176-497">Spark clusters on Linux</span></span> |<span data-ttu-id="5e176-498">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-498">N/A</span></span> |
| <span data-ttu-id="5e176-499">Jupyter Notebook 增強功能</span><span class="sxs-lookup"><span data-stu-id="5e176-499">Jupyter notebook enhancements</span></span> |<span data-ttu-id="5e176-500">可用於 Spark 叢集的 Jupyter Nnotebook 現在提供額外的 Spark 核心。</span><span class="sxs-lookup"><span data-stu-id="5e176-500">Jupyter notebooks available with Spark clusters now provide additional Spark kernels.</span></span> <span data-ttu-id="5e176-501">其中也包括增強功能，例如使用 %%magic、自動視覺化，以及與 Python 視覺化程式庫 (例如 matplotlib) 整合。</span><span class="sxs-lookup"><span data-stu-id="5e176-501">They also include enhancements like use of %%magic, auto-visualization, and integration with Python visualization libraries (such as matplotlib).</span></span> <span data-ttu-id="5e176-502">如需詳細資訊，請參閱 [可供 Jupyter 筆記本使用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="5e176-502">For more information, see [Kernels available for Jupyter notebooks](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span> |<span data-ttu-id="5e176-503">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-503">Service</span></span> |<span data-ttu-id="5e176-504">Linux 上的 Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="5e176-504">Spark clusters on Linux</span></span> |<span data-ttu-id="5e176-505">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-505">N/A</span></span> |

## <a name="notes-for-03222016-release-of-hdinsight"></a><span data-ttu-id="5e176-506">HDInsight 2016/03/22 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-506">Notes for 03/22/2016 release of HDInsight</span></span>
<span data-ttu-id="5e176-507">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-507">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-508">HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-508">HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-509">HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-509">HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-510">HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-510">HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - unchanged)</span></span>
* <span data-ttu-id="5e176-511">HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-511">HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - unchanged)</span></span>
* <span data-ttu-id="5e176-512">HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)</span><span class="sxs-lookup"><span data-stu-id="5e176-512">HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)</span></span>
* <span data-ttu-id="5e176-513">HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-513">HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - unchanged)</span></span>
* <span data-ttu-id="5e176-514">HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-514">HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - unchanged)</span></span>
* <span data-ttu-id="5e176-515">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-515">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-516">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-516">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-517">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-517">Title</span></span> | <span data-ttu-id="5e176-518">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-518">Description</span></span> | <span data-ttu-id="5e176-519">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-519">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-520">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-520">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-521">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-521">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-522">更新所有 HDInsight 叢集的 HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-522">Updated HDInsight versions for all HDInsight clusters</span></span> |<span data-ttu-id="5e176-523">在此版本中，我們已更新所有 HDInsight 叢集的 HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-523">With this release, we have updated HDInsight versions for all HDInsight clusters</span></span> |<span data-ttu-id="5e176-524">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-524">Service</span></span> |<span data-ttu-id="5e176-525">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-525">All</span></span> |<span data-ttu-id="5e176-526">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-526">N/A</span></span> |

## <a name="notes-for-03102016-release-of-hdinsight"></a><span data-ttu-id="5e176-527">HDInsight 2016/03/10 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-527">Notes for 03/10/2016 release of HDInsight</span></span>
<span data-ttu-id="5e176-528">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-528">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-529">HDInsight    (Windows)         2.1.10.859.2123216 (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-529">HDInsight    (Windows)         2.1.10.859.2123216 (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-530">HDInsight    (Windows)         3.0.6.859.2123216 (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-530">HDInsight    (Windows)         3.0.6.859.2123216 (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-531">HDInsight    (Windows)         3.1.4.859.2123216  (HDP 2.1.15.0-2374 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-531">HDInsight    (Windows)         3.1.4.859.2123216  (HDP 2.1.15.0-2374 - unchanged)</span></span>
* <span data-ttu-id="5e176-532">HDInsight    (Windows)        3.2.7.859.2123216  (HDP 2.2.9.1-7)</span><span class="sxs-lookup"><span data-stu-id="5e176-532">HDInsight    (Windows)        3.2.7.859.2123216  (HDP 2.2.9.1-7)</span></span>
* <span data-ttu-id="5e176-533">HDInsight (Windows)        3.3.0.859.2123216  (HDP 2.3.3.1-5 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-533">HDInsight (Windows)        3.3.0.859.2123216  (HDP 2.3.3.1-5 - unchanged)</span></span>
* <span data-ttu-id="5e176-534">HDInsight    (Linux)            3.2.1000.7076817   (HDP    2.2.9.1-8)</span><span class="sxs-lookup"><span data-stu-id="5e176-534">HDInsight    (Linux)            3.2.1000.7076817   (HDP    2.2.9.1-8)</span></span>
* <span data-ttu-id="5e176-535">HDInsight (Linux)            3.3.1000.7076817   (HDP 2.3.3.1-7)</span><span class="sxs-lookup"><span data-stu-id="5e176-535">HDInsight (Linux)            3.3.1000.7076817   (HDP 2.3.3.1-7)</span></span>
* <span data-ttu-id="5e176-536">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-536">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-537">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-537">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-538">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-538">Title</span></span> | <span data-ttu-id="5e176-539">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-539">Description</span></span> | <span data-ttu-id="5e176-540">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-540">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-541">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-541">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-542">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-542">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-543">更新所有 HDInsight 叢集的 HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-543">Updated HDInsight versions for all HDInsight clusters</span></span> |<span data-ttu-id="5e176-544">在此版本中，我們已更新所有 HDInsight 叢集的 HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-544">With this release, we have updated HDInsight versions for all HDInsight clusters</span></span> |<span data-ttu-id="5e176-545">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-545">Service</span></span> |<span data-ttu-id="5e176-546">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-546">All</span></span> |<span data-ttu-id="5e176-547">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-547">N/A</span></span> |

## <a name="notes-for-01272016-release-of-hdinsight"></a><span data-ttu-id="5e176-548">HDInsight 2016/01/27 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-548">Notes for 01/27/2016 release of HDInsight</span></span>
<span data-ttu-id="5e176-549">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-549">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-550">HDInsight    (Windows)         2.1.10.817.2028315 (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-550">HDInsight    (Windows)         2.1.10.817.2028315 (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-551">HDInsight    (Windows)         3.0.6.817.2028315 (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-551">HDInsight    (Windows)         3.0.6.817.2028315 (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-552">HDInsight    (Windows)         3.1.4.817.2028315  (HDP 2.1.15.0-2374 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-552">HDInsight    (Windows)         3.1.4.817.2028315  (HDP 2.1.15.0-2374 - unchanged)</span></span>
* <span data-ttu-id="5e176-553">HDInsight    (Windows)        3.2.7.817.2028315  (HDP 2.2.9.1-1)</span><span class="sxs-lookup"><span data-stu-id="5e176-553">HDInsight    (Windows)        3.2.7.817.2028315  (HDP 2.2.9.1-1)</span></span>
* <span data-ttu-id="5e176-554">HDInsight (Windows)        3.3.0.817.2028315  (HDP 2.3.3.1-5 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-554">HDInsight (Windows)        3.3.0.817.2028315  (HDP 2.3.3.1-5 - unchanged)</span></span>
* <span data-ttu-id="5e176-555">HDInsight    (Linux)            3.2.1000.4072335   (HDP    2.2.9.1-1)</span><span class="sxs-lookup"><span data-stu-id="5e176-555">HDInsight    (Linux)            3.2.1000.4072335   (HDP    2.2.9.1-1)</span></span>
* <span data-ttu-id="5e176-556">HDInsight (Linux)            3.3.1000.4072335   (HDP 2.3.3.1-1)</span><span class="sxs-lookup"><span data-stu-id="5e176-556">HDInsight (Linux)            3.3.1000.4072335   (HDP 2.3.3.1-1)</span></span>
* <span data-ttu-id="5e176-557">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-557">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-558">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-558">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-559">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-559">Title</span></span> | <span data-ttu-id="5e176-560">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-560">Description</span></span> | <span data-ttu-id="5e176-561">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-561">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-562">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-562">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-563">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-563">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-564">更新所有 HDInsight 叢集的 HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-564">Updated HDInsight versions for all HDInsight clusters</span></span> |<span data-ttu-id="5e176-565">在此版本中，我們已更新所有 HDInsight 叢集的 HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-565">With this release, we have updated HDInsight versions for all HDInsight clusters</span></span> |<span data-ttu-id="5e176-566">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-566">Service</span></span> |<span data-ttu-id="5e176-567">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-567">All</span></span> |<span data-ttu-id="5e176-568">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-568">N/A</span></span> |

## <a name="notes-for-12022015-release-of-hdinsight"></a><span data-ttu-id="5e176-569">HDInsight 2015/12/02 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-569">Notes for 12/02/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-570">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-570">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-571">HDInsight    (Windows)         2.1.10.763.1931434 (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-571">HDInsight    (Windows)         2.1.10.763.1931434 (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-572">HDInsight    (Windows)         3.0.6.763.1931434 (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-572">HDInsight    (Windows)         3.0.6.763.1931434 (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-573">HDInsight    (Windows)         3.1.4.763.1931434  (HDP 2.1.15.0-2374 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-573">HDInsight    (Windows)         3.1.4.763.1931434  (HDP 2.1.15.0-2374 - unchanged)</span></span>
* <span data-ttu-id="5e176-574">HDInsight    (Windows)        3.2.7.763.1931434  (HDP 2.2.7.1-34 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-574">HDInsight    (Windows)        3.2.7.763.1931434  (HDP 2.2.7.1-34 - unchanged)</span></span>
* <span data-ttu-id="5e176-575">HDInsight (Windows)        3.3.1000.0           (HDP 2.3.3.1-5)</span><span class="sxs-lookup"><span data-stu-id="5e176-575">HDInsight (Windows)        3.3.1000.0           (HDP 2.3.3.1-5)</span></span>
* <span data-ttu-id="5e176-576">HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-576">HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34 - unchanged)</span></span>
* <span data-ttu-id="5e176-577">HDInsight (Linux)            3.3.1000.0           (HDP 2.3.3.0-3039)</span><span class="sxs-lookup"><span data-stu-id="5e176-577">HDInsight (Linux)            3.3.1000.0           (HDP 2.3.3.0-3039)</span></span>
* <span data-ttu-id="5e176-578">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-578">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-579">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-579">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-580">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-580">Title</span></span> | <span data-ttu-id="5e176-581">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-581">Description</span></span> | <span data-ttu-id="5e176-582">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-582">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-583">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-583">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-584">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-584">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-585">新增 HDInsight 3.3 版並更新所有 HDInsight 叢集的 HDP 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-585">Added HDInsight 3.3 version and updated HDP versions for all HDInsight clusters</span></span> |<span data-ttu-id="5e176-586">在此版本中，我們新增了 HDInsight v3.3 (以 HDP 2.3 為基礎) 並且更新了其他 HDP 版本。</span><span class="sxs-lookup"><span data-stu-id="5e176-586">With this release, we have added HDInsight v3.3 (based on HDP 2.3) and have also updated other HDP versions.</span></span> <span data-ttu-id="5e176-587">HDP 2.3 版本附註可在[這裡](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html)找到，而 HDInsight 版本的詳細資訊則可以在[這裡](hdinsight-component-versioning.md)找到。</span><span class="sxs-lookup"><span data-stu-id="5e176-587">HDP 2.3 release notes are available [here](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html) and more information on HDInsight versions can be found [here](hdinsight-component-versioning.md).</span></span> |<span data-ttu-id="5e176-588">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-588">Service</span></span> |<span data-ttu-id="5e176-589">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-589">All</span></span> |<span data-ttu-id="5e176-590">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-590">N/A</span></span> |

## <a name="notes-for-11302015-release-of-hdinsight"></a><span data-ttu-id="5e176-591">HDInsight 2015/11/30 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-591">Notes for 11/30/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-592">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-592">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-593">HDInsight    (Windows)         2.1.10.757.1923908 (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-593">HDInsight    (Windows)         2.1.10.757.1923908 (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-594">HDInsight    (Windows)         3.0.6.757.1923908  (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-594">HDInsight    (Windows)         3.0.6.757.1923908  (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-595">HDInsight    (Windows)         3.1.4.757.1923908  (HDP 2.1.15.0-2374 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-595">HDInsight    (Windows)         3.1.4.757.1923908  (HDP 2.1.15.0-2374 - unchanged)</span></span>
* <span data-ttu-id="5e176-596">HDInsight    (Windows)        3.2.7.757.1923908  (HDP 2.2.7.1-34)</span><span class="sxs-lookup"><span data-stu-id="5e176-596">HDInsight    (Windows)        3.2.7.757.1923908  (HDP 2.2.7.1-34)</span></span>
* <span data-ttu-id="5e176-597">HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34)</span><span class="sxs-lookup"><span data-stu-id="5e176-597">HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34)</span></span>
* <span data-ttu-id="5e176-598">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-598">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-599">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-599">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-600">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-600">Title</span></span> | <span data-ttu-id="5e176-601">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-601">Description</span></span> | <span data-ttu-id="5e176-602">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-602">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-603">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-603">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-604">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-604">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-605">所有 HDInsight 叢集的已更新 HDInsight 版本和 HDInsight 3.2 叢集的 HDP 版本 (Windows 和 Linux)</span><span class="sxs-lookup"><span data-stu-id="5e176-605">Updated HDInsight versions for all HDInsight clusters and HDP versions for HDInsight 3.2 clusters (Windows and Linux)</span></span> |<span data-ttu-id="5e176-606">在此版本中，HDInsight 和 HDP 版本均已更新</span><span class="sxs-lookup"><span data-stu-id="5e176-606">With this release, HDInsight and HDP versions have been updated</span></span> |<span data-ttu-id="5e176-607">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-607">Service</span></span> |<span data-ttu-id="5e176-608">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-608">All</span></span> |<span data-ttu-id="5e176-609">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-609">N/A</span></span> |

## <a name="notes-for-10272015-release-of-hdinsight"></a><span data-ttu-id="5e176-610">HDInsight 2015/10/27 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-610">Notes for 10/27/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-611">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-611">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-612">HDInsight    (Windows)         2.1.10.726.1866228 (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-612">HDInsight    (Windows)         2.1.10.726.1866228 (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-613">HDInsight    (Windows)         3.0.6.726.1866228  (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-613">HDInsight    (Windows)         3.0.6.726.1866228  (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-614">HDInsight    (Windows)         3.1.4.726.1866228  (HDP 2.1.15.0-2374 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-614">HDInsight    (Windows)         3.1.4.726.1866228  (HDP 2.1.15.0-2374 - unchanged)</span></span>
* <span data-ttu-id="5e176-615">HDInsight    (Windows)        3.2.7.726.1866228  (HDP 2.2.7.1-33)</span><span class="sxs-lookup"><span data-stu-id="5e176-615">HDInsight    (Windows)        3.2.7.726.1866228  (HDP 2.2.7.1-33)</span></span>
* <span data-ttu-id="5e176-616">HDInsight    (Linux)            3.2.1000.0.6035701 (HDP    2.2.7.1-33)</span><span class="sxs-lookup"><span data-stu-id="5e176-616">HDInsight    (Linux)            3.2.1000.0.6035701 (HDP    2.2.7.1-33)</span></span>
* <span data-ttu-id="5e176-617">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-617">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-618">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-618">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-619">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-619">Title</span></span> | <span data-ttu-id="5e176-620">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-620">Description</span></span> | <span data-ttu-id="5e176-621">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-621">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-622">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-622">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-623">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-623">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-624">更新所有 HDInsight 叢集的 HDInsight 版本 (Windows 和 Linux)</span><span class="sxs-lookup"><span data-stu-id="5e176-624">Updated HDInsight versions for all HDInsight clusters (Windows and Linux)</span></span> |<span data-ttu-id="5e176-625">在此版本中，HDInsight 和 HDP 版本均已更新</span><span class="sxs-lookup"><span data-stu-id="5e176-625">With this release, HDInsight and HDP versions have been updated</span></span> |<span data-ttu-id="5e176-626">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-626">Service</span></span> |<span data-ttu-id="5e176-627">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-627">All</span></span> |<span data-ttu-id="5e176-628">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-628">N/A</span></span> |
| <span data-ttu-id="5e176-629">修正包含大寫字母叢集之 Windows Spark 叢集的 Jupyter</span><span class="sxs-lookup"><span data-stu-id="5e176-629">Fixed Jupyter for Windows Spark clusters with capital letters clusters</span></span> |<span data-ttu-id="5e176-630">以大寫字母指定 DNS 名稱的叢集，會因為原始要求檢查的緣故而使 Jupyter 筆記本發生問題。</span><span class="sxs-lookup"><span data-stu-id="5e176-630">Clusters that had DNS names specified in capital letters had issues with Jupyter notebooks due to an origin request check.</span></span> <span data-ttu-id="5e176-631">此修正是要將 Jupyter 之設定的 DNS 名稱變更為小寫。</span><span class="sxs-lookup"><span data-stu-id="5e176-631">The fix was to change the DNS name for Jupyter's configuration to lower case.</span></span> |<span data-ttu-id="5e176-632">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-632">Service</span></span> |<span data-ttu-id="5e176-633">HDInsight Spark (Windows)</span><span class="sxs-lookup"><span data-stu-id="5e176-633">HDInsight Spark (Windows)</span></span> |<span data-ttu-id="5e176-634">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-634">N/A</span></span> |

## <a name="notes-for-10202015-release-of-hdinsight"></a><span data-ttu-id="5e176-635">HDInsight 2015/10/20 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-635">Notes for 10/20/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-636">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-636">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-637">HDInsight     2.1.10.716.1846990 (Windows)    (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-637">HDInsight     2.1.10.716.1846990 (Windows)    (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-638">HDInsight     3.0.6.716.1846990 (Windows)      (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-638">HDInsight     3.0.6.716.1846990 (Windows)      (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-639">HDInsight     3.1.4.716.1846990 (Windows)      (HDP 2.1.16.0-2374)</span><span class="sxs-lookup"><span data-stu-id="5e176-639">HDInsight     3.1.4.716.1846990 (Windows)      (HDP 2.1.16.0-2374)</span></span>
* <span data-ttu-id="5e176-640">HDInsight        3.2.7.716.1846990 (Windows)      (HDP 2.2.7.1-0004)</span><span class="sxs-lookup"><span data-stu-id="5e176-640">HDInsight        3.2.7.716.1846990 (Windows)      (HDP 2.2.7.1-0004)</span></span>
* <span data-ttu-id="5e176-641">HDInsight        3.2.1000.0.5930166 (Linux)        (HDP 2.2.7.1-0004)</span><span class="sxs-lookup"><span data-stu-id="5e176-641">HDInsight        3.2.1000.0.5930166 (Linux)        (HDP 2.2.7.1-0004)</span></span>
* <span data-ttu-id="5e176-642">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-642">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-643">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-643">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-644">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-644">Title</span></span> | <span data-ttu-id="5e176-645">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-645">Description</span></span> | <span data-ttu-id="5e176-646">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-646">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-647">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-647">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-648">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-648">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-649">變更為 HDP 2.2 的預設版本 HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-649">Default HDP version changed to HDP 2.2</span></span> |<span data-ttu-id="5e176-650">HDInsight Windows 叢集的預設版本變更為 HDP 2.2。</span><span class="sxs-lookup"><span data-stu-id="5e176-650">The default version for HDInsight Windows clusters is changed to HDP 2.2.</span></span> <span data-ttu-id="5e176-651">HDInsight 版本 3.2 (HDP 2.2) 自 2015 年 2 月已在公開上市。</span><span class="sxs-lookup"><span data-stu-id="5e176-651">HDInsight version 3.2 (HDP 2.2) has been generally available in since February 2015.</span></span> <span data-ttu-id="5e176-652">這項變更只會在使用 Azure 入口網站、PowerShell Cmdlet 或 SDK 叢集佈建的同時未進行明確選擇時，翻轉預設叢集版本。</span><span class="sxs-lookup"><span data-stu-id="5e176-652">This change only flips the default cluster version, when an explicit selection has not been made while provisioning the cluster using the Azure portal, PowerShell cmdlets, or the SDK.</span></span> |<span data-ttu-id="5e176-653">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-653">Service</span></span> |<span data-ttu-id="5e176-654">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-654">All</span></span> |<span data-ttu-id="5e176-655">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-655">N/A</span></span> |
| <span data-ttu-id="5e176-656">變更 VM 名稱格式以在單一虛擬網路中的 Linux 叢集上部署多個 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="5e176-656">Changes in VM name format for deploying multiple HDInsight on Linux clusters in a single Virtual Network</span></span> |<span data-ttu-id="5e176-657">在這個版本中已加入在單一虛擬網路中部署多個 HDInsight Linux 叢集的支援。</span><span class="sxs-lookup"><span data-stu-id="5e176-657">Support for deploying multiple HDInsight Linux clusters in a single virtual network is being added in this release.</span></span> <span data-ttu-id="5e176-658">隨著更新，叢集的虛擬機器名稱的格式已從 headnode\*、workernode\* 和 zookeepernode\* 分別變更為 hn\*、wn\* 和 zk\*。</span><span class="sxs-lookup"><span data-stu-id="5e176-658">As part of update, the format of virtual machine names in the cluster has changed from headnode\*, workernode\* and zookeepernode\* to hn\*, wn\*, and zk\* respectively.</span></span> <span data-ttu-id="5e176-659">不建議採取虛擬機器名稱格式的直接相依性，因為這樣會受限於變更。</span><span class="sxs-lookup"><span data-stu-id="5e176-659">It is not a recommended practice to take a direct dependency on the format of virtual machine names, since this is subject to change.</span></span> <span data-ttu-id="5e176-660">請使用本機機器或 Ambari API 上的 "hostname -f" 以判斷主機清單和元件到主機的對應。</span><span class="sxs-lookup"><span data-stu-id="5e176-660">Use "hostname -f" on the local machine or Ambari APIs to determine the list of hosts, and the mapping of components to hosts.</span></span> <span data-ttu-id="5e176-661">您可以在 [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md) 和 [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md) 找到更多資訊。</span><span class="sxs-lookup"><span data-stu-id="5e176-661">You can find more info at [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md) and [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md).</span></span> |<span data-ttu-id="5e176-662">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-662">Service</span></span> |<span data-ttu-id="5e176-663">Linux 上的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="5e176-663">HDInsight clusters on Linux</span></span> |<span data-ttu-id="5e176-664">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-664">N/A</span></span> |
| <span data-ttu-id="5e176-665">組態變更</span><span class="sxs-lookup"><span data-stu-id="5e176-665">Configuration changes</span></span> |<span data-ttu-id="5e176-666">對於 HDInsight 3.1 叢集，現在會啟用下列組態︰</span><span class="sxs-lookup"><span data-stu-id="5e176-666">For HDInsight 3.1 clusters, the following configurations are now enabled:</span></span> <ul><li><span data-ttu-id="5e176-667">tez.yarn.ats.enabled 和 yarn.log.server.url。</span><span class="sxs-lookup"><span data-stu-id="5e176-667">tez.yarn.ats.enabled and yarn.log.server.url.</span></span> <span data-ttu-id="5e176-668">這可讓應用程式時間軸伺服器和記錄伺服器能夠提供記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5e176-668">This enables the Application Timeline Server and the Log server to be able to serve out logs.</span></span></li></ul><span data-ttu-id="5e176-669">對於 HDInsight 3.2 叢集，已經修改下列組態：</span><span class="sxs-lookup"><span data-stu-id="5e176-669">For HDInsight 3.2 clusters, the following configurations have been modified:</span></span> <ul><li><span data-ttu-id="5e176-670">mapreduce.fileoutputcommitter.algorithm.version 已設為 2。</span><span class="sxs-lookup"><span data-stu-id="5e176-670">mapreduce.fileoutputcommitter.algorithm.version has been set to 2.</span></span> <span data-ttu-id="5e176-671">這樣就可以使用 FileOutputCommitter 的 V2 版本。</span><span class="sxs-lookup"><span data-stu-id="5e176-671">This enables use of the V2 version of the FileOutputCommitter.</span></span></li></ul> |<span data-ttu-id="5e176-672">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-672">Service</span></span> |<span data-ttu-id="5e176-673">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-673">All</span></span> |<span data-ttu-id="5e176-674">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-674">N/A</span></span> |

## <a name="notes-for-09092015-release-of-hdinsight"></a><span data-ttu-id="5e176-675">HDInsight 2015/09/09 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-675">Notes for 09/09/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-676">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-676">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-677">HDInsight     2.1.10.675.1768697 (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-677">HDInsight     2.1.10.675.1768697 (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-678">HDInsight     3.0.6.675.1768697  (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-678">HDInsight     3.0.6.675.1768697  (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-679">HDInsight     3.1.4.675.1768697  (HDP 2.1.15.0-2334 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-679">HDInsight     3.1.4.675.1768697  (HDP 2.1.15.0-2334 - unchanged)</span></span>
* <span data-ttu-id="5e176-680">HDInsight        3.2.6.675.1768697  (HDP 2.2.6.1-0012 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-680">HDInsight        3.2.6.675.1768697  (HDP 2.2.6.1-0012 - unchanged)</span></span>
* <span data-ttu-id="5e176-681">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-681">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-682">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-682">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-683">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-683">Title</span></span> | <span data-ttu-id="5e176-684">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-684">Description</span></span> | <span data-ttu-id="5e176-685">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-685">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-686">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-686">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-687">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-687">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-688">更新所有 HDInsight 叢集的 HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-688">Updated HDInsight versions for all HDInsight clusters</span></span> |<span data-ttu-id="5e176-689">在此版本中，HDInsight 版本已更新</span><span class="sxs-lookup"><span data-stu-id="5e176-689">With this release, HDInsight versions have been updated</span></span> |<span data-ttu-id="5e176-690">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-690">Service</span></span> |<span data-ttu-id="5e176-691">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-691">All</span></span> |<span data-ttu-id="5e176-692">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-692">N/A</span></span> |

## <a name="notes-for-07312015-release-of-hdinsight"></a><span data-ttu-id="5e176-693">HDInsight 2015/07/31 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-693">Notes for 07/31/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-694">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-694">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-695">HDInsight     2.1.10.640.1695824 (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-695">HDInsight     2.1.10.640.1695824 (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-696">HDInsight     3.0.6.640.1695824  (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-696">HDInsight     3.0.6.640.1695824  (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-697">HDInsight     3.1.4.640.1695824  (HDP 2.1.15.0-2334 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-697">HDInsight     3.1.4.640.1695824  (HDP 2.1.15.0-2334 - unchanged)</span></span>
* <span data-ttu-id="5e176-698">HDInsight        3.2.6.640.1695824  (HDP 2.2.6.1-0012 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-698">HDInsight        3.2.6.640.1695824  (HDP 2.2.6.1-0012 - unchanged)</span></span>
* <span data-ttu-id="5e176-699">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-699">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-700">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-700">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-701">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-701">Title</span></span> | <span data-ttu-id="5e176-702">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-702">Description</span></span> | <span data-ttu-id="5e176-703">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-703">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-704">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-704">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-705">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-705">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-706">修正 Spark 叢集節點的重新製作映像工作流程</span><span class="sxs-lookup"><span data-stu-id="5e176-706">Fix Spark cluster node reimaging workflow</span></span> |<span data-ttu-id="5e176-707">修正造成 Spark 叢集節點重新製作映像後不復原的錯誤</span><span class="sxs-lookup"><span data-stu-id="5e176-707">Fixed a bug that was causing Spark cluster nodes to not recover after reimage</span></span> |<span data-ttu-id="5e176-708">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-708">Service</span></span> |<span data-ttu-id="5e176-709">Spark</span><span class="sxs-lookup"><span data-stu-id="5e176-709">Spark</span></span> |<span data-ttu-id="5e176-710">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-710">N/A</span></span> |

## <a name="notes-for-07312015-release-of-hdinsight"></a><span data-ttu-id="5e176-711">HDInsight 2015/07/31 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-711">Notes for 07/31/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-712">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-712">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-713">HDInsight     2.1.10.635.1684502 (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-713">HDInsight     2.1.10.635.1684502 (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-714">HDInsight     3.0.6.635.1684502  (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-714">HDInsight     3.0.6.635.1684502  (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-715">HDInsight     3.1.4.635.1684502  (HDP 2.1.15.0-2334 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-715">HDInsight     3.1.4.635.1684502  (HDP 2.1.15.0-2334 - unchanged)</span></span>
* <span data-ttu-id="5e176-716">HDInsight        3.2.6.635.1684502  (HDP 2.2.6.1-0012 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-716">HDInsight        3.2.6.635.1684502  (HDP 2.2.6.1-0012 - unchanged)</span></span>
* <span data-ttu-id="5e176-717">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-717">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-718">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-718">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-719">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-719">Title</span></span> | <span data-ttu-id="5e176-720">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-720">Description</span></span> | <span data-ttu-id="5e176-721">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-721">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-722">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-722">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-723">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-723">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-724">更新所有 HDInsight 叢集的 HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-724">Updated HDInsight versions for all HDInsight clusters</span></span> |<span data-ttu-id="5e176-725">在此版本中，HDInsight 版本已更新</span><span class="sxs-lookup"><span data-stu-id="5e176-725">With this release, HDInsight versions have been updated</span></span> |<span data-ttu-id="5e176-726">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-726">Service</span></span> |<span data-ttu-id="5e176-727">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-727">All</span></span> |<span data-ttu-id="5e176-728">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-728">N/A</span></span> |

## <a name="notes-for-07072015-release-of-hdinsight"></a><span data-ttu-id="5e176-729">HDInsight 2015/07/07 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-729">Notes for 07/07/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-730">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-730">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-731">HDInsight     2.1.10.610.1630216    (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-731">HDInsight     2.1.10.610.1630216    (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-732">HDInsight     3.0.6.610.1630216    (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-732">HDInsight     3.0.6.610.1630216    (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-733">HDInsight     3.1.4.610.1630216    (HDP 2.1.15.0-2334 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-733">HDInsight     3.1.4.610.1630216    (HDP 2.1.15.0-2334 - unchanged)</span></span>
* <span data-ttu-id="5e176-734">HDInsight        3.2.4.610.1630216    (HDP 2.2.6.1-0012)</span><span class="sxs-lookup"><span data-stu-id="5e176-734">HDInsight        3.2.4.610.1630216    (HDP 2.2.6.1-0012)</span></span>
* <span data-ttu-id="5e176-735">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-735">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-736">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-736">This release contains the following updates:</span></span>

| <span data-ttu-id="5e176-737">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-737">Title</span></span> | <span data-ttu-id="5e176-738">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-738">Description</span></span> | <span data-ttu-id="5e176-739">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-739">Impacted Area (for example, Service, component, or SDK)</span></span> | <span data-ttu-id="5e176-740">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-740">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span> | <span data-ttu-id="5e176-741">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-741">JIRA (if applicable)</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5e176-742">HDInsight 3.2 叢集的更新後 HDP 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-742">Updated HDP versions for HDInsight 3.2 clusters</span></span> |<span data-ttu-id="5e176-743">在此版本中，HDInsight 3.2 會部署 HDP 2.2.6.1-0012</span><span class="sxs-lookup"><span data-stu-id="5e176-743">With this release, HDInsight 3.2 deploys HDP 2.2.6.1-0012</span></span> |<span data-ttu-id="5e176-744">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-744">Service</span></span> |<span data-ttu-id="5e176-745">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-745">All</span></span> |<span data-ttu-id="5e176-746">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-746">N/A</span></span> |

## <a name="notes-for-06262015-release-of-hdinsight"></a><span data-ttu-id="5e176-747">HDInsight 2015/06/26 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-747">Notes for 06/26/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-748">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-748">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-749">HDInsight     2.1.10.601.1610731    (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-749">HDInsight     2.1.10.601.1610731    (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-750">HDInsight     3.0.6.601.1610731    (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-750">HDInsight     3.0.6.601.1610731    (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-751">HDInsight     3.1.4.601.1610731    (HDP 2.1.15.0-2334 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-751">HDInsight     3.1.4.601.1610731    (HDP 2.1.15.0-2334 - unchanged)</span></span>
* <span data-ttu-id="5e176-752">HDInsight        3.2.4.601.1610731    (HDP 2.2.6.1-0011)</span><span class="sxs-lookup"><span data-stu-id="5e176-752">HDInsight        3.2.4.601.1610731    (HDP 2.2.6.1-0011)</span></span>
* <span data-ttu-id="5e176-753">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-753">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-754">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-754">This release contains the following updates:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-755">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-755">Title</span></span></th>
<th><span data-ttu-id="5e176-756">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-756">Description</span></span></th>
<th><span data-ttu-id="5e176-757">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-757">Impacted Area (for example, Service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-758">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-758">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-759">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-759">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-760">HDInsight 3.2 叢集的更新後 HDP 版本</span><span class="sxs-lookup"><span data-stu-id="5e176-760">Updated HDP versions for HDInsight 3.2 clusters</span></span></td>
<td><span data-ttu-id="5e176-761">在此版本中，HDInsight 3.2 會部署 HDP 2.2.6.1</span><span class="sxs-lookup"><span data-stu-id="5e176-761">With this release, HDInsight 3.2 deploys HDP 2.2.6.1</span></span></td>
<td><span data-ttu-id="5e176-762">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-762">Service</span></span></td>
<td><span data-ttu-id="5e176-763">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-763">All</span></span></td>
<td><span data-ttu-id="5e176-764">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-764">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-06182015-release-of-hdinsight"></a><span data-ttu-id="5e176-765">HDInsight 2015/06/18 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-765">Notes for 06/18/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-766">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-766">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-767">HDInsight     2.1.10.596.1601657    (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-767">HDInsight     2.1.10.596.1601657    (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-768">HDInsight     3.0.6.596.1601657    (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-768">HDInsight     3.0.6.596.1601657    (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-769">HDInsight     3.1.4.596.1601657    (HDP 2.1.15.0-2334)</span><span class="sxs-lookup"><span data-stu-id="5e176-769">HDInsight     3.1.4.596.1601657    (HDP 2.1.15.0-2334)</span></span>
* <span data-ttu-id="5e176-770">HDInsight        3.2.4.596.1601657    (HDP 2.2.6.1-0002)</span><span class="sxs-lookup"><span data-stu-id="5e176-770">HDInsight        3.2.4.596.1601657    (HDP 2.2.6.1-0002)</span></span>
* <span data-ttu-id="5e176-771">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-771">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-772">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-772">This release contains the following updates:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-773">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-773">Title</span></span></th>
<th><span data-ttu-id="5e176-774">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-774">Description</span></span></th>
<th><span data-ttu-id="5e176-775">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-775">Impacted Area (for example, Service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-776">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-776">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-777">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-777">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-778">其他開啟的 HTTPS 連接埠</span><span class="sxs-lookup"><span data-stu-id="5e176-778">Additional HTTPS ports opened</span></span></td>
<td><span data-ttu-id="5e176-779">雲端服務現在會開啟叢集上的 5 個連接埠 (8001 至 8005)，例如</span><span class="sxs-lookup"><span data-stu-id="5e176-779">The cloud service now opens 5 ports 8001 to 8005 on the cluster E.g.</span></span> <span data-ttu-id="5e176-780">https://<clustername>.azurehdinsight.net:8001/。</span><span class="sxs-lookup"><span data-stu-id="5e176-780">at https://<clustername>.azurehdinsight.net:8001/.</span></span> <span data-ttu-id="5e176-781">對這些 URL 的要求會使用相同的基本驗證密碼機制驗證做為連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="5e176-781">Requests to these URLs are authenticated using the same basic authentication password mechanism as port 443.</span></span> <span data-ttu-id="5e176-782">這些連接埠會繫結至作用中前端節點上的相同連接埠。</span><span class="sxs-lookup"><span data-stu-id="5e176-782">These ports bind to the same port on the active headnode.</span></span> <span data-ttu-id="5e176-783">使用指令碼動作，可讓客戶服務在前端節點的這些連接埠上接聽並路由傳送到叢集外部。</span><span class="sxs-lookup"><span data-stu-id="5e176-783">Script actions can be used to make customer services listen on these ports on the headnode and route to outside the  cluster.</span></span></td>
<td><span data-ttu-id="5e176-784">服務雲端</span><span class="sxs-lookup"><span data-stu-id="5e176-784">Cloud Service</span></span></td>
<td><span data-ttu-id="5e176-785">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-785">All</span></span></td>
<td><span data-ttu-id="5e176-786">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-786">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-787">HDInsight 3.2 的間歇性 MapReduce Shuffle 問題</span><span class="sxs-lookup"><span data-stu-id="5e176-787">Intermittent MapReduce shuffle issue for HDInsight 3.2</span></span></td>
<td><span data-ttu-id="5e176-788">修正大型叢集上 MapReduce Shuffle 的間歇性罕見情況，會導致非經常性工作失敗。</span><span class="sxs-lookup"><span data-stu-id="5e176-788">Fix for a rare, intermittent race condition  in Map Reduce Shuffle on large clusters resulting in occasional task failures.</span></span> <span data-ttu-id="5e176-789">如需詳細資訊，請參閱 <a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a>。</span><span class="sxs-lookup"><span data-stu-id="5e176-789">See <a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a> for more information.</span></span></td>
<td><span data-ttu-id="5e176-790">Hadoop 核心</span><span class="sxs-lookup"><span data-stu-id="5e176-790">Hadoop Core</span></span></td>
<td><span data-ttu-id="5e176-791">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-791">All</span></span></td>
<td><span data-ttu-id="5e176-792"><a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a></span><span class="sxs-lookup"><span data-stu-id="5e176-792"><a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-793">移至最新的 Azure Java SDK 2.2 for HDInsight 3.2</span><span class="sxs-lookup"><span data-stu-id="5e176-793">Move to Latest Azure Java SDK 2.2 for HDInsight 3.2</span></span></td>
<td><span data-ttu-id="5e176-794">已移至 WASB 驅動程式所用的最新版 Azure SDK for Java。</span><span class="sxs-lookup"><span data-stu-id="5e176-794">Moved to latest version of the Azure SDK for Java used by the WASB driver.</span></span> <span data-ttu-id="5e176-795">最新的 SDK 有一些修正程式，而在 https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt 可取得相同的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="5e176-795">The latest SDK has a few fixes and the release notes for the same are available at https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt.</span></span></td>
<td><span data-ttu-id="5e176-796">Hadoop 核心</span><span class="sxs-lookup"><span data-stu-id="5e176-796">Hadoop Core</span></span></td>
<td><span data-ttu-id="5e176-797">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-797">All</span></span></td>
<td><span data-ttu-id="5e176-798"><a href="https://issues.apache.org/jira/browse/HADOOP-11959" target="_blank">HADOOP-11959</a></span><span class="sxs-lookup"><span data-stu-id="5e176-798"><a href="https://issues.apache.org/jira/browse/HADOOP-11959" target="_blank">HADOOP-11959</a></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-799">移至 HDP 2.1.15 for HDInsight 3.1 叢集</span><span class="sxs-lookup"><span data-stu-id="5e176-799">Move to HDP 2.1.15 for HDInsight 3.1 clusters</span></span></td>
<td><span data-ttu-id="5e176-800">這些版本的 Hortonworks 版本資訊位於<a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.15-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.15.html" target="_blank">這裡</a>。</span><span class="sxs-lookup"><span data-stu-id="5e176-800">Hortonworks release notes for the release are available <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.15-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.15.html" target="_blank">here</a>.</span></span></td>
<td><span data-ttu-id="5e176-801">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-801">HDP</span></span></td>
<td><span data-ttu-id="5e176-802">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-802">All</span></span></td>
<td><span data-ttu-id="5e176-803">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-803">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-06042015-release-of-hdinsight"></a><span data-ttu-id="5e176-804">HDInsight 2015/06/04 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-804">Notes for 06/04/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-805">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-805">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-806">HDInsight     2.1.10.583.1575584    (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-806">HDInsight     2.1.10.583.1575584    (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-807">HDInsight     3.0.6.583.1575584    (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-807">HDInsight     3.0.6.583.1575584    (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-808">HDInsight     3.1.3.583.1575584    (HDP 2.1.12.1-0003 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-808">HDInsight     3.1.3.583.1575584    (HDP 2.1.12.1-0003 - unchanged)</span></span>
* <span data-ttu-id="5e176-809">HDInsight        3.2.4.583.1575584    (HDP 2.2.6.1-1)</span><span class="sxs-lookup"><span data-stu-id="5e176-809">HDInsight        3.2.4.583.1575584    (HDP 2.2.6.1-1)</span></span>
* <span data-ttu-id="5e176-810">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-810">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-811">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-811">This release contains the following updates:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-812">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-812">Title</span></span></th>
<th><span data-ttu-id="5e176-813">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-813">Description</span></span></th>
<th><span data-ttu-id="5e176-814">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-814">Impacted Area (for example, Service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-815">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-815">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-816">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-816">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-817">修正 Storm 叢集的 502 不正確閘道器錯誤</span><span class="sxs-lookup"><span data-stu-id="5e176-817">Fix for 502 bad gateway error for Storm clusters</span></span></td>
<td><span data-ttu-id="5e176-818">此版本修正會影響工作提交 API 並導致網站在重新開機後關閉的 Bug。</span><span class="sxs-lookup"><span data-stu-id="5e176-818">This release fixes a bug affecting the job submission API that caused the website to be down after a reboot.</span></span></td>
<td><span data-ttu-id="5e176-819">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-819">Service</span></span></td>
<td><span data-ttu-id="5e176-820">Storm</span><span class="sxs-lookup"><span data-stu-id="5e176-820">Storm</span></span></td>
<td><span data-ttu-id="5e176-821">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-821">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-06012015-release-of-hdinsight"></a><span data-ttu-id="5e176-822">HDInsight 2015/06/01 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-822">Notes for 06/01/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-823">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-823">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-824">HDInsight     2.1.10.577.1563827    (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-824">HDInsight     2.1.10.577.1563827    (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-825">HDInsight     3.0.6.577.1563827    (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-825">HDInsight     3.0.6.577.1563827    (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-826">HDInsight     3.1.3.577.1563827    (HDP 2.1.12.1-0003 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-826">HDInsight     3.1.3.577.1563827    (HDP 2.1.12.1-0003 - unchanged))</span></span>
* <span data-ttu-id="5e176-827">HDInsight        3.2.4.577.1563827    (HDP 2.2.6.0-2800 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-827">HDInsight        3.2.4.577.1563827    (HDP 2.2.6.0-2800 - unchanged)</span></span>
* <span data-ttu-id="5e176-828">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-828">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-829">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-829">This release contains the following updates:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-830">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-830">Title</span></span></th>
<th><span data-ttu-id="5e176-831">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-831">Description</span></span></th>
<th><span data-ttu-id="5e176-832">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-832">Impacted Area (for example, Service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-833">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-833">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-834">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-834">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-835">各種 Bug 修正</span><span class="sxs-lookup"><span data-stu-id="5e176-835">Various bug fixes</span></span></td>
<td><span data-ttu-id="5e176-836">此版本修正與叢集佈建相關的 Bug。</span><span class="sxs-lookup"><span data-stu-id="5e176-836">This release fixes bugs related to cluster provisioning.</span></span></td>
<td><span data-ttu-id="5e176-837">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-837">Service</span></span></td>
<td><span data-ttu-id="5e176-838">所有叢集類型</span><span class="sxs-lookup"><span data-stu-id="5e176-838">All cluster types</span></span></td>
<td><span data-ttu-id="5e176-839">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-839">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-05272015-release-of-hdinsight"></a><span data-ttu-id="5e176-840">HDInsight 2015/05/27 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-840">Notes for 05/27/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-841">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-841">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-842">HDInsight        3.2.4.570.1554102    (HDP 2.2.6.0-2800)</span><span class="sxs-lookup"><span data-stu-id="5e176-842">HDInsight        3.2.4.570.1554102    (HDP 2.2.6.0-2800)</span></span>
* <span data-ttu-id="5e176-843">其他叢集版本和 SDK 不會部署為此版本的一部分。</span><span class="sxs-lookup"><span data-stu-id="5e176-843">Other cluster versions and SDK are not deployed as part of this release.</span></span>

<span data-ttu-id="5e176-844">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-844">This release contains the following updates:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-845">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-845">Title</span></span></th>
<th><span data-ttu-id="5e176-846">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-846">Description</span></span></th>
<th><span data-ttu-id="5e176-847">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-847">Impacted Area (for example, Service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-848">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-848">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-849">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-849">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-850">HDP 2.2 更新</span><span class="sxs-lookup"><span data-stu-id="5e176-850">HDP 2.2 update</span></span></td>
<td><span data-ttu-id="5e176-851">這一版的 HDInsight 3.2 包含 HDP 2.2.6，並在 HDInsight 中加入數個重要的 Bug 修正程式。</span><span class="sxs-lookup"><span data-stu-id="5e176-851">This release of HDInsight 3.2 contains HDP 2.2.6, and brings several important bug fixes to HDInsight.</span></span> <span data-ttu-id="5e176-852">在 <a href="http://dev.hortonworks.com.s3.amazonaws.com/HDPDocuments/HDP2/HDP-2.2.6/HDP_RelNotes_v226/index.html">HDP 2.2.6 版本資訊</a>可取得完整的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="5e176-852">The full release notes are available at <a href="http://dev.hortonworks.com.s3.amazonaws.com/HDPDocuments/HDP2/HDP-2.2.6/HDP_RelNotes_v226/index.html">HDP 2.2.6 Release Notes</a>.</span></span></td>
<td><span data-ttu-id="5e176-853">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-853">HDP</span></span></td>
<td><span data-ttu-id="5e176-854">所有叢集類型</span><span class="sxs-lookup"><span data-stu-id="5e176-854">All cluster types</span></span></td>
<td><span data-ttu-id="5e176-855">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-855">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-856">變更為預設 Yarn 容器記憶體設定</span><span class="sxs-lookup"><span data-stu-id="5e176-856">Change to Default Yarn Container Memory Configuration</span></span></td>
<td><span data-ttu-id="5e176-857">在這項更新中，由節點管理員啟動之 YARN 容器 (yarn.nodemanager.resource.memory-mb and yarn.scheduler.maximum-allocation-mb) 的預設可用記憶體會增加至 5632MB。</span><span class="sxs-lookup"><span data-stu-id="5e176-857">In this update, the default available memory to YARN containers (yarn.nodemanager.resource.memory-mb and yarn.scheduler.maximum-allocation-mb), launched by Node Manager, is increased to 5632MB.</span></span> <span data-ttu-id="5e176-858">先前這會縮減至 4608MB，但根據不同的工作會執行，新值必須為大部分的工作提供更佳的可靠性和效能，因此此預設值更好。</span><span class="sxs-lookup"><span data-stu-id="5e176-858">Previously this was reduced to 4608MB, but based on various job runs, the new value must offer better reliability and performance to most jobs, hence is a better default.</span></span> <span data-ttu-id="5e176-859">如往常一樣，如果您對此記憶體組態有重要相依性，請在建立叢集時加以明確設定。</span><span class="sxs-lookup"><span data-stu-id="5e176-859">As usual, if you have critical dependency on this memory configuration, set it explicitly while creating the cluster.</span></span></td>
<td><span data-ttu-id="5e176-860">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-860">HDP</span></span></td>
<td><span data-ttu-id="5e176-861">所有叢集類型</span><span class="sxs-lookup"><span data-stu-id="5e176-861">All cluster types</span></span></td>
<td><span data-ttu-id="5e176-862">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-862">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-863">HBase 和 Storm 叢集的預設組態同位檢查</span><span class="sxs-lookup"><span data-stu-id="5e176-863">Default Config parity for HBase and Storm clusters</span></span></td>
<td><span data-ttu-id="5e176-864">此更新會將 Hbase 和 Storm 叢集還原為使用與 Hadoop 叢集相同的 YARN 組態值。</span><span class="sxs-lookup"><span data-stu-id="5e176-864">This update restores Hbase and Storm clusters to use the same values of YARN configs as Hadoop clusters.</span></span> <span data-ttu-id="5e176-865">這是為了進行所有叢集類型的同位檢查。</span><span class="sxs-lookup"><span data-stu-id="5e176-865">This is done for parity across all cluster types.</span></span></td>
<td><span data-ttu-id="5e176-866">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-866">HDP</span></span></td>
<td><span data-ttu-id="5e176-867">HBase、Storm</span><span class="sxs-lookup"><span data-stu-id="5e176-867">HBase, Storm</span></span></td>
<td><span data-ttu-id="5e176-868">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-868">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-05202015-release-of-hdinsight"></a><span data-ttu-id="5e176-869">HDInsight 2015/05/20 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-869">Notes for 05/20/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-870">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-870">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-871">HDInsight     2.1.10.564.1542093    (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-871">HDInsight     2.1.10.564.1542093    (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-872">HDInsight     3.0.6.564.1542093    (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-872">HDInsight     3.0.6.564.1542093    (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-873">HDInsight     3.1.3.564.1542093    (HDP 2.1.12.1-0003)</span><span class="sxs-lookup"><span data-stu-id="5e176-873">HDInsight     3.1.3.564.1542093    (HDP 2.1.12.1-0003)</span></span>
* <span data-ttu-id="5e176-874">HDInsight        3.2.4.564.1542093    (HDP 2.2.4.6-2)</span><span class="sxs-lookup"><span data-stu-id="5e176-874">HDInsight        3.2.4.564.1542093    (HDP 2.2.4.6-2)</span></span>
* <span data-ttu-id="5e176-875">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-875">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-876">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-876">This release contains the following updates:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-877">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-877">Title</span></span></th>
<th><span data-ttu-id="5e176-878">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-878">Description</span></span></th>
<th><span data-ttu-id="5e176-879">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-879">Impacted Area (for example, Service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-880">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-880">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-881">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-881">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-882">SCP.NET EventHub 支援</span><span class="sxs-lookup"><span data-stu-id="5e176-882">SCP.NET EventHub Support</span></span></td>
<td><span data-ttu-id="5e176-883">HDInsight Storm 的更新叢集封裝加入 SCP.NET 的新功能。</span><span class="sxs-lookup"><span data-stu-id="5e176-883">The updated cluster packages for HDInsight Storm bring new features to SCP.NET.</span></span> <span data-ttu-id="5e176-884">您現在將可存取拓撲產生器中的新 API，讓您更輕鬆地使用 EventHubSpout 或 Java Spouts。</span><span class="sxs-lookup"><span data-stu-id="5e176-884">You now have access to new APIs in topology builder that make it easier to use EventHubSpout or Java Spouts.</span></span> <span data-ttu-id="5e176-885">您必須更新 SCP.NET 用戶端 SDK，才能在合約更新後使用新叢集。</span><span class="sxs-lookup"><span data-stu-id="5e176-885">You must update your SCP.NET client SDK to work with new clusters as the contracts have been updated.</span></span> <span data-ttu-id="5e176-886">如需新 API、使用方式及版本資訊 (包括 Bug 修正程式) 的詳細資訊，請參閱 SCP.NET NuGet 套件中包含的 Readme 檔案。</span><span class="sxs-lookup"><span data-stu-id="5e176-886">For details on the new APIs, usage and release notes (including bug fixes) refer to the Readme included in the SCP.NET NuGet package.</span></span></td>
<td><span data-ttu-id="5e176-887">VS 工具</span><span class="sxs-lookup"><span data-stu-id="5e176-887">VS Tooling</span></span></td>
<td><span data-ttu-id="5e176-888">Storm HDInsight 3.2 叢集</span><span class="sxs-lookup"><span data-stu-id="5e176-888">Storm HDInsight 3.2 clusters</span></span></td>
<td><span data-ttu-id="5e176-889">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-889">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-890">JDBC 驅動程式更新</span><span class="sxs-lookup"><span data-stu-id="5e176-890">JDBC driver update</span></span></td>
<td><span data-ttu-id="5e176-891">將驅動程式更新為 sqljdbc_4.1.5605.100 中支援的 SQL Server 版本。</span><span class="sxs-lookup"><span data-stu-id="5e176-891">Updated the driver to the SQL Server supported version in sqljdbc_4.1.5605.100.</span></span></td>
<td><span data-ttu-id="5e176-892">Metastore</span><span class="sxs-lookup"><span data-stu-id="5e176-892">Metastore</span></span></td>
<td><span data-ttu-id="5e176-893">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-893">All</span></span></td>
<td><span data-ttu-id="5e176-894">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-894">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-04272015-release-of-hdinsight"></a><span data-ttu-id="5e176-895">HDInsight 2015/04/27 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-895">Notes for 04/27/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-896">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-896">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-897">HDInsight     2.1.10.537.1486660    (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-897">HDInsight     2.1.10.537.1486660    (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-898">HDInsight     3.0.6.537.1486660    (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-898">HDInsight     3.0.6.537.1486660    (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-899">HDInsight     3.1.3.537.1486660    (HDP 2.1.12.0-2329 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-899">HDInsight     3.1.3.537.1486660    (HDP 2.1.12.0-2329 - unchanged)</span></span>
* <span data-ttu-id="5e176-900">HDInsight        3.2.3.537.1486660    (HDP 2.2.2.2-4)</span><span class="sxs-lookup"><span data-stu-id="5e176-900">HDInsight        3.2.3.537.1486660    (HDP 2.2.2.2-4)</span></span>
* <span data-ttu-id="5e176-901">SDK            1.5.8</span><span class="sxs-lookup"><span data-stu-id="5e176-901">SDK            1.5.8</span></span>

<span data-ttu-id="5e176-902">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-902">This release contains the following updates:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-903">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-903">Title</span></span></th>
<th><span data-ttu-id="5e176-904">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-904">Description</span></span></th>
<th><span data-ttu-id="5e176-905">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-905">Impacted Area (for example, Service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-906">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-906">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-907">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-907">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-908">修正 DLL 相依性</span><span class="sxs-lookup"><span data-stu-id="5e176-908">Fix DLL dependency</span></span></td>
<td><span data-ttu-id="5e176-909">移除對單位測試架構的 HDInsight 相依性。</span><span class="sxs-lookup"><span data-stu-id="5e176-909">Removes HDInsight dependency on Unit Test Framework.</span></span></td>
<td><span data-ttu-id="5e176-910">SDK</span><span class="sxs-lookup"><span data-stu-id="5e176-910">SDK</span></span></td>
<td><span data-ttu-id="5e176-911">Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e176-911">Hadoop</span></span></td>
<td><span data-ttu-id="5e176-912">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-912">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-913">競爭情形的 Bug 修正</span><span class="sxs-lookup"><span data-stu-id="5e176-913">Bug fix for race condition</span></span></td>
<td><span data-ttu-id="5e176-914">叢集建立要求現正等待 PUT 要求獲得接受，然後才進行狀態的輪詢</span><span class="sxs-lookup"><span data-stu-id="5e176-914">A cluster create request now waits on PUT request to be accepted before polling on the status</span></span></td>
<td><span data-ttu-id="5e176-915">SDK</span><span class="sxs-lookup"><span data-stu-id="5e176-915">SDK</span></span></td>
<td><span data-ttu-id="5e176-916">Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e176-916">Hadoop</span></span></td>
<td><span data-ttu-id="5e176-917">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-917">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-04142015-release-of-hdinsight"></a><span data-ttu-id="5e176-918">HDInsight 2015/04/14 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-918">Notes for 04/14/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-919">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-919">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-920">HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-920">HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-921">HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-921">HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-922">HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-922">HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - unchanged)</span></span>
* <span data-ttu-id="5e176-923">HDInsight        3.2.3.525.1459730    (HDP 2.2.2.2-2)</span><span class="sxs-lookup"><span data-stu-id="5e176-923">HDInsight        3.2.3.525.1459730    (HDP 2.2.2.2-2)</span></span>
* <span data-ttu-id="5e176-924">SDK            1.5.6</span><span class="sxs-lookup"><span data-stu-id="5e176-924">SDK            1.5.6</span></span>

<span data-ttu-id="5e176-925">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-925">This release contains the following updates:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-926">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-926">Title</span></span></th>
<th><span data-ttu-id="5e176-927">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-927">Description</span></span></th>
<th><span data-ttu-id="5e176-928">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-928">Impacted Area (for example, Service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-929">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-929">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-930">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-930">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-931">Tez Bug 修正</span><span class="sxs-lookup"><span data-stu-id="5e176-931">Tez bug fixes</span></span></td>
<td><span data-ttu-id="5e176-932">Apache TEZ 2214 和 TEZ 1923 的修正包含在此版本的 HDI 3.2。</span><span class="sxs-lookup"><span data-stu-id="5e176-932">Fixes for Apache TEZ 2214 and TEZ 1923 are included in this release of HDI 3.2.</span></span> <span data-ttu-id="5e176-933">Tez 上需要混和大量資料的特定 Hive 查詢需要這些修正。</span><span class="sxs-lookup"><span data-stu-id="5e176-933">These are needed for certain Hive queries on Tez which require to shuffle a significant amount of data.</span></span>
</td>
<td><span data-ttu-id="5e176-934">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-934">HDP</span></span></td>
<td><span data-ttu-id="5e176-935">Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e176-935">Hadoop</span></span></td>
<td><span data-ttu-id="5e176-936"><a href="https://issues.apache.org/jira/browse/TEZ-2214">TEZ 2214</a></span><span class="sxs-lookup"><span data-stu-id="5e176-936"><a href="https://issues.apache.org/jira/browse/TEZ-2214">TEZ 2214</a></span></span></br><span data-ttu-id="5e176-937"><a href="https://issues.apache.org/jira/browse/TEZ-1923">TEZ 1923</a></span><span class="sxs-lookup"><span data-stu-id="5e176-937"><a href="https://issues.apache.org/jira/browse/TEZ-1923">TEZ 1923</a></span></span></td>
</tr>
</table>

## <a name="notes-for-04062015-release-of-hdinsight"></a><span data-ttu-id="5e176-938">HDInsight 2015/04/06 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-938">Notes for 04/06/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-939">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-939">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-940">HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-940">HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - unchanged)</span></span>
* <span data-ttu-id="5e176-941">HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-941">HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - unchanged)</span></span>
* <span data-ttu-id="5e176-942">HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-942">HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - unchanged)</span></span>
* <span data-ttu-id="5e176-943">HDInsight        3.2.3.521.1453250    (HDP 2.2.2.2-1)</span><span class="sxs-lookup"><span data-stu-id="5e176-943">HDInsight        3.2.3.521.1453250    (HDP 2.2.2.2-1)</span></span>
* <span data-ttu-id="5e176-944">SDK            1.5.6</span><span class="sxs-lookup"><span data-stu-id="5e176-944">SDK            1.5.6</span></span>

<span data-ttu-id="5e176-945">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-945">This release contains the following updates:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-946">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-946">Title</span></span></th>
<th><span data-ttu-id="5e176-947">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-947">Description</span></span></th>
<th><span data-ttu-id="5e176-948">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-948">Impacted Area (for example, Service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-949">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-949">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-950">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-950">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-951">HDInsight .NET SDK 1.5.6</span><span class="sxs-lookup"><span data-stu-id="5e176-951">HDInsight .NET SDK 1.5.6</span></span></td>
<td><span data-ttu-id="5e176-952">此更新可移除 Linux 上之 HDInsight 的部分內部類別。</span><span class="sxs-lookup"><span data-stu-id="5e176-952">Updates to remove some internal classes for HDInsight on Linux.</span></span></td>
<td><span data-ttu-id="5e176-953">SDK</span><span class="sxs-lookup"><span data-stu-id="5e176-953">SDK</span></span></td>
<td><span data-ttu-id="5e176-954">Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e176-954">Hadoop</span></span></td>
<td><span data-ttu-id="5e176-955">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-955">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-956">Avro Library 1.5.6</span><span class="sxs-lookup"><span data-stu-id="5e176-956">Avro Library 1.5.6</span></span></td>
<td><span data-ttu-id="5e176-957">已為方法 <b>GetAllKnownTypes</b> 新增 <b>KnownTypeAttribute</b>。</span><span class="sxs-lookup"><span data-stu-id="5e176-957">Added <b>KnownTypeAttribute</b> for method <b>GetAllKnownTypes</b>.</span></span> <span data-ttu-id="5e176-958">當 GetAllKnownTypes 方法的類型為 Null 時已修正的 NullReferenceException。</span><span class="sxs-lookup"><span data-stu-id="5e176-958">Fixed NullReferenceException when a type is null for GetAllKnownTypes method.</span></span></td>
<td><span data-ttu-id="5e176-959">SDK</span><span class="sxs-lookup"><span data-stu-id="5e176-959">SDK</span></span></td>
<td><span data-ttu-id="5e176-960">Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e176-960">Hadoop</span></span></td>
<td><span data-ttu-id="5e176-961">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-961">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-962">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="5e176-962">Bug fixes</span></span></td>
<td><span data-ttu-id="5e176-963">服務的各種 Bug 修正</span><span class="sxs-lookup"><span data-stu-id="5e176-963">Various bug fixes to the service</span></span></td>
<td><span data-ttu-id="5e176-964">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-964">Service</span></span></td>
<td><span data-ttu-id="5e176-965">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-965">All</span></span></td>
<td><span data-ttu-id="5e176-966">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-966">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-04012015-release-of-hdinsight"></a><span data-ttu-id="5e176-967">HDInsight 2015/04/01 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-967">Notes for 04/01/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-968">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-968">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-969">HDInsight     2.1.10.513.1431705    (HDP 1.3.12.0-01795)</span><span class="sxs-lookup"><span data-stu-id="5e176-969">HDInsight     2.1.10.513.1431705    (HDP 1.3.12.0-01795)</span></span>
* <span data-ttu-id="5e176-970">HDInsight     3.0.6.513.1431705    (HDP 2.0.13.0-2117)</span><span class="sxs-lookup"><span data-stu-id="5e176-970">HDInsight     3.0.6.513.1431705    (HDP 2.0.13.0-2117)</span></span>
* <span data-ttu-id="5e176-971">HDInsight     3.1.3.513.1431705    (HDP 2.1.12.0-2329)</span><span class="sxs-lookup"><span data-stu-id="5e176-971">HDInsight     3.1.3.513.1431705    (HDP 2.1.12.0-2329)</span></span>
* <span data-ttu-id="5e176-972">HDInsight        3.2.3.513.1431705    (HDP 2.2.2.1-2600)</span><span class="sxs-lookup"><span data-stu-id="5e176-972">HDInsight        3.2.3.513.1431705    (HDP 2.2.2.1-2600)</span></span>
* <span data-ttu-id="5e176-973">SDK            1.5.5</span><span class="sxs-lookup"><span data-stu-id="5e176-973">SDK            1.5.5</span></span>

<span data-ttu-id="5e176-974">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-974">This release contains the following updates:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-975">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-975">Title</span></span></th>
<th><span data-ttu-id="5e176-976">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-976">Description</span></span></th>
<th><span data-ttu-id="5e176-977">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-977">Impacted Area (for example, Service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-978">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-978">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-979">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-979">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-980">透過 .NET SDK 啟用/停用 Windows 叢集上的遠端桌面認證的能力</span><span class="sxs-lookup"><span data-stu-id="5e176-980">Ability to enable/disable remote desktop credentials on Windows clusters via .NET SDK</span></span></td>
<td><span data-ttu-id="5e176-981">針對在 Windows 叢集上啟用或停用 RDP 認證的程式設計支援。</span><span class="sxs-lookup"><span data-stu-id="5e176-981">Programmatic support for enabling or disabling RDP credentials on Windows clusters.</span></span></td>
<td><span data-ttu-id="5e176-982">SDK</span><span class="sxs-lookup"><span data-stu-id="5e176-982">SDK</span></span></td>
<td><span data-ttu-id="5e176-983">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-983">All</span></span></td>
<td><span data-ttu-id="5e176-984">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-984">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-985">當叢集正在佈建時啟用遠端桌面認證的能力</span><span class="sxs-lookup"><span data-stu-id="5e176-985">Ability to enable remote desktop credentials on clusters while they are being provisioned</span></span></td>
<td><span data-ttu-id="5e176-986">針對正在建立叢集時啟用遠端桌面認證的程式設計支援。</span><span class="sxs-lookup"><span data-stu-id="5e176-986">Programmatic support for enabling remote desktop credentials as the cluster is being created.</span></span> <span data-ttu-id="5e176-987">如此便不再需要先佈建叢集再啟用遠端桌面的兩步驟程序。</span><span class="sxs-lookup"><span data-stu-id="5e176-987">This removes the two-step process for first provisioning the cluster and then enabling remote desktop.</span></span></td>
<td><span data-ttu-id="5e176-988">SDK</span><span class="sxs-lookup"><span data-stu-id="5e176-988">SDK</span></span></td>
<td><span data-ttu-id="5e176-989">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-989">All</span></span></td>
<td><span data-ttu-id="5e176-990">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-990">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-991">已將 Python 升級到 2.7.8</span><span class="sxs-lookup"><span data-stu-id="5e176-991">Upgraded Python to 2.7.8</span></span></td>
<td><span data-ttu-id="5e176-992">已將 HDInsight 叢集上的 Python 升級到 Python 2.7.8，它包含一些 HDInsight 2.1、3.0、3.1 和 3.2 版的重要安全性修正</span><span class="sxs-lookup"><span data-stu-id="5e176-992">Upgraded Python on HDInsight Clusters to Python 2.7.8, which contains some important security fixes for HDInsight versions 2.1, 3.0, 3.1, and 3.2</span></span></td>
<td><span data-ttu-id="5e176-993">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-993">Service</span></span></td>
<td><span data-ttu-id="5e176-994">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-994">All</span></span></td>
<td><span data-ttu-id="5e176-995">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-995">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-996">YARN 組態變更</span><span class="sxs-lookup"><span data-stu-id="5e176-996">YARN configuration change</span></span></td>
<td><span data-ttu-id="5e176-997">已針對 HDInsight 3.1 和 3.2 版的所有叢集類型將 YARN 組態 yarn.resourcemanager.max-completed-applications 變更為 1000。</span><span class="sxs-lookup"><span data-stu-id="5e176-997">Changed YARN configuration yarn.resourcemanager.max-completed-applications to 1000 for all cluster types for HDInsight versions 3.1 and 3.2.</span></span> <span data-ttu-id="5e176-998">此值只會控制 YARN UI 中的已完成應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="5e176-998">This value only controls the list of completed applications in the YARN UI.</span></span> <span data-ttu-id="5e176-999">若要取得在 UI 上顯示應用程式清單之前提交之應用程式的相關資訊，您可以直接移至 [記錄伺服器]。</span><span class="sxs-lookup"><span data-stu-id="5e176-999">To get information about applications that were submitted prior to the list of applications shown on the UI, you can directly go to the History Server.</span></span></td>
<td><span data-ttu-id="5e176-1000">YARN</span><span class="sxs-lookup"><span data-stu-id="5e176-1000">YARN</span></span></td>
<td><span data-ttu-id="5e176-1001">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1001">All</span></span></td>
<td><span data-ttu-id="5e176-1002">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1002">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1003">在 HBase 叢集中調整節點的大小</span><span class="sxs-lookup"><span data-stu-id="5e176-1003">Resizing of nodes in an HBase cluster</span></span></td>
<td><span data-ttu-id="5e176-1004">HBase 叢集現在允許針對 HDInsight 3.1 和 3.2 版 (向上及向下) 調整節點的大小</span><span class="sxs-lookup"><span data-stu-id="5e176-1004">HBase clusters now allow resizing of nodes (up and down) for HDInsight versions 3.1 and 3.2</span></span></td>
<td><span data-ttu-id="5e176-1005">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-1005">Service</span></span></td>
<td><span data-ttu-id="5e176-1006">hbase</span><span class="sxs-lookup"><span data-stu-id="5e176-1006">HBase</span></span></td>
<td><span data-ttu-id="5e176-1007">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1007">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1008">JDBC 升級</span><span class="sxs-lookup"><span data-stu-id="5e176-1008">JDBC upgrade</span></span></td>
<td><span data-ttu-id="5e176-1009">HDInsight 3.2 版的 SQL JDBC 驅動程式已升級到 sqljdbc_4.0.2206.100 版。</span><span class="sxs-lookup"><span data-stu-id="5e176-1009">SQL JDBC driver is upgraded to version sqljdbc_4.0.2206.100 for HDInsight version 3.2.</span></span> <span data-ttu-id="5e176-1010">此版本包含重要的安全性增強功能。</span><span class="sxs-lookup"><span data-stu-id="5e176-1010">This version contains important security enhancements.</span></span></td>
<td><span data-ttu-id="5e176-1011">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-1011">HDP</span></span></td>
<td><span data-ttu-id="5e176-1012">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1012">All</span></span></td>
<td><span data-ttu-id="5e176-1013">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1013">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1014">JVM 組態更新</span><span class="sxs-lookup"><span data-stu-id="5e176-1014">JVM configuration update</span></span></td>
<td><span data-ttu-id="5e176-1015">已針對 HDInsight 3.1 和 3.2 版將 JVM 組態 networkaddress.cache.ttl 從預設值 -1 更新到 300 秒。</span><span class="sxs-lookup"><span data-stu-id="5e176-1015">Updated JVM configuration networkaddress.cache.ttl to 300 seconds from the default value of -1 for HDInsight versions 3.1 and 3.2.</span></span> <span data-ttu-id="5e176-1016">此組態值控制來自名稱服務的成功名稱查閱快取原則。</span><span class="sxs-lookup"><span data-stu-id="5e176-1016">This configuration value controls the caching policy for successful name lookups from the name service.</span></span> <span data-ttu-id="5e176-1017">這修正了與增大和壓縮 HBase 叢集有關的 Bug。</span><span class="sxs-lookup"><span data-stu-id="5e176-1017">This fixes a bug related to growing and shrinking HBase clusters.</span></span></td>
<td><span data-ttu-id="5e176-1018">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-1018">Service</span></span></td>
<td><span data-ttu-id="5e176-1019">hbase</span><span class="sxs-lookup"><span data-stu-id="5e176-1019">HBase</span></span></td>
<td><span data-ttu-id="5e176-1020">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1020">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1021">升級到 Azure Storage SDK for Java 2.0</span><span class="sxs-lookup"><span data-stu-id="5e176-1021">Upgrade to Azure Storage SDK for Java 2.0</span></span></td>
<td><span data-ttu-id="5e176-1022">已升級 HDInsight 3.2 版以使用最新版的 Azure Storage SDK for Java。</span><span class="sxs-lookup"><span data-stu-id="5e176-1022">HDInsight version 3.2 is upgraded to use the latest version of the Azure Storage SDK for Java.</span></span> <span data-ttu-id="5e176-1023">這包含針對目前 0.6.0 版的幾項重要 Bug 修正。</span><span class="sxs-lookup"><span data-stu-id="5e176-1023">This contains several important bug fixes over the current 0.6.0 version.</span></span></td>
<td><span data-ttu-id="5e176-1024">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-1024">HDP</span></span></td>
<td><span data-ttu-id="5e176-1025">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1025">All</span></span></td>
<td><span data-ttu-id="5e176-1026">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1026">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1027">已升級到 Apache WASB 原始程式碼</span><span class="sxs-lookup"><span data-stu-id="5e176-1027">Upgraded to Apache WASB source code</span></span></td>
<td><span data-ttu-id="5e176-1028">HDInsight 3.2 版現在使用來自 Apache Hadoop 的 WASB 檔案系統驅動程式的最新程式碼。</span><span class="sxs-lookup"><span data-stu-id="5e176-1028">HDInsight version 3.2 now uses the latest code for the WASB filesystem driver from Apache Hadoop.</span></span> <span data-ttu-id="5e176-1029">有了這項變更，WASB 驅動程式現在封裝為獨立型 jar。</span><span class="sxs-lookup"><span data-stu-id="5e176-1029">With this change, the WASB driver is now packaged as a separate jar.</span></span> <span data-ttu-id="5e176-1030">這純粹是封裝變更，不包含對 WASB 驅動程式行為的任何變更。</span><span class="sxs-lookup"><span data-stu-id="5e176-1030">This is purely a packaging change and does not contain any changes to behavior of the WASB driver.</span></span> <span data-ttu-id="5e176-1031">此 JAR 檔的名稱是 hadoop-azure-2.6.0.jar。</span><span class="sxs-lookup"><span data-stu-id="5e176-1031">The name of this JAR file is hadoop-azure-2.6.0.jar.</span></span></td>
<td><span data-ttu-id="5e176-1032">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-1032">HDP</span></span></td>
<td><span data-ttu-id="5e176-1033">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1033">All</span></span></td>
<td><span data-ttu-id="5e176-1034">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1034">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1035">HDInsight 3.2 中的 Jar 檔案名稱更新</span><span class="sxs-lookup"><span data-stu-id="5e176-1035">Jar File Name updates in HDInsight 3.2</span></span></td>
<td><span data-ttu-id="5e176-1036">HDInsight 3.2 版的這項更新包含數個 Bug 修正，且封裝為包含在 HDP 的一些內部 jar 也已升級。</span><span class="sxs-lookup"><span data-stu-id="5e176-1036">This update to HDInsight version 3.2 contains several bug fixes, and a few internal jars packaged as part of HDP have been upgraded.</span></span> <span data-ttu-id="5e176-1037">這些 JAR 檔是 HDP 封裝內部使用，不供客戶應用程式直接使用。</span><span class="sxs-lookup"><span data-stu-id="5e176-1037">These JAR filesare internal to the HDP package and not for direct use by customer applications.</span></span> <span data-ttu-id="5e176-1038">應用程式應該封裝自己的 JAR 版本，如此升級 HDP 內部 JAR 時才不會中斷客戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e176-1038">Applications should package their own version of the JARs so that an upgrade to the HDP internal JARs do not break customer applications.</span></span></td>
<td><span data-ttu-id="5e176-1039">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-1039">HDP</span></span></td>
<td><span data-ttu-id="5e176-1040">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1040">All</span></span></td>
<td><span data-ttu-id="5e176-1041">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1041">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-03032015-release-of-hdinsight"></a><span data-ttu-id="5e176-1042">HDInsight 2015/03/03 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1042">Notes for 03/03/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-1043">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-1043">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-1044">HDInsight     2.1.10.488.1375841    (HDP 1.3.9.0-01351 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1044">HDInsight     2.1.10.488.1375841    (HDP 1.3.9.0-01351 - unchanged)</span></span>
* <span data-ttu-id="5e176-1045">HDInsight     3.0.6.488.1375841    (HDP 2.0.9.0-2097 -  未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1045">HDInsight     3.0.6.488.1375841    (HDP 2.0.9.0-2097 -  unchanged)</span></span>
* <span data-ttu-id="5e176-1046">HDInsight     3.1.3.488.1375841    (HDP 2.1.10.0-2290 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1046">HDInsight     3.1.3.488.1375841    (HDP 2.1.10.0-2290 - unchanged)</span></span>
* <span data-ttu-id="5e176-1047">HDInsight        3.2.3.488.1375841    (HDP-2.2.10.0-2340 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1047">HDInsight        3.2.3.488.1375841    (HDP-2.2.10.0-2340 - unchanged)</span></span>
* <span data-ttu-id="5e176-1048">SDK            1.5.0                (未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1048">SDK            1.5.0                (unchanged)</span></span>

<span data-ttu-id="5e176-1049">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-1049">This release contains the following update:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-1050">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-1050">Title</span></span></th>
<th><span data-ttu-id="5e176-1051">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-1051">Description</span></span></th>
<th><span data-ttu-id="5e176-1052">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-1052">Impacted Area (for example, service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-1053">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-1053">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-1054">JIRA</span><span class="sxs-lookup"><span data-stu-id="5e176-1054">JIRA</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-1055">可靠性的改進</span><span class="sxs-lookup"><span data-stu-id="5e176-1055">Reliability improvements</span></span></td>
<td><span data-ttu-id="5e176-1056">我們做了修正，讓服務能更妥善地隨著與叢集建立時相比增加的負載而縮放。</span><span class="sxs-lookup"><span data-stu-id="5e176-1056">We made fixes that allow the service to scale better with the increased load with respect to cluster creation.</span></span></td>
<td><span data-ttu-id="5e176-1057">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-1057">Service</span></span></td>
<td><span data-ttu-id="5e176-1058">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1058">All</span></span></td>
<td><span data-ttu-id="5e176-1059">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1059">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-02182015-release-of-hdinsight"></a><span data-ttu-id="5e176-1060">HDInsight 2015/02/18 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1060">Notes for 02/18/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-1061">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-1061">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-1062">HDInsight     2.1.10.471.1342507    (HDP 1.3.9.0-01351 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1062">HDInsight     2.1.10.471.1342507    (HDP 1.3.9.0-01351 - unchanged)</span></span>
* <span data-ttu-id="5e176-1063">HDInsight     3.0.6.471.1342507    (HDP 2.0.9.0-2097 -  未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1063">HDInsight     3.0.6.471.1342507    (HDP 2.0.9.0-2097 -  unchanged)</span></span>
* <span data-ttu-id="5e176-1064">HDInsight     3.1.3.471.1342507    (HDP 2.1.10.0-2290 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1064">HDInsight     3.1.3.471.1342507    (HDP 2.1.10.0-2290 - unchanged)</span></span>
* <span data-ttu-id="5e176-1065">HDInsight        3.2.3.471.1342507    (HDP-2.2.10.0-2340)</span><span class="sxs-lookup"><span data-stu-id="5e176-1065">HDInsight        3.2.3.471.1342507    (HDP-2.2.10.0-2340)</span></span>
* <span data-ttu-id="5e176-1066">SDK            1.5.0</span><span class="sxs-lookup"><span data-stu-id="5e176-1066">SDK            1.5.0</span></span>

<span data-ttu-id="5e176-1067">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-1067">This release contains the following updates:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-1068">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-1068">Title</span></span></th>
<th><span data-ttu-id="5e176-1069">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-1069">Description</span></span></th>
<th><span data-ttu-id="5e176-1070">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-1070">Impacted Area (for example, Service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-1071">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-1071">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-1072">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-1072">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-1073">HDInsight 3.2 叢集</span><span class="sxs-lookup"><span data-stu-id="5e176-1073">HDInsight 3.2 clusters</span></span></td>
<td><span data-ttu-id="5e176-1074">HDInsight 3.2 叢集提供 Hadoop 2.6/HDP2.2。</span><span class="sxs-lookup"><span data-stu-id="5e176-1074">Hadoop 2.6/HDP2.2 is available with HDInsight 3.2 clusters.</span></span> <span data-ttu-id="5e176-1075">它包含對所有開放原始碼元件的重大更新。</span><span class="sxs-lookup"><span data-stu-id="5e176-1075">It contains major updates to all of the open-source components.</span></span> <span data-ttu-id="5e176-1076">如需詳細資訊，請參閱 HDInsight 的新功能和 <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html" target="_blank">HDP 2.2.0.0 版本資訊</a>。</span><span class="sxs-lookup"><span data-stu-id="5e176-1076">For more information, see What's new in HDInsight and <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html" target="_blank">HDP 2.2.0.0 Release Notes</a>.</span></span></td>
<td><span data-ttu-id="5e176-1077">開放原始碼軟體</span><span class="sxs-lookup"><span data-stu-id="5e176-1077">Open-source software</span></span></td>
<td><span data-ttu-id="5e176-1078">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1078">All</span></span></td>
<td><span data-ttu-id="5e176-1079">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1079">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1080">Linux 上的 HDInsight (預覽)</span><span class="sxs-lookup"><span data-stu-id="5e176-1080">HDInsight on Linux (Preview)</span></span></td>
<td><span data-ttu-id="5e176-1081">叢集可以部署在 Ubuntu Linux 上執行。</span><span class="sxs-lookup"><span data-stu-id="5e176-1081">Clusters can be deployed running on Ubuntu Linux.</span></span> <span data-ttu-id="5e176-1082">如需詳細資訊，請參閱＜開始在 Linux 上使用 HDInsight＞。</span><span class="sxs-lookup"><span data-stu-id="5e176-1082">For more information, see Get Started with HDInsight on Linux.</span></span></td>
<td><span data-ttu-id="5e176-1083">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-1083">Service</span></span></td>
<td><span data-ttu-id="5e176-1084">Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e176-1084">Hadoop</span></span></td>
<td><span data-ttu-id="5e176-1085">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1085">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1086">Storm 公開上市</span><span class="sxs-lookup"><span data-stu-id="5e176-1086">Storm General Availability</span></span></td>
<td><span data-ttu-id="5e176-1087">Apache Storm 叢集已公開上市。</span><span class="sxs-lookup"><span data-stu-id="5e176-1087">Apache Storm clusters are generally available.</span></span> <span data-ttu-id="5e176-1088">如需詳細資訊，請參閱＜開始在 HDInsight 中使用 Storm＞。</span><span class="sxs-lookup"><span data-stu-id="5e176-1088">For more information, see Get started using Storm in HDInsight.</span></span></td>
<td><span data-ttu-id="5e176-1089">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-1089">Service</span></span></td>
<td><span data-ttu-id="5e176-1090">Storm</span><span class="sxs-lookup"><span data-stu-id="5e176-1090">Storm</span></span></td>
<td><span data-ttu-id="5e176-1091">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1091">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1092">虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="5e176-1092">Virtual machine sizes</span></span></td>
<td><span data-ttu-id="5e176-1093">Azure HDInsight 可用於更多虛擬機器類型和大小。</span><span class="sxs-lookup"><span data-stu-id="5e176-1093">Azure HDInsight is available on more virtual machine types and sizes.</span></span> <span data-ttu-id="5e176-1094">HDInsight 可以利用針對一般用途建置的 A2 到 A7 大小；D 系列節點的特色為固態硬碟 (SSD) 和處理器速度更快 60%；而 A8 和 A9 大小具有 InfiniBand 支援可快速進行網路連線。</span><span class="sxs-lookup"><span data-stu-id="5e176-1094">HDInsight can utilize A2 to A7 sizes built for general purposes; D-Series nodes that feature solid-state drives (SSDs) and 60-percent faster processors; and A8 and A9 sizes that have InfiniBand support for fast networking.</span></span></td>
<td><span data-ttu-id="5e176-1095">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-1095">Service</span></span></td>
<td><span data-ttu-id="5e176-1096">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1096">All</span></span></td>
<td><span data-ttu-id="5e176-1097">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1097">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1098">叢集縮放</span><span class="sxs-lookup"><span data-stu-id="5e176-1098">Cluster scaling</span></span></td>
<td><span data-ttu-id="5e176-1099">您可以針對執行中的 HDInsight 叢集變更資料節點的數目，而不必刪除或重建它。</span><span class="sxs-lookup"><span data-stu-id="5e176-1099">You can change the number of data nodes for a running HDInsight cluster without having to delete or re-create it.</span></span> <span data-ttu-id="5e176-1100">目前只有 Hadoop 查詢和 Apache Storm 叢集類型有此功能，但很快就會提供對 Apache HBase 叢集類型的支援。</span><span class="sxs-lookup"><span data-stu-id="5e176-1100">Currently, only Hadoop Query and Apache Storm cluster types have this ability, but support for Apache HBase cluster type is soon to follow.</span></span> <span data-ttu-id="5e176-1101">如需詳細資訊，請參閱＜管理 HDInsight 叢集＞。</span><span class="sxs-lookup"><span data-stu-id="5e176-1101">For more information, see Manage HDInsight clusters.</span></span></td>
<td><span data-ttu-id="5e176-1102">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-1102">Service</span></span></td>
<td><span data-ttu-id="5e176-1103">Hadoop、Storm</span><span class="sxs-lookup"><span data-stu-id="5e176-1103">Hadoop, Storm</span></span></td>
<td><span data-ttu-id="5e176-1104">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1104">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1105">Visual Studio 工具</span><span class="sxs-lookup"><span data-stu-id="5e176-1105">Visual Studio tooling</span></span></td>
<td><span data-ttu-id="5e176-1106">除了 Apache Storm 的完整工具，Visual Studio 中的 Apache Hive 工具也已更新到包含陳述式完成、本機驗證和改進的偵錯支援。</span><span class="sxs-lookup"><span data-stu-id="5e176-1106">In addition to complete tooling for Apache Storm, the tooling for Apache Hive in Visual Studio has been updated to include statement completion, local validation, and improved debugging support.</span></span> <span data-ttu-id="5e176-1107">如需詳細資訊，請參閱＜開始使用 HDInsight Tools for Visual Studio＞。</span><span class="sxs-lookup"><span data-stu-id="5e176-1107">For more information, see Get Started with HDInsight Hadoop Tools for Visual Studio.</span></span></td>
<td><span data-ttu-id="5e176-1108">工具</span><span class="sxs-lookup"><span data-stu-id="5e176-1108">Tooling</span></span></td>
<td><span data-ttu-id="5e176-1109">Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e176-1109">Hadoop</span></span></td>
<td><span data-ttu-id="5e176-1110">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1110">N/A</span></span></td>
</tr>
<td><span data-ttu-id="5e176-1111">適用於 Azure Cosmos DB 的 Hadoop Connector</span><span class="sxs-lookup"><span data-stu-id="5e176-1111">Hadoop Connector for Azure Cosmos DB</span></span></td>
<td><span data-ttu-id="5e176-1112">使用適用於 Azure Cosmos DB 的 Hadoop Connector，您可以針對儲存在 Azure Cosmos DB 集合之間或資料庫帳戶之間的無結構描述 JSON 文件，執行複雜的彙總、分析與操作。</span><span class="sxs-lookup"><span data-stu-id="5e176-1112">With Hadoop Connector for Azure Cosmos DB, you can perform complex aggregations, analysis, and manipulations over your schema-less JSON documents stored across Azure Cosmos DB collections or across database accounts.</span></span> <span data-ttu-id="5e176-1113">如需詳細資訊和教學課程，請參閱＜使用 Azure Cosmos DB 和 HDInsight 執行 Hadoop 作業＞。</span><span class="sxs-lookup"><span data-stu-id="5e176-1113">For more information and a tutorial, see Run Hadoop jobs using Azure Cosmos DB and HDInsight.</span></span></td>
<td><span data-ttu-id="5e176-1114">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-1114">Service</span></span></td>
<td><span data-ttu-id="5e176-1115">Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e176-1115">Hadoop</span></span></td>
<td><span data-ttu-id="5e176-1116">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1116">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1117">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="5e176-1117">Bug fixes</span></span></td>
<td><span data-ttu-id="5e176-1118">我們為 HDInsight 服務提供了各種次要 Bug 修正。</span><span class="sxs-lookup"><span data-stu-id="5e176-1118">We have made various minor bug fixes for HDInsight services.</span></span> <span data-ttu-id="5e176-1119">不應有面向客戶的行為變更。</span><span class="sxs-lookup"><span data-stu-id="5e176-1119">No customer-facing behavior changes are expected.</span></span></td>
<td><span data-ttu-id="5e176-1120">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-1120">Service</span></span></td>
<td><span data-ttu-id="5e176-1121">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1121">All</span></span></td>
<td><span data-ttu-id="5e176-1122">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1122">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-02062015-release-of-hdinsight"></a><span data-ttu-id="5e176-1123">HDInsight 2015/02/06 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1123">Notes for 02/06/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-1124">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-1124">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-1125">HDInsight     2.1.10.463.1325367    (HDP 1.3.9.0-01351 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1125">HDInsight     2.1.10.463.1325367    (HDP 1.3.9.0-01351 - unchanged)</span></span>
* <span data-ttu-id="5e176-1126">HDInsight     3.0.6.463.1325367    (HDP 2.0.9.0-2097 -  未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1126">HDInsight     3.0.6.463.1325367    (HDP 2.0.9.0-2097 -  unchanged)</span></span>
* <span data-ttu-id="5e176-1127">HDInsight     3.1.2.463.1325367    (HDP 2.1.10.0-2290)</span><span class="sxs-lookup"><span data-stu-id="5e176-1127">HDInsight     3.1.2.463.1325367    (HDP 2.1.10.0-2290)</span></span>
* <span data-ttu-id="5e176-1128">SDK            N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1128">SDK            N/A</span></span>

<span data-ttu-id="5e176-1129">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-1129">This release contains the following updates:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-1130">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-1130">Title</span></span></th>
<th><span data-ttu-id="5e176-1131">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-1131">Description</span></span></th>
<th><span data-ttu-id="5e176-1132">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-1132">Impacted Area (for example, Service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-1133">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-1133">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-1134">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-1134">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-1135">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="5e176-1135">Bug fixes</span></span></td>
<td><span data-ttu-id="5e176-1136">我們為 HDInsight 服務提供了各種次要 Bug 修正。</span><span class="sxs-lookup"><span data-stu-id="5e176-1136">We have made various minor bug fixes for HDInsight services.</span></span> <span data-ttu-id="5e176-1137">不應有面向客戶的行為變更。</span><span class="sxs-lookup"><span data-stu-id="5e176-1137">No customer-facing behavior changes are expected.</span></span></td>
<td><span data-ttu-id="5e176-1138">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-1138">Service</span></span></td>
<td><span data-ttu-id="5e176-1139">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1139">All</span></span></td>
<td><span data-ttu-id="5e176-1140">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1140">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1141">HDP 2.1 維護更新</span><span class="sxs-lookup"><span data-stu-id="5e176-1141">HDP 2.1 maintenance update</span></span></td>
<td><span data-ttu-id="5e176-1142">已更新 HDInsight 3.1 以部署 HDP 2.1.10.0。</span><span class="sxs-lookup"><span data-stu-id="5e176-1142">HDInsight 3.1 is updated to deploy HDP 2.1.10.0.</span></span> <span data-ttu-id="5e176-1143">如需詳細資訊，請參閱<a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.10/bk_releasenotes_hdp_2.1/content/ch_relnotes-HDP-2.1.10.html" target="_blank">版本資訊 HDP-2.1.10</a>。</span><span class="sxs-lookup"><span data-stu-id="5e176-1143">For more information, see <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.10/bk_releasenotes_hdp_2.1/content/ch_relnotes-HDP-2.1.10.html" target="_blank">Release Notes HDP-2.1.10</a>.</span></span> </td>
<td><span data-ttu-id="5e176-1144">開放原始碼軟體</span><span class="sxs-lookup"><span data-stu-id="5e176-1144">Open-source software</span></span></td>
<td><span data-ttu-id="5e176-1145">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1145">All</span></span></td>
<td><span data-ttu-id="5e176-1146">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1146">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1147">HDP 二進位更新</span><span class="sxs-lookup"><span data-stu-id="5e176-1147">HDP binary updates</span></span></td>
<td><span data-ttu-id="5e176-1148">HBase 中有一些 JAR 檔的檔案名稱已更新。</span><span class="sxs-lookup"><span data-stu-id="5e176-1148">There are a few JAR files in HBase for which file names have been updated.</span></span> <span data-ttu-id="5e176-1149">這些 JAR 檔由 HBase 做為內部使用，因此客戶不應對這些 JAR 檔的名稱有相依性。</span><span class="sxs-lookup"><span data-stu-id="5e176-1149">These JAR files are used internally by HBase, so it is not expected that customers have a dependency on the names of these JAR files.</span></span> <span data-ttu-id="5e176-1150">其中包含：</span><span class="sxs-lookup"><span data-stu-id="5e176-1150">These include:</span></span>
<ul>
<li><span data-ttu-id="5e176-1151">./lib/jetty-6.1.26.hwx.jar</span><span class="sxs-lookup"><span data-stu-id="5e176-1151">./lib/jetty-6.1.26.hwx.jar</span></span></li>
<li><span data-ttu-id="5e176-1152">./lib/jetty-sslengine-6.1.26.hwx.jar</span><span class="sxs-lookup"><span data-stu-id="5e176-1152">./lib/jetty-sslengine-6.1.26.hwx.jar</span></span></li>
<li><span data-ttu-id="5e176-1153">./lib/jetty-util-6.1.26.hwx.jar</span><span class="sxs-lookup"><span data-stu-id="5e176-1153">./lib/jetty-util-6.1.26.hwx.jar</span></span></li>
</ul>
</td>
<td><span data-ttu-id="5e176-1154">開放原始碼軟體</span><span class="sxs-lookup"><span data-stu-id="5e176-1154">Open-source software</span></span></td>
<td><span data-ttu-id="5e176-1155">HBase</span><span class="sxs-lookup"><span data-stu-id="5e176-1155">HBase</span></span></td>
<td><span data-ttu-id="5e176-1156">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1156">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-1292015-release-of-hdinsight"></a><span data-ttu-id="5e176-1157">HDInsight 2015/1/29 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1157">Notes for 1/29/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-1158">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-1158">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-1159">HDInsight     2.1.10.455.1309616    (HDP 1.3.9.0-01351 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1159">HDInsight     2.1.10.455.1309616    (HDP 1.3.9.0-01351 - unchanged)</span></span>
* <span data-ttu-id="5e176-1160">HDInsight     3.0.6.455.1309616    (HDP 2.0.9.0-2097 -  未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1160">HDInsight     3.0.6.455.1309616    (HDP 2.0.9.0-2097 -  unchanged)</span></span>
* <span data-ttu-id="5e176-1161">HDInsight     3.1.2.455.1309616    (HDP 2.1.9.0-2196 -  未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1161">HDInsight     3.1.2.455.1309616    (HDP 2.1.9.0-2196 -  unchanged)</span></span>
* <span data-ttu-id="5e176-1162">SDK            N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1162">SDK            N/A</span></span>

<span data-ttu-id="5e176-1163">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-1163">This release contains the following update:</span></span>

<table border="1">

<tr>
<th><span data-ttu-id="5e176-1164">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-1164">Title</span></span></th>
<th><span data-ttu-id="5e176-1165">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-1165">Description</span></span></th>
<th><span data-ttu-id="5e176-1166">受影響的區域 (例如服務、元件或 SDK)</span><span class="sxs-lookup"><span data-stu-id="5e176-1166">Impacted Area (for example, Service, component, or SDK)</span></span></p></th>
<th><span data-ttu-id="5e176-1167">叢集類型 (例如 Hadoop、HBase 或 Storm)</span><span class="sxs-lookup"><span data-stu-id="5e176-1167">Cluster Type (for example, Hadoop, HBase, or Storm)</span></span></th>
<th><span data-ttu-id="5e176-1168">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-1168">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-1169">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="5e176-1169">Bug fixes</span></span></td>
<td><span data-ttu-id="5e176-1170">我們做了一些重要 Bug 修正，可以改善 HDInsight 叢集在 Azure 升級期間的可靠性。</span><span class="sxs-lookup"><span data-stu-id="5e176-1170">We have made a few important bug fixes that improve the reliability of the HDInsight Clusters during Azure upgrades.</span></span></td>
<td><span data-ttu-id="5e176-1171">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-1171">Service</span></span></td>
<td><span data-ttu-id="5e176-1172">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1172">All</span></span></td>
<td><span data-ttu-id="5e176-1173">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1173">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-152015-release-of-hdinsight"></a><span data-ttu-id="5e176-1174">HDInsight 2015/1/5 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1174">Notes for 1/5/2015 release of HDInsight</span></span>
<span data-ttu-id="5e176-1175">使用此版本部署的 HDInsight 叢集的完整版本號碼：</span><span class="sxs-lookup"><span data-stu-id="5e176-1175">The full version numbers for HDInsight clusters deployed with this release:</span></span>

* <span data-ttu-id="5e176-1176">HDInsight     2.1.10.420.1246118    (HDP 1.3.9.0-01351 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1176">HDInsight     2.1.10.420.1246118    (HDP 1.3.9.0-01351 - unchanged)</span></span>
* <span data-ttu-id="5e176-1177">HDInsight     3.0.6.420.1246118    (HDP 2.0.9.0-2097 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1177">HDInsight     3.0.6.420.1246118    (HDP 2.0.9.0-2097 - unchanged)</span></span>
* <span data-ttu-id="5e176-1178">HDInsight     3.1.2.420.1246118    (HDP 2.1.9.0-2196 - 未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1178">HDInsight     3.1.2.420.1246118    (HDP 2.1.9.0-2196 - unchanged)</span></span>

<span data-ttu-id="5e176-1179">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-1179">This release contains the following updates:</span></span>

<table border="1">

<tr>
<th><span data-ttu-id="5e176-1180">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-1180">Title</span></span></th>
<th><span data-ttu-id="5e176-1181">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-1181">Description</span></span></th>
<th><span data-ttu-id="5e176-1182">元件</span><span class="sxs-lookup"><span data-stu-id="5e176-1182">Component</span></span></th>
<th><span data-ttu-id="5e176-1183">叢集類型</span><span class="sxs-lookup"><span data-stu-id="5e176-1183">Cluster Type</span></span></th>
<th><span data-ttu-id="5e176-1184">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-1184">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-1185">Twitter 趨勢分析及 Mahout 電影推薦的範例</span><span class="sxs-lookup"><span data-stu-id="5e176-1185">Samples for Twitter trend analysis and Mahout-based movie recommendations</span></span></td>
<td><p><span data-ttu-id="5e176-1186">在此版本中，HDInsight 查詢主控台有兩個其他範例：</span><span class="sxs-lookup"><span data-stu-id="5e176-1186">In this release, the HDInsight Query console has two additional samples:</span></span></p>

<p><span data-ttu-id="5e176-1187"><b>Twitter 趨勢分析</b></span><span class="sxs-lookup"><span data-stu-id="5e176-1187"><b>Twitter Trend Analysis</b></span></span><br>
<span data-ttu-id="5e176-1188">像 Twitter 之類的網站所提供的公開 API，是分析和了解流行趨勢的一項實用的資料來源。</span><span class="sxs-lookup"><span data-stu-id="5e176-1188">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span> <span data-ttu-id="5e176-1189">在此教學課程中，了解如何使用 Hive 取得傳送最多包含特定字之推文的 Twitter 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="5e176-1189">In this tutorial, learn how to use Hive to get a list of Twitter users that sent the most tweets containing a particular word.</span></span> </p>

<p><span data-ttu-id="5e176-1190"><b>Mahout 電影推薦</b></span><span class="sxs-lookup"><span data-stu-id="5e176-1190"><b>Mahout Movie Recommendation</b></span></span><br>
<span data-ttu-id="5e176-1191">Apache Mahout 是 Apache Hadoop 的機器學習庫。</span><span class="sxs-lookup"><span data-stu-id="5e176-1191">Apache Mahout is an Apache Hadoop machine learning library.</span></span> <span data-ttu-id="5e176-1192">Mahout 包含用來處理資料 (例如篩選、分類和叢集化) 的演算法。</span><span class="sxs-lookup"><span data-stu-id="5e176-1192">Mahout contains algorithms for processing data (such as filtering, classification, and clustering).</span></span> <span data-ttu-id="5e176-1193">在本教學課程中，請使用推薦引擎，根據朋友看過的電影來產生電影推薦。</span><span class="sxs-lookup"><span data-stu-id="5e176-1193">In this tutorial, use a recommendation engine to generate movie recommendations based on movies that your friends have seen.</span></span></p></td>
<td><span data-ttu-id="5e176-1194">查詢主控台</span><span class="sxs-lookup"><span data-stu-id="5e176-1194">Query console</span></span></td>
<td><span data-ttu-id="5e176-1195">Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e176-1195">Hadoop</span></span></td>
<td><span data-ttu-id="5e176-1196">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1196">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1197">將 Hive 組態 hive.auto.convert.join.noconditionaltask.size 變更為預設值</span><span class="sxs-lookup"><span data-stu-id="5e176-1197">Change to default value for Hive configuration: hive.auto.convert.join.noconditionaltask.size</span></span></td>
<td><p><span data-ttu-id="5e176-1198">這個大小組態適用於自動轉換的對應聯結。</span><span class="sxs-lookup"><span data-stu-id="5e176-1198">This size configuration applies to automatically converted map joins.</span></span> <span data-ttu-id="5e176-1199">值代表可以轉換成雜湊對應且可放入記憶體的資料表大小總和。</span><span class="sxs-lookup"><span data-stu-id="5e176-1199">The value represents the sum of the sizes of tables that can be converted to hash maps that fit in memory.</span></span> <span data-ttu-id="5e176-1200">在前版中，這個值從預設值 10 MB 增加到 128 MB。</span><span class="sxs-lookup"><span data-stu-id="5e176-1200">In a prior release, this value increased from the default value of 10 MB to 128 MB.</span></span> <span data-ttu-id="5e176-1201">但是新的 128 MB 值因為缺乏記憶體而導致工作失敗。</span><span class="sxs-lookup"><span data-stu-id="5e176-1201">However, the new value of 128 MB was causing jobs to fail due to lack of memory.</span></span> <span data-ttu-id="5e176-1202">此版本將預設值還原成 10MB。</span><span class="sxs-lookup"><span data-stu-id="5e176-1202">This release reverts the default value back to 10 MB.</span></span> <span data-ttu-id="5e176-1203">客戶仍然可以依據其查詢和資料表大小選擇在叢集建立期間覆寫此值。</span><span class="sxs-lookup"><span data-stu-id="5e176-1203">Customers can still choose to override this value during cluster creation, given their queries and table sizes.</span></span> <span data-ttu-id="5e176-1204">如需此設定和如何覆寫該設定的詳細資訊，請參閱 Hortonworks 文件中的<a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.0.2/ds_Hive/optimize-joins.html#JoinOptimization-OptimizeAutoJoinConversion" target="_blank">最佳化自動聯結轉換</a>。</span><span class="sxs-lookup"><span data-stu-id="5e176-1204">For more information about this setting and how to override it, see <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.0.2/ds_Hive/optimize-joins.html#JoinOptimization-OptimizeAutoJoinConversion" target="_blank">Optimize Auto Join Conversion</a> in Hortonworks documentation.</span></span> </p></td>
<td><span data-ttu-id="5e176-1205">Hive</span><span class="sxs-lookup"><span data-stu-id="5e176-1205">Hive</span></span></td>
<td><span data-ttu-id="5e176-1206">Hadoop、Hbase</span><span class="sxs-lookup"><span data-stu-id="5e176-1206">Hadoop, Hbase</span></span></td>
<td><span data-ttu-id="5e176-1207">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1207">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-12232014-release-of-hdinsight"></a><span data-ttu-id="5e176-1208">HDInsight 2014/12/23 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1208">Notes for 12/23/2014 release of HDInsight</span></span>
<span data-ttu-id="5e176-1209">使用此版本部署的 HDInsight 叢集的完整版本號碼為：</span><span class="sxs-lookup"><span data-stu-id="5e176-1209">The full version numbers for HDInsight clusters deployed with this release are:</span></span>

* <span data-ttu-id="5e176-1210">HDInsight     2.1.10.420.1246783    (HDP 版本未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1210">HDInsight     2.1.10.420.1246783    (HDP version unchanged)</span></span>
* <span data-ttu-id="5e176-1211">HDInsight     3.0.6.420.1246783    (HDP 版本未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1211">HDInsight     3.0.6.420.1246783    (HDP version unchanged)</span></span>
* <span data-ttu-id="5e176-1212">HDInsight     3.1.1.420.1246783    (HDP 版本未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1212">HDInsight     3.1.1.420.1246783    (HDP version unchanged)</span></span>

<span data-ttu-id="5e176-1213">此版本包含下列更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-1213">This release contains the following update:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-1214">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-1214">Title</span></span></th>
<th><span data-ttu-id="5e176-1215">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-1215">Description</span></span></th>
<th><span data-ttu-id="5e176-1216">元件</span><span class="sxs-lookup"><span data-stu-id="5e176-1216">Component</span></span></th>
<th><span data-ttu-id="5e176-1217">叢集類型</span><span class="sxs-lookup"><span data-stu-id="5e176-1217">Cluster Type</span></span></th>
<th><span data-ttu-id="5e176-1218">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-1218">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-1219">由於負載過度而發生間歇性叢集建立失敗</span><span class="sxs-lookup"><span data-stu-id="5e176-1219">Intermittent cluster creation failures due to excessive load</span></span></td>
<td><p><span data-ttu-id="5e176-1220">改善叢集建立期間下載 HDP 封裝的演算法，以便能更強大地處理由於負載過度而發生的失敗。</span><span class="sxs-lookup"><span data-stu-id="5e176-1220">Improved algorithm for downloading HDP packages during cluster creation enables more robust handling of failures due to excessive load.</span></span></p></td>
<td><span data-ttu-id="5e176-1221">服務</span><span class="sxs-lookup"><span data-stu-id="5e176-1221">Service</span></span></td>
<td><span data-ttu-id="5e176-1222">Hadoop、HBase、Storm</span><span class="sxs-lookup"><span data-stu-id="5e176-1222">Hadoop, Hbase, Storm</span></span></td>
<td><span data-ttu-id="5e176-1223">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1223">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-12182014-release-of-hdinsight"></a><span data-ttu-id="5e176-1224">HDInsight 2014/12/18 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1224">Notes for 12/18/2014 release of HDInsight</span></span>
<span data-ttu-id="5e176-1225">此版本包含下列元件更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-1225">This release contains the following component update:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-1226">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-1226">Title</span></span></th>
<th><span data-ttu-id="5e176-1227">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-1227">Description</span></span></th>
<th><span data-ttu-id="5e176-1228">元件</span><span class="sxs-lookup"><span data-stu-id="5e176-1228">Component</span></span></th>
<th><span data-ttu-id="5e176-1229">叢集類型</span><span class="sxs-lookup"><span data-stu-id="5e176-1229">Cluster Type</span></span></th>
<th><span data-ttu-id="5e176-1230">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-1230">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-1231"><a href = "hdinsight-hadoop-customize-cluster.md" target="_blank">叢集自訂公開上市</a></span><span class="sxs-lookup"><span data-stu-id="5e176-1231"><a href = "hdinsight-hadoop-customize-cluster.md" target="_blank">Cluster customization General Availability</a></span></span></td>
<td><p><span data-ttu-id="5e176-1232">自訂可讓您使用 Apache Hadoop 生態系統可用的專案來自訂 Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e176-1232">Customization provides the ability for you to customize your Azure HDInsight clusters with projects that are available from the Apache Hadoop ecosystem.</span></span> <span data-ttu-id="5e176-1233">有了這項新功能，您可以實驗並部署 Hadoop 專案至 Azure HDInsight。</span><span class="sxs-lookup"><span data-stu-id="5e176-1233">With this new feature, you can experiment and deploy Hadoop projects to Azure HDInsight.</span></span> <span data-ttu-id="5e176-1234">這是透過**指令碼動作**功能而啟用，它可以使用自訂指令碼，任意修改 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e176-1234">This is enabled through the **Script Action** feature, which can modify Hadoop clusters in arbitrary ways by using custom scripts.</span></span> <span data-ttu-id="5e176-1235">此自訂可在所有類型的 HDInsight 叢集上使用，包括 Hadoop、HBase 和 Storm。</span><span class="sxs-lookup"><span data-stu-id="5e176-1235">This customization is available on all types of HDInsight clusters including Hadoop, HBase, and Storm.</span></span> <span data-ttu-id="5e176-1236">為了示範此功能的威力，我們已記錄下安裝熱門 <a href = "hdinsight-hadoop-spark-install.md" target="_blank">Spark</a>、<a href = "hdinsight-hadoop-r-scripts.md" target="_blank">R</a>、<a href = "hdinsight-hadoop-solr-install.md" target="_blank">Solr</a> 和 <a href = "hdinsight-hadoop-giraph-install.md" target="_blank">Giraph</a> 模組的程序。</span><span class="sxs-lookup"><span data-stu-id="5e176-1236">To demonstrate the power of this capability, we have documented the process to install the popular <a href = "hdinsight-hadoop-spark-install.md" target="_blank">Spark</a>, <a href = "hdinsight-hadoop-r-scripts.md" target="_blank">R</a>, <a href = "hdinsight-hadoop-solr-install.md" target="_blank">Solr</a>, and <a href = "hdinsight-hadoop-giraph-install.md" target="_blank">Giraph</a> modules.</span></span> <span data-ttu-id="5e176-1237">此版本也加入讓客戶透過 Azure 入口網站指定自訂指令碼動作的功能、提供關於如何使用協助程式方法建置自訂指令碼動作的方針和最佳實務作法，以及提供如何測試指令碼動作的方針。</span><span class="sxs-lookup"><span data-stu-id="5e176-1237">This release also adds the capability for customers to specify their custom script action via the Azure portal, provides guidelines and best practices about how to build custom script actions using helper methods, and provides guidelines about how to test the script action.</span></span> </p></td>
<td><span data-ttu-id="5e176-1238">功能公開上市</span><span class="sxs-lookup"><span data-stu-id="5e176-1238">Feature General Availability</span></span></td>
<td><span data-ttu-id="5e176-1239">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1239">All</span></span></td>
<td><span data-ttu-id="5e176-1240">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1240">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-12052014-release-of-hdinsight"></a><span data-ttu-id="5e176-1241">HDInsight 2014/12/5 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1241">Notes for 12/05/2014 release of HDInsight</span></span>
<span data-ttu-id="5e176-1242">使用此版本部署的 HDInsight 叢集的完整版本號碼為：</span><span class="sxs-lookup"><span data-stu-id="5e176-1242">The full version numbers for HDInsight clusters deployed with this release are:</span></span>

* <span data-ttu-id="5e176-1243">HDInsight     2.1.9.406.1221105    (HDP 1.3.9.0-01351)</span><span class="sxs-lookup"><span data-stu-id="5e176-1243">HDInsight     2.1.9.406.1221105    (HDP 1.3.9.0-01351)</span></span>
* <span data-ttu-id="5e176-1244">HDInsight     3.0.5.406.1221105    (HDP 2.0.9.0-2097)</span><span class="sxs-lookup"><span data-stu-id="5e176-1244">HDInsight     3.0.5.406.1221105    (HDP 2.0.9.0-2097)</span></span>
* <span data-ttu-id="5e176-1245">HDInsight     3.1.1.406.1221105    (HDP 2.1.9.0-2196)</span><span class="sxs-lookup"><span data-stu-id="5e176-1245">HDInsight     3.1.1.406.1221105    (HDP 2.1.9.0-2196)</span></span>
* <span data-ttu-id="5e176-1246">HDInsight SDK N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1246">HDInsight SDK N/A</span></span>

<span data-ttu-id="5e176-1247">此版本包含下列元件更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-1247">This release contains the following component updates:</span></span>

<table border="1">
<tr>
<th><span data-ttu-id="5e176-1248">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-1248">Title</span></span></th>
<th><span data-ttu-id="5e176-1249">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-1249">Description</span></span></th>
<th><span data-ttu-id="5e176-1250">元件</span><span class="sxs-lookup"><span data-stu-id="5e176-1250">Component</span></span></th>
<th><span data-ttu-id="5e176-1251">叢集類型</span><span class="sxs-lookup"><span data-stu-id="5e176-1251">Cluster Type</span></span></th>
<th><span data-ttu-id="5e176-1252">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-1252">JIRA (if applicable)</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="5e176-1253">Bug 修正：將大量分割加入 Hive DDL 中的資料表時發生間歇性的錯誤</span><span class="sxs-lookup"><span data-stu-id="5e176-1253">Bug fix: Intermittent error while adding large numbers of partitions to a table in a Hive DDL</span></span> </td>
<td><p><span data-ttu-id="5e176-1254">將大量分割加入 Hive 資料表時，如果 Hive 中繼存放區資料庫發生間歇性的連接錯誤，則 Hive DDL 可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="5e176-1254">If there is an intermittent connection error with the Hive metastore database when adding a lot of partitions to a Hive table, the Hive DDL can fail.</span></span> <span data-ttu-id="5e176-1255">如果發生此失敗，您會在 Hive 錯誤記錄中看到下列陳述式：</span><span class="sxs-lookup"><span data-stu-id="5e176-1255">The following statement isseen in the Hive error log if this failure occurs:</span></span> </p><p><span data-ttu-id="5e176-1256">"錯誤 [main]：ql.Driver (SessionState.java:printError(547)) - 失敗：執行錯誤，從 org.apache.hadoop.hive.ql.exec.DDLTask 傳回代碼 1。</span><span class="sxs-lookup"><span data-stu-id="5e176-1256">"ERROR [main]: ql.Driver (SessionState.java:printError(547)) - FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask.</span></span> <span data-ttu-id="5e176-1257">MetaException(message:java.lang.RuntimeException: commitTransaction 已呼叫，但 openTransactionCalls = 0。</span><span class="sxs-lookup"><span data-stu-id="5e176-1257">MetaException(message:java.lang.RuntimeException: commitTransaction was called but openTransactionCalls = 0.</span></span> <span data-ttu-id="5e176-1258">這可能表示對 openTransaction/commitTransaction 進行不平衡的呼叫)"</span><span class="sxs-lookup"><span data-stu-id="5e176-1258">This probably indicates that there are unbalanced calls to openTransaction/commitTransaction)"</span></span></p></td>
<td><span data-ttu-id="5e176-1259">Hive</span><span class="sxs-lookup"><span data-stu-id="5e176-1259">Hive</span></span></td>
<td><span data-ttu-id="5e176-1260">Hadoop、Hbase</span><span class="sxs-lookup"><span data-stu-id="5e176-1260">Hadoop, Hbase</span></span></td>
<td><span data-ttu-id="5e176-1261">HIVE-482 (這是內部 JIRA，因此不可在外部加上引號。</span><span class="sxs-lookup"><span data-stu-id="5e176-1261">HIVE-482 (This is an internal JIRA, so it cannot be quoted externally.</span></span> <span data-ttu-id="5e176-1262">在此記錄供參考之用。)</span><span class="sxs-lookup"><span data-stu-id="5e176-1262">Noted here for reference.)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1263">Bug 修正：HDInsight 查詢主控台偶爾停止回應</span><span class="sxs-lookup"><span data-stu-id="5e176-1263">Bug fix: Occasional hang in the HDInsight Query Console</span></span></td>
<td><span data-ttu-id="5e176-1264">發生此情況時，可在 WebHCat 啟動器工作的 WebHCat 記錄中看到下列陳述：</span><span class="sxs-lookup"><span data-stu-id="5e176-1264">When this happens, the following statement can be seen in the WebHCat log for the WebHCat launcher job:</span></span> <p><span data-ttu-id="5e176-1265">"org.apache.hive.hcatalog.templeton.CatchallExceptionMapper | org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.yarn.exceptions.YarnRuntimeException): 無法載入歷程記錄檔 {歷程記錄檔的 wasb url}"</span><span class="sxs-lookup"><span data-stu-id="5e176-1265">"org.apache.hive.hcatalog.templeton.CatchallExceptionMapper | org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.yarn.exceptions.YarnRuntimeException): Could not load history file {wasb url to the history file}"</span></span></p></td>
<td><span data-ttu-id="5e176-1266">WebHCat</span><span class="sxs-lookup"><span data-stu-id="5e176-1266">WebHCat</span></span></td>
<td><span data-ttu-id="5e176-1267">Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e176-1267">Hadoop</span></span></td>
<td><span data-ttu-id="5e176-1268">HIVE-482 (這是內部 JIRA，因此不可在外部加上引號。</span><span class="sxs-lookup"><span data-stu-id="5e176-1268">HIVE-482 (This is an internal JIRA, so it cannot be quoted externally.</span></span> <span data-ttu-id="5e176-1269">在此記錄供參考之用。)</span><span class="sxs-lookup"><span data-stu-id="5e176-1269">Noted here for reference.)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1270">Bug 修正：Hbase 查詢延遲偶爾激增</span><span class="sxs-lookup"><span data-stu-id="5e176-1270">Bug fix: Occasional spike in latency of Hbase queries</span></span></td>
<td><span data-ttu-id="5e176-1271">如果發生這種情況，使用者會發現 Hbase 查詢延遲偶爾會激增 3 秒。</span><span class="sxs-lookup"><span data-stu-id="5e176-1271">If this happens, users will notice an occasional spike of 3 seconds in the latency of Hbase queries.</span></span> </td>
<td><span data-ttu-id="5e176-1272">HDInsight 叢集閘道</span><span class="sxs-lookup"><span data-stu-id="5e176-1272">HDInsight Cluster Gateway</span></span></td>
<td><span data-ttu-id="5e176-1273">HBase</span><span class="sxs-lookup"><span data-stu-id="5e176-1273">HBase</span></span></td>
<td><span data-ttu-id="5e176-1274">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1274">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1275">HDP JAR 檔案名稱變更</span><span class="sxs-lookup"><span data-stu-id="5e176-1275">HDP JAR file name changes</span></span></td>
<td><span data-ttu-id="5e176-1276">若為 HDI 叢集 3.0 版，HDP 安裝的內部 JAR 檔案有一些變更。</span><span class="sxs-lookup"><span data-stu-id="5e176-1276">For HDI cluster version 3.0, there a couple of changes to the internal JAR files installed by HDP.</span></span> <span data-ttu-id="5e176-1277">jetty-6.1.26.jar 已取代為 jetty-6.1.26.hwx.jar。</span><span class="sxs-lookup"><span data-stu-id="5e176-1277">jetty-6.1.26.jar has been replaced with jetty-6.1.26.hwx.jar.</span></span> <span data-ttu-id="5e176-1278">jetty-util-6.1.26.jar 已取代為 jetty-util-6.1.26.hwx.jar。</span><span class="sxs-lookup"><span data-stu-id="5e176-1278">jetty-util-6.1.26.jar has been replaced with jetty-util-6.1.26.hwx.jar.</span></span> <span data-ttu-id="5e176-1279">這些變更適用於 Hadoop、Mahout、WebHCat 和 Oozie 專案。</span><span class="sxs-lookup"><span data-stu-id="5e176-1279">These changes apply to Hadoop, Mahout, WebHCat and Oozie projects.</span></span></td>
<td><span data-ttu-id="5e176-1280">Hadoop、Mahout、WebHCat、Oozie</span><span class="sxs-lookup"><span data-stu-id="5e176-1280">Hadoop, Mahout, WebHCat, Oozie</span></span></td>
<td><span data-ttu-id="5e176-1281">Hadoop、HBase</span><span class="sxs-lookup"><span data-stu-id="5e176-1281">Hadoop, HBase</span></span></td>
<td><span data-ttu-id="5e176-1282">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1282">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-11212014-release-of-hdinsight"></a><span data-ttu-id="5e176-1283">HDInsight 2014/11/21 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1283">Notes for 11/21/2014 release of HDInsight</span></span>
<span data-ttu-id="5e176-1284">使用此版本部署的 HDInsight 叢集的完整版本號碼為：</span><span class="sxs-lookup"><span data-stu-id="5e176-1284">The full version numbers for HDInsight clusters deployed with this release are:</span></span>

* <span data-ttu-id="5e176-1285">HDInsight 2.1.9.382.1169709 (從 2014/11/14 後未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1285">HDInsight 2.1.9.382.1169709 (no change from 11/14/2014)</span></span>
* <span data-ttu-id="5e176-1286">HDInsight 3.0.5.382.1169709 (從 2014/11/14 後未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1286">HDInsight 3.0.5.382.1169709 (no change from 11/14/2014)</span></span>
* <span data-ttu-id="5e176-1287">HDInsight 3.1.1.382.1169709 (從 2014/11/14 後未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1287">HDInsight 3.1.1.382.1169709 (no change from 11/14/2014)</span></span>
* <span data-ttu-id="5e176-1288">HDInsight SDK 1.4.0</span><span class="sxs-lookup"><span data-stu-id="5e176-1288">HDInsight SDK 1.4.0</span></span>

<span data-ttu-id="5e176-1289">此版本包含下列元件更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-1289">This release contains the following component updates:</span></span>

<table border="1">
<tr><th><span data-ttu-id="5e176-1290">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-1290">Title</span></span></th><th><span data-ttu-id="5e176-1291">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-1291">Description</span></span></th><th><span data-ttu-id="5e176-1292">元件</span><span class="sxs-lookup"><span data-stu-id="5e176-1292">Component</span></span></th><th><span data-ttu-id="5e176-1293">叢集類型</span><span class="sxs-lookup"><span data-stu-id="5e176-1293">Cluster Type</span></span></th><th><span data-ttu-id="5e176-1294">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-1294">JIRA (if applicable)</span></span></th></tr>
<tr>
<td><span data-ttu-id="5e176-1295">存取應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="5e176-1295">Accessing application logs</span></span></td>
<td><span data-ttu-id="5e176-1296">您能夠以程式設計的方式列舉在叢集上執行的應用程式，並下載相關的應用程式特定或容器特定記錄以協助偵錯有問題的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e176-1296">Ability to programmatically enumerate applications that have been run on your clusters and to download relevant application-specific or container-specific logs to help debug problematic applications.</span></span></td>
<td><span data-ttu-id="5e176-1297">SDK</span><span class="sxs-lookup"><span data-stu-id="5e176-1297">SDK</span></span></td>
<td><span data-ttu-id="5e176-1298">Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e176-1298">Hadoop</span></span></td>
<td><span data-ttu-id="5e176-1299">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1299">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1300">在 IHdInsightClient.DeleteCluster 中指定地區名稱的能力</span><span class="sxs-lookup"><span data-stu-id="5e176-1300">Ability to specify region name in IHdInsightClient.DeleteCluster</span></span> </td>
<td><span data-ttu-id="5e176-1301">Azure HDInsight SDK 提供在使用 **DeleteCluster** 時指定區域名稱的能力。</span><span class="sxs-lookup"><span data-stu-id="5e176-1301">The Azure HDInsight SDK provides the ability to specify a region name when using **DeleteCluster**.</span></span> <span data-ttu-id="5e176-1302">這有助於解除封鎖在不同地區擁有兩個同名資源且已無法刪除任一資源的客戶。</span><span class="sxs-lookup"><span data-stu-id="5e176-1302">This helps unblock customers who had two resources with same name in different regions and had been unable to delete either of them.</span></span></td>
<td><span data-ttu-id="5e176-1303">SDK</span><span class="sxs-lookup"><span data-stu-id="5e176-1303">SDK</span></span></td>
<td><span data-ttu-id="5e176-1304">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1304">All</span></span></td>
<td><span data-ttu-id="5e176-1305">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1305">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1306">ClusterDetails.DeploymentId</span><span class="sxs-lookup"><span data-stu-id="5e176-1306">ClusterDetails.DeploymentId</span></span></td>
<td><span data-ttu-id="5e176-1307">**ClusterDetails** 物件會傳回 **DeploymentID** 欄位，它代表叢集的唯一識別項。</span><span class="sxs-lookup"><span data-stu-id="5e176-1307">The **ClusterDetails** object returns a **DeploymentID** field that represents a unique identifier for the cluster.</span></span> <span data-ttu-id="5e176-1308">這可在具相同名稱跨叢集建立嘗試時，保證有唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="5e176-1308">It is guaranteed to be unique across cluster creation attempts with the same names.</span></span></td>
<td><span data-ttu-id="5e176-1309">SDK</span><span class="sxs-lookup"><span data-stu-id="5e176-1309">SDK</span></span></td>
<td><span data-ttu-id="5e176-1310">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1310">All</span></span></td>
<td><span data-ttu-id="5e176-1311">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1311">N/A</span></span></td>
</tr>
</table>

## <a name="notes-for-11142014-release-of-hdinsight"></a><span data-ttu-id="5e176-1312">HDInsight 2014/11/14 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1312">Notes for 11/14/2014 release of HDInsight</span></span>

<span data-ttu-id="5e176-1313">使用此版本部署的 HDInsight 叢集的完整版本號碼為：</span><span class="sxs-lookup"><span data-stu-id="5e176-1313">The full version numbers for HDInsight clusters deployed with this release are:</span></span>

* <span data-ttu-id="5e176-1314">HDInsight 2.1.9.382.1169709</span><span class="sxs-lookup"><span data-stu-id="5e176-1314">HDInsight 2.1.9.382.1169709</span></span>
* <span data-ttu-id="5e176-1315">HDInsight 3.0.5.382.1169709</span><span class="sxs-lookup"><span data-stu-id="5e176-1315">HDInsight 3.0.5.382.1169709</span></span>
* <span data-ttu-id="5e176-1316">HDInsight 3.1.1.382.1169709</span><span class="sxs-lookup"><span data-stu-id="5e176-1316">HDInsight 3.1.1.382.1169709</span></span>

<span data-ttu-id="5e176-1317">此版本包含下列新功能、元件更新和 Bug 修正。</span><span class="sxs-lookup"><span data-stu-id="5e176-1317">This release contains the following new features, component updates, and bug fixes.</span></span>

<table border="1">
<tr><th><span data-ttu-id="5e176-1318">課程名稱</span><span class="sxs-lookup"><span data-stu-id="5e176-1318">Title</span></span></th><th><span data-ttu-id="5e176-1319">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-1319">Description</span></span></th><th><span data-ttu-id="5e176-1320">元件</span><span class="sxs-lookup"><span data-stu-id="5e176-1320">Component</span></span></th><th><span data-ttu-id="5e176-1321">叢集類型</span><span class="sxs-lookup"><span data-stu-id="5e176-1321">Cluster Type</span></span></th><th><span data-ttu-id="5e176-1322">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-1322">JIRA (if applicable)</span></span></th></tr>
<tr>
<td><span data-ttu-id="5e176-1323">指令碼動作 (預覽)</span><span class="sxs-lookup"><span data-stu-id="5e176-1323">Script Action (Preview)</span></span></td>
<td><span data-ttu-id="5e176-1324">叢集自訂功能的預覽，可使用自訂指令碼以任意方式來修改 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e176-1324">Preview of the cluster customization feature that enables modification of Hadoop clusters in arbitrary ways by using custom scripts.</span></span> <span data-ttu-id="5e176-1325">有了此功能，使用者可實驗從 Apache Hadoop 生態系統取得的專案，以及將專案部署到 Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e176-1325">With this feature, users can experiment with and deploy projects that are available from the Apache Hadoop ecosystem to Azure HDInsight clusters.</span></span> <span data-ttu-id="5e176-1326">此自訂功能可在所有類型的 HDInsight 叢集上使用，包括 Hadoop、HBase 和 Storm。</span><span class="sxs-lookup"><span data-stu-id="5e176-1326">This customization feature is available on all types of HDInsight clusters, including Hadoop, HBase, and Storm.</span></span></td>
<td><span data-ttu-id="5e176-1327">新功能</span><span class="sxs-lookup"><span data-stu-id="5e176-1327">New feature</span></span></td>
<td><span data-ttu-id="5e176-1328">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1328">All</span></span></td>
<td><span data-ttu-id="5e176-1329">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1329">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1330">為 Azure 網站與儲存體記錄分析先行建置的工作</span><span class="sxs-lookup"><span data-stu-id="5e176-1330">Prebuilt jobs for Azure websites and storage log analysis</span></span></td>
<td><span data-ttu-id="5e176-1331">HDInsight 查詢主控台具有使用者入門庫，其支援在您的資料或資料範例上運作的方案。</span><span class="sxs-lookup"><span data-stu-id="5e176-1331">The HDInsight Query Console has a Getting Started gallery that supports solutions that work on your data or on sample data.</span></span>
<p><span data-ttu-id="5e176-1332">**在您資料上運作的方案**：</span><span class="sxs-lookup"><span data-stu-id="5e176-1332">**Solutions that work on your data**:</span></span><br>
<span data-ttu-id="5e176-1333">我們已經為部分最常見的資料分析案例建立工作，以做為建立您自己的方案的起點。</span><span class="sxs-lookup"><span data-stu-id="5e176-1333">We've created jobs for some of the most common data analysis scenarios to provide a starting point for creating your own solutions.</span></span> <span data-ttu-id="5e176-1334">您可以執行工作來使用您的資料，以查看其運作方式。</span><span class="sxs-lookup"><span data-stu-id="5e176-1334">You can use your data with the job to see how it works.</span></span> <span data-ttu-id="5e176-1335">接著在就緒時，使用已學得的知識來建立您在預先建立工作後所製作的方案模型。</span><span class="sxs-lookup"><span data-stu-id="5e176-1335">Then when you are ready, use what you have learned to create a solution that is modeled after the prebuilt job.</span></span></p>
<p><span data-ttu-id="5e176-1336">**在資料範例上運作的方案**：</span><span class="sxs-lookup"><span data-stu-id="5e176-1336">**Solutions that work on sample data**:</span></span><br>
<span data-ttu-id="5e176-1337">逐步執行部分基本案例 (例如分析 Web 記錄和感應器資料) 來了解如何使用 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="5e176-1337">Learn how to work with HDInsight by walking through some basic scenarios (such as analyzing web logs and sensor data).</span></span> <span data-ttu-id="5e176-1338">您會了解如何使用 HDInsight 來分析此類資料，以及如何將其他應用程式和服務連線至此資料。</span><span class="sxs-lookup"><span data-stu-id="5e176-1338">You learn how to use HDInsight to analyze such data and how you can connect other applications and services to this data.</span></span> <span data-ttu-id="5e176-1339">藉由連線至 Microsoft Excel 來提供此強大方案範例，藉此視覺化資料。</span><span class="sxs-lookup"><span data-stu-id="5e176-1339">Visualizing data by connecting to Microsoft Excel provides an example of the power of this approach.</span></span></p></td>
<td><span data-ttu-id="5e176-1340">查詢主控台</span><span class="sxs-lookup"><span data-stu-id="5e176-1340">Query console</span></span></td>
<td><span data-ttu-id="5e176-1341">Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e176-1341">Hadoop</span></span></td>
<td><span data-ttu-id="5e176-1342">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1342">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1343">Templeton 中的記憶體遺漏修正</span><span class="sxs-lookup"><span data-stu-id="5e176-1343">Memory leak fix in Templeton</span></span></td>
<td><span data-ttu-id="5e176-1344">已解決 Templeton 中的記憶體流失，該問題會影響已長期執行叢集的客戶，或每秒提交數百次工作要求的客戶。</span><span class="sxs-lookup"><span data-stu-id="5e176-1344">A memory leak in Templeton that affected customers who had long running clusters or were submitting 100s of job requests a second has been addressed.</span></span> <span data-ttu-id="5e176-1345">此問題會顯示為 Templeton 5xx 錯誤，且因應措施為重新啟動服務。</span><span class="sxs-lookup"><span data-stu-id="5e176-1345">The issue manifested as Templeton 5xx errors and the workaround was to restart the service.</span></span> <span data-ttu-id="5e176-1346">不再需要此因應措施。</span><span class="sxs-lookup"><span data-stu-id="5e176-1346">The workaround is no longer needed.</span></span></td>
<td><span data-ttu-id="5e176-1347">Templeton</span><span class="sxs-lookup"><span data-stu-id="5e176-1347">Templeton</span></span></td>
<td><span data-ttu-id="5e176-1348">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1348">All</span></span></td>
<td><span data-ttu-id="5e176-1349">https://issues.apache.org/jira/browse/HADOOP-11248</span><span class="sxs-lookup"><span data-stu-id="5e176-1349">https://issues.apache.org/jira/browse/HADOOP-11248</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="5e176-1350">為了示範叢集自訂所提供的新功能，已記錄使用指令碼動作在叢集上安裝 Spark 和 R 模組的程序。</span><span class="sxs-lookup"><span data-stu-id="5e176-1350">To demonstrate the new capabilities made available by cluster customization, the procedures using Script Action to install Spark and R modules on a cluster have been documented.</span></span> <span data-ttu-id="5e176-1351">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5e176-1351">For more information, see:</span></span>

* [<span data-ttu-id="5e176-1352">在 HDInsight 叢集上安裝和使用 Spark 1.0</span><span class="sxs-lookup"><span data-stu-id="5e176-1352">Install and use Spark 1.0 on HDInsight clusters</span></span>](hdinsight-hadoop-spark-install.md)
* [<span data-ttu-id="5e176-1353">在 HDInsight Hadoop 叢集上安裝和使用 R</span><span class="sxs-lookup"><span data-stu-id="5e176-1353">Install and use R on HDInsight Hadoop clusters</span></span>](hdinsight-hadoop-r-scripts.md)

## <a name="notes-for-11072014-release-of-hdinsight"></a><span data-ttu-id="5e176-1354">HDInsight 2014/11/07 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1354">Notes for 11/07/2014 release of HDInsight</span></span>

<span data-ttu-id="5e176-1355">使用此版本部署的 HDInsight 叢集的完整版本號碼為：</span><span class="sxs-lookup"><span data-stu-id="5e176-1355">The full version numbers for HDInsight clusters that deployed with this release are:</span></span>

* <span data-ttu-id="5e176-1356">HDInsight 2.1    2.1.9.374.1153876</span><span class="sxs-lookup"><span data-stu-id="5e176-1356">HDInsight 2.1    2.1.9.374.1153876</span></span>
* <span data-ttu-id="5e176-1357">HDInsight 3.0    3.0.5.374.1153876</span><span class="sxs-lookup"><span data-stu-id="5e176-1357">HDInsight 3.0    3.0.5.374.1153876</span></span>
* <span data-ttu-id="5e176-1358">HDInsight 3.1    3.1.1.374.1153876</span><span class="sxs-lookup"><span data-stu-id="5e176-1358">HDInsight 3.1    3.1.1.374.1153876</span></span>

<span data-ttu-id="5e176-1359">此版本包含下列元件更新：</span><span class="sxs-lookup"><span data-stu-id="5e176-1359">This release contains the following component updates:</span></span>

<table border="1">
<tr><th><span data-ttu-id="5e176-1360">Title</span><span class="sxs-lookup"><span data-stu-id="5e176-1360">Title</span></span></th><th><span data-ttu-id="5e176-1361">說明</span><span class="sxs-lookup"><span data-stu-id="5e176-1361">Description</span></span></th><th><span data-ttu-id="5e176-1362">元件</span><span class="sxs-lookup"><span data-stu-id="5e176-1362">Component</span></span></th><th><span data-ttu-id="5e176-1363">叢集類型</span><span class="sxs-lookup"><span data-stu-id="5e176-1363">Cluster Type</span></span></th><th><span data-ttu-id="5e176-1364">JIRA (如果適用)</span><span class="sxs-lookup"><span data-stu-id="5e176-1364">JIRA (if applicable)</span></span></th></tr>
<tr>
<td><span data-ttu-id="5e176-1365">HDP 2.1.7</span><span class="sxs-lookup"><span data-stu-id="5e176-1365">HDP 2.1.7</span></span></td>
<td><span data-ttu-id="5e176-1366">此版本根據 Hortonworks Data Platform (HDP) 2.1.7。</span><span class="sxs-lookup"><span data-stu-id="5e176-1366">This release is based on Hortonworks Data Platform (HDP) 2.1.7.</span></span> <span data-ttu-id="5e176-1367">如需詳細資訊，請參閱 <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html" target="_blank">HDP 2.1.7 的版本資訊</a>。</span><span class="sxs-lookup"><span data-stu-id="5e176-1367">For more information, see <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html" target="_blank">Release Notes for HDP 2.1.7</a>.</span></span></td>
<td><span data-ttu-id="5e176-1368">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-1368">HDP</span></span></td>
<td><span data-ttu-id="5e176-1369">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1369">All</span></span></td>
<td><span data-ttu-id="5e176-1370">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1370">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1371">YARN Timeline Server</span><span class="sxs-lookup"><span data-stu-id="5e176-1371">YARN Timeline Server</span></span></td>
<td><span data-ttu-id="5e176-1372">YARN Timeline Server (也稱為 Generic Application History Server) 預設已啟用。</span><span class="sxs-lookup"><span data-stu-id="5e176-1372">The YARN Timeline Server (also known as the Generic Application History Server) has been enabled by default.</span></span> <span data-ttu-id="5e176-1373">Timeline Server 提供已完成應用程式的泛型資訊 (例如應用程式 ID、應用程式名稱、應用程式狀態、應用程式提交時間及應用程式完成時間)。</span><span class="sxs-lookup"><span data-stu-id="5e176-1373">The Timeline Server provides generic information about completed applications (such as application ID, application name, application status, application submission time, and application completion time).</span></span>

<span data-ttu-id="5e176-1374">可透過存取 URI http://headnodehost:8188 或執行 YARN 命令：yarn application -list -appStates ALL，從前端節點擷取此應用程式資訊。</span><span class="sxs-lookup"><span data-stu-id="5e176-1374">This application information can be retrieved from the head node by accessing the URI http://headnodehost:8188 or by running the YARN command: yarn application -list -appStates ALL.</span></span>

<span data-ttu-id="5e176-1375">此資訊也可以透過 REST API 從 https://{ClusterDnsName}.</span><span class="sxs-lookup"><span data-stu-id="5e176-1375">This information can also be retrieved remotely though a REST API at https://{ClusterDnsName}.</span></span> <span data-ttu-id="5e176-1376">azurehdinsight.net/ws/v1/applicationhistory/ 遠端擷取。</span><span class="sxs-lookup"><span data-stu-id="5e176-1376">azurehdinsight.net/ws/v1/applicationhistory/.</span></span>

<span data-ttu-id="5e176-1377">如需詳細資訊，請參閱 <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a>。</span><span class="sxs-lookup"><span data-stu-id="5e176-1377">For more detailed information, see <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a>.</span></span></td>
<td><span data-ttu-id="5e176-1378">服務、YARN</span><span class="sxs-lookup"><span data-stu-id="5e176-1378">Service, YARN</span></span></td>
<td><span data-ttu-id="5e176-1379">Hadoop、HBase</span><span class="sxs-lookup"><span data-stu-id="5e176-1379">Hadoop, HBase</span></span></td>
<td><span data-ttu-id="5e176-1380">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1380">N/A</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5e176-1381">叢集部署 ID</span><span class="sxs-lookup"><span data-stu-id="5e176-1381">Cluster deployment ID</span></span></td>
<td><span data-ttu-id="5e176-1382">從 SDK 1.3.3.1.5426.29232 版開始，使用者可存取 HDInsight 發行給每個叢集的唯一 ID。</span><span class="sxs-lookup"><span data-stu-id="5e176-1382">Starting with SDK version 1.3.3.1.5426.29232, users can access a unique ID for each cluster, which is issued HDInsight.</span></span> <span data-ttu-id="5e176-1383">這能讓客戶在跨建立/捨棄案例重複使用 DNS 名稱時，找出叢集的唯一執行個體。</span><span class="sxs-lookup"><span data-stu-id="5e176-1383">This enables customers to figure out unique instances of clusters when a DNS name is being reused across create or drop scenarios.</span></span></td>
<td><span data-ttu-id="5e176-1384">SDK</span><span class="sxs-lookup"><span data-stu-id="5e176-1384">SDK</span></span></td>
<td><span data-ttu-id="5e176-1385">全部</span><span class="sxs-lookup"><span data-stu-id="5e176-1385">All</span></span></td>
<td><span data-ttu-id="5e176-1386">N/A</span><span class="sxs-lookup"><span data-stu-id="5e176-1386">N/A</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="5e176-1387">這個版本已修正防止入口網站顯示及防止 SDK 或 Windows PowerShell 傳回完整版本號碼的 Bug。</span><span class="sxs-lookup"><span data-stu-id="5e176-1387">The bug that prevented the full version number from showing up in the portal or from being returned by the SDK or by Windows PowerShell has been fixed in this release.</span></span>

## <a name="notes-for-10152014-release"></a><span data-ttu-id="5e176-1388">2014/10/15 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1388">Notes for 10/15/2014 release</span></span>

<span data-ttu-id="5e176-1389">此 Hotfix 版本修復 Templeton 中影響 Templeton 重度使用者的記憶體遺漏。</span><span class="sxs-lookup"><span data-stu-id="5e176-1389">This hotfix release fixed a memory leak in Templeton that affected the heavy users of Templeton.</span></span> <span data-ttu-id="5e176-1390">在某些情況下，Templeton 的重度使用者會看到以 500 錯誤碼表示的錯誤，因為要求沒有足夠的記憶體可執行。</span><span class="sxs-lookup"><span data-stu-id="5e176-1390">In some cases, users who exercised Templeton heavily would see errors manifested as 500 error codes because the requests would not have enough memory to run.</span></span> <span data-ttu-id="5e176-1391">重新啟動 Templeton 服務就能解決此問題。</span><span class="sxs-lookup"><span data-stu-id="5e176-1391">The workaround for this issue was to restart the Templeton service.</span></span> <span data-ttu-id="5e176-1392">已修正此問題。</span><span class="sxs-lookup"><span data-stu-id="5e176-1392">This issue has been fixed.</span></span>

## <a name="notes-for-1072014-release"></a><span data-ttu-id="5e176-1393">2014/10/7 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1393">Notes for 10/7/2014 release</span></span>

* <span data-ttu-id="5e176-1394">使用 Ambari 端點 "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}" 時，*host_name* 欄位會傳回節點的完整網域名稱 (FQDN)，而不只是主機名稱。</span><span class="sxs-lookup"><span data-stu-id="5e176-1394">When using Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", the *host_name* field returns the fully qualified domain name (FQDN) of the node instead of only the host name.</span></span> <span data-ttu-id="5e176-1395">例如，不是傳回 "**headnode0**"，而是傳回 FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**"。</span><span class="sxs-lookup"><span data-stu-id="5e176-1395">For example, instead of returning "**headnode0**", you get the FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**".</span></span> <span data-ttu-id="5e176-1396">需要此變更才能協助在一個虛擬網路中部署多種叢集類型 (例如 HBase 和 Hadoop) 的情況。</span><span class="sxs-lookup"><span data-stu-id="5e176-1396">This change was required to facilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network.</span></span> <span data-ttu-id="5e176-1397">例如，使用 HBase 做為 Hadoop 的後端平台時就是這種情形。</span><span class="sxs-lookup"><span data-stu-id="5e176-1397">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

* <span data-ttu-id="5e176-1398">我們為 HDInsight 叢集的預設部署提供新的記憶體設定。</span><span class="sxs-lookup"><span data-stu-id="5e176-1398">We have provided new memory settings for the default deployment of the HDInsight cluster.</span></span> <span data-ttu-id="5e176-1399">先前的預設記憶體設定並未充分考量所部署 CPU 核心數目的方針。</span><span class="sxs-lookup"><span data-stu-id="5e176-1399">Previous default memory settings did not adequately account for the guidance for the number of CPU cores being deployed.</span></span> <span data-ttu-id="5e176-1400">根據 Hortonworks 建議，這些新的記憶體設定應該提供更佳的預設值。</span><span class="sxs-lookup"><span data-stu-id="5e176-1400">These new memory settings should provide better defaults (as per Hortonworks recommendations).</span></span> <span data-ttu-id="5e176-1401">若要變更，請參閱關於變更叢集組態的 SDK 參考文件。</span><span class="sxs-lookup"><span data-stu-id="5e176-1401">To change these, refer to the SDK reference documentation about changing cluster configuration.</span></span> <span data-ttu-id="5e176-1402">下表列舉預設 4 CPU 核心 (8 容器) HDInsight 叢集所使用的新記憶體設定。</span><span class="sxs-lookup"><span data-stu-id="5e176-1402">The new memory settings that are used by the default 4 CPU core (8 container) HDInsight cluster are itemized in the following table.</span></span> <span data-ttu-id="5e176-1403">(同時也附帶提供此版本之前使用的值。)</span><span class="sxs-lookup"><span data-stu-id="5e176-1403">(The values used prior to this release are also provided parenthetically.)</span></span>

<table border="1">
<tr><th><span data-ttu-id="5e176-1404">元件</span><span class="sxs-lookup"><span data-stu-id="5e176-1404">Component</span></span></th><th><span data-ttu-id="5e176-1405">記憶體配置</span><span class="sxs-lookup"><span data-stu-id="5e176-1405">Memory Allocation</span></span></th></tr>
<tr><td> <span data-ttu-id="5e176-1406">yarn.scheduler.minimum-allocation</span><span class="sxs-lookup"><span data-stu-id="5e176-1406">yarn.scheduler.minimum-allocation</span></span></td><td><span data-ttu-id="5e176-1407">768 MB (先前是 512 MB)</span><span class="sxs-lookup"><span data-stu-id="5e176-1407">768 MB (previously 512 MB)</span></span></td></tr>
<tr><td> <span data-ttu-id="5e176-1408">yarn.scheduler.maximum-allocation</span><span class="sxs-lookup"><span data-stu-id="5e176-1408">yarn.scheduler.maximum-allocation</span></span></td><td><span data-ttu-id="5e176-1409">6144 MB (未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1409">6144 MB (unchanged)</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1410">yarn.nodemanager.resource.memory</span><span class="sxs-lookup"><span data-stu-id="5e176-1410">yarn.nodemanager.resource.memory</span></span></td><td><span data-ttu-id="5e176-1411">6144 MB (未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1411">6144 MB (unchanged)</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1412">mapreduce.map.memory</span><span class="sxs-lookup"><span data-stu-id="5e176-1412">mapreduce.map.memory</span></span></td><td><span data-ttu-id="5e176-1413">768 MB (先前是 512 MB)</span><span class="sxs-lookup"><span data-stu-id="5e176-1413">768 MB (previously 512 MB)</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1414">mapreduce.map.java.opts</span><span class="sxs-lookup"><span data-stu-id="5e176-1414">mapreduce.map.java.opts</span></span></td><td><span data-ttu-id="5e176-1415">opts=-Xmx512m (先前是 -Xmx410m)</span><span class="sxs-lookup"><span data-stu-id="5e176-1415">opts=-Xmx512m (previously -Xmx410m)</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1416">mapreduce.reduce.memory</span><span class="sxs-lookup"><span data-stu-id="5e176-1416">mapreduce.reduce.memory</span></span></td><td><span data-ttu-id="5e176-1417">1536 MB (先前是 1024 MB)</span><span class="sxs-lookup"><span data-stu-id="5e176-1417">1536 MB (previously 1024 MB)</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1418">mapreduce.reduce.java.opts</span><span class="sxs-lookup"><span data-stu-id="5e176-1418">mapreduce.reduce.java.opts</span></span></td><td><span data-ttu-id="5e176-1419">opts=-Xmx1024m (先前是 -Xmx819m)</span><span class="sxs-lookup"><span data-stu-id="5e176-1419">opts=-Xmx1024m (previously -Xmx819m)</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1420">yarn.app.mapreduce.am.resource</span><span class="sxs-lookup"><span data-stu-id="5e176-1420">yarn.app.mapreduce.am.resource</span></span></td><td><span data-ttu-id="5e176-1421">768 MB (先前是 1024 MB)</span><span class="sxs-lookup"><span data-stu-id="5e176-1421">768 MB (previously 1024 MB)</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1422">yarn.app.mapreduce.am.command</span><span class="sxs-lookup"><span data-stu-id="5e176-1422">yarn.app.mapreduce.am.command</span></span></td><td><span data-ttu-id="5e176-1423">opts=-Xmx512m (先前是 -Xmx819m)</span><span class="sxs-lookup"><span data-stu-id="5e176-1423">opts=-Xmx512m (previously -Xmx819m)</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1424">mapreduce.task.io.sort</span><span class="sxs-lookup"><span data-stu-id="5e176-1424">mapreduce.task.io.sort</span></span></td><td><span data-ttu-id="5e176-1425">256 MB (先前是 200 MB)</span><span class="sxs-lookup"><span data-stu-id="5e176-1425">256 MB (previously 200 MB)</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1426">tez.am.resource.memory</span><span class="sxs-lookup"><span data-stu-id="5e176-1426">tez.am.resource.memory</span></span></td><td><span data-ttu-id="5e176-1427">1536 MB (未變更)</span><span class="sxs-lookup"><span data-stu-id="5e176-1427">1536 MB (unchanged)</span></span></td></tr>
</table>

<span data-ttu-id="5e176-1428">如需 HDInsight 使用的 Hortonworks Data Platform 上供 YARN 和 MapReduce 使用的記憶體組態設定的詳細資訊，請參閱 [決定 HDP 記憶體組態設定](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1-latest/bk_installing_manually_book/content/rpm-chap1-11.html)。</span><span class="sxs-lookup"><span data-stu-id="5e176-1428">For more information about the memory configuration settings used by YARN and MapReduce on the Hortonworks Data Platform that is used by HDInsight, see [Determine HDP Memory Configuration Settings](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1-latest/bk_installing_manually_book/content/rpm-chap1-11.html).</span></span> <span data-ttu-id="5e176-1429">Hortonworks 也提供工具來計算適當的記憶體設定。</span><span class="sxs-lookup"><span data-stu-id="5e176-1429">Hortonworks also provided a tool to calculate proper memory settings.</span></span>

<span data-ttu-id="5e176-1430">關於 Azure PowerShell 和 HDInsight SDK 的錯誤訊息：「叢集未設定 HTTP 服務存取」：</span><span class="sxs-lookup"><span data-stu-id="5e176-1430">Regarding the Azure PowerShell and the HDInsight SDK error message: "*Cluster is not configured for HTTP services access*":</span></span>

* <span data-ttu-id="5e176-1431">此錯誤是已知的[相容性問題](https://social.msdn.microsoft.com/Forums/azure/a7de016d-8de1-4385-b89e-d2e7a1a9d927/hdinsight-powershellsdk-error-cluster-is-not-configured-for-http-services-access?forum=hdinsight)，起因可能是 HDInsight 或 Azure PowerShell 版本和叢集版本的差異。</span><span class="sxs-lookup"><span data-stu-id="5e176-1431">This error is a known [compatibility issue](https://social.msdn.microsoft.com/Forums/azure/a7de016d-8de1-4385-b89e-d2e7a1a9d927/hdinsight-powershellsdk-error-cluster-is-not-configured-for-http-services-access?forum=hdinsight) that may occur due to a difference in the version of the  HDInsight SDK or Azure PowerShell and the version of the cluster.</span></span> <span data-ttu-id="5e176-1432">在 8/15 或之後建立的叢集支援佈建到虛擬網路的這項新功能。</span><span class="sxs-lookup"><span data-stu-id="5e176-1432">Clusters created on 8/15 or later have support for new provisioning capability into virtual networks.</span></span> <span data-ttu-id="5e176-1433">但舊版的 HDInsight SDK 或 Azure PowerShell 無法正確解譯此功能。</span><span class="sxs-lookup"><span data-stu-id="5e176-1433">But this capability is not correctly interpreted by older versions of the  HDInsight SDK or Azure PowerShell.</span></span> <span data-ttu-id="5e176-1434">結果造成某些工作提交作業失敗。</span><span class="sxs-lookup"><span data-stu-id="5e176-1434">The result is a failure in some job submission operations.</span></span> <span data-ttu-id="5e176-1435">如果您使用 HDInsight SDK API 或 Azure PowerShell Cmdlet (**Use-AzureRmHDInsightCluster** 或 **Invoke-AzureRmHDInsightHiveJob**) 來提交工作，這些作業可能會失敗並傳回錯誤訊息「叢集 <clustername> 未設定 HTTP 服務存取」。</span><span class="sxs-lookup"><span data-stu-id="5e176-1435">If you use  HDInsight SDK APIs or Azure PowerShell cmdlets (**Use-AzureRmHDInsightCluster** or **Invoke-AzureRmHDInsightHiveJob**) to submit jobs, those operations may fail with the error message "*Cluster <clustername> is not configured for HTTP services access*."</span></span> <span data-ttu-id="5e176-1436">或者 (根據作業而定) 傳回其他錯誤訊息，例如「無法連接到叢集」。</span><span class="sxs-lookup"><span data-stu-id="5e176-1436">Or (depending on the operation), you may get other error messages, such as "*Cannot connect to cluster*".</span></span>
* <span data-ttu-id="5e176-1437">最新版的 HDInsight SDK 和 Azure PowerShell 中已解決這些相容性問題。</span><span class="sxs-lookup"><span data-stu-id="5e176-1437">These compatibility issues are resolved in the latest versions of the HDInsight SDK and Azure PowerShell.</span></span> <span data-ttu-id="5e176-1438">建議將 HDInsight SDK 更新到 1.3.1.6 版或更新版本，並將 Azure PowerShell 工具更新到 0.8.8 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="5e176-1438">We recommend updating the HDInsight SDK to version 1.3.1.6 or later and Azure PowerShell Tools to version 0.8.8 or later.</span></span> <span data-ttu-id="5e176-1439">您可以從 [NuGet](http://nuget.codeplex.com/wikipage?title=Getting%20Started) 取得最新的 HDInsight SDK，並從[如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 取得 Azure PowerShell 工具。</span><span class="sxs-lookup"><span data-stu-id="5e176-1439">You can get access to the latest HDInsight SDK from [NugGet](http://nuget.codeplex.com/wikipage?title=Getting%20Started) and the Azure PowerShell Tools at [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="notes-for-9122014-release-of-hdinsight-31"></a><span data-ttu-id="5e176-1440">HDInsight 3.1 2014/9/12 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1440">Notes for 9/12/2014 release of HDInsight 3.1</span></span>
* <span data-ttu-id="5e176-1441">此版本根據 Hortonworks Data Platform (HDP) 2.1.5。</span><span class="sxs-lookup"><span data-stu-id="5e176-1441">This release is based on Hortonworks Data Platform (HDP) 2.1.5.</span></span> <span data-ttu-id="5e176-1442">如需此版本中修正的 Bug 清單，請參閱 Hortonworks 網站上的 [已在此版本修正](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.5/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.5-fixed.html) 頁面。</span><span class="sxs-lookup"><span data-stu-id="5e176-1442">For a list of the bugs fixed in this release, see the [Fixed in this Release](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.5/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.5-fixed.html) page on the Hortonworks site.</span></span>
* <span data-ttu-id="5e176-1443">在 Pig 程式庫資料夾中，"avro-mapred-1.7.4.jar" 檔案已變更為 "avro-mapred-1.7.4-hadoop2.jar"。</span><span class="sxs-lookup"><span data-stu-id="5e176-1443">In the Pig libraries folder, the "avro-mapred-1.7.4.jar" file has been changed to "avro-mapred-1.7.4-hadoop2.jar."</span></span> <span data-ttu-id="5e176-1444">此檔案的內容包含非中斷的次要 Bug 修正。</span><span class="sxs-lookup"><span data-stu-id="5e176-1444">The contents of this file contains a minor bug fix that is non-breaking.</span></span> <span data-ttu-id="5e176-1445">建議客戶不要直接依賴 JAR 檔案的名稱，以避免檔案重新命名時中斷。</span><span class="sxs-lookup"><span data-stu-id="5e176-1445">It is recommended that customers do not make a direct dependency on the name of the JAR file to avoid breaks when files are renamed.</span></span>

## <a name="notes-for-8212014-release"></a><span data-ttu-id="5e176-1446">2014/8/21 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1446">Notes for 8/21/2014 release</span></span>
* <span data-ttu-id="5e176-1447">我們加入下列 WebHCat 組態 (HIVE-7155)，其將 Templeton 控制器工作的預設記憶體限制設為 1GB。</span><span class="sxs-lookup"><span data-stu-id="5e176-1447">We are adding the following WebHCat configuration (HIVE-7155), which sets the default memory limit for a Templeton controller job to 1 GB.</span></span> <span data-ttu-id="5e176-1448">(先前的預設值是 512 MB。)</span><span class="sxs-lookup"><span data-stu-id="5e176-1448">(The previous default value was 512 MB.)</span></span>

     <span data-ttu-id="5e176-1449">templeton.mapper.memory.mb (=1024)</span><span class="sxs-lookup"><span data-stu-id="5e176-1449">templeton.mapper.memory.mb (=1024)</span></span>

  * <span data-ttu-id="5e176-1450">此變更解決了某些 Hive 查詢因為記憶體限制較低而發生的下列錯誤：「容器超過實體記憶體限制」。</span><span class="sxs-lookup"><span data-stu-id="5e176-1450">This change addresses the following error with certain Hive queries due to lower memory limits: "Container is running beyond physical memory limits."</span></span>
  * <span data-ttu-id="5e176-1451">若要還原成舊的預設值，您可以在建立叢集時使用下列命令以透過 Azure PowerShell 將此組態值設為 512：</span><span class="sxs-lookup"><span data-stu-id="5e176-1451">To revert to the old defaults, you can set this configuration value to 512 through Azure PowerShell at cluster creation time by using the following command:</span></span>

      <span data-ttu-id="5e176-1452">Add-AzureRmHDInsightConfigValues -Core @{"templeton.mapper.memory.mb"="512";}</span><span class="sxs-lookup"><span data-stu-id="5e176-1452">Add-AzureRmHDInsightConfigValues -Core @{"templeton.mapper.memory.mb"="512";}</span></span>
* <span data-ttu-id="5e176-1453">Zookeeper 角色的主機名稱已變更為 *zookeeper*。</span><span class="sxs-lookup"><span data-stu-id="5e176-1453">The host name of the zookeeper role was changed to *zookeeper*.</span></span> <span data-ttu-id="5e176-1454">這會影響叢集內的名稱解析，但不影響外部 REST API。</span><span class="sxs-lookup"><span data-stu-id="5e176-1454">This affects name resolution within the cluster, but it doesn't affect external REST APIs.</span></span> <span data-ttu-id="5e176-1455">如果您有元件使用 *zookeepernode* 主機名稱，則必須更新元件以改用新名稱。</span><span class="sxs-lookup"><span data-stu-id="5e176-1455">If you have components that use the *zookeepernode* host name, you need to update them to use new name.</span></span> <span data-ttu-id="5e176-1456">三個 zookeeper 節點的新名稱如下：</span><span class="sxs-lookup"><span data-stu-id="5e176-1456">The new names for the three zookeeper nodes are:</span></span>

  * <span data-ttu-id="5e176-1457">zookeeper0</span><span class="sxs-lookup"><span data-stu-id="5e176-1457">zookeeper0</span></span>
  * <span data-ttu-id="5e176-1458">zookeeper1</span><span class="sxs-lookup"><span data-stu-id="5e176-1458">zookeeper1</span></span>
  * <span data-ttu-id="5e176-1459">zookeeper2</span><span class="sxs-lookup"><span data-stu-id="5e176-1459">zookeeper2</span></span>
* <span data-ttu-id="5e176-1460">已更新 HBase 版本支援矩陣。</span><span class="sxs-lookup"><span data-stu-id="5e176-1460">HBase version support matrix is updated.</span></span> <span data-ttu-id="5e176-1461">只有 HBase 工作負載的生產才能支援 HDInsight 3.1 版 (HBase 0.98 版)。</span><span class="sxs-lookup"><span data-stu-id="5e176-1461">Only HDInsight version 3.1 (HBase version 0.98) is supported for production for HBase workloads.</span></span> <span data-ttu-id="5e176-1462">將不再支援 3.0 版(之前可用於預覽)。</span><span class="sxs-lookup"><span data-stu-id="5e176-1462">Version 3.0 (which was available for preview) is not supported moving forward.</span></span>

## <a name="notes-about-clusters-created-prior-to-8152014"></a><span data-ttu-id="5e176-1463">2014/8/15 之前所建立之叢集的附註</span><span class="sxs-lookup"><span data-stu-id="5e176-1463">Notes about clusters created prior to 8/15/2014</span></span>
<span data-ttu-id="5e176-1464">因為 Azure PowerShell 或 HDInsight SDK 的版本與叢集版本不同，而可能遇到 Azure PowerShell 或 HDInsight SDK 錯誤訊息：「HTTP 服務存取未設定叢集 <clustername>」(或者根據作業而定，可能遇到其他錯誤訊息，例如「*無法連接到叢集*」)。</span><span class="sxs-lookup"><span data-stu-id="5e176-1464">An Azure PowerShell or HDInsight SDK error message, "Cluster <clustername> is not configured for HTTP services access" (or depending on the operation, other error messages such as: "Cannot connect to cluster") may be encountered due to a version difference between Azure PowerShell or the HDInsight SDK and a cluster.</span></span> <span data-ttu-id="5e176-1465">在 8/15 或之後建立的叢集支援佈建到虛擬網路的這項新功能。</span><span class="sxs-lookup"><span data-stu-id="5e176-1465">Clusters created on 8/15 or later have support for new provisioning capability into virtual networks.</span></span> <span data-ttu-id="5e176-1466">舊版的 Azure PowerShell 或 HDInsight SDK 無法正確解譯此功能，導致工作提交作業失敗。</span><span class="sxs-lookup"><span data-stu-id="5e176-1466">This capability isn't correctly interpreted by older versions of the Azure PowerShell or the HDInsight SDK, which results in failures of job submission operations.</span></span> <span data-ttu-id="5e176-1467">如果您使用 HDInsight SDK API 或 Azure PowerShell Cmdlet (例如 Use-AzureRmHDInsightCluster 或 Invoke-AzureRmHDInsightHiveJob) 來提交工作，這些作業可能會失敗並傳回上述其中一個錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5e176-1467">If you use HDInsight SDK APIs or Azure PowerShell cmdlets (such as Use-AzureRmHDInsightCluster or Invoke-AzureRmHDInsightHiveJob) to submit jobs, those operations may fail with one of the error messages described.</span></span>

<span data-ttu-id="5e176-1468">最新版的 HDInsight SDK 和 Azure PowerShell 中已解決這些相容性問題。</span><span class="sxs-lookup"><span data-stu-id="5e176-1468">These compatibility issues are resolved in the latest versions of the HDInsight SDK and Azure PowerShell.</span></span> <span data-ttu-id="5e176-1469">建議將 HDInsight SDK 更新到 1.3.1.6 版或更新版本，並將 Azure PowerShell 工具更新到 0.8.8 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="5e176-1469">We recommend updating the HDInsight SDK to version 1.3.1.6 or later and Azure PowerShell Tools to version 0.8.8 or later.</span></span> <span data-ttu-id="5e176-1470">您可以從 [NuGet][nuget-link] 存取最新的 HDInsight SDK。</span><span class="sxs-lookup"><span data-stu-id="5e176-1470">You can get access to the latest HDInsight SDK from [NuGet][nuget-link].</span></span> <span data-ttu-id="5e176-1471">您可以使用 [Microsoft Web Platform Installer][webpi-link] 存取 Azure PowerShell 工具。</span><span class="sxs-lookup"><span data-stu-id="5e176-1471">You can access the Azure PowerShell Tools by using [Microsoft Web Platform Installer][webpi-link].</span></span>

## <a name="notes-for-7282014-release"></a><span data-ttu-id="5e176-1472">2014/7/28 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1472">Notes for 7/28/2014 release</span></span>
* <span data-ttu-id="5e176-1473">**新區域可用 HDInsight**：我們將 HDInsight 的地理位置據點擴展到三個區域。</span><span class="sxs-lookup"><span data-stu-id="5e176-1473">**HDInsight available in new regions**:  We expanded HDInsight geographical presence to three regions.</span></span> <span data-ttu-id="5e176-1474">HDInsight 客戶可以在這三個區域建立叢集：</span><span class="sxs-lookup"><span data-stu-id="5e176-1474">HDInsight customers can create clusters in these regions:</span></span>
  * <span data-ttu-id="5e176-1475">東亞</span><span class="sxs-lookup"><span data-stu-id="5e176-1475">East Asia</span></span>
  * <span data-ttu-id="5e176-1476">美國中北部</span><span class="sxs-lookup"><span data-stu-id="5e176-1476">North Central US</span></span>
  * <span data-ttu-id="5e176-1477">美國中南部</span><span class="sxs-lookup"><span data-stu-id="5e176-1477">South Central US</span></span>
* <span data-ttu-id="5e176-1478">正在將 HDInsight 1.6 版 (HDP 1.1 和 Hadoop 1.0.3) 和 HDInsight 2.1 版 (HDP1.3 和 Hadoop 1.2) 從 Azure 入口網站移除。</span><span class="sxs-lookup"><span data-stu-id="5e176-1478">HDInsight version 1.6 (HDP 1.1 and Hadoop 1.0.3) and HDInsight version 2.1 (HDP1.3 and Hadoop 1.2) are being removed from the Azure portal.</span></span> <span data-ttu-id="5e176-1479">您可以繼續使用 Azure PowerShell Cmdlet、[New-AzureRmHDInsightCluster](http://msdn.microsoft.com/library/dn593744.aspx) 或使用 [HDInsight SDK](http://msdn.microsoft.com/library/azure/dn469975.aspx) 來建立這些版本的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e176-1479">You can continue to create Hadoop clusters for these versions by using the Azure PowerShell cmdlet, [New-AzureRmHDInsightCluster](http://msdn.microsoft.com/library/dn593744.aspx) or by using the [HDInsight SDK](http://msdn.microsoft.com/library/azure/dn469975.aspx).</span></span> <span data-ttu-id="5e176-1480">如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="5e176-1480">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="5e176-1481">此版本中的 Hortonworks Data Platform (HDP) 變更：</span><span class="sxs-lookup"><span data-stu-id="5e176-1481">Hortonworks Data Platform (HDP) changes in this release:</span></span>

<table border="1">
<tr><th><span data-ttu-id="5e176-1482">HDP</span><span class="sxs-lookup"><span data-stu-id="5e176-1482">HDP</span></span></th><th><span data-ttu-id="5e176-1483">變更</span><span class="sxs-lookup"><span data-stu-id="5e176-1483">Changes</span></span></th></tr>
<tr><td><span data-ttu-id="5e176-1484">HDP 1.3 / HDI 2.1</span><span class="sxs-lookup"><span data-stu-id="5e176-1484">HDP 1.3 / HDI 2.1</span></span></td><td><span data-ttu-id="5e176-1485">沒有變更</span><span class="sxs-lookup"><span data-stu-id="5e176-1485">No changes</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1486">HDP 2.0 / HDI 3.0</span><span class="sxs-lookup"><span data-stu-id="5e176-1486">HDP 2.0 / HDI 3.0</span></span></td><td><span data-ttu-id="5e176-1487">沒有變更</span><span class="sxs-lookup"><span data-stu-id="5e176-1487">No changes</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1488">HDP 2.1 / HDI 3.1</span><span class="sxs-lookup"><span data-stu-id="5e176-1488">HDP 2.1 / HDI 3.1</span></span></td><td><span data-ttu-id="5e176-1489">zookeeper: ['3.4.5.2.1.3.0-1948'] -> ['3.4.5.2.1.3.2-0002']</span><span class="sxs-lookup"><span data-stu-id="5e176-1489">zookeeper: ['3.4.5.2.1.3.0-1948'] -> ['3.4.5.2.1.3.2-0002']</span></span></td></tr>
</table>

## <a name="notes-for-6242014-release"></a><span data-ttu-id="5e176-1490">2014/6/24 版本的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1490">Notes for 6/24/2014 release</span></span>
<span data-ttu-id="5e176-1491">此版本包含 HDInsight 服務的增強功能：</span><span class="sxs-lookup"><span data-stu-id="5e176-1491">This release contains enhancements to the HDInsight service:</span></span>

* <span data-ttu-id="5e176-1492">**HDP 2.1 可用性**：HDInsight 3.1 (內含 HDP 2.1) 已公開上市，且為新叢集的預設版本。</span><span class="sxs-lookup"><span data-stu-id="5e176-1492">**HDP 2.1 availability**: HDInsight 3.1 (which contains HDP 2.1) is generally available and is the default version for new clusters.</span></span>
* <span data-ttu-id="5e176-1493">**HBase - Azure 入口網站改進**：我們正使 HBase 叢集可用於預覽版。</span><span class="sxs-lookup"><span data-stu-id="5e176-1493">**HBase - Azure portal improvements**: We are making HBase clusters available in Preview.</span></span> <span data-ttu-id="5e176-1494">您可以從入口網站建立 HBase 叢集，只要按幾下滑鼠即可。</span><span class="sxs-lookup"><span data-stu-id="5e176-1494">You can create HBase clusters from the portal with just a few clicks.</span></span>

<span data-ttu-id="5e176-1495">HBase 可讓您在 HDInsight 上建置各種即時工作負載，包括處理大型資料集的互動式網站，甚至是將數百萬個端點的感應器和遙測資料儲存起來的服務，都沒問題。</span><span class="sxs-lookup"><span data-stu-id="5e176-1495">With HBase, you can build a variety of real-time workloads on HDInsight, from interactive websites that work with large datasets to services storing sensor and telemetry data from millions of end points.</span></span> <span data-ttu-id="5e176-1496">下一步是使用 Hadoop 工作來分析這些工作負載中的資料，而透過 Azure PowerShell 和 Hive 叢集儀表板，就能在 HDInsight 中進行此分析。</span><span class="sxs-lookup"><span data-stu-id="5e176-1496">The next step would be to analyze the data in these workloads with Hadoop jobs, and this is possible in HDInsight through Azure PowerShell and the Hive cluster dashboard.</span></span>

### <a name="apache-mahout-preinstalled-on-hdinsight-31"></a><span data-ttu-id="5e176-1497">Apache Mahout 預先安裝在 HDInsight 3.1</span><span class="sxs-lookup"><span data-stu-id="5e176-1497">Apache Mahout preinstalled on HDInsight 3.1</span></span>
 <span data-ttu-id="5e176-1498">[Mahout](http://hortonworks.com/hadoop/mahout/) 已預先安裝在 HDInsight 3.1 Hadoop 叢集，因此您可以執行 Mahout 工作，而不需要其他叢集組態。</span><span class="sxs-lookup"><span data-stu-id="5e176-1498">[Mahout](http://hortonworks.com/hadoop/mahout/) is pre-installed on HDInsight 3.1 Hadoop clusters, so you can run Mahout jobs without the need for additional cluster configuration.</span></span> <span data-ttu-id="5e176-1499">例如，您可以使用遠端桌面通訊協定 (RDP) 從遠端進入 Hadoop 叢集，且不需要額外的步驟就能執行下列 Hello World Mahout 命令：</span><span class="sxs-lookup"><span data-stu-id="5e176-1499">For example, you can remote into a Hadoop cluster by using Remote Desktop Protocol (RDP), and without additional steps, you can run the following Hello World Mahout command:</span></span>

        mahout org.apache.mahout.classifier.df.tools.Describe -p /user/hdp/glass.data -f /user/hdp/glass.info -d I 9 N L

        mahout org.apache.mahout.classifier.df.BreimanExample -d /user/hdp/glass.data -ds /user/hdp/glass.info -i 10 -t 100

<span data-ttu-id="5e176-1500">如需此程序更完整的說明，請參閱 Apache Mahout 網站上關於 [Breiman 範例](https://mahout.apache.org/users/classification/breiman-example.html) 的文件。</span><span class="sxs-lookup"><span data-stu-id="5e176-1500">For a more complete explanation of this procedure, see the documentation for the [Breiman Example](https://mahout.apache.org/users/classification/breiman-example.html) on the Apache Mahout website.</span></span>

### <a name="hive-queries-can-use-tez-in-hdinsight-31"></a><span data-ttu-id="5e176-1501">Hive 查詢可在 HDinsight 3.1 中使用 Tez</span><span class="sxs-lookup"><span data-stu-id="5e176-1501">Hive queries can use Tez in HDInsight 3.1</span></span>
<span data-ttu-id="5e176-1502">Hive 0.13 可在 HDInsight 3.1 中使用，且能夠使用 Tez 來執行查詢，妥善運用可大幅提升效能。</span><span class="sxs-lookup"><span data-stu-id="5e176-1502">Hive 0.13 is available in HDInsight 3.1, and it is capable of running queries using Tez, which can be leveraged for substantial performance improvements.</span></span>
<span data-ttu-id="5e176-1503">依預設不會對 Hive 查詢啟用 Tez。</span><span class="sxs-lookup"><span data-stu-id="5e176-1503">Tez is not enabled by default for Hive queries.</span></span> <span data-ttu-id="5e176-1504">若要使用，您必須自行啟用。</span><span class="sxs-lookup"><span data-stu-id="5e176-1504">To use it, you must opt in.</span></span> <span data-ttu-id="5e176-1505">您可以執行下列程式碼片段來啟用 Tez：</span><span class="sxs-lookup"><span data-stu-id="5e176-1505">You can enable Tez by running the following code snippet:</span></span>

        set hive.execution.engine=tez;
        select sc_status, count(*), histogram_numeric(sc_bytes,5) from website_logs_orc_local group by sc_status;

<span data-ttu-id="5e176-1506">Hortonworks 在標準效能評比中，已發表一份關於 Hive 查詢搭配 Tez 而提升效能的詳細數據。</span><span class="sxs-lookup"><span data-stu-id="5e176-1506">Hortonworks has published a detailed breakdown of Hive query performance enhancements with Tez as delivered in standard benchmarks.</span></span> <span data-ttu-id="5e176-1507">如需詳細資訊，請參閱 [Apache Hive 13 for Enterprise Hadoop 效能評比](http://hortonworks.com/blog/benchmarking-apache-hive-13-enterprise-hadoop/)(英文)。</span><span class="sxs-lookup"><span data-stu-id="5e176-1507">For details, see [Benchmarking Apache Hive 13 for Enterprise Hadoop](http://hortonworks.com/blog/benchmarking-apache-hive-13-enterprise-hadoop/).</span></span>

<span data-ttu-id="5e176-1508">如需詳細資訊，請參閱 [Tez 上的 Hive](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez)。</span><span class="sxs-lookup"><span data-stu-id="5e176-1508">For more information, see [Hive on Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez).</span></span>

### <a name="global-availability"></a><span data-ttu-id="5e176-1509">正式上市</span><span class="sxs-lookup"><span data-stu-id="5e176-1509">Global availability</span></span>
<span data-ttu-id="5e176-1510">隨著 HDInsight 在 Hadoop 2.2 上推出，Microsoft 已在所有主要的 Azure 提供地理區提供 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="5e176-1510">With the release of HDInsight on Hadoop 2.2, Microsoft has made HDInsight available in all major geographies where Azure is available.</span></span> <span data-ttu-id="5e176-1511">尤其，西歐和東南亞資料中心已上線運作。</span><span class="sxs-lookup"><span data-stu-id="5e176-1511">Specifically, the west Europe and southeast Asia datacenters have been brought online.</span></span> <span data-ttu-id="5e176-1512">這可讓客戶將叢集配置在鄰近且可能位於相似符合性需求區域中的資料中心。</span><span class="sxs-lookup"><span data-stu-id="5e176-1512">This enables customers to locate clusters in a datacenter that is close and potentially in a zone of similar compliance requirements.</span></span>

### <a name="dos--donts-between-cluster-versions"></a><span data-ttu-id="5e176-1513">叢集版本之間的注意事項</span><span class="sxs-lookup"><span data-stu-id="5e176-1513">Dos & Don'ts between cluster versions</span></span>
<span data-ttu-id="5e176-1514">**與 HDInsight 3.1 叢集搭配使用的 Oozie 中繼存放區與舊版的 HDInsight 2.1 叢集無法回溯相容，且兩者無法與此舊版本搭配使用**。</span><span class="sxs-lookup"><span data-stu-id="5e176-1514">**Oozie metastores used with an HDInsight 3.1 cluster are not backward compatible with HDInsight 2.1 clusters, and they cannot be used with this previous version**.</span></span>

<span data-ttu-id="5e176-1515">與 HDInsight 3.1 叢集一起部署的自訂 Oozie metastore 資料庫，無法在 HDInsight 2.1 叢集上重複使用。</span><span class="sxs-lookup"><span data-stu-id="5e176-1515">A custom Oozie metastore database deployed with an HDInsight 3.1 cluster cannot be reused with an HDInsight 2.1 cluster.</span></span> <span data-ttu-id="5e176-1516">即使是源自 HDInsight 2.1 叢集的中繼存放區也是如此。</span><span class="sxs-lookup"><span data-stu-id="5e176-1516">This is the case even if the metastore originated with an HDInsight 2.1 cluster.</span></span> <span data-ttu-id="5e176-1517">不支援此案例，因為中繼存放區結構描述與 HDInsight 3.1 叢集一起使用時會升級，所以與 HDInsight 2.1 叢集所需的中繼存放區就不再相容。</span><span class="sxs-lookup"><span data-stu-id="5e176-1517">This scenario is not supported because the metastore schema gets upgraded when used with an  HDInsight 3.1 cluster, so it is no longer compatible with the metastore required by the HDInsight 2.1 clusters.</span></span> <span data-ttu-id="5e176-1518">嘗試重複使用已在 HDInsight 3.1 叢集上使用過的 Oozie 中繼存放區，將會使 HDInsight 2.1 叢集變得無法使用。</span><span class="sxs-lookup"><span data-stu-id="5e176-1518">Any attempt to reuse an Oozie metastore that has been used with an HDInsight 3.1 cluster render the HDInsight 2.1 cluster useless.</span></span>

<span data-ttu-id="5e176-1519">**叢集之間無法共用 Oozie 中繼存放區。**</span><span class="sxs-lookup"><span data-stu-id="5e176-1519">**Oozie metastores cannot be shared across clusters.**</span></span>

<span data-ttu-id="5e176-1520">Oozie 中繼存放區會連接到特定叢集，且兩者無法在叢集之間共用。</span><span class="sxs-lookup"><span data-stu-id="5e176-1520">Oozie metastores are attached to specific clusters, and they cannot be shared across clusters.</span></span>

### <a name="breaking-changes"></a><span data-ttu-id="5e176-1521">重大變更</span><span class="sxs-lookup"><span data-stu-id="5e176-1521">Breaking changes</span></span>
<span data-ttu-id="5e176-1522">**前置詞語法**：HDInsight 3.1 和 3.0 叢集僅支援 "wasb://" 語法。</span><span class="sxs-lookup"><span data-stu-id="5e176-1522">**Prefix syntax**: Only the "wasb://" syntax is supported in HDInsight 3.1 and 3.0 clusters.</span></span> <span data-ttu-id="5e176-1523">HDInsight 2.1 和 1.6 叢集支援舊的 "asv://" 語法，但在 HDInsight 3.1 或 3.0 叢集中不支援。</span><span class="sxs-lookup"><span data-stu-id="5e176-1523">The older "asv://" syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.1 or 3.0 clusters.</span></span> <span data-ttu-id="5e176-1524">這表示任何提交至 HDInsight 3.1 或 3.0 叢集且明確使用 “asv://” 語法的工作將會失敗。</span><span class="sxs-lookup"><span data-stu-id="5e176-1524">This means that any jobs submitted to an HDInsight 3.1  or 3.0 cluster that explicitly uses the "asv://" syntax will fail.</span></span> <span data-ttu-id="5e176-1525">應該改用 "wasb://" 語法。</span><span class="sxs-lookup"><span data-stu-id="5e176-1525">The "wasb://" syntax should be used instead.</span></span> <span data-ttu-id="5e176-1526">此外，如果工作提交至任何以現有中繼存放區建立的 HDInsight 3.1 或 3.0 叢集，且中繼存放區中使用 asv:// 語法來明確參考資源，則也會失敗。</span><span class="sxs-lookup"><span data-stu-id="5e176-1526">Also, jobs submitted to any HDInsight 3.1 or 3.0 clusters that are created with an existing metastore that contains explicit references to resources using the "asv://" syntax will fail.</span></span> <span data-ttu-id="5e176-1527">必須使用 "wasb://" 語法來定址資源以重新建立這些中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="5e176-1527">These metastores need to be re-created using the "wasb://" syntax to address resources.</span></span>

<span data-ttu-id="5e176-1528">**連接埠**：已變更 HDInsight 服務所使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="5e176-1528">**Ports**: The ports used by the HDInsight service have changed.</span></span> <span data-ttu-id="5e176-1529">以前所使用的連接埠號碼都在 Windows 作業系統暫時連接埠範圍內。</span><span class="sxs-lookup"><span data-stu-id="5e176-1529">The port numbers that were being used were within the ephemeral port range of the Windows operating system.</span></span> <span data-ttu-id="5e176-1530">對於短期的網際網路通訊協定通訊，會自動從預設定義的暫時範圍中配置連接埠。</span><span class="sxs-lookup"><span data-stu-id="5e176-1530">Ports are allocated automatically from a predefined ephemeral range for short-lived Internet protocol-based communications.</span></span> <span data-ttu-id="5e176-1531">新的一組允許的 Hortonworks Data Platform (HDP) 服務連接埠號碼不在此範圍內，以避免與前端節點上執行的服務所使用的連接埠發生衝突。</span><span class="sxs-lookup"><span data-stu-id="5e176-1531">The new set of allowed Hortonworks Data Platform (HDP) service port numbers are outside this range to avoid encountering conflicts that could arise with the ports used by services running on the head node.</span></span> <span data-ttu-id="5e176-1532">新的連接埠號碼應該不會引起任何重大變更。</span><span class="sxs-lookup"><span data-stu-id="5e176-1532">The new port numbers should not cause any breaking changes.</span></span> <span data-ttu-id="5e176-1533">使用的號碼如下：</span><span class="sxs-lookup"><span data-stu-id="5e176-1533">The numbers used are as follows:</span></span>

 <span data-ttu-id="5e176-1534">**HDInsight 1.6 (HDP 1.1)**</span><span class="sxs-lookup"><span data-stu-id="5e176-1534">**HDInsight 1.6 (HDP 1.1)**</span></span>

<table border="1">
<tr><th><span data-ttu-id="5e176-1535">名稱</span><span class="sxs-lookup"><span data-stu-id="5e176-1535">Name</span></span></th><th><span data-ttu-id="5e176-1536">值</span><span class="sxs-lookup"><span data-stu-id="5e176-1536">Value</span></span></th></tr>
<tr><td><span data-ttu-id="5e176-1537">dfs.http.address</span><span class="sxs-lookup"><span data-stu-id="5e176-1537">dfs.http.address</span></span></td><td><span data-ttu-id="5e176-1538">namenodehost:30070</span><span class="sxs-lookup"><span data-stu-id="5e176-1538">namenodehost:30070</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1539">dfs.datanode.address</span><span class="sxs-lookup"><span data-stu-id="5e176-1539">dfs.datanode.address</span></span></td><td><span data-ttu-id="5e176-1540">0.0.0.0:30010</span><span class="sxs-lookup"><span data-stu-id="5e176-1540">0.0.0.0:30010</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1541">dfs.datanode.http.address</span><span class="sxs-lookup"><span data-stu-id="5e176-1541">dfs.datanode.http.address</span></span></td><td><span data-ttu-id="5e176-1542">0.0.0.0:30075</span><span class="sxs-lookup"><span data-stu-id="5e176-1542">0.0.0.0:30075</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1543">dfs.datanode.ipc.address</span><span class="sxs-lookup"><span data-stu-id="5e176-1543">dfs.datanode.ipc.address</span></span></td><td><span data-ttu-id="5e176-1544">0.0.0.0:30020</span><span class="sxs-lookup"><span data-stu-id="5e176-1544">0.0.0.0:30020</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1545">dfs.secondary.http.address</span><span class="sxs-lookup"><span data-stu-id="5e176-1545">dfs.secondary.http.address</span></span></td><td><span data-ttu-id="5e176-1546">0.0.0.0:30090</span><span class="sxs-lookup"><span data-stu-id="5e176-1546">0.0.0.0:30090</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1547">mapred.job.tracker.http.address</span><span class="sxs-lookup"><span data-stu-id="5e176-1547">mapred.job.tracker.http.address</span></span></td><td><span data-ttu-id="5e176-1548">jobtrackerhost:30030</span><span class="sxs-lookup"><span data-stu-id="5e176-1548">jobtrackerhost:30030</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1549">mapred.task.tracker.http.address</span><span class="sxs-lookup"><span data-stu-id="5e176-1549">mapred.task.tracker.http.address</span></span></td><td><span data-ttu-id="5e176-1550">0.0.0.0:30060</span><span class="sxs-lookup"><span data-stu-id="5e176-1550">0.0.0.0:30060</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1551">mapreduce.history.server.http.address</span><span class="sxs-lookup"><span data-stu-id="5e176-1551">mapreduce.history.server.http.address</span></span></td><td><span data-ttu-id="5e176-1552">0.0.0.0:31111</span><span class="sxs-lookup"><span data-stu-id="5e176-1552">0.0.0.0:31111</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1553">templeton.port</span><span class="sxs-lookup"><span data-stu-id="5e176-1553">templeton.port</span></span></td><td><span data-ttu-id="5e176-1554">30111</span><span class="sxs-lookup"><span data-stu-id="5e176-1554">30111</span></span></td></tr>
</table>

 <span data-ttu-id="5e176-1555">**HDInsight 3.1 和 3.0 (HDP 2.1 和 2.0)**</span><span class="sxs-lookup"><span data-stu-id="5e176-1555">**HDInsight 3.1 and 3.0 (HDP 2.1 and 2.0)**</span></span>

<table border="1">
<tr><th><span data-ttu-id="5e176-1556">名稱</span><span class="sxs-lookup"><span data-stu-id="5e176-1556">Name</span></span></th><th><span data-ttu-id="5e176-1557">值</span><span class="sxs-lookup"><span data-stu-id="5e176-1557">Value</span></span></th></tr>
<tr><td><span data-ttu-id="5e176-1558">dfs.namenode.http-address</span><span class="sxs-lookup"><span data-stu-id="5e176-1558">dfs.namenode.http-address</span></span></td><td><span data-ttu-id="5e176-1559">namenodehost:30070</span><span class="sxs-lookup"><span data-stu-id="5e176-1559">namenodehost:30070</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1560">dfs.namenode.https-address</span><span class="sxs-lookup"><span data-stu-id="5e176-1560">dfs.namenode.https-address</span></span></td><td><span data-ttu-id="5e176-1561">headnodehost:30470</span><span class="sxs-lookup"><span data-stu-id="5e176-1561">headnodehost:30470</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1562">dfs.datanode.address</span><span class="sxs-lookup"><span data-stu-id="5e176-1562">dfs.datanode.address</span></span></td><td><span data-ttu-id="5e176-1563">0.0.0.0:30010</span><span class="sxs-lookup"><span data-stu-id="5e176-1563">0.0.0.0:30010</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1564">dfs.datanode.http.address</span><span class="sxs-lookup"><span data-stu-id="5e176-1564">dfs.datanode.http.address</span></span></td><td><span data-ttu-id="5e176-1565">0.0.0.0:30075</span><span class="sxs-lookup"><span data-stu-id="5e176-1565">0.0.0.0:30075</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1566">dfs.datanode.ipc.address</span><span class="sxs-lookup"><span data-stu-id="5e176-1566">dfs.datanode.ipc.address</span></span></td><td><span data-ttu-id="5e176-1567">0.0.0.0:30020</span><span class="sxs-lookup"><span data-stu-id="5e176-1567">0.0.0.0:30020</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1568">dfs.namenode.secondary.http-address</span><span class="sxs-lookup"><span data-stu-id="5e176-1568">dfs.namenode.secondary.http-address</span></span></td><td><span data-ttu-id="5e176-1569">0.0.0.0:30090</span><span class="sxs-lookup"><span data-stu-id="5e176-1569">0.0.0.0:30090</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1570">yarn.nodemanager.webapp.address</span><span class="sxs-lookup"><span data-stu-id="5e176-1570">yarn.nodemanager.webapp.address</span></span></td><td><span data-ttu-id="5e176-1571">0.0.0.0:30060</span><span class="sxs-lookup"><span data-stu-id="5e176-1571">0.0.0.0:30060</span></span></td></tr>
<tr><td><span data-ttu-id="5e176-1572">templeton.port</span><span class="sxs-lookup"><span data-stu-id="5e176-1572">templeton.port</span></span></td><td><span data-ttu-id="5e176-1573">30111</span><span class="sxs-lookup"><span data-stu-id="5e176-1573">30111</span></span></td></tr>
</table>

### <a name="dependencies"></a><span data-ttu-id="5e176-1574">相依項目</span><span class="sxs-lookup"><span data-stu-id="5e176-1574">Dependencies</span></span>
<span data-ttu-id="5e176-1575">HDInsight 3.x (HDP2.x) 加入下列相依項目：</span><span class="sxs-lookup"><span data-stu-id="5e176-1575">The following dependencies were added in HDInsight 3.x (HDP2.x):</span></span>

* <span data-ttu-id="5e176-1576">guice-servlet</span><span class="sxs-lookup"><span data-stu-id="5e176-1576">guice-servlet</span></span>
* <span data-ttu-id="5e176-1577">optiq-core</span><span class="sxs-lookup"><span data-stu-id="5e176-1577">optiq-core</span></span>
* <span data-ttu-id="5e176-1578">javax.inject</span><span class="sxs-lookup"><span data-stu-id="5e176-1578">javax.inject</span></span>
* <span data-ttu-id="5e176-1579">activation</span><span class="sxs-lookup"><span data-stu-id="5e176-1579">activation</span></span>
* <span data-ttu-id="5e176-1580">jsr305</span><span class="sxs-lookup"><span data-stu-id="5e176-1580">jsr305</span></span>
* <span data-ttu-id="5e176-1581">geronimo-jaspic_1.0_spec</span><span class="sxs-lookup"><span data-stu-id="5e176-1581">geronimo-jaspic_1.0_spec</span></span>
* <span data-ttu-id="5e176-1582">jul-to-slf4j</span><span class="sxs-lookup"><span data-stu-id="5e176-1582">jul-to-slf4j</span></span>
* <span data-ttu-id="5e176-1583">java-xmlbuilder</span><span class="sxs-lookup"><span data-stu-id="5e176-1583">java-xmlbuilder</span></span>
* <span data-ttu-id="5e176-1584">ant</span><span class="sxs-lookup"><span data-stu-id="5e176-1584">ant</span></span>
* <span data-ttu-id="5e176-1585">commons-compiler</span><span class="sxs-lookup"><span data-stu-id="5e176-1585">commons-compiler</span></span>
* <span data-ttu-id="5e176-1586">jdo-api</span><span class="sxs-lookup"><span data-stu-id="5e176-1586">jdo-api</span></span>
* <span data-ttu-id="5e176-1587">commons-math3</span><span class="sxs-lookup"><span data-stu-id="5e176-1587">commons-math3</span></span>
* <span data-ttu-id="5e176-1588">paranamer</span><span class="sxs-lookup"><span data-stu-id="5e176-1588">paranamer</span></span>
* <span data-ttu-id="5e176-1589">jaxb-impl</span><span class="sxs-lookup"><span data-stu-id="5e176-1589">jaxb-impl</span></span>
* <span data-ttu-id="5e176-1590">stringtemplate</span><span class="sxs-lookup"><span data-stu-id="5e176-1590">stringtemplate</span></span>
* <span data-ttu-id="5e176-1591">eigenbase-xom</span><span class="sxs-lookup"><span data-stu-id="5e176-1591">eigenbase-xom</span></span>
* <span data-ttu-id="5e176-1592">jersey-servlet</span><span class="sxs-lookup"><span data-stu-id="5e176-1592">jersey-servlet</span></span>
* <span data-ttu-id="5e176-1593">commons-exec</span><span class="sxs-lookup"><span data-stu-id="5e176-1593">commons-exec</span></span>
* <span data-ttu-id="5e176-1594">jaxb-api</span><span class="sxs-lookup"><span data-stu-id="5e176-1594">jaxb-api</span></span>
* <span data-ttu-id="5e176-1595">jetty-all-server</span><span class="sxs-lookup"><span data-stu-id="5e176-1595">jetty-all-server</span></span>
* <span data-ttu-id="5e176-1596">janino</span><span class="sxs-lookup"><span data-stu-id="5e176-1596">janino</span></span>
* <span data-ttu-id="5e176-1597">xercesImpl</span><span class="sxs-lookup"><span data-stu-id="5e176-1597">xercesImpl</span></span>
* <span data-ttu-id="5e176-1598">optiq-avatica</span><span class="sxs-lookup"><span data-stu-id="5e176-1598">optiq-avatica</span></span>
* <span data-ttu-id="5e176-1599">jta</span><span class="sxs-lookup"><span data-stu-id="5e176-1599">jta</span></span>
* <span data-ttu-id="5e176-1600">eigenbase-properties</span><span class="sxs-lookup"><span data-stu-id="5e176-1600">eigenbase-properties</span></span>
* <span data-ttu-id="5e176-1601">groovy-all</span><span class="sxs-lookup"><span data-stu-id="5e176-1601">groovy-all</span></span>
* <span data-ttu-id="5e176-1602">hamcrest-core</span><span class="sxs-lookup"><span data-stu-id="5e176-1602">hamcrest-core</span></span>
* <span data-ttu-id="5e176-1603">mail</span><span class="sxs-lookup"><span data-stu-id="5e176-1603">mail</span></span>
* <span data-ttu-id="5e176-1604">linq4j</span><span class="sxs-lookup"><span data-stu-id="5e176-1604">linq4j</span></span>
* <span data-ttu-id="5e176-1605">jpam</span><span class="sxs-lookup"><span data-stu-id="5e176-1605">jpam</span></span>
* <span data-ttu-id="5e176-1606">jersey-client</span><span class="sxs-lookup"><span data-stu-id="5e176-1606">jersey-client</span></span>
* <span data-ttu-id="5e176-1607">aopalliance</span><span class="sxs-lookup"><span data-stu-id="5e176-1607">aopalliance</span></span>
* <span data-ttu-id="5e176-1608">geronimo-annotation_1.0_spec</span><span class="sxs-lookup"><span data-stu-id="5e176-1608">geronimo-annotation_1.0_spec</span></span>
* <span data-ttu-id="5e176-1609">ant-launcher</span><span class="sxs-lookup"><span data-stu-id="5e176-1609">ant-launcher</span></span>
* <span data-ttu-id="5e176-1610">jersey-guice</span><span class="sxs-lookup"><span data-stu-id="5e176-1610">jersey-guice</span></span>
* <span data-ttu-id="5e176-1611">xml-apis</span><span class="sxs-lookup"><span data-stu-id="5e176-1611">xml-apis</span></span>
* <span data-ttu-id="5e176-1612">stax-api</span><span class="sxs-lookup"><span data-stu-id="5e176-1612">stax-api</span></span>
* <span data-ttu-id="5e176-1613">asm-commons</span><span class="sxs-lookup"><span data-stu-id="5e176-1613">asm-commons</span></span>
* <span data-ttu-id="5e176-1614">asm-tree</span><span class="sxs-lookup"><span data-stu-id="5e176-1614">asm-tree</span></span>
* <span data-ttu-id="5e176-1615">wadl</span><span class="sxs-lookup"><span data-stu-id="5e176-1615">wadl</span></span>
* <span data-ttu-id="5e176-1616">geronimo-jta_1.1_spec</span><span class="sxs-lookup"><span data-stu-id="5e176-1616">geronimo-jta_1.1_spec</span></span>
* <span data-ttu-id="5e176-1617">guice</span><span class="sxs-lookup"><span data-stu-id="5e176-1617">guice</span></span>
* <span data-ttu-id="5e176-1618">leveldbjni-all</span><span class="sxs-lookup"><span data-stu-id="5e176-1618">leveldbjni-all</span></span>
* <span data-ttu-id="5e176-1619">velocity</span><span class="sxs-lookup"><span data-stu-id="5e176-1619">velocity</span></span>
* <span data-ttu-id="5e176-1620">jettison</span><span class="sxs-lookup"><span data-stu-id="5e176-1620">jettison</span></span>
* <span data-ttu-id="5e176-1621">snappy-java</span><span class="sxs-lookup"><span data-stu-id="5e176-1621">snappy-java</span></span>
* <span data-ttu-id="5e176-1622">jetty-all</span><span class="sxs-lookup"><span data-stu-id="5e176-1622">jetty-all</span></span>
* <span data-ttu-id="5e176-1623">commons-dbcp</span><span class="sxs-lookup"><span data-stu-id="5e176-1623">commons-dbcp</span></span>

<span data-ttu-id="5e176-1624">HDInsight 3.x (HDP2.x) 中已不存在下列相依項目：</span><span class="sxs-lookup"><span data-stu-id="5e176-1624">The following dependencies no longer exist in HDInsight 3.x (HDP2.x):</span></span>

* <span data-ttu-id="5e176-1625">jdeb</span><span class="sxs-lookup"><span data-stu-id="5e176-1625">jdeb</span></span>
* <span data-ttu-id="5e176-1626">kfs</span><span class="sxs-lookup"><span data-stu-id="5e176-1626">kfs</span></span>
* <span data-ttu-id="5e176-1627">sqlline</span><span class="sxs-lookup"><span data-stu-id="5e176-1627">sqlline</span></span>
* <span data-ttu-id="5e176-1628">ivy</span><span class="sxs-lookup"><span data-stu-id="5e176-1628">ivy</span></span>
* <span data-ttu-id="5e176-1629">aspectjrt</span><span class="sxs-lookup"><span data-stu-id="5e176-1629">aspectjrt</span></span>
* <span data-ttu-id="5e176-1630">json</span><span class="sxs-lookup"><span data-stu-id="5e176-1630">json</span></span>
* <span data-ttu-id="5e176-1631">core</span><span class="sxs-lookup"><span data-stu-id="5e176-1631">core</span></span>
* <span data-ttu-id="5e176-1632">jdo2-api</span><span class="sxs-lookup"><span data-stu-id="5e176-1632">jdo2-api</span></span>
* <span data-ttu-id="5e176-1633">avro-mapred</span><span class="sxs-lookup"><span data-stu-id="5e176-1633">avro-mapred</span></span>
* <span data-ttu-id="5e176-1634">datanucleus-enhancer</span><span class="sxs-lookup"><span data-stu-id="5e176-1634">datanucleus-enhancer</span></span>
* <span data-ttu-id="5e176-1635">jsp</span><span class="sxs-lookup"><span data-stu-id="5e176-1635">jsp</span></span>
* <span data-ttu-id="5e176-1636">commons-logging-api</span><span class="sxs-lookup"><span data-stu-id="5e176-1636">commons-logging-api</span></span>
* <span data-ttu-id="5e176-1637">commons-math</span><span class="sxs-lookup"><span data-stu-id="5e176-1637">commons-math</span></span>
* <span data-ttu-id="5e176-1638">JavaEWAH</span><span class="sxs-lookup"><span data-stu-id="5e176-1638">JavaEWAH</span></span>
* <span data-ttu-id="5e176-1639">aspectjtools</span><span class="sxs-lookup"><span data-stu-id="5e176-1639">aspectjtools</span></span>
* <span data-ttu-id="5e176-1640">javolution</span><span class="sxs-lookup"><span data-stu-id="5e176-1640">javolution</span></span>
* <span data-ttu-id="5e176-1641">hdfsproxy</span><span class="sxs-lookup"><span data-stu-id="5e176-1641">hdfsproxy</span></span>
* <span data-ttu-id="5e176-1642">hbase</span><span class="sxs-lookup"><span data-stu-id="5e176-1642">hbase</span></span>
* <span data-ttu-id="5e176-1643">snappy</span><span class="sxs-lookup"><span data-stu-id="5e176-1643">snappy</span></span>

### <a name="version-changes"></a><span data-ttu-id="5e176-1644">版本變更</span><span class="sxs-lookup"><span data-stu-id="5e176-1644">Version changes</span></span>
<span data-ttu-id="5e176-1645">HDInsight 2.x (HDP1.x) 與 HDInsight 3.x (HDP2.x) 之間有下列版本變更：</span><span class="sxs-lookup"><span data-stu-id="5e176-1645">The following version changes were made between HDInsight 2.x (HDP1.x) and HDInsight 3.x (HDP2.x):</span></span>

* <span data-ttu-id="5e176-1646">metrics-core: ['2.1.2'] -> ['3.0.0']</span><span class="sxs-lookup"><span data-stu-id="5e176-1646">metrics-core: ['2.1.2'] -> ['3.0.0']</span></span>
* <span data-ttu-id="5e176-1647">derbynet: ['10.4.2.0'] -> ['10.10.1.1']</span><span class="sxs-lookup"><span data-stu-id="5e176-1647">derbynet: ['10.4.2.0'] -> ['10.10.1.1']</span></span>
* <span data-ttu-id="5e176-1648">datanucleus: ['rdbms-3.0.8'] -> ['rdbms-3.2.9']</span><span class="sxs-lookup"><span data-stu-id="5e176-1648">datanucleus: ['rdbms-3.0.8'] -> ['rdbms-3.2.9']</span></span>
* <span data-ttu-id="5e176-1649">jasper-compiler: ['5.5.12'] -> ['5.5.23']</span><span class="sxs-lookup"><span data-stu-id="5e176-1649">jasper-compiler: ['5.5.12'] -> ['5.5.23']</span></span>
* <span data-ttu-id="5e176-1650">log4j: ['1.2.15', '1.2.16'] -> ['1.2.16', '1.2.17']</span><span class="sxs-lookup"><span data-stu-id="5e176-1650">log4j: ['1.2.15', '1.2.16'] -> ['1.2.16', '1.2.17']</span></span>
* <span data-ttu-id="5e176-1651">derbyclient: ['10.4.2.0'] -> ['10.10.1.1']</span><span class="sxs-lookup"><span data-stu-id="5e176-1651">derbyclient: ['10.4.2.0'] -> ['10.10.1.1']</span></span>
* <span data-ttu-id="5e176-1652">httpcore: ['4.2.4'] -> ['4.2.5']</span><span class="sxs-lookup"><span data-stu-id="5e176-1652">httpcore: ['4.2.4'] -> ['4.2.5']</span></span>
* <span data-ttu-id="5e176-1653">hsqldb: ['1.8.0.10'] -> ['2.0.0']</span><span class="sxs-lookup"><span data-stu-id="5e176-1653">hsqldb: ['1.8.0.10'] -> ['2.0.0']</span></span>
* <span data-ttu-id="5e176-1654">jets3t: ['0.6.1'] -> ['0.9.0']</span><span class="sxs-lookup"><span data-stu-id="5e176-1654">jets3t: ['0.6.1'] -> ['0.9.0']</span></span>
* <span data-ttu-id="5e176-1655">protobuf-java: ['2.4.1'] -> ['2.5.0']</span><span class="sxs-lookup"><span data-stu-id="5e176-1655">protobuf-java: ['2.4.1'] -> ['2.5.0']</span></span>
* <span data-ttu-id="5e176-1656">derby: ['10.4.2.0'] -> ['10.10.1.1']</span><span class="sxs-lookup"><span data-stu-id="5e176-1656">derby: ['10.4.2.0'] -> ['10.10.1.1']</span></span>
* <span data-ttu-id="5e176-1657">jasper: ['runtime-5.5.12'] -> ['runtime-5.5.23']</span><span class="sxs-lookup"><span data-stu-id="5e176-1657">jasper: ['runtime-5.5.12'] -> ['runtime-5.5.23']</span></span>
* <span data-ttu-id="5e176-1658">commons-daemon: ['1.0.1'] -> ['1.0.13']</span><span class="sxs-lookup"><span data-stu-id="5e176-1658">commons-daemon: ['1.0.1'] -> ['1.0.13']</span></span>
* <span data-ttu-id="5e176-1659">datanucleus-core: ['3.0.9'] -> ['3.2.10']</span><span class="sxs-lookup"><span data-stu-id="5e176-1659">datanucleus-core: ['3.0.9'] -> ['3.2.10']</span></span>
* <span data-ttu-id="5e176-1660">datanucleus-api-jdo: ['3.0.7'] -> ['3.2.6']</span><span class="sxs-lookup"><span data-stu-id="5e176-1660">datanucleus-api-jdo: ['3.0.7'] -> ['3.2.6']</span></span>
* <span data-ttu-id="5e176-1661">zookeeper: ['3.4.5.1.3.9.0-01320'] -> ['3.4.5.2.1.3.0-1948']</span><span class="sxs-lookup"><span data-stu-id="5e176-1661">zookeeper: ['3.4.5.1.3.9.0-01320'] -> ['3.4.5.2.1.3.0-1948']</span></span>
* <span data-ttu-id="5e176-1662">bonecp: ['0.7.1.RELEASE'] -> ['</span><span class="sxs-lookup"><span data-stu-id="5e176-1662">bonecp: ['0.7.1.RELEASE'] -> ['</span></span>
* <span data-ttu-id="5e176-1663">0.8.0.RELEASE']</span><span class="sxs-lookup"><span data-stu-id="5e176-1663">0.8.0.RELEASE']</span></span>

### <a name="drivers"></a><span data-ttu-id="5e176-1664">驅動程式</span><span class="sxs-lookup"><span data-stu-id="5e176-1664">Drivers</span></span>
<span data-ttu-id="5e176-1665">SQL Server 的 Java 資料庫連接 (JDBC) 驅動程式僅供 HDInsight 內部使用，且不適用於外部作業。</span><span class="sxs-lookup"><span data-stu-id="5e176-1665">The Java Database Connectivity (JDBC) driver for SQL Server is used internally by HDInsight and is not used for external operations.</span></span> <span data-ttu-id="5e176-1666">如果您想要使用開放式資料庫連接 (ODBC) 連線至 HDInsight，請使用 Microsoft Hive ODBC 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="5e176-1666">If you want to connect to HDInsight by using Open Database Connectivity (ODBC), please use the Microsoft Hive ODBC driver.</span></span> <span data-ttu-id="5e176-1667">如需詳細資訊，請參閱 [使用 Microsoft Hive ODBC 驅動程式將 Excel 連接到 HDInsight](hdinsight-connect-excel-hive-odbc-driver.md)。</span><span class="sxs-lookup"><span data-stu-id="5e176-1667">For more information, see [Connect Excel to HDInsight with the Microsoft Hive ODBC Driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="5e176-1668">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="5e176-1668">Bug fixes</span></span>
<span data-ttu-id="5e176-1669">在此版本中，我們使用幾個 Bug 修正來重新整理下列 HDInsight 版本：</span><span class="sxs-lookup"><span data-stu-id="5e176-1669">With this release, we have refreshed the following HDInsight versions with several bug fixes:</span></span>

* <span data-ttu-id="5e176-1670">HDInsight 2.1 (HDP 1.3)</span><span class="sxs-lookup"><span data-stu-id="5e176-1670">HDInsight 2.1 (HDP 1.3)</span></span>
* <span data-ttu-id="5e176-1671">HDInsight 3.0 (HDP 2.0)</span><span class="sxs-lookup"><span data-stu-id="5e176-1671">HDInsight 3.0 (HDP 2.0)</span></span>
* <span data-ttu-id="5e176-1672">HDInsight 3.1 (HDP 2.1)</span><span class="sxs-lookup"><span data-stu-id="5e176-1672">HDInsight 3.1 (HDP 2.1)</span></span>

## <a name="hortonworks-release-notes"></a><span data-ttu-id="5e176-1673">Hortonworks 版本資訊</span><span class="sxs-lookup"><span data-stu-id="5e176-1673">Hortonworks release notes</span></span>
<span data-ttu-id="5e176-1674">下列位置提供 HDInsight 版本叢集使用的 Hortonworks Data Platform (HDP) 的版本資訊：</span><span class="sxs-lookup"><span data-stu-id="5e176-1674">Release notes for the Hortonworks Data Platforms (HDPs) that are used by HDInsight version clusters are available at the following locations:</span></span>

* <span data-ttu-id="5e176-1675">HDInsight 3.1 版採用以 [Hortonworks Data Platform 2.1.7][hdp-2-1-7] 為基礎的 Hadoop 散發。</span><span class="sxs-lookup"><span data-stu-id="5e176-1675">HDInsight version 3.1 uses a Hadoop distribution that is based on the [Hortonworks Data Platform 2.1.7][hdp-2-1-7].</span></span> <span data-ttu-id="5e176-1676">這是在 2014/11/7 之後使用 Azure 入口網站時所建立的預設 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e176-1676">This is the default Hadoop cluster created when using the Azure portal after 11/7/2014.</span></span> <span data-ttu-id="5e176-1677">在 2014/11/7 之前建立的 HDInsight 3.1 叢集是以 [Hortonworks Data Platform 2.1.1][hdp-2-1-1] 為基礎。</span><span class="sxs-lookup"><span data-stu-id="5e176-1677">HDInsight 3.1 clusters created before 11/7/2014 were based on the [Hortonworks Data Platform 2.1.1][hdp-2-1-1]</span></span>
* <span data-ttu-id="5e176-1678">HDInsight 3.0 版採用以 [Hortonworks Data Platform 2.0][hdp-2-0-8] 為基礎的 Hadoop 散發。</span><span class="sxs-lookup"><span data-stu-id="5e176-1678">HDInsight version 3.0 uses a Hadoop distribution that is based on the [Hortonworks Data Platform 2.0][hdp-2-0-8].</span></span>
* <span data-ttu-id="5e176-1679">HDInsight 2.1 版採用以 [Hortonworks Data Platform 1.3][hdp-1-3-0] 為基礎的 Hadoop 散發。</span><span class="sxs-lookup"><span data-stu-id="5e176-1679">HDInsight version 2.1 uses a Hadoop distribution that is based on the [Hortonworks Data Platform 1.3][hdp-1-3-0].</span></span>
* <span data-ttu-id="5e176-1680">HDInsight 1.6 版採用以 [Hortonworks Data Platform 1.1][hdp-1-1-0] 為基礎的 Hadoop 散發。</span><span class="sxs-lookup"><span data-stu-id="5e176-1680">HDInsight version 1.6 uses a Hadoop distribution that is based on the [Hortonworks Data Platform 1.1][hdp-1-1-0].</span></span>

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[nuget-link]: https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.HDInsight/

[webpi-link]: http://go.microsoft.com/?linkid=9811175&clcid=0x409

[hdinsight-install-spark]: ../hdinsight-hadoop-spark-install/
[hdinsight-r-scripts]: ../hdinsight-hadoop-r-scripts/

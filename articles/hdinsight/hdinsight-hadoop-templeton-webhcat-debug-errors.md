---
title: "了解並解決 HDInsight 上的 WebHCat 錯誤 - Azure | Microsoft Docs"
description: "了解 WebHCat 在 HDInsight 上傳回的常見錯誤以及如何解決這些問題。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 6d8162e0d64ec9fc42690392b7c822593c0c2767
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="41afa-103">了解並解決 HDInsight 上從 WebHCat 收到的錯誤</span><span class="sxs-lookup"><span data-stu-id="41afa-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="41afa-104">了解搭配 HDInsight 使用 WebHCat 時遇到的錯誤，以及如何解決它們。</span><span class="sxs-lookup"><span data-stu-id="41afa-104">Learn about errors received when using WebHCat with HDInsight, and how to resolve them.</span></span> <span data-ttu-id="41afa-105">WebHCat 是由用戶端工具 (例如 Azure PowerShell 與 Data Lake Tools for Visual Studio) 在內部使用。</span><span class="sxs-lookup"><span data-stu-id="41afa-105">WebHCat is used internally by client-side tools such as Azure PowerShell and the Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="41afa-106">什麼是 WebHCat？</span><span class="sxs-lookup"><span data-stu-id="41afa-106">What is WebHCat</span></span>

<span data-ttu-id="41afa-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) 是適用於 [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog) 的 REST API，這是 Hadoop 的資料表和儲存體管理層。</span><span class="sxs-lookup"><span data-stu-id="41afa-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="41afa-108">WebHCat 預設會在 HDInsight 叢集上啟用，並由各種工具用來提交工作、取得工作狀態等，而不需登入叢集。</span><span class="sxs-lookup"><span data-stu-id="41afa-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools to submit jobs, get job status, etc. without logging in to the cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="41afa-109">修改組態</span><span class="sxs-lookup"><span data-stu-id="41afa-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41afa-110">因為已超過設定的上限，而發生本文件中所列的幾個錯誤。</span><span class="sxs-lookup"><span data-stu-id="41afa-110">Several of the errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="41afa-111">當解決步驟提到您可以變更值時，您必須使用下列其中一項來執行變更：</span><span class="sxs-lookup"><span data-stu-id="41afa-111">When the resolution step mentions that you can change a value, you must use one of the following to perform the change:</span></span>

* <span data-ttu-id="41afa-112">針對 **Windows** 叢集：使用指令碼動作在叢集建立期間設定此值。</span><span class="sxs-lookup"><span data-stu-id="41afa-112">For **Windows** clusters: Use a script action to configure the value during cluster creation.</span></span> <span data-ttu-id="41afa-113">如需詳細資訊，請參閱 [開發指令碼動作](hdinsight-hadoop-script-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="41afa-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="41afa-114">針對 **Linux** 叢集：使用 Ambari (Web 或 REST API) 來修改此值。</span><span class="sxs-lookup"><span data-stu-id="41afa-114">For **Linux** clusters: Use Ambari (web or REST API) to modify the value.</span></span> <span data-ttu-id="41afa-115">如需詳細資訊，請參閱 [使用 Ambari 管理 HDInsight](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="41afa-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41afa-116">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="41afa-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="41afa-117">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="41afa-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="41afa-118">預設組態</span><span class="sxs-lookup"><span data-stu-id="41afa-118">Default configuration</span></span>

<span data-ttu-id="41afa-119">如果超過下列預設值，可能會使得 WebHCat 效能變差或導致發生錯誤：</span><span class="sxs-lookup"><span data-stu-id="41afa-119">If the following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="41afa-120">設定</span><span class="sxs-lookup"><span data-stu-id="41afa-120">Setting</span></span> | <span data-ttu-id="41afa-121">作用</span><span class="sxs-lookup"><span data-stu-id="41afa-121">What it does</span></span> | <span data-ttu-id="41afa-122">預設值</span><span class="sxs-lookup"><span data-stu-id="41afa-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="41afa-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="41afa-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="41afa-124">可以同時為作用中 (擱置或執行中) 的工作數目上限</span><span class="sxs-lookup"><span data-stu-id="41afa-124">The maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="41afa-125">10,000</span><span class="sxs-lookup"><span data-stu-id="41afa-125">10,000</span></span> |
| <span data-ttu-id="41afa-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="41afa-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="41afa-127">可以同時提供服務的要求數目上限</span><span class="sxs-lookup"><span data-stu-id="41afa-127">The maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="41afa-128">20</span><span class="sxs-lookup"><span data-stu-id="41afa-128">20</span></span> |
| <span data-ttu-id="41afa-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="41afa-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="41afa-130">將保留作業歷程記錄的天數</span><span class="sxs-lookup"><span data-stu-id="41afa-130">The number of days that job history are retained</span></span> |<span data-ttu-id="41afa-131">7 天</span><span class="sxs-lookup"><span data-stu-id="41afa-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="41afa-132">要求太多</span><span class="sxs-lookup"><span data-stu-id="41afa-132">Too many requests</span></span>

<span data-ttu-id="41afa-133">**HTTP 狀態碼**：429</span><span class="sxs-lookup"><span data-stu-id="41afa-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="41afa-134">原因</span><span class="sxs-lookup"><span data-stu-id="41afa-134">Cause</span></span> | <span data-ttu-id="41afa-135">解決方案</span><span class="sxs-lookup"><span data-stu-id="41afa-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="41afa-136">您已超出 WebHCat 每分鐘提供服務的並行要求上限 (預設值為 20)</span><span class="sxs-lookup"><span data-stu-id="41afa-136">You have exceeded the maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="41afa-137">減少您的工作負載以確保不會提交超過並行要求數目上限，或藉由修改 `templeton.exec.max-procs`來提高並行要求限制。</span><span class="sxs-lookup"><span data-stu-id="41afa-137">Reduce your workload to ensure that you do not submit more than the maximum number of concurrent requests or increase the concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="41afa-138">如需詳細資訊，請參閱[修改組態](#modifying-configuration) 。</span><span class="sxs-lookup"><span data-stu-id="41afa-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="41afa-139">無法使用伺服器</span><span class="sxs-lookup"><span data-stu-id="41afa-139">Server unavailable</span></span>

<span data-ttu-id="41afa-140">**HTTP 狀態碼**：503</span><span class="sxs-lookup"><span data-stu-id="41afa-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="41afa-141">原因</span><span class="sxs-lookup"><span data-stu-id="41afa-141">Cause</span></span> | <span data-ttu-id="41afa-142">解決方案</span><span class="sxs-lookup"><span data-stu-id="41afa-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="41afa-143">此狀態碼通常發生於叢集的主要和次要 HeadNode 間的容錯移轉期間</span><span class="sxs-lookup"><span data-stu-id="41afa-143">This status code usually occurs during failover between the primary and secondary HeadNode for the cluster</span></span> |<span data-ttu-id="41afa-144">等候兩分鐘，然後重試作業</span><span class="sxs-lookup"><span data-stu-id="41afa-144">Wait two minutes, then retry the operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="41afa-145">不正確的要求內容：找不到工作</span><span class="sxs-lookup"><span data-stu-id="41afa-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="41afa-146">**HTTP 狀態碼**：400</span><span class="sxs-lookup"><span data-stu-id="41afa-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="41afa-147">原因</span><span class="sxs-lookup"><span data-stu-id="41afa-147">Cause</span></span> | <span data-ttu-id="41afa-148">解決方案</span><span class="sxs-lookup"><span data-stu-id="41afa-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="41afa-149">工作歷程記錄清除器已清除工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="41afa-149">Job details have been cleaned up by the job history cleaner</span></span> |<span data-ttu-id="41afa-150">工作歷程記錄的預設保留期間為 7 天。</span><span class="sxs-lookup"><span data-stu-id="41afa-150">The default retention period for job history is 7 days.</span></span> <span data-ttu-id="41afa-151">您可以透過修改 `mapreduce.jobhistory.max-age-ms` 來變更預設保留期間。</span><span class="sxs-lookup"><span data-stu-id="41afa-151">The default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="41afa-152">如需詳細資訊，請參閱[修改組態](#modifying-configuration) 。</span><span class="sxs-lookup"><span data-stu-id="41afa-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="41afa-153">工作因為容錯移轉而遭到刪除</span><span class="sxs-lookup"><span data-stu-id="41afa-153">Job has been killed due to a failover</span></span> |<span data-ttu-id="41afa-154">最多重試工作提交兩分鐘</span><span class="sxs-lookup"><span data-stu-id="41afa-154">Retry job submission for up to two minutes</span></span> |
| <span data-ttu-id="41afa-155">使用的工作識別碼無效</span><span class="sxs-lookup"><span data-stu-id="41afa-155">An Invalid job id was used</span></span> |<span data-ttu-id="41afa-156">檢查工作識別碼是否正確</span><span class="sxs-lookup"><span data-stu-id="41afa-156">Check if the job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="41afa-157">閘道不正確</span><span class="sxs-lookup"><span data-stu-id="41afa-157">Bad gateway</span></span>

<span data-ttu-id="41afa-158">**HTTP 狀態碼**：502</span><span class="sxs-lookup"><span data-stu-id="41afa-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="41afa-159">原因</span><span class="sxs-lookup"><span data-stu-id="41afa-159">Cause</span></span> | <span data-ttu-id="41afa-160">解決方案</span><span class="sxs-lookup"><span data-stu-id="41afa-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="41afa-161">內部記憶體回收會發生於 WebHCat 程序中</span><span class="sxs-lookup"><span data-stu-id="41afa-161">Internal garbage collection is occurring within the WebHCat process</span></span> |<span data-ttu-id="41afa-162">等候記憶體回收完成，或重新啟動 WebHCat 服務</span><span class="sxs-lookup"><span data-stu-id="41afa-162">Wait for garbage collection to finish or restart the WebHCat service</span></span> |
| <span data-ttu-id="41afa-163">等候 ResourceManager 服務回應時逾時。</span><span class="sxs-lookup"><span data-stu-id="41afa-163">Time out waiting on a response from the ResourceManager service.</span></span> <span data-ttu-id="41afa-164">此錯誤發生於作用中應用程式的數目達到設定的最大值時 (預設值為 10,000)</span><span class="sxs-lookup"><span data-stu-id="41afa-164">This error can occur when the number of active applications goes the configured maximum (default 10,000)</span></span> |<span data-ttu-id="41afa-165">等候目前執行中的工作完成，或修改 `yarn.scheduler.capacity.maximum-applications`以提高並行工作限制。</span><span class="sxs-lookup"><span data-stu-id="41afa-165">Wait for currently running jobs to complete or increase the concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="41afa-166">如需詳細資訊，請參閱[修改組態](#modifying-configuration)一節。</span><span class="sxs-lookup"><span data-stu-id="41afa-166">For more information, see the [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="41afa-167">嘗試在 `Fields` 設定為 `*` 時透過 [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) 呼叫擷取所有作業</span><span class="sxs-lookup"><span data-stu-id="41afa-167">Attempting to retrieve all jobs through the [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set to `*`</span></span> |<span data-ttu-id="41afa-168">不要擷取*所有*作業詳細資料。</span><span class="sxs-lookup"><span data-stu-id="41afa-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="41afa-169">請改為使用 `jobid` 只擷取大於特定作業識別碼的作業詳細資料。</span><span class="sxs-lookup"><span data-stu-id="41afa-169">Instead use `jobid` to retrieve details for jobs only greater than certain job id.</span></span> <span data-ttu-id="41afa-170">或者，不要使用 `Fields`</span><span class="sxs-lookup"><span data-stu-id="41afa-170">Or, do not use `Fields`</span></span> |
| <span data-ttu-id="41afa-171">WebHCat 服務在 HeadNode 容錯移轉期間關閉</span><span class="sxs-lookup"><span data-stu-id="41afa-171">The WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="41afa-172">等候兩分鐘，然後重試作業</span><span class="sxs-lookup"><span data-stu-id="41afa-172">Wait for two minutes and retry the operation</span></span> |
| <span data-ttu-id="41afa-173">有 500 個以上透過 WebHCat 提交的擱置工作</span><span class="sxs-lookup"><span data-stu-id="41afa-173">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="41afa-174">等到目前擱置的工作完成，再送出更多工作</span><span class="sxs-lookup"><span data-stu-id="41afa-174">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml

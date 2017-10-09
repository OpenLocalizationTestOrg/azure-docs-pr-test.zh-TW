---
title: "HDInsight 的 Azure 上的 aaaUnderstand 並解決 WebHCat 錯誤 |Microsoft 文件"
description: "了解如何在 HDInsight 上 WebHCat 傳回 tooabout 常見錯誤以及如何 tooresolve 它們。"
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
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="80e38-103">了解並解決 HDInsight 上從 WebHCat 收到的錯誤</span><span class="sxs-lookup"><span data-stu-id="80e38-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="80e38-104">了解使用 HDInsight WebHCat 何時及如何所收到的錯誤 tooresolve 它們。</span><span class="sxs-lookup"><span data-stu-id="80e38-104">Learn about errors received when using WebHCat with HDInsight, and how tooresolve them.</span></span> <span data-ttu-id="80e38-105">WebHCat 為內部使用的用戶端工具，例如 Azure PowerShell 和 hello Data Lake Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="80e38-105">WebHCat is used internally by client-side tools such as Azure PowerShell and hello Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="80e38-106">什麼是 WebHCat？</span><span class="sxs-lookup"><span data-stu-id="80e38-106">What is WebHCat</span></span>

<span data-ttu-id="80e38-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) 是適用於 [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog) 的 REST API，這是 Hadoop 的資料表和儲存體管理層。</span><span class="sxs-lookup"><span data-stu-id="80e38-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="80e38-108">WebHCat HDInsight 叢集上的預設會啟用和使用各種工具 toosubmit 工作，而不記錄 toohello 叢集中取得作業狀態等。</span><span class="sxs-lookup"><span data-stu-id="80e38-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools toosubmit jobs, get job status, etc. without logging in toohello cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="80e38-109">修改組態</span><span class="sxs-lookup"><span data-stu-id="80e38-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80e38-110">有幾個這份文件中所列的 hello 錯誤發生的原因已超過設定的上限。</span><span class="sxs-lookup"><span data-stu-id="80e38-110">Several of hello errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="80e38-111">當 hello 解決步驟提及您可以變更值時，您必須使用其中一個 hello tooperform hello 變更之後：</span><span class="sxs-lookup"><span data-stu-id="80e38-111">When hello resolution step mentions that you can change a value, you must use one of hello following tooperform hello change:</span></span>

* <span data-ttu-id="80e38-112">如**Windows**叢集： 在叢集建立期間使用指令碼動作 tooconfigure hello 值。</span><span class="sxs-lookup"><span data-stu-id="80e38-112">For **Windows** clusters: Use a script action tooconfigure hello value during cluster creation.</span></span> <span data-ttu-id="80e38-113">如需詳細資訊，請參閱 [開發指令碼動作](hdinsight-hadoop-script-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="80e38-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="80e38-114">如**Linux**叢集： 使用 Ambari （web 或 REST API） toomodify hello 值。</span><span class="sxs-lookup"><span data-stu-id="80e38-114">For **Linux** clusters: Use Ambari (web or REST API) toomodify hello value.</span></span> <span data-ttu-id="80e38-115">如需詳細資訊，請參閱 [使用 Ambari 管理 HDInsight](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="80e38-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80e38-116">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="80e38-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="80e38-117">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="80e38-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="80e38-118">預設組態</span><span class="sxs-lookup"><span data-stu-id="80e38-118">Default configuration</span></span>

<span data-ttu-id="80e38-119">如果超過 hello 下列預設值，它可以降低 WebHCat 效能，或造成錯誤：</span><span class="sxs-lookup"><span data-stu-id="80e38-119">If hello following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="80e38-120">設定</span><span class="sxs-lookup"><span data-stu-id="80e38-120">Setting</span></span> | <span data-ttu-id="80e38-121">作用</span><span class="sxs-lookup"><span data-stu-id="80e38-121">What it does</span></span> | <span data-ttu-id="80e38-122">預設值</span><span class="sxs-lookup"><span data-stu-id="80e38-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="80e38-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="80e38-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="80e38-124">hello 可以同時為作用中的作業數目上限 （暫止或執行）</span><span class="sxs-lookup"><span data-stu-id="80e38-124">hello maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="80e38-125">10,000</span><span class="sxs-lookup"><span data-stu-id="80e38-125">10,000</span></span> |
| <span data-ttu-id="80e38-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="80e38-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="80e38-127">hello 可以同時處理要求的數目上限</span><span class="sxs-lookup"><span data-stu-id="80e38-127">hello maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="80e38-128">20</span><span class="sxs-lookup"><span data-stu-id="80e38-128">20</span></span> |
| <span data-ttu-id="80e38-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="80e38-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="80e38-130">hello 的作業歷程記錄會保留天數</span><span class="sxs-lookup"><span data-stu-id="80e38-130">hello number of days that job history are retained</span></span> |<span data-ttu-id="80e38-131">7 天</span><span class="sxs-lookup"><span data-stu-id="80e38-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="80e38-132">要求太多</span><span class="sxs-lookup"><span data-stu-id="80e38-132">Too many requests</span></span>

<span data-ttu-id="80e38-133">**HTTP 狀態碼**：429</span><span class="sxs-lookup"><span data-stu-id="80e38-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="80e38-134">原因</span><span class="sxs-lookup"><span data-stu-id="80e38-134">Cause</span></span> | <span data-ttu-id="80e38-135">解決方案</span><span class="sxs-lookup"><span data-stu-id="80e38-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="80e38-136">您已超過 hello 最大並行要求由 WebHCat 每分鐘 （預設值 20）</span><span class="sxs-lookup"><span data-stu-id="80e38-136">You have exceeded hello maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="80e38-137">減少您不要未送出多個 hello 的並行要求數目上限或藉由修改提高 hello 並行要求限制您的工作負載 tooensure `templeton.exec.max-procs`。</span><span class="sxs-lookup"><span data-stu-id="80e38-137">Reduce your workload tooensure that you do not submit more than hello maximum number of concurrent requests or increase hello concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="80e38-138">如需詳細資訊，請參閱[修改組態](#modifying-configuration) 。</span><span class="sxs-lookup"><span data-stu-id="80e38-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="80e38-139">無法使用伺服器</span><span class="sxs-lookup"><span data-stu-id="80e38-139">Server unavailable</span></span>

<span data-ttu-id="80e38-140">**HTTP 狀態碼**：503</span><span class="sxs-lookup"><span data-stu-id="80e38-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="80e38-141">原因</span><span class="sxs-lookup"><span data-stu-id="80e38-141">Cause</span></span> | <span data-ttu-id="80e38-142">解決方案</span><span class="sxs-lookup"><span data-stu-id="80e38-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="80e38-143">此狀態碼，通常會發生在 hello 主要與次要資料庫之間的容錯移轉期間 hello 叢集前端節點</span><span class="sxs-lookup"><span data-stu-id="80e38-143">This status code usually occurs during failover between hello primary and secondary HeadNode for hello cluster</span></span> |<span data-ttu-id="80e38-144">等待兩分鐘，然後重試 hello 作業</span><span class="sxs-lookup"><span data-stu-id="80e38-144">Wait two minutes, then retry hello operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="80e38-145">不正確的要求內容：找不到工作</span><span class="sxs-lookup"><span data-stu-id="80e38-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="80e38-146">**HTTP 狀態碼**：400</span><span class="sxs-lookup"><span data-stu-id="80e38-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="80e38-147">原因</span><span class="sxs-lookup"><span data-stu-id="80e38-147">Cause</span></span> | <span data-ttu-id="80e38-148">解決方案</span><span class="sxs-lookup"><span data-stu-id="80e38-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="80e38-149">工作詳細資料已遭清除 hello 作業歷程記錄的清除器</span><span class="sxs-lookup"><span data-stu-id="80e38-149">Job details have been cleaned up by hello job history cleaner</span></span> |<span data-ttu-id="80e38-150">作業記錄的 hello 預設保留期限為 7 天。</span><span class="sxs-lookup"><span data-stu-id="80e38-150">hello default retention period for job history is 7 days.</span></span> <span data-ttu-id="80e38-151">要變更 hello 預設保留期限，請修改`mapreduce.jobhistory.max-age-ms`。</span><span class="sxs-lookup"><span data-stu-id="80e38-151">hello default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="80e38-152">如需詳細資訊，請參閱[修改組態](#modifying-configuration) 。</span><span class="sxs-lookup"><span data-stu-id="80e38-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="80e38-153">作業已經刪除到期 tooa 容錯移轉</span><span class="sxs-lookup"><span data-stu-id="80e38-153">Job has been killed due tooa failover</span></span> |<span data-ttu-id="80e38-154">重試作業提交向上 tootwo 分鐘</span><span class="sxs-lookup"><span data-stu-id="80e38-154">Retry job submission for up tootwo minutes</span></span> |
| <span data-ttu-id="80e38-155">使用的工作識別碼無效</span><span class="sxs-lookup"><span data-stu-id="80e38-155">An Invalid job id was used</span></span> |<span data-ttu-id="80e38-156">請檢查是否正確 hello 作業識別碼</span><span class="sxs-lookup"><span data-stu-id="80e38-156">Check if hello job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="80e38-157">閘道不正確</span><span class="sxs-lookup"><span data-stu-id="80e38-157">Bad gateway</span></span>

<span data-ttu-id="80e38-158">**HTTP 狀態碼**：502</span><span class="sxs-lookup"><span data-stu-id="80e38-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="80e38-159">原因</span><span class="sxs-lookup"><span data-stu-id="80e38-159">Cause</span></span> | <span data-ttu-id="80e38-160">解決方案</span><span class="sxs-lookup"><span data-stu-id="80e38-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="80e38-161">內部記憶體回收發生在 hello WebHCat 程序</span><span class="sxs-lookup"><span data-stu-id="80e38-161">Internal garbage collection is occurring within hello WebHCat process</span></span> |<span data-ttu-id="80e38-162">等候記憶體回收集合 toofinish 或重新啟動 hello WebHCat 服務</span><span class="sxs-lookup"><span data-stu-id="80e38-162">Wait for garbage collection toofinish or restart hello WebHCat service</span></span> |
| <span data-ttu-id="80e38-163">逾時等候 hello ResourceManager 服務的回應。</span><span class="sxs-lookup"><span data-stu-id="80e38-163">Time out waiting on a response from hello ResourceManager service.</span></span> <span data-ttu-id="80e38-164">當使用中的應用程式的 hello 數目變成 hello 設定最大值 （預設值 10000） 時，會發生這個錯誤</span><span class="sxs-lookup"><span data-stu-id="80e38-164">This error can occur when hello number of active applications goes hello configured maximum (default 10,000)</span></span> |<span data-ttu-id="80e38-165">等待目前執行的作業 toocomplete 或藉由修改提高 hello 並行工作限制`yarn.scheduler.capacity.maximum-applications`。</span><span class="sxs-lookup"><span data-stu-id="80e38-165">Wait for currently running jobs toocomplete or increase hello concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="80e38-166">如需詳細資訊，請參閱 hello[修改組態](#modifying-configuration)> 一節。</span><span class="sxs-lookup"><span data-stu-id="80e38-166">For more information, see hello [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="80e38-167">嘗試透過 hello 的所有工作 tooretrieve [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs)時呼叫`Fields`太設定`*`</span><span class="sxs-lookup"><span data-stu-id="80e38-167">Attempting tooretrieve all jobs through hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set too`*`</span></span> |<span data-ttu-id="80e38-168">不要擷取*所有*作業詳細資料。</span><span class="sxs-lookup"><span data-stu-id="80e38-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="80e38-169">改用`jobid`tooretrieve 作業只大於特定的作業識別碼的詳細資料。或者，不要使用 `Fields`</span><span class="sxs-lookup"><span data-stu-id="80e38-169">Instead use `jobid` tooretrieve details for jobs only greater than certain job id. Or, do not use `Fields`</span></span> |
| <span data-ttu-id="80e38-170">在前端節點容錯移轉期間 hello WebHCat 服務已關閉</span><span class="sxs-lookup"><span data-stu-id="80e38-170">hello WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="80e38-171">等待兩分鐘後再重試 hello 作業</span><span class="sxs-lookup"><span data-stu-id="80e38-171">Wait for two minutes and retry hello operation</span></span> |
| <span data-ttu-id="80e38-172">有 500 個以上透過 WebHCat 提交的擱置工作</span><span class="sxs-lookup"><span data-stu-id="80e38-172">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="80e38-173">等到目前擱置的工作完成，再送出更多工作</span><span class="sxs-lookup"><span data-stu-id="80e38-173">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml

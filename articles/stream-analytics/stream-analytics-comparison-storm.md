---
title: "分析平台： Apache Storm 比較 tooStream 分析 |Microsoft 文件"
description: "取得使用 Apache Storm 比較 tooStream 分析選擇雲端分析平台的指引。 了解功能和差異。"
keywords: "分析平台, 分析平台, 雲端分析平台, storm 比較"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a><span data-ttu-id="e2ab4-105">選擇串流分析平台：比較 Apache Storm 與 Azure 串流分析</span><span class="sxs-lookup"><span data-stu-id="e2ab4-105">Choosing a streaming analytics platform: comparing Apache Storm and Azure Stream Analytics</span></span>
<span data-ttu-id="e2ab4-106">Azure 提供多種解決方案來分析串流資料：[Azure 串流分析](https://docs.microsoft.com/azure/stream-analytics/)和 [Azure HDInsight 上的 Apache Storm](https://azure.microsoft.com/services/hdinsight/apache-storm/)。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-106">Azure provides multiple solutions for analyzing streaming data: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) and [Apache Storm on Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span></span> <span data-ttu-id="e2ab4-107">這兩個分析平台提供 hello PaaS 解決方案的優點。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-107">Both analytics platforms provide hello benefits of a PaaS solution.</span></span> <span data-ttu-id="e2ab4-108">但 hello 平台都有一些顯著的差異，功能也如同您設定和管理它們的方式。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-108">But hello platforms have some significant differences in their capabilities as well as in how you configure and manage them.</span></span> 

<span data-ttu-id="e2ab4-109">本文章提供您選擇 Apache Storm 或 Azure Stream Analytics 中做為雲端分析平台功能 toohelp 來並行比較。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-109">This article provides a side-by-side comparison of features toohelp you choose between Apache Storm and Azure Stream Analytics as a cloud analytics platform.</span></span> 

## <a name="general-features"></a><span data-ttu-id="e2ab4-110">一般功能</span><span class="sxs-lookup"><span data-stu-id="e2ab4-110">General features</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-111">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-111">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="e2ab4-112">
                    <strong>Azure 串流分析</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-112">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="e2ab4-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-114">
                    <strong>開放原始碼？</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-114">
                    <strong>Open source?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-115">不可以。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-115">No.</span></span> <span data-ttu-id="e2ab4-116">Azure 串流分析 Microsoft 專屬服務。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-116">Azure Stream Analytics is a Microsoft proprietary offering.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-117">是。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-117">Yes.</span></span> <span data-ttu-id="e2ab4-118">Apache Storm 是 Apache 授權技術。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-118">Apache Storm is an Apache licensed technology.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-119">
                    <strong>Microsoft 支援服務？</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-119">
                    <strong>Microsoft support?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-120">是</span><span class="sxs-lookup"><span data-stu-id="e2ab4-120">Yes</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-121">是</span><span class="sxs-lookup"><span data-stu-id="e2ab4-121">Yes</span></span> </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-122">
                    <strong>硬體需求</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-122">
                    <strong>Hardware requirements</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-123">無。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-123">None.</span></span> <span data-ttu-id="e2ab4-124">Azure 串流分析是一種 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-124">Azure Stream Analytics is an Azure Service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-125">無。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-125">None.</span></span> <span data-ttu-id="e2ab4-126">Apache Storm 是一種 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-126">Apache Storm is an Azure Service.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-127">
                    <strong>最上層單位</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-127">
                    <strong>Top-level unit</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-128">使用者可部署和監視串流作業。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-128">Users deploy and monitor streaming jobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-129">使用者可部署和監視整個叢集，該叢集可裝載多個 Storm 作業，以及其他工作負載 (包括批次)。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-129">Users deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other workloads (including batch).</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-130">
                    <strong>價格</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-130">
                    <strong>Pricing</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-131">價格所處理的資料量，且 hello 數目的資料流單位需要每小時 hello 工作正在執行。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-131">Priced by volume of data processed and hello number of streaming units required per hour that hello job is running.</span></span> 
                </p>
                    <p><span data-ttu-id="e2ab4-132">如需詳細資訊，請參閱<a href="http://azure.microsoft.com/pricing/details/stream-analytics/">串流分析定價</a>。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-132">For more information, see <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics Pricing</a>.</span></span></p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-133">購買 hello 單位是以叢集為基礎，而且會負責根據準時 hello hello 叢集正在執行，獨立於部署的工作。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-133">hello unit of purchase is cluster-based, and is charged based on hello time hello cluster is running, independent of jobs deployed.</span></span>
                </p>
                <p>
<span data-ttu-id="e2ab4-134">如需詳細資訊，請參閱 <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight 定價</a>。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-134">For more information, see <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight pricing</a>.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a><span data-ttu-id="e2ab4-135">編寫</span><span class="sxs-lookup"><span data-stu-id="e2ab4-135">Authoring</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-136">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-136">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="e2ab4-137">
                    <strong>Azure 串流分析</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-137">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="e2ab4-138">
                    <strong>Apache Storm on HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-138">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-139">
                    <strong>功能：SQL DSL？</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-139">
                    <strong>Capabilities: SQL DSL?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-140">是。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-140">Yes.</span></span> <span data-ttu-id="e2ab4-141">串流分析提供類似 SQL 的語言來建立轉換。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-141">Stream Analytics provides a SQL-like language for creating transformations.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-142">否。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-142">No.</span></span> <span data-ttu-id="e2ab4-143">使用者可用 Java 或 C# 來撰寫程式碼，或使用 Trident API。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-143">Users write code in Java or C#, or use Trident APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-144">
                    <strong>功能：時態性運算子？</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-144">
                    <strong>Capabilities: Temporal operators?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-145">預設支援時間範圍的彙總和時態性聯結。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-145">Windowed aggregates and temporal joins are supported by default.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-146">必須實作 hello 使用者暫時運算子。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-146">Temporal operators must be implemented by hello user.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-147">
                    <strong>開發經驗</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-147">
                    <strong>Development experience</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-148">使用者可以建立、 偵錯和監視 hello Azure 入口網站中的工作使用衍生自即時資料流的範例資料。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-148">Users can create, debug, and monitor jobs through hello Azure portal, using sample data derived from a live stream.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-149">使用 .NET 使用者可以透過 Visual Studio 來開發、偵錯和監視。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-149">Users using .NET can develop, debug, and monitor through Visual Studio.</span></span> <span data-ttu-id="e2ab4-150">使用 Java 或其他語言的使用者可以使用自己選擇的 IDE hello。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-150">Users using Java or other languages can use hello IDE of their choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-151">
                    <strong>偵錯支援</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-151">
                    <strong>Debugging support</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-152">基本的工作狀態和操作記錄檔的可用 toohelp 偵錯。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-152">Basic job status and operations logs are available toohelp debug.</span></span> <span data-ttu-id="e2ab4-153">目前資料流分析不會讓使用者指定內容量納入 hello 記錄檔 （亦即，詳細資訊模式）。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-153">Stream Analytics currently does not let users specify what content or how much content is included in hello logs (i.e., verbose mode).</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-154">有詳細的記錄可用。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-154">Detailed logs are available.</span></span> <span data-ttu-id="e2ab4-155">使用者可以存取 Visual Studio 中或 toohello 叢集中的記錄，並直接存取 hello 記錄檔的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-155">Users can access logs in Visual Studio or by logging in toohello cluster and accessing hello logs directly.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-156">
                    <strong>使用自訂程式碼來擴充？</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-156">
                    <strong>Extensibility using custom code?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-157">部分支援 JavaScript UDF。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-157">Partially support with JavaScript UDFs.</span></span> <span data-ttu-id="e2ab4-158">如需詳細資訊，請參閱 <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF 整合</a>。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-158">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF integration</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-159">是。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-159">Yes.</span></span> <span data-ttu-id="e2ab4-160">使用者可以使用 C#、Java 或 Strom 支援的其他任何語言來撰寫自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-160">Users can write custom code in C#, Java, or any other language supported on Storm.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a><span data-ttu-id="e2ab4-161">資料來源 (輸入) 和輸出</span><span class="sxs-lookup"><span data-stu-id="e2ab4-161">Data sources (inputs) and outputs</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-162">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-162">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="e2ab4-163">
                    <strong>Azure 串流分析</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-163">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="e2ab4-164">
                    <strong>Apache Storm on HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-164">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-165">
                 <strong>輸入資料來源</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-165">
                 <strong>Input data sources</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="e2ab4-166">Azure 事件中樞和 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-166">Azure Event Hubs and Azure Blob storage.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-167">有適用於 Azure 事件中樞、Microsoft Azure 服務匯流排、Kafka 等的連接器可用。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-167">Connectors are available for Azure Event Hubs, Azure Service Bus, Kafka, and more.</span></span> <span data-ttu-id="e2ab4-168">使用者可以使用自訂程式碼來建立其他連接器。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-168">Users can create additional connectors using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-169">
                    <strong>輸入資料格式</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-169">
                    <strong>Input data formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-170">Avro、JSON、CSV</span><span class="sxs-lookup"><span data-stu-id="e2ab4-170">Avro, JSON, CSV</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-171">使用者可以使用自訂程式碼來實作任何格式。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-171">Users can implement any format using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-172">
                    <strong>輸出</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-172">
                    <strong>Outputs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-173">一個串流作業可以有多個輸出。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-173">A streaming job can have multiple outputs.</span></span> <span data-ttu-id="e2ab4-174">支援的輸出包括 Azure 事件中樞、Azure Blob 儲存體、Azure 資料表儲存體、Azure SQL DB 和 Power BI。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-174">Supported outputs are Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB, and Power BI.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-175">Storm 在一個拓撲中支援多個輸出，每個輸出可以有自訂邏輯來進行下游處理。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-175">Storm supports many outputs in a topology, and each output can have custom logic for downstream processing.</span></span> <span data-ttu-id="e2ab4-176">Storm 包含適用於 Power BI、Azure 事件中樞、Azure Blob 儲存體、Azure Cosmos DB、SQL 和 HBase 的連接器。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-176">Storm includes connectors for Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL, and HBase.</span></span> <span data-ttu-id="e2ab4-177">使用者可以使用自訂程式碼來建立其他連接器。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-177">Users can create additional connectors using custom code.</span></span>    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-178">
                    <strong>資料編碼格式</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-178">
                    <strong>Data-encoding formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-179">資料必須以 UTF-8 製作格式。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-179">Data must be formatted using UTF-8.</span></span>
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-180">使用者可以使用自訂程式碼來實作任何資料編碼。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-180">Users can implement any data encoding format using custom code.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a><span data-ttu-id="e2ab4-181">管理和作業</span><span class="sxs-lookup"><span data-stu-id="e2ab4-181">Management and operations</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-182">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-182">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="e2ab4-183">
                    <strong>Azure 串流分析</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-183">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="e2ab4-184">
                    <strong>Apache Storm on HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-184">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-185">
                    <strong>作業部署模型</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-185">
                    <strong>Job deployment model</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-186">Azure 入口網站、PowerShell 和 REST API。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-186">Azure portal, PowerShell, and REST APIs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-187">Azure 入口網站、PowerShell、Visual Studio 和 REST API。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-187">Azure portal, PowerShell, Visual Studio, and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-188">
                    <strong>監視 (統計資料、計數器等)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-188">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-189">使用者可使用 Azure 入口網站和 REST API 實作監視。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-189">Monitoring is implemented using Azure portal and REST APIs.</span></span> <span data-ttu-id="e2ab4-190">使用者也可以設定 Azure 警示。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-190">Users can also configure Azure alerts.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-191">監視使用實作 hello Storm UI 和 REST Api。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-191">Monitoring is implemented using hello Storm UI and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-192">
                    <strong>延展性</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-192">
                    <strong>Scalability</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-193">延展性取決於 hello Streaming Units 數目 (SUs) 為每個工作。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-193">Scalability is determined by hello number of Streaming Units (SUs) for each job.</span></span> <span data-ttu-id="e2ab4-194">每個資料流處理單位 too1 總 MB/秒，使用處理最多 50 個單位。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-194">Each Streaming Unit processes up too1 MB/second, with a maximum 50 units.</span></span> <span data-ttu-id="e2ab4-195">如需詳細資訊，請參閱<a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">標尺 tooincrease 輸送量</a>。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-195">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale tooincrease throughput</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-196">Hello hello HDInsight Storm 叢集的節點數目取決於延展性。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-196">Scalability is determined by hello number of nodes in hello HDInsight Storm cluster.</span></span> <span data-ttu-id="e2ab4-197">hello 使用者 Azure 配額均 hello 最上層節點的 hello 數目限制。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-197">hello top limit on hello number of nodes is defined by hello user's Azure quota.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-198">
                    <strong>資料處理限制</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-198">
                    <strong>Data processing limits</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-199">使用者可以增加資料處理，或藉由增加或減少 hello Streaming Units 數目，上限為 1 GB/秒與最佳化成本。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-199">Users can increase data processing or optimize costs by increasing or decreasing hello number of Streaming Units, with an upper limit of 1 GB/second.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-200">使用者可以將叢集相應增加或相應減少。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-200">Users can scale cluster size up or down.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-201">
                    <strong>停止/繼續</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-201">
                    <strong>Stop/Resume</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-202">停止並從上次的停止處繼續。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-202">Stop and resume from last place stopped.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-203">停止並根據浮水印從上次的停止處繼續。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-203">Stop and resume from last place stopped based on a watermark.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-204">
                    <strong>服務和架構更新</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-204">
                    <strong>Service and framework update</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-205">可不停機自動修補。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-205">Automatic patching with no downtime.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-206">可不停機自動修補。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-206">Automatic patching with no downtime.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-207">
                    <strong>透過具有 SLA 保證所保障的高可用性服務提供商務持續性</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLAs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li><span data-ttu-id="e2ab4-208">SLA 保證運作時間達 99.9%</span><span class="sxs-lookup"><span data-stu-id="e2ab4-208">SLA of 99.9% uptime</span></span></li>
                <li><span data-ttu-id="e2ab4-209">可在失敗時自動復原</span><span class="sxs-lookup"><span data-stu-id="e2ab4-209">Auto-recovery from failures</span></span></li>
                <li><span data-ttu-id="e2ab4-210">內建復原可設定狀態的時態性運算子</span><span class="sxs-lookup"><span data-stu-id="e2ab4-210">Built-in recovery of stateful temporal operators</span></span></li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-211">99.9%正常運作的 hello Storm 叢集的 SLA。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-211">SLA of 99.9% uptime of hello Storm cluster.</span></span> 
                </p>
                <p>
<span data-ttu-id="e2ab4-212">Apache Storm 是容錯的串流平台。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-212">Apache Storm is a fault-tolerant streaming platform.</span></span> <span data-ttu-id="e2ab4-213">不過，它是 hello 使用者的責任 tooensure 串流處理的工作不會中斷的執行。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-213">However, it is hello user's responsibility tooensure that streaming jobs run uninterrupted.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a><span data-ttu-id="e2ab4-214">進階功能</span><span class="sxs-lookup"><span data-stu-id="e2ab4-214">Advanced features</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-215">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-215">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="e2ab4-216">
                    <strong>Azure 串流分析</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-216">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="e2ab4-217">
                    <strong>Apache Storm on HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-217">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-218">
                    <strong>延遲傳入和失序事件處理</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-218">
                    <strong>Late arrival and out-of-order event handling</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-219">內建可設定的原則可以重新排序事件、捨棄事件或調整事件時間。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-219">Built-in configurable policies can reorder events, drop events, or adjust event time.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-220">使用者必須實作此案例中的邏輯 toohandle。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-220">Users must implement logic toohandle this scenario.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-221">
                    <strong>參考資料</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-221">
                    <strong>Reference data</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-222">可從 Azure Blob 儲存體取得參考資料，記憶體內部快取最大為 100 MB。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-222">Reference data is available from Azure Blob storage with a maximum of 100 MB of in-memory cache.</span></span> <span data-ttu-id="e2ab4-223">Hello 服務重新整理參考資料。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-223">Reference data is refreshed by hello service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-224">資料大小沒有限制。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-224">No limits on data size.</span></span> <span data-ttu-id="e2ab4-225">有適用於 HBase、Azure Cosmos DB、SQL Server 和 Azure 的連接器可用。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-225">Connectors are available for HBase, Azure Cosmos DB, SQL Server, and Azure.</span></span> <span data-ttu-id="e2ab4-226">使用者可以使用自訂程式碼來建立其他連接器。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-226">Users can create additional connectors using custom code.</span></span> <span data-ttu-id="e2ab4-227">必須使用自訂程式碼來重新整理參考資料。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-227">Reference data must be refreshed using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="e2ab4-228">
                    <strong>與 Machine Learning 整合</strong>
                </span><span class="sxs-lookup"><span data-stu-id="e2ab4-228">
                    <strong>Integration with Machine Learning</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="e2ab4-229">在建立作業期間，已發佈的 Azure Machine Learning 模型可設定為函式。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-229">Published Azure Machine Learning models can be configured as functions during job creation.</span></span> <span data-ttu-id="e2ab4-230">如需詳細資訊，請參閱<a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">為 Machine Learning 函式進行規模調整</a>。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-230">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scale for Machine Learning functions</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="e2ab4-231">透過 Storm Bolt 提供。</span><span class="sxs-lookup"><span data-stu-id="e2ab4-231">Available through Storm Bolts.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

---
title: "SCP.NET 程式設計指南 | Microsoft Docs"
description: "了解如何使用 SCP.NET 建立以 .NET 為基礎的 Storm 拓撲並用於 HDInsight 上的 Storm。"
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: 3d76aebd2a1fd729c8e0639e6afcbde4c3fb752b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="5d546-103">SCP 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="5d546-103">SCP programming guide</span></span>
<span data-ttu-id="5d546-104">SCP 是一個用來建置即時、可靠、一致和高效能資料處理應用程式的平台。</span><span class="sxs-lookup"><span data-stu-id="5d546-104">SCP is a platform to build real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="5d546-105">建置在由 OSS 社群所設計的串流處理系統 [Apache Storm](http://storm.incubator.apache.org/) 之上。</span><span class="sxs-lookup"><span data-stu-id="5d546-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by the OSS communities.</span></span> <span data-ttu-id="5d546-106">Storm 由 Nathan Marz 所設計，由 Twitter 公開原始碼。</span><span class="sxs-lookup"><span data-stu-id="5d546-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="5d546-107">它採用 [Apache ZooKeeper](http://zookeeper.apache.org/)，這是另一個可發揮極可靠的分散式協調和狀態管理的 Apache 專案。</span><span class="sxs-lookup"><span data-stu-id="5d546-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project to enable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="5d546-108">SCP 專案不僅將 Storm 移植到 Windows 上，此專案也為 Windows 生態系統加入擴充和自訂功能。</span><span class="sxs-lookup"><span data-stu-id="5d546-108">Not only the SCP project ported Storm on Windows but also the project added extensions and customization for the Windows ecosystem.</span></span> <span data-ttu-id="5d546-109">擴充功能包括 .NET 開發人員體驗和程式庫，自訂功能包括以 Windows 為基礎的部署。</span><span class="sxs-lookup"><span data-stu-id="5d546-109">The extensions include .NET developer experience, and libraries, the customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="5d546-110">擴充和自訂功能的設計讓我們不需要將 OSS 專案分岔，我們可以運用根據 Storm 而導出的生態系統。</span><span class="sxs-lookup"><span data-stu-id="5d546-110">The extension and customization is done in such a way that we do not need to fork the OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="5d546-111">處理模型</span><span class="sxs-lookup"><span data-stu-id="5d546-111">Processing model</span></span>
<span data-ttu-id="5d546-112">SCP 中的資料模擬成連續的 Tuple 串流。</span><span class="sxs-lookup"><span data-stu-id="5d546-112">The data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="5d546-113">通常，Tuple 會先流進一些佇列，經過挑選，再由 Storm 拓撲內裝載的商業邏輯來轉換，最後，輸出以 Tuple 的形式傳遞至另一個 SCP 系統，或認可到存放區 (例如分散式檔案系統) 或資料庫 (例如 SQL Server)。</span><span class="sxs-lookup"><span data-stu-id="5d546-113">Typically the tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally the output could be piped as tuples to another SCP system, or be committed to stores like distributed file system or databases like SQL Server.</span></span>

![佇列饋送資料 (饋送資料存放區) 以供處理的圖](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="5d546-115">在 Storm 中，應用程式拓撲定義一份運算圖。</span><span class="sxs-lookup"><span data-stu-id="5d546-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="5d546-116">拓撲中的每個節點包含處理邏輯，節點之間的連結代表資料流程。</span><span class="sxs-lookup"><span data-stu-id="5d546-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="5d546-117">將輸入資料注入拓撲中的節點稱為 Spout，可用來編排資料。</span><span class="sxs-lookup"><span data-stu-id="5d546-117">The nodes to inject input data into the topology are called Spouts, which can be used to sequence the data.</span></span> <span data-ttu-id="5d546-118">輸入資料可能位於檔案記錄、交易式資料庫、系統效能計數器等。同時有輸入和輸出資料流程的節點稱為 Bolt，負責進行實際的資料篩選及挑選和彙總。</span><span class="sxs-lookup"><span data-stu-id="5d546-118">The input data could reside in file logs, transactional database, system performance counter etc. The nodes with both input and output data flows are called Bolts, which do the actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="5d546-119">SCP 支援竭盡所能、至少一次和剛好一次這三種資料處理方法。</span><span class="sxs-lookup"><span data-stu-id="5d546-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="5d546-120">在分散式串流處理應用程式中，資料處理期間可能發生各種錯誤，例如網路中斷、機器故障或使用者程式碼錯誤等。至少一次的處理方法會在錯誤發生時自動重播相同資料，以確保所有資料至少處理一次。</span><span class="sxs-lookup"><span data-stu-id="5d546-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically the same data when error happens.</span></span> <span data-ttu-id="5d546-121">至少一次的處理方法簡單又可靠，在許多應用程式中都很適合。</span><span class="sxs-lookup"><span data-stu-id="5d546-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="5d546-122">不過，當應用程式需要準確計數時 (只是舉例)，至少一次的處理方法就無法勝任，因為同樣的資料可能在應用程式拓撲中播放。</span><span class="sxs-lookup"><span data-stu-id="5d546-122">However, when the application requires exact counting, for example, at-least-once processing is insufficient since the same data could potentially be played in the application topology.</span></span> <span data-ttu-id="5d546-123">在此情況下，剛好一次的處理方法可確保即使資料可能重播和處理多次，結果也一定正確。</span><span class="sxs-lookup"><span data-stu-id="5d546-123">In that case, exactly-once processing is designed to make sure the result is correct even when the data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="5d546-124">SCP 可讓 .NET 開發人員以 Java 虛擬機器 (JVM) 型 Storm 為基礎，開發即時資料處理應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d546-124">SCP enables .NET developers to develop real time data process applications while leverage the Java Virtual Machine (JVM) based Storm under the cover.</span></span> <span data-ttu-id="5d546-125">.NET 與 JVM 是透過 TCP 本機通訊端來進行通訊。</span><span class="sxs-lookup"><span data-stu-id="5d546-125">The .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="5d546-126">基本上，每個 Spout/Bolt 就是一對 .Net/Java 程序，而使用者邏輯在 .Net 程序中以外掛程式的方式運作。</span><span class="sxs-lookup"><span data-stu-id="5d546-126">Basically each Spout/Bolt is a .Net/Java process pair, where the user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="5d546-127">若要根據 SCP 來建置資料處理應用程式，需要幾個步驟：</span><span class="sxs-lookup"><span data-stu-id="5d546-127">To build a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="5d546-128">設計和實作 Spout 從佇列中拉進資料。</span><span class="sxs-lookup"><span data-stu-id="5d546-128">Design and implement the Spouts to pull in data from queue.</span></span>
* <span data-ttu-id="5d546-129">設計和實作 Bolt 來處理輸入資料，並將資料儲存至外部存放區，例如資料庫。</span><span class="sxs-lookup"><span data-stu-id="5d546-129">Design and implement Bolts to process the input data, and save data to external stores such as Database.</span></span>
* <span data-ttu-id="5d546-130">設計拓撲，然後提交並執行拓撲。</span><span class="sxs-lookup"><span data-stu-id="5d546-130">Design the topology, then submit and run the topology.</span></span> <span data-ttu-id="5d546-131">拓撲定義頂點及頂點之間的資料流程。</span><span class="sxs-lookup"><span data-stu-id="5d546-131">The topology defines vertexes and the data flows between the vertexes.</span></span> <span data-ttu-id="5d546-132">SCP 會採納拓撲規格，並部署到 Storm 叢集，而每個頂點就在一個邏輯節點上運作。</span><span class="sxs-lookup"><span data-stu-id="5d546-132">SCP will take the topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="5d546-133">容錯移轉和調整由 Storm 工作排程器負責處理。</span><span class="sxs-lookup"><span data-stu-id="5d546-133">The failover and scaling will be taken care of by the Storm task scheduler.</span></span>

<span data-ttu-id="5d546-134">本文利用一些簡單的範例來逐步解說如何使用 SCP 建置資料處理應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d546-134">This document will use some simple examples to walk through how to build data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="5d546-135">SCP 外掛程式介面</span><span class="sxs-lookup"><span data-stu-id="5d546-135">SCP Plugin Interface</span></span>
<span data-ttu-id="5d546-136">SCP 外掛程式 (或應用程式) 是獨立式 EXE，可在開發階段於 Visual Studio 內執行，也可以在部署到實際執行環境之後插入 Storm 管線中。</span><span class="sxs-lookup"><span data-stu-id="5d546-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during the development phase, and be plugged into the Storm pipeline after deployment in production.</span></span> <span data-ttu-id="5d546-137">撰寫 SCP 外掛程式就像是撰寫其他任何標準的 Windows 主控台應用程式一樣。</span><span class="sxs-lookup"><span data-stu-id="5d546-137">Writing the SCP plugin is just the same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="5d546-138">SCP.NET 平台為 spout/bolt 宣告一些介面，使用者外掛程式的程式碼應該實作這些介面。</span><span class="sxs-lookup"><span data-stu-id="5d546-138">SCP.NET platform declares some interface for spout/bolt, and the user plugin code should implement these interfaces.</span></span> <span data-ttu-id="5d546-139">此設計的主要目的是讓用者專注於自己的商業邏輯，將其他一切交給 SCP.NET 平台來處理。</span><span class="sxs-lookup"><span data-stu-id="5d546-139">The main purpose of this design is that the user can focus on their own business logics, and leaving other things to be handled by SCP.NET platform.</span></span>

<span data-ttu-id="5d546-140">使用者外掛程式的程式碼應該實作下列其中一個介面，視拓撲為交易式或非交易式而定，以及元作是 spout 或 bolt 而定。</span><span class="sxs-lookup"><span data-stu-id="5d546-140">The user plugin code should implement one of the followings interfaces, depends on whether the topology is transactional or non-transactional, and whether the component is spout or bolt.</span></span>

* <span data-ttu-id="5d546-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="5d546-141">ISCPSpout</span></span>
* <span data-ttu-id="5d546-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="5d546-142">ISCPBolt</span></span>
* <span data-ttu-id="5d546-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="5d546-143">ISCPTxSpout</span></span>
* <span data-ttu-id="5d546-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="5d546-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="5d546-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="5d546-145">ISCPPlugin</span></span>
<span data-ttu-id="5d546-146">ISCPPlugin 是各種外掛程式的共同介面。</span><span class="sxs-lookup"><span data-stu-id="5d546-146">ISCPPlugin is the common interface for all kinds of plugins.</span></span> <span data-ttu-id="5d546-147">目前為虛擬介面。</span><span class="sxs-lookup"><span data-stu-id="5d546-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="5d546-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="5d546-148">ISCPSpout</span></span>
<span data-ttu-id="5d546-149">ISCPSpout 為非交易式 spout 的介面。</span><span class="sxs-lookup"><span data-stu-id="5d546-149">ISCPSpout is the interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="5d546-150">呼叫 `NextTuple()` 時，C\# 使用者程式碼可能發出一或多個 Tuple。</span><span class="sxs-lookup"><span data-stu-id="5d546-150">When `NextTuple()` is called, the C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="5d546-151">如果沒有資料可發出，此方法應該返回而不發出任何資料。</span><span class="sxs-lookup"><span data-stu-id="5d546-151">If there is nothing to emit, this method should return without emitting anything.</span></span> <span data-ttu-id="5d546-152">請注意，`NextTuple()`、`Ack()` 和 `Fail()` 都是在 C\# 程序的單一執行緒中放在密封迴圈內呼叫。</span><span class="sxs-lookup"><span data-stu-id="5d546-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="5d546-153">沒有 Tuple 可發出時，建議讓 NextTuple 短暫休息 (例如 10 毫秒)，不致於浪費太多 CPU。</span><span class="sxs-lookup"><span data-stu-id="5d546-153">When there are no tuples to emit, it is courteous to have NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="5d546-154">只有當規格檔中啟用認可機制時，才會呼叫 `Ack()` 和 `Fail()`。</span><span class="sxs-lookup"><span data-stu-id="5d546-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="5d546-155">`seqId` 用來識別已認可或失敗的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="5d546-155">The `seqId` is used to identify the tuple which is acked or failed.</span></span> <span data-ttu-id="5d546-156">因此，如果非交易式拓撲中啟用認可，則 Spout 中應該使用下列 emit 函數：</span><span class="sxs-lookup"><span data-stu-id="5d546-156">So if ack is enabled in non-transactional topology, the following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="5d546-157">如果非交易式拓撲中不支援認可，則 `Ack()` 和 `Fail()` 可保持為空白函數。</span><span class="sxs-lookup"><span data-stu-id="5d546-157">If ack is not supported in non-transactional topology, the `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="5d546-158">這些函數中的 `parms` 輸入參數只是空的 Dictionary，保留供未來使用。</span><span class="sxs-lookup"><span data-stu-id="5d546-158">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="5d546-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="5d546-159">ISCPBolt</span></span>
<span data-ttu-id="5d546-160">ISCPBolt 為非交易式 bolt 的介面。</span><span class="sxs-lookup"><span data-stu-id="5d546-160">ISCPBolt is the interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="5d546-161">有新的 Tuple 可用時，將會呼叫 `Execute()` 函數來處理它。</span><span class="sxs-lookup"><span data-stu-id="5d546-161">When new tuple is available, the `Execute()` function will be called to process it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="5d546-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="5d546-162">ISCPTxSpout</span></span>
<span data-ttu-id="5d546-163">ISCPTxSpout 為交易式 spout 的介面。</span><span class="sxs-lookup"><span data-stu-id="5d546-163">ISCPTxSpout is the interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="5d546-164">就像對應的非交易式節點一樣，`NextTx()`、`Ack()` 和 `Fail()` 也都是在 C\# 程序的單一執行緒中放在密封迴圈內呼叫。</span><span class="sxs-lookup"><span data-stu-id="5d546-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="5d546-165">沒有資料可發出時，建議讓 `NextTx` 短暫休息 (10 毫秒)，不致於浪費太多 CPU。</span><span class="sxs-lookup"><span data-stu-id="5d546-165">When there are no data to emit, it is courteous to have `NextTx` sleep for a short amount of time (10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="5d546-166">`NextTx()` 可呼叫來啟動新的交易，out 參數 `seqId` 用來識別交易，`Ack()` 和 `Fail()` 中也使用此參數。</span><span class="sxs-lookup"><span data-stu-id="5d546-166">`NextTx()` is called to start a new transaction, the out parameter `seqId` is used to identify the transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="5d546-167">在 `NextTx()`中，使用者可以發出資料給 Java 端。</span><span class="sxs-lookup"><span data-stu-id="5d546-167">In `NextTx()`, user can emit data to Java side.</span></span> <span data-ttu-id="5d546-168">資料會儲存在 ZooKeeper 中以支援重播。</span><span class="sxs-lookup"><span data-stu-id="5d546-168">The data will be stored in ZooKeeper to support replay.</span></span> <span data-ttu-id="5d546-169">因為 ZooKeeper 的容量極為有限，使用者在交易式 spout 中應該只發出中繼資料，而非大量資料。</span><span class="sxs-lookup"><span data-stu-id="5d546-169">Because the capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="5d546-170">Storm 會自動重播交易 (若失敗)，所以正常情況下應該不會呼叫 `Fail()` 。</span><span class="sxs-lookup"><span data-stu-id="5d546-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="5d546-171">但是，如果 SCP 可以檢查交易式 spout 所發出的元資料，則元資料無效時可以呼叫 `Fail()` 。</span><span class="sxs-lookup"><span data-stu-id="5d546-171">But if SCP can check the metadata emitted by transactional spout, it can call `Fail()` when the metadata is invalid.</span></span>

<span data-ttu-id="5d546-172">這些函數中的 `parms` 輸入參數只是空的 Dictionary，保留供未來使用。</span><span class="sxs-lookup"><span data-stu-id="5d546-172">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="5d546-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="5d546-173">ISCPBatchBolt</span></span>
<span data-ttu-id="5d546-174">ISCPBatchBolt 為交易式 bolt 的介面。</span><span class="sxs-lookup"><span data-stu-id="5d546-174">ISCPBatchBolt is the interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="5d546-175">`Execute()` 。</span><span class="sxs-lookup"><span data-stu-id="5d546-175">`Execute()` is called when there is new tuple arriving at the bolt.</span></span> <span data-ttu-id="5d546-176">`FinishBatch()` 。</span><span class="sxs-lookup"><span data-stu-id="5d546-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="5d546-177">`parms` 輸入參數保留供未來使用。</span><span class="sxs-lookup"><span data-stu-id="5d546-177">The `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="5d546-178">在交易式拓撲中，有一個重要的概念 – `StormTxAttempt`。</span><span class="sxs-lookup"><span data-stu-id="5d546-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="5d546-179">它有 `TxId` 和 `AttemptId` 兩個欄位。</span><span class="sxs-lookup"><span data-stu-id="5d546-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="5d546-180">`TxId` 用來識別特定的交易，在給定的交易中，如果交易失敗且重播，可能會嘗試很多次。</span><span class="sxs-lookup"><span data-stu-id="5d546-180">`TxId` is used to identify a specific transaction, and for a given transaction, there may be multiple attempt if the transaction fails and is replayed.</span></span> <span data-ttu-id="5d546-181">SCP.NET 會建立一個不同的 ISCPBatchBolt 物件來處理每個 `StormTxAttempt`，就像 Storm 在 Java 端的做法一樣。</span><span class="sxs-lookup"><span data-stu-id="5d546-181">SCP.NET will new a different ISCPBatchBolt object to process each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="5d546-182">此設計是為了支援平行交易處理。</span><span class="sxs-lookup"><span data-stu-id="5d546-182">The purpose of this design is to support parallel transactions processing.</span></span> <span data-ttu-id="5d546-183">使用者應該留意，如果交易嘗試完成，則會終結對應的 ISCPBatchBolt 物件，並回收其記憶體。</span><span class="sxs-lookup"><span data-stu-id="5d546-183">User should keep it in mind that if transaction attempt is finished, the corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="5d546-184">物件模型</span><span class="sxs-lookup"><span data-stu-id="5d546-184">Object Model</span></span>
<span data-ttu-id="5d546-185">SCP.NET 也提供一組簡單的關鍵物件供開發人員在程式設計中使用。</span><span class="sxs-lookup"><span data-stu-id="5d546-185">SCP.NET also provides a simple set of key objects for developers to program with.</span></span> <span data-ttu-id="5d546-186">包括 **Context**、**StateStore** 和 **SCPRuntime**。</span><span class="sxs-lookup"><span data-stu-id="5d546-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="5d546-187">本節其餘部分將討論這些物件。</span><span class="sxs-lookup"><span data-stu-id="5d546-187">They will be discussed in the rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="5d546-188">Context</span><span class="sxs-lookup"><span data-stu-id="5d546-188">Context</span></span>
<span data-ttu-id="5d546-189">Context 提供應用程式的執行環境。</span><span class="sxs-lookup"><span data-stu-id="5d546-189">Context provides a running environment to the application.</span></span> <span data-ttu-id="5d546-190">每個 ISCPPlugin 執行個體 (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) 都有一個對應的 Context 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5d546-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="5d546-191">Context 提供的功能分成兩部分：(1) 靜態部分，供整個 C\# 程序使用，(2) 動態部分，僅供特定的 Context 執行個體使用。</span><span class="sxs-lookup"><span data-stu-id="5d546-191">The functionality provided by Context can be divided into two parts: (1) the static part which is available in the whole C\# process, (2) the dynamic part which is only available for the specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="5d546-192">靜態部分</span><span class="sxs-lookup"><span data-stu-id="5d546-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="5d546-193">`Logger` 做為記錄用途。</span><span class="sxs-lookup"><span data-stu-id="5d546-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="5d546-194">`pluginType` 用來指出 C\# 程序的外掛程式類型。</span><span class="sxs-lookup"><span data-stu-id="5d546-194">`pluginType` is used to indicate the plugin type of the C\# process.</span></span> <span data-ttu-id="5d546-195">如果 C\# 程序在本機測試模式 (無 Java) 中執行，則外掛程式類型為 `SCP_NET_LOCAL`。</span><span class="sxs-lookup"><span data-stu-id="5d546-195">If the C\# process is run in local test mode (without Java), the plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="5d546-196">`Config` 可從 Java 端取得組態參數。</span><span class="sxs-lookup"><span data-stu-id="5d546-196">`Config` is provided to get configuration parameters from Java side.</span></span> <span data-ttu-id="5d546-197">C\# 外掛程式初始化時，Java 端會傳回參數。</span><span class="sxs-lookup"><span data-stu-id="5d546-197">The parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="5d546-198">`Config` 參數分成兩部分：`stormConf` 和 `pluginConf`。</span><span class="sxs-lookup"><span data-stu-id="5d546-198">The `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="5d546-199">`stormConf` 是由 Storm 定義的參數，`pluginConf` 是由 SCP 定義的參數。</span><span class="sxs-lookup"><span data-stu-id="5d546-199">`stormConf` is parameters defined by Storm and `pluginConf` is the parameters defined by SCP.</span></span> <span data-ttu-id="5d546-200">例如：</span><span class="sxs-lookup"><span data-stu-id="5d546-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="5d546-201">`TopologyContext` 可取得拓撲內容，這對多重平行處理的元件最實用。</span><span class="sxs-lookup"><span data-stu-id="5d546-201">`TopologyContext` is provided to get the topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="5d546-202">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="5d546-202">Here is an example:</span></span>

    //demo how to get TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a><span data-ttu-id="5d546-203">動態部分</span><span class="sxs-lookup"><span data-stu-id="5d546-203">Dynamic Part</span></span>
<span data-ttu-id="5d546-204">下列介面與特定的 Context 執行個體有關。</span><span class="sxs-lookup"><span data-stu-id="5d546-204">The following interfaces are pertinent to a certain Context instance.</span></span> <span data-ttu-id="5d546-205">Context 執行個體由 SCP.NET 平台建立，並傳給使用者程式碼：</span><span class="sxs-lookup"><span data-stu-id="5d546-205">The Context instance is created by SCP.NET platform and passed to the user code:</span></span>

    // Declare the Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple to default stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple to the specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="5d546-206">對於支援認可的非交易式 spout，已提供下列方法：</span><span class="sxs-lookup"><span data-stu-id="5d546-206">For non-transactional spout supporting ack, the following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="5d546-207">對於支援認可的非交易式 bolt，應該明確呼叫 `Ack()` 或 `Fail()` 來處理收到的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="5d546-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` the tuple it received.</span></span> <span data-ttu-id="5d546-208">發出新的 Tuple 時，也必須指定新 Tuple 的錨點。</span><span class="sxs-lookup"><span data-stu-id="5d546-208">And when emitting new tuple, it must also specify the anchors of the new tuple.</span></span> <span data-ttu-id="5d546-209">已提供下列方法。</span><span class="sxs-lookup"><span data-stu-id="5d546-209">The following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="5d546-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="5d546-210">StateStore</span></span>
<span data-ttu-id="5d546-211">`StateStore` 提供元資料服務、單調數列產生和免等待協調。</span><span class="sxs-lookup"><span data-stu-id="5d546-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="5d546-212">高階分散式並行抽象可根據 `StateStore`來建置，包括分散式鎖定、分散式佇列、屏障和交易服務。</span><span class="sxs-lookup"><span data-stu-id="5d546-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="5d546-213">SCP 應用程式可使用 `State` 物件將某些資訊保存在 ZooKeeper 中，特別是針對交易式拓撲。</span><span class="sxs-lookup"><span data-stu-id="5d546-213">SCP applications may use the `State` object to persist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="5d546-214">如此一來，如果交易式 spout 當機並重新啟動，就可從 ZooKeeper 擷取必要的資訊並重新啟動管線。</span><span class="sxs-lookup"><span data-stu-id="5d546-214">Doing so, if transactional spout crashes and restart, it can retrieve the necessary information from ZooKeeper and restart the pipeline.</span></span>

<span data-ttu-id="5d546-215">`StateStore` 物件主要有這些方法：</span><span class="sxs-lookup"><span data-stu-id="5d546-215">The `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method to retrieve a state store of the given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all the States in the StateStore
    /// </summary>
    /// <returns>All the States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all the committed states
    /// </summary>
    /// <returns>Registries contain the Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all the Aborted State in the StateStore
    /// </summary>
    /// <returns>Registries contain the Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of the State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="5d546-216">`State` 物件主要有這些方法：</span><span class="sxs-lookup"><span data-stu-id="5d546-216">The `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set the status of the state object to commit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set the status of the state object to abort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under the give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get the attribute value associated with the given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="5d546-217">在 `Commit()` 方法中，當 simpleMode 設為 true 時，就會直接在 ZooKeeper 中刪除對應的 ZNode。</span><span class="sxs-lookup"><span data-stu-id="5d546-217">For the `Commit()` method, when simpleMode is set to true, it will simply delete the corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="5d546-218">否則會刪除目前的 ZNode，並在 COMMITTED\_PATH 中加入新的節點。</span><span class="sxs-lookup"><span data-stu-id="5d546-218">Otherwise, it will delete the current ZNode, and adding a new node in the COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="5d546-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="5d546-219">SCPRuntime</span></span>
<span data-ttu-id="5d546-220">SCPRuntime 提供下列兩個方法。</span><span class="sxs-lookup"><span data-stu-id="5d546-220">SCPRuntime provides the following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="5d546-221">`Initialize()` 用來初始化 SCP 執行階段環境。</span><span class="sxs-lookup"><span data-stu-id="5d546-221">`Initialize()` is used to initialize the SCP runtime environment.</span></span> <span data-ttu-id="5d546-222">在此方法中，C\# 程序會連接到 Java 端，並取得組態參數和拓撲內容。</span><span class="sxs-lookup"><span data-stu-id="5d546-222">In this method, the C\# process will connect to the Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="5d546-223">`LaunchPlugin()` 用來啟動訊息處理迴圈。</span><span class="sxs-lookup"><span data-stu-id="5d546-223">`LaunchPlugin()` is used to kick off the message processing loop.</span></span> <span data-ttu-id="5d546-224">在此迴圈中，C\# 外掛程式會從 Java 端接收訊息 (包括 Tuple 和控制訊號)，然後處理訊息，也許會呼叫使用者程式碼提供的介面方法。</span><span class="sxs-lookup"><span data-stu-id="5d546-224">In this loop, the C\# plugin will receive messages form Java side (including tuples and control signals), and then process the messages, perhaps calling the interface method provide by the user code.</span></span> <span data-ttu-id="5d546-225">`LaunchPlugin()` 方法的輸入參數是委派，可傳回一個實作 ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt 介面的物件。</span><span class="sxs-lookup"><span data-stu-id="5d546-225">The input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="5d546-226">在 ISCPBatchBolt 中，我們可以從 `parms` 取得 `StormTxAttempt`，用以判斷是否為重播的嘗試。</span><span class="sxs-lookup"><span data-stu-id="5d546-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it to judge whether it is a replayed attempt.</span></span> <span data-ttu-id="5d546-227">這通常是在認可 bolt 上完成， `HelloWorldTx` 範例中會示範。</span><span class="sxs-lookup"><span data-stu-id="5d546-227">This is usually done at the commit bolt, and it is demonstrated in the `HelloWorldTx` example.</span></span>

<span data-ttu-id="5d546-228">一般而言，SCP 外掛程式可能在以下兩種模式中執行：</span><span class="sxs-lookup"><span data-stu-id="5d546-228">Generally speaking, the SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="5d546-229">本機測試模式：在此模式中，SCP 外掛程式 (C\# 使用者程式碼) 在開發階段是在 Visual Studio 內執行。</span><span class="sxs-lookup"><span data-stu-id="5d546-229">Local Test Mode: In this mode, the SCP plugins (the C\# user code) run inside Visual Studio during the development phase.</span></span> <span data-ttu-id="5d546-230">`LocalContext` ，它提供方法將發出的 Tuple 序列化到本機檔案，再讀回到記憶體中。</span><span class="sxs-lookup"><span data-stu-id="5d546-230">`LocalContext` can be used in this mode, which provides method to serialize the emitted tuples to local files, and read them back to memory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="5d546-231">標準模式：在此模式中，SCP 外掛程式由 storm java 程序啟動。</span><span class="sxs-lookup"><span data-stu-id="5d546-231">Regular Mode: In this mode, the SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="5d546-232">以下是啟動 SCP 外掛程式的範例：</span><span class="sxs-lookup"><span data-stu-id="5d546-232">Here is an example of launching SCP plugin:</span></span>
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting the environment variable here can change the log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="5d546-233">拓撲規格語言</span><span class="sxs-lookup"><span data-stu-id="5d546-233">Topology Specification Language</span></span>
<span data-ttu-id="5d546-234">SCP 拓撲規格是特定領域的語言，用來描述和設定 SCP 拓撲。</span><span class="sxs-lookup"><span data-stu-id="5d546-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="5d546-235">它以 Storm 的 Clojure DSL 為基礎 (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>)，而由 SCP 擴充。</span><span class="sxs-lookup"><span data-stu-id="5d546-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="5d546-236">拓撲規格可透過 ***runspec*** 命令直接提交給 storm 叢集來執行。</span><span class="sxs-lookup"><span data-stu-id="5d546-236">Topology specifications can be submitted directly to storm cluster for execution via the ***runspec*** command.</span></span>

<span data-ttu-id="5d546-237">SCP.NET 已增加下列函數來定義交易式拓撲：</span><span class="sxs-lookup"><span data-stu-id="5d546-237">SCP.NET has add follow functions to define the Transactional Topology:</span></span>

| <span data-ttu-id="5d546-238">**新函數**</span><span class="sxs-lookup"><span data-stu-id="5d546-238">**New Functions**</span></span> | <span data-ttu-id="5d546-239">**參數**</span><span class="sxs-lookup"><span data-stu-id="5d546-239">**Parameters**</span></span> | <span data-ttu-id="5d546-240">**說明**</span><span class="sxs-lookup"><span data-stu-id="5d546-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5d546-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="5d546-241">**tx-topolopy**</span></span> |<span data-ttu-id="5d546-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="5d546-242">topology-name</span></span><br /><span data-ttu-id="5d546-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="5d546-243">spout-map</span></span><br /><span data-ttu-id="5d546-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="5d546-244">bolt-map</span></span> |<span data-ttu-id="5d546-245">以拓撲名稱、&nbsp;spout 定義對應和 bolt 定義對應來定義交易式拓撲</span><span class="sxs-lookup"><span data-stu-id="5d546-245">Define a transactional topology with the topology name, &nbsp;spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="5d546-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="5d546-246">**scp-tx-spout**</span></span> |<span data-ttu-id="5d546-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="5d546-247">exec-name</span></span><br /><span data-ttu-id="5d546-248">args</span><span class="sxs-lookup"><span data-stu-id="5d546-248">args</span></span><br /><span data-ttu-id="5d546-249">fields</span><span class="sxs-lookup"><span data-stu-id="5d546-249">fields</span></span> |<span data-ttu-id="5d546-250">定義交易式 spout。</span><span class="sxs-lookup"><span data-stu-id="5d546-250">Define a transactional spout.</span></span> <span data-ttu-id="5d546-251">它會使用 ***args*** 搭配 ***exec-name*** 來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d546-251">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="5d546-252">***fields*** 是 spout 的輸出欄位</span><span class="sxs-lookup"><span data-stu-id="5d546-252">The ***fields*** is the Output Fields for spout</span></span> |
| <span data-ttu-id="5d546-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="5d546-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="5d546-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="5d546-254">exec-name</span></span><br /><span data-ttu-id="5d546-255">args</span><span class="sxs-lookup"><span data-stu-id="5d546-255">args</span></span><br /><span data-ttu-id="5d546-256">fields</span><span class="sxs-lookup"><span data-stu-id="5d546-256">fields</span></span> |<span data-ttu-id="5d546-257">定義交易式批次 Bolt。</span><span class="sxs-lookup"><span data-stu-id="5d546-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="5d546-258">它會使用 ***args*** 搭配 ***exec-name*** 來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d546-258">It will run the application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="5d546-259">fields 是 bolt 的輸出欄位。</span><span class="sxs-lookup"><span data-stu-id="5d546-259">The Fields is the Output Fields for bolt.</span></span> |
| <span data-ttu-id="5d546-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="5d546-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="5d546-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="5d546-261">exec-name</span></span><br /><span data-ttu-id="5d546-262">args</span><span class="sxs-lookup"><span data-stu-id="5d546-262">args</span></span><br /><span data-ttu-id="5d546-263">fields</span><span class="sxs-lookup"><span data-stu-id="5d546-263">fields</span></span> |<span data-ttu-id="5d546-264">定義交易式認可者 Bolt。</span><span class="sxs-lookup"><span data-stu-id="5d546-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="5d546-265">它會使用 ***args*** 搭配 ***exec-name*** 來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d546-265">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="5d546-266">***fields*** 是 bolt 的輸出欄位</span><span class="sxs-lookup"><span data-stu-id="5d546-266">The ***fields*** is the Output Fields for bolt</span></span> |
| <span data-ttu-id="5d546-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="5d546-267">**nontx-topolopy**</span></span> |<span data-ttu-id="5d546-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="5d546-268">topology-name</span></span><br /><span data-ttu-id="5d546-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="5d546-269">spout-map</span></span><br /><span data-ttu-id="5d546-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="5d546-270">bolt-map</span></span> |<span data-ttu-id="5d546-271">以拓撲名稱、&nbsp;spout 定義對應和 bolt 定義對應來定義非交易式拓撲</span><span class="sxs-lookup"><span data-stu-id="5d546-271">Define a nontransactional topology with the topology name,&nbsp; spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="5d546-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="5d546-272">**scp-spout**</span></span> |<span data-ttu-id="5d546-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="5d546-273">exec-name</span></span><br /><span data-ttu-id="5d546-274">args</span><span class="sxs-lookup"><span data-stu-id="5d546-274">args</span></span><br /><span data-ttu-id="5d546-275">fields</span><span class="sxs-lookup"><span data-stu-id="5d546-275">fields</span></span><br /><span data-ttu-id="5d546-276">參數</span><span class="sxs-lookup"><span data-stu-id="5d546-276">parameters</span></span> |<span data-ttu-id="5d546-277">定義非交易式 spout。</span><span class="sxs-lookup"><span data-stu-id="5d546-277">Define a nontransactional spout.</span></span> <span data-ttu-id="5d546-278">它會使用 ***args*** 搭配 ***exec-name*** 來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d546-278">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="5d546-279">***fields*** 是 spout 的輸出欄位</span><span class="sxs-lookup"><span data-stu-id="5d546-279">The ***fields*** is the Output Fields for spout</span></span><br /><br /><span data-ttu-id="5d546-280">***parameters*** 為選用，使用它來指定一些參數，例如 "nontransactional.ack.enabled"。</span><span class="sxs-lookup"><span data-stu-id="5d546-280">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="5d546-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="5d546-281">**scp-bolt**</span></span> |<span data-ttu-id="5d546-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="5d546-282">exec-name</span></span><br /><span data-ttu-id="5d546-283">args</span><span class="sxs-lookup"><span data-stu-id="5d546-283">args</span></span><br /><span data-ttu-id="5d546-284">fields</span><span class="sxs-lookup"><span data-stu-id="5d546-284">fields</span></span><br /><span data-ttu-id="5d546-285">參數</span><span class="sxs-lookup"><span data-stu-id="5d546-285">parameters</span></span> |<span data-ttu-id="5d546-286">定義非交易式 Bolt。</span><span class="sxs-lookup"><span data-stu-id="5d546-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="5d546-287">它會使用 ***args*** 搭配 ***exec-name*** 來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d546-287">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="5d546-288">***fields*** 是 bolt 的輸出欄位</span><span class="sxs-lookup"><span data-stu-id="5d546-288">The ***fields*** is the Output Fields for bolt</span></span><br /><br /><span data-ttu-id="5d546-289">***parameters*** 為選用，使用它來指定一些參數，例如 "nontransactional.ack.enabled"。</span><span class="sxs-lookup"><span data-stu-id="5d546-289">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="5d546-290">SCP.NET 定義下列關鍵字：</span><span class="sxs-lookup"><span data-stu-id="5d546-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="5d546-291">**關鍵字**</span><span class="sxs-lookup"><span data-stu-id="5d546-291">**Key Words**</span></span> | <span data-ttu-id="5d546-292">**說明**</span><span class="sxs-lookup"><span data-stu-id="5d546-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="5d546-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="5d546-293">**:name**</span></span> |<span data-ttu-id="5d546-294">定義拓撲名稱</span><span class="sxs-lookup"><span data-stu-id="5d546-294">Define the Topology Name</span></span> |
| <span data-ttu-id="5d546-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="5d546-295">**:topology**</span></span> |<span data-ttu-id="5d546-296">使用上述函數和內建函數來定義拓撲。</span><span class="sxs-lookup"><span data-stu-id="5d546-296">Define the Topology using the above functions and build in ones.</span></span> |
| <span data-ttu-id="5d546-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="5d546-297">**:p**</span></span> |<span data-ttu-id="5d546-298">為每個 spout 或 bolt 定義平行處理提示。</span><span class="sxs-lookup"><span data-stu-id="5d546-298">Define the parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="5d546-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="5d546-299">**:config**</span></span> |<span data-ttu-id="5d546-300">定義設定參數或更新現有的設定參數</span><span class="sxs-lookup"><span data-stu-id="5d546-300">Define configure parameter or update the existing ones</span></span> |
| <span data-ttu-id="5d546-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="5d546-301">**:schema**</span></span> |<span data-ttu-id="5d546-302">定義串流的結構描述。</span><span class="sxs-lookup"><span data-stu-id="5d546-302">Define the Schema of Stream.</span></span> |

<span data-ttu-id="5d546-303">還有常用參數：</span><span class="sxs-lookup"><span data-stu-id="5d546-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="5d546-304">**參數**</span><span class="sxs-lookup"><span data-stu-id="5d546-304">**Parameter**</span></span> | <span data-ttu-id="5d546-305">**說明**</span><span class="sxs-lookup"><span data-stu-id="5d546-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="5d546-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="5d546-306">**"plugin.name"**</span></span> |<span data-ttu-id="5d546-307">C# 外掛程式的 exe 檔名</span><span class="sxs-lookup"><span data-stu-id="5d546-307">exe file name of the C# plugin</span></span> |
| <span data-ttu-id="5d546-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="5d546-308">**"plugin.args"**</span></span> |<span data-ttu-id="5d546-309">外掛程式引數</span><span class="sxs-lookup"><span data-stu-id="5d546-309">plugin args</span></span> |
| <span data-ttu-id="5d546-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="5d546-310">**"output.schema"**</span></span> |<span data-ttu-id="5d546-311">輸出結構描述</span><span class="sxs-lookup"><span data-stu-id="5d546-311">Output schema</span></span> |
| <span data-ttu-id="5d546-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="5d546-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="5d546-313">非交易式拓撲是否啟用認可</span><span class="sxs-lookup"><span data-stu-id="5d546-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="5d546-314">runspec 命令會隨著程式碼一起部署，用法如下：</span><span class="sxs-lookup"><span data-stu-id="5d546-314">The runspec command will be deployed together with the bits, the usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="5d546-315">***resource-dir*** 參數是選擇性，想要插入 C\# 應用程式時需要指定它，此目錄將包含應用程式、依存性和組態。</span><span class="sxs-lookup"><span data-stu-id="5d546-315">The ***resource-dir*** parameter is optional, you need to specify it when you want to plug a C\# application, and this directory will contain the application, the dependencies and configurations.</span></span>

<span data-ttu-id="5d546-316">***classpath*** 參數也是選擇性。</span><span class="sxs-lookup"><span data-stu-id="5d546-316">The ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="5d546-317">用來指定 Java 類別路徑 (如果規格檔包含 Java Spout 或 Bolt)。</span><span class="sxs-lookup"><span data-stu-id="5d546-317">It is used to specify the Java classpath if the spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="5d546-318">其他功能</span><span class="sxs-lookup"><span data-stu-id="5d546-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="5d546-319">輸入和輸出結構描述宣告</span><span class="sxs-lookup"><span data-stu-id="5d546-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="5d546-320">使用者可以在 C\# 程序中發出 Tuple，平台必須將 Tuple 序列化為 byte，並傳送至 Java 端，Storm 會將此 Tuple 傳送至目標。</span><span class="sxs-lookup"><span data-stu-id="5d546-320">The user can emit tuple in C\# process, the platform needs to serialize the tuple into byte[], transfer to Java side, and Storm will transfer this tuple to the targets.</span></span> <span data-ttu-id="5d546-321">同時，在下游元件中，C\# 程序會接收 java 端傳回的 Tuple，由平台將它轉換成原始類型，而所有這些操作都由平台在幕後進行。</span><span class="sxs-lookup"><span data-stu-id="5d546-321">Meanwhile in downstream component, the C\# process will receive tuple back from java side, and convert it to the original types by platform, all these operations are hidden by the Platform.</span></span>

<span data-ttu-id="5d546-322">為了支援序列化和還原序列化，使用者程式碼需要宣告輸入和輸出的結構描述。</span><span class="sxs-lookup"><span data-stu-id="5d546-322">To support the serialization and deserialization, user code needs to declare the schema of the inputs and outputs.</span></span>

<span data-ttu-id="5d546-323">輸入/輸出串流結構描述定義為字典，索引鍵是 StreamId，值為資料行的類型。</span><span class="sxs-lookup"><span data-stu-id="5d546-323">The input/output stream schema is defined as a dictionary, the key is the StreamId and the value is the Types of the columns.</span></span> <span data-ttu-id="5d546-324">元件可以宣告多重串流。</span><span class="sxs-lookup"><span data-stu-id="5d546-324">The component can have multi-streams declared.</span></span>

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


<span data-ttu-id="5d546-325">在 Context 物件中，我們增加下列 API：</span><span class="sxs-lookup"><span data-stu-id="5d546-325">In Context object, we have the following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="5d546-326">使用者程式碼必須確定發出的 Tuple 遵守該串流所定義的結構描述，否則系統會擲回執行階段例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5d546-326">User code must make sure the tuples emitted obey the schema defined for that stream, or the system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="5d546-327">多重串流支援</span><span class="sxs-lookup"><span data-stu-id="5d546-327">Multi-Stream Support</span></span>
<span data-ttu-id="5d546-328">SCP 支援使用者程式碼同時發出或接收多個不同串流。</span><span class="sxs-lookup"><span data-stu-id="5d546-328">SCP supports user code to emit or receive from multiple distinct streams at the same time.</span></span> <span data-ttu-id="5d546-329">此支援反映在 Context 物件中，因為 Emit 方法接受一個選擇性串流 ID 參數。</span><span class="sxs-lookup"><span data-stu-id="5d546-329">The support reflects in the Context object as the Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="5d546-330">SCP.NET Context 物件中已增加兩個方法。</span><span class="sxs-lookup"><span data-stu-id="5d546-330">Two methods in the SCP.NET Context object have been added.</span></span> <span data-ttu-id="5d546-331">用以發出一或多個 Tuple 來指定 StreamId。</span><span class="sxs-lookup"><span data-stu-id="5d546-331">They are used to emit Tuple or Tuples to specify StreamId.</span></span> <span data-ttu-id="5d546-332">StreamId 是字串，在 C\# 與拓撲定義規格中必須一致。</span><span class="sxs-lookup"><span data-stu-id="5d546-332">The StreamId is a string and it needs to be consistent in both C\# and the Topology Definition Spec.</span></span>

        /* Emit tuple to the specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="5d546-333">發出給不存在的串流會造成執行階段例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5d546-333">The emitting to a non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="5d546-334">欄位分組</span><span class="sxs-lookup"><span data-stu-id="5d546-334">Fields Grouping</span></span>
<span data-ttu-id="5d546-335">Strom 中內建的欄位群組功能在 SCP.NET 中無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="5d546-335">The build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="5d546-336">在 Java Proxy 端，所有欄位資料類型實際上為 byte[]，而欄位群組會使用 byte[] 物件雜湊碼來執行群組。</span><span class="sxs-lookup"><span data-stu-id="5d546-336">On the Java Proxy side, all the fields data types are actually byte[], and the fields grouping uses the byte[] object hash code to perform the grouping.</span></span> <span data-ttu-id="5d546-337">byte[] 物件雜湊碼是此物件在記憶體中的位址。</span><span class="sxs-lookup"><span data-stu-id="5d546-337">The byte[] object hash code is the address of this object in memory.</span></span> <span data-ttu-id="5d546-338">因此，共用相同內容但不是相同位址的兩個 byte[] 物件，分組會錯誤。</span><span class="sxs-lookup"><span data-stu-id="5d546-338">So the grouping will be wrong for two byte[] objects that share the same content but not the same address.</span></span>

<span data-ttu-id="5d546-339">SCP.NET 增加一個自訂的分組方法，它會使用 byte[] 的內容來執行分組。</span><span class="sxs-lookup"><span data-stu-id="5d546-339">SCP.NET adds a customized grouping method, and it will use the content of the byte[] to do the grouping.</span></span> <span data-ttu-id="5d546-340">在 **SPEC** 檔案中，語法如下：</span><span class="sxs-lookup"><span data-stu-id="5d546-340">In **SPEC** file, the syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="5d546-341">在這裡，</span><span class="sxs-lookup"><span data-stu-id="5d546-341">Here,</span></span>

1. <span data-ttu-id="5d546-342">“scp-field-group” 表示「SCP 實作的自訂欄位分組」。</span><span class="sxs-lookup"><span data-stu-id="5d546-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="5d546-343">“:tx” 或 “:non-tx” 表示是否為交易式拓撲。</span><span class="sxs-lookup"><span data-stu-id="5d546-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="5d546-344">我們需要此資訊，因為 tx 和非 tx 拓撲中的起始索引不同。</span><span class="sxs-lookup"><span data-stu-id="5d546-344">We need this information since the starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="5d546-345">[0,1] 表示欄位 Id 的雜湊集，從 0 開始。</span><span class="sxs-lookup"><span data-stu-id="5d546-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="5d546-346">混合式拓撲</span><span class="sxs-lookup"><span data-stu-id="5d546-346">Hybrid topology</span></span>
<span data-ttu-id="5d546-347">原生 Storm 是以 Java 撰寫。</span><span class="sxs-lookup"><span data-stu-id="5d546-347">The native Storm is written in Java.</span></span> <span data-ttu-id="5d546-348">且 SCP.Net 已經加以增強，讓我們的客戶可以撰寫 C\# 程式碼來處理其商業邏輯。</span><span class="sxs-lookup"><span data-stu-id="5d546-348">And SCP.Net has enhanced it to enable our customs to write C\# code to handle their business logic.</span></span> <span data-ttu-id="5d546-349">但我們也支援混合式拓撲，不僅包含 C\# spout/bolt，也包含 Java Spout/Bolt。</span><span class="sxs-lookup"><span data-stu-id="5d546-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="5d546-350">在規格檔中指定 Java Spout/Bolt</span><span class="sxs-lookup"><span data-stu-id="5d546-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="5d546-351">在規格檔中，"scp-spout" 和 "scp-bolt" 也可用來指定 Java Spout 和 Bolt，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="5d546-351">In spec file, "scp-spout" and "scp-bolt" can also be used to specify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="5d546-352">其中 `microsoft.scp.example.HybridTopology.Generator` 是 Java Spout 類別的名稱。</span><span class="sxs-lookup"><span data-stu-id="5d546-352">Here `microsoft.scp.example.HybridTopology.Generator` is the name of the Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="5d546-353">在 runSpec 命令中指定 Java 類別路徑</span><span class="sxs-lookup"><span data-stu-id="5d546-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="5d546-354">如果您要提交包含 Java Spout 或 Bolt 的拓撲，則必須先編譯 Java Spout 或 Bolt 並取得 Jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="5d546-354">If you want to submit topology containing Java Spouts or Bolts, you need to first compile the Java Spouts or Bolts and get the Jar files.</span></span> <span data-ttu-id="5d546-355">然後，在提交拓撲時，應該指定包含這些 Jar 檔案的 java 類別路徑。</span><span class="sxs-lookup"><span data-stu-id="5d546-355">Then you should specify the java classpath that contains the Jar files when submitting topology.</span></span> <span data-ttu-id="5d546-356">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="5d546-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="5d546-357">在這裡，**examples\\HybridTopology\\java\\target\\** 是包含 Java Spout/Bolt Jar 檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5d546-357">Here **examples\\HybridTopology\\java\\target\\** is the folder containing the Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="5d546-358">Java 與 C\ 之間的序列化和還原序列化</span><span class="sxs-lookup"><span data-stu-id="5d546-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="5d546-359">我們的 SCP 元件包含 Java 和 C\# 端。</span><span class="sxs-lookup"><span data-stu-id="5d546-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="5d546-360">為了與原生 Java Spout/Bolt 互動，必須在 Java 和 C\# 端之間進行序列化/還原序列化，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="5d546-360">In order to interact with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in the following graph.</span></span>

![Java 元件傳送至 SCP 元件再傳送至 Java 元件的圖](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="5d546-362">**Java 端序列化和 C\# 端還原序列化**</span><span class="sxs-lookup"><span data-stu-id="5d546-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="5d546-363">首次，我們提供 Java 端序列化和 C\# 端還原序列化的預設實作。</span><span class="sxs-lookup"><span data-stu-id="5d546-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="5d546-364">Java 端的序列化方法可以在 SPEC 檔案中指定：</span><span class="sxs-lookup"><span data-stu-id="5d546-364">The serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="5d546-365">C\# 端的還原序列化方法應該在 C\# 使用者程式碼中指定：</span><span class="sxs-lookup"><span data-stu-id="5d546-365">The deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="5d546-366">只要資料類型不要太複雜，此預設實作應該能夠因應大多數的情況。</span><span class="sxs-lookup"><span data-stu-id="5d546-366">This default implementation should handle most cases if the data type is not too complex.</span></span> <span data-ttu-id="5d546-367">在某些情況下，由於使用者資料類型太複雜，或因為預設實作的效能不符合使用者的需求，使用者可以插入自己的實作。</span><span class="sxs-lookup"><span data-stu-id="5d546-367">For certain cases, either because the user data type is too complex, or because the performance of our default implementation does not meet the user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="5d546-368">Java 端的序列化介面定義為：</span><span class="sxs-lookup"><span data-stu-id="5d546-368">The serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="5d546-369">C\# 端的還原序列化介面定義為：</span><span class="sxs-lookup"><span data-stu-id="5d546-369">The deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="5d546-370">公用介面 ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="5d546-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="5d546-371">**C\# 端序列化和 Java 端還原序列化**</span><span class="sxs-lookup"><span data-stu-id="5d546-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="5d546-372">應該在 C\# 使用者程式碼中指定 C\# 端的還原序列化方法：</span><span class="sxs-lookup"><span data-stu-id="5d546-372">The serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="5d546-373">應該在 SPEC 檔案中指定 Java 端的還原序列化方法：</span><span class="sxs-lookup"><span data-stu-id="5d546-373">The Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="5d546-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="5d546-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="5d546-375">其中 "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" 是 Deserializer (還原序列化程式) 的名稱，"microsoft.scp.example.HybridTopology.Person" 是資料還原序列化的目標類別。</span><span class="sxs-lookup"><span data-stu-id="5d546-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is the name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is the target class the data is deserialized to.</span></span>
   
   <span data-ttu-id="5d546-376">使用者也可以外掛其自己實作的 C\# 序列化程式和 Java Deserializer。</span><span class="sxs-lookup"><span data-stu-id="5d546-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="5d546-377">這是 C\# 序列化程式的介面︰</span><span class="sxs-lookup"><span data-stu-id="5d546-377">This is the interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="5d546-378">這是 Java Deserializer 的介面︰</span><span class="sxs-lookup"><span data-stu-id="5d546-378">This is the interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="5d546-379">SCP 主機模式</span><span class="sxs-lookup"><span data-stu-id="5d546-379">SCP Host Mode</span></span>
<span data-ttu-id="5d546-380">在此模式中，使用者可以將程式碼編譯成 DLL，並使用 SCP 提供的 SCPHost.exe 來提交拓撲。</span><span class="sxs-lookup"><span data-stu-id="5d546-380">In this mode, user can compile their codes to DLL, and use SCPHost.exe provided by SCP to submit topology.</span></span> <span data-ttu-id="5d546-381">規格檔如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d546-381">The spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="5d546-382">其中，`plugin.name` 指定為 SCP SDK 所提供的 `SCPHost.exe`。</span><span class="sxs-lookup"><span data-stu-id="5d546-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="5d546-383">SCPHost.exe 只接受三個參數：</span><span class="sxs-lookup"><span data-stu-id="5d546-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="5d546-384">第一個是 DLL 名稱，在此範例中為 `"HelloWorld.dll"` 。</span><span class="sxs-lookup"><span data-stu-id="5d546-384">The first one is the DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="5d546-385">第二個是類別名稱，在此範例中為 `"Scp.App.HelloWorld.Generator"` 。</span><span class="sxs-lookup"><span data-stu-id="5d546-385">The second one is the Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="5d546-386">第三個是 public static 方法的名稱，可叫用來取得 ISCPPlugin 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="5d546-386">The third one is the name of a public static method, which can be invoked to get an instance of ISCPPlugin.</span></span>

<span data-ttu-id="5d546-387">在主機模式中，使用者程式碼會編譯成 DLL，供 SCP 平台叫用。</span><span class="sxs-lookup"><span data-stu-id="5d546-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="5d546-388">SCP 平台可以完全掌控整個處理邏輯。</span><span class="sxs-lookup"><span data-stu-id="5d546-388">So SCP platform can get full control of the whole processing logic.</span></span> <span data-ttu-id="5d546-389">因此，建議客戶在 SCP 主機模式中提交拓撲，因為這樣可以簡化開發過程，讓我們有更大的彈性，在後續版本中也能有更高的回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="5d546-389">So we recommend our customers to submit topology in SCP host mode since it can simplify the development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="5d546-390">SCP 程式設計範例</span><span class="sxs-lookup"><span data-stu-id="5d546-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="5d546-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="5d546-391">HelloWorld</span></span>
<span data-ttu-id="5d546-392">**HelloWorld** 是一個體驗 SCP.Net 的極簡單範例。</span><span class="sxs-lookup"><span data-stu-id="5d546-392">**HelloWorld** is a very simple example to show a taste of SCP.Net.</span></span> <span data-ttu-id="5d546-393">它使用非交易拓撲，具有一個名為 **generator** 的 spout，以及名為 **splitter** 和 **counter** 的兩個 bolt。</span><span class="sxs-lookup"><span data-stu-id="5d546-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="5d546-394">spout **generator** 會隨機產生一些句子，並發出這些句子給 **splitter**。</span><span class="sxs-lookup"><span data-stu-id="5d546-394">The spout **generator** will randomly generate some sentences, and emit these sentences to **splitter**.</span></span> <span data-ttu-id="5d546-395">bolt **splitter** 會將這些句子分割成單字，再發出這些單字給 **counter** bolt。</span><span class="sxs-lookup"><span data-stu-id="5d546-395">The bolt **splitter** will split the sentences to words and emit these words to **counter** bolt.</span></span> <span data-ttu-id="5d546-396">bolt "counter" 使用字典來記錄每個單字出現的次數。</span><span class="sxs-lookup"><span data-stu-id="5d546-396">The bolt "counter" uses a dictionary to record the occurrence number of each word.</span></span>

<span data-ttu-id="5d546-397">此範例有兩個規格檔：**HelloWorld.spec** 和 **HelloWorld\_EnableAck.spec**。</span><span class="sxs-lookup"><span data-stu-id="5d546-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="5d546-398">在 C\# 程式碼中，可從 Java 端取得 pluginConf 來檢查認可是否已啟用。</span><span class="sxs-lookup"><span data-stu-id="5d546-398">In the C\# code, it can find out whether ack is enabled by getting the pluginConf from Java side.</span></span>

    /* demo how to get pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="5d546-399">在 spout 中，如果認可已啟用，則會使用字典來快取尚未認可的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="5d546-399">In the spout, if ack is enabled, a dictionary is used to cache the tuples that have not been acked.</span></span> <span data-ttu-id="5d546-400">如果呼叫 Fail()，則會重播失敗的 Tuple：</span><span class="sxs-lookup"><span data-stu-id="5d546-400">If Fail() is called, the failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get the cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay the failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="5d546-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="5d546-401">HelloWorldTx</span></span>
<span data-ttu-id="5d546-402">**HelloWorldTx** 範例示範如何實作交易式拓撲。</span><span class="sxs-lookup"><span data-stu-id="5d546-402">The **HelloWorldTx** example demonstrates how to implement transactional topology.</span></span> <span data-ttu-id="5d546-403">它有一個名為 **generator** 的 spout，一個名為 **partial-count** 的批次 bolt，以及一個名為 **count-sum** 的認可 bolt。</span><span class="sxs-lookup"><span data-stu-id="5d546-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="5d546-404">另外還有三個預先建立的 txt 檔案︰**DataSource0.txt**、**DataSource1.txt**、**DataSource2.txt**。</span><span class="sxs-lookup"><span data-stu-id="5d546-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="5d546-405">在每個交易中，**generator** spout 會從預先建立的三個檔案中隨機選擇兩個檔案，然後發出這兩個檔名給 **partial-count** bolt。</span><span class="sxs-lookup"><span data-stu-id="5d546-405">In each transaction, the spout **generator** will randomly choose two files from the pre-created three files, and emit the two file names to the **partial-count** bolt.</span></span> <span data-ttu-id="5d546-406">**partial-count** bolt 會先從收到的 Tuple 中取得檔名，然後開啟檔案並計算此檔案中的字數，最後再發出字數給 **count-sum** bolt。</span><span class="sxs-lookup"><span data-stu-id="5d546-406">The bolt **partial-count** will first get the file name from the received tuple, then open the file and count the number of words in this file, and finally emit the word number to the **count-sum** bolt.</span></span> <span data-ttu-id="5d546-407">**count-sum** bolt 將計算總數。</span><span class="sxs-lookup"><span data-stu-id="5d546-407">The **count-sum** bolt will summarize the total count.</span></span>

<span data-ttu-id="5d546-408">為了符合**剛好一次**語意，認可 bolt **count-sum** 需要判斷它是否為重播的交易。</span><span class="sxs-lookup"><span data-stu-id="5d546-408">To achieve **exactly once** semantics, the commit bolt **count-sum** need to judge whether it is a replayed transaction.</span></span> <span data-ttu-id="5d546-409">在此範例中，它有一個靜態成員變數：</span><span class="sxs-lookup"><span data-stu-id="5d546-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="5d546-410">建立 ISCPBatchBolt 執行個體時，它會從輸入參數中取得 `txAttempt`：</span><span class="sxs-lookup"><span data-stu-id="5d546-410">When an ISCPBatchBolt instance is created, it will get the `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from the input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

<span data-ttu-id="5d546-411">呼叫 `FinishBatch()` 時，將會更新 `lastCommittedTxId` (如果不是重播的交易)。</span><span class="sxs-lookup"><span data-stu-id="5d546-411">When `FinishBatch()` is called, the `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update the toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="5d546-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="5d546-412">HybridTopology</span></span>
<span data-ttu-id="5d546-413">此拓撲包含 Java Spout 和 C\# Bolt。</span><span class="sxs-lookup"><span data-stu-id="5d546-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="5d546-414">它採用 SCP 平台提供的預設序列化和還原序列化實作。</span><span class="sxs-lookup"><span data-stu-id="5d546-414">It uses the default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="5d546-415">請查閱 **examples\\HybridTopology** 資料夾中的 **HybridTopology.spec**，以取得規格檔詳細資料，並查看 **SubmitTopology.bat** 了解如何指定 Java 類別路徑。</span><span class="sxs-lookup"><span data-stu-id="5d546-415">Please ref the **HybridTopology.spec** in **examples\\HybridTopology** folder for the spec file details, and **SubmitTopology.bat** for how to specify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="5d546-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="5d546-416">SCPHostDemo</span></span>
<span data-ttu-id="5d546-417">此範例在本質上與 HelloWorld 相同。</span><span class="sxs-lookup"><span data-stu-id="5d546-417">This example is the same as HelloWorld in essence.</span></span> <span data-ttu-id="5d546-418">唯一的差別在於使用者程式碼是編譯成 DLL，且使用 SCPHost.exe 提交拓撲。</span><span class="sxs-lookup"><span data-stu-id="5d546-418">The only difference is that the user code is compiled as DLL and the topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="5d546-419">如需詳細說明，請參閱＜SCP 主機模式＞一節。</span><span class="sxs-lookup"><span data-stu-id="5d546-419">Please ref the section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d546-420">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d546-420">Next Steps</span></span>
<span data-ttu-id="5d546-421">有關使用 SCP 建立之 Storm 拓撲的詳細資訊，請參閱下列各文︰</span><span class="sxs-lookup"><span data-stu-id="5d546-421">For examples of Storm topologies created using SCP, see the following:</span></span>

* [<span data-ttu-id="5d546-422">使用 Visual Studio 開發 Apache Storm on HDInsight 的 C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="5d546-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="5d546-423">利用 Storm on HDInsight 處理 Azure 事件中心的事件</span><span class="sxs-lookup"><span data-stu-id="5d546-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="5d546-424">在 C# Storm 拓樸中建立多個資料流</span><span class="sxs-lookup"><span data-stu-id="5d546-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="5d546-425">使用 Power BI 視覺化 Storm 拓撲的資料</span><span class="sxs-lookup"><span data-stu-id="5d546-425">Use Power Bi to visualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="5d546-426">使用 Storm on HDInsight 處理事件中心的車輛感應器資料</span><span class="sxs-lookup"><span data-stu-id="5d546-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="5d546-427">從 Azure 事件中樞擷取、轉換及載入 (ETL) 至 HBase</span><span class="sxs-lookup"><span data-stu-id="5d546-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="5d546-428">在 HDInsight 上使用 Storm 和 HBase 讓事件相互關聯</span><span class="sxs-lookup"><span data-stu-id="5d546-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)


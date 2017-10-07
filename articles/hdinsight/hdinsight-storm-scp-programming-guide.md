---
title: "aaaSCP.NET 程式設計指南 |Microsoft 文件"
description: "深入了解如何 toouse SCP.NET toocreate。以網路為基礎的 Storm 拓撲使用 HDInsight 上出現。"
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
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="facb0-103">SCP 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="facb0-103">SCP programming guide</span></span>
<span data-ttu-id="facb0-104">SCP 是平台 toobuild 即時、 可靠、 一致和高效能資料處理應用程式。</span><span class="sxs-lookup"><span data-stu-id="facb0-104">SCP is a platform toobuild real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="facb0-105">它最上層的內建[Apache Storm](http://storm.incubator.apache.org/) -處理 hello OSS 社群所設計的系統資料流。</span><span class="sxs-lookup"><span data-stu-id="facb0-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by hello OSS communities.</span></span> <span data-ttu-id="facb0-106">Storm 由 Nathan Marz 所設計，由 Twitter 公開原始碼。</span><span class="sxs-lookup"><span data-stu-id="facb0-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="facb0-107">它會運用[Apache 動物園管理員](http://zookeeper.apache.org/)，另一個 Apache 專案 tooenable 可靠的分散式的協調和狀態管理。</span><span class="sxs-lookup"><span data-stu-id="facb0-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project tooenable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="facb0-108">Hello SCP 專案移植 Windows 上的出現不僅 hello 專案也加入擴充功能和自訂 hello Windows 生態系統。</span><span class="sxs-lookup"><span data-stu-id="facb0-108">Not only hello SCP project ported Storm on Windows but also hello project added extensions and customization for hello Windows ecosystem.</span></span> <span data-ttu-id="facb0-109">hello 擴充功能包括.NET 開發人員體驗和程式庫、 hello 自訂包括 Windows 為基礎的部署。</span><span class="sxs-lookup"><span data-stu-id="facb0-109">hello extensions include .NET developer experience, and libraries, hello customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="facb0-110">hello 擴充和自訂完成的方式，我們不需要 toofork hello OSS 專案，而且我們可能會利用衍生之上 Storm 的生態系統。</span><span class="sxs-lookup"><span data-stu-id="facb0-110">hello extension and customization is done in such a way that we do not need toofork hello OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="facb0-111">處理模型</span><span class="sxs-lookup"><span data-stu-id="facb0-111">Processing model</span></span>
<span data-ttu-id="facb0-112">hello SCP 中的資料會模型化為連續資料流的 tuple。</span><span class="sxs-lookup"><span data-stu-id="facb0-112">hello data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="facb0-113">通常 hello tuple 流入某些佇列第一次，然後挑選，以及裝載於 Storm 拓撲的商務邏輯所轉換，最後 hello 輸出無法使用管線傳送 tuple tooanother SCP 系統，或者是認可的 toostores 喜歡分散式的檔案系統或資料庫，例如 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="facb0-113">Typically hello tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally hello output could be piped as tuples tooanother SCP system, or be committed toostores like distributed file system or databases like SQL Server.</span></span>

![填入資料 tooprocessing，摘要的資料存放區的佇列的圖表](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="facb0-115">在 Storm 中，應用程式拓撲定義一份運算圖。</span><span class="sxs-lookup"><span data-stu-id="facb0-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="facb0-116">拓撲中的每個節點包含處理邏輯，節點之間的連結代表資料流程。</span><span class="sxs-lookup"><span data-stu-id="facb0-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="facb0-117">hello 節點 tooinject 輸入的資料到 hello 拓撲稱為 Spouts，可以是使用的 toosequence hello 資料。</span><span class="sxs-lookup"><span data-stu-id="facb0-117">hello nodes tooinject input data into hello topology are called Spouts, which can be used toosequence hello data.</span></span> <span data-ttu-id="facb0-118">hello 輸入的資料可能位於檔案記錄檔、 交易式資料庫、 系統效能計數器等等。 使用這兩個輸入和輸出資料流的 hello 節點稱為攻擊，請勿 hello 實際資料的篩選和項目，並彙總。</span><span class="sxs-lookup"><span data-stu-id="facb0-118">hello input data could reside in file logs, transactional database, system performance counter etc. hello nodes with both input and output data flows are called Bolts, which do hello actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="facb0-119">SCP 支援竭盡所能、至少一次和剛好一次這三種資料處理方法。</span><span class="sxs-lookup"><span data-stu-id="facb0-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="facb0-120">在分散式串流處理應用程式中，資料處理期間可能發生各種錯誤，例如網路中斷、機器故障或使用者程式碼錯誤等。在-至少一次處理可以確保將會處理所有資料至少一次重新執行自動 hello 相同的資料時就會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="facb0-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically hello same data when error happens.</span></span> <span data-ttu-id="facb0-121">至少一次的處理方法簡單又可靠，在許多應用程式中都很適合。</span><span class="sxs-lookup"><span data-stu-id="facb0-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="facb0-122">不過，當 hello 應用程式需要精確的計算，例如，在-至少一次處理會不足因為 hello 相同的資料無法潛在播放 hello 應用程式拓撲中。</span><span class="sxs-lookup"><span data-stu-id="facb0-122">However, when hello application requires exact counting, for example, at-least-once processing is insufficient since hello same data could potentially be played in hello application topology.</span></span> <span data-ttu-id="facb0-123">在此情況下，完全-hello 資料可能會重新執行，並多次處理時，即使之後處理的設計 toomake 確定 hello 結果是否正確。</span><span class="sxs-lookup"><span data-stu-id="facb0-123">In that case, exactly-once processing is designed toomake sure hello result is correct even when hello data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="facb0-124">SCP 運用 hello Java Virtual Machine (JVM) 出現在 hello 封面時，可讓.NET 開發人員 toodevelop 即時資料處理序應用程式。</span><span class="sxs-lookup"><span data-stu-id="facb0-124">SCP enables .NET developers toodevelop real time data process applications while leverage hello Java Virtual Machine (JVM) based Storm under hello cover.</span></span> <span data-ttu-id="facb0-125">hello.NET 和 JVM 透過 TCP 本機通訊端進行通訊。</span><span class="sxs-lookup"><span data-stu-id="facb0-125">hello .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="facb0-126">基本上每個 Spout/閃電是以.Net/Java 處理序組 hello 使用者邏輯與外掛程式的.Net 處理序中執行的所在。</span><span class="sxs-lookup"><span data-stu-id="facb0-126">Basically each Spout/Bolt is a .Net/Java process pair, where hello user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="facb0-127">toobuild 資料，處理 SCP 之上的應用程式，需要數個步驟：</span><span class="sxs-lookup"><span data-stu-id="facb0-127">toobuild a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="facb0-128">設計和實作 hello Spouts toopull 資料從佇列中。</span><span class="sxs-lookup"><span data-stu-id="facb0-128">Design and implement hello Spouts toopull in data from queue.</span></span>
* <span data-ttu-id="facb0-129">設計和實作發射 tooprocess hello 輸入的資料，並儲存資料 tooexternal 存放區，例如資料庫。</span><span class="sxs-lookup"><span data-stu-id="facb0-129">Design and implement Bolts tooprocess hello input data, and save data tooexternal stores such as Database.</span></span>
* <span data-ttu-id="facb0-130">設計 hello 拓樸，然後送出，再執行 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="facb0-130">Design hello topology, then submit and run hello topology.</span></span> <span data-ttu-id="facb0-131">hello 拓撲定義端點和 hello 資料 hello 端點之間的流量。</span><span class="sxs-lookup"><span data-stu-id="facb0-131">hello topology defines vertexes and hello data flows between hello vertexes.</span></span> <span data-ttu-id="facb0-132">SCP 會採取 hello 拓撲規格，並將它部署在 Storm 叢集上，每個頂點邏輯的其中一個節點執行的位置。</span><span class="sxs-lookup"><span data-stu-id="facb0-132">SCP will take hello topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="facb0-133">hello 容錯移轉和調整將會處理 hello Storm 工作排程器。</span><span class="sxs-lookup"><span data-stu-id="facb0-133">hello failover and scaling will be taken care of by hello Storm task scheduler.</span></span>

<span data-ttu-id="facb0-134">本文件將會使用一些簡單的範例 toowalk，如何透過 SCP toobuild 資料處理應用程式。</span><span class="sxs-lookup"><span data-stu-id="facb0-134">This document will use some simple examples toowalk through how toobuild data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="facb0-135">SCP 外掛程式介面</span><span class="sxs-lookup"><span data-stu-id="facb0-135">SCP Plugin Interface</span></span>
<span data-ttu-id="facb0-136">SCP 外掛程式 （或應用程式） 是獨立的 Exe，可以同時執行 Visual Studio 內 hello 開發階段，並在生產環境中部署之後插入 hello Storm 管線。</span><span class="sxs-lookup"><span data-stu-id="facb0-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during hello development phase, and be plugged into hello Storm pipeline after deployment in production.</span></span> <span data-ttu-id="facb0-137">撰寫 hello SCP 外掛程式是只 hello 與撰寫任何其他標準 Windows 主控台應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="facb0-137">Writing hello SCP plugin is just hello same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="facb0-138">SCP.NET 平台宣告 spout/閃電，某些介面和 hello 使用者外掛程式程式碼應該實作這些介面。</span><span class="sxs-lookup"><span data-stu-id="facb0-138">SCP.NET platform declares some interface for spout/bolt, and hello user plugin code should implement these interfaces.</span></span> <span data-ttu-id="facb0-139">這項設計 hello 主要用途是該 hello 使用者可以專注於他們自己的商務 logics，並保留 SCP.NET 平台所處理其他事情 toobe。</span><span class="sxs-lookup"><span data-stu-id="facb0-139">hello main purpose of this design is that hello user can focus on their own business logics, and leaving other things toobe handled by SCP.NET platform.</span></span>

<span data-ttu-id="facb0-140">hello 使用者外掛程式程式碼應該實作其中一個 hello 下列項目介面，取決於是否 hello 拓撲是交易式或非交易式和 hello 元件是否 spout 或閃電。</span><span class="sxs-lookup"><span data-stu-id="facb0-140">hello user plugin code should implement one of hello followings interfaces, depends on whether hello topology is transactional or non-transactional, and whether hello component is spout or bolt.</span></span>

* <span data-ttu-id="facb0-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="facb0-141">ISCPSpout</span></span>
* <span data-ttu-id="facb0-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="facb0-142">ISCPBolt</span></span>
* <span data-ttu-id="facb0-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="facb0-143">ISCPTxSpout</span></span>
* <span data-ttu-id="facb0-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="facb0-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="facb0-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="facb0-145">ISCPPlugin</span></span>
<span data-ttu-id="facb0-146">ISCPPlugin 是 hello 所有種類外掛程式的通用介面。</span><span class="sxs-lookup"><span data-stu-id="facb0-146">ISCPPlugin is hello common interface for all kinds of plugins.</span></span> <span data-ttu-id="facb0-147">目前為虛擬介面。</span><span class="sxs-lookup"><span data-stu-id="facb0-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="facb0-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="facb0-148">ISCPSpout</span></span>
<span data-ttu-id="facb0-149">ISCPSpout 是非交易式 spout hello 介面。</span><span class="sxs-lookup"><span data-stu-id="facb0-149">ISCPSpout is hello interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="facb0-150">當`NextTuple()`會呼叫 hello C\#使用者程式碼可以發出一個或多個 tuple。</span><span class="sxs-lookup"><span data-stu-id="facb0-150">When `NextTuple()` is called, hello C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="facb0-151">如果沒有任何 tooemit，此方法應傳回而不發出任何項目。</span><span class="sxs-lookup"><span data-stu-id="facb0-151">If there is nothing tooemit, this method should return without emitting anything.</span></span> <span data-ttu-id="facb0-152">請注意，`NextTuple()`、`Ack()` 和 `Fail()` 都是在 C\# 程序的單一執行緒中放在密封迴圈內呼叫。</span><span class="sxs-lookup"><span data-stu-id="facb0-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="facb0-153">當不有任何 tuple tooemit 時，是禮貌 toohave NextTuple 睡眠的短的時間量 （例如 10 毫秒為單位），以不 toowaste 太多的 CPU。</span><span class="sxs-lookup"><span data-stu-id="facb0-153">When there are no tuples tooemit, it is courteous toohave NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="facb0-154">只有當規格檔中啟用認可機制時，才會呼叫 `Ack()` 和 `Fail()`。</span><span class="sxs-lookup"><span data-stu-id="facb0-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="facb0-155">hello`seqId`是使用的 tooidentify hello tuple acked 或者失敗。</span><span class="sxs-lookup"><span data-stu-id="facb0-155">hello `seqId` is used tooidentify hello tuple which is acked or failed.</span></span> <span data-ttu-id="facb0-156">因此如果 ack 已啟用非交易式拓撲中，應使用下列發出函式的 hello Spout 中：</span><span class="sxs-lookup"><span data-stu-id="facb0-156">So if ack is enabled in non-transactional topology, hello following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="facb0-157">如果非交易式拓撲中不支援通知，hello`Ack()`和`Fail()`可以保留為空白的函式。</span><span class="sxs-lookup"><span data-stu-id="facb0-157">If ack is not supported in non-transactional topology, hello `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="facb0-158">hello`parms`在這些函式的輸入的參數並非只是空的字典，這些是保留供未來使用。</span><span class="sxs-lookup"><span data-stu-id="facb0-158">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="facb0-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="facb0-159">ISCPBolt</span></span>
<span data-ttu-id="facb0-160">ISCPBolt 是非交易式閃電 hello 介面。</span><span class="sxs-lookup"><span data-stu-id="facb0-160">ISCPBolt is hello interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="facb0-161">新的 tuple 可用時，hello`Execute()`函式呼叫 tooprocess 它。</span><span class="sxs-lookup"><span data-stu-id="facb0-161">When new tuple is available, hello `Execute()` function will be called tooprocess it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="facb0-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="facb0-162">ISCPTxSpout</span></span>
<span data-ttu-id="facb0-163">ISCPTxSpout 是交易式 spout hello 介面。</span><span class="sxs-lookup"><span data-stu-id="facb0-163">ISCPTxSpout is hello interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="facb0-164">就像對應的非交易式節點一樣，`NextTx()`、`Ack()` 和 `Fail()` 也都是在 C\# 程序的單一執行緒中放在密封迴圈內呼叫。</span><span class="sxs-lookup"><span data-stu-id="facb0-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="facb0-165">沒有資料 tooemit 時，它是禮貌 toohave`NextTx`進入睡眠短的時間 （10 毫秒） 內，以不 toowaste 太多的 CPU。</span><span class="sxs-lookup"><span data-stu-id="facb0-165">When there are no data tooemit, it is courteous toohave `NextTx` sleep for a short amount of time (10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="facb0-166">`NextTx()`之所以是新的交易，toostart hello 參數`seqId`並使用的 tooidentify hello 交易，也會用於`Ack()`和`Fail()`。</span><span class="sxs-lookup"><span data-stu-id="facb0-166">`NextTx()` is called toostart a new transaction, hello out parameter `seqId` is used tooidentify hello transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="facb0-167">在`NextTx()`，使用者可以發出資料 tooJava 側邊。</span><span class="sxs-lookup"><span data-stu-id="facb0-167">In `NextTx()`, user can emit data tooJava side.</span></span> <span data-ttu-id="facb0-168">hello 資料會儲存在動物園管理員 toosupport 重新執行。</span><span class="sxs-lookup"><span data-stu-id="facb0-168">hello data will be stored in ZooKeeper toosupport replay.</span></span> <span data-ttu-id="facb0-169">動物園管理員 hello 容量皆有限，因為使用者應該只會發出中繼資料，不在交易式 spout 大量資料。</span><span class="sxs-lookup"><span data-stu-id="facb0-169">Because hello capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="facb0-170">Storm 會自動重播交易 (若失敗)，所以正常情況下應該不會呼叫 `Fail()` 。</span><span class="sxs-lookup"><span data-stu-id="facb0-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="facb0-171">但是如果 SCP 可以檢查交易式 spout 所發出的 hello 中繼資料，可以呼叫`Fail()`hello 的中繼資料無效。</span><span class="sxs-lookup"><span data-stu-id="facb0-171">But if SCP can check hello metadata emitted by transactional spout, it can call `Fail()` when hello metadata is invalid.</span></span>

<span data-ttu-id="facb0-172">hello`parms`在這些函式的輸入的參數並非只是空的字典，這些是保留供未來使用。</span><span class="sxs-lookup"><span data-stu-id="facb0-172">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="facb0-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="facb0-173">ISCPBatchBolt</span></span>
<span data-ttu-id="facb0-174">ISCPBatchBolt 是交易式閃電 hello 介面。</span><span class="sxs-lookup"><span data-stu-id="facb0-174">ISCPBatchBolt is hello interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="facb0-175">`Execute()`新的 tuple 抵達 hello 閃電時呼叫。</span><span class="sxs-lookup"><span data-stu-id="facb0-175">`Execute()` is called when there is new tuple arriving at hello bolt.</span></span> <span data-ttu-id="facb0-176">`FinishBatch()` 。</span><span class="sxs-lookup"><span data-stu-id="facb0-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="facb0-177">hello`parms`輸入的參數保留供未來使用。</span><span class="sxs-lookup"><span data-stu-id="facb0-177">hello `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="facb0-178">在交易式拓撲中，有一個重要的概念 – `StormTxAttempt`。</span><span class="sxs-lookup"><span data-stu-id="facb0-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="facb0-179">它有 `TxId` 和 `AttemptId` 兩個欄位。</span><span class="sxs-lookup"><span data-stu-id="facb0-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="facb0-180">`TxId`並使用的 tooidentify 是特定的交易，並針對給定的交易，如果可能會有多個嘗試 hello 交易失敗，而是重新執行。</span><span class="sxs-lookup"><span data-stu-id="facb0-180">`TxId` is used tooidentify a specific transaction, and for a given transaction, there may be multiple attempt if hello transaction fails and is replayed.</span></span> <span data-ttu-id="facb0-181">SCP.NET 新將不同 ISCPBatchBolt 物件 tooprocess 每個`StormTxAttempt`，就和 Java 端中的哪些 Storm 執行一樣。</span><span class="sxs-lookup"><span data-stu-id="facb0-181">SCP.NET will new a different ISCPBatchBolt object tooprocess each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="facb0-182">hello 這種設計的目的是 toosupport 平行交易處理。</span><span class="sxs-lookup"><span data-stu-id="facb0-182">hello purpose of this design is toosupport parallel transactions processing.</span></span> <span data-ttu-id="facb0-183">使用者應該記住它，如果完成交易嘗試，將會終結 hello 對應 ISCPBatchBolt 物件，記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="facb0-183">User should keep it in mind that if transaction attempt is finished, hello corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="facb0-184">物件模型</span><span class="sxs-lookup"><span data-stu-id="facb0-184">Object Model</span></span>
<span data-ttu-id="facb0-185">SCP.NET 與開發人員 tooprogram 也提供一組簡單的索引鍵物件。</span><span class="sxs-lookup"><span data-stu-id="facb0-185">SCP.NET also provides a simple set of key objects for developers tooprogram with.</span></span> <span data-ttu-id="facb0-186">包括 **Context**、**StateStore** 和 **SCPRuntime**。</span><span class="sxs-lookup"><span data-stu-id="facb0-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="facb0-187">在本節 hello 其餘部分中，將討論它們。</span><span class="sxs-lookup"><span data-stu-id="facb0-187">They will be discussed in hello rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="facb0-188">Context</span><span class="sxs-lookup"><span data-stu-id="facb0-188">Context</span></span>
<span data-ttu-id="facb0-189">內容會提供執行的環境 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="facb0-189">Context provides a running environment toohello application.</span></span> <span data-ttu-id="facb0-190">每個 ISCPPlugin 執行個體 (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) 都有一個對應的 Context 執行個體。</span><span class="sxs-lookup"><span data-stu-id="facb0-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="facb0-191">內容所提供的 hello 功能可分成兩個部分: （1) hello 靜態部分中可用 hello 整個 C\#處理時，只適用於 hello 特定內容執行個體 （2) hello 動態組件。</span><span class="sxs-lookup"><span data-stu-id="facb0-191">hello functionality provided by Context can be divided into two parts: (1) hello static part which is available in hello whole C\# process, (2) hello dynamic part which is only available for hello specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="facb0-192">靜態部分</span><span class="sxs-lookup"><span data-stu-id="facb0-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="facb0-193">`Logger` 做為記錄用途。</span><span class="sxs-lookup"><span data-stu-id="facb0-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="facb0-194">`pluginType`是用 hello C tooindicate hello 外掛程式類型\#程序。</span><span class="sxs-lookup"><span data-stu-id="facb0-194">`pluginType` is used tooindicate hello plugin type of hello C\# process.</span></span> <span data-ttu-id="facb0-195">如果 hello C\# （不含 Java) 的本機測試模式中執行程序，hello 外掛程式型別是`SCP_NET_LOCAL`。</span><span class="sxs-lookup"><span data-stu-id="facb0-195">If hello C\# process is run in local test mode (without Java), hello plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="facb0-196">`Config`提供從 Java 端 tooget 組態參數。</span><span class="sxs-lookup"><span data-stu-id="facb0-196">`Config` is provided tooget configuration parameters from Java side.</span></span> <span data-ttu-id="facb0-197">從 Java 端 hello 參數傳遞時 C\#初始化外掛程式。</span><span class="sxs-lookup"><span data-stu-id="facb0-197">hello parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="facb0-198">hello`Config`參數分為兩個部分：`stormConf`和`pluginConf`。</span><span class="sxs-lookup"><span data-stu-id="facb0-198">hello `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="facb0-199">`stormConf`Storm 所定義的參數和`pluginConf`hello SCP 所定義的參數。</span><span class="sxs-lookup"><span data-stu-id="facb0-199">`stormConf` is parameters defined by Storm and `pluginConf` is hello parameters defined by SCP.</span></span> <span data-ttu-id="facb0-200">例如：</span><span class="sxs-lookup"><span data-stu-id="facb0-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="facb0-201">`TopologyContext`會提供 tooget hello 拓撲內容，它是最有用之元件的多個平行處理原則。</span><span class="sxs-lookup"><span data-stu-id="facb0-201">`TopologyContext` is provided tooget hello topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="facb0-202">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="facb0-202">Here is an example:</span></span>

    //demo how tooget TopologyContext info
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

### <a name="dynamic-part"></a><span data-ttu-id="facb0-203">動態部分</span><span class="sxs-lookup"><span data-stu-id="facb0-203">Dynamic Part</span></span>
<span data-ttu-id="facb0-204">下列介面 hello 是相關 tooa 特定內容執行個體。</span><span class="sxs-lookup"><span data-stu-id="facb0-204">hello following interfaces are pertinent tooa certain Context instance.</span></span> <span data-ttu-id="facb0-205">hello 內容執行個體是 SCP.NET 平台所建立，並傳遞 toohello 使用者程式碼：</span><span class="sxs-lookup"><span data-stu-id="facb0-205">hello Context instance is created by SCP.NET platform and passed toohello user code:</span></span>

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="facb0-206">針對非交易式 spout 支援通知，會提供下列方法 hello:</span><span class="sxs-lookup"><span data-stu-id="facb0-206">For non-transactional spout supporting ack, hello following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="facb0-207">對於非交易式閃電支援通知，它應該明確`Ack()`或`Fail()`hello 它接收的 tuple。</span><span class="sxs-lookup"><span data-stu-id="facb0-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` hello tuple it received.</span></span> <span data-ttu-id="facb0-208">且當發出新的 tuple，也必須指定 hello 新 tuple 的 hello 錨點。</span><span class="sxs-lookup"><span data-stu-id="facb0-208">And when emitting new tuple, it must also specify hello anchors of hello new tuple.</span></span> <span data-ttu-id="facb0-209">提供下列方法 hello。</span><span class="sxs-lookup"><span data-stu-id="facb0-209">hello following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="facb0-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="facb0-210">StateStore</span></span>
<span data-ttu-id="facb0-211">`StateStore` 提供元資料服務、單調數列產生和免等待協調。</span><span class="sxs-lookup"><span data-stu-id="facb0-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="facb0-212">高階分散式並行抽象可根據 `StateStore`來建置，包括分散式鎖定、分散式佇列、屏障和交易服務。</span><span class="sxs-lookup"><span data-stu-id="facb0-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="facb0-213">SCP 應用程式可能使用 hello`State`物件 toopersist 中動物園管理員，特別是針對交易式拓撲的特定資訊。</span><span class="sxs-lookup"><span data-stu-id="facb0-213">SCP applications may use hello `State` object toopersist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="facb0-214">因此，如果交易式 spout 損毀，並重新啟動，它可以從動物園管理員擷取 hello 所需的資訊，然後重新啟動 hello 管線進行。</span><span class="sxs-lookup"><span data-stu-id="facb0-214">Doing so, if transactional spout crashes and restart, it can retrieve hello necessary information from ZooKeeper and restart hello pipeline.</span></span>

<span data-ttu-id="facb0-215">hello`StateStore`物件主要有這些方法：</span><span class="sxs-lookup"><span data-stu-id="facb0-215">hello `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
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
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="facb0-216">hello`State`物件主要有這些方法：</span><span class="sxs-lookup"><span data-stu-id="facb0-216">hello `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="facb0-217">Hello`Commit()`方法，當 simpleMode tootrue 設定時，將只會刪除對應 ZNode 動物園管理員中的 hello。</span><span class="sxs-lookup"><span data-stu-id="facb0-217">For hello `Commit()` method, when simpleMode is set tootrue, it will simply delete hello corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="facb0-218">否則，它會刪除 hello 目前 ZNode，並加入新的節點在 hello 已認可\_路徑。</span><span class="sxs-lookup"><span data-stu-id="facb0-218">Otherwise, it will delete hello current ZNode, and adding a new node in hello COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="facb0-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="facb0-219">SCPRuntime</span></span>
<span data-ttu-id="facb0-220">SCPRuntime 提供下列兩種方法的 hello。</span><span class="sxs-lookup"><span data-stu-id="facb0-220">SCPRuntime provides hello following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="facb0-221">`Initialize()`是使用的 tooinitialize hello SCP 執行階段環境。</span><span class="sxs-lookup"><span data-stu-id="facb0-221">`Initialize()` is used tooinitialize hello SCP runtime environment.</span></span> <span data-ttu-id="facb0-222">在此方法中，hello C\# toohello Java 端，以及取得設定參數和拓撲內容，將連線程序。</span><span class="sxs-lookup"><span data-stu-id="facb0-222">In this method, hello C\# process will connect toohello Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="facb0-223">`LaunchPlugin()`正在使用的 tookick 關閉 hello 訊息處理迴圈。</span><span class="sxs-lookup"><span data-stu-id="facb0-223">`LaunchPlugin()` is used tookick off hello message processing loop.</span></span> <span data-ttu-id="facb0-224">在此迴圈中，hello C\#外掛程式將會收到訊息格式 （包括 tuple 和控制訊號） 的 Java 端，，，然後處理 hello 訊息時，可能呼叫 hello 介面方法提供 hello 使用者程式碼。</span><span class="sxs-lookup"><span data-stu-id="facb0-224">In this loop, hello C\# plugin will receive messages form Java side (including tuples and control signals), and then process hello messages, perhaps calling hello interface method provide by hello user code.</span></span> <span data-ttu-id="facb0-225">hello 方法的輸入的參數`LaunchPlugin()`是一種委派可傳回實作 ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt 介面的物件。</span><span class="sxs-lookup"><span data-stu-id="facb0-225">hello input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="facb0-226">如 ISCPBatchBolt，我們可以得到`StormTxAttempt`從`parms`，並用它 toojudge 是否在重新執行的嘗試。</span><span class="sxs-lookup"><span data-stu-id="facb0-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it toojudge whether it is a replayed attempt.</span></span> <span data-ttu-id="facb0-227">這通常在 hello 認可閃電，並示範在 hello`HelloWorldTx`範例。</span><span class="sxs-lookup"><span data-stu-id="facb0-227">This is usually done at hello commit bolt, and it is demonstrated in hello `HelloWorldTx` example.</span></span>

<span data-ttu-id="facb0-228">一般而言，hello SCP 增益集可以執行以下兩種模式：</span><span class="sxs-lookup"><span data-stu-id="facb0-228">Generally speaking, hello SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="facb0-229">本機測試模式： 在此模式中，hello SCP 外掛程式 (hello C\#使用者程式碼) 在 Visual Studio 內執行 hello 開發階段。</span><span class="sxs-lookup"><span data-stu-id="facb0-229">Local Test Mode: In this mode, hello SCP plugins (hello C\# user code) run inside Visual Studio during hello development phase.</span></span> <span data-ttu-id="facb0-230">`LocalContext`可在此模式，提供方法 tooserialize hello 發出 tuple toolocal 檔案，以及送回 toomemory 讀取。</span><span class="sxs-lookup"><span data-stu-id="facb0-230">`LocalContext` can be used in this mode, which provides method tooserialize hello emitted tuples toolocal files, and read them back toomemory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="facb0-231">一般模式： 在此模式中，hello SCP 外掛程式所啟動 storm java 處理序。</span><span class="sxs-lookup"><span data-stu-id="facb0-231">Regular Mode: In this mode, hello SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="facb0-232">以下是啟動 SCP 外掛程式的範例：</span><span class="sxs-lookup"><span data-stu-id="facb0-232">Here is an example of launching SCP plugin:</span></span>
   
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
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="facb0-233">拓撲規格語言</span><span class="sxs-lookup"><span data-stu-id="facb0-233">Topology Specification Language</span></span>
<span data-ttu-id="facb0-234">SCP 拓撲規格是特定領域的語言，用來描述和設定 SCP 拓撲。</span><span class="sxs-lookup"><span data-stu-id="facb0-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="facb0-235">它以 Storm 的 Clojure DSL 為基礎 (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>)，而由 SCP 擴充。</span><span class="sxs-lookup"><span data-stu-id="facb0-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="facb0-236">直接透過 hello toostorm 叢集來執行，就可以提出拓撲規格***runspec***命令。</span><span class="sxs-lookup"><span data-stu-id="facb0-236">Topology specifications can be submitted directly toostorm cluster for execution via hello ***runspec*** command.</span></span>

<span data-ttu-id="facb0-237">SCP.NET 已新增下列函式 toodefine hello 交易式拓撲：</span><span class="sxs-lookup"><span data-stu-id="facb0-237">SCP.NET has add follow functions toodefine hello Transactional Topology:</span></span>

| <span data-ttu-id="facb0-238">**新函數**</span><span class="sxs-lookup"><span data-stu-id="facb0-238">**New Functions**</span></span> | <span data-ttu-id="facb0-239">**參數**</span><span class="sxs-lookup"><span data-stu-id="facb0-239">**Parameters**</span></span> | <span data-ttu-id="facb0-240">**說明**</span><span class="sxs-lookup"><span data-stu-id="facb0-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="facb0-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="facb0-241">**tx-topolopy**</span></span> |<span data-ttu-id="facb0-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="facb0-242">topology-name</span></span><br /><span data-ttu-id="facb0-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="facb0-243">spout-map</span></span><br /><span data-ttu-id="facb0-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="facb0-244">bolt-map</span></span> |<span data-ttu-id="facb0-245">定義具有 hello 拓撲名稱的交易式拓撲&nbsp;spouts 定義地圖與 hello 發射定義地圖</span><span class="sxs-lookup"><span data-stu-id="facb0-245">Define a transactional topology with hello topology name, &nbsp;spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="facb0-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="facb0-246">**scp-tx-spout**</span></span> |<span data-ttu-id="facb0-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="facb0-247">exec-name</span></span><br /><span data-ttu-id="facb0-248">args</span><span class="sxs-lookup"><span data-stu-id="facb0-248">args</span></span><br /><span data-ttu-id="facb0-249">fields</span><span class="sxs-lookup"><span data-stu-id="facb0-249">fields</span></span> |<span data-ttu-id="facb0-250">定義交易式 spout。</span><span class="sxs-lookup"><span data-stu-id="facb0-250">Define a transactional spout.</span></span> <span data-ttu-id="facb0-251">它會執行與 hello 應用程式***exec 名稱***使用***args***。</span><span class="sxs-lookup"><span data-stu-id="facb0-251">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="facb0-252">hello***欄位***是 spout 的 hello 輸出欄位</span><span class="sxs-lookup"><span data-stu-id="facb0-252">hello ***fields*** is hello Output Fields for spout</span></span> |
| <span data-ttu-id="facb0-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="facb0-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="facb0-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="facb0-254">exec-name</span></span><br /><span data-ttu-id="facb0-255">args</span><span class="sxs-lookup"><span data-stu-id="facb0-255">args</span></span><br /><span data-ttu-id="facb0-256">fields</span><span class="sxs-lookup"><span data-stu-id="facb0-256">fields</span></span> |<span data-ttu-id="facb0-257">定義交易式批次 Bolt。</span><span class="sxs-lookup"><span data-stu-id="facb0-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="facb0-258">它會執行與 hello 應用程式***exec 名稱***使用***引數。***</span><span class="sxs-lookup"><span data-stu-id="facb0-258">It will run hello application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="facb0-259">hello 欄位是針對閃電 hello 輸出欄位。</span><span class="sxs-lookup"><span data-stu-id="facb0-259">hello Fields is hello Output Fields for bolt.</span></span> |
| <span data-ttu-id="facb0-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="facb0-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="facb0-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="facb0-261">exec-name</span></span><br /><span data-ttu-id="facb0-262">args</span><span class="sxs-lookup"><span data-stu-id="facb0-262">args</span></span><br /><span data-ttu-id="facb0-263">fields</span><span class="sxs-lookup"><span data-stu-id="facb0-263">fields</span></span> |<span data-ttu-id="facb0-264">定義交易式認可者 Bolt。</span><span class="sxs-lookup"><span data-stu-id="facb0-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="facb0-265">它會執行與 hello 應用程式***exec 名稱***使用***args***。</span><span class="sxs-lookup"><span data-stu-id="facb0-265">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="facb0-266">hello***欄位***是閃電的 hello 輸出欄位</span><span class="sxs-lookup"><span data-stu-id="facb0-266">hello ***fields*** is hello Output Fields for bolt</span></span> |
| <span data-ttu-id="facb0-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="facb0-267">**nontx-topolopy**</span></span> |<span data-ttu-id="facb0-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="facb0-268">topology-name</span></span><br /><span data-ttu-id="facb0-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="facb0-269">spout-map</span></span><br /><span data-ttu-id="facb0-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="facb0-270">bolt-map</span></span> |<span data-ttu-id="facb0-271">定義非交易式拓撲 hello 拓撲，以名稱&nbsp;spouts 定義地圖與 hello 發射定義地圖</span><span class="sxs-lookup"><span data-stu-id="facb0-271">Define a nontransactional topology with hello topology name,&nbsp; spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="facb0-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="facb0-272">**scp-spout**</span></span> |<span data-ttu-id="facb0-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="facb0-273">exec-name</span></span><br /><span data-ttu-id="facb0-274">args</span><span class="sxs-lookup"><span data-stu-id="facb0-274">args</span></span><br /><span data-ttu-id="facb0-275">fields</span><span class="sxs-lookup"><span data-stu-id="facb0-275">fields</span></span><br /><span data-ttu-id="facb0-276">參數</span><span class="sxs-lookup"><span data-stu-id="facb0-276">parameters</span></span> |<span data-ttu-id="facb0-277">定義非交易式 spout。</span><span class="sxs-lookup"><span data-stu-id="facb0-277">Define a nontransactional spout.</span></span> <span data-ttu-id="facb0-278">它會執行與 hello 應用程式***exec 名稱***使用***args***。</span><span class="sxs-lookup"><span data-stu-id="facb0-278">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="facb0-279">hello***欄位***是 spout 的 hello 輸出欄位</span><span class="sxs-lookup"><span data-stu-id="facb0-279">hello ***fields*** is hello Output Fields for spout</span></span><br /><br /><span data-ttu-id="facb0-280">hello***參數***是選擇性的它使用 toospecify 某些參數，例如"nontransactional.ack.enabled"。</span><span class="sxs-lookup"><span data-stu-id="facb0-280">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="facb0-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="facb0-281">**scp-bolt**</span></span> |<span data-ttu-id="facb0-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="facb0-282">exec-name</span></span><br /><span data-ttu-id="facb0-283">args</span><span class="sxs-lookup"><span data-stu-id="facb0-283">args</span></span><br /><span data-ttu-id="facb0-284">fields</span><span class="sxs-lookup"><span data-stu-id="facb0-284">fields</span></span><br /><span data-ttu-id="facb0-285">參數</span><span class="sxs-lookup"><span data-stu-id="facb0-285">parameters</span></span> |<span data-ttu-id="facb0-286">定義非交易式 Bolt。</span><span class="sxs-lookup"><span data-stu-id="facb0-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="facb0-287">它會執行與 hello 應用程式***exec 名稱***使用***args***。</span><span class="sxs-lookup"><span data-stu-id="facb0-287">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="facb0-288">hello***欄位***是閃電的 hello 輸出欄位</span><span class="sxs-lookup"><span data-stu-id="facb0-288">hello ***fields*** is hello Output Fields for bolt</span></span><br /><br /><span data-ttu-id="facb0-289">hello***參數***是選擇性的它使用 toospecify 某些參數，例如"nontransactional.ack.enabled"。</span><span class="sxs-lookup"><span data-stu-id="facb0-289">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="facb0-290">SCP.NET 定義下列關鍵字：</span><span class="sxs-lookup"><span data-stu-id="facb0-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="facb0-291">**關鍵字**</span><span class="sxs-lookup"><span data-stu-id="facb0-291">**Key Words**</span></span> | <span data-ttu-id="facb0-292">**說明**</span><span class="sxs-lookup"><span data-stu-id="facb0-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="facb0-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="facb0-293">**:name**</span></span> |<span data-ttu-id="facb0-294">定義 hello 拓撲名稱</span><span class="sxs-lookup"><span data-stu-id="facb0-294">Define hello Topology Name</span></span> |
| <span data-ttu-id="facb0-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="facb0-295">**:topology**</span></span> |<span data-ttu-id="facb0-296">定義 hello 拓撲使用上述函式的 hello 和中的建置。</span><span class="sxs-lookup"><span data-stu-id="facb0-296">Define hello Topology using hello above functions and build in ones.</span></span> |
| <span data-ttu-id="facb0-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="facb0-297">**:p**</span></span> |<span data-ttu-id="facb0-298">定義每個 spout 或閃電 hello 平行處理原則提示。</span><span class="sxs-lookup"><span data-stu-id="facb0-298">Define hello parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="facb0-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="facb0-299">**:config**</span></span> |<span data-ttu-id="facb0-300">定義設定參數，或更新 hello 現有的</span><span class="sxs-lookup"><span data-stu-id="facb0-300">Define configure parameter or update hello existing ones</span></span> |
| <span data-ttu-id="facb0-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="facb0-301">**:schema**</span></span> |<span data-ttu-id="facb0-302">定義 hello 結構描述的資料流。</span><span class="sxs-lookup"><span data-stu-id="facb0-302">Define hello Schema of Stream.</span></span> |

<span data-ttu-id="facb0-303">還有常用參數：</span><span class="sxs-lookup"><span data-stu-id="facb0-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="facb0-304">**參數**</span><span class="sxs-lookup"><span data-stu-id="facb0-304">**Parameter**</span></span> | <span data-ttu-id="facb0-305">**說明**</span><span class="sxs-lookup"><span data-stu-id="facb0-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="facb0-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="facb0-306">**"plugin.name"**</span></span> |<span data-ttu-id="facb0-307">hello C# 外掛程式 exe 檔案名稱</span><span class="sxs-lookup"><span data-stu-id="facb0-307">exe file name of hello C# plugin</span></span> |
| <span data-ttu-id="facb0-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="facb0-308">**"plugin.args"**</span></span> |<span data-ttu-id="facb0-309">外掛程式引數</span><span class="sxs-lookup"><span data-stu-id="facb0-309">plugin args</span></span> |
| <span data-ttu-id="facb0-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="facb0-310">**"output.schema"**</span></span> |<span data-ttu-id="facb0-311">輸出結構描述</span><span class="sxs-lookup"><span data-stu-id="facb0-311">Output schema</span></span> |
| <span data-ttu-id="facb0-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="facb0-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="facb0-313">非交易式拓撲是否啟用認可</span><span class="sxs-lookup"><span data-stu-id="facb0-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="facb0-314">hello runspec 命令將會部署與 hello 位元，hello 使用量就像是：</span><span class="sxs-lookup"><span data-stu-id="facb0-314">hello runspec command will be deployed together with hello bits, hello usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="facb0-315">hello***資源-dir***參數是選擇性的您需要 toospecify 時想 tooplug C\# hello 應用程式、 hello 相依性和組態，則將會包含應用程式，而此目錄。</span><span class="sxs-lookup"><span data-stu-id="facb0-315">hello ***resource-dir*** parameter is optional, you need toospecify it when you want tooplug a C\# application, and this directory will contain hello application, hello dependencies and configurations.</span></span>

<span data-ttu-id="facb0-316">hello ***classpath***也是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="facb0-316">hello ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="facb0-317">如果 hello 規格檔案包含 Java Spout 或閃電，則使用的 toospecify hello Java classpath。</span><span class="sxs-lookup"><span data-stu-id="facb0-317">It is used toospecify hello Java classpath if hello spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="facb0-318">其他功能</span><span class="sxs-lookup"><span data-stu-id="facb0-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="facb0-319">輸入和輸出結構描述宣告</span><span class="sxs-lookup"><span data-stu-id="facb0-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="facb0-320">hello 使用者可發出 C 中的 tuple\#處理、 hello 平台需要 tooserialize hello tuple 成 byte []、 傳輸 tooJava 端，以及 Storm 會傳輸此 tuple toohello 的目標。</span><span class="sxs-lookup"><span data-stu-id="facb0-320">hello user can emit tuple in C\# process, hello platform needs tooserialize hello tuple into byte[], transfer tooJava side, and Storm will transfer this tuple toohello targets.</span></span> <span data-ttu-id="facb0-321">同時在下游元件 hello C\#程序將會接收 tuple 從 java 端，並將它轉換 toohello 原始型別平台，所有這些作業會隱藏 hello 平台。</span><span class="sxs-lookup"><span data-stu-id="facb0-321">Meanwhile in downstream component, hello C\# process will receive tuple back from java side, and convert it toohello original types by platform, all these operations are hidden by hello Platform.</span></span>

<span data-ttu-id="facb0-322">toosupport hello 序列化和還原序列化，使用者程式碼需要 hello 輸入和輸出的 toodeclare hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="facb0-322">toosupport hello serialization and deserialization, user code needs toodeclare hello schema of hello inputs and outputs.</span></span>

<span data-ttu-id="facb0-323">hello 輸入/輸出資料流之結構描述是定義為字典，hello 金鑰為 hello StreamId hello 值為 hello hello 資料行類型。</span><span class="sxs-lookup"><span data-stu-id="facb0-323">hello input/output stream schema is defined as a dictionary, hello key is hello StreamId and hello value is hello Types of hello columns.</span></span> <span data-ttu-id="facb0-324">hello 元件可以有多個宣告的資料流。</span><span class="sxs-lookup"><span data-stu-id="facb0-324">hello component can have multi-streams declared.</span></span>

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


<span data-ttu-id="facb0-325">在內容物件有的 hello 加入下列 API:</span><span class="sxs-lookup"><span data-stu-id="facb0-325">In Context object, we have hello following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="facb0-326">使用者程式碼必須確定發出 hello tuple 遵守 hello，該資料流所定義的結構描述或 hello 系統將會擲回執行階段例外狀況。</span><span class="sxs-lookup"><span data-stu-id="facb0-326">User code must make sure hello tuples emitted obey hello schema defined for that stream, or hello system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="facb0-327">多重串流支援</span><span class="sxs-lookup"><span data-stu-id="facb0-327">Multi-Stream Support</span></span>
<span data-ttu-id="facb0-328">SCP 支援使用者程式碼 tooemit，或是接收來自多個不同的資料流 hello 在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="facb0-328">SCP supports user code tooemit or receive from multiple distinct streams at hello same time.</span></span> <span data-ttu-id="facb0-329">hello 支援反映 hello 內容物件中 hello 發出方法會接受選擇性的資料流識別碼參數。</span><span class="sxs-lookup"><span data-stu-id="facb0-329">hello support reflects in hello Context object as hello Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="facb0-330">已加入 hello SCP.NET 內容物件中的兩個方法。</span><span class="sxs-lookup"><span data-stu-id="facb0-330">Two methods in hello SCP.NET Context object have been added.</span></span> <span data-ttu-id="facb0-331">它們是使用的 tooemit Tuple 或 Tuple toospecify StreamId。</span><span class="sxs-lookup"><span data-stu-id="facb0-331">They are used tooemit Tuple or Tuples toospecify StreamId.</span></span> <span data-ttu-id="facb0-332">hello StreamId 是字串，而且它需要 toobe 一致，在這兩個 C\#和 hello 拓撲定義規格。</span><span class="sxs-lookup"><span data-stu-id="facb0-332">hello StreamId is a string and it needs toobe consistent in both C\# and hello Topology Definition Spec.</span></span>

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="facb0-333">hello 發出 tooa 不存在的資料流將導致執行階段例外狀況。</span><span class="sxs-lookup"><span data-stu-id="facb0-333">hello emitting tooa non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="facb0-334">欄位分組</span><span class="sxs-lookup"><span data-stu-id="facb0-334">Fields Grouping</span></span>
<span data-ttu-id="facb0-335">內建欄位群組在 Strom 運作不正確 SCP.NET 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="facb0-335">hello build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="facb0-336">Hello Java Proxy 側邊，在所有 hello 欄位資料型別都是實際 byte []，並分組 hello 欄位使用 hello 位元組 [] 物件的雜湊程式碼 tooperform hello 群組。</span><span class="sxs-lookup"><span data-stu-id="facb0-336">On hello Java Proxy side, all hello fields data types are actually byte[], and hello fields grouping uses hello byte[] object hash code tooperform hello grouping.</span></span> <span data-ttu-id="facb0-337">hello 位元組 [] 物件的雜湊程式碼是此物件在記憶體中的 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="facb0-337">hello byte[] object hash code is hello address of this object in memory.</span></span> <span data-ttu-id="facb0-338">因此 hello 群組會是錯誤的兩個位元組 [] 的物件相同的內容，但不是 hello 相同的位址，該共用 hello。</span><span class="sxs-lookup"><span data-stu-id="facb0-338">So hello grouping will be wrong for two byte[] objects that share hello same content but not hello same address.</span></span>

<span data-ttu-id="facb0-339">SCP.NET 加入自訂的群組的方法，它會使用 hello hello 位元組 [] toodo hello 群組內容。</span><span class="sxs-lookup"><span data-stu-id="facb0-339">SCP.NET adds a customized grouping method, and it will use hello content of hello byte[] toodo hello grouping.</span></span> <span data-ttu-id="facb0-340">在**規格**檔案，就像是 hello 語法：</span><span class="sxs-lookup"><span data-stu-id="facb0-340">In **SPEC** file, hello syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="facb0-341">在這裡，</span><span class="sxs-lookup"><span data-stu-id="facb0-341">Here,</span></span>

1. <span data-ttu-id="facb0-342">“scp-field-group” 表示「SCP 實作的自訂欄位分組」。</span><span class="sxs-lookup"><span data-stu-id="facb0-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="facb0-343">“:tx” 或 “:non-tx” 表示是否為交易式拓撲。</span><span class="sxs-lookup"><span data-stu-id="facb0-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="facb0-344">由於 hello 的起始索引與非 tx 拓撲不同 tx 中，我們需要這項資訊。</span><span class="sxs-lookup"><span data-stu-id="facb0-344">We need this information since hello starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="facb0-345">[0,1] 表示欄位 Id 的雜湊集，從 0 開始。</span><span class="sxs-lookup"><span data-stu-id="facb0-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="facb0-346">混合式拓撲</span><span class="sxs-lookup"><span data-stu-id="facb0-346">Hybrid topology</span></span>
<span data-ttu-id="facb0-347">原生 Storm 以 Java 撰寫的 hello。</span><span class="sxs-lookup"><span data-stu-id="facb0-347">hello native Storm is written in Java.</span></span> <span data-ttu-id="facb0-348">和 SCP.Net 已經增強，它 tooenable 我們自訂 toowrite C\#程式碼 toohandle 其商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="facb0-348">And SCP.Net has enhanced it tooenable our customs toowrite C\# code toohandle their business logic.</span></span> <span data-ttu-id="facb0-349">但我們也支援混合式拓撲，不僅包含 C\# spout/bolt，也包含 Java Spout/Bolt。</span><span class="sxs-lookup"><span data-stu-id="facb0-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="facb0-350">在規格檔中指定 Java Spout/Bolt</span><span class="sxs-lookup"><span data-stu-id="facb0-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="facb0-351">在規格的檔案中，「 scp spout"和"scp 閃電 」 也可以使用的 toospecify Java Spouts 和攻擊，範例如下：</span><span class="sxs-lookup"><span data-stu-id="facb0-351">In spec file, "scp-spout" and "scp-bolt" can also be used toospecify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="facb0-352">這裡`microsoft.scp.example.HybridTopology.Generator`hello hello Java Spout 類別名稱。</span><span class="sxs-lookup"><span data-stu-id="facb0-352">Here `microsoft.scp.example.HybridTopology.Generator` is hello name of hello Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="facb0-353">在 runSpec 命令中指定 Java 類別路徑</span><span class="sxs-lookup"><span data-stu-id="facb0-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="facb0-354">如果您想包含 Java Spouts 或發射 toosubmit 拓撲時，您需要使用 Java Spouts toofirst 編譯 hello 或攻擊，並取得 hello Jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="facb0-354">If you want toosubmit topology containing Java Spouts or Bolts, you need toofirst compile hello Java Spouts or Bolts and get hello Jar files.</span></span> <span data-ttu-id="facb0-355">接著，您應該指定 hello java classpath 提交拓撲時，包含 hello Jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="facb0-355">Then you should specify hello java classpath that contains hello Jar files when submitting topology.</span></span> <span data-ttu-id="facb0-356">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="facb0-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="facb0-357">這裡**範例\\HybridTopology\\java\\目標\\** hello 資料夾包含 hello Java Spout/閃電 Jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="facb0-357">Here **examples\\HybridTopology\\java\\target\\** is hello folder containing hello Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="facb0-358">Java 與 C\ 之間的序列化和還原序列化</span><span class="sxs-lookup"><span data-stu-id="facb0-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="facb0-359">我們的 SCP 元件包含 Java 和 C\# 端。</span><span class="sxs-lookup"><span data-stu-id="facb0-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="facb0-360">順序 toointeract 與原生 Java Spouts/攻擊，序列化/還原序列化必須執行時，在 Java 側邊與 C 之間\#端 hello 下列圖表所示。</span><span class="sxs-lookup"><span data-stu-id="facb0-360">In order toointeract with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in hello following graph.</span></span>

![java 元件傳送 tooSCP 元件傳送 tooJava 元件的圖表](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="facb0-362">**Java 端序列化和 C\# 端還原序列化**</span><span class="sxs-lookup"><span data-stu-id="facb0-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="facb0-363">首次，我們提供 Java 端序列化和 C\# 端還原序列化的預設實作。</span><span class="sxs-lookup"><span data-stu-id="facb0-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="facb0-364">Java 端中的 hello 序列化方法可加以指定規格的檔案中：</span><span class="sxs-lookup"><span data-stu-id="facb0-364">hello serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="facb0-365">還原序列化方法，在 C 中的 hello\#端應該指定在 C 中\#使用者程式碼：</span><span class="sxs-lookup"><span data-stu-id="facb0-365">hello deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="facb0-366">這個預設實作應該處理大部分的情況下，如果 hello 資料類型不是太複雜。</span><span class="sxs-lookup"><span data-stu-id="facb0-366">This default implementation should handle most cases if hello data type is not too complex.</span></span> <span data-ttu-id="facb0-367">某些情況下，可能是因為 hello 使用者資料型別是過於複雜、 或 hello 效能在我們的預設實作不符合 hello 使用者的需求，使用者可以外掛程式自己的實作。</span><span class="sxs-lookup"><span data-stu-id="facb0-367">For certain cases, either because hello user data type is too complex, or because hello performance of our default implementation does not meet hello user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="facb0-368">hello 序列化介面端定義為在 java 中：</span><span class="sxs-lookup"><span data-stu-id="facb0-368">hello serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="facb0-369">hello 還原序列化介面，在 C 中\#端定義為：</span><span class="sxs-lookup"><span data-stu-id="facb0-369">hello deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="facb0-370">公用介面 ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="facb0-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="facb0-371">**C\# 端序列化和 Java 端還原序列化**</span><span class="sxs-lookup"><span data-stu-id="facb0-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="facb0-372">hello C 中的序列化方法\#端應該指定在 C 中\#使用者程式碼：</span><span class="sxs-lookup"><span data-stu-id="facb0-372">hello serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="facb0-373">hello Java 端中的還原序列化方法應指定規格的檔案中：</span><span class="sxs-lookup"><span data-stu-id="facb0-373">hello Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="facb0-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="facb0-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="facb0-375">這裡"microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer"hello 還原序列化程式，名稱，而 「 microsoft.scp.example.HybridTopology.Person"hello 目標類別 hello 資料還原序列化。</span><span class="sxs-lookup"><span data-stu-id="facb0-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is hello name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is hello target class hello data is deserialized to.</span></span>
   
   <span data-ttu-id="facb0-376">使用者也可以外掛其自己實作的 C\# 序列化程式和 Java Deserializer。</span><span class="sxs-lookup"><span data-stu-id="facb0-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="facb0-377">這是 C hello 介面\#序列化程式：</span><span class="sxs-lookup"><span data-stu-id="facb0-377">This is hello interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="facb0-378">這是 Java 還原序列化程式的 hello 介面：</span><span class="sxs-lookup"><span data-stu-id="facb0-378">This is hello interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="facb0-379">SCP 主機模式</span><span class="sxs-lookup"><span data-stu-id="facb0-379">SCP Host Mode</span></span>
<span data-ttu-id="facb0-380">在此模式中，使用者可以編譯它們代碼 tooDLL，，並使用 SCPHost.exe SCP toosubmit 拓撲所提供。</span><span class="sxs-lookup"><span data-stu-id="facb0-380">In this mode, user can compile their codes tooDLL, and use SCPHost.exe provided by SCP toosubmit topology.</span></span> <span data-ttu-id="facb0-381">hello 規格檔案看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="facb0-381">hello spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="facb0-382">其中，`plugin.name` 指定為 SCP SDK 所提供的 `SCPHost.exe`。</span><span class="sxs-lookup"><span data-stu-id="facb0-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="facb0-383">SCPHost.exe 只接受三個參數：</span><span class="sxs-lookup"><span data-stu-id="facb0-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="facb0-384">hello 第一次是 hello DLL 名稱，亦即`"HelloWorld.dll"`在此範例中。</span><span class="sxs-lookup"><span data-stu-id="facb0-384">hello first one is hello DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="facb0-385">hello 第二個是 hello 類別名稱，亦即`"Scp.App.HelloWorld.Generator"`在此範例中。</span><span class="sxs-lookup"><span data-stu-id="facb0-385">hello second one is hello Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="facb0-386">hello 第三個是 hello 的公用靜態方法，它可以是叫用的 tooget ISCPPlugin 的執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="facb0-386">hello third one is hello name of a public static method, which can be invoked tooget an instance of ISCPPlugin.</span></span>

<span data-ttu-id="facb0-387">在主機模式中，使用者程式碼會編譯成 DLL，供 SCP 平台叫用。</span><span class="sxs-lookup"><span data-stu-id="facb0-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="facb0-388">因此 SCP 平台可以得到 hello 整個處理邏輯的完整控制權。</span><span class="sxs-lookup"><span data-stu-id="facb0-388">So SCP platform can get full control of hello whole processing logic.</span></span> <span data-ttu-id="facb0-389">因此，建議客戶 SCP 主機模式 toosubmit 拓撲因為它可以簡化 hello 開發經驗，以及較新版本的更多的彈性和更好的回溯相容性帶我們。</span><span class="sxs-lookup"><span data-stu-id="facb0-389">So we recommend our customers toosubmit topology in SCP host mode since it can simplify hello development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="facb0-390">SCP 程式設計範例</span><span class="sxs-lookup"><span data-stu-id="facb0-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="facb0-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="facb0-391">HelloWorld</span></span>
<span data-ttu-id="facb0-392">**HelloWorld**是非常簡單的範例 tooshow SCP.Net 的功用。</span><span class="sxs-lookup"><span data-stu-id="facb0-392">**HelloWorld** is a very simple example tooshow a taste of SCP.Net.</span></span> <span data-ttu-id="facb0-393">它使用非交易拓撲，具有一個名為 **generator** 的 spout，以及名為 **splitter** 和 **counter** 的兩個 bolt。</span><span class="sxs-lookup"><span data-stu-id="facb0-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="facb0-394">hello spout**產生器**將隨機產生某些句子，並發出這些句子太**分隔器**。</span><span class="sxs-lookup"><span data-stu-id="facb0-394">hello spout **generator** will randomly generate some sentences, and emit these sentences too**splitter**.</span></span> <span data-ttu-id="facb0-395">hello 閃電**分隔器**會分割 hello 句子 toowords 和發出這些字太**計數器**閃電。</span><span class="sxs-lookup"><span data-stu-id="facb0-395">hello bolt **splitter** will split hello sentences toowords and emit these words too**counter** bolt.</span></span> <span data-ttu-id="facb0-396">hello 閃電"counter"會使用每個字組的字典 toorecord hello 發生次數。</span><span class="sxs-lookup"><span data-stu-id="facb0-396">hello bolt "counter" uses a dictionary toorecord hello occurrence number of each word.</span></span>

<span data-ttu-id="facb0-397">此範例有兩個規格檔：**HelloWorld.spec** 和 **HelloWorld\_EnableAck.spec**。</span><span class="sxs-lookup"><span data-stu-id="facb0-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="facb0-398">在 hello C\#程式碼，它可以找出是否藉由取得 hello pluginConf Java 來自啟用通知。</span><span class="sxs-lookup"><span data-stu-id="facb0-398">In hello C\# code, it can find out whether ack is enabled by getting hello pluginConf from Java side.</span></span>

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="facb0-399">Hello spout 中啟用通知時，字典有尚未 acked 使用的 toocache hello tuple。</span><span class="sxs-lookup"><span data-stu-id="facb0-399">In hello spout, if ack is enabled, a dictionary is used toocache hello tuples that have not been acked.</span></span> <span data-ttu-id="facb0-400">如果呼叫 Fail()，hello 失敗的 tuple 重新執行：</span><span class="sxs-lookup"><span data-stu-id="facb0-400">If Fail() is called, hello failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="facb0-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="facb0-401">HelloWorldTx</span></span>
<span data-ttu-id="facb0-402">hello **HelloWorldTx**範例將示範如何 tooimplement 交易式拓撲。</span><span class="sxs-lookup"><span data-stu-id="facb0-402">hello **HelloWorldTx** example demonstrates how tooimplement transactional topology.</span></span> <span data-ttu-id="facb0-403">它有一個名為 **generator** 的 spout，一個名為 **partial-count** 的批次 bolt，以及一個名為 **count-sum** 的認可 bolt。</span><span class="sxs-lookup"><span data-stu-id="facb0-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="facb0-404">另外還有三個預先建立的 txt 檔案︰**DataSource0.txt**、**DataSource1.txt**、**DataSource2.txt**。</span><span class="sxs-lookup"><span data-stu-id="facb0-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="facb0-405">在每個交易中，hello spout**產生器**會隨機選擇兩個檔案從 hello 預先建立的三個檔案，並發出 hello 兩個檔案名稱 toohello**部分計數**閃電。</span><span class="sxs-lookup"><span data-stu-id="facb0-405">In each transaction, hello spout **generator** will randomly choose two files from hello pre-created three files, and emit hello two file names toohello **partial-count** bolt.</span></span> <span data-ttu-id="facb0-406">hello 閃電**部分計數**會先收到 hello tuple，然後開啟 hello 檔案和計數 hello 數字從取得 hello 檔案名稱，這個檔案中，以及最後發出 hello 文字數字 toohello**計數總和**閃電。</span><span class="sxs-lookup"><span data-stu-id="facb0-406">hello bolt **partial-count** will first get hello file name from hello received tuple, then open hello file and count hello number of words in this file, and finally emit hello word number toohello **count-sum** bolt.</span></span> <span data-ttu-id="facb0-407">hello**計數總和**閃電將摘要說明 hello 總計數。</span><span class="sxs-lookup"><span data-stu-id="facb0-407">hello **count-sum** bolt will summarize hello total count.</span></span>

<span data-ttu-id="facb0-408">tooachieve**正好一次**語意、 hello 認可閃電**計數總和**需要 toojudge 是否在重新執行的交易。</span><span class="sxs-lookup"><span data-stu-id="facb0-408">tooachieve **exactly once** semantics, hello commit bolt **count-sum** need toojudge whether it is a replayed transaction.</span></span> <span data-ttu-id="facb0-409">在此範例中，它有一個靜態成員變數：</span><span class="sxs-lookup"><span data-stu-id="facb0-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="facb0-410">建立 ISCPBatchBolt 執行個體時，它會取得 hello`txAttempt`從輸入參數：</span><span class="sxs-lookup"><span data-stu-id="facb0-410">When an ISCPBatchBolt instance is created, it will get hello `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
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

<span data-ttu-id="facb0-411">當`FinishBatch()`呼叫時，hello`lastCommittedTxId`如果它不是重新執行的交易將會更新。</span><span class="sxs-lookup"><span data-stu-id="facb0-411">When `FinishBatch()` is called, hello `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="facb0-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="facb0-412">HybridTopology</span></span>
<span data-ttu-id="facb0-413">此拓撲包含 Java Spout 和 C\# Bolt。</span><span class="sxs-lookup"><span data-stu-id="facb0-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="facb0-414">它會使用 hello 預設序列化和還原序列化實作 SCP 平台所提供。</span><span class="sxs-lookup"><span data-stu-id="facb0-414">It uses hello default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="facb0-415">請 ref hello **HybridTopology.spec**中**範例\\HybridTopology** hello 規格檔案的詳細資訊，資料夾和**SubmitTopology.bat**的方式toospecify Java classpath。</span><span class="sxs-lookup"><span data-stu-id="facb0-415">Please ref hello **HybridTopology.spec** in **examples\\HybridTopology** folder for hello spec file details, and **SubmitTopology.bat** for how toospecify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="facb0-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="facb0-416">SCPHostDemo</span></span>
<span data-ttu-id="facb0-417">在本質上這個範例是 hello 與 HelloWorld 相同。</span><span class="sxs-lookup"><span data-stu-id="facb0-417">This example is hello same as HelloWorld in essence.</span></span> <span data-ttu-id="facb0-418">hello 只差別 hello 使用者程式碼會編譯為 DLL，並使用 SCPHost.exe 送出 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="facb0-418">hello only difference is that hello user code is compiled as DLL and hello topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="facb0-419">如需詳細說明，請 ref hello > 一節 「 SCP 主機模式 」。</span><span class="sxs-lookup"><span data-stu-id="facb0-419">Please ref hello section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="facb0-420">後續步驟</span><span class="sxs-lookup"><span data-stu-id="facb0-420">Next Steps</span></span>
<span data-ttu-id="facb0-421">建立使用 SCP 的 Storm 拓撲的範例，請參閱 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="facb0-421">For examples of Storm topologies created using SCP, see hello following:</span></span>

* [<span data-ttu-id="facb0-422">使用 Visual Studio 開發 Apache Storm on HDInsight 的 C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="facb0-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="facb0-423">利用 Storm on HDInsight 處理 Azure 事件中心的事件</span><span class="sxs-lookup"><span data-stu-id="facb0-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="facb0-424">在 C# Storm 拓樸中建立多個資料流</span><span class="sxs-lookup"><span data-stu-id="facb0-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="facb0-425">使用 Storm 拓撲從 Power Bi toovisualize 資料</span><span class="sxs-lookup"><span data-stu-id="facb0-425">Use Power Bi toovisualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="facb0-426">使用 Storm on HDInsight 處理事件中心的車輛感應器資料</span><span class="sxs-lookup"><span data-stu-id="facb0-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="facb0-427">擷取、 轉換及載入 (ETL) 從 Azure 事件中心 tooHBase</span><span class="sxs-lookup"><span data-stu-id="facb0-427">Extract, Transform, and Load (ETL) from Azure Event Hubs tooHBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="facb0-428">在 HDInsight 上使用 Storm 和 HBase 讓事件相互關聯</span><span class="sxs-lookup"><span data-stu-id="facb0-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)


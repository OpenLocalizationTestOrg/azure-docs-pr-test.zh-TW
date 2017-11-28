---
title: "Azure 事件中樞擷取概觀 | Microsoft Docs"
description: "使用事件中樞擷取來擷取遙測資料"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 9ae6aa57200b99f382c6e60565db9cfc69f1d3c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="b5ff7-103">Azure 事件中樞擷取</span><span class="sxs-lookup"><span data-stu-id="b5ff7-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="b5ff7-104">Azure 事件中樞擷取可讓您自動將事件中樞的串流資料傳遞到您選擇的 [Azure Blob 儲存體](https://azure.microsoft.com/services/storage/blobs/)或 [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) 帳戶，並另外增加了可指定時間或大小間隔的彈性。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-104">Azure Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to an [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with the added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="b5ff7-105">設定擷取的作業很快，因此執行時不需要系統管理成本，而且它可以針對事件中樞的[輸送量單位](event-hubs-features.md#capacity)自動進行調整。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-105">Setting up Capture is fast, there are no administrative costs to run it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="b5ff7-106">事件中樞擷取是將串流資料載入至 Azure 的最簡單方式，並可讓您專注於處理資料而非擷取資料。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-106">Event Hubs Capture is the easiest way to load streaming data into Azure, and enables you to focus on data processing rather than on data capture.</span></span>

<span data-ttu-id="b5ff7-107">事件中樞擷取可讓您在相同資料流上處理即時和批次型的管線。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-107">Event Hubs Capture enables you to process real-time and batch-based pipelines on the same stream.</span></span> <span data-ttu-id="b5ff7-108">這表示您可以建置會隨時間配合需求成長的解決方案。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="b5ff7-109">不論您現在是要建置著眼於未來即時處理的批次型系統，或想要為現有即時解決方案新增有效率的冷路徑，事件中樞擷取都可以讓使用串流資料變得更簡單。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want to add an efficient cold path to an existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="b5ff7-110">事件中樞擷取的運作方式</span><span class="sxs-lookup"><span data-stu-id="b5ff7-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="b5ff7-111">事件中樞是用於輸入遙測的時間保留持久緩衝區，類似於分散式記錄。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar to a distributed log.</span></span> <span data-ttu-id="b5ff7-112">在事件中樞調整大小的關鍵是 [資料分割取用者模型](event-hubs-features.md#partitions)。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-112">The key to scaling in Event Hubs is the [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="b5ff7-113">每個資料分割都是獨立的資料區段，可獨立取用。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="b5ff7-114">根據可設定的保留期限，此資料會隨時間而過時。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-114">Over time this data ages off, based on the configurable retention period.</span></span> <span data-ttu-id="b5ff7-115">因此，給定的事件中樞永遠不會「太滿」。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="b5ff7-116">事件中樞擷取可讓您指定自己的 Azure Blob 儲存體帳戶和容器，或是 Azure Data Lake Store 帳戶，可用來儲存擷取的資料。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-116">Event Hubs Capture enables you to specify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used to store the captured data.</span></span> <span data-ttu-id="b5ff7-117">這些帳戶可以和事件中樞位於相同區域，也可以位於另一個區域，從而新增至事件中樞擷取功能的彈性。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-117">These accounts can be in the same region as your event hub or in another region, adding to the flexibility of the Event Hubs Capture feature.</span></span>

<span data-ttu-id="b5ff7-118">擷取的資料會以 [Apache Avro][Apache Avro] 格式寫入，此為精簡、快速、二進位的格式，可使用內嵌結構描述提供豐富的資料結構。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="b5ff7-119">此格式廣泛運用在 Hadoop 生態系統、串流分析和 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-119">This format is widely used in the Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="b5ff7-120">關於使用 Avro 的詳細資訊可在本文稍後看到。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="b5ff7-121">擷取範圍</span><span class="sxs-lookup"><span data-stu-id="b5ff7-121">Capture windowing</span></span>

<span data-ttu-id="b5ff7-122">事件中樞擷取可讓您設定要控制擷取的範圍。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-122">Event Hubs Capture enables you to set up a window to control capturing.</span></span> <span data-ttu-id="b5ff7-123">此範圍是具有「先者勝出原則」的最小大小和時間組態，這表示所遇到的第一個觸發條件會導致擷取作業。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-123">This window is a minimum size and time configuration with a "first wins policy," meaning that the first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="b5ff7-124">如果您有一個 15 分鐘 100 MB 的擷取範圍，且傳送速率為每秒 1 MB，則大小範圍會比時間範圍更早觸發。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, the size window triggers before the time window.</span></span> <span data-ttu-id="b5ff7-125">每個分割區都會獨立擷取，並在擷取時寫入已完成的區塊 Blob，而且會以遇到擷取間隔的時間命名。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-125">Each partition captures independently and writes a completed block blob at the time of capture, named for the time at which the capture interval was encountered.</span></span> <span data-ttu-id="b5ff7-126">儲存體命名慣例如下︰</span><span class="sxs-lookup"><span data-stu-id="b5ff7-126">The storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-to-throughput-units"></a><span data-ttu-id="b5ff7-127">調整至輸送量單位</span><span class="sxs-lookup"><span data-stu-id="b5ff7-127">Scaling to throughput units</span></span>

<span data-ttu-id="b5ff7-128">事件中樞的流量會受到 [輸送量單位](event-hubs-features.md#capacity)控制。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="b5ff7-129">單一輸送量單位可允許每秒 1 MB 或每秒 1000 個事件的輸入，輸出則為此數量的兩倍。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="b5ff7-130">標準事件中樞可以設定 1-20 個輸送量單位，您可以透過增加配額的[支援要求][support request]購買更多單位。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="b5ff7-131">超過所購買輸送量單位的使用量將遭到節流。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="b5ff7-132">事件中樞擷取會直接從內部的事件中樞儲存體複製資料，略過輸送量單位輸出配額，並將輸出節省下來以供串流分析或 Spark 等其他處理讀取器使用。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-132">Event Hubs Capture copies data directly from the internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="b5ff7-133">一旦設定，事件中樞擷取會在您傳送第一個事件時自動執行，並且持續執行。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="b5ff7-134">為了讓下游處理更輕鬆地知道處理程序正在運作，事件中樞會在沒有資料時寫入空白檔案。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-134">To make it easier for your downstream processing to know that the process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="b5ff7-135">這個程序會提供可預測的頻率和標記，以供饋送給批次處理器。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="b5ff7-136">設定事件中樞擷取</span><span class="sxs-lookup"><span data-stu-id="b5ff7-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="b5ff7-137">您可以使用 [Azure 入口網站](https://portal.azure.com)或使用 Azure Resource Manager 範本，在建立事件中樞時設定擷取功能。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-137">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="b5ff7-138">如需詳細資訊，請參閱下列文章。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-138">For more information, see the following articles:</span></span>

- [<span data-ttu-id="b5ff7-139">使用 Azure 入口網站啟用事件中樞擷取功能</span><span class="sxs-lookup"><span data-stu-id="b5ff7-139">Enable Event Hubs Capture using the Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="b5ff7-140">使用 Azure Resource Manager 範本建立含有一個事件中樞的事件中樞命名空間並啟用擷取</span><span class="sxs-lookup"><span data-stu-id="b5ff7-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-the-captured-files-and-working-with-avro"></a><span data-ttu-id="b5ff7-141">瀏覽擷取檔案並使用 Avro</span><span class="sxs-lookup"><span data-stu-id="b5ff7-141">Exploring the captured files and working with Avro</span></span>

<span data-ttu-id="b5ff7-142">事件中樞擷取會以 Avro 格式建立檔案，如設定之時間範圍內所指定。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-142">Event Hubs Capture creates files in Avro format, as specified on the configured time window.</span></span> <span data-ttu-id="b5ff7-143">您可以在任何工具 (例如 [Azure 儲存體總管][Azure Storage Explorer]) 檢視這些檔案。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="b5ff7-144">您可以在本機下載檔案，以對其進行處理。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-144">You can download the files locally to work on them.</span></span>

<span data-ttu-id="b5ff7-145">事件中樞擷取所產生的檔案會有下列 Avro 結構描述︰</span><span class="sxs-lookup"><span data-stu-id="b5ff7-145">The files produced by Event Hubs Capture have the following Avro schema:</span></span>

![][3]

<span data-ttu-id="b5ff7-146">瀏覽 Avro 檔案的簡易方式是使用 Apache 所提供的 [Avro Tools][Avro Tools] jar。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-146">An easy way to explore Avro files is by using the [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="b5ff7-147">下載這個 jar 之後，您可以執行下列命令來查看特定 Avro 檔案的結構描述︰</span><span class="sxs-lookup"><span data-stu-id="b5ff7-147">After downloading this jar, you can see the schema of a specific Avro file by running the following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="b5ff7-148">此命令會傳回</span><span class="sxs-lookup"><span data-stu-id="b5ff7-148">This command returns</span></span>

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

<span data-ttu-id="b5ff7-149">您也可以使用 Avro Tools 將檔案轉換成 JSON 格式，並執行其他處理。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-149">You can also use Avro Tools to convert the file to JSON format and perform other processing.</span></span>

<span data-ttu-id="b5ff7-150">若要執行更進階的處理，請下載並安裝您所選平台適用的 Avro。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-150">To perform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="b5ff7-151">在本文撰寫當下，已有適用於 C、C++、C\#、Java、NodeJS、Perl、PHP、Python 和 Ruby 的實作。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-151">At the time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="b5ff7-152">Apache Avro 已完成適用於 [Java][Java] 和 [Python][Python] 的快速入門指南。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="b5ff7-153">您也可以閱讀[開始使用事件中樞擷取](event-hubs-capture-python.md)一文。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-153">You can also read the [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="b5ff7-154">事件中樞擷取的收費方式</span><span class="sxs-lookup"><span data-stu-id="b5ff7-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="b5ff7-155">事件中樞擷取的計量方式類似輸送量單位，屬於每小時的費用。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-155">Event Hubs Capture is metered similarly to throughput units: as an hourly charge.</span></span> <span data-ttu-id="b5ff7-156">其費用與命名空間所購買的輸送量單位數目成正比。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-156">The charge is directly proportional to the number of throughput units purchased for the namespace.</span></span> <span data-ttu-id="b5ff7-157">當輸送量單位增加和減少時，事件中樞擷取也會增加和減少以提供相符的效能。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease to provide matching performance.</span></span> <span data-ttu-id="b5ff7-158">計量會串聯地發生。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-158">The meters occur in tandem.</span></span> <span data-ttu-id="b5ff7-159">如需定價詳細資訊，請參閱[事件中樞定價](https://azure.microsoft.com/pricing/details/event-hubs/)。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b5ff7-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5ff7-160">Next steps</span></span>

<span data-ttu-id="b5ff7-161">事件中樞擷取是將資料載入 Azure 中最簡單的方式。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-161">Event Hubs Capture is the easiest way to get data into Azure.</span></span> <span data-ttu-id="b5ff7-162">使用 Azure Data Lake、Azure Data Factory 和 Azure HDInsight，即可使用您選擇的工具和平台，以您需要的規模執行批次處理和其他分析。</span><span class="sxs-lookup"><span data-stu-id="b5ff7-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="b5ff7-163">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="b5ff7-163">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="b5ff7-164">開始傳送和接收事件</span><span class="sxs-lookup"><span data-stu-id="b5ff7-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="b5ff7-165">[使用事件中樞的完整範例應用程式][sample application that uses Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="b5ff7-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="b5ff7-166">[事件中樞概觀][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="b5ff7-166">[Event Hubs overview][Event Hubs overview]</span></span>

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3

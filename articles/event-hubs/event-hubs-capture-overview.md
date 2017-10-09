---
title: "Azure 事件中心擷取 aaaOverview |Microsoft 文件"
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
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="a51df-103">Azure 事件中樞擷取</span><span class="sxs-lookup"><span data-stu-id="a51df-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="a51df-104">擷取 azure 事件中樞可讓您串流處理資料，在事件中心 tooan tooautomatically 傳送 hello [Azure Blob 儲存體](https://azure.microsoft.com/services/storage/blobs/)或[Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) hello 與您選擇的帳戶加入彈性指定時間或大小的間隔。</span><span class="sxs-lookup"><span data-stu-id="a51df-104">Azure Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooan [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with hello added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="a51df-105">設定擷取很快速、 有沒有它，而且它自動擴充的事件中心的管理成本 toorun[輸送量單位](event-hubs-features.md#capacity)。</span><span class="sxs-lookup"><span data-stu-id="a51df-105">Setting up Capture is fast, there are no administrative costs toorun it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="a51df-106">事件中心擷取 hello 串流到 Azure 中，資料最簡單方式 tooload 並提供您 toofocus 資料處理而不是在資料擷取。</span><span class="sxs-lookup"><span data-stu-id="a51df-106">Event Hubs Capture is hello easiest way tooload streaming data into Azure, and enables you toofocus on data processing rather than on data capture.</span></span>

<span data-ttu-id="a51df-107">擷取的事件中樞可讓您即時 tooprocess 和批次為基礎的管線，在 hello 相同的資料流。</span><span class="sxs-lookup"><span data-stu-id="a51df-107">Event Hubs Capture enables you tooprocess real-time and batch-based pipelines on hello same stream.</span></span> <span data-ttu-id="a51df-108">這表示您可以建置會隨時間配合需求成長的解決方案。</span><span class="sxs-lookup"><span data-stu-id="a51df-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="a51df-109">不論您要建置的角度未來的即時處理批次為基礎的系統，或者您想 tooadd 有效率的原始路徑 tooan 現有即時解決方案，事件中心擷取可以讓資料流資料更容易使用。</span><span class="sxs-lookup"><span data-stu-id="a51df-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want tooadd an efficient cold path tooan existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="a51df-110">事件中樞擷取的運作方式</span><span class="sxs-lookup"><span data-stu-id="a51df-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="a51df-111">事件中心是遙測 ingress，類似 tooa 分散式記錄的時間保留長期緩衝區。</span><span class="sxs-lookup"><span data-stu-id="a51df-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar tooa distributed log.</span></span> <span data-ttu-id="a51df-112">事件中心中的 hello 金鑰 tooscaling 為 hello[分割式取用者模型](event-hubs-features.md#partitions)。</span><span class="sxs-lookup"><span data-stu-id="a51df-112">hello key tooscaling in Event Hubs is hello [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="a51df-113">每個資料分割都是獨立的資料區段，可獨立取用。</span><span class="sxs-lookup"><span data-stu-id="a51df-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="a51df-114">經過一段時間關閉年齡 」 這項資料，根據 hello 可設定保留期限。</span><span class="sxs-lookup"><span data-stu-id="a51df-114">Over time this data ages off, based on hello configurable retention period.</span></span> <span data-ttu-id="a51df-115">因此，給定的事件中樞永遠不會「太滿」。</span><span class="sxs-lookup"><span data-stu-id="a51df-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="a51df-116">擷取的事件中樞可讓您 toospecify 您自己的 Azure Blob 儲存體帳戶和容器或 Azure Data Lake Store 帳戶，也就是使用的 toostore hello 擷取資料。</span><span class="sxs-lookup"><span data-stu-id="a51df-116">Event Hubs Capture enables you toospecify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used toostore hello captured data.</span></span> <span data-ttu-id="a51df-117">這些帳戶可以在 hello 是相同的區域，為事件中樞，或在另一個區域中，加入 toohello 彈性 hello 事件中心擷取功能。</span><span class="sxs-lookup"><span data-stu-id="a51df-117">These accounts can be in hello same region as your event hub or in another region, adding toohello flexibility of hello Event Hubs Capture feature.</span></span>

<span data-ttu-id="a51df-118">擷取的資料會以 [Apache Avro][Apache Avro] 格式寫入，此為精簡、快速、二進位的格式，可使用內嵌結構描述提供豐富的資料結構。</span><span class="sxs-lookup"><span data-stu-id="a51df-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="a51df-119">Hello Hadoop 生態系統、 資料流分析和 Azure Data Factory 中廣泛使用此格式。</span><span class="sxs-lookup"><span data-stu-id="a51df-119">This format is widely used in hello Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="a51df-120">關於使用 Avro 的詳細資訊可在本文稍後看到。</span><span class="sxs-lookup"><span data-stu-id="a51df-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="a51df-121">擷取範圍</span><span class="sxs-lookup"><span data-stu-id="a51df-121">Capture windowing</span></span>

<span data-ttu-id="a51df-122">事件中心擷取可讓您 tooset 向上視窗 toocontrol 擷取。</span><span class="sxs-lookup"><span data-stu-id="a51df-122">Event Hubs Capture enables you tooset up a window toocontrol capturing.</span></span> <span data-ttu-id="a51df-123">此視窗是最小值和 「 第一個 wins 原則，"表示第一個觸發程序發生原因的 hello 擷取作業的時間設定。</span><span class="sxs-lookup"><span data-stu-id="a51df-123">This window is a minimum size and time configuration with a "first wins policy," meaning that hello first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="a51df-124">如果您有十五分鐘，100 MB 擷取視窗和 hello 大小視窗觸發程序之前 hello 時段每秒傳送 1 MB。</span><span class="sxs-lookup"><span data-stu-id="a51df-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, hello size window triggers before hello time window.</span></span> <span data-ttu-id="a51df-125">每個資料分割會獨立擷取，並將已完成的區塊 blob 時擷取的 hello 名為 hello 在哪一個 hello 遇到擷取間隔的時間。</span><span class="sxs-lookup"><span data-stu-id="a51df-125">Each partition captures independently and writes a completed block blob at hello time of capture, named for hello time at which hello capture interval was encountered.</span></span> <span data-ttu-id="a51df-126">hello 儲存體命名慣例如下所示：</span><span class="sxs-lookup"><span data-stu-id="a51df-126">hello storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a><span data-ttu-id="a51df-127">縮放比例 toothroughput 單位</span><span class="sxs-lookup"><span data-stu-id="a51df-127">Scaling toothroughput units</span></span>

<span data-ttu-id="a51df-128">事件中樞的流量會受到 [輸送量單位](event-hubs-features.md#capacity)控制。</span><span class="sxs-lookup"><span data-stu-id="a51df-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="a51df-129">單一輸送量單位可允許每秒 1 MB 或每秒 1000 個事件的輸入，輸出則為此數量的兩倍。</span><span class="sxs-lookup"><span data-stu-id="a51df-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="a51df-130">標準事件中樞可以設定 1-20 個輸送量單位，您可以透過增加配額的[支援要求][support request]購買更多單位。</span><span class="sxs-lookup"><span data-stu-id="a51df-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="a51df-131">超過所購買輸送量單位的使用量將遭到節流。</span><span class="sxs-lookup"><span data-stu-id="a51df-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="a51df-132">略過輸送量單位輸出配額及其他處理的讀取器，例如資料流分析或 Spark 儲存您的輸出事件中樞擷取複製直接從 hello 內部事件中心儲存體的資料。</span><span class="sxs-lookup"><span data-stu-id="a51df-132">Event Hubs Capture copies data directly from hello internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="a51df-133">一旦設定，事件中樞擷取會在您傳送第一個事件時自動執行，並且持續執行。</span><span class="sxs-lookup"><span data-stu-id="a51df-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="a51df-134">toomake 輕鬆您下游處理 tooknow hello 程序運作時，事件中心寫入空白檔案，當沒有資料。</span><span class="sxs-lookup"><span data-stu-id="a51df-134">toomake it easier for your downstream processing tooknow that hello process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="a51df-135">這個程序會提供可預測的頻率和標記，以供饋送給批次處理器。</span><span class="sxs-lookup"><span data-stu-id="a51df-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="a51df-136">設定事件中樞擷取</span><span class="sxs-lookup"><span data-stu-id="a51df-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="a51df-137">您可以在 hello 事件中心建立期間使用 hello 設定擷取[Azure 入口網站](https://portal.azure.com)，或使用 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="a51df-137">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="a51df-138">如需詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="a51df-138">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="a51df-139">啟用事件中心擷取使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a51df-139">Enable Event Hubs Capture using hello Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="a51df-140">使用 Azure Resource Manager 範本建立含有一個事件中樞的事件中樞命名空間並啟用擷取</span><span class="sxs-lookup"><span data-stu-id="a51df-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a><span data-ttu-id="a51df-141">瀏覽 hello 擷取檔案及使用 Avro</span><span class="sxs-lookup"><span data-stu-id="a51df-141">Exploring hello captured files and working with Avro</span></span>

<span data-ttu-id="a51df-142">事件中心擷取 Avro 格式，如同指定 hello 設定時間間隔中建立檔案。</span><span class="sxs-lookup"><span data-stu-id="a51df-142">Event Hubs Capture creates files in Avro format, as specified on hello configured time window.</span></span> <span data-ttu-id="a51df-143">您可以在任何工具 (例如 [Azure 儲存體總管][Azure Storage Explorer]) 檢視這些檔案。</span><span class="sxs-lookup"><span data-stu-id="a51df-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="a51df-144">您可以下載 hello 檔案在本機 toowork 它們。</span><span class="sxs-lookup"><span data-stu-id="a51df-144">You can download hello files locally toowork on them.</span></span>

<span data-ttu-id="a51df-145">所產生的事件中樞擷取的 hello 檔案具有下列 Avro 結構描述的 hello:</span><span class="sxs-lookup"><span data-stu-id="a51df-145">hello files produced by Event Hubs Capture have hello following Avro schema:</span></span>

![][3]

<span data-ttu-id="a51df-146">輕鬆 tooexplore Avro 檔案是使用 hello [Avro 工具][ Avro Tools] apache 的 jar。</span><span class="sxs-lookup"><span data-stu-id="a51df-146">An easy way tooexplore Avro files is by using hello [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="a51df-147">下載這個 jar 之後, 您可以藉由執行下列命令的 hello 看到 hello 結構描述的特定 Avro 檔案：</span><span class="sxs-lookup"><span data-stu-id="a51df-147">After downloading this jar, you can see hello schema of a specific Avro file by running hello following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="a51df-148">此命令會傳回</span><span class="sxs-lookup"><span data-stu-id="a51df-148">This command returns</span></span>

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

<span data-ttu-id="a51df-149">您也可以使用 Avro 工具 tooconvert hello 檔案 tooJSON 格式，以及執行其他處理。</span><span class="sxs-lookup"><span data-stu-id="a51df-149">You can also use Avro Tools tooconvert hello file tooJSON format and perform other processing.</span></span>

<span data-ttu-id="a51df-150">tooperform 更進階的處理，下載並安裝您所選擇的平台 Avro。</span><span class="sxs-lookup"><span data-stu-id="a51df-150">tooperform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="a51df-151">在 hello 撰寫本文時，有可用的實作 C、 c + +、 C\#、 Java、 NodeJS、 Perl、 PHP、 Python 和 Ruby。</span><span class="sxs-lookup"><span data-stu-id="a51df-151">At hello time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="a51df-152">Apache Avro 已完成適用於 [Java][Java] 和 [Python][Python] 的快速入門指南。</span><span class="sxs-lookup"><span data-stu-id="a51df-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="a51df-153">您也可以讀取 hello[開始使用事件中心擷取](event-hubs-capture-python.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="a51df-153">You can also read hello [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="a51df-154">事件中樞擷取的收費方式</span><span class="sxs-lookup"><span data-stu-id="a51df-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="a51df-155">事件中心擷取計量付費同樣 toothroughput 單位： 為每小時的費用。</span><span class="sxs-lookup"><span data-stu-id="a51df-155">Event Hubs Capture is metered similarly toothroughput units: as an hourly charge.</span></span> <span data-ttu-id="a51df-156">hello 費用是與呈現直接正比 toohello hello 命名空間所購買的輸送量單位數目。</span><span class="sxs-lookup"><span data-stu-id="a51df-156">hello charge is directly proportional toohello number of throughput units purchased for hello namespace.</span></span> <span data-ttu-id="a51df-157">增加和減少輸送量單位時，事件中心擷取公尺增加，並降低 tooprovide 相符的效能。</span><span class="sxs-lookup"><span data-stu-id="a51df-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease tooprovide matching performance.</span></span> <span data-ttu-id="a51df-158">hello 公尺會一起發生。</span><span class="sxs-lookup"><span data-stu-id="a51df-158">hello meters occur in tandem.</span></span> <span data-ttu-id="a51df-159">如需定價詳細資訊，請參閱[事件中樞定價](https://azure.microsoft.com/pricing/details/event-hubs/)。</span><span class="sxs-lookup"><span data-stu-id="a51df-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a51df-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a51df-160">Next steps</span></span>

<span data-ttu-id="a51df-161">擷取的事件中樞是 hello 最簡單方式 tooget 資料至 Azure。</span><span class="sxs-lookup"><span data-stu-id="a51df-161">Event Hubs Capture is hello easiest way tooget data into Azure.</span></span> <span data-ttu-id="a51df-162">使用 Azure Data Lake、Azure Data Factory 和 Azure HDInsight，即可使用您選擇的工具和平台，以您需要的規模執行批次處理和其他分析。</span><span class="sxs-lookup"><span data-stu-id="a51df-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="a51df-163">您可以進一步了解事件中心瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="a51df-163">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="a51df-164">開始傳送和接收事件</span><span class="sxs-lookup"><span data-stu-id="a51df-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="a51df-165">[使用事件中樞的完整範例應用程式][sample application that uses Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="a51df-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="a51df-166">[事件中樞概觀][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="a51df-166">[Event Hubs overview][Event Hubs overview]</span></span>

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

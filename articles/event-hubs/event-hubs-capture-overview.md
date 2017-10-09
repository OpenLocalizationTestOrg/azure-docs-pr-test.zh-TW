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
# <a name="azure-event-hubs-capture"></a>Azure 事件中樞擷取

擷取 azure 事件中樞可讓您串流處理資料，在事件中心 tooan tooautomatically 傳送 hello [Azure Blob 儲存體](https://azure.microsoft.com/services/storage/blobs/)或[Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) hello 與您選擇的帳戶加入彈性指定時間或大小的間隔。 設定擷取很快速、 有沒有它，而且它自動擴充的事件中心的管理成本 toorun[輸送量單位](event-hubs-features.md#capacity)。 事件中心擷取 hello 串流到 Azure 中，資料最簡單方式 tooload 並提供您 toofocus 資料處理而不是在資料擷取。

擷取的事件中樞可讓您即時 tooprocess 和批次為基礎的管線，在 hello 相同的資料流。 這表示您可以建置會隨時間配合需求成長的解決方案。 不論您要建置的角度未來的即時處理批次為基礎的系統，或者您想 tooadd 有效率的原始路徑 tooan 現有即時解決方案，事件中心擷取可以讓資料流資料更容易使用。

## <a name="how-event-hubs-capture-works"></a>事件中樞擷取的運作方式

事件中心是遙測 ingress，類似 tooa 分散式記錄的時間保留長期緩衝區。 事件中心中的 hello 金鑰 tooscaling 為 hello[分割式取用者模型](event-hubs-features.md#partitions)。 每個資料分割都是獨立的資料區段，可獨立取用。 經過一段時間關閉年齡 」 這項資料，根據 hello 可設定保留期限。 因此，給定的事件中樞永遠不會「太滿」。

擷取的事件中樞可讓您 toospecify 您自己的 Azure Blob 儲存體帳戶和容器或 Azure Data Lake Store 帳戶，也就是使用的 toostore hello 擷取資料。 這些帳戶可以在 hello 是相同的區域，為事件中樞，或在另一個區域中，加入 toohello 彈性 hello 事件中心擷取功能。

擷取的資料會以 [Apache Avro][Apache Avro] 格式寫入，此為精簡、快速、二進位的格式，可使用內嵌結構描述提供豐富的資料結構。 Hello Hadoop 生態系統、 資料流分析和 Azure Data Factory 中廣泛使用此格式。 關於使用 Avro 的詳細資訊可在本文稍後看到。

### <a name="capture-windowing"></a>擷取範圍

事件中心擷取可讓您 tooset 向上視窗 toocontrol 擷取。 此視窗是最小值和 「 第一個 wins 原則，"表示第一個觸發程序發生原因的 hello 擷取作業的時間設定。 如果您有十五分鐘，100 MB 擷取視窗和 hello 大小視窗觸發程序之前 hello 時段每秒傳送 1 MB。 每個資料分割會獨立擷取，並將已完成的區塊 blob 時擷取的 hello 名為 hello 在哪一個 hello 遇到擷取間隔的時間。 hello 儲存體命名慣例如下所示：

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a>縮放比例 toothroughput 單位

事件中樞的流量會受到 [輸送量單位](event-hubs-features.md#capacity)控制。 單一輸送量單位可允許每秒 1 MB 或每秒 1000 個事件的輸入，輸出則為此數量的兩倍。 標準事件中樞可以設定 1-20 個輸送量單位，您可以透過增加配額的[支援要求][support request]購買更多單位。 超過所購買輸送量單位的使用量將遭到節流。 略過輸送量單位輸出配額及其他處理的讀取器，例如資料流分析或 Spark 儲存您的輸出事件中樞擷取複製直接從 hello 內部事件中心儲存體的資料。

一旦設定，事件中樞擷取會在您傳送第一個事件時自動執行，並且持續執行。 toomake 輕鬆您下游處理 tooknow hello 程序運作時，事件中心寫入空白檔案，當沒有資料。 這個程序會提供可預測的頻率和標記，以供饋送給批次處理器。

## <a name="setting-up-event-hubs-capture"></a>設定事件中樞擷取

您可以在 hello 事件中心建立期間使用 hello 設定擷取[Azure 入口網站](https://portal.azure.com)，或使用 Azure Resource Manager 範本。 如需詳細資訊，請參閱下列文章 hello:

- [啟用事件中心擷取使用 hello Azure 入口網站](event-hubs-capture-enable-through-portal.md)
- [使用 Azure Resource Manager 範本建立含有一個事件中樞的事件中樞命名空間並啟用擷取](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a>瀏覽 hello 擷取檔案及使用 Avro

事件中心擷取 Avro 格式，如同指定 hello 設定時間間隔中建立檔案。 您可以在任何工具 (例如 [Azure 儲存體總管][Azure Storage Explorer]) 檢視這些檔案。 您可以下載 hello 檔案在本機 toowork 它們。

所產生的事件中樞擷取的 hello 檔案具有下列 Avro 結構描述的 hello:

![][3]

輕鬆 tooexplore Avro 檔案是使用 hello [Avro 工具][ Avro Tools] apache 的 jar。 下載這個 jar 之後, 您可以藉由執行下列命令的 hello 看到 hello 結構描述的特定 Avro 檔案：

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

此命令會傳回

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

您也可以使用 Avro 工具 tooconvert hello 檔案 tooJSON 格式，以及執行其他處理。

tooperform 更進階的處理，下載並安裝您所選擇的平台 Avro。 在 hello 撰寫本文時，有可用的實作 C、 c + +、 C\#、 Java、 NodeJS、 Perl、 PHP、 Python 和 Ruby。

Apache Avro 已完成適用於 [Java][Java] 和 [Python][Python] 的快速入門指南。 您也可以讀取 hello[開始使用事件中心擷取](event-hubs-capture-python.md)發行項。

## <a name="how-event-hubs-capture-is-charged"></a>事件中樞擷取的收費方式

事件中心擷取計量付費同樣 toothroughput 單位： 為每小時的費用。 hello 費用是與呈現直接正比 toohello hello 命名空間所購買的輸送量單位數目。 增加和減少輸送量單位時，事件中心擷取公尺增加，並降低 tooprovide 相符的效能。 hello 公尺會一起發生。 如需定價詳細資訊，請參閱[事件中樞定價](https://azure.microsoft.com/pricing/details/event-hubs/)。 

## <a name="next-steps"></a>後續步驟

擷取的事件中樞是 hello 最簡單方式 tooget 資料至 Azure。 使用 Azure Data Lake、Azure Data Factory 和 Azure HDInsight，即可使用您選擇的工具和平台，以您需要的規模執行批次處理和其他分析。

您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [開始傳送和接收事件](event-hubs-dotnet-framework-getstarted-send.md)
* [使用事件中樞的完整範例應用程式][sample application that uses Event Hubs]
* [事件中樞概觀][Event Hubs overview]

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

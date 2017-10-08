---
title: "與 HDInsight 上的 Apache Storm aaaProcess vehicle 感應器資料 |Microsoft 文件"
description: "深入了解如何從事件中樞在 HDInsight 上使用 Apache Storm tooprocess vehicle 感應器資料。 新增模型資料從 Azure Cosmos DB，以及儲存輸出 toostorage。"
services: hdinsight,documentdb,notification-hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 78980635-8bef-4c33-96c3-fae50e932e31
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/03/2017
ms.author: larryfr
ms.openlocfilehash: 8f7b1dbb9072e095ea32160bb731bedd071288af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="process-vehicle-sensor-data-from-azure-event-hubs-using-apache-storm-on-hdinsight"></a>使用 Apache Storm on HDInsight 處理 Azure 事件中樞的車輛感應器資料

深入了解如何從 Azure 事件中樞在 HDInsight 上使用 Apache Storm tooprocess vehicle 感應器資料。 這個範例會從 Azure 事件中心讀取感應器資料，藉由參考資料儲存在 Azure Cosmos DB 豐富 hello 資料。 hello 資料會儲存到 Azure 儲存體使用 hello Hadoop 檔案系統 (HDFS)。

![HDInsight 和 hello 物聯網 (IoT) 架構圖表](./media/hdinsight-storm-iot-eventhub-documentdb/iot.png)

## <a name="overview"></a>概觀

加入 toovehicles 感應器可讓您根據歷程記錄資料的趨勢 toopredict 設備問題。 它也可讓您 toomake 改進 toofuture 版本使用模式分析為基礎。 您必須是能夠 tooquickly，並且有效率地載入 hello 資料從所有車輛 Hadoop MapReduce 處理發生之前。 此外，您可能希望 toodo 分析嚴重失敗的路徑 （引擎溫度、 brakes 等） 的即時。

Azure 事件中心是建置 toohandle hello 大量的磁碟區的感應器所產生的資料。 Apache Storm 之前，可以使用的 tooload 和處理序 hello 資料儲存到 HDFS。

## <a name="solution"></a>方案

感應器會記錄引擎溫度、周圍溫度和車輛速度的遙測資料。 然後，資料會傳送 tooEvent 中心以及 hello 汽車的汽車識別號碼 (VIN) 和時間戳記。 從該處，Storm 拓撲上 Apache Storm，HDInsight 叢集上執行讀取 hello 資料、 加以處理，並將它儲存到 HDFS。

在處理期間，hello VIN 就是從 Cosmos DB 使用的 tooretrieve 模型資訊。 這項資料會加入 toohello 資料流，再儲存。

hello hello Storm 拓撲中使用的元件如下：

* **EventHubSpout** - 讀取 Azure 事件中心的資料
* **TypeConversionBolt** -將 hello tuple，其中包含下列感應器資料的 hello 事件中心從 JSON 字串：
    * Engine temperature
    * 周圍溫度
    * 速度
    * VIN
    * Timestamp
* **DataReferencBolt** -從 Cosmos DB 使用 hello VIN 查閱 hello vehicle 模型
* **WasbStoreBolt** -存放區 hello 資料 tooHDFS （Azure 儲存體）

下列映像的 hello 是此解決方案的圖表：

![Storm 拓撲](./media/hdinsight-storm-iot-eventhub-documentdb/iottopology.png)

## <a name="implementation"></a>實作

完成、 自動解決方案，此案例中是可用的 hello 一部分[HDInsight-Storm-範例](https://github.com/hdinsight/hdinsight-storm-examples)GitHub 上的儲存機制。 toouse 此範例中，遵循 hello 步驟在 hello [IoTExample 讀我檔案。MD](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md)。

## <a name="next-steps"></a>後續步驟

若需更多範例 Storm 拓撲，請參閱 [Storm on HDInsight 上的範例拓撲](hdinsight-storm-example-topology.md)。


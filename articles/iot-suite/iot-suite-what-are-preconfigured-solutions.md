---
title: "aaaAzure IoT 預先設定的解決方案 |Microsoft 文件"
description: "Hello Azure IoT 描述預先設定的解決方案與它們的架構與連結 tooadditional 資源。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 59009f37-9ba0-4e17-a189-7ea354a858a2
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: bd059d08ab458fdb0b6f49b3ac469db930dab09e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-azure-iot-suite-preconfigured-solutions"></a>Hello 預先設定的 Azure IoT 套件解決方案有哪些？

hello 預先設定的 Azure IoT 套件解決方案是常見的 IoT 解決方案模式，您可以部署 tooAzure 使用您的訂用帳戶的實作。 您可以使用預先設定的 hello 解決方案：

* 做為您的 IoT 解決方案的起點。
* toolearn 有關 IoT 解決方案設計和開發中常見的模式。

每個預先設定的解決方案是使用模擬裝置 toogenerate 遙測完整的端對端實作。

您可以下載 hello 完整的程式碼 toocustomize 並擴充 hello 方案 toomeet IoT 您的特定需求。

> [!NOTE]
> hello toodeploy 其中一個預先設定的解決方案，請瀏覽[Microsoft Azure IoT 套件][lnk-azureiotsuite]。 hello 文章[開始與 hello 預先設定的 IoT 解決方案][ lnk-getstarted-preconfigured]提供 toodeploy 並執行的其中 hello 解決方案的詳細資訊。

hello 下表顯示 hello 解決方案將 toospecific IoT 功能的對應：

| 方案 | 資料擷取 | 裝置身分識別 | 裝置管理 | 命令與控制 | 執行和動作 | 預測性分析 |
| --- | --- | --- | --- | --- | --- | --- |
| [遠端監視][lnk-getstarted-preconfigured] |是 |是 |是 |是 |是 |- |
| [預測性維護][lnk-predictive-maintenance] |是 |是 |- |是 |是 |是 |
| [連線的處理站][lnk-getstarted-factory] |是 |是 |是 |是 |是 |- |

* *擷取資料*： 在標尺 toohello 雲端的資料輸入。
* *裝置識別身分*： 管理裝置的唯一身分識別，並控制裝置存取 toohello 解決方案。
* *裝置管理*：管理裝置中繼資料，以及執行裝置重新開機和韌體升級等作業。
* *命令和控制*: toocause hello 裝置 tootake 動作，傳送訊息 tooa 裝置從 hello 雲端。
* *規則和動作*: tooact 上特定裝置到雲端資料，hello 方案後端所使用的規則。
* *預測分析*: hello 方案後端會分析裝置到雲端資料 toopredict 時應該會發生特定動作。 例如，分析飛機引擎遙測 toodetermine 引擎維護時到期。

## <a name="remote-monitoring-preconfigured-solution-overview"></a>遠端監視預先設定解決方案概觀

我們已選擇 toodiscuss hello 本文章中的遠端監視預先設定的解決方案，因為它會說明許多 hello 其他方案共用的一般設計元素。

hello 下列圖表說明 hello 的 hello 遠端監視解決方案的重要元素。 hello 下列各節提供有關這些元素的詳細資訊。

![遠端監視預先設定解決方案架構][img-remote-monitoring-arch]

## <a name="devices"></a>裝置

當您部署的 hello 遠端監視預先設定的解決方案時，四個模擬的裝置會預先佈建，模擬冷卻裝置 hello 方案中。 這些模擬裝置具有可發出遙測資訊的內建溫度和溼度模型。 包含這些模擬裝置是為了：

- 說明 hello 的透過 hello 解決方案的端對端資料流程。
- 提供便利的遙測資料來源。
- 如果您是使用做為起點的 hello 方案的自訂實作的後端開發人員，提供目標的方法或命令。

hello 方案中的 hello 模擬裝置可回應 toohello 下列雲端到裝置通訊：

- *方法 ([直接方法][lnk-direct-methods])*： 其中連接的裝置是預期的 toorespond 立即的雙向通訊方法。
- *命令 （雲端到裝置訊息）*： 其中裝置 hello 命令會從擷取長期佇列的單向通訊方法。

如需這些不同方法的比較，請參閱[雲端到裝置通訊指引][lnk-c2d-guidance]。

當裝置第一次連接 tooIoT 中樞 hello 預先設定的方案中時，它會傳送裝置資訊訊息 toohello 集線器。 此訊息會列舉 hello 回應 hello 裝置的方法。 Hello 遠端監視預先設定的解決方案，在模擬的裝置會支援這些方法：

* *起始韌體更新*： 這個方法會起始非同步工作上 hello 裝置 tooperform 軔體更新。 hello 非同步工作會使用報告的屬性 toodeliver 狀態更新 toohello 方案的儀表板。
* *重新啟動*： 這個方法會導致 hello 模擬裝置 tooreboot。
* *FactoryReset*： 這個方法會觸發原廠重設 hello 模擬的裝置。

當裝置第一次連接 tooIoT 中樞 hello 預先設定的方案中時，它會傳送裝置資訊訊息 toohello 集線器。 此訊息會列舉 hello 裝置可回應 hello 命令。 Hello 遠端監視預先設定的解決方案，在模擬的裝置會支援這些命令：

* *Ping 裝置*: hello 裝置回應 toothis 命令確認。 此命令可用於檢查該 hello 裝置仍然使用中並在接聽。
* *啟動遙測*： 指示 hello 裝置 toostart 傳送遙測。
* *停止遙測*： 指示 hello 裝置 toostop 傳送遙測。
* *變更設定點溫度*： 控制項 hello 模擬的溫度遙測值 hello 裝置傳送。 此命令可用來測試後端邏輯。
* *診斷遙測*： 控制是否 hello 裝置應該當做遙測傳送嗨外部溫度。
* *變更裝置狀態*: hello 裝置狀態的中繼資料屬性 hello 裝置報告的設定。 此命令可用來測試後端邏輯。

您可以加入多個發出 hello 的模擬的裝置 toohello 方案相同的遙測和回應 toohello 相同的方法和命令。

此外 tooresponding toocommands 和方法，hello 解決方案使用[裝置雙][lnk-device-twin]。 裝置使用裝置雙 tooreport 屬性值 toohello 方案後端。 hello 方案儀表板會在裝置上使用裝置雙 tooset toonew 預期屬性值。 比方說，hello 韌體更新程序模擬的 hello 裝置報告期間的 hello hello 狀態更新使用報告的屬性。

## <a name="iot-hub"></a>IoT 中樞

在此預先設定的解決方案，hello IoT 中樞執行個體對應 toohello*雲端閘道*一般[IoT 解決方案架構][lnk-what-is-azure-iot]。

IoT 中心會從單一端點的 hello 裝置接收遙測。 IoT 中心也會維護每個裝置可以在其中擷取傳送 tooit hello 命令的裝置特定端點。

hello IoT 中樞可讓您可透過 hello 服務端遙測讀取端點收到 hello 遙測。

IoT 中樞的 hello 裝置管理功能可讓您 toomanage hello 方案入口網站與排程工作，例如執行作業從您裝置的屬性：

- 重新啟動裝置
- 變更裝置狀態
- 韌體更新

## <a name="azure-stream-analytics"></a>Azure 串流分析

hello 預先設定的解決方案會使用三個[Azure Stream Analytics] [ lnk-asa] (ASA) 作業 toofilter hello 遙測資料流從 hello 裝置：

* *DeviceInfo 作業*-輸出資料 tooan 事件中樞，將裝置註冊特定的訊息 toohello 方案裝置登錄的路由。 此裝置登錄是 Azure Cosmos DB 資料庫。 這些訊息會傳送第一次連接裝置時或在回應 tooa**變更裝置狀態**命令。
* *遙測作業*-傳送所有原始遙測 tooAzure blob 儲存體冷儲存體和計算 hello 方案儀表板中顯示的遙測彙總。
* *規則工作*-篩選 hello 超過任何規則的臨界值的值的遙測資料流，並輸出 hello 資料 tooan 事件中心。 當規則引發時，hello 方案入口網站儀表板檢視會顯示此事件為 hello 警示歷程記錄資料表中的新資料列。 這些規則也會觸發的動作取決於 hello 上定義的 hello 設定**規則**和**動作**hello 方案入口網站中的檢視。

在此預先設定的解決方案，hello ASA 工作表單一部分 toohello **IoT 解決方案後端**一般[IoT 解決方案架構][lnk-what-is-azure-iot]。

## <a name="event-processor"></a>事件處理器

在此預先設定的解決方案，hello 事件處理器的一部分 hello **IoT 解決方案後端**一般[IoT 解決方案架構][lnk-what-is-azure-iot]。

hello **DeviceInfo**和**規則**ASA 工作傳送傳遞其輸出 tooEvent 集線器 tooother 後端服務。 hello 解決方案會使用[EventProcessorHost] [ lnk-event-processor] ，以執行執行個體[WebJob][lnk-web-job]，從這些事件中樞 tooread hello 訊息。 hello **EventProcessorHost**使用：
- hello **DeviceInfo**資料 tooupdate hello hello Cosmos DB 資料庫中的裝置資料。
- hello**規則**資料 tooinvoke hello 邏輯應用程式和更新 hello 警示會顯示 hello 方案入口網站。

## <a name="device-identity-registry-device-twin-and-cosmos-db"></a>裝置身分識別登錄、裝置對應項及 Cosmos DB

每個 IoT 中樞都包括儲存裝置金鑰的[裝置身分識別登錄][lnk-identity-registry]。 IoT 中樞會使用這項資訊驗證裝置-裝置必須註冊，並且具有有效的索引鍵，才能連線 toohello 中樞。

A[裝置兩個][ lnk-device-twin]是 JSON 文件受 hello IoT 中樞。 裝置的裝置對應項包含：

- 傳送 hello 裝置 toohello 集線器所報告的屬性。 您可以在 hello 方案入口網站中檢視這些屬性。
- 您想 toosend toohello 裝置所需的屬性。 您可以在 hello 方案入口網站中設定這些屬性。
- 只在兩個-裝置 hello 和 hello 裝置上不存在的標記。 您可以使用這些標記 toofilter 清單的裝置 hello 方案入口網站中。

這個解決方案會使用裝置雙 toomanage 裝置中繼資料。 hello 解決方案也會使用 Cosmos DB 資料庫 toostore 其他解決方案專用裝置 」 資料，例如支援的每個裝置與 hello 命令歷程記錄的 hello 命令。

hello 解決方案也必須保留 hello 裝置身分登錄與 hello 內容 hello Cosmos DB 資料庫的同步處理檔案中的 hello 資訊。 hello **EventProcessorHost**使用 hello 資料**DeviceInfo** stream analytics 工作 toomanage hello 同步處理。

## <a name="solution-portal"></a>解決方案入口網站

![解決方案入口網站][img-dashboard]

hello 方案入口網站是網頁的 UI，是部署 toohello 雲端做為預先設定的 hello 方案的一部分。 可以讓您：

* 檢視儀表板中的遙測和警示歷程記錄。
* 佈建新裝置。
* 管理和監視裝置。
* 傳送命令 toospecific 裝置。
* 在特定裝置上叫用方法。
* 管理規則和動作。
* 排程作業 toorun 一或多個裝置上。

此預先設定的解決方案中 hello 方案入口網站的一部分 hello **IoT 解決方案後端**而一部分 hello**處理與商務連線**中典型的 hello[的 IoT 解決方案架構][lnk-what-is-azure-iot]。

## <a name="next-steps"></a>後續步驟

如需 IoT 解決方案架構的詳細資訊，請參閱 [Microsoft Azure IoT 服務 ︰參考架構][lnk-refarch]。

現在您已經知道哪些預先設定的解決方案是，您可以開始部署 hello*遠端監視*預先設定的方案：[開始使用預先設定的 hello 解決方案][ lnk-getstarted-preconfigured].

[img-remote-monitoring-arch]: ./media/iot-suite-what-are-preconfigured-solutions/remote-monitoring-arch1.png
[img-dashboard]: ./media/iot-suite-what-are-preconfigured-solutions/dashboard.png
[lnk-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-event-processor]: ../event-hubs/event-hubs-programming-guide.md#event-processor-host
[lnk-web-job]: ../app-service-web/web-sites-create-web-jobs.md
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-getstarted-preconfigured]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-getstarted-factory]: iot-suite-connected-factory-overview.md

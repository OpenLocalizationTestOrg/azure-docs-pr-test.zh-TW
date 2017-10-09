---
title: "aaaConnected factory Azure IoT 套件方案逐步解說 |Microsoft 文件"
description: "Hello 預先設定的 Azure IoT 解決方案描述連接處理站和其架構。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a>連線處理站預先設定的解決方案逐步解說

hello IoT 套件連線 factory[預先設定的解決方案][ lnk-preconfigured-solutions]是端對端工業解決方案的實作的：

* 連接 tooboth 模擬工業 OPC UA 伺服器以執行模擬原廠生產線條，以及實際 OPC UA 伺服器裝置的裝置。 如需有關 OPC UA 的詳細資訊，請參閱 hello[連接工廠常見問題集](iot-suite-faq-cf.md)。
* 顯示作業 KPI 和這些裝置與生產線的 OEE。
* 示範如何以雲端為基礎的應用程式可能是使用的 toointeract 與 OPC UA 伺服器系統。
* 可讓您 tooconnect 自己 OPC UA 伺服器裝置。
* 可讓您 toobrowse 和修改 hello OPC UA 伺服器資料。
* 整合與 hello Azure 時間數列 Insights (TSI) 服務 tooprovide OPC UA 伺服器 hello 資料的自訂的檢視。

您可以做為起點使用 hello 解決方案，為您自己的實作和[自訂][ lnk-customize]它 toomeet 特定的業務需求。

這篇文章會引導您完成 hello 索引鍵的某些項目連接的 hello factory 方案 tooenable 您 toounderstand 它的運作方式。 這項知識能協助您︰

* 疑難排解 hello 方案中的問題。
* 規劃如何 toocustomize toohello 方案 toomeet 您自己的特定需求。
* 設計使用 Azure 服務的 IoT 解決方案。

如需詳細資訊，請參閱 hello[連接工廠常見問題集](iot-suite-faq-cf.md)。

## <a name="logical-architecture"></a>邏輯架構

下列圖表中的 hello 概述 hello 邏輯解決方案元件的預先設定的 hello:

![連線處理站的邏輯架構][connected-factory-logical]

## <a name="communication-patterns"></a>通訊模式

hello 解決方案使用 hello [OPC UA Pub/Sub 規格](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/)toosend OPC UA 遙測資料 tooIoT 中樞 JSON 格式。 hello 解決方案使用 hello [OPC 發行者](https://github.com/Azure/iot-edge-opc-publisher)IoT 邊緣適用於此用途的模組。

hello 方案還有整合到 web 應用程式，可以建立具有內部 OPC UA 伺服器連接的 OPC UA 用戶端。 hello 用戶端會使用[反向 proxy](https://wikipedia.org/wiki/Reverse_proxy) ，並接收來自 IoT 中樞 toomake hello 連線的說明，而不需要 hello 內部防火牆中的開啟通訊埠。 此通訊模式稱為[服務輔助通訊](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/)。 hello 解決方案使用 hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT 邊緣適用於此用途的模組。


## <a name="simulation"></a>模擬

hello 模擬工作站與 hello 模擬製造執行 systems (MES) 組成原廠生產線上。 hello 模擬的裝置和 hello OPC 發行者模組取決於 hello [OPC UA.NET 標準][ lnk-OPC-UA-NET-Standard] hello OPC Foundation 所發行。

hello OPC Proxy 和 OPC 發行者會實作為基礎的模組[Azure IoT 邊緣][lnk-Azure-IoT-Gateway]。 每個模擬產品線都已連結指定的閘道。

所有模擬元件都是在裝載於 Azure Linux VM 的 Docker 容器中執行。 hello 模擬是設定的 toorun 八個模擬的生產行的預設值。

## <a name="simulated-production-line"></a>模擬生產線

生產線可製造零件。 它是由不同的工作站所組成︰組裝工作站、測試工作站和包裝工作站。

hello 模擬執行，並更新透過 hello OPC UA 節點公開的 hello 資料。 所有的模擬的生產線站台是由 hello 透過 OPC UA MES 協調。

## <a name="simulated-manufacturing-execution-system"></a>模擬製造執行系統

hello MES 監視透過 OPC UA toodetect 站台的狀態變更的 hello 生產列中的每個站台。 它呼叫 OPC UA 方法 toocontrol hello 站台，並傳遞產品從一個站台 toohello 下一步完成為止。

## <a name="gateway-opc-publisher-module"></a>閘道 OPC 發行者模組

OPC 發行者模組會連接 toohello 站 OPC UA 伺服器，並訂閱 toohello OPC 節點 toobe 發行。 hello 模組將 hello 節點資料轉換成 JSON 格式，會加密，並將它以 OPC UA Pub/Sub 訊息傳送 tooIoT 中樞。

hello OPC 發行者模組只需要輸出的 https 連接埠 (443)，並且可以使用與現有的企業基礎結構。

## <a name="gateway-opc-proxy-module"></a>閘道 OPC Proxy 模組

hello 閘道 OPC UA Proxy 模組二進位 OPC UA 命令和控制訊息以通道連接，而且只要求的輸出 https 連接埠 (443)。 它可以使用現有的企業基礎結構，包括 Web Proxy。

它使用 hello 應用程式層級的 IoT 中樞裝置方法 tootransfer packetized TCP/IP 資料，並因此可確保端點信任、 資料加密，以及使用 SSL/TLS 的完整性。

UA 驗證和加密，則會使用 hello OPC UA 二進位通訊協定透過本身的 hello proxy 轉送。

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

hello 閘道 OPC 發行者模組訂閱 tooOPC UA 伺服器節點 toodetect hello 資料值變更。 其中一個 hello 節點中，偵測到的資料變更時，此模組會接著傳送訊息 tooAzure IoT 中樞。

IoT 中樞提供事件來源 tooAzure TSI。 TSI 30 天的時間戳記為基礎的存放區資料會附加 toohello 訊息。 這項資料包括︰

* OPC UA ApplicationUri
* OPC UA NodeId
* Hello 節點的值
* 來源時間戳記
* OPC UA DisplayName

目前，TSI 不允許客戶 toocustomize 多久他們希望 tookeep hello 資料。

TSI 會使用 SearchSpan (Time.From、Time.To) 針對節點資料進行查詢，並依 OPC UA ApplicationUri 或 OPC UA NodeId 或 OPC UA DisplayName 進行彙總。

依計數事件、 Sum、 Avg、 Min 和 Max 彙總 tooretrieve hello hello OEE 和 KPI 量測計和 hello 時間序列圖表資料的資料。

使用不同的處理序建立 hello 時間序列。 OEE 和 Kpi 從站台的基底資料計算出來，hello 應用程式中的反昇註冊 hello 拓撲 （生產線、 處理站、 enterprise）。

此外，OEE 和 KPI 拓撲的時間序列是在計算 hello 應用程式，準備好顯示的時間範圍時。 例如，每個完整小時會更新 hello 天檢視。

節點資料 hello 時間序列檢視直接來自 TSI 使用彙總的 timespan。

## <a name="iot-hub"></a>IoT 中樞
hello [IoT 中樞][ lnk-IoT Hub]接收到 hello 雲端 hello OPC 發行者模組從傳送的資料並使其可用 toohello Azure TSI 服務。 

hello 方案中的 hello IoT 中樞也：
- 會維護所有 OPC 發行者模組和所有 OPC Proxy 模組儲存 hello 識別碼的身分識別登錄。
- 作為傳輸通道的 hello OPC 的 Proxy 模組的雙向通訊。

## <a name="azure-storage"></a>Azure 儲存體
hello 解決方案會使用磁碟儲存體與 Azure blob 儲存體，hello 的 VM 和 toostore 部署的資料。

## <a name="web-app"></a>Web 應用程式
hello web 應用程式部署為預先設定的 hello 方案的一部分包含整合式的 OPC UA 用戶端、 處理警示和遙測視覺效果。

## <a name="next-steps"></a>後續步驟

您可以繼續閱讀下列文章 hello 入門 IoT 套件：

* [Hello azureiotsuite.com 網站的權限][lnk-permissions]
* [部署 Windows 或 Linux 上閘道連線的 hello factory 預先設定的解決方案](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md

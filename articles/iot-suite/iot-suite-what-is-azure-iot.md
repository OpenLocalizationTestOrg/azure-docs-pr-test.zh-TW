---
title: "物聯網 （IoT 套件） 的 aaaAzure 解決方案 |Microsoft 文件"
description: "包括範例解決方案架構，以及它與 tooAzure IoT 套件和預先設定的 hello 方案的 azure IoT 的概觀。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 437d2655-896f-4a9e-a4a8-b864790d3ef8
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: e527ca3f7541c84fbd6abc99ee38792468f88644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="azure-iot-suite"></a><span data-ttu-id="77f5e-103">Azure IoT 套件</span><span class="sxs-lookup"><span data-stu-id="77f5e-103">Azure IoT Suite</span></span>
<span data-ttu-id="77f5e-104">Microsoft Azure IoT 套件 hello 是企業級解決方案，可讓您 tooget 透過一組預先設定的解決方案可延伸的快速入門。</span><span class="sxs-lookup"><span data-stu-id="77f5e-104">hello Microsoft Azure IoT Suite is an enterprise-grade solution that enables you tooget started quickly through a set of extensible preconfigured solutions.</span></span> <span data-ttu-id="77f5e-105">這些解決方案可滿足常見的 IoT 案例，例如[遠端監視][lnk-preconfigured-solutions]、[預測性維護][lnk-predictive-maintenance]和[連線的處理站][lnk-connected-factory]。</span><span class="sxs-lookup"><span data-stu-id="77f5e-105">These solutions address common IoT scenarios, such as [remote monitoring][lnk-preconfigured-solutions], [predictive maintenance][lnk-predictive-maintenance], and [connected factory][lnk-connected-factory].</span></span> <span data-ttu-id="77f5e-106">這些解決方案都 hello 這篇文章中所述的 IoT 解決方案架構的實作。</span><span class="sxs-lookup"><span data-stu-id="77f5e-106">These solutions are implementations of hello IoT solution architecture outlined in this article.</span></span>

<span data-ttu-id="77f5e-107">hello 預先設定的解決方案是完成工作，端對端解決方案，包括：</span><span class="sxs-lookup"><span data-stu-id="77f5e-107">hello preconfigured solutions are complete, working, end-to-end solutions that include:</span></span>

- <span data-ttu-id="77f5e-108">模擬裝置 tooget 您已啟動。</span><span class="sxs-lookup"><span data-stu-id="77f5e-108">Simulated devices tooget you started.</span></span>
- <span data-ttu-id="77f5e-109">預先設定的 Azure 服務，例如 [Azure IoT 中樞][Azure IoT Hub]、[Azure 事件中樞][Azure Event Hubs]、[Azure 串流分析][Azure Stream Analytics]、[Azure Machine Learning][Azure Machine Learning] 和 [Azure 儲存體][Azure storage]。</span><span class="sxs-lookup"><span data-stu-id="77f5e-109">Preconfigured Azure services such as [Azure IoT Hub][Azure IoT Hub], [Azure Event Hubs][Azure Event Hubs], [Azure Stream Analytics][Azure Stream Analytics], [Azure Machine Learning][Azure Machine Learning], and [Azure storage][Azure storage].</span></span>
- <span data-ttu-id="77f5e-110">解決方案專用的管理主控台。</span><span class="sxs-lookup"><span data-stu-id="77f5e-110">Solution-specific management consoles.</span></span>

<span data-ttu-id="77f5e-111">hello 預先設定的方案包含經實證可實際執行的程式碼，您可以自訂及擴充 tooimplement 您自己的特定 IoT 案例。</span><span class="sxs-lookup"><span data-stu-id="77f5e-111">hello preconfigured solutions contain proven, production-ready code that you can customize and extend tooimplement your own specific IoT scenarios.</span></span>

<span data-ttu-id="77f5e-112">您可能也會想要 hello [Azure IoT 中樞][ Azure IoT Hub]許多 hello 預先設定的解決方案使用的服務。</span><span class="sxs-lookup"><span data-stu-id="77f5e-112">You may also be interested in hello [Azure IoT Hub][Azure IoT Hub] service that many of hello preconfigured solutions use.</span></span> <span data-ttu-id="77f5e-113">[Azure IoT 中樞][ Azure IoT Hub]提供裝置和預先設定的 hello 解決方案架構中使用的 hello 雲端之間的 hello 安全而可靠雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="77f5e-113">[Azure IoT Hub][Azure IoT Hub] provides hello secure and reliable bi-directional communications between devices and hello cloud used in hello preconfigured solution architecture.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77f5e-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="77f5e-114">Next steps</span></span>
<span data-ttu-id="77f5e-115">瀏覽深入了解 IoT 套件這些資源 toocontinue 和 hello 預先設定的解決方案：</span><span class="sxs-lookup"><span data-stu-id="77f5e-115">Explore these resources toocontinue learning about IoT Suite and hello preconfigured solutions:</span></span>

* <span data-ttu-id="77f5e-116">[什麼是 Azure IoT 套件？][lnk-whatissuite]</span><span class="sxs-lookup"><span data-stu-id="77f5e-116">[What is Azure IoT Suite?][lnk-whatissuite]</span></span>
* <span data-ttu-id="77f5e-117">[Hello 預先設定的 Azure IoT 套件解決方案有哪些？][lnk-whatarepreconfigured]</span><span class="sxs-lookup"><span data-stu-id="77f5e-117">[What are hello Azure IoT Suite preconfigured solutions?][lnk-whatarepreconfigured]</span></span>

[lnk-whatissuite]: iot-suite-overview.md
[lnk-whatarepreconfigured]: iot-suite-what-are-preconfigured-solutions.md

[lnk-preconfigured-solutions]: iot-suite-getstarted-preconfigured-solutions.md
[Azure IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[Azure Event Hubs]: https://azure.microsoft.com/documentation/services/event-hubs/
[Azure Stream Analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[Azure Machine Learning]: https://azure.microsoft.com/documentation/services/machine-learning/
[Azure storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-connected-factory]: iot-suite-connected-factory-overview.md
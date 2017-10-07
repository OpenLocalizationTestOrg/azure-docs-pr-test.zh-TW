---
title: "aaaMicrosoft Azure IoT 套件概觀 |Microsoft 文件"
description: "Azure IoT 套件如何傳遞的項目預先設定的解決方案 toocollect，網際網路概觀分析，和儲存資料、 提供視覺效果，並與其他系統整合。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a>Azure IoT 套件的概觀

hello 的項目 (IoT) 服務的 Azure 網際網路提供廣泛的功能。 這些企業等級的服務可讓您：

* 從裝置收集資料
* 分析移動中的資料串流
* 儲存和查詢大型資料集
* 視覺化即時和歷程記錄資料
* 與後端辦公室系統整合
* 管理您的裝置

toodeliver 這些功能，Azure IoT 套件一起封裝以做為自訂延伸模組的多個 Azure 服務*預先設定的解決方案*。 這些預先設定的解決方案是常見的 IoT 解決方案模式可協助您採取 toodeliver IoT 解決方案 tooreduce hello 時間的基底實作。 使用 hello [IoT 軟體開發套件][lnk-sdks]，您可以自訂及擴充這些解決方案 toomeet 您自己的需求。 您也可以使用這些解決方案作為開發新 IoT 解決方案時的範例或範本。

hello 下列影片提供簡介 tooAzure IoT 套件：

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a>Azure IoT 套件中的 Azure IoT 服務
預先設定的 hello 解決方案通常是使用下列服務的 hello:

* 核心 tooAzure IoT 套件為 hello [Azure IoT 中樞][ lnk-iot-hub]服務。 此服務會提供 hello 裝置的雲端和雲端到裝置訊息功能是做為 hello 閘道 toohello 雲端和 hello 其他索引鍵的 IoT Suite 服務。 hello 服務可讓您從您的裝置在標尺，tooreceive 訊息，並將命令傳送 tooyour 裝置。 hello 服務也可讓您太[管理您的裝置][lnk-device-management]。 例如，您可以設定、 重新開機，或為原廠重設一或多個裝置連線的 toohello 集線器上。
* [Azure 串流分析][lnk-asa]提供移動中的資料分析。 IoT 套件會使用此服務 tooprocess 傳入遙測、 執行彙總，以及偵測到事件。 預先設定的 hello 解決方案也使用資料流分析 tooprocess 參考用訊息包含資料，例如從裝置的中繼資料或命令的回應。 hello 解決方案會使用資料流分析 tooprocess hello 訊息，從您的裝置，並將這些訊息傳遞 tooother 服務。
* [Azure 儲存體][ lnk-azure-storage]和[Azure Cosmos DB] [ lnk-document-db]提供 hello 資料儲存體功能。 hello 預先設定的解決方案使用 blob 儲存體 toostore 遙測和 toomake 它可用於分析。 hello 解決方案使用 Cosmos DB toostore 裝置中繼資料，並啟用 hello 解決方案 hello 裝置管理功能。
* [Azure Web Apps] [ lnk-web-apps]和[Microsoft Power BI] [ lnk-power-bi]提供 hello 資料視覺效果功能。 hello 彈性的 Power BI 可讓您 tooquickly 建置您自己使用 IoT 套件資料的互動式儀表板。

典型的 IoT 解決方案的 hello 架構的概觀，請參閱[Microsoft Azure 與 hello 物聯網 (IoT)][iot-suite-what-is-azure-iot]。

## <a name="preconfigured-solutions"></a>預先設定的解決方案

IoT 套件包含預先設定的解決方案，啟用您 tooquickly 開始使用和 tooexplore hello 常見 IoT 案例中，例如：

* 遠端監視
* 預測性維護
* 連線的處理站

您可以部署這些方案 tooyour Azure 訂用帳戶，然後再執行完整的端對端的 IoT 案例。

## <a name="next-steps"></a>後續步驟

您已經有 IoT 套件可以做什麼，以及其主要元件的概觀，您可以深入了解 IoT 套件中的 hello 預先設定的解決方案。 如需詳細資訊，請參閱[為何 hello Azure IoT 預先設定的解決方案嗎？][lnk-what-are-preconfig]

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md

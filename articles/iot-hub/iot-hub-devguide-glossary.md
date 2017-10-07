---
title: "IoT 中樞詞彙表 aaaAzure |Microsoft 文件"
description: "開發人員指南-相關 tooAzure IoT 中樞的通用詞彙的詞彙。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 16ef29ea-a185-48c3-ba13-329325dc6716
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 217eb082c13e06df5c07543c65d498ad3e395939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="glossary-of-iot-hub-terms"></a>IoT 中樞術語詞彙
本文列出一些 hello 經常使用的 hello 的字彙 IoT 中樞文件。

## <a name="advanced-message-queueing-protocol"></a>進階訊息佇列通訊協定
[進階訊息佇列通訊協定 (AMQP)](https://www.amqp.org/)是其中一個 hello 訊息通訊協定[IoT 中樞](#iot-hub)支援，與裝置通訊。 如需 hello 訊息 IoT 中心支援的通訊協定的詳細資訊，請參閱[傳送和接收訊息與 IoT 中樞](iot-hub-devguide-messaging.md)。

## <a name="azure-cli"></a>Azure CLI
hello [Azure CLI](../cli-install-nodejs.md)是跨平台、 開放原始碼、 shell 為基礎的命令工具，來建立及管理 Microsoft Azure 中的資源。 此版的 hello CLI 會使用 Node.js 來實作。

## <a name="azure-cli-20"></a>Azure CLI 2.0
hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)是跨平台、 開放原始碼、 shell 為基礎的命令工具，來建立及管理 Microsoft Azure 中的資源。 使用 Python 實作 hello CLI 此預覽版本。


## <a name="azure-iot-device-sdks"></a>Azure IoT 裝置 SDK
有_裝置 Sdk_供多個語言，可讓您 toocreate[裝置應用程式](#device-app)與 IoT 中樞的互動。 hello IoT 中樞教學課程告訴您如何 toouse 這些裝置 Sdk。 您可以找到此 GitHub hello 原始碼，以及進一步資訊 hello 裝置 Sdk[儲存機制](https://github.com/Azure/azure-iot-sdks)。

## <a name="azure-iot-edge"></a>Azure IoT Edge
IoT 邊緣可讓您啟用與閘道連線的裝置 toocommunicate toowrite 應用程式[IoT 中樞](#iot-hub)。 hello IoT 邊緣教學課程告訴您如何 toouse 這項服務。 您可以找到此 GitHub hello 原始程式碼和進一步了解 Azure IoT 邊緣[儲存機制](https://github.com/Azure/iot-edge)。

## <a name="azure-iot-service-sdks"></a>Azure IoT 服務 SDK
有_服務 Sdk_供多個語言，可讓您 toocreate[後端應用程式](#back-end-app)與 IoT 中樞的互動。 hello IoT 中樞教學課程示範這些服務 toouse 如何 Sdk。 您可以找到此 GitHub hello 原始程式碼和 hello 服務 Sdk 進一步資訊[儲存機制](https://github.com/Azure/azure-iot-sdks)。

## <a name="azure-portal"></a>Azure 入口網站
hello [Microsoft Azure 入口網站](https://portal.azure.com)是您可以在此設定佈建和管理您的 Azure 資源的中央位置。 它會使用_刀鋒視窗_來組織其內容。 在某些 hello IoT 中樞教學課程中，您可能會要求 toouse hello [Azure 傳統入口網站](https://manage.windowsazure.com)。

## <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell](/powershell/azure/overview)是一組指令程式可以使用 toomanage Azure 使用 Windows PowerShell。 您可以使用 hello cmdlet toocreate、 測試、 部署及管理方案和服務透過 hello Azure 平台傳遞。

## <a name="azure-resource-manager"></a>Azure Resource Manager
[Azure 資源管理員](../azure-resource-manager/resource-group-overview.md)可讓您與您的解決方案，為群組中的 hello 資源 toowork。 您可以部署、 更新或刪除 hello 資源是單一的協調作業，在您的解決方案。

## <a name="azure-service-bus"></a>Azure 服務匯流排
[服務匯流排](../service-bus/index.md)提供具備雲端功能的通訊，與企業傳訊和轉送的通訊，可協助您連接內部部署解決方案以 hello 雲端。 有些 IoT 中樞教學課程會利用服務匯流排[佇列](../service-bus-messaging/service-bus-messaging-overview.md)。

## <a name="azure-storage"></a>Azure 儲存體
[Azure 儲存體](../storage/common/storage-introduction.md)是一套雲端儲存體解決方案。 它包含 hello Blob 儲存體服務，您可以使用非結構化的 toostore 物件資料。 有些 IoT 中樞教學課程會使用 Blob 儲存體。

## <a name="back-end-app"></a>後端應用程式
中的 hello 內容[IoT 中樞](#iot-hub)後, 端應用程式是連接 tooone hello 服務端上的端點 IoT 中樞的應用程式。 例如後, 端應用程式可以擷取[裝置到雲端](#device-to-cloud)訊息或管理 hello[身分識別登錄](#identity-registry)。 一般而言，hello 雲端中執行的後端應用程式，但在許多 hello 教學課程中 hello 後端應用程式會在本機開發電腦上執行的主控台應用程式。

## <a name="built-in-endpoints"></a>內建端點
每個 IoT 中樞都包含與事件中樞相容的內建[端點](iot-hub-devguide-endpoints.md)。 您可以使用任何適用於此端點從事件中心 tooread 裝置到雲端訊息的機制。

## <a name="cloud-gateway"></a>雲端閘道
雲端閘道啟用連線，連線的裝置無法直接太[IoT 中樞](#iot-hub)。 雲端閘道裝載在 hello 雲端中對比 tooa[欄位閘道](#field-gateway)執行本機 tooyour 裝置。 用於雲端閘道的典型使用案例是 tooimplement 通訊協定轉譯，您的裝置。

## <a name="cloud-to-device"></a>雲端到裝置
是指 toomessages 從 IoT 中樞 tooa 連接裝置傳送。 通常，這些訊息會指示 hello 裝置 tootake 動作的命令。 如需詳細資訊，請參閱[使用 IoT 中樞傳送及接收訊息](iot-hub-devguide-messaging.md)。

## <a name="connection-string"></a>連接字串
您可以使用連接字串中您的應用程式程式碼 tooencapsulate hello 所需的資訊 tooconnect tooan 的端點。 連接字串通常包括 hello 位址 hello 端點和安全性資訊，但是格式不同，在服務間的連接字串。 有兩種類型的 hello IoT 中樞服務相關聯的連接字串：
- *裝置連線字串*啟用裝置上 IoT 中樞 tooconnect toohello 面對裝置的端點。
- *IoT 中樞連接字串*啟用後端應用程式 tooconnect toohello IoT 中樞上的服務對向端點。

## <a name="custom-endpoints"></a>自訂端點
您可以建立自訂[端點](iot-hub-devguide-endpoints.md)IoT 中樞 toodeliver 上由訊息發送[路由規則](#routing-rules)。 自訂端點直接連接 tooan 事件中樞、 服務匯流排佇列或服務匯流排主題。

## <a name="custom-gateway"></a>自訂閘道
閘道啟用連線，連線的裝置無法直接太[IoT 中樞](#iot-hub)。 您可以使用[Azure IoT 邊緣](#azure-iot-edge)toobuild 實作自訂邏輯 toohandle 訊息、 自訂通訊協定轉換和其他處理程序的自訂閘道 hello 邊緣。

## <a name="data-point-message"></a>資料點訊息
資料點訊息是[裝置到雲端](#device-to-cloud)的訊息，內含風速或溫度等[遙測](#telemetry)資料。

## <a name="desired-configuration"></a>所需組態
中的 hello 內容[裝置兩個](iot-hub-devguide-device-twins.md)，預期組態參考 toohello 組完整的屬性和中繼資料中應該與 hello 裝置同步的 hello 裝置兩個。

## <a name="desired-properties"></a>所需屬性
中的 hello 內容[裝置兩個](iot-hub-devguide-device-twins.md)，所需的屬性是 hello 裝置兩個，搭配使用的子區段[報告屬性](#reported-properties)toosynchronize 裝置組態或條件。 所需的屬性只能設定[後端應用程式](#back-end-app)並觀察到由 hello[裝置應用程式](#device-app)。

## <a name="device-to-cloud"></a>裝置到雲端
是指太從連接的裝置傳送 toomessages[IoT 中樞](#iot-hub)。 這些訊息可能是[資料點](#data-point-message)訊息或[互動式](#interactive-message)訊息。 如需詳細資訊，請參閱[使用 IoT 中樞傳送及接收訊息](iot-hub-devguide-messaging.md)。

## <a name="device"></a>裝置
Hello IoT 內容中的裝置通常是小型，獨立運算裝置，可能會收集資料，或控制其他裝置。 例如，裝置可能是環境的監視裝置，或是 hello 澆水通風中與系統 greenhouse 的控制站。 hello[裝置類別目錄](https://catalog.azureiotsuite.com/)提供一份硬體與裝置認證 toowork [IoT 中樞](#iot-hub)。

## <a name="device-app"></a>裝置應用程式
裝置應用程式上執行您[裝置](#device)和控制代碼 hello 與通訊程式[IoT 中樞](#iot-hub)。 一般而言，您使用其中一個 hello [Azure IoT 裝置 Sdk](#azure-iot-device-sdks)當您實作裝置應用程式。 在許多 hello IoT 教學課程中，您可以使用[模擬的裝置](#simulated-device)為了方便起見。

## <a name="device-condition"></a>裝置狀況
是指 toodevice 狀態資訊，例如目前使用中的 hello 連線方法所報告[裝置應用程式](#device-app)。 [裝置應用程式](#device-app)也可以報告其功能。 您可以使用裝置對應項來查詢狀況和功能資訊。

## <a name="device-data"></a>裝置資料
裝置資料是指 toohello 每一裝置的資料儲存在 hello IoT 中樞[身分識別登錄](#identity-registry)。 可能的 tooimport，並將這些資料匯出。

## <a name="device-explorer"></a>裝置總管
hello[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)是一種工具，在 Windows 上執行，並讓您 toomanage 裝置 hello[身分識別登錄](#identity-registry).hello 工具也可以傳送和接收訊息 tooyour 裝置。

## <a name="device-identities-rest-api"></a>裝置身分識別 REST API
hello[裝置身分識別 REST API](https://docs.microsoft.com/rest/api/iothub/iothubresource) toomanage hello 中註冊您的裝置可讓您[身分識別登錄](#identity-registry)使用 REST API。 一般而言，您應該使用其中一個較高層級的 hello[服務 Sdk](#azure-iot-service-sdks)中所示 hello IoT 中樞教學課程。

## <a name="device-identity"></a>裝置身分識別
hello 裝置身分識別是 hello 指派唯一識別碼 tooevery 裝置註冊在 hello[身分識別登錄](#identity-registry)。

## <a name="device-management"></a>裝置管理
裝置管理包含 hello 與管理您的 IoT 解決方案包括規劃、 佈建、 設定、 監視及淘汰中的 hello 裝置相關聯的完整生命週期。

## <a name="device-management-patterns"></a>裝置管理模式
[IoT 中樞](#iot-hub)可啟用一般裝置管理模式，包括重新開機、執行恢復出廠預設值，以及在裝置上執行韌體更新。

## <a name="device-messaging-rest-api"></a>裝置傳訊 REST API
您可以使用 hello[裝置傳訊 REST API](https://docs.microsoft.com/rest/api/iothub/httpruntime) toosend 裝置到雲端訊息 tooan IoT 中樞，並接收從裝置[雲端到裝置](#cloud-to-device)從 IoT 中樞的訊息。 一般而言，您應該使用其中一個較高層級的 hello[裝置 Sdk](#azure-iot-device-sdks)中所示 hello IoT 中樞教學課程。

## <a name="device-provisioning"></a>裝置佈建
裝置佈建是 hello 程序加入 hello 初始[裝置資料](#device-data)toohello 將儲存在您的方案。 tooenable 新裝置 tooconnect tooyour 中樞，您必須新增裝置識別碼和金鑰 toohello IoT 中樞[身分識別登錄](#identity-registry)。 Hello 佈建程序的一部分，您可能需要其他的方案存放區中的 tooinitialize 裝置的特定資料。

## <a name="device-twin"></a>裝置對應項
[裝置對應項](iot-hub-devguide-device-twins.md)是存放裝置狀態資訊 (例如中繼資料、組態和狀況) 的 JSON 文件。 [IoT 中樞](#iot-hub)會為您在 IoT 中樞佈建的每個裝置保存裝置對應項。 裝置雙可讓您 toosynchronize[裝置條件](#device-condition)和 hello 裝置與 hello 方案之間的設定後端。 您可以查詢裝置雙 toolocate 特定裝置和查詢 hello 長時間執行的作業狀態。

## <a name="device-twin-queries"></a>裝置對應項查詢
[裝置的兩個查詢](iot-hub-devguide-query-language.md)使用 hello 類似 SQL 的 IoT 中樞查詢語言 tooretrieve 資訊從裝置雙。 您可以使用相同的 IoT 中樞的查詢語言 tooretrieve 資訊有關的 hello[作業](#job)IoT 中樞中執行。

## <a name="device-twin-rest-api"></a>裝置對應項 REST API
您可以使用 hello[裝置兩個 REST API](https://docs.microsoft.com/rest/api/iothub/devicetwinapi) hello 方案從後端 toomanage 裝置雙。 hello API 可讓您 tooretrieve 和 update[裝置兩個](#device-twin)屬性，並叫用[直接方法](#direct-method)。 一般而言，您應該使用其中一個較高層級的 hello[服務 Sdk](#azure-iot-service-sdks)中所示 hello IoT 中樞教學課程。

## <a name="device-twin-synchronization"></a>裝置對應項同步處理
裝置的兩個同步處理所使用 hello[所需屬性](#desired-properties)您裝置的雙 tooconfigure 在您的裝置和擷取[報告屬性](#reported-properties)從您的裝置 toostore 在 hello 裝置兩個。

## <a name="direct-method"></a>直接方法
A[直接方法](iot-hub-devguide-direct-methods.md)叫用您的 IoT 中樞上的 API 可讓您 tootrigger 方法 tooexecute 在裝置上的。

## <a name="endpoint"></a>端點
IoT 中心會公開多個[端點](iot-hub-devguide-endpoints.md)可讓您的應用程式 tooconnect toohello IoT 中樞。 會有裝置向端點啟用裝置 tooperform 作業，例如傳送[裝置到雲端](#device-to-cloud)訊息和接收[雲端到裝置](#cloud-to-device)訊息。 有可讓服務向管理端點[後端應用程式](#back-end-app)tooperform 作業，例如[裝置身分識別](#device-identity)管理和兩個裝置的管理。 有可用於讀取裝置到雲端訊息的服務面向[內建端點](#built-in-endpoints)。 您可以建立[自訂端點](#custom-endpoints)tooreceive 裝置到雲端訊息的分派[路由規則](#routing-rules)。

## <a name="event-hubs-service"></a>事件中樞服務
[事件中樞](../event-hubs/event-hubs-what-is-event-hubs.md)是可高度調整的資料擷取服務，每秒可以擷取數以百萬計的事件。 hello 服務可讓您 tooprocess 和分析 hello 連接的裝置和應用程式所產生的資料量很大。 如需比較以 hello IoT 中心服務，請參閱[Azure IoT 中樞的比較與 Azure 事件中心](iot-hub-compare-event-hubs.md)。

## <a name="event-hub-compatible-endpoint"></a>事件中樞相容端點
tooread[裝置到雲端](#device-to-cloud)訊息傳送 tooyour IoT 中樞，您可以在您的中樞連線 tooan 端點並使用任何事件中樞相容方法 tooread 這些訊息。 事件中樞相容的方法包括使用 hello[事件中心 Sdk](../event-hubs/event-hubs-programming-guide.md)和[Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md)。

## <a name="field-gateway"></a>現場閘道
領域閘道啟用連線，連線的裝置無法直接太[IoT 中樞](#iot-hub)通常是與您的裝置在本機部署。 如需詳細資訊，請參閱[何謂 Azure IoT 中樞？](iot-hub-what-is-iot-hub.md)

## <a name="free-account"></a>免費帳戶
您可以建立[免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)toocomplete hello IoT 中樞教學課程和試驗 hello IoT 中心服務 （和其他 Azure 服務）。

## <a name="gateway"></a>閘道器
閘道啟用連線，連線的裝置無法直接太[IoT 中樞](#iot-hub)。 另請參閱[現場閘道](#field-gateway)、[雲端閘道](#cloud-gateway)和[自訂閘道](#custom-gateway)。

## <a name="identity-registry"></a>身分識別登錄
hello[身分識別登錄](iot-hub-devguide-identity-registry.md)就 hello 的 IoT 中樞儲存 hello 個別裝置的相關資訊的內建元件允許 tooconnect tooan IoT 中樞。

## <a name="interactive-message"></a>互動式訊息
互動式的訊息是[雲端到裝置](#cloud-to-device)觸發立即 hello 方案後端中的動作的訊息。 例如，裝置可能會傳送應該自動登入 tooa CRM 系統失敗相關警示。

## <a name="iot-hub"></a>IoT 中樞
IoT 中樞是一項完全受管理的 Azure 服務，可在數百萬個裝置和一個解決方案後端之間啟用可靠且安全的雙向通訊。 如需詳細資訊，請參閱[何謂 Azure IoT 中樞？](iot-hub-what-is-iot-hub.md) 使用您[Azure 訂用帳戶](#subscription)，您可以建立 IoT 中樞 toohandle 您 IoT 傳訊工作負載。

## <a name="iot-hub-metrics"></a>IoT 中樞計量
[IoT 中樞度量](iot-hub-metrics.md)提供您有關 hello 狀態中的 hello IoT 中樞的資料，您[Azure 訂用帳戶](#subscription)。 IoT 中樞度量啟用您 tooassess hello hello 服務和 hello 裝置的整體健全狀況連接 tooit。 IoT 中樞度量可協助您查看與您的 IoT 中樞狀況，並調查根本原因問題，而不需要 toocontact Azure 支援。

## <a name="iot-hub-query-language"></a>IoT 中樞查詢語言
hello [IoT 中樞的查詢語言](iot-hub-devguide-query-language.md)是一種類似 SQL 的語言，可讓您 tooquery 您[作業](#job)和裝置雙。

## <a name="iot-hub-resource-provider-rest-api"></a>IoT 中樞資源提供者 REST API
您可以使用 hello [IoT 中樞資源提供者 REST API](https://docs.microsoft.com/rest/api/iothub/resourceprovider/iot-hub-resource-provider-rest) toomanage hello IoT 中樞中的您[Azure 訂用帳戶](#subscription)執行建立、 更新和刪除中樞之類的作業。

## <a name="iot-suite"></a>IoT 套件
Azure IoT 套件會使用預先設定的解決方案將多項 Azure 服務封裝在一起。 這些預先設定的解決方案可讓您 tooget 快速地開始使用常見的 IoT 案例的端對端實作。 如需詳細資訊，請參閱[什麼是 Azure IoT 套件？](../iot-suite/iot-suite-overview.md)

## <a name="iothub-explorer"></a>iothub-explorer
hello [iot 中樞總管](https://github.com/azure/iothub-explorer)是跨平台、 命令列工具。 hello 工具可讓您 toomanage 裝置 hello[身分識別登錄](#identity-registry)、 傳送和接收的郵件和檔案從您的裝置，及監視您的 IoT 中樞作業。

## <a name="job"></a>作業
可以使用您的方案後端[作業](iot-hub-devguide-jobs.md)tooschedule 和追蹤的活動，在一組裝置上註冊與 IoT 中樞。 這些活動包括更新裝置對應項[所需屬性](#desired-properties)、更新裝置對應項[標籤](#tags)，以及叫用[直接方法](#direct-method)。 [IoT 中樞](#iot-hub)也會使用作業太[匯入 tooand 匯出](iot-hub-devguide-identity-registry.md#import-and-export-device-identities)從 hello[身分識別登錄](#identity-registry)。

## <a name="jobs-rest-api"></a>作業 REST API
hello[作業的 REST API](https://docs.microsoft.com/rest/api/iothub/jobapi)可讓您 toomanage[作業](#job)IoT 中樞中執行。

## <a name="module"></a>模組
在 [Azure IoT Edge](iot-hub-linux-iot-edge-get-started.md) 中，[模組](iot-hub-linux-iot-edge-get-started.md)是可執行特定工作的元件。 工作可能包括擷取來自裝置的訊息、 訊息、 轉換或傳送訊息 tooan IoT 中樞。 訊息代理程式會負責在模組之間轉送訊息。 Azure IoT Edge 包含一組範例模組。 您也可以建立自己的自訂模組。

## <a name="mqtt"></a>MQTT
[MQTT](http://mqtt.org/)是其中一個 hello 訊息通訊協定[IoT 中樞](#iot-hub)支援，與裝置通訊。 如需 hello 訊息 IoT 中心支援的通訊協定的詳細資訊，請參閱[傳送和接收訊息與 IoT 中樞](iot-hub-devguide-messaging.md)。

## <a name="operations-monitoring"></a>作業監視
IoT 中樞[作業監視](iot-hub-operations-monitoring.md)可讓您即時您 IoT 中樞上的作業 toomonitor hello 狀態。 [IoT 中樞](#iot-hub)可追蹤橫跨數個作業類別的事件。 您可以選擇傳送事件，從一或多個類別 tooan IoT 中樞端點進行處理。 您可以監視有錯誤的 hello 資料或設定根據資料模式更複雜的處理。

## <a name="physical-device"></a>實體裝置
實體裝置是實際連線 tooan IoT 中樞覆盆子 Pi 之類的裝置。 為了方便起見，許多 hello IoT 中樞教學課程都使用[模擬裝置](#simulated-device)tooenable 您 toorun 範例在本機電腦。

## <a name="primary-and-secondary-keys"></a>主要和次要金鑰
當您連接 tooa 面對裝置的服務對向端點在 IoT 中樞內，或您[連接字串](#connection-string)包含您所存取的索引鍵 toogrant。 當您新增裝置 toohello[身分識別登錄](#identity-registry)或新增[共用存取原則](#shared-access-policy)tooyour 集線器，hello 服務會產生主要和次要金鑰。 必須要有兩個金鑰可讓您 tooroll 透過從一個索引鍵 tooanother 當您更新金鑰，而不會遺失存取 toohello IoT 中樞。

## <a name="protocol-gateway"></a>通訊協定閘道
通訊協定閘道通常 hello 雲端中部署，並提供通訊協定轉譯服務的裝置連線太[IoT 中樞](#iot-hub)。 如需詳細資訊，請參閱[何謂 Azure IoT 中樞？](iot-hub-what-is-iot-hub.md)

## <a name="quotas-and-throttling"></a>配額和節流
有各種[配額](iot-hub-devguide-quotas-throttling.md)套用 tooyour 使用[IoT 中樞](#iot-hub)，許多 hello 配額不同的 hello IoT 中樞的 hello 層為基礎。 [IoT 中樞](#iot-hub)也適用於[節流](iot-hub-devguide-quotas-throttling.md)tooyour 使用 hello 服務在執行階段。

## <a name="reported-configuration"></a>報告組態
中的 hello 內容[裝置兩個](iot-hub-devguide-device-twins.md)、 報告的組態參考 toohello 組完整的屬性和中繼資料中應 hello 裝置兩個報告 toohello 方案後端。

## <a name="reported-properties"></a>報告屬性
Hello 內容中[裝置兩個](iot-hub-devguide-device-twins.md)，屬性為的子區段的 hello 裝置兩個用於[所需屬性](#desired-properties)toosynchronize 裝置組態或條件。 報告 hello 只可以設定屬性[裝置應用程式](#device-app)和可讀取，並由查詢[後端應用程式](#back-end-app)。

## <a name="resource-group"></a>資源群組
[Azure 資源管理員](#azure-resource-manager)使用資源群組 toogroup 相互關聯的資源。 您可以同時使用所有 hello 資源的資源群組 tooperform 的操作 hello 群組上。

## <a name="retry-policy"></a>重試原則
使用重試原則 toohandle[暫時性錯誤](https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx)tooa 雲端服務的連接時。

## <a name="routing-rules"></a>路由規則
您設定[路由規則](iot-hub-devguide-messages-read-custom.md)在 IoT 中樞 tooroute 裝置到雲端訊息 tooa[內建端點](#built-in-endpoints)或太[自訂端點](#custom-endpoints)方案後所處理結束。

## <a name="sasl-plain"></a>SASL PLAIN
SASL 純是 hello 的通訊協定[AMQP](#advanced-message-queue-protocol)通訊協定會使用 tootransfer 安全性權杖。

## <a name="shared-access-signature"></a>共用存取簽章
共用存取簽章 (SAS) 是以 SHA-256 安全雜湊或 URI 為基礎的驗證機制。 SAS 驗證有兩個元件：「共用存取原則」和「共用存取簽章」 (通常稱為權杖)。 裝置會使用 SAS tooauthenticate 與 IoT 中樞。 [後端應用程式](#back-end-app)也使用 SAS tooauthenticate 與 hello IoT 中樞上的服務對向端點。 一般而言，您將納入 hello SAS 權杖 hello[連接字串](#connection-string)應用程式使用 tooestablish 連接 tooan IoT 中樞。

## <a name="shared-access-policy"></a>共用存取原則
共用的存取原則都會定義一些 hello 權限授與具有有效 tooanyone[主要或次要金鑰](#primary-and-secondary-keys)與該原則相關聯。 您可以管理在 hello 中樞 hello 共用存取原則和索引鍵[入口網站](#azure-portal)。

## <a name="simulated-device"></a>模擬裝置
為了方便起見，許多 hello IoT 中樞教學課程都使用模擬裝置 tooenable 您 toorun 範例在本機電腦。 相反地，[實體裝置](#physical-device)是實際連線 tooan IoT 中樞覆盆子 Pi 之類的裝置。

## <a name="solution"></a>方案
A_方案_可以參考 tooa Visual Studio 方案所包含的一或多個專案。 A_方案_也可能會參考 tooan IoT 方案所包含的項目裝置，例如[裝置應用程式](#device-app)，IoT 中樞、 其他 Azure 服務和[後端應用程式](#back-end-app)。

## <a name="subscription"></a>訂用帳戶
Azure 訂用帳戶是發生帳單的地方。 您建立的每個 Azure 資源，或您使用的 Azure 服務會與單一訂用帳戶相關聯。 許多的配額也適用於層級 hello 的訂用帳戶。

## <a name="system-properties"></a>系統屬性
中的 hello 內容[裝置兩個](iot-hub-devguide-device-twins.md)，系統屬性是唯讀，並且包含 hello 裝置使用量，例如上次活動時間和連接狀態的相關資訊。

## <a name="tags"></a>標記
中的 hello 內容[裝置兩個](iot-hub-devguide-device-twins.md)，標記是裝置的中繼資料儲存和擷取 hello 方案後端 hello 格式的 JSON 文件。 不會在裝置上的可見 tooapps 標記。

## <a name="telemetry"></a>遙測
裝置收集遙測資料，例如風速度或溫度，並使用[資料點訊息](#data-point-messages)toosend hello 遙測 tooan IoT 中樞。

## <a name="token-service"></a>權杖服務
您可以使用語彙基元服務 tooimplement 驗證機制，您的裝置。 它會使用 IoT 中樞[共用存取原則](#shared-access-policy)與**DeviceConnect**權限 toocreate*裝置範圍*語彙基元。 這些語彙基元可讓裝置 tooconnect tooyour IoT 中樞。 裝置會使用自訂驗證機制 tooauthenticate 與 hello 權杖的服務。 如果裝置 hello 成功通過驗證，hello 語彙基元服務發出 hello 裝置 toouse tooaccess 的 SAS token IoT 中樞。

## <a name="x509-client-certificate"></a>X.509 用戶端憑證
裝置可以使用具有 X.509 憑證 tooauthenticate [IoT 中樞](#iot-hub)。 使用 X.509 憑證是替代的 toousing [SAS 權杖](#shared-access-signature)。

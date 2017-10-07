---
title: "aaaAzure IoT 中樞概觀 |Microsoft 文件"
description: "Hello Azure IoT 中心服務的概觀： 什麼是 IoT 中樞、 裝置連線能力、 網際網路的事情通訊模式、 閘道和 hello 服務輔助通訊模式"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0b46868a1ec9e13c8f107b90269c5307f4ba27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-iot-hub-service"></a>Hello Azure IoT 中心服務的概觀

歡迎使用 tooAzure IoT 中樞。 這篇文章會提供 Azure IoT 中樞的概觀，並說明為什麼您應該使用此服務 tooimplement 物聯網 (IoT) 解決方案。 Azure IoT 中樞是一項完全受管理的服務，可在數百萬個 IoT 裝置和一個解決方案後端之間啟用可靠且安全的雙向通訊。 Azure IoT 中樞：

* 提供多個裝置到雲端和雲端到裝置通訊選項，包括單向傳訊、檔案傳輸，以及要求-回覆方法。
* 提供內建的宣告式訊息路由 tooother Azure 服務。
* 針對裝置中繼資料與同步化狀態資訊提供可查詢存放區。
* 使用每一裝置的安全性金鑰或 X.509 憑證啟用安全通訊與存取控制。
* 可廣泛監視裝置的連線情況和裝置的身分識別管理事件。
* 包含裝置 hello 最受歡迎的語言與平台的程式庫。

hello 文章[比較的 IoT 中樞與事件中心][ lnk-compare]描述 hello 這兩個服務之間的主要差異，並反白顯示您的 IoT 解決方案中使用 IoT 中樞的 hello 優點。

如需有關如何 Azure 與 IoT 中樞協助保護您的 IoT 解決方案的詳細資訊，請參閱[從 hello 地面物聯網安全性][lnk-security-ground-up]。

![Azure IoT 中樞做為物聯網解決方案中的雲端閘道][img-architecture]

> [!NOTE]
> IoT 架構的深入討論，請參閱 hello [Microsoft Azure IoT 參考架構][lnk-refarch]。

## <a name="iot-device-connectivity-challenges"></a>IoT 裝置連線能力面臨的挑戰

IoT 中樞與 hello 裝置庫幫助您如何 toomeet hello 挑戰 tooreliably 安全地連線裝置 toohello 方案後端。 IoT 裝置：

* 通常是無人操作的嵌入式系統。
* 可以位於實體存取很昂貴的遠端位置。
* 只能透過 hello 方案後端連線。
* 能力和/或處理資源可能都有限。
* 網路連線能力可能不穩定、緩慢或昂貴。
* 可能需要 toouse 專用、 自訂或業界特定的應用程式通訊協定。
* 可以使用一組大型常見的硬體和軟體平台來建立。

除了上述 toohello 需求，任何 IoT 解決方案必須也提供小數位數、 安全性和可靠性。 hello 產生的連線需求是困難且耗時 tooimplement 當您使用傳統的技術，例如 web 容器及訊息代理人。

## <a name="why-use-azure-iot-hub"></a>為何使用 Azure IoT 中心？

此外 tooa 豐富的[裝置到雲端][ lnk-d2c-guidance]和[雲端到裝置][ lnk-c2d-guidance]通訊選項，包括訊息、 檔案轉送和要求-回覆方法 Azure IoT 中樞位址 hello hello 下列方式中的裝置連線挑戰：

* **裝置對應項**。 使用[裝置對應項][lnk-twins]，您可以儲存、同步處理，以及查詢裝置中繼資料與狀態資訊。 「裝置對應項」是存放裝置狀態資訊 (中繼資料、組態和條件) 的 JSON 文件。 IoT 中樞保存您連接 tooIoT 中樞的每個裝置的裝置兩個。

* **每一裝置的驗證和安全連線能力**。 您可以將每個裝置使用它自己佈建[安全性金鑰][ lnk-devguide-security] tooenable 它 tooconnect tooIoT 中樞。 hello [IoT 中樞身分識別登錄][ lnk-devguide-identityregistry]將裝置身分識別和索引鍵儲存在方案中。 方案的後端加入個別裝置 tooallow 或拒絕清單 tooenable 擁有完整控制權存取裝置。

* **路由裝置到雲端訊息的宣告式規則為基礎的 tooAzure 服務**。 IoT 中樞可讓您 toodefine 訊息讓您的中樞傳送裝置到雲端訊息的路由規則 toocontrol 為基礎的路由。 路由規則不需要您 toowrite 任何程式碼中，而且可以進行 hello 的自訂後擷取訊息發送器。

* **裝置連線作業的監視**。 您可以收到有關裝置身分識別管理作業與裝置連線事件的詳細作業記錄檔。 這項監視功能可以讓您 IoT 解決方案 tooidentify 連線問題，例如頻率太高，傳送訊息，或拒絕所有雲端到裝置訊息 tooconnect 不正確的認證，再試一次的裝置。

* **一組廣泛的裝置程式庫**。 [Azure IoT 裝置 SDK][lnk-device-sdks] 可供各種語言和平台使用並受其支援，例如許多 Linux 發行版本都支援的 C、Windows 和即時作業系統。 Azure IoT 裝置 SDK 也支援 C#、Java 和 JavaScript 等 Managed 語言。

* **IoT 通訊協定和擴充性**。 如果您的方案無法使用 hello 裝置程式庫，IoT 中樞會公開公用的通訊協定，可讓裝置 toonatively 使用 hello MQTT v3.1.1、 HTTP 1.1 或 AMQP 1.0 通訊協定。 您也可以擴充的自訂通訊協定的 IoT 中樞 toosupport:

  * 建立具有欄位閘道[Azure IoT 邊緣][ lnk-iot-edge]將您的自訂通訊協定 tooone hello 三種通訊協定瞭解 IoT 中樞的轉換。
  * 自訂 hello [Azure IoT 通訊協定閘道][protocol-gateway]，hello 雲端中執行的開放原始碼元件。

* **規模**。 Azure IoT 中樞縮放 toomillions 的同時連線的裝置和數百萬個每秒的事件。

## <a name="gateways"></a>閘道

閘道的 IoT 解決方案通常是 [通訊協定閘道][ lnk-iotedge] hello 雲端中為針對部署或[欄位閘道][ lnk-field-gateway]也就是部署在本機裝置。 通訊協定閘道執行通訊協定轉譯，例如 MQTT tooAMQP。 欄位閘道可以 hello 邊緣上執行分析，做出時間緊迫 tooreduce 延遲、 提供裝置管理服務，強制執行安全性和隱私權條件約束，且也執行通訊協定轉譯。 這兩種閘道器可做為您的裝置與 IoT 中樞之間的媒介。

現場閘道器與簡單的流量路由裝置 (例如網路位址轉譯裝置或防火牆) 不同，因為它通常會在解決方案內管理存取和資訊流程中扮演主動的角色。

解決方案可以同時包含通訊協定閘道和領域閘道。

## <a name="how-does-iot-hub-work"></a>IoT 中樞如何運作？

Azure IoT 中樞實作 hello[服務輔助通訊][ lnk-service-assisted-pattern]您的裝置與您的方案之間的模式 toomediate hello 互動後端。 hello 目標服務輔助通訊是 tooestablish trustworthy，雙向通訊路徑之間控制系統，例如 IoT 中樞和特殊用途的裝置部署在不受信任的實體空間。 hello 模式建立 hello 下列原則：

* 安全性的優先順序高於所有其他功能。

* 裝置不會接受未經要求的網路資訊。 裝置會以僅限輸出方式建立所有連接和路由。 裝置 tooreceive hello 方案後端的命令，如 hello 裝置必須定期啟動任何暫止命令 tooprocess 連接的 toocheck。

* 裝置應該只在連接 tooor 建立它們是否例如 IoT Hub 對等與路由 toowell 已知服務。

* hello 應用程式通訊協定層級受到保護裝置與服務之間或裝置和閘道之間的 hello 通訊路徑。

* 系統層級的授權和驗證是以每個裝置的身分識別為基礎。 可讓存取認證和權限能近乎即時撤銷。

* 連線偶發性到期 toopower 或連線問題的裝置的雙向通訊透過來保存命令和裝置通知，直到裝置連線 tooreceive 實現它們。 IoT 中樞維護裝置的特定佇列傳送 hello 命令。

* 應用程式裝載資料是透過閘道 tooa 特定服務的受保護傳輸資料的報表分開保護。

hello 行動業界已用 hello 服務輔助通訊模式在龐大的小數位數 tooimplement 推播通知服務如[Windows 推播通知服務][lnk-wns]， [Google 雲端訊息][lnk-google-messaging]，和[Apple 推播通知服務][lnk-apple-push]。

ExpressRoute 的公用對等互連路徑支援 IoT 中樞。

## <a name="next-steps"></a>後續步驟

toolearn toosend 訊息從裝置的方式，並接收 IoT 中樞，以及如何 tooconfigure 訊息會路由傳送，請參閱[傳送和接收訊息與 IoT 中樞][lnk-send-messages]。

toolearn 如何 IoT 中樞可讓標準為基礎的裝置管理，針對您 tooremotely 管理、 設定及更新您的裝置，請參閱[裝置管理概觀與 IoT 中樞][lnk-device-management]。

tooimplement 各種裝置的硬體平台和作業系統上的用戶端應用程式，您可以使用 hello Azure IoT 裝置 Sdk。 hello 裝置 Sdk 包含程式庫，以便傳送遙測 tooan IoT 中樞與接收雲端到裝置的訊息。 當您使用 hello 裝置 Sdk 時，您可以選擇從各種網路通訊協定 toocommunicate 與 IoT 中樞。 toolearn 詳細資訊，請參閱 hello[裝置 Sdk 的相關資訊][lnk-device-sdks]。

tooget 啟動撰寫一些程式碼，並執行一些範例，請參閱 hello[開始使用 IoT 中樞][ lnk-get-started]教學課程。

[img-architecture]: media/iot-hub-what-is-iot-hub/hubarchitecture.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[protocol-gateway]: https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md
[lnk-service-assisted-pattern]: http://blogs.msdn.com/b/clemensv/archive/2014/02/10/service-assisted-communication-for-connected-devices.aspx "服務輔助通訊 (由 Clemens Vasters 撰寫的部落格文章)"
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-iotedge]: iot-hub-protocol-gateway.md
[lnk-field-gateway]: iot-hub-devguide-endpoints.md#field-gateways
[lnk-devguide-identityregistry]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-wns]: https://msdn.microsoft.com/library/windows/apps/mt187203.aspx
[lnk-google-messaging]: https://developers.google.com/cloud-messaging/
[lnk-apple-push]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-send-messages]: iot-hub-devguide-messaging.md
[lnk-device-management]: iot-hub-device-management-overview.md

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-security-ground-up]: iot-hub-security-ground-up.md

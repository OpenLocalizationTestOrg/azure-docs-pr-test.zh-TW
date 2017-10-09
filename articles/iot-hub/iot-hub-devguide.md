---
title: "Azure IoT 中樞 aaaDeveloper 指南 |Microsoft 文件"
description: "hello Azure IoT 中樞開發人員指南包含端點、 安全性、 hello 身分識別登錄、 裝置管理、 直接的方法、 裝置雙、 檔案上傳、 作業、 hello IoT 中樞的查詢語言和傳訊的討論。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a>Azure IoT 中樞開發人員指南

Azure IoT 中樞是一項完全受管理的服務，有助於讓數百萬個裝置和一個解決方案後端進行可靠且安全的雙向通訊。

Azure IoT 中樞可提供您︰

* 使用每一裝置的安全性認證和存取控制來保護通訊的安全。
* 多個裝置到雲端和雲端到裝置的超大規模通訊選項。
* 每一裝置狀態資訊和中繼資料的可查詢儲存體。
* 簡單的裝置與裝置 hello 最受歡迎的語言與平台的程式庫的連線。

此 IoT 中樞開發人員指南包含下列發行項的 hello:

* [裝置對雲端通訊指引][lnk-d2c-guidance]可協助您在裝置對雲端訊息、裝置對應項報告屬性和檔案上傳之間做出選擇。
* [雲端對裝置通訊指引][lnk-c2d-guidance]可協助您在直接方法、裝置對應項所需屬性和雲端對裝置訊息之間做出選擇。
* [裝置的雲端和雲端的裝置與 IoT 中樞傳訊][ devguide-messaging]描述 hello 訊息功能 （裝置到雲端和雲端到裝置） 公開 IoT 中樞。
  * [傳送裝置到雲端訊息 tooIoT 中樞][devguide-messages-d2c]。
  * [讀取 hello 內建端點的裝置到雲端訊息][devguide-builtin]。
  * [使用適用於裝置對雲端訊息的自訂端點和路由規則][devguide-custom]。
  * [從 IoT 中樞傳送雲端到裝置訊息][devguide-messages-c2d]。
  * [建立及讀取 IoT 中樞訊息][devguide-format]。
* [從裝置上傳檔案][devguide-upload]說明如何從裝置上傳檔案。 hello 文章也包含通知 hello 上傳程序可以傳送 hello 等主題的資訊。
* [在 IoT 中樞管理裝置身分識別][devguide-identities]說明各 IoT 中樞的身分識別登錄所儲存的資訊，以及您可以存取和修改資訊的方式。
* [控制存取 tooIoT 中樞][ devguide-security]描述 hello 安全性模型使用 toogrant 存取 tooIoT 中樞功能的裝置和雲端元件。 hello 發行項包含使用權杖和 X.509 憑證和 hello 可以授與的權限的詳細資料的相關資訊。
* [使用裝置雙 toosynchronize 狀態和設定][ devguide-device-twins]描述 hello*裝置兩個*概念和 hello 與裝置同步處理裝置，例如，它會公開的功能兩個。 hello 發行項包含 hello 資料儲存在裝置的兩個相關資訊。
* [叫用的裝置上直接方法][ devguide-directmethods]描述 hello 生命週期的直接的方法時，如何 tooinvoke 方法從後端應用程式和控制代碼 hello 裝置上的直接在裝置上的方法的相關資訊。
* [排程多個裝置上的作業][devguide-jobs]說明如何排程多個裝置上的作業。 hello 文章說明如何 toosubmit 工作在執行直接的方法，更新使用裝置的兩個裝置時執行工作。 此外也說明如何 tooquery hello 工作的狀態。
* [參考-選擇通訊協定][ devguide-protocol]描述 hello 通訊協定支援的裝置通訊的 IoT 中樞，並列出 hello 應開啟的連接埠。
* [參考-IoT 中樞端點][ devguide-endpoints]描述 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。 hello 本文也描述您可以建立其他端點，在您的 IoT 中樞，以及如何 toouse 欄位閘道 tooenable 裝置連線 tooyour IoT 中樞端點在非標準的案例。
* [參考-裝置雙、 作業和訊息路由的 IoT 中樞查詢語言][ devguide-query]描述該裝置雙和作業的相關的 tooretrieve 資訊從您的中樞可讓您的 IoT 中樞查詢語言。
* [參考-配額和節流][ devguide-quotas] hello 配額 hello IoT 中心服務和節流行為，當超過配額時，您可以預期 toosee hello 設定彙總。
* [參考-定價][ devguide-pricing]提供不同的 Sku 和定價的 IoT 中樞與 hello 做為計量 IoT 中樞的各種不同功能的 IoT 中樞的訊息的詳細資訊的一般資訊。
* [參考-裝置和服務 Sdk] [ devguide-sdks]清單 hello Azure IoT Sdk，您可以使用 toodevelop 與 IoT 中樞互動的裝置和服務應用程式。 hello 文件包含連結 tooonline API 文件。
* [參考-IoT 中樞 MQTT 支援][ devguide-mqtt]提供 IoT 中樞的 hello MQTT 通訊協定的支援方式的詳細的資訊。 hello 文件描述 hello hello MQTT 通訊協定內建 toohello Azure IoT Sdk 支援，並且提供直接使用 hello MQTT 通訊協定的相關資訊。
* [詞彙][devguide-glossary]是常見 IoT 中樞相關術語的清單。

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md

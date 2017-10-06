---
title: "aaaUnderstand hello Azure IoT 中樞身分識別登錄 |Microsoft 文件"
description: "開發人員指南-hello IoT 中樞身分識別登錄的描述以及 toouse 它 toomanage 您的裝置。 包含大量的 hello 匯入和匯出裝置身分識別的相關資訊。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0706eccd-e84c-4ae7-bbd4-2b1a22241147
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c9fe3730a4608e28c47807ecb42e13e73f6a2e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-identity-registry-in-your-iot-hub"></a>了解 hello 身分識別登錄在 IoT 中樞

每個 IoT 中樞的身分識別登錄儲存 hello 裝置允許 tooconnect toohello IoT 中樞的相關資訊。 裝置可以連線 tooan IoT 中樞之前，必須是該裝置 hello IoT 中樞的身分識別登錄中的項目。 裝置也必須與 hello IoT 中樞根據 hello 身分識別登錄中儲存的認證驗證。

儲存在 hello 身分識別登錄中的 hello 裝置識別碼會區分大小寫。

在高層級，hello 身分識別登錄是 REST 支援的裝置識別資源的集合。 當您在 hello 身分識別登錄中新增項目時，IoT 中樞將建立每一裝置的資源，例如 hello 佇列，其中包含執行中雲端到裝置訊息的集。

### <a name="when-toouse"></a>當 toouse

當您需要時，請使用 hello 身分識別登錄：

* 連接 tooyour IoT 中樞的佈建裝置。
* 控制每一裝置存取 tooyour 中樞的面對裝置的端點。

> [!NOTE]
> hello 身分識別登錄未包含任何應用程式專屬的中繼資料。

## <a name="identity-registry-operations"></a>身分識別登錄作業

hello IoT 中樞身分識別登錄公開 hello 下列作業：

* 建立裝置身分識別
* 更新裝置身分識別
* 依照 ID 擷取裝置身分識別別
* 刪除裝置身分識別
* 列出向上 too1000 身分識別
* 匯出所有識別 tooAzure blob 儲存體
* 從 Azure Blob 儲存體匯入身分識別

上述所有作業均可使用 [RFC7232][lnk-rfc7232] 中指定的開放式並行存取。

> [!IMPORTANT]
> hello 只方式 tooretrieve IoT 中樞的身分識別登錄中的所有識別身分為 toouse hello[匯出][ lnk-export]功能。

IoT 中樞身分識別登錄：

* 不包含任何應用程式中繼資料。
* 就如同字典，可以存取使用 hello **deviceId** hello 索引鍵。
* 不支援表達式查詢。

IoT 方案通常具有不同的方案專屬存放區，其中包含應用程式特定的中繼資料。 比方說，hello 智慧建置方案中的特定解決方案的存放區會記錄其中溫度感應器部署的 hello 聊天室。

> [!IMPORTANT]
> 只使用 hello 身分識別登錄裝置管理和佈建作業。 在執行階段的高輸送量作業不應依賴在 hello 身分識別登錄中執行作業。 例如，傳送命令之前，先檢查裝置 hello 連線狀態不支援的模式。 請確定 toocheck hello[節流速率][ lnk-quotas] hello 身分識別登錄及 hello[裝置活動訊號][ lnk-guidance-heartbeat]模式。

## <a name="disable-devices"></a>停用裝置

您可以藉由更新 hello 停用裝置**狀態**hello 身分識別登錄中的身分識別的屬性。 您通常會在兩種情況下使用此屬性：

* 在佈建協調程序期間。 如需詳細資訊，請參閱[裝置佈建][lnk-guidance-provisioning]。
* 如果因為任何原因，您認為裝置遭到入侵，或變成未經授權。

## <a name="import-and-export-device-identities"></a>匯入和匯出裝置身分識別

您也可以使用非同步作業上 hello 從 IoT 中樞的身分識別登錄，匯出大量裝置身分識別[IoT 中樞資源提供者端點][lnk-endpoints]。 匯出是長時間執行從 hello 身分識別登錄讀取使用客戶所提供的 blob 容器 toosave 裝置身分識別資料的工作。

您可以使用非同步作業上 hello 匯入裝置身分識別在大量 tooan IoT 中樞的身分識別登錄中， [IoT 中樞資源提供者端點][lnk-endpoints]。 匯入而使用客戶所提供的 blob 容器 toowrite 裝置身分識別資料中的資料，到 hello 身分識別登錄的長時間執行作業。

* 如需 hello 匯入和匯出應用程式開發介面的詳細資訊，請參閱[IoT 中樞資源提供者 REST Api][lnk-resource-provider-apis]。
* 執行有關的詳細資訊匯入和匯出工作，請參閱的 toolearn[大量的 IoT 中樞裝置身分識別管理][lnk-bulk-identity]。

## <a name="device-provisioning"></a>裝置佈建

給定的 IoT 解決方案儲存 hello 裝置資料 hello 的該方案的特定需求而定。 但是解決方案至少必須儲存裝置身分識別和驗證金鑰。 Azure IoT 中樞包含身分識別登錄，其可以儲存每個裝置的值，例如識別碼、驗證金鑰和狀態碼。 解決方案可以使用其他 Azure 服務，例如資料表儲存體、 blob 儲存體或 Cosmos DB toostore 任何其他裝置的資料。

*裝置佈建*是 hello 程序在您的方案中加入 hello 初始裝置資料 toohello 存放區。 tooenable 新裝置 tooconnect tooyour 中樞，您必須新增裝置識別碼和金鑰 toohello IoT 中樞身分識別登錄。 Hello 佈建程序的一部分，您可能需要其他的方案存放區中的 tooinitialize 裝置的特定資料。

## <a name="device-heartbeat"></a>裝置活動訊號

hello IoT 中樞身分識別登錄包含名為的欄位**connectionState**。 只使用 hello **connectionState**欄位在開發和偵錯。 IoT 解決方案不應該在執行階段查詢 hello 欄位。 例如，不會查詢 hello **connectionState**欄位 toocheck 如果裝置傳送 SMS 或雲端到裝置訊息之前，先連線。

如果您的 IoT 解決方案需要 tooknow，如果裝置連線，您應該實作 hello*活動訊號模式*。

在 hello 活動訊號模式中，hello 裝置傳送裝置到雲端訊息至少一次每個固定的 （例如，至少一次每小時） 的時間量。 因此，即使裝置沒有任何資料 toosend，它仍會傳送空的裝置到雲端訊息 （通常會有這種屬性識別為活動訊號）。 Hello 服務端，hello 方案會針對每個裝置收到 hello 上次活動訊號與維護對應。 如果 hello 方案從 hello 裝置 hello 預期時間內未收到活動訊號訊息，則會假設沒有發生 hello 裝置。

更複雜的實作可能包含來自 hello 資訊[作業監視][ lnk-devguide-opmon]嘗試 tooconnect 或通訊的 tooidentify 裝置但失敗。 當您實作 hello 活動訊號模式時，請確定 toocheck [IoT 中樞配額與節流閥][lnk-quotas]。

> [!NOTE]
> 如果 IoT 解決方案會使用 hello 連接狀態而單獨 toodetermine 是否 toosend 雲端到裝置訊息，而且訊息已經不廣播 toolarge 設定的裝置，請考慮使用簡單的 hello*簡短到期時間*模式。 此模式不會達到相同結果與維護裝置連線狀態登錄使用 hello 活動訊號模式，同時會更有效率的 hello。 如果您要求訊息收條，IoT 中樞會通知您相關的裝置是無法 tooreceive 訊息，並不是。

## <a name="device-lifecycle-notifications"></a>裝置的生命週期通知

IoT 中樞在裝置身分識別建立或刪除時，可透過傳送裝置的生命週期通知，以通知 IoT 解決方案。 toodo 因此，您的 IoT 解決方案需要 toocreate 路由和 tooset hello 資料來源等太*DeviceLifecycleEvents*。 根據預設，不會傳送任何生命週期通知，亦即沒有預先存在的這類路由。 hello 通知訊息包含屬性和內文。

屬性： 訊息系統屬性前面會加上 hello`'$'`符號。

| 名稱 | 值 |
| --- | --- |
$content-type | application/json |
$iothub-enqueuedtime |  傳送嗨通知時間 |
$iothub-message-source | deviceLifecycleEvents |
$content-encoding | utf-8 |
opType | **createDeviceIdentity** 或 **deleteDeviceIdentity** |
hubName | IoT 中樞名稱 |
deviceId | Hello 裝置識別碼 |
operationTimestamp | 作業的 ISO8601 時間戳記 |
iothub-message-schema | deviceLifecycleNotification |

本文： 本章節的 JSON 格式，並代表 hello 兩個的 hello 建立裝置身分識別。 例如，

```json
{
    "deviceId":"11576-ailn-test-0-67333793211",
    "etag":"AAAAAAAAAAE=",
    "properties": {
        "desired": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        },
        "reported": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        }
    }
}
```

## <a name="reference-topics"></a>參考主題：

hello 下列參考主題提供您有關 hello 身分識別登錄的詳細資訊。

## <a name="device-identity-properties"></a>裝置身分識別屬性

裝置身分識別被以 JSON 文件以 hello 下列屬性：

| 屬性 | 選項 | 說明 |
| --- | --- | --- |
| deviceId |必要，只能讀取更新 |ASCII 7 位元的英數字元的區分大小寫字串 （向上 too128 字元） + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`。 |
| generationId |必要，唯讀 |IoT 中樞產生、 區分大小寫的字串 too128 字元組成。 這個值是使用的 toodistinguish 裝置 hello 相同**deviceId**，當它們已經刪除並重新建立。 |
| etag |必要，唯讀 |表示弱式 ETag hello 裝置身分識別，做為每個字串[RFC7232][lnk-rfc7232]。 |
| auth |選用 |包含驗證資訊和安全性資料的複合物件。 |
| auth.symkey |選用 |包含主要和次要金鑰 (以 base64 格式儲存) 的複合物件。 |
| status |必要 |存取指示器。 可以是 [已啟用] 或 [已停用]。 如果**啟用**，且允許 tooconnect hello 裝置。 如果為 [已停用] ，此裝置無法存取任何裝置面向的端點。 |
| statusReason |選用 |128 字元長時間的字串存放區 hello 因此 hello 裝置身分識別的狀態。 允許所有 UTF-8 字元。 |
| statusUpdateTime |唯讀 |顯示 hello 日期和時間的最後一個狀態更新 hello 時態指標。 |
| connectionState |唯讀 |指出連線狀態的欄位︰**已連線**或**已中斷連線**。 此欄位會顯示 hello IoT 中樞角度 hello 裝置連接狀態。 **重要事項**：此欄位只應用於開發/偵錯用途。 hello 連線狀態會更新僅適用於使用 MQTT 或 AMQP 的裝置。 此外，它是以通訊協定層級的偵測 (MQTT 偵測或 AMQP 偵測) 為基礎，而且最多只能有 5 分鐘的延遲。 基於這些理由，其中可能會有誤判的情形，例如將裝置回報為已連線，但卻已中斷連線。 |
| connectionStateUpdatedTime |唯讀 |已更新時態的指標，並顯示 hello 日期和最後一個階段 hello 連線狀態。 |
| lastActivityTime |唯讀 |暫時的指標，並顯示 hello 日期和最後一個時間 hello 裝置連線、 收到，或已傳送訊息。 |

> [!NOTE]
> 連接狀態只能表示 hello IoT 中樞角度 hello hello 連線狀態。 更新 toothis 狀態可能會延遲，視網路狀況和組態而定。

## <a name="additional-reference-material"></a>其他參考資料

Hello IoT 中樞開發人員指南 》 中的其他參考主題包括：

* [IoT 中樞端點][ lnk-endpoints]描述 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。
* [節流和配額][ lnk-quotas]描述 hello 配額和節流套用 toohello IoT 中心服務的行為。
* [Azure IoT 裝置和服務 Sdk] [ lnk-sdks]清單 hello 各種語言互動的裝置和服務應用程式開發與 IoT 中樞時，您可以使用的 Sdk。
* [IoT 中樞的查詢語言][ lnk-query]描述 hello 查詢語言，您可以使用您的裝置雙和作業相關的 tooretrieve 資訊從 IoT 中樞。
* [IoT 中樞 MQTT 支援][ lnk-devguide-mqtt] hello MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。

## <a name="next-steps"></a>後續步驟

現在您已經學會如何 toouse hello IoT 中樞身分識別登錄，您可能會想要遵循 IoT 中樞開發人員指南主題 hello:

* [控制存取 tooIoT 中樞][lnk-devguide-security]
* [使用裝置雙 toosynchronize 狀態和組態][lnk-devguide-device-twins]
* [在裝置上叫用直接方法][lnk-devguide-directmethods]
* [排程多個裝置上的作業][lnk-devguide-jobs]

如果您想要查看這篇文章中所述的 hello 概念 tootry，您可能想要遵循 IoT 中樞教學課程中的 hello:

* [開始使用 Azure IoT 中樞][lnk-getstarted-tutorial]

<!-- Links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-guidance-provisioning]: iot-hub-devguide-identity-registry.md#device-provisioning
[lnk-guidance-heartbeat]: iot-hub-devguide-identity-registry.md#device-heartbeat
[lnk-rfc7232]: https://tools.ietf.org/html/rfc7232
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-export]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-devguide-opmon]: iot-hub-operations-monitoring.md

[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
